# Paper 07 (NORMAL / experimental): Structural auxiliary supervision for OCR of low-legibility handwritten answers

**Authors:** Shrey Chandola, Manikandan Ravikiran, Rohit Saluja (IIT Mandi; Thoughtworks AI Labs; BharatGen, India)

---

## 1. Venue info

| Item | Details |
|---|---|
| Publisher | Elsevier |
| Journal | **Array**, Vol 31 (2026), 101051 |
| Dates | Received 28 Dec 2025, accepted 26 Jun 2026, online 2 Jul 2026 |
| Access | Open access (CC BY) |
| Impact factor | সূত্রভেদে ভিন্ন: **~4.5 (2025)**, ~5.3 (2026 release), আরেকটায় ~8.1। তাই "প্রায় 4.5–5.3, verify" বলাই নিরাপদ |
| Quartile | **Q1** (aggregator-এর JCR record ও Scimago "Computer Science (miscellaneous)") |
| Scopus | CiteScore ~10, SJR ~1.26 |
| A*? | না (journal) |

---

## 2. Paper কী করেছে (সহজ ভাষায়)

**সমস্যা:** স্কুলের ছাত্রদের খারাপ হাতের লেখা (অক্ষর জোড়া লাগা, বাঁকা, overlapping) থেকে single-word cloze answer পড়া। TrOCR-এর মতো model এতে বেশি ভুল করে।

**Idea:** TrOCR (ViT encoder + text decoder) fine-tune করার সময় একটা **অতিরিক্ত কাজ (auxiliary task)** দেওয়া: decoder প্রতিটা step-এ ওই অক্ষরের **stroke-direction signature** predict করবে।
- প্রতি অক্ষরের জন্য হাতে বানানো **32-bit code** = সর্বোচ্চ **8 ধাপ × 4 দিক** (Up, Down, Left, Right, one-hot)। যেমন `a`: ← ↓ → ↑ ↓ →।
- Loss: **L = L_CE + λ·L_struct** (binary cross-entropy), **λ = 0.05**।
- Structural loss শুধু **training-এ**; inference আগের মতোই (কোনো বাড়তি খরচ নেই)।
- Loss লাগানো হয় তিনটা decoder layer-এ (L/3, 2L/3, L), নাম "**Multi**"।

**Fig. 1:** খারাপ লেখার নমুনা। **Fig. 2:** architecture (encoder → decoder → LM head + structural head)। **Fig. 3:** একটা অক্ষর থেকে 32-bit code বানানো। **Fig. 4:** ৬টা difficulty group। **Fig. 5:** group অনুযায়ী error কমা। **Fig. 6:** decoder layer ablation। **Fig. 7:** ভালো/খারাপ উদাহরণ।

### Dataset
- **3000 word image** (English single word, cloze answer), 2400 train / 600 test; train থেকে 10% validation (seed 42)।
- ৬টা difficulty group × 500 image (Group 1 সহজ, Group 6 কঠিন)।
- ⚠️ Split **image-level**; writer-disjoint নয় (একই ছাত্রের লেখা train ও test-এ থাকতে পারে)।

### Results (Table 2 থেকে)

| Model | CER (CE only) | CER (Ours) | WER (CE only) | WER (Ours) |
|---|---|---|---|---|
| TrOCR-Small | 4.31 | 3.82 | 8.50 | 7.50 |
| TrOCR-Base | 3.70 | 2.71 | 8.08 | 5.91 |
| TrOCR-Large | 2.89 | **1.69** | 7.00 | **4.58** |

- Zero-shot ভীষণ খারাপ: Tesseract CER 77.5%, Google Vision 23.45%, Qwen2-VL-7B 24.17%, TrOCR-Large 31.5%।
- CTC auxiliary loss দিলে result **খারাপ** হয় (Large 3.52%)।
- Exact-match accuracy: 95.42% vs 93.00%; **McNemar p = 0.016**; paired bootstrap significant।
- Random code assignment (8 seed) CER 2.66±0.36, মানে হাতে বানানো code ভালো (1.69)।
- সব layer-এ loss দিলে খারাপ (CER 3.00)।
- Error analysis: ছোট/মাঝারি শব্দে বেশি উন্নতি, 10+ অক্ষরের শব্দে প্রায় সমান (2.94 → 2.90)।
- **IAM, CVL:** উন্নতি খুব সামান্য (2.14→2.08, 2.75→2.50)।
- Cross-dataset (IAM/CVL-এ train, bad-handwriting-এ test): IAM 22.11→22.03; CVL 54.13→28.34, অসামঞ্জস্যপূর্ণ।

---

## 3. Online-এ পাওয়া যায় কিনা? (এই paper-এর বড় সুবিধা)
- **Dataset:** ✅ Zenodo: `doi.org/10.5281/zenodo.18851954` (CC BY 4.0) এবং GitHub `Shrey0900/ClozeFormHandwriting`।
- **Code:** ✅ GitHub `Shrey0900/structural-supervision-htr` (MIT license), training/inference/metric script সহ।
- Base model: TrOCR (HuggingFace `transformers`), সহজলভ্য।
- 👉 তুমি নিজে চালিয়ে দেখতে পারো এবং নিজের C-code handwriting data দিয়ে adapt করতে পারো।

## 4. Critical observations / Gap
1. **Single English word** শুধু, বাক্য/code নয়। C code-এ `{ } ( ) ; * & # % ->`, indentation, multi-line আছে, আর code-এর 32-bit stroke code শুধু **Latin letter**-এর জন্য, symbol-এর জন্য নেই।
2. **Code হাতে বানানো** ও coarse (শুধু ৪ দিক, ≤8 step, loop/diagonal নেই)। Random-এর চেয়ে ভালো, কিন্তু "সেরা" প্রমাণ হয়নি (paper নিজেই স্বীকার করেছে)।
3. **Writer-disjoint test নেই:** same writer leak থাকলে সংখ্যা বেশি দেখাতে পারে।
4. **Test set মাত্র 600**; 1% WER ≈ 6 শব্দ। প্রধান ফলাফল প্রায় একটাই run (শুধু random control-এ 8 seed)।
5. কোনো classical preprocessing (slant correction, denoise) তুলনা করেনি।
6. Token-to-character alignment heuristic; M = 8 cap।
7. Autoregressive decoding-এ শুরুর ভুল ছড়ায় (long word দুর্বল; Fig. 7: "Zoological" → "biological")।
8. Fig. 7-এ regression-ও আছে (Emulator → Simulator, Neutron → Xenotron), মানে সবসময় ভালো করে না।
9. Grading-এর সাথে সংযোগ নেই: OCR-এর পরে answer check/grade হয় না, শুধু recognition মাপা।

## 5. TRACE-এর জন্য ব্যবহার
- ✅ **সবচেয়ে কাছের paper:** classroom handwritten student answer + TrOCR fine-tuning + খারাপ লেখা।
- ✅ Dataset ও code open, baseline হিসেবে নেওয়া যায়।
- ✅ Idea adapt: C code-এর জন্য **token-aware বা syntax-aware auxiliary loss** (keyword, bracket matching, indentation) একটা নতুন contribution হতে পারে।
- ❗ Gap: handwritten **C code**-এর OCR, **OCR → grading** end-to-end, OCR error কীভাবে নম্বর বদলায় তার বিশ্লেষণ।

## 6. My notes (নিজে লেখো)
- সমস্যা:
- Idea (stroke code, loss):
- Dataset/code link:
- Results:
- Weakness:
- TRACE-এ কীভাবে ব্যবহার করব:
- Questions for supervisor:

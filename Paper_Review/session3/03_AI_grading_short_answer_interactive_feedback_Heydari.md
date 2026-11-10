# Paper 03 (NORMAL / experimental): AI-Based Automated Grading of Short Answer Responses with Interactive Feedback

**Authors:** Ali Heydari, Saeed Alkendi, Sauleh Eetemadi (School of Computer Science, University of Birmingham, UK)

---

## 1. Venue info

| Item | Details |
|---|---|
| Publisher | Elsevier |
| Series | Procedia Computer Science, Vol 275 (2026), pp 716–723 |
| Event | ACLing 2025: 7th International Conference on AI in Computational Linguistics |
| Impact factor | Procedia CS-এর প্রকৃত JCR IF নেই (proceedings) |
| Scopus metrics | CiteScore ~3, SJR ~0.5 (পুরোনো aggregator figure) |
| Quartile | **Q1 নয়**, সর্বোচ্চ Q2 (verify করো) |
| A*? | না। ACLing-এর CORE rank পাইনি |

> Reference [6] (RATAS) এখনো "Manuscript in preparation", মানে একটা গুরুত্বপূর্ণ citation যাচাই করা যায় না।

---

## 2. Paper কী করেছে (সহজ ভাষায়)

**সমস্যা:** Short-answer exam হাতে grade করা ধীর, grader-ভেদে অসঙ্গত, feedback দিতে দেরি।
**ধারণা:** দুটো আলাদা pipeline বানিয়ে তুলনা:

1. **Local pipeline:** একটা fine-tuned **GPT-2**, response → score দেয়। ইন্টারনেট লাগে না, privacy ভালো, খরচ প্রায় শূন্য।
2. **API pipeline:** **GPT-4o Vision** দিয়ে scanned exam OCR ও structure বের করা, তারপর **LLaMA-2 / LLaMA-3.1 (Groq)** দিয়ে grade + **RAG** দিয়ে feedback (rubric ও model answer থেকে top 2–3 passage retrieve করে)।

**Fig. 1:** Data → image processing/retrieval → LLM (with/without API) → Evaluator → score + feedback; RAG loop evaluator থেকে retrieval-এ ফিরে আসে।

### Data
- Course: *Current Topics in Data Science*, দুটো exam: 33 + 31 = **64 student paper (256 page)**।
- Scanned PDF → image → **GPT-4o Vision OCR** → question structure → official grade sheet-এর সাথে align।
- Student-দের **explicit consent** আছে, anonymized। **একজন instructor** ground truth দিয়েছেন।

### Model/training
- GPT-2 loss: **L = 0.7·L_LM + 0.3·L_score** (λ = 0.7), language modeling + score MSE।
- Split: 70/15/15 (শুধু GPT-2-এর জন্য)। API model: zero/few-shot, **পুরো dataset-এ** evaluate।
- Prompt: LLaMA-কে "flexible, alternative solution গ্রহণ করো"; GPT-4o-কে "STRICT but FAIR, পূর্ণ নম্বর শুধু COMPLETELY correct হলে", JSON output।

### Results (সংখ্যা মনে রাখো)

| Model | R² | MAE | RMSE | κ (Cohen) | Time/script | Cost/script |
|---|---|---|---|---|---|---|
| Offline GPT-2 | 0.895 | 0.42 | 0.54 | 0.78 | 1.8s | $0 |
| GPT-4o + LLaMA-2 | 0.920 | 0.35 | 0.48 | 0.82 | 12s | $0.15 |
| Groq LLaMA-3.1 | 0.910 | 0.37 | 0.50 | 0.81 | 6.5s | $0.10 |

- Within ±0.5 নম্বর: 68% / 72% / 70%; within ±1.0: 90% / 93% / 92%।
- Feedback quality (3 rater, 1–5 scale, Fleiss κ = 0.75): GPT-4o 4.3/4.5/4.4 (specificity/groundedness/helpfulness) বনাম GPT-2 3.2/3.4/3.3।
- Throughput: GPT-2 ~2000 scripts/hour, GPT-4o ~300/hour।
- **Conclusion:** hybrid ভালো (সহজ প্রশ্নে local, জটিলে API); high-risk exam-এ human verification।

---

## 3. Online-এ পাওয়া যায় কিনা?
- **Dataset:** public না (student privacy/consent)।
- **Code:** paper-এ code/GitHub link **নেই**।
- **Training hyperparameter** (learning rate, batch size, epoch) paper-এই নেই, তাই reproducible না।
- Model: GPT-2, LLaMA, GPT-4o সব available, কিন্তু তাদের pipeline নিজে বানাতে হবে।

---

## 4. Critical observations (supervisor-কে দেখানোর মতো)
1. **তুলনা সমান নয়:** GPT-2 শুধু ~15% test split-এ (প্রায় ১০টা paper) মাপা হয়েছে, কিন্তু API model-গুলো **পুরো ৬৪ paper-এ**। তাই R²/MAE সরাসরি তুলনা করা ঠিক না।
2. **খুব ছোট dataset** (64), একটা course, একজন grader। Model আসলে instructor-এর bias শিখছে কিনা বোঝা যায় না (paper নিজেই বলেছে)।
3. **OCR error মাপা হয়নি** (GPT-4o Vision), অথচ পুরো pipeline OCR-এর উপর নির্ভর করে। এটা TRACE-এর জন্য সরাসরি relevant।
4. "Calibration analysis showed minimal bias" বলা হয়েছে, কিন্তু কোনো figure/table নেই।
5. Paper-এর মধ্যে "Note: specific hyperparameters were not detailed in the source material" ধরনের বাক্য আছে, যা সম্পাদনার অসতর্কতা বা AI-সহায়তার চিহ্ন হতে পারে (সন্দেহ, প্রমাণ না)।
6. Prompt বদলালে result কেমন বদলায় (sensitivity) পরীক্ষা করেনি।
7. Task: নিয়মিত English short answer (Data Science), **code নয়**।

## 5. Findings সংক্ষেপে
- API + RAG: feedback quality ও জটিল উত্তরে ভালো; কিন্তু ধীর ও খরচ বেশি।
- Local GPT-2: দ্রুত ও সস্তা, score ঠিকঠাক, feedback দুর্বল।
- Efficiency বনাম quality-র trade-off পরিষ্কার।

## 6. TRACE-এর জন্য Gap / ব্যবহার
- ✅ **Scanned handwritten exam → OCR → grade** pipeline-এর সরাসরি উদাহরণ (GPT-4o Vision ব্যবহার করে)।
- ✅ Hybrid (local + API) ও privacy নিয়ে চিন্তা, তোমার deployment decision-এ কাজে লাগবে।
- ✅ RAG দিয়ে rubric/model answer থেকে grounding।
- ❗ Gap: **code না**, শুধু prose। C code-এ syntax, indentation, `{ } ; * &` চিহ্ন OCR-এ অনেক কঠিন।
- ❗ OCR error → grading error-এর প্রভাব কেউ মাপেনি।
- ❗ Partial credit ও rubric (compile ঠিক, logic ভুল ইত্যাদি) এখানে নেই।

## 7. My notes (নিজে লেখো)
- কী সমস্যা সমাধান করছে:
- Method:
- Dataset/availability:
- Results:
- Weakness:
- TRACE-এ কীভাবে ব্যবহার করব:

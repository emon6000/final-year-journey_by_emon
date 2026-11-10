# Paper 05 (REVIEW): Large Language Model-Powered Automated Assessment: A Systematic Review

**Author:** Emrah Emirtekin (Ege University, Izmir, Turkey), একক লেখক
**Type:** Systematic review (PRISMA), 49 studies, 2018 – Oct 2024

---

## 1. Venue info

| Item | Details |
|---|---|
| Publisher | MDPI |
| Journal | Applied Sciences, 2025, 15(10), 5683 |
| Dates | Received 14 Apr 2025, accepted 12 May 2025, published 20 May 2025 |
| Access | Open access (CC BY) |
| Impact factor | 2024 JIF **2.5**; 2025 JIF ~**2.9** (aggregator, JCR 2026 release) |
| JCR quartile | **Q2** (Engineering, Multidisciplinary); কিছু বিভাগে Q3 |
| Scopus | CiteScore ~5.3–5.5; MDPI-র নিজের flyer অনুযায়ী CiteScore **Q1 (General Engineering)** |
| A*? | না |

> Applied Sciences বড় multidisciplinary MDPI journal (বছরে হাজার হাজার paper), তাই selectivity নিয়ে কিছু academic সমালোচনা আছে। "Q1/Q2" বলার সময় কোন category আর JCR না Scopus সেটা বলো।

---

## 2. Section-by-section সারাংশ

### Abstract
- LLM-Powered Automated Assessment (**LLMPAA**) = AES (essay scoring) + ASAG (short answer grading) যেখানে LLM ব্যবহার হয়।
- 49 paper; Web of Science, Scopus, IEEE, ACM, PubMed।
- ব্যবহার: reading comprehension, language education, computer science। কিছু paper-এ human-এর সাথে খুব ভালো agreement (QWK 0.99, r 0.95), কিছুতে কম (ICC 0.45, r 0.38)।
- Benefit: efficiency, scalability, personalized feedback। Challenge: bias, inconsistency, hallucination, explainability, dataset quality, privacy। **Human oversight জরুরি**।

### 1. Introduction (page 1–2)
- Objective প্রশ্ন (MCQ) সহজে grade হয়, কিন্তু subjective (essay, open-ended) প্রশ্ন শেখার জন্য ভালো।
- Automated scoring সবসময় bias কমায় না, বরং কখনো বাড়ায়।
- 3 RQ: **RQ1** কোন domain-এ? **RQ2** কীভাবে (dataset, model, metric)? **RQ3** কী চ্যালেঞ্জ?

### 2. Methods (page 2–3)
- PRISMA, protocol **OSF-এ pre-registered** (ভালো practice)।
- 2018 বেছেছে কারণ BERT ওই বছর এসেছে।
- **Fig. 1 (PRISMA):** 816 → duplicate 219 বাদ → 597 → abstract screening-এ 537 বাদ → 60 → full text-এ 11 বাদ (8টা LLM নয়, 2টা literature review, 1টা full text নেই) → **49**।
- Database: WoS 287, Scopus 142, IEEE 49, ACM 161, PubMed 177।

### 3.1 Usage domains — Table 4 (49 study-র dataset list)
- Reading comprehension **14**, Language education **13**, Computer science **10**, Medical **5**, Writing **5**। Math/physics/chemistry খুব কম।

### 3.2 Details
- **Datasets:** নিজে বানানো (SELF) **23**; ASAP-AES **11**; MOHLER (CS short answer) **4**।
- **Question type:** Essay 30, Short-answer 16, Open-ended 3।
- **Language:** 67% English, বাকি 33% অন্য ভাষা (Spanish, Japanese, Arabic, Chinese, Indonesian...)। English-নির্ভরতা non-native student-এর জন্য অন্যায্য হতে পারে।
- Dataset size 3 থেকে 37,346 পর্যন্ত বড় variation।
- **Model ও metric (Table 5):** BERT ও variants সবচেয়ে বেশি; GPT-4 ও fine-tuned BERT সেরা। তিন ধরনের metric:
  1. Performance: accuracy (7), F1 (2), precision (2), recall (1)
  2. Human agreement: **QWK (18)**, Cohen's κ (5), LWK (1), correlation r (16)
  3. Reliability: ICC (6)
- QWK-তে: 40% excellent (0.81–1.00), 33% good, 20% moderate। Correlation-এ: 91% strong (≥0.70), একটা দুর্বল (r 0.30–0.50)।
- উদাহরণ: GPT-4 (Bui & Barrot) weak correlation; GPT-4 (Pack) ICC 0.927 (ভালো consistency)।
- ⚠️ "LLM" এখানে BERT, ALBERT, LSTM-মিশ্র model-ও ধরেছে, সব generative LLM না।

### 3.3 Challenges (7টা)
1. **Bias/fairness:** non-native বা ভিন্ন ভাষাভাষী ছাত্রের কম নম্বর; উচ্চ risk।
2. **Consistency:** LLM probabilistic, temperature বদলালে result বদলায়; prompt/fine-tune সাহায্য করে।
3. **Dataset quality:** ছোট/imbalanced/অ-বৈচিত্র্যময় dataset।
4. **Explainability:** "black box"; ছাত্র আপত্তি করলে কারণ দেখানো কঠিন; rubric-based approach সাহায্য করে।
5. **Hallucination:** essay-তে নেই এমন জিনিস আছে ধরে নেওয়া।
6. **Language/human traits:** সূক্ষ্মতা, creativity ধরতে পারে না; কখনো বেশি নম্বর দেয় (Kortemeyer: physics-এ GPT-4 বেশি দেয়)।
7. **Privacy/security:** ChatGPT/Gemini-তে student data বাইরের server-এ যায়; সমাধান: local open-source LLM, federated learning, anonymization, GDPR।

### 4. Discussion & 5. Conclusion
- Physics/chemistry/math-এ কম গবেষণা (symbol, graph বোঝা কঠিন)।
- সমাধান: **hybrid human + AI, RLHF**, confidence score, review checkpoint।
- Claude 2 শুধু একটা paper-এ ছিল; নতুন model (Claude 3.5, Grok 3, DeepSeek-V3) পরে এসেছে, তাই পুনঃমূল্যায়ন দরকার।
- Ethics: OECD AI Principles, EU AI Act (education = "high-risk"), IEEE Ethically Aligned Design।
- Claim: workload কমে, কিন্তু cost কমে কিনা সন্দেহ (computing/fine-tuning খরচ)।

---

## 3. Figure/Table কী বোঝায়
- Fig. 1: 816 → 49 selection flow।
- Table 1–2: inclusion/exclusion ও search string।
- Table 3: database ভিত্তিক সংখ্যা।
- Table 4: ৪৯ study-র domain, dataset, language, size।
- Table 5: প্রতি study-র model, metric, result।

## 4. Critical observations (নিজের পর্যবেক্ষণ)
- **ছোট অসঙ্গতি:** Bui & Barrot-এর correlation Table 5-এ r = 0.382, কিন্তু discussion-এ r = 0.359। QWK study-র সংখ্যা এক জায়গায় 18, আরেক জায়গায় 15।
- Table 4-এ কিছু "Additional Info" copy-paste ভুল মনে হয় (একই "grades 7–10 in USA" বিবরণ অন্য dataset-এ)।
- Human-agreement-ই মূল মাপকাঠি ধরা হয়েছে, human grader নিজে নির্ভরযোগ্য কিনা প্রশ্ন নেই।
- Computer science (10 study) আছে কিন্তু বেশিরভাগ **short-answer text**, programming code না।

## 5. TRACE-এর জন্য Gap / ব্যবহার
- ✅ Metric guide: **QWK, Cohen's κ, ICC, r** এর ব্যবহার ও মানের ব্যাখ্যা (0.81+ excellent), তোমার evaluation-এ কাজে লাগবে।
- ✅ Privacy ও local deployment যুক্তি (বাংলাদেশের university exam data)।
- ✅ Bias, explainability, hallucination, rubric-based grading তোমার "limitations/risks" section-এর ভিত্তি।
- ❗ **Handwritten input একদমই নেই**; সব typed text।
- ❗ Code grading, C language নেই।
- ❗ Bangla/Bangladesh context নেই; non-English শুধু ভাষা হিসেবে আছে।

## 6. My notes (নিজে লেখো)
- Abstract/Intro:
- Method (816→49):
- Domains/datasets:
- Models & metrics:
- 7 challenges:
- Discussion:
- Questions for supervisor:

# Paper 02 (REVIEW): AI-based automated grading in higher education: A scoping review and landscape analysis for sustainable education

**Authors:** Yelmar Orazbek, Yerlan Shildibekov, Aigerim Balkenova (International Information Technologies University, Almaty, Kazakhstan)
**Type:** Scoping review (PRISMA-ScR), 72 studies, Scopus only. পুরো paper ছোট (মাত্র 6 page: 902–907)

---

## 1. Venue info

| Item | Details |
|---|---|
| Publisher | Elsevier |
| Series | Procedia Computer Science, Vol 290 (2026), pp 902–907 |
| Event | 1st International Workshop on Digital Intelligence for Sustainable Development (DI4SD), 18–20 Aug 2026, Athens |
| Type | **Workshop proceedings**, regular journal না |
| Impact factor | Procedia CS-এর নিজস্ব কোনো প্রকৃত JCR impact factor নেই (proceedings series) |
| Scopus metrics | CiteScore ~3, SJR ~0.5 (পুরোনো figure, aggregator থেকে) |
| Quartile | **Q1 নয়।** সর্বোচ্চ Q2 (Computer Science), কিছু উৎসে best quartile দেওয়াই নেই। verify করো |
| A*? | না। DI4SD নতুন workshop, CORE ranking পাইনি |
| License | CC BY-NC-ND |

> ⚠️ Supervisor-কে সৎভাবে বলো: এটা workshop-level paper, তাই এর evidence শক্তি কম। Quartile ও score Scimago/Scopus থেকে নিজে confirm করো।

---

## 2. Section-by-section সারাংশ

### Abstract
- Higher education-এ assessment-এর চাপ বাড়ছে; AI automated grading-এর সম্ভাব্য সমাধান কিন্তু ক্ষমতা/সীমা অস্পষ্ট।
- Scopus থেকে **72 study** map করেছে: AI technique, assessment task, metric, dataset।
- Findings: LLM এখন প্রধান; short-answer-এ ভালো; জটিল ও subjective assessment-এ দুর্বল; ছোট dataset, standardization-এর অভাব, fairness/reliability নিয়ে চিন্তা।

### 1. Introduction
- SDG 4 (Quality Education)-এর প্রেক্ষাপটে grading হতে হবে fair, timely, scalable, valid।
- Essay/short answer হাতে grade করা ধীর ও evaluator-ভেদে অসঙ্গত।
- আরেকটা সমস্যা: ছাত্ররা এখন AI দিয়ে উত্তর বানায়, তাই submission আরো বৈচিত্র্যময়।
- ইতিহাস: ML (essay scoring) → deep learning → LLM।
- তিনটা Research Question:
  - **RQ1** Landscape কী (model, task, evaluation)?
  - **RQ2** কতটা কার্যকর ও reliable?
  - **RQ3** সীমাবদ্ধতা ও gap কী?

### 2. Methodology
- Search: **শুধু Scopus**, 23 March 2026, title/abstract/keyword। Year 2013–2026।
- Records: **701 → 300 (title) → 130 (abstract) → 72 (full text)**।
- Include: AI দিয়ে grading + empirical result। Exclude: শুধু feedback, peer assessment, non-AI, যথেষ্ট detail নেই।
- Data extraction: AI type, task, domain, dataset size, metric, limitation ইত্যাদি।
- ChatGPT শুধু language editing-এ ব্যবহৃত (declared)।
- ⚠️ ভুল-বোঝা: "রেজিস্ট্রেশন/protocol" উল্লেখ নেই; দুইজন reviewer-এর agreement মাপার কথা নেই।

### 3.1 Overview
- 72 study; journal 43, conference 29; 39 দেশের affiliation; 16 multi-country।
- Funding তথ্য অসম্পূর্ণ।

### 3.2 Landscape
- **Table 1 (year × AI category):**
  - 2013–2017: শুধু "Other" (rule/non-standard)।
  - 2019–2022: ML ও DL প্রধান।
  - 2023: 3 (LLM 1)। 2024: 12 (LLM 9)। **2025: 41 (LLM 30)**। 2026: 6 (LLM 5)।
  - 👉 LLM-এর বিস্ফোরণ 2024–2025-এ।
- ⚠️ **ছোট একটা ভুল পেয়েছি:** Table 1-এর row যোগ করলে মোট হয় **73**, কিন্তু paper বলছে 72। (ছোট inconsistency, কিন্তু critical reading-এর উদাহরণ।)
- **Table 2 (task type):**

| Task | Count | % |
|---|---|---|
| Short answer | 32 | 44% |
| Essay | 19 | 26% |
| **Code** | **6** | **8%** |
| Numerical | 2 | 3% |
| Other/mixed | 13 | 18% |

### 3.3 Effectiveness
- **Table 3 (dataset size):** <500: 29 (40%); 500–5,000: 18 (25%); 5,000–50,000: 11 (15%); >50,000: 5 (7%); not reported: 9 (13%)। 👉 প্রায় অর্ধেক study ছোট dataset-এ।
- **Table 4 (metric):** Correlation 33, Agreement (Kappa) 33, Accuracy-based 24, Error (RMSE/MAE) 20, F1 14। একাধিক metric একসাথে, তাই sum আলাদা।
- Shared evaluation framework নেই, তাই তুলনা কঠিন।

### 3.4 Limitations / Gaps
1. ছোট/domain-specific dataset (40%)।
2. Evidence task-dependent: short-answer শক্ত, essay/code/numerical দুর্বল।
3. Result rubric, prompt, model config-এর উপর খুব নির্ভরশীল (reproducibility সমস্যা)।
4. Standard metric নেই।
5. Fairness, bias, transparency অবহেলিত (ভাষা, লেখার ধরন, background ভেদে ভিন্ন grade)।

### 4. Discussion
- ML/DL: ভালো যেখানে criteria স্থির, interpretable। LLM: flexible কিন্তু prompt sensitivity, model version পরিবর্তন, opacity।
- মূল trade-off: **semantic flexibility vs assessment reliability**।
- AI grading **সহায়ক (assistive) টুল**, মানুষের সম্পূর্ণ বিকল্প না।
- SDG 4: ভুল প্রয়োগ হলে inequality বাড়াতে পারে।

### 5. Conclusion
- Short-answer সবচেয়ে mature; essay, programming, numerical, project, multimodal কম validated।
- ভবিষ্যৎ: বড় dataset, standard protocol, fairness testing, real-world validation।

---

## 3. Figure/Table কী বোঝায়
- Table 1: সময়ের সাথে ML → DL → LLM-এর পরিবর্তন।
- Table 2: কোন ধরনের প্রশ্ন বেশি গবেষণা হয়েছে (code মাত্র 8%)।
- Table 3: dataset ছোট কিনা।
- Table 4: কোন metric বেশি ব্যবহার।
(কোনো সাধারণ figure নেই, শুধু table।)

## 4. TRACE-এর জন্য Gap / ব্যবহার
- ✅ সহজ প্রমাণ: **code grading-এ এখনো কম কাজ হয়েছে (6/72 = 8%)**। supervisor-কে এই সংখ্যা দেখাতে পারো।
- ✅ "ছোট dataset ও single-institution" সমস্যা তোমার নিজের dataset বানানোর যুক্তি দেয়।
- ❗ Handwriting, OCR, বা handwritten code নিয়ে **কিছুই নেই**।
- ⚠️ এই paper-এর নিজস্ব দুর্বলতা: শুধু Scopus, ছোট workshop paper, কোনো quality assessment নেই। সরাসরি "প্রধান উৎস" হিসেবে না, "সংখ্যার পটভূমি" হিসেবে ব্যবহার করো।

## 5. My notes (নিজে লেখো)
- Abstract:
- Intro:
- Method (701→72):
- Tables 1–4:
- Limitations:
- Discussion/Conclusion:
- Questions for supervisor:

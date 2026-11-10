# Paper 01 (REVIEW): A comparative analytical study of LLM-based automated grading in programming education

**Authors:** Abderazzak EL Mernissi, Fatima Lakrami, Hicham Toumi (Chouaib Doukkali University, Morocco)
**Type:** Review article (PRISMA-guided, 17 studies, 2023–2026)

---

## 1. Venue info

| Item | Details |
|---|---|
| Publisher | Elsevier |
| Journal | Social Sciences & Humanities Open, Vol 14 (2026), 103144 |
| Access | Open access (CC BY) |
| Published | Received 13 Jan 2026, accepted 19 Jun 2026, online 22 Jun 2026 |
| Impact factor | কোনো একক নির্ভরযোগ্য সংখ্যা পাইনি। Third-party site-গুলো ভিন্ন ভিন্ন সংখ্যা দেয় (একটায় ~4.3, আরেকটায় ~1.4 টাইপের), তাই **JCR/Scimago-তে নিজে check করো** |
| SJR (Scimago) | ~0.6–0.7 (সাইটভেদে ভিন্ন) |
| Quartile | Scimago-তে **Social Sciences এ Q1**, Decision Sciences/Psychology তে Q2 (একটি aggregator অনুযায়ী) |
| A*? | না। A* হলো conference ranking (CORE), journal-এর জন্য না |

> ⚠️ লক্ষ্য করো: এটা CS journal না, Social Science journal। তাই supervisor-কে বলার সময় "Q1 (Social Sciences category)" বলো, "Q1 CS" না। এই তথ্য web aggregator থেকে নেওয়া, final করার আগে Scimago (scimagojr.com) এ ISSN **2590-2911** দিয়ে verify করো।

---

## 2. Section-by-section সারাংশ

### Abstract
- LLM দিয়ে programming assignment grade করার গবেষণা অনেক, কিন্তু **methodology এলোমেলো (fragmented)**, তাই তুলনা করা কঠিন।
- ১৭টা peer-reviewed paper (2023–2026) PRISMA পদ্ধতিতে বিশ্লেষণ করেছে।
- ৫টা dimension এর একটা **taxonomy** বানিয়েছে: grading paradigm, LLM-এর role, human involvement, evaluation strategy, generalization scope। সাথে "level of evidence" ভাগ করেছে।
- মূল findings: fully automated grading সবচেয়ে বেশি; hybrid/human-supervised বাড়ছে; বেশিরভাগ paper শুধু **human grader-এর সাথে correlation/agreement** মাপে; cross-rubric ও pedagogical validation কম।

### 1. Introduction (page 1–3)
- হাতে programming assignment grade করা ধীর, subjective, scale করা কঠিন।
- Test-case based autograder partial correctness, alternative solution, student-এর intent ধরতে পারে না।
- LLM code-এর logic ও intent বুঝতে পারে, তাই আগ্রহ বাড়ছে।
- এই paper-এর সংজ্ঞা: automated grading = minimal/no human intervention-এ score/category দেওয়া।
- আগের review (Messer et al., 2024) পুরো autograding ecosystem দেখেছে, কিন্তু **LLM-specific methodological diversity** দেখেনি। এটাই এই paper-এর gap।
- ৫টা contribution: taxonomy, key dimensions, hidden assumptions, evidence-aware view, gaps।

### 2. Related Work (page 2–3)
গ্রেডিং-এর ৪টা ধাপের ইতিহাস:
1. **Rule/test-case based** (1990s–2000s): compile + run, শুধু output দেখে।
2. **Static analysis, MOOC scale** (2000s–2010s): Web-CAT, linter, plagiarism detection।
3. **ML / neural code models** (2010s–2020s): CodeBERT, GraphCodeBERT; fine-tuning দরকার।
4. **LLM grading** (2023–এখন): semantic বোঝে, rubric-based, feedback, human-AI collaboration।
- 2.1 Grading-কে binary, category, continuous score, rubric এই ভাবে ভিন্নভাবে define করা হয়।
- 2.2 Human involvement একটা **design choice**, শুধু সাময়িক সীমাবদ্ধতা না।
- 2.3 Evaluation: বেশিরভাগ agreement-based (correlation, MAE); equivalence testing (TOST) খুব কম।
- 2.4–2.5 আগের review-গুলো performance দেখেছে, **design choice কীভাবে result-কে প্রভাবিত করে** দেখেনি।

### 3. Methodology (page 3–5)
- Database: **Scopus + Web of Science** (ACM/IEEE-র বড় অংশ cover করে)।
- ৩টা query (A: core, B: expanded, C: feedback-grading intersection)। বছর 2023–2026, ভাষা English।
- **Fig. 1 (PRISMA flow):** 801 record → 320 duplicate বাদ → 481 → title/abstract-এ 394 বাদ → 87 full-text → **17 included** (12 journal + 5 conference)।
- Inclusion: LLM দিয়ে student-written code grade, programming education context, peer-reviewed, যথেষ্ট method detail। Exclusion: শুধু feedback/essay, code generation evaluation, preprint।
- দুইজন screen করেছে, তৃতীয়জন validate; **কোনো formal inter-rater coefficient (Kappa) বের করেনি**। এটা একটা দুর্বলতা।
- Taxonomy বানানো: open → axial → selective coding।
- Level of evidence: Exploratory pilot, Case study, Controlled experiment, Large-scale/comparative।

### 4. Taxonomy (page 5–6)
- **Fig. 2:** মাঝে taxonomy, চারপাশে ৫টা dimension (Grading Paradigm, Role of LLM, Human Involvement, Evaluation Strategy, Generalization Scope)।
- Coding scheme:
  - Paradigm: **Type I** binary, **II** category, **III** continuous score, **IV** rubric-based।
  - Human: **Level 0** fully automated, **1** human-on-the-loop, **2** human-in-the-loop।
  - Evaluation: agreement-based / accuracy-based / equivalence testing।
- **Table 1:** ১৭টা study-র প্রত্যেকটা এই dimension অনুযায়ী ভাগ করা। **Table 2:** কী evaluate হয়েছে, metric, hidden assumption, main limitation। **Table 3 (সংখ্যা):**

| Dimension | Count |
|---|---|
| Continuous score (Type III) | 8 (47.1%) |
| Rubric-based (Type IV) | 5 (29.4%) |
| Category (Type II) | 3 (17.6%) |
| Binary (Type I) | 1 (5.9%) |
| Fully automated (Level 0) | 10 (58.8%) |
| Human-in-the-loop (Level 2) | 5 (29.4%) |
| Human-on-the-loop (Level 1) | 2 (11.8%) |
| Agreement-based eval | 14 (82.4%) |

### 5. Comparative Discussion (page 6–9) — সবচেয়ে গুরুত্বপূর্ণ অংশ
মূল যুক্তি: **field সেই জিনিসটাই করছে যেটা মাপা সহজ, যেটা শেখার জন্য সবচেয়ে useful সেটা না।**
- 5.1 Continuous score সবচেয়ে বেশি, কারণ numeric grade আগে থেকেই আছে। কিন্তু ১ নম্বরের ভুল pass/fail সীমায় বিশাল, মাঝামাঝি জায়গায় তুচ্ছ।
- 5.2 শুধু paradigm না, **কীভাবে LLM চালানো হয়েছে** (prompt, fine-tune, hybrid) সেটাও performance ঠিক করে।
- 5.3 Rubric-based grading সবচেয়ে pedagogically ভালো, কিন্তু বানানো ও validate করা কঠিন, তাই কম।
- 5.4 Full automation কাজ করে যেখানে **domain সীমিত** (যেমন SQL)। এটা LLM-এর ক্ষমতা না, problem-এর গঠনের কারণে।
- 5.5 **Triage** (LLM সহজ case নেয়, মানুষ কঠিন case দেখে): এখানে score agreement ঠিক metric না; "কোন submission human-কে দেখাতে হবে" সেটা ঠিকমতো ধরছে কিনা মাপা উচিত। এটা কোনো paper মাপেনি।
- 5.6 Agreement metric ML-এর অভ্যাস। Educational measurement-এর Cohen's Kappa, Krippendorff's Alpha, pass/fail agreement, grade-boundary accuracy প্রায় কেউ ব্যবহার করেনি।
- 5.7 Validation সবই single course/exam/language, তাই শুধু **feasibility** দেখানো যায়, robustness না।

### 6. Research gaps (page 9–10)
1. "Automated grading" বলতে কী বোঝায় তার সাধারণ সংজ্ঞা নেই।
2. Agreement ছাড়িয়ে educational validation (inter-rater, decision-oriented) দরকার।
3. Scalable rubric-aware grading বাড়াতে হবে।
4. বহু course/language/longitudinal validation।
5. Human oversight-কে design variable হিসেবে মডেল করা (triage, selective review)।
6. Explainability, fairness, multimodal, sustainability।

### 7–8. Conclusion & Limitations
- Variation আসে methodology-র ভিন্নতা থেকে, বিপরীত result থেকে না।
- Fully automated: constrained task-এ; human-AI: যেখানে interpretability/accountability দরকার।
- Limitations: Scopus/WoS-এর বাইরের venue (AIED, EDM, L@S) miss হতে পারে; secondary analysis, নিজে replicate করেনি; কোনো model benchmark করেনি।

---

## 3. Figure/Table কী বোঝায় (দ্রুত)
- **Fig 1:** কীভাবে 801 → 17 paper বাছাই হলো।
- **Fig 2:** taxonomy-র ৫ dimension-এর overview।
- **Table 1:** ১৭ study × ৫ dimension + level of evidence।
- **Table 2:** metric + hidden assumption + limitation।
- **Table 3:** সংখ্যায় কোন choice কতবার।

## 4. TRACE-এর জন্য যা কাজে লাগবে / Gap
- ✅ তোমার TRACE-এর জন্য পরিষ্কার vocabulary: তুমি কোন paradigm (rubric-based Type IV?) আর কোন human level (triage?) নিচ্ছ সেটা বলতে পারবে।
- ✅ "Triage evaluation absent" ও "decision-oriented metric (pass/fail, grade boundary) absent" দুটো সরাসরি তোমার evaluation design-এ কাজে লাগবে।
- ❗ **এই review-এর ১৭টা study-র সবই typed/digital code grading। Handwritten code-এর কথা একবারও নেই।** এটা TRACE-এর সবচেয়ে বড় gap দাবি করার জায়গা (OCR error → grading error pipeline)।
- ❗ C language-specific কিছু নেই (Python, Java, SQL বেশি)।

## 5. My notes (নিজে লেখো)
- Abstract:
- Intro:
- Related work:
- Methodology:
- Taxonomy & figures:
- Discussion:
- Gaps:
- Questions for supervisor:

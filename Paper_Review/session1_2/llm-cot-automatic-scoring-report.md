# Reading Notes & Report: Applying Large Language Models and Chain-of-Thought for Automatic Scoring

**Paper Title:** Applying large language models and chain-of-thought for automatic scoring [1]  
**Authors:** Gyeong-Geon Lee, Ehsan Latif, Xuansheng Wu, Ninghao Liu, and Xiaoming Zhai [1]  
**Affiliations:** AI4STEM Education Center & School of Computing, University of Georgia, Athens, GA, USA [1]  
**Publication Venue:** _Computers & Education: Artificial Intelligence_, Volume 6 (2024), Article 100213 (Elsevier) [1]

---

## 1. Core Problem & Motivation

Automatic scoring systems in education—particularly in science assessment—have historically relied on supervised machine learning and natural language processing (NLP) techniques [10, 12]. While effective, traditional machine learning models present three major hurdles [10, 15]:

1. **Labor-Intensive Data Preparation:** Building an accurate scoring model typically requires collecting, manually scoring, and algorithmically processing thousands of student responses to train custom text classifiers or neural networks [10, 11].
2. **Technical Barriers for Educators:** Developing, fine-tuning, and ensembling complex models demands advanced programming and data science expertise, keeping these tools out of reach for general classroom teachers [13, 14].
3. **The "Black Box" Explainability Deficit:** Neural networks and abstract mathematical embeddings classify student answers without explaining _why_ a particular grade was assigned [15]. In educational settings, teachers and students require transparent, evidence-backed feedback to rectify scientific misconceptions [16].

Large Language Models (LLMs) like GPT-4 offer a way forward via **prompt engineering**, enabling automated scoring without retraining models from scratch [6, 7]. However, off-the-shelf LLMs frequently struggle with the domain-specific reasoning required by strict grading rubrics [6, 24]. This study investigates how combining LLMs with **Chain-of-Thought (CoT) prompting**, **contextual scoring rubrics**, and **structured prompt engineering** creates an accurate, explainable, and accessible automatic scoring workflow [2, 7].

---

## 2. Sequential System Architecture & The WRVRT Lifecycle

The authors introduce a structured, 5-stage iterative prompt development lifecycle called **WRVRT** (_Prompt Writing, Reviewing, Validating, Revising, and Testing_) [37]:

```
[1. Write Draft Prompt] ➔ [2. Expert Review (AI & Edu)] ➔ [3. Validate on Non-Test Cases]
                                      │                             │
                                      ▼                             ▼
                            [4. Revise Prompt Structure] ◄──────────┘
                                      │
                                      ▼
                            [5. Run Final Testing]
```

### The 5 Stages of WRVRT:

1. **Write:** Science and assessment experts construct an initial prompt specifying the AI's grading role, item context, scoring rubrics, and exemplar responses [37, 39].
2. **Review:** Experts in AI/LLMs and science education evaluate the prompt to ensure face validity and internal logical consistency [37, 38].
3. **Validate:** The prompt is tested against a small validation dataset of student responses (separate from the testing set) to evaluate external scoring reliability [37].
4. **Revise:** If validation reveals errors or structural drift, the prompt undergoes iterative revisions (the authors finalized their prompts after three revision cycles) [37, 38].
5. **Test:** The finalized prompt is deployed across the target dataset to compute scoring performance metrics against ground-truth human expert scores [37].

---

## 3. Prompt Building Blocks & Tested Strategies

To isolate what makes LLM scoring effective, the study disassembled prompts into **six structural components** [39]:

- **`BasicRole`:** System-level instruction designating the LLM's persona (e.g., _"Please act as an impartial science teacher..."_) [39].
- **`ContRubTEXT`:** The item stem provided to students alongside the explicit scoring rubric components (e.g., Component A, Component B) [39].
- **`FewEXAMPLES`:** Four exemplar student responses representing human-graded proficiency levels ('Proficient', 'Developing', 'Beginning') [39].
- **`CoT Initiator`:** A trigger mechanism that forces step-by-step reasoning. For zero-shot prompts, this is _"Let's think step by step"_; for few-shot prompts, it consists of human-written CoT explanations demonstrating how rubric components were identified [39, 41].

### Six Comparative Prompting Strategies Tested:

1. **`ZS_noCoT` (Zero-Shot Baseline):** `BasicRole` only, without CoT or rubric text [44].
2. **`ZS_CoT`:** `BasicRole` + zero-shot CoT trigger (_"Let's think step by step"_) [44].
3. **`ZS_CoT_CR`:** `BasicRole` + `ContRubTEXT` (Context & Rubric) + zero-shot CoT trigger [44].
4. **`FS_noCoT`:** `BasicRole` + 4 Few-Shot examples (without reasoning steps) [44].
5. **`FS_CoT`:** `BasicRole` + 4 Few-Shot examples containing human CoT explanations [44].
6. **`FS_CoT_CR`:** `BasicRole` + `ContRubTEXT` + 4 Few-Shot CoT examples (Full Context & Rubric) [44].

---

## 4. Experimental Setup & Empirical Findings

### Dataset Characteristics

- **1,650 Student Responses:** Drawn from middle school science assessments aligned with Next Generation Science Standards (NGSS MS-PS1-4: particle motion and thermal energy) [33].
- **Task Diversity:** 6 assessment items—3 binomial tasks (2 score tiers) and 3 trinomial tasks (3 score tiers: 'Beginning', 'Developing', 'Proficient') [33, 35].
- **Balanced Stratification:** Responses were randomly sampled to maintain equal representation across proficiency levels, preventing delusive accuracy from class imbalance [34].
- **Ground Truth:** Human expert agreement benchmarked at inter-rater reliability Cohen's $\kappa > 0.75$ [33].

### Key Performance Benchmarks:

| Prompting Strategy             | Average Accuracy | Relative Improvement vs. Baseline |
| :----------------------------- | :--------------: | :-------------------------------: |
| **`ZS_noCoT` (Baseline)**      |      0.5487      |                 -                 |
| **`ZS_CoT`**                   |      0.5532      |              +0.82%               |
| **`ZS_CoT_CR`**                |      0.6831      |            **+13.44%**            |
| **`FS_noCoT`**                 |      0.6604      |              +20.36%              |
| **`FS_CoT`**                   |      0.6515      |              -1.35%               |
| **`FS_CoT_CR` (Best Overall)** |    **0.6975**    |            **+14.88%**            |

#### Core Insights from the Results:

1. **Few-Shot Outperforms Zero-Shot:** Few-shot learning averaged **0.6698 accuracy** vs. **0.5950 for zero-shot**—a **12.6% overall performance boost** [48].
2. **CoT Requires Context & Rubrics (`CR`):** Standard Chain-of-Thought prompting _without_ problem stems and rubrics yielded minimal improvement (+0.82% in zero-shot, -1.35% in few-shot) [51]. However, when CoT was paired with `ContRubTEXT` (`CoT_CR`), accuracy jumped by **13.44% in zero-shot** and **3.7% in few-shot** [51].
3. **Category-Wise Balancing Effect:** CoT paired with rubrics significantly improved model accuracy on harder, under-predicted score tiers ('Beginning' and 'Proficient') without sacrificing performance on 'Developing' cases, substantially raising Quadratic Weighted Kappa [52, 53].
4. **GPT-4 vs. GPT-3.5:** GPT-4 outperformed GPT-3.5 by **8.64% on average** (0.6975 vs 0.6331) [55]. GPT-4 strictly adhered to rubric structures, whereas GPT-3.5 occasionally generated correct component extractions but assigned incorrect holistic scores [59, 60].
5. **Sampling Strategy (Greedy vs. Nucleus Voting):** For GPT-4, a **single-call greedy decoding strategy** (`temperature = 0`, `top_p = 0.01`) outperformed a 3-call nucleus ensemble voting strategy (`temperature = 0.9`, `top_p = 0.95`) [55, 58]. Voting was slightly helpful for GPT-3.5, showing that higher-capacity models (GPT-4) maintain scoring stability without 3x computational costs [58, 72].

---

## 5. Practical Uses, Limitations, & Trade-offs

### Practical Uses for Education:

- **Explainable Formative Assessment:** LLMs generate explicit natural language rationales alongside grades, allowing teachers to inspect how rubric components were evaluated and quickly catch grading errors [61, 63].
- **Elimination of Machine Learning Bottlenecks:** Educators can deploy automated grading using a small set of human-coded exemplars without writing custom code or training complex ML models [65].
- **Interactive Teacher Assisting:** Teachers can draft rubrics and automated feedback using LLMs, reviewing and refining outputs prior to student release [64].

### Limitations & Critical Trade-offs:

- **Accuracy Gap vs. Fine-Tuned Supervised Ensembles:** While prompt engineering reached up to 0.9083 accuracy on binomial tasks, custom supervised ML models fine-tuned on the same dataset achieved higher accuracy (0.86–0.94) [75]. Fine-tuning trades prompt engineering efficiency for higher task-specific precision [75].
- **API Cost Considerations:** As of the study's timeframe, GPT-4 API calls were **30x more expensive** than GPT-3.5 [71]. Educators must weigh model performance against operational budgets [71].
- **Model Sensitivity in Lighter LLMs:** Lower-capacity models (e.g., GPT-3.5) occasionally fail to follow complex rubric logic despite explicit prompt instructions [59, 60].

---

## 6. Summary Checklist for your Literature Review

- **Journal & Authority:** Published in _Computers & Education: Artificial Intelligence_ (Elsevier), a high-impact peer-reviewed venue [1].
- **Core Takeaway:** Chain-of-Thought prompting is not a silver bullet on its own; it requires explicit **item contexts and domain-specific scoring rubrics** to guide the LLM's reasoning path [51, 68].
- **Optimal Recipe:** **GPT-4 + Single-Call Greedy Decoding + Few-Shot Examples + Chain-of-Thought + Contextual Rubrics (`FS_CoT_CR`)** delivers the highest accuracy (0.6975 average) and complete explainability [54, 71, 74].

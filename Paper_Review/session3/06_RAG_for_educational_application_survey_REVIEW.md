# Paper 06 (REVIEW): Retrieval-augmented generation for educational application: A systematic survey

**Authors:** Zongxi Li, Zijian Wang, Weiming Wang, Kevin Hung, Haoran Xie, Fu Lee Wang (Lingnan University & Hong Kong Metropolitan University)
**Type:** Systematic survey, 51 studies (WoS, 2020–2025)

---

## 1. Venue info

| Item | Details |
|---|---|
| Publisher | Elsevier |
| Journal | Computers and Education: Artificial Intelligence, Vol 8 (2025), 100417 |
| Access | Open access (CC BY-NC-ND) |
| Dates | Received 28 Mar 2025, accepted 6 May 2025, online 14 May 2025 |
| Scopus | CiteScore **~28.7**, SJR **~5.2** (2024, TU Dresden records) |
| Quartile | **Q1** (Computer Science Applications, AI, Education) |
| Impact factor (JCR) | নিশ্চিত JIF পাইনি (কিছু site "n/a" দেখায়); Scopus metric-ই নির্ভরযোগ্য |
| A*? | না (journal), তবে এই field-এর **শীর্ষস্থানীয় venue-দের একটা** |

> ⚠️ Declaration of competing interest-এ বলা আছে: co-author Prof. Haoran Xie এই journal-এর Editor-in-Chief, তবে তিনি review-তে জড়িত ছিলেন না।

---

## 2. Section-by-section সারাংশ

### Abstract & 1. Introduction (page 1–2)
- LLM-এর দুই বড় সমস্যা: **hallucination** (ভুল তথ্য বানানো) ও **static knowledge** (নতুন পাঠ্যক্রম জানে না)।
- **RAG** = উত্তর দেওয়ার আগে বাইরের knowledge base থেকে প্রাসঙ্গিক অংশ খুঁজে এনে LLM-কে দেওয়া। এতে factual accuracy, update, transparency বাড়ে।
- 3 RQ: **RQ1** interactive/personalized learning-এ RAG, **RQ2** content তৈরি ও assessment, **RQ3** বড় স্কেলে deployment।

### 2. Retrieval-augmented generation (page 2–3)
RAG-এর ৩ ধাপ (**Fig. 1 workflow:** User → Query → Retriever → Database ← Indexing (textbook/testpaper/courseware) → retrieved chunks + prompt → LLM → উত্তর):
- **2.1 Indexing:** preprocessing (PDF/PPT/Word থেকে clean text) → **chunking** (ছোট টুকরা) → **embedding** (BGE, OpenAI ada-002) → vector database (FAISS, Weaviate, Pinecone)।
- **2.2 Retrieval:**
  - Sparse: **BM25** (keyword মিল), সহজ ও দ্রুত।
  - Dense: **DPR, ColBERTv2, Contriever** (অর্থ-ভিত্তিক), বেশি computation।
  - Hybrid।
- **2.3 Generation:** retrieved text prompt-এ জোড়া (concatenation), বা re-ranking/compression/Fusion-in-Decoder। LLM optimize: prompt engineering, fine-tuning, hybrid।

### 3. Material and methods (page 3–4)
- শুধু **Web of Science**, query: ("retrieval augmented generation" ...) AND (education OR teaching OR student OR classroom), 6 March 2025, 2020–2025।
- Exclusion: শুধু future work-এ RAG উল্লেখ; non-education; review article।
- **45 article** + backward citation search-এ **6** = **51**।
- প্রতিটা paper-কে 3 শ্রেণিতে ভাগ → RQ-তে map।

### 4. RAG application in education (page 4–10) — মূল অংশ
**Table 1:** ~50 application: নাম, scenario, objective, indexing, retrieval, generation। দেখা যায় বেশিরভাগ **OpenAI ada-002 embedding + semantic similarity retrieval + GPT-3.5/GPT-4**।
**Fig. 2:** পুরো taxonomy tree।

- **4.1 Interactive learning (RQ1):**
  - Q&A system (Anatbuddy anatomy, supply chain, math, MOOC, course logistics/SyllabusQA)।
  - Chatbot (**MoodleBot, ChatEd, EduChat, VizChat**)।
  - AI tutor (KG-RAG, OwlMentor, Jill Watson, **CS50 duck**, HiTA, CVTutor, LAMB, BiWi)।
  - Adaptive learning path (RAMO, SKYRAG)।
- **4.2 Content development & assessment (RQ2):**
  - 4.2.1 Question ও lesson plan তৈরি: MCQGen, ALINet, lesson plan generation।
  - **4.2.2 Intelligent assessment & feedback (আমাদের জন্য সবচেয়ে relevant):**
    - **SteLLA** (Qiu 2024): teacher-এর reference answer ও rubric দিয়ে short answer structured scoring।
    - **Jauhiainen & Guerra 2024:** GPT-3.5, GPT-4, Claude-3, Mistral-Large দিয়ে open-ended উত্তর grade, RAG দিয়ে variability কমানো, temperature-এর প্রভাব দেখা।
    - **Han et al. 2024:** tutoring practice assess, RAG > zero-shot/Tree-of-Thought।
    - Feedback: **UML diagram feedback** (Ardimento), K-12 data science (Fung, DSRAG), **programming feedback with lecture transcripts** (Jacobs & Jaschke)।
  - 4.2.3 Knowledge retrieval: knowledge graph, curriculum-aligned retrieval।
- **4.3 Scaling (RQ3):** admissions chatbot, dropout prediction, discipline-specific (medical, programming, geography, music), small language model + RAG (Liu 2024c), RAG-এর ৭টা failure point (Barnett).

### 5. Challenges & future (page 10–12)
1. **Hallucination এখনো আছে:** Harvard CS50-এ RAG assistant-ও কখনো ভুল ব্যাখ্যা দিয়েছে, তাই সব উত্তর মানুষ review করে।
2. **Knowledge base-এর completeness ও timeliness:** static database, update দরকার (agentic RAG)।
3. **খরচ ও latency:** commercial API, প্রতি ছাত্র ~$1.65 (Neumann); কিছু method 15 সেকেন্ড।
4. **Multimodal সীমাবদ্ধতা:** image, equation, diagram, video ভালো বোঝে না (faculty feedback: RAG struggles with images and equations)।
- প্রস্তাব: uncertainty estimation, human-in-the-loop, lightweight/open-source model, vision-language model, cross-modal retrieval, নীতিনির্ধারকের জন্য certification framework।

### 6. Conclusion
- RAG accuracy, personalization, teacher workload-এর জন্য সম্ভাবনাময়; কিন্তু উপরের ৪ চ্যালেঞ্জ বাকি।

---

## 3. Critical observations
- **শুধু WoS** ব্যবহার (arXiv/ACM/IEEE বাদ), তবে backward search দিয়ে কিছু পূরণ করেছে।
- Assessment-সংক্রান্ত paper খুব কম (মাত্র ৩–৬টা); বেশিরভাগ Q&A/chatbot।
- Study-গুলোর quality বা effect-এর মূল্যায়ন নেই, শুধু বর্ণনামূলক।
- Table 1-এ অনেক cell "-" (indexing/retrieval তথ্য অনুপস্থিত)।

## 4. TRACE-এর জন্য Gap / ব্যবহার
- ✅ **RAG দিয়ে rubric, model answer, লেকচার-নোট থেকে grading-কে "ground" করা** TRACE-এর সরাসরি design idea (SteLLA, Jauhiainen & Guerra)।
- ✅ Hallucination কমানো ও human review loop-এর যুক্তি।
- ✅ Programming feedback + RAG (Jacobs & Jaschke) প্রাসঙ্গিক।
- ❗ **Handwritten input ও OCR এর সাথে RAG-এর কোনো কাজ এখানে নেই।**
- ❗ Code grading-এ RAG (যেমন C-এর syntax rule, marking scheme) খুব কম।
- ❗ Multimodal gap = TRACE-এর handwritten image দিয়ে মাপা সুযোগ।

## 5. My notes (নিজে লেখো)
- Abstract/Intro:
- RAG 3 stages (Fig 1):
- Method (51 papers):
- Application taxonomy (Fig 2, Table 1):
- Assessment & feedback studies:
- Challenges:
- Questions for supervisor:

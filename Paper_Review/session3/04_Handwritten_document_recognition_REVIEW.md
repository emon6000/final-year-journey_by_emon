# Paper 04 (REVIEW): Exploration of advancements in handwritten document recognition techniques

**Authors:** Vanita Agrawal, Jayant Jagtap, M.V.V. Prasad Kantipudi (Symbiosis Institute of Technology, Pune; NIMS University, Jaipur, India)
**Type:** Review = **Bibliometric survey + Systematic review** (Scopus)

---

## 1. Venue info

| Item | Details |
|---|---|
| Publisher | Elsevier |
| Journal | Intelligent Systems with Applications, Vol 22 (2024), 200358 |
| Access | Open access (CC BY-NC) |
| Dates | Received 26 Oct 2023, accepted 9 Mar 2024, online 15 Mar 2024 |
| Impact factor | ~**5.5** (2025 JIF, journalmetrics.org); আগের বছর ~4.3 |
| JCR quartile | Information Systems **Q1**; AI ও Interdisciplinary Applications **Q2** |
| Scopus | CiteScore ~7 (পুরোনো figure); Scimago-তে CS Applications / CV & Pattern Recognition **Q1** |
| A*? | না (journal) |

> সংখ্যা aggregator থেকে নেওয়া। Final দেওয়ার আগে JCR/Scimago-তে ISSN **2667-3053** দিয়ে মিলিয়ে নাও।

---

## 2. Section-by-section সারাংশ

### Abstract & 1. Introduction (page 1–2)
- Handwritten document মানে শুধু text না: **text, digit, diagram, math expression, table**।
- Writing style-এর বৈচিত্র্য ও ভাষার জটিলতার জন্য recognition কঠিন।
- Digitize করলে সংরক্ষণ সস্তা, search সহজ; ব্যবহার: শিক্ষা, স্বাস্থ্য, ব্যাংক, logistics।
- Paper-এর দাবি: এটাই প্রথম যেখানে **bibliometric + systematic review একসাথে**। আগে Ruiz-Parrado et al. (2022) শুধু bibliometric করেছিল।
- **Fig. 1:** একটা handwritten page-এ পাঁচ ধরনের অংশ (Text, Diagram, Equation, Table) রঙ করে দেখানো।
- **Fig. 2:** real-world application (Education, IT, Documentation, Signature verification, Mailing address, Bank check)।

### 2. Handwritten document recognition (page 2)
- Technique: template matching, feature extraction, neural network, SVM।
- **Online** (stroke, গতি, চাপ ধরা যায়) বনাম **Offline** (শুধু scanned image, বেশি কঠিন)।
- **Fig. 3 (workflow):** Input image → Text/Non-text classifier → আলাদা ৫টা model (text, digit, diagram, math, table) → সব মিলিয়ে digital output।

### 3. Bibliometric review (page 3–5)
- Scopus query (Fig. 4)। 11,115 record (13 June 2023) → filter → **6,812** → manual ঘষামাজা → **~6,800** paper।
- **Fig. 5:** keyword co-occurrence: "recognition" সবচেয়ে বেশি, তারপর handwritten, handwriting, feature, neural networks।
- 3.1 Growth: 1961-এ শুরু (Kamentsky); **2018-এর পর বিস্ফোরণ**, প্রতি বছর 400+ (Fig. 6)। Covid ও digitization কারণ।
- Table 1/Fig. 7: **India সবচেয়ে বেশি paper**, তারপর China, USA।
- 3.2 Citation: Table 2: সবচেয়ে বেশি cited = Plamondon & Srihari (2000) survey (1936 cite); MNIST (Deng 2012), IAM database ইত্যাদি। Fig. 8 alluvial diagram: IEEE TPAMI সবচেয়ে বেশি cited source।
- 3.3 Funding: 25 sponsor ≥10 article করে fund করেছে (মোট 875)। বড়: National Natural Science Foundation of China (>30%)। Fig. 9, 10 funding ও affiliation (Indian Statistical Institute 144, Jadavpur 137, ...)।
- 3.4 Bibliographic coupling (Table 3, Fig. 11): Günter S. & Bunke H. সবচেয়ে strong link (TLS 20.39)।
- 3.5: কাদের সাথে কাজ করবে, কোথায় publish করবে সে গাইড।

### 4. Systematic review (page 6–11)
প্রতিটা অংশে সর্বোচ্চ cited open-access ~15 paper (last 5 years) নেওয়া, table-এ benefit ও challenge।
- **4.1 Text recognition (Table 4):** CNN সবচেয়ে বেশি, সাথে LSTM/RNN/ELM/MLP/VGG। Dataset **IAM** সবচেয়ে বেশি; metric **CER, WER**। ভবিষ্যৎ: **Vision Transformer (ViT)**, language model/grammar correction, line reading order।
- **4.2 Digit (Table 5):** MNIST-এ CNN ~99%+। সমস্যা: MNIST পরিষ্কার image, real noisy image-এ test দরকার।
- **4.3 Diagram (Table 6):** flowchart, circuit, UML, sketch। CNN, YOLO, k-means; dataset ছোট ও benchmark নেই।
- **4.4 Math expression (Table 7):** graph-based বা tree-based parsing, encoder-decoder। Dataset **CROHME**; metric **ExpRate** মাত্র ~45–67%, অর্থাৎ কঠিন।
- **4.5 Table (Table 8):** CRF, Graph Attention Network; কাজ কম, historical/chemistry document-এ বেশি।
- **4.6 Performance (Table 9):** সারসংক্ষেপ: Text CER ~4.5%, WER ~17.5% (ICFHR/ICDAR), digit 99%+, diagram 71–95%, math 43–67% ExpRate। **CNN = state of the art**।

### 5. Conclusion
- CNN feature extraction-এ সবচেয়ে জনপ্রিয়।
- **Non-text (circuit, UML, table) এর annotated benchmark নেই**।
- চ্যালেঞ্জ: writer style, real-time, কম training data, processing power।
- ভবিষ্যৎ: fine-tuning, noise-resistant preprocessing, lightweight real-time model, human-centered interface, edge computing, AR।

---

## 3. Critical observations
- 2024 publish, কিন্তু প্রায় সব সংখ্যা **2023-এর আগের**; ViT/TrOCR/VLM যুগের অনেক কাজ নেই।
- **Systematic অংশে quality assessment নেই**; শুধু "highest cited + open access" দিয়ে বাছাই (এতে নতুন paper বাদ পড়ে)।
- Bibliometric অংশ (author, funding) পড়তে আকর্ষণীয় কিন্তু TRACE-এর গবেষণা-প্রশ্নের জন্য কম কাজের।
- Table 9-এর তুলনা বিভিন্ন dataset ও metric-এ, সরাসরি তুলনা ঠিক না।
- Section 4.4-এ কিছু বর্ণনা অস্পষ্ট/ভুল (যেমন HMER-এর "three categories" speech recognition সহ)।

## 4. TRACE-এর জন্য Gap / ব্যবহার
- ✅ Handwriting recognition-এর **background ও vocabulary** (online/offline, CER/WER, IAM, CNN→Transformer)।
- ✅ Text/digit/diagram/math/table যে আলাদা সমস্যা তা বোঝায়। **C program = text + symbols + structure (indentation) + কখনো flowchart/diagram**, তাই TRACE এই সবগুলোর মিশ্রণ।
- ❗ **Handwritten source code recognition নিয়ে কোনো section নেই।** এটাই নিখুঁত gap।
- ❗ Education context-এ (exam grading) recognition-এর প্রভাব নেই।
- ❗ Benchmark অভাবের কথা paper নিজেই বলেছে, TRACE নিজের dataset বানালে সেটা contribution হতে পারে।

## 5. My notes (নিজে লেখো)
- Abstract/Intro:
- Fig 1–3:
- Bibliometric (Fig 4–11, Table 1–3):
- Text/Digit recognition:
- Diagram/Math/Table:
- Table 9 performance:
- Conclusion:
- Questions for supervisor:

# Summary: Towards Trustworthy AutoGrading of Short, Multi-lingual, Multi-type Answers

## 🎯 Overview & Purpose

While Artificial Intelligence (AI) can automatically grade short text answers, people often do not trust it because AI makes mistakes—especially "false negatives" (failing a student who actually gave a correct answer). Furthermore, most previous studies only tested AI on small datasets in a single language. 

**The Goal:** This paper aims to create a highly trustworthy autograding system. It uses a massive, real-world dataset (about 10 million question-answer pairs from a startup called Classtime) covering multiple languages (Ukrainian, English, Russian, etc.) and diverse subjects (Math, Language, Biology, etc.). 

> **সারসংক্ষেপ:** এআই দিয়ে স্বয়ংক্রিয়ভাবে পরীক্ষার ছোট উত্তর (Short answers) গ্রেডিং করা সম্ভব হলেও, মানুষ এর ওপর পুরোপুরি আস্থা রাখতে পারে না। কারণ এআই মাঝে মাঝেই সঠিক উত্তরকে ভুল বলে মার্ক করে (False Negative)। আগের গবেষণাগুলো সাধারণত ছোট এবং এক ভাষার ডাটাসেট নিয়ে কাজ করেছে। এই গবেষণার মূল উদ্দেশ্য হলো এমন একটি নির্ভরযোগ্য এআই গ্রেডিং সিস্টেম তৈরি করা, যার ওপর শিক্ষক ও শিক্ষার্থীরা ভরসা করতে পারে। এর জন্য তারা 'Classtime' নামের একটি প্ল্যাটফর্ম থেকে প্রায় ১ কোটি প্রশ্ন-উত্তরের একটি বিশাল ডাটাসেট ব্যবহার করেছেন, যেখানে গণিত থেকে শুরু করে ভাষা—নানা ধরনের এবং নানা ভাষার প্রশ্ন রয়েছে।

## 🧠 AI Models Used

The researchers tested state-of-the-art Natural Language Processing (NLP) Transformer models:
*   **Multilingual BERT**
*   **LaBSE (Language-agnostic BERT Sentence Embedding)** *(This model performed the best in their tests).*

The AI takes the student's answer and the teacher's correct answer, converts them into mathematical vectors, and calculates a **similarity score** (Cosine Similarity) between them.

> **ব্যবহৃত এআই মডেল:** গবেষকরা আধুনিক এনএলপি (NLP) ট্রান্সফরমার মডেল যেমন- Multilingual BERT এবং LaBSE ব্যবহার করেছেন। এর মধ্যে LaBSE সবচেয়ে ভালো পারফর্ম করেছে। এই মডেলগুলো মূলত শিক্ষার্থীর দেওয়া উত্তর এবং শিক্ষকের দেওয়া সঠিক উত্তরের মধ্যে তুলনা করে একটি 'সিমিলারিটি স্কোর' (Similarity Score) বা মিলের হার বের করে।

## 🛡️ The Core Innovation: Trust via "Human-in-the-Loop"

If the AI tries to grade *every single answer*, its accuracy drops to around 86.5%, which is not good enough for high-stakes exams. To fix this, the researchers introduced **Thresholds ($T^c$ for correct, $T^i$ for incorrect)** based on the similarity score:

1.  **Easy to Grade (Autograded):** If the similarity score is very high, the AI confidently marks it *Correct*. If it is very low, it confidently marks it *Incorrect*.
2.  **Difficult to Grade (Manual Grading):** If the score falls in the middle (uncertain), the AI does *not* grade it. Instead, it passes these "difficult" answers to the human teacher to grade manually.

Teachers can set a strict accuracy constraint (e.g., "I want 98% accuracy and 0 false negatives"). The AI will adjust its thresholds to ensure it only grades the questions it is absolutely sure about.

> **মূল উদ্ভাবন - আস্থার জন্য 'থ্রেশহোল্ড' পদ্ধতি:** এআই যদি সবগুলো খাতা একাই দেখতে যায়, তবে এর নির্ভুলতা ৮৬.৫%-এ নেমে আসে, যা মূল পরীক্ষার জন্য যথেষ্ট নয়। এর সমাধানে গবেষকরা একটি চমৎকার পদ্ধতি বের করেছেন। এআই শুধুমাত্র সেই উত্তরগুলোই গ্রেডিং করবে যেগুলো সে নিশ্চিতভাবে বুঝতে পারছে (Easy to grade)। আর যেসব উত্তরে এআই কনফিউজড বা দ্বিধান্বিত (Difficult to grade), সেগুলো সে শিক্ষকের কাছে পাঠিয়ে দেবে ম্যানুয়ালি চেক করার জন্য। শিক্ষক চাইলে এআই-কে নির্দেশ দিতে পারেন যে, "আমি ৯৮% নির্ভুলতা চাই", তখন এআই শুধু সেই অনুযায়ী নিশ্চিত উত্তরগুলোই চেক করবে।

## 🔎 Autograder Validation

To ensure the AI is performing well on a specific, individual exam (and not just on average), the system uses a clever validation step. It looks at how the teacher manually graded the "difficult" questions. If the AI's predictions align well with the teacher's manual grades on this tricky subset, the teacher can trust that the AI graded the "easy" questions correctly for that specific exam.

> **ভ্যালিডেশন বা যাচাইকরণ:** এআই সত্যিই ঠিকমতো কাজ করছে কি না, তা যাচাই করার জন্য একটি ভ্যালিডেশন পদ্ধতি রাখা হয়েছে। শিক্ষক যখন 'কঠিন' উত্তরগুলো ম্যানুয়ালি গ্রেড করেন, তখন সিস্টেম মিলিয়ে দেখে যে ওই কঠিন উত্তরগুলোতে এআই-এর ধারণা আর শিক্ষকের গ্রেডিং কতটা মিলছে। যদি ভালো মিল থাকে, তবে শিক্ষক নিশ্চিন্ত হতে পারেন যে এআই বাকি 'সহজ' খাতাগুলোও ঠিকভাবেই দেখেছে।

## 🏆 The Results

*   **Baseline Accuracy:** ~86.5% (when forcing the AI to grade 100% of the answers).
*   **Trustworthy Accuracy:** By setting a high-accuracy constraint (like 98%) and letting humans grade the tricky ones, the system achieves **human-level accuracy**.
*   **Workload Reduction:** Even with the AI skipping the hard questions, it still automatically grades about 56% of the exam, cutting the teacher's grading workload by roughly **50%**.

> **ফলাফল:** এআইকে জোর করে সব খাতা দেখতে দিলে অ্যাকুরেসি হয় ৮৬.৫%। কিন্তু থ্রেশহোল্ড পদ্ধতি ব্যবহার করে কঠিন খাতাগুলো শিক্ষককে দেখতে দিলে, এর অ্যাকুরেসি মানুষের সমপর্যায়ে (যেমন ৯৮%) পৌঁছায়। মজার ব্যাপার হলো, কঠিন খাতাগুলো বাদ দেওয়ার পরও এআই অর্ধেকের বেশি খাতা একাই দেখতে পারে, যার ফলে শিক্ষকের গ্রেডিং করার কষ্ট এবং সময় প্রায় **৫০% কমে যায়**।
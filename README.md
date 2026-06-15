# 🎯 AI Interview Analyzer

> **Practice your interview. Build your confidence. Get real feedback.**

A Jupyter Notebook tool designed for students who want to sharpen their interview skills. Upload a video of yourself answering interview questions and receive a detailed, AI-powered analysis covering how you speak, how you look, and what you say — all in a downloadable PDF report.

---

## 🌟 What It Does

Most students practice interviews by guessing — *"Did I say 'um' too much? Was I too fast? Did I look confident?"*

This tool answers those questions objectively. Record yourself doing a mock interview, upload the video, and get scored across five key dimensions:

| Dimension | What's Measured |
|---|---|
| 🗣️ **Communication** | Speaking pace (WPM), filler word usage |
| 💪 **Confidence** | Voice energy, consistency, pitch, pausing |
| 👁️ **Eye Contact** | Camera engagement throughout the session |
| 🧠 **Content Quality** | Technical vocabulary, answer structure, clarity |
| 😌 **Emotion Stability** | Facial emotion distribution and composure |

---

## 📸 Output: Professional PDF Report

After analysis, a PDF is automatically generated with:
- Overall interview score (out of 100) with a verdict (Excellent / Good / Average / Needs Improvement)
- Section-by-section score breakdown
- Speaking pace classification (Too Slow / Ideal / Too Fast)
- Filler word counts and severity rating
- Eye contact percentage and assessment
- Emotion distribution chart (happy, neutral, fear, etc.)
- Detected technical keywords from your answer
- Personalized **strengths** and **areas for improvement**
- First 1,000 characters of your transcript

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- Jupyter Notebook or JupyterLab
- A webcam recording of your mock interview (`.mp4`, `.avi`, `.mov`, or `.mkv`)

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/ai-interview-analyzer.git
cd ai-interview-analyzer

# Install dependencies
pip install -r requirements.txt
```

### Required Libraries

```bash
pip install faster-whisper deepface opencv-python moviepy librosa \
            transformers ipywidgets tqdm reportlab
```

> **Note on model size:** The notebook uses `faster-whisper` with the `tiny` model by default, which runs on CPU. If you have 16GB+ RAM and a GPU, you can switch to `medium` for better transcription accuracy (see Section 7 of the notebook).

---

## 📖 How to Use

1. **Open the notebook** in Jupyter:
   ```bash
   jupyter notebook code.ipynb
   ```

2. **Run all cells** from top to bottom (`Kernel → Restart & Run All`)

3. **Upload your video** using the file upload widget that appears

4. **Click "▶ Analyze Video"** and wait while the AI processes your recording

5. **Download your PDF report** from the link that appears when analysis completes

---

## 🔬 How It Works (Under the Hood)

The notebook runs a multi-stage analysis pipeline:

```
Video File
   │
   ├──► Audio Extraction (moviepy)
   │         │
   │         ├──► Transcription (faster-whisper)  → Words per minute, transcript
   │         ├──► Filler Word Detection            → "um", "uh", "like", etc.
   │         ├──► Sentiment Analysis (DistilBERT)  → Positive/Negative tone
   │         └──► Voice Analysis (librosa)         → Energy, pitch, clarity, pauses
   │
   └──► Frame Sampling (OpenCV, 0.5 fps)
             │
             ├──► Facial Emotion Analysis (DeepFace) → Emotion per frame
             └──► Eye Contact Detection (Haar Cascades) → Camera engagement %
                       │
                       └──► Score Computation → PDF Report (reportlab)
```

---

## 📊 Scoring Breakdown

| Score | Weight | Criteria |
|---|---|---|
| Communication | 25% | Speaking pace (ideal: 110–160 WPM) + filler word ratio |
| Confidence | 25% | Voice features + eye contact + positive emotions |
| Content Quality | 30% | Technical keywords + answer structure + clarity |
| Eye Contact | 10% | % of frames with visible eye engagement |
| Emotion Stability | 10% | Ratio of neutral/positive to negative emotions |

---

## 💡 Tips for Best Results

- **Record in good lighting** — the face detection works better with a clear, well-lit face
- **Look directly at your camera** as if making eye contact with an interviewer
- **Aim for 2–5 minutes** of speaking — longer videos give more accurate averages
- **Use technical terms** relevant to your field — the content analyzer detects hundreds of keywords across AI, data engineering, software development, and more
- **Speak at a natural pace** — the ideal range is 110–160 words per minute

---

## 🎓 Who This Is For

This tool is built for:
- **CS and engineering students** preparing for technical interviews
- **Anyone doing mock interviews** who wants objective feedback
- **Self-learners** who want to track improvement over multiple sessions

---

## 🛠️ Project Structure

```
ai-interview-analyzer/
│
├── code.ipynb              # Main analysis notebook
├── README.md               # You are here
└── Interview_Professional_Report.pdf   # Generated after each analysis run
```

---

## ⚠️ Known Limitations

- Eye contact detection uses Haar Cascades which work best with a **front-facing, well-lit face**
- Transcription accuracy depends on audio quality — use a decent microphone if possible
- The `tiny` Whisper model trades accuracy for speed; switch to `medium` for better results on longer videos
- Analysis may take 2–10 minutes depending on your hardware and video length

---

## 🤝 Contributing

Contributions are welcome! If you have ideas for new features or improvements:
1. Fork the repo
2. Create a new branch (`git checkout -b feature/your-feature`)
3. Commit your changes
4. Open a Pull Request

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

*Built to help students walk into interviews with confidence. Good luck! 🚀*

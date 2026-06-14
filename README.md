# 🎯 AI Interview Analyzer

An AI-powered Jupyter Notebook tool that analyzes mock interview videos and generates a detailed professional PDF report with scores across communication, confidence, eye contact, emotion stability, and content quality.

---

## 🚀 Features

- 🎙️ **Speech Transcription** — Transcribes audio using [faster-whisper](https://github.com/SYSTRAN/faster-whisper) and computes words-per-minute (WPM)
- 😊 **Facial Emotion Detection** — Analyzes emotions frame-by-frame using [DeepFace](https://github.com/serengil/deepface)
- 👁️ **Eye Contact Tracking** — Detects camera engagement using OpenCV Haar Cascades
- 🗣️ **Filler Word Analysis** — Identifies 50+ filler words and verbal crutches with severity scoring
- 💬 **Sentiment Analysis** — Classifies transcript sentiment using DistilBERT (HuggingFace Transformers)
- 🔊 **Voice Confidence Scoring** — Computes energy, pitch, steadiness, and clarity from audio features via librosa
- 📝 **Content Quality Analysis** — Detects 300+ technical keywords and evaluates structure and clarity
- 📄 **PDF Report Generation** — Produces a multi-section professional report with scores and personalized feedback

---

## 📋 Requirements

- Python 3.8+
- Jupyter Notebook / JupyterLab
- A webcam-recorded interview video (`.mp4`, `.avi`, `.mov`, `.mkv`)

---

## 📦 Installation

```bash
pip install faster-whisper deepface opencv-python moviepy librosa transformers \
            ipywidgets tqdm reportlab torch
```

> **Note:** If your machine has ≤16 GB RAM, the notebook defaults to the `tiny` Whisper model. You can switch to `medium` for better transcription accuracy.

---

## ▶️ Usage

1. Launch Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
2. Open `code.ipynb` and run all cells in order.
3. Use the **Upload Video** widget to upload your interview recording.
4. Click **▶ Analyze Video** to start the analysis pipeline.
5. Download the generated `Interview_Professional_Report.pdf` when complete.

---

## 📊 Report Sections

| Section | Description |
|---|---|
| Candidate Summary | Duration, word count, overall score & verdict |
| Score Breakdown | Scores for all 5 dimensions |
| Speaking Analysis | WPM, pace classification, and feedback |
| Filler Word Analysis | Count, ratio, top fillers, severity |
| Eye Contact Analysis | Contact percentage and engagement assessment |
| Emotion Stability | Distribution across 7 emotions + stability score |
| Content Quality | Clarity, relevance, structure, and tech vocabulary |
| Technical Keywords | Detected domain-specific terms |
| Strengths & Improvements | Personalized, auto-generated feedback |
| Transcript | First 1000 characters of spoken content |

---

## 🏗️ Project Structure

```
code.ipynb                        # Main notebook (all logic)
Interview_Professional_Report.pdf # Generated after analysis
```

---

## 🛠️ Tech Stack

| Component | Library |
|---|---|
| Speech-to-Text | `faster-whisper` |
| Emotion Recognition | `deepface` |
| Eye Detection | `opencv-python` (Haar Cascades) |
| Audio Features | `librosa` |
| Sentiment Analysis | `transformers` (DistilBERT) |
| Video Processing | `moviepy`, `opencv-python` |
| PDF Generation | `reportlab` |
| Notebook UI | `ipywidgets` |

---

## ⚠️ Notes

- The notebook runs entirely **locally** — no data is sent to external servers.
- Analysis time depends on video length and hardware; expect 1–5 minutes for a typical 5-minute video.
- For GPU acceleration with Whisper, change `device='cpu'` to `device='cuda'` in Section 7.

---

## 📄 License

MIT License — feel free to use, modify, and distribute.

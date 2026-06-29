# 🎥 Interview Analyzer

An offline, end-to-end interview practice tool that runs entirely inside a Jupyter notebook. Upload a video of yourself answering an interview question, and it analyzes your **speech, content, voice, eye contact, and facial expressions** to generate a scored PDF report — with honest caveats about what each metric can and can't actually tell you.
Mainly for tech people

## What it does

Upload a short video and the pipeline runs through seven stages:

1. **Audio extraction** — pulls a clean WAV track from the video (gracefully continues with visual-only analysis if there's no audio)
2. **Frame sampling** — samples video frames at ~0.5 fps (capped at 240 frames) for facial/gaze analysis
3. **Transcription** — uses `faster-whisper` to transcribe speech with word-level timestamps and computes words-per-minute
4. **Gaze estimation** — uses MediaPipe Face Landmarker (iris vs. eye-corner offset) to estimate camera engagement
5. **Facial expression analysis** — uses DeepFace to classify expressions per frame, with a confidence threshold below which readings are marked `uncertain_reading` rather than guessed
6. **Voice & content analysis** — extracts acoustic features (energy, pitch variability, pause quality, etc.), detects filler words, scores technical vocabulary, and runs sentiment analysis on the transcript
7. **Scoring & report generation** — combines everything into a weighted overall score and renders a multi-section PDF report

The whole thing runs through a simple `ipywidgets` UI inside the notebook — upload a video, click **Analyze Video**, and a results card plus a downloadable PDF report are produced.

## Scored dimensions

| Metric | What feeds into it |
|---|---|
| **Communication** | Speaking pace (WPM vs. ideal ~135 WPM) + filler word ratio |
| **Confidence** | Vocal presence score, eye contact score, and positive-expression ratio |
| **Content Quality** | Sentence clarity, structure markers, technical vocabulary, relevance |
| **Eye Contact** | % of sampled frames where gaze is aligned with the camera |
| **Emotion Stability** | Ratio of composed/positive expressions to anxious/negative ones across the session |

These combine into a single **Overall Score (0–100)** with a verdict (*Excellent / Good / Average / Needs Improvement*), plus a list of strengths and concrete areas for improvement.

## Why it's designed this way

A lot of "AI interview scorer" tools overstate what facial expression or voice analysis can actually detect. This project tries not to:

- Every metric ships with an explicit caveat in the report (e.g. *"these are facial expression classifications, not true emotional states"*, *"voice metrics are acoustic proxies, not personality traits"*).
- Expression and emotion readings below a confidence threshold are labeled `uncertain_reading` instead of being forced into a category.
- Filler word detection includes an honest false-positive/false-negative risk note (fast speech, accents, and non-English words can throw it off).
- Technical keyword scoring is **density-capped** so the score rewards depth over keyword-stuffing.

## Output

- An in-notebook results summary (overall score, sub-scores, verdict)
- A downloadable **PDF report** with 12 sections: transcript stats, speaking pace, filler analysis, eye contact, expression breakdown, voice features, content quality, sentiment, strengths, improvements, and a transcript excerpt
- A console "honest self-assessment summary" printed for quick reference

## Tech stack

| Component | Library |
|---|---|
| Transcription | [`faster-whisper`](https://github.com/SYSTRAN/faster-whisper) (`tiny` model, CPU/int8) |
| Gaze tracking | [`mediapipe`](https://github.com/google/mediapipe) Face Landmarker |
| Facial expression | [`deepface`](https://github.com/serengil/deepface) |
| Sentiment analysis | 🤗 `transformers` (`distilbert-base-uncased-finetuned-sst-2-english`) |
| Audio/video processing | `moviepy`, `opencv-python` |
| PDF generation | `reportlab` |
| Notebook UI | `ipywidgets` |

Everything runs **locally and offline** (after the one-time MediaPipe model download) — no API keys, no cloud calls.

## Getting started

### Requirements

- Python 3.10+ (developed on 3.13)
- ~16 GB RAM recommended (for smoother DeepFace/Whisper performance — it will still run on less, just slower)
- `ffmpeg` installed and on your PATH

### Installation

```bash
pip install faster-whisper mediapipe deepface opencv-python moviepy \
            transformers torch reportlab ipywidgets tqdm numpy
```

> The MediaPipe Face Landmarker model (`face_landmarker.task`) is downloaded automatically on first run.

### Usage

1. Open `Interview_Analyzer.ipynb` in Jupyter Lab/Notebook (or VS Code).
2. Run all cells in order.
3. Use the upload widget to select a video (`.mp4`, `.avi`, `.mov`, `.mkv`, `.webm` — 5 minutes or less recommended).
4. Click **▶ Analyze Video**.
5. Review the in-notebook results card and download the generated PDF report.

## Limitations

- Designed for single-face, front-facing webcam-style videos — not group calls or low-light/occluded footage.
- Facial expression and voice "confidence" scores are proxies based on signal/visual patterns, not validated psychological measures.
- The `tiny` Whisper model is used for speed; swapping in `base` or `medium` will improve transcription accuracy at the cost of runtime (see Cell 7).
- Filler word detection is dictionary/regex-based, not context-aware — it can both over- and under-count depending on speaking style.

## License

Add your preferred license here (e.g. MIT).

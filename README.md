# 🎙️ MeetingMind AI
> An AI-powered meeting assistant built with LangGraph + OpenAI

Upload a meeting recording (or paste a transcript) and instantly get a structured summary, action items with owners and deadlines, and a professional follow-up email — all generated automatically.

---

## 📸 Demo

Paste any meeting transcript → hit **Analyze Meeting** → get results across 4 tabs:

| Tab | What you get |
|---|---|
| 📋 Summary | Meeting overview, key points, decisions made |
| ✅ Action Items | Structured table — task, owner, due date |
| 📧 Email | Ready-to-send follow-up email |
| 📄 Transcript | Raw transcript from Whisper or your paste |

---

## 🔄 Workflow

```
┌─────────────────────────────────────┐
│         User Input                  │
│  Audio File  ──or──  Paste Text     │
└────────────────┬────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────┐
│       Whisper Transcription         │
│   (skipped if text is pasted)       │
└────────────────┬────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────┐
│         LangGraph Workflow          │
│                                     │
│   ┌─────────────────────────────┐   │
│   │   Node 1 — Summarize        │   │
│   │   Reads transcript,         │   │
│   │   writes structured summary │   │
│   └──────────────┬──────────────┘   │
│                  │                  │
│   ┌──────────────▼──────────────┐   │
│   │   Node 2 — Extract Tasks    │   │
│   │   Pulls action items as     │   │
│   │   structured JSON           │   │
│   └──────────────┬──────────────┘   │
│                  │                  │
│   ┌──────────────▼──────────────┐   │
│   │   Node 3 — Generate Email   │   │
│   │   Uses summary + tasks to   │   │
│   │   write follow-up email     │   │
│   └──────────────┬──────────────┘   │
│                  │                  │
└──────────────────┼──────────────────┘
                   │
                   ▼
┌─────────────────────────────────────┐
│           Display Results           │
│   Summary / Tasks / Email /         │
│   Transcript tabs                   │
└─────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| UI | Streamlit |
| AI Workflow | LangGraph |
| LLM | OpenAI GPT-4o-mini |
| Transcription | OpenAI Whisper-1 |
| Orchestration | LangChain |
| Language | Python 3.10+ |

---

## 📁 Project Structure

```
meetingmind/
│
├── app.py           # Streamlit frontend and UI
├── graph.py         # LangGraph workflow definition
├── nodes.py         # Node functions (summarize, extract_tasks, generate_email)
├── prompts.py       # All LLM prompt templates
├── requirements.txt # Python dependencies
├── .env             # Your OpenAI API key (never commit this)
├── .gitignore
└── uploads/         # Temp folder for audio files
```

---

## 🚀 Setup & Run

### 1. Clone the repo

```bash
git clone https://github.com/your-username/meetingmind.git
cd meetingmind
```

### 2. Create virtual environment

```bash
python -m venv venv

# Mac/Linux
source venv/bin/activate

# Windows
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Add your OpenAI API key

Create a `.env` file in the root folder:

```
OPENAI_API_KEY=sk-...
```

### 5. Run the app

```bash
streamlit run app.py
```

Open [http://localhost:8501](http://localhost:8501) in your browser.

---

## 🎤 Supported Audio Formats

`mp3` `mp4` `wav` `m4a` `ogg` `webm`

---

## 💡 Why LangGraph?

Instead of making one big GPT call that does everything, LangGraph breaks the work into an explicit pipeline:

- Each node does **one job only**
- State is passed cleanly between nodes
- If something fails, you know **exactly which step** broke
- Easy to extend — add a new node without touching the rest
# ⚙️ Gistly — AI Meeting & Video Intelligence Assistant

Gistly turns any YouTube video or local audio/video file into a searchable, chattable meeting record. It transcribes the audio, generates a summary, extracts action items, key decisions, and open questions, and lets you ask follow-up questions grounded in the transcript through a RAG-powered chat interface.

## Features

- 🎥 **Flexible input** - accepts a YouTube URL or a local file path
- 🌐 **Multilingual transcription** - local Whisper for English, Sarvam AI's speech-to-text-translate API for Hindi → English
- 📋 **Automatic summarization** - concise summary and auto-generated title for every session
- ✅ **Structured extraction** - action items, key decisions, and open questions pulled straight from the transcript
- 💬 **RAG chat** - ask questions about the meeting and get answers grounded in the actual transcript, powered by LangChain + ChromaDB + Mistral
- 🎨 **Custom UI** - fully themed Streamlit interface, no default styling

## Tech Stack

| Layer | Tools |
|---|---|
| UI | Streamlit |
| Transcription | OpenAI Whisper (local), Sarvam AI STT |
| LLM | Mistral AI (`mistral-small-latest`) via LangChain |
| RAG / Vector store | LangChain, ChromaDB, `langchain_chroma` |
| Video/audio handling | yt-dlp, FFmpeg, pydub |

## Project Structure

```
Gistly/
├── app.py                     # Streamlit UI and pipeline orchestration
├── core/
│   ├── transcriber.py         # Whisper + Sarvam transcription logic
│   ├── summarizer.py          # Summary + title generation
│   ├── extractor.py           # Action items / decisions / questions extraction
│   ├── rag_engine.py          # RAG chain build + query
│   └── vector_store.py        # ChromaDB vector store setup
├── utils/
│   └── audio_processor.py     # Input handling (YouTube download / local file → audio chunks)
├── Requirements.txt
└── main.py
```

## Setup

### Prerequisites

- Python 3.10+
- [FFmpeg](https://ffmpeg.org/download.html) installed and available on your system PATH
- A [Mistral AI](https://console.mistral.ai/) API key
- A [Sarvam AI](https://www.sarvam.ai/) API key (only required for Hindi transcription — English mode works without it)

### Installation

```bash
git clone https://github.com/Tanishka798/Gistly-AI-Meeting-Video-Intelligence-Assistant-.git
cd Gistly-AI-Meeting-Video-Intelligence-Assistant-

python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # macOS/Linux

pip install -r Requirements.txt
```

### Environment variables

Create a `.env` file in the project root:

```
MISTRAL_API_KEY=your_mistral_key_here
SARVAM_API_KEY=your_sarvam_key_here
```

### Run

```bash
streamlit run app.py
```

The app opens at `http://localhost:8501`.

## Usage

1. Paste a YouTube URL or a local file path in the sidebar
2. Choose a language - `english` (local Whisper) or `hinglish` (Sarvam API)
3. Click **Analyse** to run the pipeline
4. Review the summary, action items, key decisions, and open questions
5. Use the chat panel at the bottom to ask questions about the transcript

## License

This project is open source. Add a license of your choice (MIT recommended for personal/portfolio projects).

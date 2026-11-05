# Local RAG

A small retrieval-augmented generation (RAG) command-line app. It indexes Markdown files in `docs/`, retrieves the most relevant text chunks for a question, and asks a local Ollama model to answer using that context.

## Requirements

- Python 3.9+
- [uv](https://docs.astral.sh/uv/getting-started/installation/)
- [Ollama](https://ollama.com/) installed and running

## Setup

Pull the models used by the app:

```powershell
ollama pull nomic-embed-text
ollama pull qwen3.5:4b
```

If this project isn’t already initialized with `uv`, initialize it and add the dependencies:

```powershell
uv init --bare
uv add requests numpy
```

Add Markdown files to the `docs` folder next to `rag.py`. The app splits each file into chunks at blank lines.

## Run

From the project directory:

```powershell
uv run python rag.py
```

Enter a question at the `Ask:` prompt. The app retrieves the three most similar chunks by cosine similarity and prints the model's answer. Press `Ctrl+C` to exit.

## Sample Questions

- What time does Byte Bistro open on weekdays?
- What are the cafe's weekend hours?
- Are dogs allowed inside the cafe?

## Configuration

Edit the constants near the top of `rag.py` to change the Ollama URL or models:

- `OLLAMA` — Ollama API address (default: `http://localhost:11434`)
- `EMBED_MODEL` — embedding model (default: `nomic-embed-text`)
- `CHAT_MODEL` — chat model (default: `qwen3.5:4b`)

If the context does not contain the answer, the prompt instructs the model to respond with “I don't know”.

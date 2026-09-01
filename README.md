# Business AI Chatbot (Python + Hugging Face)

A lightweight, CPU-friendly AI chatbot built with an open-source Hugging Face
model. Designed as a foundation for business use cases — with knowledge-base
lookup, a web interface, guardrails, and persistent memory built in.

## Features

- **Conversational chatbot** powered by `Qwen2.5-0.5B-Instruct` (runs on CPU, no GPU required)
- **Conversation history** so the bot remembers context within a session
- **Model upgrade helper** to switch to a bigger model (e.g. `Qwen2.5-1.5B-Instruct`) when a GPU is available
- **Simple knowledge base search** — keyword matching against company facts, injected into the prompt for more relevant answers
- **Web interface** via [Gradio](https://www.gradio.app/), with a shareable public link
- **Basic guardrails** — blocks inappropriate messages before they reach the model
- **Persistent memory** — saves and reloads conversations per user with SQLite, so chats survive restarts

## Tech Stack

- Python 3.12
- [Transformers](https://github.com/huggingface/transformers) (Hugging Face)
- PyTorch
- Gradio
- SQLite (built into Python)

## Getting Started

### Prerequisites

- Python 3.10+
- pip

### Installation

```bash
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>
pip install -r requirements.txt
```

If you don't have a `requirements.txt` yet, install manually:

```bash
pip install transformers accelerate torch gradio
```

### Running the Notebook

Open `ai-chatbot-python-huggingface.ipynb` in Jupyter, Kaggle, or Google Colab
and run the cells in order (Step 1 through Step 13).

### Running the Web Interface

After running through Step 11 in the notebook, the Gradio interface will
launch and print a local and public URL:

```
Running on local URL:  http://127.0.0.1:7860
Running on public URL: https://xxxxx.gradio.live
```

Open either link in your browser to chat with the bot.

## Project Structure

```
.
├── ai-chatbot-python-huggingface.ipynb   # Main notebook (all steps)
├── README.md                             # This file
└── chat_history.db                       # Created automatically (SQLite, gitignored)
```

## How It Works

1. **Model loading** — loads a small instruct-tuned model from Hugging Face.
2. **Chat function** — maintains a conversation history and generates replies using the model's chat template.
3. **Knowledge base search** — checks the user's message against a list of business facts and adds any matches as context before generating a reply.
4. **Guardrails** — filters messages containing blocked keywords before they reach the model.
5. **Persistent memory** — saves each session's conversation to a local SQLite database, keyed by `session_id`.

## Known Limitations

- The default model (0.5B parameters) is small and can sometimes give generic or repetitive answers. Switching to a larger model (Step 9) or tuning generation settings (temperature, repetition penalty) can help.
- Knowledge base search uses simple keyword matching, not semantic search — it won't catch questions phrased very differently from the stored facts.
- Guardrails use basic substring matching and are not a complete content-safety solution.

## Roadmap

- [ ] Replace keyword search with a proper embedding-based RAG pipeline
- [ ] Add support for a larger/fine-tuned model by default
- [ ] Permanent deployment (e.g. Hugging Face Spaces)
- [ ] Stronger guardrails / moderation
- [ ] Multi-user session handling in the Gradio UI

## License

Add your preferred license here (e.g. MIT).

## Acknowledgements

- [Hugging Face Transformers](https://github.com/huggingface/transformers)
- [Qwen2.5](https://huggingface.co/Qwen) by Alibaba Cloud
- [Gradio](https://www.gradio.app/)

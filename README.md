
# YouTube RAG Chatbot

A notebook-based Retrieval-Augmented Generation (RAG) chatbot that answers questions about a YouTube video transcript.

## What It Does

The pipeline:

1. Fetches a YouTube transcript.
2. Splits the transcript into overlapping text chunks.
3. Creates embeddings for each chunk with OpenAI.
4. Stores the embeddings in a local FAISS vector store.
5. Retrieves the most relevant chunks for each question.
6. Uses `gpt-4o-mini` to answer from the retrieved context.
7. Keeps previous questions and answers in the conversation prompt.

When the transcript does not contain enough information, the chatbot is instructed to answer `I don't know.`

## Requirements

- Python 3.10 or newer
- An OpenAI API key
- Internet access for the YouTube transcript and OpenAI API
- Jupyter support in VS Code or another Jupyter environment

## Setup

Create and activate a virtual environment, then install the dependencies:

bash

python -m venv .venv

Windows PowerShell:

PowerShell
.\.venv\Scripts\Activate.ps1
Install packages:

Bash
pip install -r requirements.txt
Create a .env file in the project directory:

Code snippet
OPENAI_API_KEY=your_openai_api_key
Note: Never commit .env or expose the API key in the notebook.

Run
Open task.ipynb, select the virtual environment as the notebook kernel, and run the code cell. Enter questions at the prompt. Type exit, quit, or q to end the conversation.

To use another video, change the video_id value in the notebook. The value is the part after v= in a YouTube URL. For example, https://www.youtube.com/watch?v=SfOaZIGJ_gs has the video ID SfOaZIGJ_gs.

Project Structure
Plaintext
.
├── task.ipynb       # Transcript ingestion, retrieval, and chatbot loop
├── requirements.txt # Python dependencies
├── README.md        # Project documentation
├── .gitignore       # Git ignore file (excludes .env, venv, etc.)
└── .env             # Local API key; do not commit
Notes
Each question triggers embedding retrieval and an LLM request, which may incur OpenAI usage charges.

FAISS is built in memory each time the notebook starts; it is not persisted between runs.

The chatbot answers from the selected transcript, not from general web search.


---

### 3. Recommended `.gitignore`
Make sure you have a `.gitignore` in the repo to prevent accidentally uploading `.env` or virtual environment files:

`gitignore
# Environment & Secrets
.env
*.env

# Virtual Environment
.venv/
venv/
env/

# Python Cache & Jupyter Checkpoints
__pycache__/
*.py[cod]
.ipynb_checkpoints/

# Vector stores & cache
.faiss/

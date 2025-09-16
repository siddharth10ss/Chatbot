# LunaLink AI Chatbot

## Overview
LunaLink is an AI-powered chatbot designed to provide intelligent responses, understand natural language, and interact with users through various modalities, including text, speech, and image processing. This project integrates a Python backend for core AI functionalities (NLU, OCR, text-to-speech) with a Next.js frontend for a rich user interface.

## Features
*   **Conversational AI:** Engage in natural language conversations.
*   **Natural Language Understanding (NLU):** Powered by Rasa, Regex, and Sentiment analysis for robust intent recognition and entity extraction.
*   **Optical Character Recognition (OCR):** Extract text from images and PDFs using Tesseract OCR.
*   **Text-to-Speech (TTS):** Convert chatbot responses into spoken audio.
*   **Speech-to-Text (STT):** (Implied by Mic button) Convert user's speech into text input.
*   **File Upload and Summarization:** Upload documents (images, PDFs) for text extraction and summarization.

## Prerequisites
Before you begin, ensure you have the following installed on your system:

*   **Git:** For cloning the repository.
*   **Python 3.9+:** For the backend services.
*   **Node.js (LTS recommended):** For the Next.js frontend.
*   **npm (Node Package Manager):** Usually comes with Node.js.
*   **Tesseract OCR:**
    *   **Installation:** Follow the instructions for your operating system from the official Tesseract GitHub page: [https://tesseract-ocr.github.io/tessdoc/Installation.html](https://tesseract-ocr.github.io/tessdoc/Installation.html)
    *   **Environment Variable:** Ensure the Tesseract executable is added to your system's PATH environment variable.

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/siddharth10ss/Chatbot.git
cd Chatbot
```

### 2. Backend Setup (Python)

1.  **Create and Activate a Virtual Environment:**
    ```bash
    python -m venv venv
    # On Windows
    .\venv\Scripts\activate
    # On macOS/Linux
    source venv/bin/activate
    ```

2.  **Install Python Dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Environment Variables:**
    Create a `.env` file in the root directory (`Yuva_Competition/`) and add any necessary environment variables for your backend services (e.g., API keys for Groq, Ollama, etc.). A `.env` file might look like this:
    ```
    GROQ_API_KEY=your_groq_api_key
    OLLAMA_API_BASE_URL=http://localhost:11434
    # Add other environment variables as needed
    ```

4.  **Run the Backend Server:**
    ```bash
    uvicorn main:app --reload
    ```
    The backend server will typically run on `http://127.0.0.1:8000` or `http://localhost:8000`.

### 3. Frontend Setup (Next.js)

1.  **Navigate to the Frontend Directory:**
    ```bash
    cd lunalink
    ```

2.  **Install Node.js Dependencies:**
    ```bash
    npm install
    ```
    *   **Troubleshooting `npm install` ERESOLVE errors:** If you encounter `ERESOLVE` errors related to conflicting peer dependencies (e.g., `react` versions), you can try running the installation with `--force` or `--legacy-peer-deps`. Be aware that `--force` can lead to an unstable dependency tree.
        ```bash
        npm install --force
        # OR
        npm install --legacy-peer-deps
        ```

3.  **Environment Variables:**
    Create a `.env.local` file in the `lunalink/` directory and add any necessary environment variables for your frontend (e.g., API endpoint for the backend).
    ```
    NEXT_PUBLIC_BACKEND_URL=http://localhost:8000
    # Add other environment variables as needed
    ```

4.  **Run the Frontend Development Server:**
    ```bash
    npm run dev
    ```
    The frontend application will typically run on `http://localhost:3000`.

## Usage
Once both the backend and frontend servers are running:
1.  Open your web browser and navigate to `http://localhost:3000`.
2.  You should see the LunaLink chatbot interface.
3.  Type your queries into the input field and press Enter or click the send button.
4.  Use the microphone button for speech input (if configured).
5.  Use the upload button to upload images or PDFs for text extraction and summarization.

## Known Issues / Troubleshooting

*   **`Mic is not defined` error:** This error indicates that the `Mic` component (likely from `lucide-react`) is not correctly imported or recognized in `src/app/dashboard/page.js`. Ensure all necessary icons are imported from `lucide-react`.
*   **`Expected 'from', got 'import'` syntax error:** This suggests a potential issue with how imports are structured in `src/app/dashboard/page.js`, possibly a mixed `export` and `import` syntax or an incorrect destructuring of imports. Review the file for correct JavaScript module syntax.
*   **Text-to-Speech (Speaker Button) Repetition:** The current implementation might be replaying the entire chat history. This needs to be debugged to ensure only the latest response is spoken and that the mute functionality works correctly.
*   **File Upload Functionality:** The file upload button currently extracts text to the clipboard. The goal is to integrate this extracted text into the chatbot's context for summarization or other operations, similar to how ChatGPT or Gemini handle file uploads. This requires further development to pass the extracted text to the backend for processing and then display the results within the chat interface.

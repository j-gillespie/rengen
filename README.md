# ACME Product Release Notes Generator

This project is an AI-powered release notes generator that runs entirely on your local machine. It requires no API key, and no data leaves your computer. It's a no-cost solution.

## How It Works
You provide the product name, version, release date, and paste raw engineering notes into the form. The app sends your input to a local AI model (running via Ollama), which sorts and formats it into a structured release notes document based on a standard template.

## Requirements

- [Ollama](https://ollama.com) — a free tool for running AI models locally
- A modern web browser (Chrome, Firefox, Edge, or Safari)
- No internet connection required after setup

## One-Time Setup

### 1. Install Ollama

Download and install Ollama for your operating system from <https://ollama.com>.

### 2. Pull the model

Open a terminal and run:

```
ollama pull gemma2:2b
```

This downloads the Gemma 2 2B model (~3 GB). You only need to do this once.


## Running the App

### 1. Start Ollama with browser access enabled

Ollama needs one extra flag to accept requests from a local HTML file. Open a terminal and run:

**Mac / Linux:**

```
OLLAMA_ORIGINS="*" ollama serve
```

**Windows (Command Prompt):**

```
set OLLAMA_ORIGINS=* && ollama serve
```

**Windows (PowerShell):**

```
$env:OLLAMA_ORIGINS="*"; ollama serve
```

Leave this terminal window open while using the app.

### 2. Open the app

Open `index.html` in your web browser; no local server is needed.

### 3. Generate release notes

To use the ACME Product Release Notes Generator:
1. Select a solution from the dropdown menu (options are hard-coded in index.html).
2. Enter the version number.
3. Select the release date.
4. Paste raw engineering notes into the Details area.
5. Click **Generate Release Notes**.

The generated release notes will appear below the form. Use the **Copy to Clipboard** button to copy the output.

Click **Clear** to reset all of the fields.

## Using a Different Model

If you prefer to use a model other than Gemma 2 2B, pull it with Ollama and update the `OLLAMA_MODEL` value near the top of the `<script>` block in `index.html`:

```js
const OLLAMA_MODEL = "llama3"; // change to "mistral", "llama3.2", etc.
```

Other models that work well for this task:

- `mistral` — fast, good at structured output
- `llama3.2` — smaller and faster than llama3, good for lower-memory machines
- `gemma2` — strong at following formatting instructions

## Troubleshooting

**“Could not connect to Ollama”**
Ollama is not running, or was started without the `OLLAMA_ORIGINS` flag. Stop it and restart using the command in Step 1 above.

**Output is blank or garbled**
The model may have timed out or run out of memory. Try a smaller model such as `llama3.2`, or close other applications to free up RAM.

**The page doesn’t load**
Make sure you are opening `index.html` directly in a browser. No local server or build step is required.

## File Structure

```
release-notes-generator/
├── index.html          — the app (form, styles, and API logic in one file)
├── README.md           — this file
└── sample-notes.txt    — example raw engineering notes for testing
```
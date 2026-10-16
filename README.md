# Super Investing AI Agent

## Overview
A Python-based AI research agent that analyzes a supplied research pack and generates an investment research brief for Sarvottam Cables Ltd (SRVCABLE), a fictional Indian company.

## Technology Stack
- Python
- Google Gemini 2.5 Flash
- OpenRouter API
- OpenAI Python SDK

## Project Structure

```text
Super-Investing-AI-Agent/
├── agent.py
├── system_prompt.md
├── README.md
├── TEST_LOG.md
├── research_pack/
└── runs/
```

## Setup and Installation

### 1. Clone the repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd Super-Investing-AI-Agent
```

Replace `YOUR_GITHUB_REPOSITORY_URL` with the repository's HTTPS URL.

### 2. Create and activate a virtual environment

**Windows PowerShell:**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Linux/macOS:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
python -m pip install openai
```

Install any additional third-party packages required by `agent.py`.

### 4. Configure your OpenRouter API key

Create an API key through OpenRouter. The agent reads the key from the `OPENROUTER_API_KEY` environment variable.

**Windows PowerShell:**

```powershell
$env:OPENROUTER_API_KEY = "YOUR_OPENROUTER_API_KEY"
```

**Linux/macOS:**

```bash
export OPENROUTER_API_KEY="YOUR_OPENROUTER_API_KEY"
```

Replace the placeholder with your own API key. Keep the key private and never commit it to GitHub.

The environment variable must be set in the terminal session used to run the agent.

## Run the Agent

From the project root, execute:

```bash
python agent.py SRVCABLE final
```

To run separate test cases, use different run names:

```bash
python agent.py SRVCABLE run1
python agent.py SRVCABLE run2
python agent.py SRVCABLE run3
```

The agent reads the Markdown documents from `research_pack/`, follows the instructions in `system_prompt.md`, calls the LLM through OpenRouter, and saves the generated report and validation log in `runs/`.

## How It Works

1. Loads the supplied Markdown research documents.
2. Assigns source IDs for traceable citations.
3. Uses the system prompt to guide source evaluation, entity matching, and financial discrepancy analysis.
4. Generates a structured research brief using Google Gemini 2.5 Flash through OpenRouter.
5. Runs validation checks on the generated report.
6. Saves the report and validation log in `runs/`.

## Testing

Three test runs were conducted:

- **Run 1:** Baseline prompt.
- **Run 2:** Improved source handling through system-prompt changes.
- **Run 3:** Improved validation through code changes.

See `TEST_LOG.md` for the test results and limitations.

## Model Used

Google Gemini 2.5 Flash, accessed through OpenRouter using the OpenAI Python SDK.

Why: Selected for its ability to synthesize multiple documents, follow structured prompts, identify conflicting financial figures, and generate concise research reports.


## Limitations

- SRVCABLE is fictional, and the agent relies on the supplied research documents.
- The agent does not independently verify claims online.
- Automated validation cannot guarantee factual accuracy or citation correctness.
- URLs using the reserved `.example` domain are placeholders, not verified working links.
- API or network failures can interrupt report generation.
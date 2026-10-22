<div align="center">
  <img src="assets/moodlens-mark.svg" alt="MoodLens logo" width="96">
  <h1>MoodLens</h1>
  <p>Understand the emotion behind every message.</p>

  <a href="https://www.python.org/"><img src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python 3.10 or newer"></a>
  <a href="https://flask.palletsprojects.com/"><img src="https://img.shields.io/badge/Flask-3.0-000000?style=flat-square&logo=flask&logoColor=white" alt="Flask 3.0"></a>
  <a href="https://www.ibm.com/watson"><img src="https://img.shields.io/badge/IBM%20Watson-NLP-1261FE?style=flat-square&logo=ibm&logoColor=white" alt="IBM Watson NLP"></a>
  <a href="https://github.com/PVegananda/oaqjp-final-project-emb-ai/commits/main"><img src="https://img.shields.io/github/last-commit/PVegananda/oaqjp-final-project-emb-ai?style=flat-square" alt="Last commit"></a>
  <a href="https://github.com/PVegananda/oaqjp-final-project-emb-ai"><img src="https://img.shields.io/github/repo-size/PVegananda/oaqjp-final-project-emb-ai?style=flat-square" alt="Repository size"></a>
</div>

## Overview

MoodLens is a lightweight Flask application that turns text into a clear emotional
profile. It uses IBM Watson Natural Language Understanding to score anger, disgust,
fear, joy, and sadness, then highlights the dominant emotion through a focused web
experience and a JSON API.

The project is intentionally small, readable, and easy to extend. It is a practical
example of connecting a Python web service to a natural-language intelligence API.

## Highlights

- A clean browser interface for quick emotion analysis
- JSON API endpoint for integrating analysis into other applications
- Consistent response format with five emotion scores and a dominant emotion
- Health check endpoint for deployment monitoring
- Input validation and explicit handling of upstream API errors
- Unit tests for the analyzer's input and response behavior

## Getting started

### Requirements

- Python 3.10 or newer
- An IBM Watson Natural Language Understanding instance

### Installation

```bash
git clone https://github.com/PVegananda/oaqjp-final-project-emb-ai.git
cd oaqjp-final-project-emb-ai
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Set `WATSON_NLP_URL` and `WATSON_AUTHORIZATION` in your environment before starting
the application. Keep credentials out of source control.

### Run locally

```bash
python app.py
```

Open <http://localhost:5000> in your browser.

## API

### `POST /emotions`

Analyze text by sending a JSON body with the `textToAnalyze` field:

```bash
curl -X POST http://localhost:5000/emotions \
  -H "Content-Type: application/json" \
  -d '{"textToAnalyze":"I am excited about the possibilities."}'
```

Example response:

```json
{
  "anger": 0.001,
  "disgust": 0.002,
  "fear": 0.004,
  "joy": 0.94,
  "sadness": 0.003,
  "dominant_emotion": "joy"
}
```

### `GET /health`

Returns `{"status": "healthy"}` when the service is available.

## Python usage

```python
from emotion_analyzer import emotion_detector

result = emotion_detector("This is a wonderful day.")
print(result["dominant_emotion"])
```

## Development

Run the tests:

```bash
python -m pytest test_emotion_analyzer.py -v
```

Run static analysis:

```bash
pylint emotion_analyzer.py app.py
```

## Project layout

```text
.
├── app.py                 # Flask routes and application entry point
├── emotion_analyzer.py    # Watson NLP integration
├── test_emotion_analyzer.py
├── templates/index.html   # Browser interface
├── assets/moodlens-mark.svg
└── requirements.txt
```

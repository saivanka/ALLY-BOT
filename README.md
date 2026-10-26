# ALLY-BOT

A chatbot web app built with ChatterBot and Flask. It greets visitors as a medical chatbot, answers messages from a trained model, and saves each conversation to a numbered file.

## What it does

- `app.py` runs a Flask app with three routes:
  - `/` serves `home.html`
  - `/index` serves `index.html`
  - `/get?msg=...` returns the bot's reply to the given message
- The bot is a ChatterBot `ChatBot('Bot')` using the SQL storage adapter and the BestMatch logic adapter, so replies come from its trained database (`db.sqlite3`).
- Every conversation is written to a numbered file in `saved_conversations/`, starting with the bot's greeting.
- `train.py` rebuilds the bot's knowledge: it deletes the old `db.sqlite3` if one exists, then trains the bot on every conversation file in `data/` using a ListTrainer.

## Tech stack

- Python 3 with Flask 2.0.2 (served with gunicorn in production, per `Procfile`)
- ChatterBot 1.0.4 with the chatterbot-corpus package, NLTK and scikit-learn
- SQLite storage (`db.sqlite3`)
- HTML templates in `templates/` and static assets in `static/`

## How to run

```bash
pip install -r requirements.txt
python train.py   # rebuilds db.sqlite3 from the files in data/
python app.py
```

Then open the app in your browser and send a message; the bot replies through the `/get` endpoint.

## Project structure

```
app.py                # Flask app: home/index pages and the /get chat endpoint
train.py              # Trains the bot on the conversation files in data/
data/                 # Conversation files used for training
templates/            # home.html, index.html
static/               # Static assets for the web pages
saved_conversations/  # Numbered files holding past conversations
db.sqlite3            # Trained bot database (SQLite)
requirements.txt      # Python dependencies
Procfile, runtime.txt # Deployment configuration
```

## Status

An older project (Python 3.6-era dependencies) that still runs as a self-contained chatbot demo. It is a general-purpose trained chatbot, not a substitute for professional medical advice.

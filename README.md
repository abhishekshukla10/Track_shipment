# Track Shipment — RAG Logistics Chatbot

🔗 **Live Demo:** [trackshipment.streamlit.app](https://trackshipment.streamlit.app)

Natural-language shipment tracking in **Hindi, English & Hinglish** — built for how Indian logistics actually communicates.

---

## Business Problem

Logistics teams waste hours on manual shipment status calls. Language barriers across Hindi / English / Hinglish create friction in last-mile operations — a driver's dispatcher asks *"Tata Motors ka shipment kahan hai?"* and no dashboard understands the question.

## Solution

A RAG pipeline that accepts natural-language queries in any of the three languages, parses intent, queries live shipment data, and responds conversationally — 24/7, no human support needed.

## How It Works

```
User Query (Hindi/English/Hinglish)
        ↓
Intent Parser — Groq LLM → 5 intents, 7 entities → structured JSON
        ↓
SQL Lookup — Supabase PostgreSQL (shipments, trips, events)
        ↓
Response Generator — Groq Llama 3.3-70B narrative reply
        ↓
Streamlit UI — session memory for multi-turn context
```

## Key Technical Decisions

- **Intent parsing before retrieval** — a lightweight LLM classification step (5 intents, 7 entities) converts messy multilingual input into structured queries, making SQL retrieval deterministic instead of embedding-search fuzzy
- **Session memory** — conversation context maintained across turns so follow-ups like *"aur uska ETA?"* resolve against the previous shipment
- **Supabase over local DB** — cloud PostgreSQL keeps the demo stateless and deployable on Streamlit Cloud

## Business Impact

- Eliminates manual status calls · 24/7 self-service
- Zero language barrier — Hindi / English / Hinglish native
- Scales to thousands of shipments instantly

## Stack

`Python` `Groq Llama 3.3-70B` `LangChain` `Supabase (PostgreSQL)` `Streamlit` `psycopg2`

## Setup

```bash
git clone https://github.com/abhishekshukla10/track-shipment
cd track-shipment
pip install -r requirements.txt
cp .env.example .env   # add your keys
streamlit run app.py
```

**.env.example**
```
GROQ_API_KEY=
SUPABASE_URL=
SUPABASE_KEY=
```

## Roadmap

→ Logistics Command Center — proactive delay alerts, predictive ETAs, carrier performance intelligence

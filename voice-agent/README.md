# Coldroom — Live Conversation Trainer

A single-file, browser-based trainer for **any high-stakes conversation**. You
configure who you're up against, run a **live voice call** powered by a real
language model, then get the call **graded against a scenario-specific rubric**
with progress tracking, an AI-generated **development plan**, and an exportable
**progress report**.

It's one self-contained `index.html` — no build step, no server, no dependencies.

## Scenario types

Not just sales. Pick one and it sets the counterpart and the rubric you're scored on:

- **Sales** — discovery, negotiation, closing, security / vendor review
- **Fundraising** — investor meeting, term-sheet negotiation
- **Interviews** — job interview (you're the candidate), executive / panel interview
- **Negotiation** — salary / offer negotiation
- **Media** — press / media interview
- **Custom** — define your own counterpart and objective

Each scenario type has its own rubric (e.g. discovery scores questioning &
qualification; negotiation scores anchoring, concessions & composure; interviews
score STAR structure & evidence), so your progress is tracked coherently per type.

## What's new in this version

- **Any scenario, not just sales calls** — with matching rubrics per type.
- **Much better voices** — the browser voice list is now ranked to surface your
  system's best neural/online voices first (marked ★). For genuinely natural
  speech, switch the **Voice engine** to **OpenAI TTS** or **ElevenLabs** and
  paste that provider's key — a big quality jump.
- **Hands-free** — automatic speaker detection. Speak, pause, and it sends on its
  own (no clicking). Tune the auto-send silence threshold in setup. Half-duplex,
  so the customer's voice never gets transcribed as you. You can toggle hands-free
  off, or type, any time.
- **Progress & Development tab** — score-over-time chart, per-scenario breakdown,
  a **Generate plan** button that synthesises your whole history into prioritised
  development areas with drills and a two-week plan, and **Export report** which
  writes a self-contained HTML you can open anywhere or publish as an artifact.

## Running it

Open it over `http(s)://` (not `file://`) so the microphone works:

```bash
cd voice-agent
python3 -m http.server 8000
# then visit http://localhost:8000
```

Or deploy the folder anywhere static (GitHub Pages, Netlify, etc.).

**Browser:** use **Chrome or Edge** for hands-free voice (Web Speech API). Other
browsers fall back to typing; the counterpart still speaks their replies.

## Setup inside the app

1. **Choose the conversation** — pick a scenario type, optionally a quick-start,
   then edit the person opposite (role, context, stance, disposition, personality,
   difficulty) and your objective.
2. **Add your Anthropic API key** — stored only in this browser, sent only to
   `api.anthropic.com`. Get one at [console.anthropic.com](https://console.anthropic.com/).
3. **Pick voice & mic** — browser voices (free) or a premium engine (OpenAI /
   ElevenLabs, separate key). Set pace and the auto-send silence threshold.
4. **Start** — talk hands-free or type. The counterpart stays in character and
   only gives ground when you earn it.
5. **End & grade** — an independent pass scores the transcript, gives "do more /
   do less" coaching and a focus for next time. Everything is saved locally.
6. **Progress tab** — watch your trend, generate a development plan, export a report.

## Privacy

Everything lives in your browser (`localStorage`). Your Anthropic key, any voice
key, personas, history, and plan never leave the device except as API calls to
Anthropic (and, if you enable premium voices, to OpenAI/ElevenLabs). Add keys only
through the in-app fields — never hard-code them into the file, especially in a
public repo.

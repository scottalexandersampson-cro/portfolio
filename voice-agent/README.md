# Coldroom — Mock Customer Call Trainer

A single-file, browser-based **sales training simulator**. You configure a mock
customer (their role, awareness, context, personality, and disposition), run a
**live voice call** against them powered by a real language model, then get the
call **graded against a discovery rubric** with progressive tracking across every
call you make.

It's one self-contained `index.html` — no build step, no server, no dependencies.

## Why it's a standalone app and not a hosted artifact

Real, live conversation needs the page to call a language model at runtime.
A published claude.ai artifact runs under a strict content-security policy that
blocks all external network calls, so it can't reach a model. This app instead
runs locally in your browser and calls the **Anthropic Messages API** directly
with your own key — which is what makes the live conversation and grading work.

## Running it

Because browsers restrict microphone access to secure contexts, open it over
`http(s)://` rather than `file://`:

```bash
cd voice-agent
python3 -m http.server 8000
# then visit http://localhost:8000
```

Or deploy the folder anywhere static (GitHub Pages, Netlify, etc.) and open it there.

**Browser:** use **Chrome or Edge** for voice — they support the Web Speech API
for speech-to-text. In other browsers the mic falls back to a text box, and the
customer still speaks their replies aloud.

## Setup inside the app

1. **Brief the customer** — pick a quick-start persona or fill in the fields
   (name, role, company context, awareness, disposition, personality, scenario,
   difficulty) plus a line on what you're selling.
2. **Add your Anthropic API key** — stored only in this browser's local storage,
   sent only to `api.anthropic.com`. Get one at
   [console.anthropic.com](https://console.anthropic.com/).
3. **Pick models** — the conversation defaults to a fast model (voice feels best
   with low latency); grading defaults to a more rigorous one. Both are your choice.
4. **Start the call** — talk (hold-to-talk mic) or type. The customer stays in
   character, only reveals information when you earn it, and raises realistic
   objections that fit their disposition and difficulty.
5. **End & grade** — an independent grading pass scores the whole transcript on
   seven discovery dimensions, gives an overall score, "do more / do less"
   coaching, and a single focus for next time. Your scores are saved locally and
   charted so you can see whether you're actually improving.

## The rubric

Rapport & opening · Discovery & questioning · Active listening · Pain & value ·
Qualification · Objection handling · Control & next steps — each scored 1–5, plus
a 0–100 overall and per-dimension trend across your call history.

## Privacy

Everything lives in your browser. Your API key, persona, preferences, and call
history are kept in `localStorage`. Transcripts are sent to the Anthropic API
only to generate the customer's replies and the grade; nothing is stored anywhere
else. Clear it any time via your browser's site-data settings.

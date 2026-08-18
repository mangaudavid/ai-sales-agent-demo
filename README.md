# AI sales agent that refuses to invent stock or price

A catalog-grounded sales agent running **entirely in the browser** — no backend, no API keys, no network calls after page load.

**Live demo:** https://mangaudavid.github.io/ai-sales-agent-demo/

## What it does

Answers technical buying questions over a 75-product catalog (pool equipment, synthetic data) and **visibly refuses** when the answer isn't in the catalog. The refusal path is a first-class feature, not an error state.

- **Retrieval** — BM25 lexical scoring (k1=1.5, b=0.75) combined with structured constraint extraction (volume, voltage, phase, port size, budget, turnover rate)
- **Rule engine** — pump sizing with head-loss margin, port matching, electrical phase compatibility, dependency chains, discontinued → replacement
- **Guardrails** — refuses invented model codes, refuses to negotiate price, refuses off-topic and prompt-injection attempts
- **"Under the hood" panel** — live retrieval scores per query, so you can verify nothing is scripted
- **Eval modal** — includes two tests that still fail, with explanations

## Why it's built this way

The failure mode that kills adoption isn't bad UX — it's an agent confidently inventing a price or a stock level. In the EU that is now a legal liability (Air Canada precedent). So the demo puts the refusal on screen instead of hiding it.

The catalog is synthetic and the brands are fictional, following the same approach Google uses with "Cymbal Shops" for its own public shopping-AI demo. The specifications are physically correct — that's what matters, not the names.

No LLM runs in this demo; composition is deterministic and anchored to retrieved fields. Production systems I ship do use an LLM, with the same grounding guarantees.

## About

Built by David Mangău — David Digital Dynamics. I build production AI sales assistants that answer only from a client's live product catalog: hybrid retrieval, three-layer guardrails, and an adversarial test harness so they never invent stock or price. Self-hosted, AI Act / GDPR compliant, client owns the code.

Previously: an assistant handling 12,300+ messages at 99.92% accuracy, and a second production system at 97.7% retrieval accuracy against a 224-case adversarial suite.

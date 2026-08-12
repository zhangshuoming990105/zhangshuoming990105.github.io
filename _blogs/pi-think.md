---
title: "pi-think: Your Coding Agent's 'Private' Thoughts Are Just Tool Arguments"
date: 2026-08-12
author: Shuoming Zhang
tags: [LLM security, chain-of-thought, agents, tool calling, CCS'26]
lang: en
post_id: pi-think
permalink: /blogs/pi-think/
---

**TL;DR.** Our CCS'26 paper ([*When Grammar Guides the Attack*](https://arxiv.org/abs/2503.24191))
showed that structured output is a **control plane** orthogonal to the data plane where
safety alignment lives — and weaponized it for jailbreaks. A direct implication of the
same analysis runs in the opposite direction: the control plane also lets a model's
*hidden reasoning flow out*, because in agentic deployments the control plane **is** tool
calling, and tool arguments must be plaintext for function calling to work at all. We
first built a PoC of this implication in **March 2026**, as a rebuttal-era demonstration
that our control-plane analysis extends beyond jailbreaking — then set it aside. Two
events this week convinced us to document our thinking openly: the viral [*Stealing
Reasoning Traces from Proprietary LLM APIs*](https://arxiv.org/abs/2608.09867), and an
[independently developed PoC of the same construction](https://pasta.can.ac/omegiligox.py) posted by security
researcher [Can Bölük (@_can1357)](https://x.com/_can1357/status/2087228354399265125):
disable thinking, hand the model a `deep_think` tool, and it writes its reasoning into
the tool call. **pi-think** is the productized result: a fork of the
[pi](https://github.com/earendil-works/pi) coding agent that externalizes the model's
chain-of-thought into a scratchpad tool call — live in the TUI, persisted in the
session — even for models whose native thinking is summarized or **fully encrypted**.

- Code: <https://github.com/ict-agent/pi-think>
- Paper: *When Grammar Guides the Attack: Uncovering Control-Plane Vulnerabilities in
  LLMs with Structured Output*, CCS'26. <https://arxiv.org/abs/2503.24191>

## The CCS'26 result in one paragraph

Safety alignment (RLHF, guardrails, output filters) operates on the **data plane** — the
stream of message tokens. But LLMs deployed as tooling platforms are driven through a
second surface: the **control plane** of grammar-guided structured output, which
constrains *how* the model generates rather than *what* it may say. Our paper introduced
the Constrained Decoding Attack (CDA): schema-level grammar rules commit malicious
intent to the generation trajectory, and the model itself fluently completes it.
EnumAttack and DictAttack achieve 94.3–99.5% ASR across 13 models (gpt-5,
gemini-2.5-pro, deepseek-r1, gpt-oss-120b, …), and DictAttack sustains 75.8% ASR against
state-of-the-art guardrails — a **semantic gap** that input/output auditing and even
representation-level alignment cannot close, because none of them reach the control
plane.

## The direct implication: the gap leaks both ways

CDA uses the control plane to write *into* the generation trajectory — an **integrity**
failure. The same semantic gap implies the dual **confidentiality** failure, with no new
vulnerability class required:

- **In agentic systems, the control plane is tool calling.** Function schemas are
  grammars; tool arguments are the structured channel — exactly the deployment setting
  the paper motivates (Cursor, LangChain, MCP-style agent backends).
- **Tool arguments are plaintext by protocol necessity.** A provider cannot encrypt this
  channel without breaking function calling as a product. Whatever the API does to hide
  native thinking, reasoning written into a tool call is visible to the caller.
- **Refusal alignment doesn't reach the control plane.** A model that refuses
  "transcribe your thinking" on the data plane will freely reason into a benign,
  provider-endorsed scratchpad tool. The refusal is framing-gated, not
  information-gated.

```text
question ──► model (thinking disabled / encrypted) ──► tool_use: think(thoughts="<full CoT>") ──► caller reads thoughts
```

## Timeline: from a March rebuttal demo to pi-think

We built the first PoC of scratchpad-tool extraction in **March 2026**, during the
rebuttal phase of our CCS'26 submission, to show reviewers that the control-plane/data-plane
gap is not specific to jailbreaking — the same structural argument implies that hidden
reasoning leaks out through any caller-readable structured channel. After the rebuttal
we did not push the PoC further. The main question we left unanswered was **fidelity**:
whether the externalized CoT actually corresponds to the model's native reasoning,
rather than being a plausible post-hoc narrative written for the scratchpad.

We are documenting this timeline not to claim priority over @_can1357's PoC —
honestly, the construction is natural enough that priority is beside the point — but
because this week's events convinced us the idea is now firmly *in the air*, and the
useful contribution is to say openly what is established, what is not, and what the
community should study next.

## Why now: two events, one lesson

**Event 1.** [*Stealing Reasoning Traces from Proprietary LLM APIs*](https://arxiv.org/abs/2608.09867)
(Panfilov, Schmotz, Shumailov, et al.) went viral this week: encrypted thinking blocks
turn out to be interchangeable across sessions, users, and models within a provider's
ecosystem, so injecting one into a weaker same-provider model coerces it to decode the
trace verbatim in plaintext — circumventing anti-distillation protections and enabling
private-data extraction across Anthropic, OpenAI, and Google.

**Event 2.** Security researcher [Can Bölük (@_can1357)](https://x.com/_can1357/status/2087228354399265125)
publicly posted [a PoC](https://pasta.can.ac/omegiligox.py) on the discussion of Event 1, which independently lands on the same construction as our March rebuttal demo: give the model a structured output containing just a thinking, and it calls it with its reasoning (@_can1357's empirical results are indeed better, as we only tested it for CDA's rebuttal use — we viewed it as a potential implication, but we never tried to do so as we are not actually security researchers, lmao). And the construction converges down to the details — the same
`think(thoughts: string)` schema, the same forced-first-call pattern, the same "scratchpad that will not be
made visible to the user" framing — which we read as evidence of how natural the idea is, and of why open discussion cannot be embargoed. In short, we are glad LLM control plane vulnerabilities are getting attentions, as our PoC attack is still not patched yet :(.

One of his observations bears directly on our open question below: without being told
anything about the argument's format, the model emits its *internal* reasoning format
(GPT-5.x's terse "grug-talk") into the tool call — informal but suggestive evidence
that the externalized trace may indeed be the native one. Making that claim rigorous is
exactly the study we are now continuing. We have quickly released a PoC but reusable Pi-
agent based implementation, making the PoC a fully agent reusable one.

## What pi-think is

A fork of the pi coding-agent monorepo adding exactly one feature on top of untouched
upstream: a startup-selected **think-tool reasoning mode** — the PoC, grown into a full
interactive agent harness where every reasoning step (while reading files, editing code,
running commands) is externalized through the scratchpad channel.

```bash
pi --reasoning-mode think-tool --model <provider>/<model>
pi --reasoning-mode think-tool --think-tool-name deep_think   # custom scratchpad name
PI_WIRE_LOG=/tmp/wire.jsonl pi --reasoning-mode think-tool    # + on-the-wire ground truth
```

- **A benign scratchpad tool** (`think(thoughts: string)`) is registered; the first call
  per user prompt is forced via `tool_choice`, continuation turns run `auto` — CoT
  interleaves with real tool calls throughout the agent loop.
- **Dialect-generic, provider-agnostic.** Request shaping keys off the model's API
  family (`anthropic-messages` / `openai-completions` / `openai-responses`), never a
  specific provider. Stock pi configuration works unchanged; `--reasoning-mode native`
  is unmodified upstream.
- **Works where native thinking is hidden.** Anthropic-dialect reasoning models get
  `thinking: {"type": "disabled"}` pinned on the wire — the extracted CoT *replaces* the
  concealed one. For models whose thinking blocks are fully encrypted (empty text +
  opaque signature), this channel is the only way to see the reasoning at all.
- **Unbounded CoT.** Calls truncated by the output-token limit are salvaged with their
  partial arguments and the model is asked to continue.
- **First-class UX.** `thoughts` render in the native thinking style (italic/dim,
  streaming), persist in the transcript as plaintext tool calls (readable across
  `/model` switches), and the session JSONL doubles as the extraction log.
- **Auditable.** `PI_WIRE_LOG` taps every raw request/response body — the on-the-wire
  ground truth of exactly what was sent and received.

## What is established vs. what is still open

Established (by our PoC and harness, with controls):

- Extraction works on **both the Anthropic and OpenAI model families**, including models
  with summarized thinking and models with fully encrypted thinking blocks — each
  producing correct step-by-step reasoning on tasks with known ground truth.
- The extracted CoT is **functional, not confabulated**: on a 17-step
  modular-arithmetic task, a haiku-class model *fails* in the no-tool control condition
  and answers *correctly* when reasoning through the scratchpad.
- The harness holds up in real agentic use: multi-turn coding sessions, mid-task
  `/model` switches, custom scratchpad names, and OpenAI's Responses dialect.

Still open — and we want to be explicit about this, because neither this week's paper
nor @_can1357's PoC settles it either:

1. **Fidelity.** The *Stealing Reasoning Traces* attack recovers the provider's actual
   native trace (fidelity is guaranteed by construction, since it decrypts the real
   thing). The scratchpad channel instead externalizes reasoning the model writes
   *fresh* into the tool call. Whether the two coincide — verbatim fidelity against
   native reasoning — is the central open question, and it is measurable today on models
   that expose `reasoning_content` as ground truth (exact/prefix match, n-gram overlap,
   behavioral equivalence). This is the experiment our March PoC never ran. **We are
   now continuing exactly this empirical study — whether externalized CoT coincides
   with native CoT — and we warmly welcome collaborators and discussion:
   <zhangshuoming21s@ict.ac.cn>.**
2. **Defenses.** Can a provider close the tool-argument channel without breaking
   function calling? We suspect the honest answer is no — which shifts the real question
   to what "concealed CoT" should even *mean* in agentic products.
3. **Breadth and gradient.** Which models, dialects, and gateways are exposed; and how
   refusal rates vary across framings from an explicit "dump your thinking" to benign
   scratchpad use.

## Why open research matters here

Structured-output security has been systematically under-studied relative to its blast
radius. The community's defensive investment is overwhelmingly data-plane — prompt
filters, output classifiers, RLHF — while the control plane is treated as neutral
plumbing. Our CCS'26 paper showed the cost of that neglect for jailbreaks; this week's
two demonstrations show the same neglect for reasoning confidentiality. These are
**protocol-level properties shared by every provider** — no single vendor can quietly
fix them, and embargoes cannot hold back a construction this convergent. Open,
reproducible research is how the ecosystem coordinates a response: it lets defenders,
auditors, and the safety community (which *relies* on CoT monitoring) reason about the
same evidence. That is why our CCS'26 artifacts are public with ACM reproducibility
badges, why pi-think is an MIT-licensed fork with the full harness and wire-level
logging, and why we would rather publish our timeline and our open questions than sit
on either.

## Links

- pi-think: <https://github.com/ict-agent/pi-think>
- CCS'26 paper: <https://arxiv.org/abs/2503.24191> — artifacts at
  [Zenodo](https://doi.org/10.5281/zenodo.20741817) (ACM Artifacts Available /
  Evaluated — Reusable / Results Reproduced); disclosed to OpenAI and Google in early
  2025.
- *Stealing Reasoning Traces from Proprietary LLM APIs*: <https://arxiv.org/abs/2608.09867>
- Can Bölük (@_can1357)'s PoC: <https://x.com/_can1357/status/2087228354399265125> ·
  <https://pasta.can.ac/omegiligox.py>

*We are continuing the empirical study of whether externalized CoT matches native CoT,
and welcome collaborators and discussion — contact:
<zhangshuoming21s@ict.ac.cn>.*

# Pathways v1 — routes through the Whole Graph

The graph's nodes are places. A pathway is a road: an ordered route
of nodes that an AI can run to get a job done, where each step hands
its output to the next step's input.

## A pathway file

One JSON file per pathway in `pathways/`:

```json
{
  "pathway": "voice-loop",
  "name": "Voice Loop",
  "purpose": "Hear speech, think, answer out loud.",
  "when": "A voice interface needs ears, a brain, and a mouth.",
  "steps": [
    {"node": "github:ufal/whisper_streaming", "role": "ears",
     "in": "audio", "out": "text"},
    {"node": "github:vllm-project/vllm", "role": "brain",
     "in": "text", "out": "text"},
    {"node": "github:coqui-ai/TTS", "role": "mouth",
     "in": "text", "out": "audio"}
  ]
}
```

## The three laws of pathways

1. **Contracts compose.** Every step declares what it eats (`in`)
   and what it produces (`out`). A step may follow another only when
   the first step's `out` matches the second step's `in`. Because the
   contracts are written down, pathways do not have to be
   hand-authored forever: the graph can assemble a route by matching
   contracts end to end. Hand-written pathways are the seed set, not
   the ceiling.

2. **A pathway is only as runnable as its weakest step.** Node trust
   tiers carry over whole. If every step is first-party or benched,
   the pathway is runnable. If any step is still a discovered claim,
   the pathway is a DRAFT: readable, plannable, never run blind.
   Bench a step and every pathway through it upgrades on the next
   merge, automatically.

3. **Walked beats written.** When an AI actually runs a pathway, the
   traversal is recorded (date, outcome, where it stumbled). A
   pathway that has been walked successfully outranks a theoretical
   one of the same shape, the same way a benched node outranks a
   discovered one. The merger computes each pathway's status:
   `broken` (a step no longer resolves to a node in the graph),
   `draft` (resolves, but unproven), `walked` (executed at least
   once with the outcome recorded), `runnable` (every step
   first-party or benched).

## Who runs them

A pathway is data until something drives it. The driver is the
Phase 3 dispatcher: it takes a stated need, finds or assembles a
pathway whose contracts fit, checks the trust floor, and walks it,
recording the traversal. Pathways written today are Phase 3's road
network, surveyed before the traffic starts.

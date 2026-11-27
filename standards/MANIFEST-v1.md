# Brain Map Manifest Standard v1 (Phase 1, Nov 26, 2026)

Every repo that joins the GitHub Brain Map carries ONE manifest file at
its root: `brainmap.json`. It is the node's herald in written form: what
this repo is, what it can do, and how much it has been verified.

```json
{
  "brainmap": 1,
  "node": "owner/repo",
  "name": "Plain Name",
  "kind": "tool | service | site | library | social-lane | registry",
  "does": "One sentence, plain words: what this node does.",
  "capabilities": [
    {
      "id": "make-pdf",
      "takes": "html or markdown text",
      "gives": "a PDF file",
      "invoke": "workflow_dispatch: make-pdf.yml",
      "cost": "free"
    }
  ],
  "peers": "brainmap-peers.json",
  "license": "MIT",
  "trust": "first-party | member | discovered",
  "bench": {
    "status": "passed | queued | untested",
    "last": "YYYY-MM-DD",
    "report": "path or URL to the bench record"
  },
  "access": "public | dispatch-with-permission | estate-only",
  "keys": "none-in-repo"
}
```

Rules:
- `keys` is ALWAYS "none-in-repo". A manifest never contains a password,
  token, or secret of any kind. It points; it never holds. Credentials
  live in the Secure Vault / estate connectors, nowhere else.
- `trust` starts at "discovered" for anything found by the waterfall.
  Only a bench pass moves a node up, and trust never travels along a
  peer link.
- `does` and capability names are plain and on-the-nose (public naming
  rule). No internal codenames in a published manifest.
- A node whose manifest lies about a capability loses its tier on the
  first failed verification and is flagged in the index.

# Link File Standard v1 (same phase)

`brainmap-peers.json` at the repo root:

```json
{
  "brainmap_peers": 1,
  "knows": [
    {"node": "owner/repo", "why": "one line: what it is good for"},
    {"node": "other-owner/other-repo", "why": "one line"}
  ]
}
```

Rules:
- Links are discovery only. Following one grants nothing but knowledge
  that the node exists and what it claims to do.
- Cycles are fine (the crawler keeps a visited set and a depth budget;
  bounded searches rule applies).
- A peer entry is an opinion, not an endorsement. The index records who
  pointed at whom, so a bad pointer source is visible.

# Herald / Watchdog Spec v1 (same phase)

- Member repos: a scheduled GitHub Action ("herald") that refreshes the
  manifest's `last_seen` in the registry index and answers capability
  calls routed by dispatch.
- Non-member repos: no resident herald is possible; estate scouts check
  liveness and manifest drift from outside on the crawler cycle.
- A node silent past two crawler cycles is marked STALE in the index.
  Stale nodes are never selected to fill a need until they answer again.

# What connects (Robert's order, Nov 26, 2026)

- His GitHub repos (founding nodes, first-party tier).
- His web pages: the .com flagship and every free-tier site. Each site
  repo carries a manifest; live sites also expose their toolbox tools
  as named capabilities (invoke = the estate's gated pipeline, keys stay
  home).
- His social media: manifests describe the LANES (which platform, what
  the lane can do) and point at the estate connectors. The map never
  holds a social login or token; an AI asking the map for a social
  action is routed to the estate side, where Robert's connectors and
  permissions decide. The map is a roadmap, never a keyring.
- Other people's repos: discovered tier, claim-only, per the blueprint.

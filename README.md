# The Brain Map

A public registry of tools and capabilities that any AI can read.

Every node in this map carries a small file that says what it does, who
it knows, and how it was verified. Connect an AI to this repository and
it can find a tool for a job the way you would ask a room: state the
need, and the map answers with who can fill it, how good they are
proven to be, and what it costs.

## How to use this map

1. Read `index.json` for the whole map, or fetch one file from
   `shards/` named for the capability you need (for example
   `shards/make-pdf.json`) to see only the nodes that offer it.
2. Check the node's `trust` and `bench` fields before relying on it.
   "discovered" means found, not verified. "passed" means it was
   tested and the test is on record.
3. A node's own `brainmap.json` is the source of truth for what it
   does. Its `brainmap-peers.json` lists the nodes it knows about, on
   any account. Follow those links and the map grows.

## The rules of the map

- **Pointers, never keys.** No manifest ever holds a password, token,
  or secret. Capabilities that need an account are routed through
  their owner's own systems, where their permissions decide.
- **Trust is earned per node.** A bench pass belongs to the node that
  passed it. Trust never travels along a link.
- **Grades decay.** A node that stops answering, or stops passing its
  own test, slides down. The map would rather say "stale" than lie.
- **Unfilled needs become wants.** Needs nobody can fill are filed on
  the wanted board (this repo's issues, label `wanted`), where
  builders can see real demand.

## Joining the map

Add a `brainmap.json` to your repository root following
`standards/MANIFEST-v1.md`, and a `brainmap-peers.json` pointing at
the nodes you know. That is all it takes to be discovered. Verification
is a separate step, and it is earned by test, not by asking.

Built and maintained by Dimon Global Group. The map is the public
layer; the systems behind the nodes are their owners' own.

# Changelog

All notable changes to the Synod examples. Versions share MAJOR.MINOR with the language.

## v0.3.0 — 2026-10-29

Implements Synod 0.3; works with compiler v0.3.0: `synod.mod` says `synod 0.3`. The programs are unchanged except `paxos` (below) and `ringlook`, whose wheel is `look.Circle 200` to match `look.Orbit` on the 1040 by 650 canvas.

### Changed

- `paxos` is correct under crash and restart: an acceptor writes `Promised` before it sends a Promise, and `Promised`, `AcceptedBallot` and `AcceptedValue` before it sends Accepted; a proposer writes `round` before it sends Prepare; `define [n: Node] start` reads them back with `disk.Read`. Before, `sim.Restart` reset these fields and two values could be chosen. The demo (seed 105) tells the same story; its trace gains `disk.Written` events.
- `ringlook` draws each node as a small disc at its first token, over the marks of all its tokens, with the node's keys listed in a column beside it (each key below the last key of its owner), so keys never stack and the marks lie under the discs.
- `ringlook` redraws every node's key slot when a node joins, so a placement round after a join starts each column at its owner again instead of continuing below the last key.

## v0.2.1 — 2026-10-22

Implements Synod 0.2; works with compiler v0.2.5.

### Changed

- Every demo's `lesson.Ask` now uses `choosing {…}` with three or four choices, so Predict mode can offer them. The questions are unchanged. One choice is what `synod run --summary` shows; the others are plausible misconceptions.
- The README summary excerpt shows the `Choices` of `lesson.Asked`.

## v0.2.0 — 2026-10-22

Implements Synod 0.2.

### Added

- Nine runnable programs in one module (`github.com/synodlang/examples`): tcp, gossip, paxos, raft, twopc, ring, cassandra, webapp and wal.
- Two look packages, raftlook and ringlook, that draw the raft and ring scenes.
- Demo seeds chosen so each run tells its story (cassandra uses seed 3).
- A README that walks through every example, explains the name and honours Leslie Lamport.
- `vendor/` is git-ignored.

### Changed

- Rewritten for specification v0.2.1: explicit receivers, `define main` and `define [n: Node] start`, typed collections and node effects that name their node.

# Changelog

All notable changes to the Synod examples. Versions share MAJOR.MINOR with the language.

## Unreleased

Implements Synod 0.3: `synod.mod` says `synod 0.3`. The programs are unchanged except `ringlook`, whose wheel is `look.Circle 200` to match `look.Orbit` on the 1040 by 650 canvas.

### Changed

- `ringlook` draws each node as a small disc at its first token, over the marks of all its tokens, with the node's keys listed in a column beside it (each key below the last key of its owner), so keys never stack and the marks lie under the discs.

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

# Examples

Canonical sample programs. They form one module,
`github.com/synodlang/examples`. Each behaviour package folder holds a
`demo.synod` main file (`# package main`) next to the library;
`webapp/demo.synod` is a pure program in a folder of sub-packages.

| Folder | Topic | What to watch | Run |
| --- | --- | --- | --- |
| `tcp` | TCP three-way handshake | SYN, SYN-ACK, ACK and the state changes on both ends | `synod run ./tcp` |
| `gossip` | Gossip membership and failure detection | Heartbeats spreading; a crashed node marked down after 4s; generations after restart | `synod run ./gossip` |
| `paxos` | Single-decree Paxos (the Synod protocol) | Two racing proposers; the higher ballot adopts any accepted value; the invariant "at most one chosen value" | `synod run ./paxos` |
| `raft` + `raftlook` | Raft leader election | Randomized timeouts, votes, a leader crash, a new term; "never two leaders in a term" | `synod run ./raft` |
| `twopc` | Two-phase commit | The blocking problem when the coordinator crashes between phases; the atomicity invariant | `synod run ./twopc` |
| `ring` + `ringlook` | Consistent hashing with virtual nodes | Which keys move when a fifth node joins | `synod run ./ring` |
| `cassandra` | A Cassandra-style cluster: gossip + ring + replication factor 3 + QUORUM + hinted handoff | A write succeeding with a replica down, and the hint replayed after restart | `synod run ./cassandra` |
| `webapp` | Cache-aside behind a load balancer (`api`, `lb`, `app`, `cache`, `db`) | Hit rate warming up; what happens when the cache crashes and there is no timeout | `synod run ./webapp` |
| `wal` | Write-ahead log and checkpoint recovery | Which writes survive a crash between checkpoints | `synod run ./wal` |

## Why Synod

Synod is named after the Synod protocol, the core consensus algorithm in Leslie Lamport's paper "The Part-Time Parliament" (ACM Transactions on Computer Systems, 1998; first submitted in 1990). The paper tells it as the story of the parliament of the ancient Greek island of Paxos, whose part-time legislators could agree on decrees although they came and went; today the algorithm is known as Paxos. Lamport later explained it plainly in "Paxos Made Simple" (2001), and in 2013 he received the ACM A.M. Turing Award for fundamental contributions to the theory and practice of distributed and concurrent systems. His "Time, Clocks, and the Ordering of Events in a Distributed System" (1978) and his TLA+ specification language shaped how we reason about such systems. We are grateful for his work, and we hope Synod honours it by making these ideas easier to watch and understand. The `paxos` example is Synod's own namesake algorithm, written in Synod so you can watch it run.

## Things to try (Break it)

- **Paxos:** delete the loop that adopts the highest prior value, run
  seeds 1–200, and watch `always` break.
- **Raft:** shorten the election timeout range to `150ms and 160ms` and
  watch split votes.
- **Two-phase commit:** move the coordinator crash to `after 80ms`; the
  decision now reaches the participants.
- **Cassandra:** set `Quorum` to 3; the second write no longer succeeds
  while a replica is down.
- **Web app:** add a timeout in `app` so requests fail fast when the cache is down.

## Notes for implementers

- These programs are the acceptance tests of `implementation/10-roadmap.md` in [dsl](https://github.com/synodlang/dsl).
- Timings in the demos (for example the 45ms coordinator crash) were
  chosen to land between protocol phases with typical latencies. If the
  golden trace for a seed does not show the intended story, adjust the
  timing or the seed, never the protocol, and record it here.
- tcp: the closing note at 100ms lands after both ends are ESTABLISHED
  (at most 90ms with the default 10-30ms latency).
- cassandra's record timestamps are named `stamp` (`at` is reserved).

Implements the Synod language specification v0.2.1: https://github.com/synodlang/dsl

Licensed under [CC BY 4.0](LICENSE).

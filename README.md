# interactor-zone-router-guest

The model of a zone that only routes: it hands each member the others' frames and reads none of them.

## What is here

- `router.sgd`: four slots, two frames a slot. A half takes one frame in 5 ticks with a burst of two, on the router's own clock; a frame beyond that is counted and not stored.
- `tests/router_trace.gd`: writes every call and every answer of a scripted scenario to a file that a relay in another language replays. `transport-zone-relay` is held to it.
- `docs/router-trace.md`: the file format, the scenario and the controls.

    godot --headless --path . -s tests/router_trace.gd -- <out file> [--ticks=N] [--control=flip|flood|silent|order|window]

What a frame is and what the router's calls are is in `docs/wire.md` of `interactor-presence-gates`.

## The other parts

Each part of the presence slice is a repository of its own in `V-Sekai-fire`, and they are checked
out side by side.

| Repository | What it holds |
| --- | --- |
| `interactor-packets-guest` | the Packet codec and the order of a body's 21 parts |
| `interactor-zone-router-guest` | the model of a zone that only routes, and the trace a relay replays |
| `interactor-observer-guest` | one client's check of what the zone relays: hashes, tags and verdicts |
| `interactor-curve-guest` | curve playback between sends |
| `interactor-replica-guest` | a shared object as four replicas |
| `interactor-anny-follow-guest` | the avatar posed from the muscle skeleton |
| `transport-zone-relay` | the relay in C, on sockets, with its load generator |
| `interactor-presence-gates` | the gates that join the parts on a real body, the videos and the ledger |

## Rules of the source

Guests are SafeGDScript and gates are GDScript run on a double-precision editor with the sandbox
built in. A gate prints a `RESULT:` line and has controls that must fail. Comments are at most 3%
of a file's lines, which `tools/comment_density.exs` of `interactor-presence-gates` checks, and
the explanation is in the documentation.

## Licence

MIT; see `LICENSE`.

# 00 — Frame

Status: **agreed** (owner)
Re-entered via back-edge: (none yet)

## Problem (one sentence)

Deaf riders cannot access the spotter→riders talkie channel, so they ride downhill
blind to the road status (clear / N cars / last car color / ALL-STOP) that every
other rider already receives — and an error in this channel can have dramatic
consequences.

## Actors (multi-actor system)

- **Spotter** — drives the opener car ahead of the group, reads the road, talks the
  status on the talkie. Must keep driving and working the car; the solution must not
  remove him from the driver's seat.
- **Non-deaf riders** — already receive the channel via talkie. Should see as little
  change in their gear and habits as possible.
- **Deaf riders** — currently outside the talkie loop. The people the solution
  exists for. **Currently kept in the loop by other riders around them giving signs
  when there is danger.**

## Project roles (this repo)

- **Owner / operator** — you. Sole designer of the technical solution, drives the
  process, decides on back-edges, approves sign-off.
- **Friends (co-designers / domain witnesses)** — contribute domain truth (spotting,
  riding, conditions). Not editors of the process.
- **Builder** — a third party who will build the design. Out of scope of this repo
  but their constraints may inform it (asked at phase 4).
- **Test rider** — the owner's deaf friend, controlled-environment testing only.

## Sign-off

Phase 0 is signed off by the owner. From phase 1 onward, the owner signs off on
every phase doc; the design itself (phase 6) additionally requires the friends'
review as domain witnesses.

Communication is **one-directional: spotter → riders**. There is no rider→spotter
requirement in scope. Failure of this channel is not a soft failure — it can be
catastrophic (see Constraints).

## What we're building

A **coherent design** (the artifact of this project). Building it is someone else's
job; testing will be done with the owner's deaf friend in a controlled environment.
This repo produces the design + documentation, not the hardware.

**Definition of done (owner-confirmed default):** the phase 6 handoff doc for the
builder contains — system architecture, bill of materials (BOM), mechanical and
electrical interfaces, failure-mode analysis, build instructions, and a test plan.

## Rider / equipment context (owner-verified)

- All involved are **advanced downhill skateboarders**.
- Speeds up to **100 km/h**.
- **Modern slalom boards**, **80 mm wheels**: high turn-ability and grip, exceptional
  stability — the back end barely turns, the front does the work.
- Standard gear: **talkies, full-face helmets, leather suit or motorbike-style
  protective gear, slide gloves**.
- Braking is done by **sliding the board** — wheel friction is the brake. Very
  efficient, but hard to execute in a constrained environment. Hence the talkie
  process: **you must brake before you encounter the issue, not at it.**
- Long-term target environment: the best roads in Europe, including
  **Col de la Bonnette** (no phone coverage).

## Constraints

1. **Usability** — primary constraint. The solution must be simple and reliable; the
   two are correlated and both are non-negotiable.
2. **No cell network dependence** — riding areas are poorly covered; the solution
   cannot assume a data or voice network. (Talkies are the existing radio channel.)
3. **Spotter continuity** — the spotter also drives the car; the solution must be
   operable while driving, without removing him from the car.
4. **Proportionate change for existing riders** — non-deaf riders and the spotter
   should see only as much change in gear and habits as the solution requires. The
   right amount of change is a *proportionality to find* (phase 3–4), not a fixed
   "minimal" target — it must land somewhere everyone can actually use it.
5. **Modifications allowed** — board, helmet, talkie, and glove may all be modified.
   No hardware limitation.

## Success criteria (ideal scenario)

The information content the talkie channel already carries must be **accessible to
the deaf rider** in real time. The talkie carries states like these (owner
transcript, verbatim) — **illustrative, not exhaustive**; there are many call
variants, all sharing these characteristics (owner-confirmed):

- **Short calls, repeated, frequent (every 3–5 s), relevant and clear information
  only.**
- **Road completely free** — `ok, ok, ok`
- **N cars, one at a time** — `one white car, one white car, one white car`
- **Car passed, clear again** — `after the white car it's ok, after the white car it's ok`
- **Motorbikes, repeated** — `motorbike, 3 motorbike, 3 motorbikes, 3 motorbikes`
- **Count + last car color** — `2 cars, 2 cars, 2 cars the last one is red`
- **ALARM = everybody stops**
- (…and other variants in the same style)

So the deaf rider must be able to tell: is the road completely free? how many
cars? what's the value of N? what color is the last car? and is this an alarm?

**Scope note (owner-confirmed):** these are *information requirements* — what must
reach the deaf rider. **How the information is carried and represented is a
solutioning-phase question** (phases 3–4), not a constraint on this frame.

Plus: non-deaf riders and the spotter experience a proportionate amount of change
to gear/habits — enough for everyone to actually use the solution, no more.

Measured by: a deaf rider completes a controlled run with the solution in use and
receives the correct state for every transmitted call, including at least one
alarm call, with no missed or misread messages.

## Out of scope

- **Talkie signal loss** — not solved here. The existing rule stands: if anyone
  receives nothing for **10 seconds, they stop.**
- **Replacing the opener-car + talkie process** — it is the reference, not the
  target. We are extending it, not trusting it, not removing it.
- **General risk mitigation** — the existing process is known-not-100%-safe and the
  group already rides conservatively assuming a car, pedestrian, bike, or dog can
  appear. That posture is unchanged by this project.
- **Building the solution** and **production/field testing** — separate workstreams,
  owned by others. This project delivers the design.

## Non-goals (explicit)

- Improving the hearing channel itself (talkie range, clarity, protocol).
- Training hearing riders in new procedures beyond what the solution requires.

Speed is not a design target: the solution will incidentally let the deaf rider
ride faster (having real-time road status), but that outcome is **out of scope** —
it is a side effect, not something this project designs or measures for.

## Known failure cases (owner inventory, verbatim)

These are real or near-miss events on the existing process. They are *inputs to the
design's threat model*, not problems this project must solve individually — but the
design must not make any of them worse.

1. **Gone too fast after the opener car, no signal received, transmission was bad** —
   speed outran the channel; the channel had a gap.
2. **A car exits onto a hidden path between the opener car and the riders** — the
   spotter's vantage doesn't see it until it's already alongside the riders.
3. **Communication cut + spotter did not repeat an important event enough** — a
   critical call was lost and never re-broadcast.

## Resolved in this phase (record for audit)

- **Broadcast, not point-to-point.** The talkie is a broadcast channel; the design
  inherits that. No per-rider addressing required.
- **Information, not representation.** The talkie states above are *information
  requirements*; how they're carried/displayed is deferred to phases 3–4.
- **Power / duration** — trips are short; not a primary constraint.
- **Call set is open-ended** — the listed states are examples, not a closed
  vocabulary. The design must handle "short, repeated, frequent, clear" calls in
  general, not just these six.
- **Current workaround (owner-verified):** today the deaf rider is kept in the loop
  **by signs from a rider positioned in front of him**. If no one is close enough
  in front, he has no security information and must ride with extra caution.
- **Crash survivability** — lowest priority; crashes hurt the rider more than the
  gear. The gear only needs to be robust enough not to be a secondary risk.
- **Maintenance** — everyone maintains their own gear; the group helps each other.
  No dedicated maintainer role.

## Open questions (to be answered during phase 1 — Empathize)

(none blocking — phase 1 will extract the full security process, spotter routine,
and the sign-based workaround's limits)

## Back-edges

(see README for the iteration rules)

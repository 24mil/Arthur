# Evidence behind the presentation

Snapshot reviewed for this portfolio: 8 October 2026. Completed experiments below are dated 2 October 2026. Their original reports and artifacts are retained privately.

## Model and demonstrations

The demonstration checkpoint is **L10 EMA @100**, SHA-256 beginning `76d20cb7849f`. Its saved configuration and loaded tensors give **6,672,466 total parameters** and **5,152,965 policy parameters**. Both counts come from the loaded model, not a rounded design estimate.

The README now contains one 24-second decision demonstration rather than nine separate players. It shows four recorded L10 EMA @100 decisions (three plays and one wait) from native_v45. Each root is held for one second for readability, then its recorded battle context advances for five seconds. The annotations show the public hand at that exact decision, conditional card and placement probabilities, action-type probabilities, and the sampled command. These are output probabilities, not win chances or a verbal rationale. None of the four displayed commands was overridden by search. The earlier bounded trace contains six public-belief searches with zero audited hidden reads; the edited video is an illustration, not a new strength evaluation.

The board is rendered using the existing project replay viewer's canvas drawing functions. This private offline export removes the surrounding inspection panels; it does not replace or change the engine. The video runs at 30 frames per second. Between archived snapshots, x/y positions interpolate for display only. HP, resources, object presence and policy outputs remain their recorded step values. Unexported projectiles and tower activation are not invented; unit attack rings derive from recorded targets and pinned ranges. Viewer orientation remains y-up, with the blue AI at the top. The highlighted action tile uses that same transform and the acting player's verified canonical mapping.

The original viewer recordings and historical diagnostic assets are retained as supporting material. They are not additional current demonstrations. The Python clip shows the retained historical implementation on a frozen data pin, driven by a scripted deployment planner. It is a bounded 90-second scenario, not a completed-match validation or the current training engine.

The memory clip uses 20 archived snapshots from a TV Royale capture dated 8 September 2026. It displays troop identities and coordinates, omits unverified HP and ability semantics, and identifies the reads as non-atomic. It does not claim frame-accurate screen alignment.

The phone footage is cropped from the same historical TV Royale recording to remove player/clan identification. It is **human replay capture footage, not footage of the showcased model playing**. The separate deployment diagram describes the harness. A fresh model-on-phone recording is deferred at the owner’s request. No device was connected during this edit; the continuous-play pause was preserved. It will use matching card, placement and probability annotations when captured.

The human-learning diagram and action illustration describe recorded commands and reconstructed training contexts. Reconstruction uncertainty, supported prefixes and component-specific validity matter; a recorded card action does not provide a complete observed board. Level-16 cards alone do not establish Ultimate Champion league.

## Case study 1: an evaluation-interface defect

**Model:** H6, human-imitation checkpoint. **Opponent:** L10 EMA @100. **Environment:** native_v33, period-3 data pin, ranked-loadout panel.

| Interface | Score | Reported 95% interval | Games |
|---|---:|---:|---:|
| Original | 7.4% | 4.8–11.3% | 256 |
| Corrected | 67.2% | 61.2–72.6% | 256 |

Score is wins plus half draws. The pooled results combine two episode-seed series, each containing 64 seat-swapped pairs over the same 64 loadouts. Intervals shown in the chart are the original report's Wilson intervals on games; deck/seed repetitions limit independence. The report also includes paired difference estimates and a replication.

The correction aligned wait-context fields with the training data, replaced incompatible banking behavior with the dataset's one-decision WAIT, and changed card/placement decoding. The action-type head remained sampled. **Weights did not change.** This demonstrates an interface failure and its correction, not a training improvement or human win rate.

## Case study 2: public-belief engine search

**Model:** L10 EMA @50, SHA-256 beginning `72d39105bcdf`. **Comparison:** the same network with vs without search. **Environment:** native_v44, in-engine battles.

- 512 games: 256 seat-swapped pairs; 64 ranked loadouts repeated with episode seeds.
- 327 wins, 185 losses: **63.9% score**.
- Relative Elo: **+99**, reported pair-bootstrap 95% interval **+74 to +125**.
- The sequential decision occurred earlier; the reported number comes from completing the predetermined 256-pair panel.

Search used top placement candidates, four opponent-belief samples per candidate and a five-second rollout horizon, with no subsequent deployments inside the rollouts. Scoring used public value and tower terms. The public-belief search recorded zero audited hidden reads in 26,080 searches. A later native_v45 audit separately hardened observation features; the earlier result is not a claim that every historical actor feature had already passed that later audit.

The adapter was subsequently exercised **offline on 103 real captures**. That establishes an integration result, not a live-game strength gain. Elo estimates here are comparison-specific and must not be added to unrelated runs.

## What is still open

Real-game transfer, late-game engine fidelity and independently verified human-opponent performance require their own evidence. Superhuman play remains the objective. Search traces and architecture illustrations are displayed outputs and simplified diagrams, not a claim of verbal reasoning or perfect game fidelity.

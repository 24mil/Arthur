# Evidence behind the presentation

Presentation updated: 10 October 2026. Model and experiment snapshot reviewed: 8 October 2026. Completed experiments below are dated 2 October 2026. Their original reports and artifacts are retained privately.

## Model and demonstrations

The demonstration checkpoint is **L10 EMA @100**, SHA-256 beginning `76d20cb7849f`. Its saved configuration and loaded tensors give **6,672,466 total parameters** and **5,152,965 policy parameters**. Both counts come from the loaded model, not a rounded design estimate.

The README now contains one 12-second decision demonstration at 2× playback speed. It shows the same four recorded L10 EMA @100 decisions (three plays and one wait) from native_v45 as the previous 24-second edit. Each root is held for 0.5 output seconds, then five source seconds of recorded battle context advance in 2.5 output seconds. The on-screen game clock remains source time. The annotations show the public hand at that exact decision, conditional card and placement probabilities, action-type probabilities, and the sampled command. These are output probabilities, not win chances or a verbal rationale. None of the four displayed commands was overridden by search. The earlier bounded trace contains six public-belief searches with zero audited hidden reads; the edited video is an illustration, not a new strength evaluation.

The architecture diagram reflects the frozen checkpoint configuration: a spatial U-Net with widths 96/144/192; 64 entity and 32 event tokens processed by a three-layer, four-head transformer of width 128; and two-layer, four-head feature fusion. The staged heads choose action type, wait duration, card slot, card-conditioned placement and ability carrier. The separate training critic is not part of the deployed action-selection path. The diagram simplifies internal connections; the total count also includes auxiliary prediction heads.

The board is rendered using the existing project replay viewer's canvas drawing functions. This private offline export removes the surrounding inspection panels; it does not replace or change the engine. The video runs at 30 frames per second. Between archived snapshots, x/y positions interpolate for display only. HP, resources, object presence and policy outputs remain their recorded step values. Unexported projectiles and tower activation are not invented; unit attack rings derive from recorded targets and pinned ranges. Viewer orientation remains y-up, with the blue AI at the top. The highlighted action tile uses that same transform and the acting player's verified canonical mapping.

The original viewer recordings and historical diagnostic assets are retained privately as supporting material. They are removed from the repository’s current file list and are not additional current demonstrations. The Python clip shows the retained historical implementation on a frozen data pin, driven by a scripted deployment planner. It is a bounded 90-second scenario, not a completed-match validation or the current training engine.

The memory clip uses 20 archived snapshots from a TV Royale capture dated 8 September 2026. It displays troop identities and coordinates, omits unverified HP and ability semantics, and identifies the reads as non-atomic. It does not claim frame-accurate screen alignment.

The README now opens with a **30-second human-gameplay reference** by [Red Guy Gameplay](https://www.youtube.com/watch?v=qXb0ZuQQqNs), originally published 31 August 2025. It shows the normal player hand, card selection and troop placement, rather than TV Royale replay controls. This is third-party footage: **neither Arthur nor this project's AI is the player**. The excerpt covers source-video seconds 8–38; it has no additional speed change, no audio, a player/clan-name mask, and small human-gameplay/source labels. It is encoded as H.264 at 30 fps. No policy probabilities, memory observations or AI-control claims are added to this footage.

The creator's video description explicitly permits reuse with credit and prohibits republishing it as a stock “No Copyright Gameplay” offering. This portfolio uses a credited excerpt to illustrate the game; it does not claim a specific Creative Commons license version, ownership of the recording, or creator endorsement. The full source is linked above. A current model-on-phone recording is not included; the updated game client's compatibility with the existing observation reader remains unresolved. The earlier TV Royale capture is retained privately as historical material.

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

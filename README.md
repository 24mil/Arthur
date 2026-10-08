<p align="center">
  <img src="project-mark.svg" width="128" height="128" alt="Clash Royale AI project mark">
</p>

<h1 align="center">Clash Royale AI</h1>

<p align="center">
  <img src="badge-engine.svg" alt="Engine: Rust">
  <img src="badge-ml.svg" alt="ML: Python and PyTorch">
  <img src="badge-model.svg" alt="Model: 6.67 million parameters"><br>
  <img src="badge-tick.svg" alt="Engine tick: 50 milliseconds, 20 Hz">
  <img src="badge-learning.svg" alt="Learning: imitation and PPO">
  <img src="badge-code.svg" alt="Implementation: private">
</p>

<p align="center">
  <a href="overview.mp4">90-second overview</a> ·
  <a href="#the-model">Model architecture</a> ·
  <a href="#learning-from-human-games">Human learning</a> ·
  <a href="#what-the-experiments-show">Results</a> ·
  <a href="EVIDENCE.md">Methods and evidence</a>
</p>

An end-to-end game-playing AI project by **Arthur**: battle simulation, a neural player, human-replay learning, self-play and real-game integration. I own the direction, experiments, integration and validation across the stack. **Application code, weights and datasets stay private.**

## Rust battle simulator

The current engine runs movement, targeting, combat, card cycles and deployment mechanics in Rust. This is the **existing project replay viewer**, displaying frozen native frames with its own playback controls, unit inspection and HP display.

[![Existing replay viewer displaying the frozen Rust battle](rust-engine.gif)](rust-engine.mp4)

[Full viewer recording](rust-engine.mp4) · L10 EMA @100, native_v45 · sped-up recorded states. Unexported fields are labeled; this is a bounded illustration, not a fidelity or strength test.

<details>
<summary><strong>Python prototype — historical</strong></summary>

The original implementation established the inspectable simulation workflow. Rust is now the behavioral authority. This bounded, scripted scenario is shown through the same project viewer.

[![Historical Python simulation in the existing replay viewer](python-prototype.gif)](python-prototype.mp4)

[Full recording](python-prototype.mp4)

</details>

## The model

Spatial board features and entity/event tokens pass through spatial processing, transformers and feature fusion. Separate heads choose the action type, card, placement, ability carrier and waiting duration.

![Player V2 architecture, with the training critic outside the deployed actor's input path](architecture.svg)

The loaded **L10 EMA @100** checkpoint contains **6,672,466 parameters**, including **5,152,965 in the policy path**. The critic is a training component.

<details>
<summary><strong>Recorded probabilities and placement heatmaps</strong></summary>

These are offline diagnostic figures from actual frozen policy outputs, not a recreated application interface or a verbal explanation of the model's reasoning.

[![Recorded policy probability and placement diagnostics](neural-decisions.gif)](neural-decisions.mp4)

[Full diagnostic sequence](neural-decisions.mp4) · [Inspect one decision](decision-detail.jpg)

</details>

## Learning from human games

Recorded card choices, placements and ability markers feed Rust reconstruction and imitation learning. Recorded commands and reconstructed board state remain distinct; unsupported labels are masked.

![Human learning, self-play and evaluation workflow](learning.svg)

<details>
<summary><strong>Recorded actions and self-play demonstrations</strong></summary>

[![Recorded placement markers and the learning workflow](human-learning.gif)](human-learning.mp4)

[Recorded-action demonstration](human-learning.mp4) · Placement markers are not recorded troop trajectories. Level 16 does not establish Ultimate Champion league.

[![Frozen opponents, exploiters and evaluation workflow](self-play.gif)](self-play.mp4)

[Self-play walkthrough](self-play.mp4) · Workflow illustration; no active training run is implied.

</details>

## Engine search

Candidate actions are compared through simulated futures. A public belief supplies unknown opponent state; the candidate scores and selected branch shown here are recorded outputs.

[![Candidate actions, rollout scores and selected simulated future](engine-search.gif)](engine-search.mp4)

[Full search diagnostic](engine-search.mp4) · Five-second rollouts; no additional deployments; six recorded searches with zero audited hidden reads.

## Real-game observations and deployment

The deployed observation route uses **memory-derived state**. The capture below shows the existing game interface. It is an archived **human TV Royale replay**, not the showcased model playing.

<p align="center"><a href="deployment.mp4"><img src="deployment.gif" width="420" alt="Cropped historical TV Royale game capture; human replay, not model gameplay"></a></p>

[Full capture](deployment.mp4) · Recorded 8 September 2026 · Player/clan identification cropped out.

![Observation, policy, optional search, command execution and validation boundaries](system.svg)

<details>
<summary><strong>Inspect the archived observation outputs</strong></summary>

The diagnostic uses 20 recorded memory snapshots. Verified identity/coordinates are displayed; unverified HP is omitted. Reads were non-atomic and are not claimed to align exactly with video frames.

[![Archived coordinate and identity diagnostic](memory-observations.gif)](memory-observations.mp4)

[Observation diagnostic](memory-observations.mp4) · The search adapter also has offline evidence on 103 captures. A fresh model-on-phone recording remains pending a connected device.

</details>

## What the experiments show

![H6 evaluation-interface correction: simulator score increased from 7.4 percent to 67.2 percent without retraining](interface-result.svg)

**H6 vs L10 EMA @100, native_v33:** 256 games per arm. Waiting and placement interface corrections changed the score from 7.4% to 67.2%, with unchanged weights.

![Public-belief search comparison: plus 99 relative simulator Elo, reported interval plus 74 to plus 125](search-result.svg)

**L10 EMA @50 with vs without search, native_v44:** 512 games; +99 relative simulator Elo, reported 95% interval [+74, +125]. [Conditions, uncertainty and limitations](EVIDENCE.md).

Superhuman play is the research objective; it has not been established. Development includes AI-assisted coding and analysis. Implementation can be discussed privately with internship teams.

**[GitHub profile / contact](https://github.com/24mil)**

This is an unofficial project, not endorsed by Supercell. Gameplay belongs to Supercell; see the [Fan Content Policy](https://supercell.com/en/fan-content-policy/).

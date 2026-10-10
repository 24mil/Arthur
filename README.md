# Clash Royale AI

Rust simulator · Python / PyTorch · 6.67M parameters

An AI player built around a **Rust battle simulator**, a neural policy and learning from human replays and self-play. My work covers system design, experiments, integration and validation across the stack.

## Watch it choose a move

https://github.com/user-attachments/assets/3323f397-0c3a-437c-83ef-01f9fe6bc50a

- **Observe:** the model receives structured board features, troops, resources and recent events. The arena shows the corresponding simulated battle.
- **Choose:** percentages show the model's action probabilities. Card percentages assume it chooses to play; they are not win probabilities.
- **Execute:** the selected card and highlighted placement become a command in the Rust engine. Waiting and abilities are decisions too.

## Engineering that improved results

![Interface correction and public-information search, with sample sizes and reported uncertainty](https://raw.githubusercontent.com/24mil/Arthur/3bf95a756165988f2b8d9b945dc0739386d334cb/improvements.svg)

- **Fix the interface:** matching waiting and placement decoding to training changed H6's simulator score from **7.4% to 67.2%**, without retraining.
- **Look ahead:** public-information search added **+99 simulator Elo** against the same network without search; reported 95% interval **+74 to +125**, over **512 games**.

[Models, opponents, methods and limitations](EVIDENCE.md). Superhuman play remains the research goal.

## Neural network and learning

![Observation, neural architecture, action and learning pipeline](https://raw.githubusercontent.com/24mil/Arthur/3bf95a756165988f2b8d9b945dc0739386d334cb/pipeline.svg)

The **U-Net** processes the board. **Transformer blocks** process troops and recent events. Their features are combined; separate heads choose the action, card, placement, ability carrier and wait duration. The checkpoint has **6.67M parameters**, with **5.15M in the policy path**. A separate critic learns during training.

Human replays teach decisions; PPO self-play develops them further. Rust replaced the historical Python engine. Real-game integration uses memory-derived observations.

**Implementation, weights and datasets remain private**, available for discussion with internship teams. Development includes AI-assisted coding and analysis. [Contact Arthur](https://github.com/24mil).

<a id="real-gameplay"></a>

## Real-game interface

The deployment system connects memory-derived game state to the policy, then sends its chosen card and position to the phone. This footage is human-controlled.

https://github.com/user-attachments/assets/1e25c6cf-c03e-4b53-a444-fc6ba0259419

<sub>Unofficial project, not endorsed by Supercell. [Fan Content Policy](https://supercell.com/en/fan-content-policy/).</sub>

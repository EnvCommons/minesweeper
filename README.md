# Minesweeper

[![OpenReward Environment](https://img.shields.io/badge/%E2%AD%90%20OpenReward-Environment-f7e6cc)](https://openreward.ai/GeneralReasoning/Minesweeper)

## Description

**Minesweeper** is an environment for evaluating agents on spatial reasoning, probabilistic inference, and strategic exploration. This environment wraps the Minesweeper implementation from [TextArena](https://github.com/LeonGuertler/TextArena), a framework for text-based game environments.

## Capabilities

- Probabilistic reasoning under uncertainty
- Spatial pattern recognition and inference
- Strategic decision-making with risk assessment
- Constraint satisfaction from partial information

## Compute Requirements

Minesweeper does not require a sandbox. It has minimal compute requirements.

## License

[MIT](https://opensource.org/licenses/MIT). The underlying [TextArena](https://github.com/LeonGuertler/TextArena) framework is also MIT.

## Tasks

There are 600 tasks in the `train` split and 600 in `test`. Each split contains 50 tasks across each of 12 variants:

- **Minesweeper-v0**
- **Minesweeper-v0-train**
- **Minesweeper-v0-raw**
- **Minesweeper-v0-small**
- **Minesweeper-v0-small-train**
- **Minesweeper-v0-small-raw**
- **Minesweeper-v0-medium**
- **Minesweeper-v0-medium-train**
- **Minesweeper-v0-medium-raw**
- **Minesweeper-v0-hard**
- **Minesweeper-v0-hard-train**
- **Minesweeper-v0-hard-raw**

Each task is seeded for reproducibility.

## Reward Structure

This is a sparse reward environment. TextArena's Minesweeper reward is already in `[0.0, 1.0]` and is passed through unchanged: clearing the board scores `1.0`, and every other terminal outcome (hitting a mine or reaching the turn limit) scores the fraction of safe cells revealed. Intermediate moves score `0.0`.

We do not use LLM graders for this environment; reward is determined programmatically.

## Data

Game state is generated procedurally by the TextArena engine using seeded randomness. No external data files are required.

## Tools

Agents are given a single tool:

- `reveal_cell(row, column)`: Reveal a cell on the minesweeper grid at the given row and column (0-indexed). Numbers show adjacent mine count. Hitting a mine ends the game.

## Time Horizon

Minesweeper is a multi-turn environment.

## Environment Difficulty

Difficulty depends on the variant. In TextArena's registration the small variants use a 5x5 board with 5 mines, the base `Minesweeper-v0` variants 8x8 with 10 mines, medium 10x10 with 20 mines and hard 12x12 with 30 mines, each with a 100-turn limit. The `-train` and `-raw` suffixes change only the observation wrappers, not the board.

## Other Environment Requirements

There are no further environment requirements; Minesweeper works out of the box without any secrets or API keys.

## Safety

Agents in Minesweeper interact only with a puzzle game and have no access to external systems, the internet, or sensitive data. The environment does not present safety risks.

## Citations

```bibtex
@misc{guertler2025textarena,
    title={TextArena},
    author={Leon Guertler and Bobby Cheng and Simon Yu and Bo Liu and Leshem Choshen and Cheston Tan},
    year={2025},
    eprint={2504.11442},
    archivePrefix={arXiv},
    primaryClass={cs.CL},
    url={https://arxiv.org/abs/2504.11442},
}
```

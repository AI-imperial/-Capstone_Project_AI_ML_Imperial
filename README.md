# Black-Box Optimisation Capstone

## Project Overview
This repository documents my work on a black-box optimisation (BBO) capstone project. The task is to optimise eight hidden functions whose internal equations are unknown. Each function behaves like a real ML or scientific objective where evaluations are limited and expensive, so the goal is to make careful sequential decisions rather than rely on brute-force search.

The project is framed as a maximisation problem for all eight functions. Across the capstone, I submit one new query per function per round, review the returned outputs, and refine the strategy using ideas from each module.

## Problem Setup
Each function takes a continuous input vector in `[0, 1]`.

- Function 1: 2D
- Function 2: 2D
- Function 3: 3D
- Function 4: 4D
- Function 5: 4D
- Function 6: 5D
- Function 7: 6D
- Function 8: 8D

The starter observations are provided as `.npy` arrays inside the course archive. New submissions are stored as hyphen-separated strings, for example:

- Function 1: `0.737117-0.744495`
- Function 8: `0.109267-0.208876-0.199814-0.102895-0.922936-0.611119-0.116371-0.632024`

## Repository Contents
- [data/raw/README.md](C:/root/Imperial%20Course/data/raw/README.md): starter data and raw archive notes
- [queries/README.md](C:/root/Imperial%20Course/queries/README.md): submission files for each round
- [results/README.md](C:/root/Imperial%20Course/results/README.md): results folder overview
- [results/round-output-summary.md](C:/root/Imperial%20Course/results/round-output-summary.md): returned outputs and best-so-far summary
- [docs/datasheet-bbo-capstone.md](C:/root/Imperial%20Course/docs/datasheet-bbo-capstone.md): datasheet for the capstone dataset
- [docs/model-card-bbo-approach.md](C:/root/Imperial%20Course/docs/model-card-bbo-approach.md): model card for the optimisation approach
- [docs/discussion-board-draft.md](C:/root/Imperial%20Course/docs/discussion-board-draft.md): supporting written reflections
- [src/README.md](C:/root/Imperial%20Course/src/README.md): reserved code area for reusable scripts

## Round History
The repository currently includes query submissions through round 10:

- [round01.txt](C:/root/Imperial%20Course/queries/round01.txt)
- [round02.txt](C:/root/Imperial%20Course/queries/round02.txt)
- [round03.txt](C:/root/Imperial%20Course/queries/round03.txt)
- [round04.txt](C:/root/Imperial%20Course/queries/round04.txt)
- [round05.txt](C:/root/Imperial%20Course/queries/round05.txt)
- [round06.txt](C:/root/Imperial%20Course/queries/round06.txt)
- [round07.txt](C:/root/Imperial%20Course/queries/round07.txt)
- [round08.txt](C:/root/Imperial%20Course/queries/round08.txt)
- [round09.txt](C:/root/Imperial%20Course/queries/round09.txt)
- [round10.txt](C:/root/Imperial%20Course/queries/round10.txt)

Returned outputs are documented through round 9 in [round-output-summary.md](C:/root/Imperial%20Course/results/round-output-summary.md).

## Strategy Evolution
The optimisation approach evolved across the course instead of staying fixed:

- Early rounds used Gaussian-process style surrogate modelling, uncertainty ranking, and broad exploration.
- Mid rounds became more function-specific, mixing local trust-region search with wider resets when a function stalled.
- Later rounds used shallow neural-network surrogates, SVM-inspired region logic, and explicit hyperparameter tuning.
- By the later rounds, functions with repeated gains such as 4, 5, and 7 were treated with tight exploitation, while flatter or less stable functions such as 1, 2, 3, and 6 kept more exploratory behaviour.

The main principle throughout is simple: exploit locally when repeated evidence supports a region, and widen the search when performance stalls or drops.

## Current Best Results
Best observed outputs so far:

- Function 1: approximately `0`
- Function 2: `0.6690984814241058`
- Function 3: `-0.007191586817437852`
- Function 4: `0.543132017668857`
- Function 5: `4461.674159058348`
- Function 6: `-0.3375310420057598`
- Function 7: `1.9438801032749091`
- Function 8: `9.9654927093175`

## Status
This is now a local git-ready project repository. A public GitHub publishing step can be done later once the capstone is fully complete and all required final materials are ready.

# Model Card: BBO Optimisation Approach

## Overview
Model name: BBO Capstone Iterative Surrogate Optimiser  
Type: sequential black-box optimisation workflow  
Version: working version through round 13 preparation

This is not a single fixed model. It is a round-based optimisation approach that combines surrogate modelling, manual trust-region logic, and evolving exploration-exploitation choices.

## Intended Use
This approach is intended for:

- small-data black-box optimisation
- expensive-query settings where only one or a few new evaluations are possible per round
- educational demonstration of adaptive optimisation strategy

This approach should be avoided for:

- problems requiring guaranteed global optimality
- high-throughput settings where many evaluations are cheap
- formal algorithm benchmarking without controlling for manual intervention

## Details
The strategy evolved across the rounds rather than staying tied to one method.

### Rounds 1-3
- Began with surrogate-based search using Gaussian-process reasoning, random forest support, and acquisition-style ranking.
- Moved into more function-specific logic rather than one shared optimiser.
- Used SVM-style ideas to separate promising and weak regions when regression confidence was not enough.

### Rounds 4-6
- Shifted toward shallow neural-network surrogates to capture more nonlinear structure.
- Introduced local trust-region updates for functions that showed repeated improvement.
- Used broader resets for flatter or less stable functions.

### Rounds 7-10
- Added explicit hyperparameter tuning for surrogate flexibility and regularisation.
- Tightened the search around stable high-performing regions for functions 4, 5, and 7.
- Continued to treat functions 1, 2, 3, 6, and 8 more cautiously when trends stalled or became noisy.
- Used increasingly small exploit moves in regions showing consistent gains, especially for function 5.

### Rounds 11-13
- Continued trust-region style refinement in the strongest regions rather than broad resets.
- Treated functions 5 and 7 as the clearest exploit cases because they kept showing stable gains.
- Kept functions 1, 2, 3, 6, and 8 more cautious, using small local moves or renewed exploration when recent gains were weak.
- Prepared the final round by leaning even more on stable local regions while still allowing limited exploration for weaker functions.
- Reinforced the idea that later-round optimisation is mostly about filtering noise, preserving robustness, and avoiding overreaction to one bad round.

The decision rule throughout was simple in spirit:
- if a function was improving steadily, refine locally
- if it stalled or dropped, either broaden the search slightly or move back toward a stronger earlier region

## Performance
The main performance measure is the returned scalar objective value for each function, since every task is framed as maximisation.

### Best observed values so far
- Function 1: approximately `0` (no stable positive signal found)
- Function 2: `0.6690984814241058`
- Function 3: `-0.0037854953032998894`
- Function 4: `0.543132017668857`
- Function 5: `4463.16253498912`
- Function 6: `-0.3375310420057598`
- Function 7: `1.94923271396076`
- Function 8: `9.9654927093175`

### Performance interpretation
- Functions 4, 5, and 7 showed the clearest sustained local improvement.
- Function 8 reached a strong region early and then largely plateaued.
- Functions 1, 2, 3, and 6 remained harder to model reliably.

Metrics used in the workflow:
- best observed output per function
- round-to-round improvement or decline
- local consistency of strong regions
- surrogate plausibility rather than raw model fit alone

## Assumptions and Limitations
### Key assumptions
- nearby points in a strong region are likely to remain strong
- repeated local improvements indicate a useful trust region
- surrogate model outputs are informative enough to rank candidate queries even when absolute predictions are wrong

### Limitations
- very limited number of evaluations
- heavy path dependence from earlier query choices
- manual intervention when surrogate recommendations looked unrealistic
- strong sampling bias toward already promising regions
- no guarantee that the best observed point is close to the global maximum

Failure modes include:
- overfitting to a narrow local region
- flat or noisy functions being misread as structure
- underexploration of distant regions in high dimensions

## Ethical Considerations
The main ethical issue here is not human harm through demographic bias, but transparency and reproducibility in optimisation claims. Clear documentation matters because a black-box search can easily appear more systematic than it really is if manual judgment is hidden.

This model card supports responsible use by making the following explicit:
- how decisions were made
- when manual overrides were used
- what assumptions shaped the search
- where the evidence is sparse or biased

That transparency makes the project more useful for adaptation in real-world settings, where optimisation systems are often deployed under uncertainty and with incomplete knowledge.

## Clarity and Future Improvement
Adding more detail could improve this model card later, especially:

- a round-by-round performance table
- explicit trust-region sizes by function
- formal record of surrogate hyperparameters

For now, the current structure is sufficient for a working capstone because it explains the purpose, decision logic, results, assumptions, and main limitations without pretending the approach is more formalised than it actually is. The main requirement at this stage is that a reviewer can follow how the strategy changed from broad exploration into narrow local refinement over the later rounds.

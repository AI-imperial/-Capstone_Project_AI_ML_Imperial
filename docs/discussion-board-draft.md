# Discussion Board Draft

## Repository Structure
So far, I have organised the repository around the main parts of the capstone: raw data, round submissions, results, source code, and written reflections. The starter archive is kept in `data/raw`, while the proposed query strings for each round are stored in `queries`. I also separated `results` and `docs` so that returned outputs and written discussion posts do not get mixed together.

To improve clarity and reproducibility, I would keep each round in its own submission file and record any returned outputs in the results folder. I would also move reusable modelling scripts into `src` rather than leaving the project as a collection of ad hoc experiments. This makes the repository easier to navigate and makes it clearer how decisions were produced.

## Coding Libraries And Packages
The main libraries for my approach are `numpy`, `scikit-learn`, and `scipy`. `numpy` is useful for handling the input and output arrays, `scikit-learn` supports surrogate models such as Gaussian processes, random forests, logistic regression, and other baseline models, and `scipy` is useful for sampling and optimisation utilities.

These choices are appropriate because the capstone has a relatively small amount of data per function, so lightweight classical ML methods are usually more suitable than large deep learning frameworks. The trade-off is that these models may be less flexible in very high-dimensional or highly irregular problems, but they are easier to interpret and much more practical for small-data black-box optimisation.

## Documentation
My README currently explains the purpose of the capstone, the input and output format, the maximisation objective, and the way my strategy has evolved across rounds. I have also added round submission files and supporting notes so the repository structure matches the actual workflow.

The main documentation update I still need is to keep the README aligned with my latest strategy changes and any real outputs returned by the challenge. As more rounds are completed, I would update the technical approach section so it reflects which functions responded better to exploration, which benefited from local exploitation, and how later modules influenced my modelling decisions.

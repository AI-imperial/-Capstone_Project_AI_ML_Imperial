# Datasheet: BBO Capstone Data Set

## Motivation
This data set was created to support a black-box optimisation (BBO) capstone project in which the goal is to find high-performing inputs for eight unknown functions. It supports iterative optimisation under uncertainty rather than standard supervised learning on a fixed labelled benchmark. The practical purpose is to document how queries were chosen, what outputs were returned, and how the evidence changed the optimisation strategy over time.

The data set also fills a documentation gap in the project itself. The capstone is not only about getting strong outputs, but also about showing how decisions were made across rounds, what assumptions were used, and where the search may be biased or incomplete.

Creator: project author for the Imperial Course BBO capstone.  
Funding/support: course-provided starter archive and challenge framing from the programme.

## Composition
The data set contains:

- the original starter archive with initial input-output arrays for eight functions
- one submitted query per function per round
- returned scalar outputs for submitted queries
- supporting notes on strategy, assumptions, and reflections

### Function structure
- Function 1: 2D input
- Function 2: 2D input
- Function 3: 3D input
- Function 4: 4D input
- Function 5: 4D input
- Function 6: 5D input
- Function 7: 6D input
- Function 8: 8D input

### Formats
- starter data: `.npy` arrays inside `data/raw/Initial_data_points_starter.zip`
- round submissions: plain text files in `queries/roundXX.txt`
- project documentation: Markdown files in `docs/`

### Approximate size
- starter data includes 10 to 40 initial observations per function, depending on the function
- round submissions currently extend through round 10
- returned outputs are currently documented through round 9, with round 10 queries prepared but not yet evaluated

### Gaps and incompleteness
- the search space is continuous, so the data set is only a sparse sample
- some early round feedback was less systematically documented than later rounds
- strong sampling bias exists around promising local regions for functions such as 4, 5, 7, and 8
- large parts of the search space remain unexplored, especially in higher dimensions

The data set does not contain personal data, protected characteristics, or directly sensitive content.

## Collection Process
The initial observations were provided by the course as a starter archive. All later query points were generated manually and computationally through iterative optimisation. The process was not random in a pure statistical sense; it was adaptive and decision-based.

Across rounds, query generation used a mixture of:

- Gaussian-process style surrogate modelling
- acquisition-style search balancing exploration and exploitation
- random forest and classification-style region ranking
- SVM-inspired region separation
- shallow neural-network surrogate models
- trust-region refinement around the best known points
- manual constraint checks when surrogate suggestions looked unrealistic

The time frame was the duration of the capstone, with one query per function per round. This means the data set reflects a sequential optimisation process rather than a one-time collection event.

## Preprocessing, Cleaning, and Uses
Very little preprocessing was applied to the raw challenge data. The main transformations were:

- loading `.npy` arrays into analysis scripts
- storing submitted queries in a standard hyphen-separated text format
- appending returned outputs to the running optimisation history

The raw starter archive is preserved separately from later round notes and submissions.

### Intended uses
- documenting the capstone search process
- analysing optimisation decisions over time
- comparing exploration versus exploitation behaviour
- reflecting on surrogate-model assumptions and failure modes

### Inappropriate uses
- treating the data set as a complete representation of the hidden functions
- using it to claim globally optimal solutions
- using the optimisation history as an unbiased benchmark for comparing algorithms

The data set is highly path-dependent: later observations depend on earlier decisions.

## Distribution
At this stage, the data set is stored locally in the project workspace and is intended to be added to the public GitHub repository at the end of the capstone. Until then, it is effectively a working project artefact rather than a formally released benchmark.

Expected distribution method at project close:
- GitHub repository for the capstone

Terms of use:
- starter data remains subject to the course/challenge conditions
- project documentation and round files are for educational and portfolio use unless later relicensed explicitly

## Maintenance
The data set is maintained by the project author. Maintenance includes:

- adding new round submission files
- recording newly returned outputs
- updating accompanying notes when strategy changes
- preserving the starter archive and round history

Versioning is currently informal and round-based. A fuller release structure, repository linking, and final maintenance notes will be added at the end of the capstone when the repository is finalised.

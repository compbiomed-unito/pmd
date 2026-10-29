# Figure notebooks and input tables

## Extracting the archive `tar.gz`

Extract `pmd.tar.gz` into a dedicated directory

```sh
tar -xzf pmd.tar.gz
```

The archive contains `figure1.Rmd`–`figure6.Rmd`, `accuracy_precision.Rmd`, and `data/`. Open the notebooks from this directory to resolve correctly the path.

The figure notebooks are `figure1.Rmd`-`figure6.Rmd`. They calculate indices and draw the corresponding manuscript figures from existing data. `accuracy_precision.Rmd` separately calculates the experimental mixture accuracy and precision table. Run the notebooks with this directory as the working directory. Input paths refer to `./data/`.

## Synthetic datasets

Each count table has one row per detected integration site (IS) per sample. `sample` identifies the sample, `chromosome` and `position` identify the IS, and `frequency` contains an integer count.

| Input file in `data/` | Notebook | Sample identifiers and additional columns |
| --- | --- | --- |
| `S0.csv` | `figure1.Rmd` | `sample_A`, `sample_B`, and `sample_C` |
| `S1-4.csv` | `figure2.Rmd` | `batch` identifies S1–S4; `sample` is `01`, `03`, `10`, or `30`, denoting designated-clone target frequencies of 1%, 3%, 10%, or 30%. Identify a sample using both `batch` and `sample`. Read `sample` as text to preserve leading zeros |
| `Figure3_is_counts.csv` | `figure3.Rmd` | `Sample` is a composite label, `n100_t01_r01` denotes sampling depth n=100, pseudotime t=1, replicate r=1 |
| `Figure4_is_counts.csv` | `figure4.Rmd` | `Sample` is a composite label, `f003_d100_r01` denotes designated-clone frequency f=0.003, depth d=100, replicate r=1 |
| `Figure5_is_counts.csv` | `figure5.Rmd` | `Sample` is a composite label, `sc041_d100000_r01` identifies scenario 41 (combination of distribution type, tail, frequencyi, ...), depth d=100000, replicate r=1. `baseline_family` identifies the background model. |

Sampling replicates share the underlying population for their condition.

`Figure5_population_frequencies.csv` supplies the representative rank-abundance profiles in Figure 5B.

| Column | Meaning |
| --- | --- |
| `clone_id` | Synthetic population-component identifier |
| `baseline_prob` | Relative frequency in the initial background, before the ceiling adjustment and imposed dominance |
| `simulated_prob` | Relative frequency after adjustment and imposed dominance. |
| `rank` | Rank by decreasing `simulated_prob` |
| `is_target_clone` | Whether the component is the designated expansion target |
| `baseline_family` | Background model: Dirichlet, Log-series, or Zipf |

## Figure 6 experimental data

`figure6.Rmd` expects `data/Figure6_is_counts.csv`, a long-format subset of the Six et al. (2020) dataset cited in the manuscript, containing only patients `b0/bE` and `WAS5`. This experimental input is not included. Download the source dataset using the link in the manuscript and prepare the table described below.

The columns `sample`, `chromosome`, `position`, and `frequency` identify the sample, IS coordinate, and abundance estimate (`estAbund` in the source). 

Additional columns are `patient`, `cellType`, `timePoint`, and `timePointMonths`. 
Sample identifiers combine patient, cell type, and time point with `__`. 

## `accuracy_precision.Rmd`

`accuracy_precision.Rmd` expects `data/Mix1-3_is_counts.csv`. This table is a reformatted subset of the published experimental dataset cited in the manuscript and is not generated for this study. This experimental input is not included. Obtain the source dataset using the link in the manuscript. To prepare the input, retain only mixtures 1–3. The table uses the same long format with `sample`, `chromosome`, `position`, and `frequency`. Sample `1_2` identifies mixture 1, replicate 2.  

The notebook estimates the dominant-clone frequency before and after plateau correction, then calculates accuracy and precision across the three replicates.



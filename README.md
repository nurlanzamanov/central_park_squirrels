# 🐿️ Central Park Squirrel Behavior Analysis

Exploratory data analysis of squirrel behavior in the **2018 Central Park Squirrel Census**, using only **Python, Pandas and NumPy**. It looks at how often squirrels approach, ignore, or run from observers, and how those recorded behaviors overlap.

## Research question

> What patterns can we identify in squirrels' recorded behavioral responses?

The analysis focuses on three Boolean columns: `Approaches`, `Indifferent` and `Runs from`.

## Dataset

- **Source:** 2018 Central Park Squirrel Census (squirrel data), published through NYC Open Data. Please check the original source for current licensing and redistribution terms.
- **Size:** 3,023 observations, 31 columns.
- **Note:** the original CSV is kept unchanged. No cleaning or imputation is applied, because the three behavior columns have no missing values.

## Methodology

The analysis lives in [`analysis.ipynb`](analysis.ipynb) and is divided into five parts:

1. **Dataset overview:** dimensions, column names, data types and column categories.
2. **Data quality:** missing values (counts and percentages), duplicate rows, duplicate IDs and cleaning decisions.
3. **Behavioral analysis:** `True`/`False` counts, proportions and ranking of the three behaviors.
4. **Statistical summaries:** means, verification that the mean equals the proportion of `True` values, and overlap analysis using Boolean masks.
5. **Findings:** a research summary with limitations.

All results are calculated from the data. No visualization libraries or machine learning are used.

## Key findings

| Behavior | Observations recorded | Share of all observations |
|---|---|---|
| Indifferent | 1,454 | 48.1% |
| Runs from | 678 | 22.4% |
| Approaches | 178 | 5.9% |

- **The behaviors are not mutually exclusive.** 2,243 observations (74.2%) record at least one of the three, and 780 (25.8%) record none. 59 observations record exactly two behaviors and 4 record all three.
- **`Indifferent` and `Runs from` overlap the most** (32 observations, versus 20 for `Approaches` + `Runs from` and 19 for `Approaches` + `Indifferent`). These are nearly opposite behaviors, which suggests ambiguity in how observations were recorded.
- **The three proportions sum to about 76%**, but only 74.2% of observations record any behavior, because of the overlap.
- **Data quality:** there are no fully duplicated rows. 5 `Unique Squirrel ID` values appear twice, apparently the same squirrel recorded twice (about 0.17% of rows), with matching behavior values. `Color notes` (about 94%) and `Highlight Fur Color` (about 36%) have the most missing values.

## Limitations

- **Observation bias:** behavior was recorded by human observers and may be overlooked or interpreted differently.
- **No causal evidence:** the dataset records behaviors, not their causes. It cannot show that human presence caused a squirrel to approach or flee.
- **Limited scope:** one park, one year (2018), and only observed squirrels, so easily spotted squirrels may be overrepresented.
- **Overlapping indicators:** several behaviors can be recorded in one observation.
- **Meaning of `False`:** it means a behavior was not recorded, not that it never happens.

These results describe patterns in the recorded observations, not definitive rules about squirrel behavior.

## Repository structure

```text
central_park_squirrels/
├── data/
│   └── squirrel_data.csv
├── analysis.ipynb
├── README.md
└── requirements.txt
```

## How to reproduce

```bash
git clone https://github.com/nurlanzamanov/central_park_squirrels.git
cd central_park_squirrels

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

jupyter notebook analysis.ipynb
```

Run the notebook from the project root so the relative path `data/squirrel_data.csv` resolves, then use **Run All**.

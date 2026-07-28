# Revenue Prediction with Regression Analysis

This project uses **regression** (a way of drawing the "best fit" line through data) to predict a company's monthly **revenue**. It tries out several combinations of predictors and picks the one that guesses revenue the most accurately.

Think of it like this: if you know how much a factory produced and how hot or cold the month was, can you guess how much money it made? This code answers that question and shows which clues give the best guess.

---

## What's in the data

The code reads a file called `AICPA_regressionAnalysisData.csv`. Each row is one month, and it has these columns:

| Column | What it means |
|--------|---------------|
| `type` | Whether the row is for **training** (`dt4training`) or **testing** (`dt4testing`) the model |
| `date` | The last day of the month |
| `revenue` | Money the company made that month — *this is the thing we're trying to predict* |
| `production` | How much the company produced that month |
| `coolDD` | A measure of how hot the month was *(likely "cooling degree days" — see note below)* |
| `heatDD` | A measure of how cold the month was *(likely "heating degree days" — see note below)* |

> **Note on `coolDD` / `heatDD`:** These names are not defined inside the notebook. Based on the abbreviations they most likely mean *cooling degree days* and *heating degree days* (standard ways of measuring how hot or cold a period was). You may want to confirm this against your project or course materials before writing it up as fact.

The data in the notebook runs from **January 2011 to December 2014**.

---

## How it works, step by step

The idea is simple: **learn from old data, then test the guess on new data you didn't learn from.** That way you know if the model actually works, instead of just memorizing answers.

1. **Load the data** — Reads the CSV file into a table using pandas.
2. **Split the data into two piles:**
   - **Training pile** (`dt4training`) — the model *learns* from these months (2011–2013).
   - **Testing pile** (`dt4testing`) — the model is *quizzed* on these months (2014) to see how good its guesses are.
3. **Build a model** — Uses `statsmodels` to fit a regression line that connects the predictors (like `production`) to `revenue`.
4. **Make predictions** — Uses the model to guess revenue for the testing months.
5. **Measure how wrong it is** — Calculates the **MAPE** (Mean Absolute Percentage Error). This is the average "how far off was each guess, in percent." **Lower is better** — a MAPE of 0.14 means the guesses were off by about 14% on average.
6. **Draw a picture** — Plots the *real* revenue (green) against the *predicted* revenue (blue) so you can see how close they are.
7. **Compare every combination** — Tests 7 different sets of predictors and prints the MAPE for each, so you can see which clues make the best guesses.

---

## The results

Here are the MAPE scores that the notebook produced for each combination of predictors (remember: **lower = better**):

| Predictors used | MAPE (approx.) |
|-----------------|----------------|
| production only | 0.254 |
| coolDD only | 0.296 |
| heatDD only | 0.216 |
| production + coolDD | 0.217 |
| **production + heatDD** | **0.139 ← best** |
| coolDD + heatDD | 0.139 |
| production + coolDD + heatDD | 0.143 |

**Conclusion:** `production + heatDD` gave the lowest error, so it was chosen as the best model. (Note that `coolDD + heatDD` was almost identical — the two are extremely close, so it's worth being aware they nearly tie.)

*These numbers are copied directly from the notebook's output. If you re-run the code with different data, the numbers will change.*

---

## What you need to run it

**Python libraries used:**
- `pandas` — for holding and slicing the data table
- `numpy` — for math (imported in the notebook)
- `matplotlib` — for the chart
- `statsmodels` — for building the regression models

You can install them with:

```
pip install pandas numpy matplotlib statsmodels
```

> I'd suggest checking the exact install command and library names against the official docs if anything doesn't run — versions and package details can change over time.

**File you need:**
- `AICPA_regressionAnalysisData.csv` must be in the same folder as the notebook, or the first cell won't be able to find it.

---

## How to run it

1. Make sure the CSV file is in the same place as the notebook.
2. Open `participation.ipynb` in Jupyter Notebook or Google Colab.
3. Run the cells from top to bottom.

The notebook was written in Google Colab, so it should run there without changes.

---

## Files in this project

- `participation.ipynb` — the notebook with all the code.
- `AICPA_regressionAnalysisData.csv` — the data (you provide this).
- `README.md` — this file.

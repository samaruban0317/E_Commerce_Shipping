# E-Commerce Shipping

Team: THE ETERNAL FLAME  
Members: SAMARUBAN V; YUVARAJ K; DINESHWARA M; ROHITH KUMAR S; KATHIR S  
Department of Artificial Intelligence and Data Science (B.Tech.), Panimalar Engineering College

## Files and running the analysis

- `E_Commerce_Shipping.ipynb`: analysis, explanations, saved outputs and charts.
- `Train.csv`: original dataset, kept beside the notebook.
- `requirements.txt`: tested Python package versions.

From this folder, install packages with `python -m pip install -r requirements.txt` and start Jupyter using `python -m jupyterlab`. Open the notebook, restart its kernel, and run all cells in order. The relative path `Train.csv` assumes this folder is the working directory. The notebook does not modify the CSV.

Verified using Python 3.14. The notebook uses NumPy, Pandas, Matplotlib, SciPy and Seaborn. Saved outputs allow inspection without rerunning, but reproducing the analysis requires the CSV and packages.

## Dataset and outcome

Source: Prachi Gopalani, *E-Commerce Shipping Data*, Kaggle: https://www.kaggle.com/datasets/prachi13/customer-analytics

There are 10,999 rows and 12 original fields. `Reached.on.Time_Y.N` is renamed to `Delayed`: 1 means late and 0 means on time in this dataset. No missing values or duplicate rows were found by the implemented checks, so no records were removed or imputed. ID is a record label and is excluded from business comparisons.

## Main findings and new checks

- Overall late rate: 59.67%.
- Every discount above 10 is paired with a late label; this needs a source-system audit.
- Among discounts 1-10, the baseline late rate is 46.89% (95% Wilson interval 45.82-47.96%).
- Weight Q2 remains associated with lateness after Holm correction across the 18 listed chi-square comparisons. The restricted prior-purchase p-value changes from 0.017 to 0.190 after correction.
- Combining light weight/few purchases with Weight Q2 flags 1,262 orders, finds 829 late orders, and raises 433 false alarms. Precision is 65.69%, recall 21.17%, and review workload 15.11% of the discount 1-10 subset.
- The notebook shows 95% Wilson intervals, raw and adjusted p-values, effect sizes, and expected cell counts. Very small computed p-values can underflow to zero; zero in the output means below numerical precision, not certainty.

## Interpretation and remaining limitations

The rules were chosen after examining this file. Confidence intervals assume independent observations; neither these intervals, multiple-testing correction, nor the random-half check makes this an independent validation. The Holm adjustment addresses only the listed test family. Conditioning on discount does not remove all potential confounding.

The project identifies investigation priorities and review tradeoffs. It has not shown that changing discount, weight, or shipping mode prevents delays. New order, dispatch, promised-arrival, actual-arrival, carrier, route and interaction timestamps are needed to validate future performance and test an intervention. No data or causal effect has been invented to fill those gaps.

## Submission checklist

The paper and notebook omit personal task assignments. All five members' roll and registration numbers are included in the notebook and paper. The supplied brief also mentions a presentation/recording: that separate deliverable is not included in this code-and-paper package. Confirm the portal's exact upload and ZIP naming requirements.

## Find the calculations cited in the paper

Cell numbers below count all notebook cells from 1, including markdown. Saved code execution numbers are also shown.

| Calculation | Notebook cell | Code execution |
|---|---:|---:|
| Original warning rules | 57 | 31 |
| Random-half check | 61 | 33 |
| Wilson intervals and union rule | 66 | 35 |
| Holm correction across 18 tests | 69 | 36 |

Holm adjustment is implemented with NumPy sorting and cumulative maxima; Wilson intervals use the SciPy normal quantile and the Wilson formula. These do not require statsmodels. The notebook contains 71 total cells and 36 executed code cells. A view ending at cell 30 is incomplete.

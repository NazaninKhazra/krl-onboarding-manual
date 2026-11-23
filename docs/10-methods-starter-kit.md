# 10. Methods Starter Kit

This kit introduces the empirical methods most lab projects use. Each section gives the main idea, the key assumption, a short Python example, and one or two references for further study. The examples use `pandas` and `statsmodels`. More complete code is on the lab's events page (<https://krlresearchlab.github.io/events.html>) and in the data catalogue (<https://www.nazaninkhazra.com/data-catalog>).

## 1. Regression basics

Ordinary least squares (OLS) estimates how the average of an outcome changes with a variable, holding other included variables fixed. The coefficient has a causal reading only if nothing left out of the model is related to both the variable and the outcome.

```python
import statsmodels.formula.api as smf

model = smf.ols("rent ~ distance_to_transit + bedrooms + C(year)", data=df)
result = model.fit(cov_type="cluster", cov_kwds={"groups": df["neighbourhood"]})
print(result.summary())
```

Cluster standard errors at the level where the treatment varies or where outcomes are likely to be correlated.

**Reference:** Angrist, J. D., and Pischke, J.-S. (2015). *Mastering 'Metrics*. Princeton University Press, Chapter 2.

## 2. Difference-in-differences (DiD)

DiD compares the change in an outcome for a group affected by a policy with the change for a group that was not affected. The key assumption is parallel trends: without the policy, both groups would have changed by the same amount.

```python
df["post"] = (df["year"] >= 2022).astype(int)
df["treated_post"] = df["treated"] * df["post"]

did = smf.ols("outcome ~ treated_post + C(unit) + C(year)", data=df).fit(
    cov_type="cluster", cov_kwds={"groups": df["unit"]}
)
print(did.params["treated_post"])
```

With unit and year fixed effects, the coefficient on `treated_post` is the DiD estimate. When units are treated at different times, this simple version can be biased; see Callaway and Sant'Anna (2021).

**References:** Cunningham, S. (2021). *Causal Inference: The Mixtape*, Chapter 9 (free at <https://mixtape.scunning.com/>). Callaway, B., and Sant'Anna, P. H. C. (2021). "Difference-in-Differences with Multiple Time Periods." *Journal of Econometrics* 225(2): 200–230.

## 3. Event study

An event study estimates a separate effect for each period before and after treatment. The pre-treatment estimates test parallel trends: they should be close to zero.

```python
df["rel_year"] = df["year"] - df["treat_year"]   # NaN for never-treated units
df["rel_year"] = df["rel_year"].clip(-4, 4).fillna(-1)  # -1 is the omitted period

es = smf.ols(
    "outcome ~ C(rel_year, Treatment(reference=-1)) + C(unit) + C(year)", data=df
).fit(cov_type="cluster", cov_kwds={"groups": df["unit"]})
```

Plot the coefficients with their confidence intervals against `rel_year`.

**Reference:** Shapiro, J. M., and Sun, L. (2023). "Linear Panel Event Studies." NBER Methods Lectures, slides and videos. <https://www.nber.org/lecture/2023-methods-lectures-jesse-shapiro-and-liyang-sophie-sun-linear-panel-event-studies>

## 4. Synthetic control

When only one or a few units are treated (for example, one city), synthetic control builds a comparison unit as a weighted average of untreated units. The weights are chosen so that the synthetic unit matches the treated unit before the policy. The method works best with a long pre-treatment period and a good match.

Python package: `pysyncon` (<https://github.com/sdfordham/pysyncon>). The lab's March 2026 seminar included a hands-on synthetic control workshop, and its slides and code are on the events page.

**Reference:** Abadie, A. (2021). "Using Synthetic Controls: Feasibility, Data Requirements, and Methodological Aspects." *Journal of Economic Literature* 59(2): 391–425.

## 5. Checks every project should run

- Summary statistics for treated and control groups before treatment.
- A plot of raw outcome trends by group over time.
- Results with and without control variables.
- A placebo test: a fake treatment date or a group that should not be affected.
- A check that results do not depend on one unit or one year.

## Free resources

- Shapiro's "Some Data Recipes": <https://jmslab.github.io/DataRecipes/>

- *Causal Inference: The Mixtape* (Cunningham): <https://mixtape.scunning.com/>
- *The Effect* (Huntington-Klein): <https://theeffectbook.net/>
- *Python for Data Analysis* (McKinney): <https://wesmckinney.com/book/>
- QuantEcon lectures: <https://quantecon.org/lectures/>
- Chapters 4 and 5 of the Research Mentoring TA Manual, on common errors in code and empirical results: <https://github.com/NazaninKhazra/research-mentoring-ta-manual>

# The Difference-in-Differences Model

`The Difference-in-Differences (DiD)` or `diff-in-diff` model is a statistical technique used in `econometrics` and other fields to estimate `causal effects` in observational studies. It is commonly employed when analyzing the impact of a `treatment` or intervention by comparing the changes in outcomes over time between a `treatment group` and a `control group`.

Suppose, we have a DataFrame with features: `'group'`, `'time_period'`, and `'outcome'`. 

- `'group'` is a binary indicator for the treatment group (`1 for treatment`, `0 for control`)

- `'time_period'` is a binary indicator for the post-treatment period (`1 for post-treatment`, `0 for pre-treatment`)

- `'outcome'` is the outcome variable

The key idea of DiD is that the treatment effect is estimated by comparing the changes in the treatment group with the changes in the control group over time.

***The basic equation for a Difference-in-Differences (DiD) model can be expressed as follows:***

$Y_{it} = \beta_0 + \beta_1 \text{group}_{i} + \beta_2 \text{time\_period}_{t} + \beta_3 (\text{group}_{i} \times \text{time\_period}_{t}) + \epsilon_{it}$

Where,
- $Y_{it}$ is the outcome variable for observation i at time t.

- $group_i$ is a binary indicator variable for whether observation $i$ received the treatment (1 for treatment group, 0 for control group).

- $time\_period_t$ is a binary indicator variable for whether the observation is in the `post-treatment` period or `pre_treatment` period(1 for post-treatment, 0 for pre-treatment).

- $\text{group}_{i} \times \text{time\_period}_{t}$ is the interaction term between treatment and post-treatment indicators.

- $β_0$ is the intercept, representing the average outcome in the control group during the pre-treatment period.

- $β_1$ is the average treatment effect on the control group during the pre-treatment period.

- $β_2$ is the average time effect on the control group.

- $β_3$ is the DiD estimator, representing the average treatment effect on the treated group. It shows the differnetial treatment effect.


we can insert the values of `group` and `time_period` using the table below and see that coefficient ($\beta_3$) of the interaction of `group` and `time_period` is the value for DID：

|              | Control Group (g=0) | Treatment Group (g=1)                   |                 |
|--------------|---------------------|-----------------------------------------|-----------------|
| Before (t=0) | $\beta_0$           | $\beta_0 + \beta_1$                     |                 |
| After (t=1)  | $\beta_0 + \beta_2$ | $\beta_0 + \beta_1 + \beta_2 + \beta_3$ |                 |
| Difference   | $\beta_2$           | $\beta_2 + \beta_3$                     | $\beta_3$ (DID) |

The goal is to estimate the DiD coefficient $(β_3)$, which captures the average treatment effect by comparing the change in outcomes over time between the treatment and control groups.

## Assumptions
The key assumption of the DiD model is the `parallel trends assumption`. It assumes that, in the absence of treatment, the average outcomes of the treatment and control groups would have followed a parallel trend.

## Practical Application:
- Econometricians use the DiD model to evaluate policy interventions, such as the impact of a new law or program on economic outcomes.

The DiD model is a powerful tool for estimating causal effects in observational data by leveraging the differences in trends over time between treated and control groups.

Here's a basic outline of how to implement a `Difference-in-Differences` model in Python using the statsmodels library:

The dataset is adapted from the dataset in [Card and Krueger (1994)](https://davidcard.berkeley.edu/papers/njmin-aer.pdf), which estimates the causal effect of an increase in the state minimum wage on the employment. 

- On April 1, 1992, New Jersey (`NJ`) raised the state minimum wage from 4.25 USD to 5.05 USD while the minimum wage in Pennsylvania (`PA`) stays the same at 4.25 USD. 
- Data about employment in fast-food restaurants in `NJ` and `PA` were collected in `February 1992` and in `November 1992`.
- 384 restaurants in total after removing null values.

-  - `state` is `0 for the control group` (PA) and `1 for the treatment group` (NJ).
-  - `time` is `0 for before` (i.e., before April 1, 1992) and `1 for after` (i.e., after April 1, 1992).
 
## Usage
Install required libraries by running this-

```bash
pip install -r requirements.txt
```

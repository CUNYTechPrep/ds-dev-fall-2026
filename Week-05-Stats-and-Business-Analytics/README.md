# Week 05: Stats and Business Analytics — Probability Distributions

Hands-on notebooks for learning the probability distributions that show up most in business analytics, split into three levels so everyone can find the right challenge.

## Files

| File | What it is |
|---|---|
| `Business-Stats-Distributions.ipynb` | Main lecture/exercise notebook (Beginner → Intermediate → Advanced) |
| `Business-Stats-Distributions-SOLUTIONS.ipynb` | Worked solutions for every exercise, with explanations |
| `README.md` | This file |

## Setup

The notebooks need `numpy`, `pandas`, `matplotlib`, and `scipy` (all included with Anaconda).

```bash
pip install numpy pandas matplotlib scipy
```

Open the notebook, select your Python kernel, and run all cells. A fixed random seed means everyone gets the same numbers.

## How to use this

**Students:** Start with 🟢 Beginner. Move on when you can explain, in plain English, what each distribution models and give a business example. Try each exercise before opening the solutions notebook. Reading a solution is not the same as being able to write one.

**Instructors/TAs:** The whole notebook is more than one class. A suggested split:

| Part | Suggested use | Approx. time |
|---|---|---|
| 🟢 Beginner | Live-code in class, or assign as pre-class | 30–40 min |
| 🟡 Intermediate | Live-code 2–3 of the business questions (Q2 staffing and Q5 misleading mean land best), assign the rest | 45–60 min |
| 🔴 Advanced | Optional stretch / homework for students who finished early | self-paced |

The A/B test in Advanced A3 is set up so the p-value lands just above 0.05 while the Bayesian analysis says B is ~97% likely to be better. It makes a good discussion question and pairs with the A/B testing slides.

## What's in the notebook

### 🟢 Beginner: Meet the Distributions
What a distribution is, discrete vs. continuous, and a simulation + plot of each distribution with its mean and median.

| Distribution | Business example |
|---|---|
| Bernoulli | Did this visitor convert? |
| Binomial | Conversions out of 500 visitors |
| Normal | Delivery time |
| Poisson | Support tickets per hour |
| Exponential | Minutes between tickets |
| Uniform | Random promo discount |
| Log-normal | Revenue per customer |
| Pareto | Revenue per product (80/20) |

### 🟡 Intermediate: Answering Business Questions
Using `scipy.stats` methods (`pmf/pdf`, `cdf`, `sf`, `ppf`) to answer:
- Is today's low sales number suspicious? (binomial, the logic behind p-values)
- How many support agents do we need? (Poisson, planning for tails, not averages)
- How often do customers arrive back-to-back? (exponential)
- What delivery time should we promise? (normal percentiles / SLAs)
- Why is "average revenue per customer" misleading? (log-normal)
- Is our product revenue really 80/20? (Pareto)
- The Central Limit Theorem, the t-distribution, and confidence intervals

### 🔴 Advanced: Working With Messy Data
- Fitting distributions to unknown data (AIC, KS statistic, Q-Q plots)
- Overdispersion: when Poisson fails and the negative binomial works
- A/B testing, frequentist (two-proportion z-test) vs. Bayesian (Beta-Binomial)
- Bootstrapping confidence intervals for medians
- Monte Carlo simulation to forecast monthly revenue

## Common mistakes

- **Off-by-one with discrete distributions.** `sf(k)` is P(X > k). For "k or more", use `sf(k - 1)`.
- **Reporting the mean for skewed data.** For money, wait times, and anything with a long tail, the median is "typical"; the mean is for totals.
- **Planning for the average.** Staffing, inventory, and SLAs fail in the tails.
- **Misreading a confidence interval.** A 95% CI does *not* mean "95% chance the true value is in this interval". It means the method captures the true value 95% of the time.
- **Peeking at A/B tests.** Decide the sample size before the test and don't stop early just because the result looks significant.

## Videos

Most of these are from **StatQuest** (Josh Starmer): short, clear, and beginner-friendly. Full index: [statquest.org/video_index.html](https://statquest.org/video_index.html)

### 🟢 Beginner
| Topic | Video |
|---|---|
| Histograms | [Histograms, Clearly Explained](https://youtu.be/qBigTkBLU6g) |
| What is a distribution? | [The Main Ideas behind Probability Distributions](https://youtu.be/oI3hZJqXJuc) |
| Normal distribution | [The Normal Distribution, Clearly Explained](https://youtu.be/rzFX5NWojp0) |
| Binomial | [The Binomial Distribution and Test](https://youtu.be/J8jNoF-K8E8) |
| Exponential (1-min song) | [The Exponential Distribution Sing-a-long](https://youtube.com/shorts/wtLQUjfomig) |
| Sampling | [What does it mean to "sample from a distribution"?](https://youtu.be/XLCWeSVzHUU) |

### 🟡 Intermediate
| Topic | Video |
|---|---|
| Quantiles & percentiles (`ppf`) | [Quantiles and Percentiles](https://youtu.be/IFKQLDmRK0Y) |
| Expected values | [Expected Values Part 1](https://youtu.be/KLs_7b7SKi4) |
| Central Limit Theorem | [StatQuest: The Central Limit Theorem](https://youtu.be/YAlJCEDH2uY) |
| Central Limit Theorem (deeper, 31 min) | [3Blue1Brown: But what is the Central Limit Theorem?](https://www.3blue1brown.com/lessons/clt/) |
| Standard deviation vs. standard error | [Standard Deviation vs Standard Error](https://youtu.be/A82brFpdr9g) |
| Confidence intervals | [Confidence Intervals](https://youtu.be/TqOeMYtOc1w) |
| Hypothesis testing | [Hypothesis Testing and the Null Hypothesis](https://youtu.be/0oc49DyA3hU) |
| p-values | [p-values: What they are and how to interpret them](https://youtu.be/vemZtEM63GY) |

### 🔴 Advanced
| Topic | Video |
|---|---|
| Q-Q plots | [Quantile-Quantile Plots](https://youtu.be/okjYjClSjOg) |
| Fitting distributions | [Maximum Likelihood](https://youtu.be/XepXtl9YKwc) |
| Probability vs. likelihood | [Probability vs Likelihood](https://youtu.be/pYxNSUDSFH4) |
| Bayesian thinking | [Bayes' Theorem, Clearly Explained](https://youtu.be/9wCnvr7Xw4E) |
| Bootstrapping | [Bootstrapping Part 1: Main Ideas](https://youtu.be/Xz0x-8-cgaQ) |
| A/B test sample size | [Power Analysis, Clearly Explained](https://youtu.be/VX_M3tIyiYk) |
| Why you shouldn't peek | [p-hacking: What it is and how to avoid it](https://youtu.be/HDCOUXE3HMM) |

## Other resources

**Interactive**
- [Seeing Theory (Brown University)](https://seeing-theory.brown.edu/): drag sliders and watch distributions, the CLT, and Bayesian updating in real time. Great for building intuition.
- [Central Limit Theorem in action](https://cltapp.fly.dev/): StatQuest's interactive CLT demo.
- [Evan Miller's A/B Test Sample Size Calculator](https://evanmiller.org/ab-testing/sample-size.html): the industry-standard calculator for planning A/B tests. [Other A/B tools](https://www.evanmiller.org/ab-testing) include a Poisson means test and chi-squared test.

**Reading**
- [Think Stats, 3rd ed. (Allen Downey)](https://greenteapress.com/wp/think-stats-3e/): free online, stats taught through Python code, every chapter is a runnable Jupyter notebook.
- [SciPy probability distributions tutorial](https://docs.scipy.org/doc/scipy/tutorial/stats/probability_distributions.html): official guide to the `scipy.stats` methods used throughout the notebook.

**Playlists**
- [StatQuest Statistics Fundamentals playlist](https://www.youtube.com/playlist?list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9): the full series in order, if you want to go beyond this week.

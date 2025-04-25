## Cohort Analysis

Cohort analysis is a useful way to compare groups of entities over time. Cohort analysis provides a framework for detecting correlations between cohort characteristics and these long-term trends, which can lead to hypotheses about the causal drivers. Cohort analysis is also used to mine historical data.

Cohort analyses have three components: **the cohort grouping**, **a time series of data** over which the cohort is observed, and an **aggregate metric** that measures an action done by cohort members.

Four types of cohort analysis: 
- Retention
  - Retention is concerned with whether the cohort member has a record in the time series on a particular date, expressed as a number of periods from the starting date.
- Survivorship
  - Survivorship is concerned with how many entities remained in the data set for a certain length of time or longer, regardless of the number or frequency of actions up to that time.
- Returnship or repeat purchase behavior
  - Returnship or repeat purchase behavior is concerned with whether an action has happened more than some minimum threshold of times—often simply more than once—during a fixed window of time.
- Cumulative behavior
  - Cumulative calculations are concerned with the total number or amounts measured at one or more fixed time windows, regardless of when they happened during that window.


### Retention
The main question in retention analysis is whether the starting size of the cohort-number of subscribers or employees, amount spent, or another key metric—will remain constant, decay, or increase over time.

#### Example

The `age` function is applied to calculate the intervals between each `term_start` and the `first_term` for each legislator.
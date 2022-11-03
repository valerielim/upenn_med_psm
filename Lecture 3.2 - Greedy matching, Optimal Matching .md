# Lecture 3.2 - Greedy matching, Optimal Matching 

*How to program greedy matching yourself*

Steps:

1. Randomly order two lists of treated and control subjects 
2. Starting with the top of the treated list, match to the control with the smallest distance (ie., grab what seems best)
3. After matching, remove that control from list of available matches
4. Move to next treated subject
5. Repeat step 2-4 until all treated subjects are matched  

PS: create a `match_id` and assign both the treated and control pair, the same `match_id` number, like this 

```
| match_id | subject_id | group | distance | 
| -------- | ---------- | ----- | -------- | 
|        1 |          1 | treat |      ... | 
|        1 |          2 | ctrl  |      ... | 
|        2 |          3 | treat |      ... | 
|        2 |          4 | ctrl  |      ... | 
```

Package to use in R: `MatchIt` 

Note: Not always optimal. Always taking the smallest distance match does not minimize the total distance, and can sometimes still lead to bad matches.  If you change the order of the list, some matches would change, so it's not *globally optimal*.

### 1:k matches

Difference in approach: If you go for 1:k matches, after getting the first pair, cycle through the list from the first subject and find the 2nd match for them. Repeat as many times as desired. 

* Pair matching
	* closer matches
	* faster computing time 
* 1:k matches (many-to-one match)
	* Larger sample size 
	* weaker / more distance matches (because the 1st match is always most optimal) 

Note: Choosing between both is largely a bias-variance tradeoff issue. In general, its always preferable to spend those resources adding a new PAIR (ie., +1 treated, +1 control) than adding more MATCHES (ie., +0 treated, +2 control). Pair matching has less bias but more variance. Adding samples via 1:k has more bias (towards the treated or smaller group) but less variance. 

### Calipers 

> Q: Do we want to exclude treated subjects for whom there's no good match? 
> 
> A: Use Calipers!  

**Calipers** are definitions of *maximum acceptable distance* between subjects; discard matches outside that distance as "bad matches". 

Recall: the positivity assumption means that the probability of each treatement within covariate X should be non-zero. But if there's no match within a reasonable caliper, it is a sign that the posiviity assumption might be violated, aka, this subject was unlikely to be chosen as a treatment/control subject since NO EQUIVALENT exist in that group! ---> Excluding these subjects makes assumptions more valid. 

### Optimal matching 

Greedy matching is not optimal in terms of global distance measures across all pairs. 

However, its computationally demanding as sample size increases because of the *network flow optimisation* problem (details are beyond this course). 

* 100 treated + 1,000 controls = 100 x 1000 = 100,000 possible pairs
* 1,000 treated + 1,000 controls = 1,000 x 1,000 = 1,000,000 possible pairs 
* 100,000 treated + 100,000 controls = 1,000 x 1,000 = 10,000,000,000 possible pairs
* 1 mil pairings is feasible on most computers 
* 1 bil pairings is not feasible (it'll be running for a month or longer) 

**Compromises via Sparse Matching**

Constraints can be imposed to make optimal matching computationally feasible for larger data sets. For example, matching within hospitals, service areas, countries or disease categories. 

This is known as **sparse matching**, and is still acceptable given *fine balance is maintained within groups*. 

R packages: `optmatch` and `rcbalance`. 

### Assessing whether balance is maintained

*Did matching work?*

Approaches to check: Covariate balance analysis

* Stnadardized differences without looking at the outcome 
* Similar means, again without looking at the outcome 
* Look at `Table1` (a table that shows pre-matching vs post-matching differences) 

Approach 2: Hypothesis test 

* See whether means in both groups are the same after matching 
* Two-sample t-tests for continuous variables
* Chi-square tests for discrete variables 
* Check p-values
* Drawbacks: in large sample sizes, a small difference in means will have a significant p-value, even though it's still ideal because overall the mean is pretty similar
* So, standardized differences are still the preferred method

Approach: Standardized Differences 

![alt text](https://github.com/valerielim/upenn_med_psm/raw/main/images/image_7.png)

Description:

1. Find mean of treatment group
2. Find mean of control group
3. Find step 1- step 2 
4. square the std dev of treatment
5. square the std dev of control 
6. add 4 and 5 together 
7. divide 6 by 2 
8. find squareroot of 7
9. divide item 3 by item 8 

See screenshot for formula. 

Advantages:

* Does not depend on sample size
* The absolute value of SMD is useful for reporting so you'll have to calculate it anyway
* Calculate SMD for each variable you match on 
* Guidelines:
	* `<0.1` indicates good balance
	* `0.1 - 0.2` indicates adequate balance 
	* `>0.2` indicates serious imbalance, not acceptable

### Table1 

*A generic term for a summary table.*

![alt text](https://github.com/valerielim/upenn_med_psm/raw/main/images/image_8.png)

Description above: 

* The left-hand "unmatched" table shows the summary of samples and covariate distribution within the control (No-RHC) group, treatment (RHC) group, and their Standardised Mean Difference (SMD). 
* The right-hand "matched" table shows the same distribution after matching. 
* Note that the sample sizes are now equal, and the distribution of covariates are almost equal too. 
* Finally, the SMD is within healthy range for all except Age.

Note: Plotting a line graph of Covariates' SMD scores, grouped by matched/ unmatched, is very helpful to show how matching is effective in cases where you have multiple variables. Remember to draw a cut-off line at SMD = 0.1 (because less than 0.1 is ideal!)






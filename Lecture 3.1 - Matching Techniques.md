# Lecture 3.1 - Matching

**Randomised Trial**

Recap -- In causal inference, we try to understand the relationship from treatment (A) to outcome (Y), by isolating and removing any backdoor paths between A --> Y. 

In observational studies, confounds (X) could create unwanted backdoor paths between A --> Y, like this: 

```
A <--- X ----> Y
A -----------> Y
```

In a *randomised trial*, treatment (A) would be determined by a coin toss, effectively erasing the arrow from any confounds (X) to assignment (A), and removing backdoor paths from A to Y, leaving only the frontdoor path we're studying. 


```
A      X ----> Y
A -----------> Y
```
**Covariate Balance**

Covariate balance is when the distribution of pre-treatment variables X would be equal in both groups due to a randomised trial. It would also mean that if the outcome distribution ends up differing, it will NOT be due to differences in X, and can be attributed to Y instead. 

**Why not always randomise trials?**

1. Expensive 
2. Unethical to withhold medicine or inflict treatment 
3. Hard to find volunteer participants willing to accept placebo
4. Time consuming, especially on survival rate analysis, on scale of years 

**Why not always observational studies?**

1. Regulations weaker since not actively randomising or manipulating treatment
2. Broader population eligible, since not allowed to exclude, diluted effects
3. Lower data quality because no uniform standard of collection 

**Advantages of Matching**

1. Controlling for confounds is achieved at design phase already
2. Difficult statistical work will be done completely blinded to the outcomes
3. Matching reveals lap of overlap in covariate distribution. (ie., some treated people would have NO chance of getting the control treatment, which we should remove in order to not violate the positivity assumption)
4. Once groups are matched, analysis is equal to a randomised trial
5. Outcome analysis can be simple 

### Matching Types: Stochastic, Fine Balance 

TLDR: find the best match between control + treatment group, then discard the unmatched samples.

**Balance**

Matching closely on covariates can achieve a **stochastic balance** similar to a randomised trial (ie., age, gender). When it is difficult to find a good match, we can accept some non-ideal matches if both groups have the *same distribution of covariates*, aka, **fine balance**. 

* Pair 1: treated, male, age = 40 
* Pair 1: control, female, age = 45 
* Pair 1: treated, female, age = 45 
* Pair 1: control, male, age = 40 

*Above: Even though neither match is great, average age and average percent of gender are the same in both groups. In this case, we dont have great stochastic balance, but we have Fine Balance.*


Hint: It helps to make one group to have a bigger sample size than the other, in order to find matches for the rarer condition. 

* one to one 
* many to one 
* variable matching: we'll take more than one match for a given treated subject if we can find several control subjects that have fine balance with the treated. 

*How? He didn't explain, but I suppose there's some software that will let us pick matches up next.*

### Matching directly on confounders 

What's the metric of closeness, or a good match? Two options for now: 

* Mahalanobis distance
* Robus Mahalanobis distance 

*From the lecture notes*

![alt text](https://github.com/valerielim/upenn_med_psm/raw/main/images/image_5.png)

* Xi - Xj = get a vector of the differences between subject i, j
* T = transpose vector
* S = invert (power to -1 aka invert)

> take diference in age, square the difference, divide by the variance, then take the square root. 

![alt text](https://github.com/valerielim/upenn_med_psm/raw/main/images/image_6.png)

In the above image, let's say there are 6 possible control subjects that would match with the treated subject. We find the M-distance score for all of them, and pick the lowest score (lowest = closest = best). 

### Robust Mahalanobis distance

This deals with outliers where outliers can ceate a great distance and mess up the averages. In this case, we use **ranks**. So the person with the youngest might get a rank of one, and the oldest would get the rank of, if there are 100 people, then they get ranked 100. This helps if the values and range are extreme between the largest and second largest score. The ranks also put everything on the same scale. 

### Alternatives

You can also use software to use a propensity score, then do a **distance match** on the propensity score (topic covered in another course - just fyi that it exists). 

You can also apply **greedy matching** (nearest-neighbour approach). This has the advantage of being computationally fast. 

There's also **optimal matching**, but this is computationally demanding on larger datasets. 




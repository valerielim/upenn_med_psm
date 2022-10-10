# Youtube Notes

*This is one of the best, short and sweet introductions to the subject of Propensity Score Matching. I found it clearer than the UPenn Course so I've included it here too.*

[![Best Propensity Score Matching Explanation on Youtube](https://github.com/valerielim/upenn_med_psm/blob/main/Lectures/psm_youtube.png)](https://www.youtube.com/watch?v=ACVyPp1Fy6Y)

### Application

Suppose an NGO has built health clinics in several villages. These were not selected randomly as the NGO built clinics in areas needed most. You have data on village characteristics before and after the program. What's the effect of the program on infant mortality rate? 

**Option 1**: We can compare the average infant mortality rate in villages with clinics vs. villages with no clinics

 * But this would be unfair since we know villages with the NGO's clinics are also in areas that need it the most  

**Option 2**: We can compare the average infant mortality rate in villages with clinics, before the clinics came, vs. after the clinics came. 

* But suppose we don't have data on their infant mortality rate before treatment, since this would mean withholding treatment for X period of time to collect data, which is unethical 

**Option 3**: Use propensity score matching. 

### The Basic Idea

1. **Create a new synthetic control group**, where for each observation in the treatment group, select a control observation that looks closest to it, based on selection variables (ie., background characteristics)
2. **Compute the treatment effect**, by comparing hte average outcome in the treatment group, with the average outcome in the control group. 

**Issues with matching**

Imperfect matching: 

* Many treatment observations might match to only 1 control observation 
* Many treatment observations may not find an equal match in the control observation group 
* Many control observations may not find an equal match either 

### Multi-variate Matching 

Q: How do you actually match treatment observations to controls, especially when more than selection variable is involved? 

A: Use logistic regression to create a propensity score

> Formula: Probability (T = 1 | X1, X2 ... Xk) 

In english: regress the selection variables (aka the independent variables) like poverty rate, per-capita doctors, against the treatment variable (aka the dependent variable), infant mortality rate. 

This will produce a coefficient on the **predicted probabiliy of treatment**, aka the Propensity Score, PS1. 

How to read this? "Village A has a .928 chance of being selected for this program since it has 0.7 poverty rate and 0.1 per-capita doctors. Meanwhile village Z has only a 0.007 chance of being selected for this program since it has 0.2 poverty rate and 0.04 per-capita doctors." 

### Create synthetic control group

Using the propensity scores, match each observation in the treatment group, to an observation in the control group, with the **closest propensity score**. 

Note: observations in the control group can repeat / be selected multiple times. 

### Calculate Treatment Effect

Get the average infant mortality across all observations in your treatment group, and compare that against the average infant mortality in your synthetic control group. 

However, note that these results only generalise well to villages that look like the treatment group, and not villages with a whole other set of characteristics. 

### Quality check

How do we know how well the matching process worked? 

Ideally, we want the synthetic control group to look as close to the treatment group as possible. But sometimes we simply don't have similar data points to compare to. 

There are a few ways to evaluate and recognise this situation: 

1. Look at covariate balance between treatment and synthetic control group 
2. Compare distributions of propensity scores in both treatment and synthetic control group 
3. Compare distributions of propensity scores in both treatment and *original* control group 

### Matching vs. Regression

Q: Yes, they both solve for the same problem. So why not just control for the variables that could determine selection? 

A: Matching has these advantages. 

* Not as sensitive to the functional form of the covariates (ie., quadratics)
* Easier to assess whether its working (see prev section)
* If your treatment is rare, you may have a lot more control observations that are not as comparable, that PSM takes care of, but regression does not. Its easier to ignore irrelevant controls. 
* Its easier to think about the key determinants of treatment placement, rather than determinants of actual outcomes, which makes PSM less error prone 
* Simply easier to explain in human concepts to non-technical audience than a heavy multiple-regression model 

But regression has these advantages:

1. Regression can estimate the effect of a continuous treatment; not so easy in a matching framework.  
2. Regression shows you the effect of ALL variables, not just treatment. 
3. Lets you estimate interactions of treatment effects with covariates
4. There are so many ways to use PSM that its hard to replicate analysis; so you have to make somewhat arbitrary decisions about how to generalise it on your next population. Regression gives you the same answer every time. 

**Warning: What matching does NOT help with!!!**

Omitted variables that affect both outcome and whetheran obervation was treated (ie., unobserved confounders) will still remain invisible!! We have to account for these with other methods, such as creating additional instrumental variables, or thru difference-in-differences methods. 

**Further reading:**

* *Mostly Harmless Econometrics*, Section 3.3 Angrist and Pischke (2009)
* *Propensity Score Analysis: Statistical Methods and Applications*, Guo and Fraser (2014) 

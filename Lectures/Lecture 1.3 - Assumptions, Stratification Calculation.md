# Lecture 1.3 - Assumptions, Stratification Calculation

### Causal Assumptions

**Identifiability**

* Identifiability refers to variables that you can identify from data
* The identifiability of causal effects require making some untestable assumptions, known as causal assumptions

4 Causal Assumptions:

1. Consistency
* Ignorability
* Positivity 
* Stable Unit of Treatment Value Assumption (SUTVA) 
	* Units do NOT inferfere with each other
	* Only ONE version of treatment 

Example of violations of **SUTVA** / interference / contagion / spillover:

* Behavioral interventions, but patients between groups chat with each other
* Vaccine studies, where what vaccine a person gets, depends on what vaccine their family member gets 

Example of violations of only ONE version / **consistency** assumption: 

* Behavioral interventions but not properly applied, counsellor is nicer to some patients than others 
* Pretty straightforward really 

Example of **ignorability** assumption: *(most important!!)*

* Given pre-treatment covariate X, treatment assignment is independent from the potential outcomes
* Amongst people with the same value X, we can think of A being randomly assigned 
* Example: within controlled groups of age or same sickness, treatment is randomly assigned

Good Example: physician assigns treatment amongst sick people equally, and not because some are older, or poorer. 

If confounded by age, like the physician gives treatment to those who are older ... BUT older people are also more likely to have an outcome like hip fractures regardless of treatments ... then the ignorability assumption is violated. 

However, we can also look at treatment WITHIN age groups, and make age a known covariate. This way, we can say that *within younger/older age subpopulations*, treatment is randomly assigned, and move on with our analysis. 

Example of **positivity** assumption:

* For every set of value for X, treatment assignment is not deterministic
* There is a likelihood of getting treated / not treated 
* Example: All old people MUST get treated, but not all young people need to get treated
* Violating this makes it impossible to collect data on what happened if people did NOT get treated 
* Variability in treatment assignment is important for identification 

### Linking assumptions to actual outcomes

*This section is really just about proving and explaining the notation formula with regards to the 4 assumptions, but doesn't introduce anything new.*

> E(Y|A=a, X=x) involves only observed data

Expected value of Y given treatment A = a, and covariate X = x, like age. This must therefore be true as 

* E(Y^a | A=a, X=x) by consistency 
* E(Y^a | X=x) by ignorability (since treatment assignment is random within X) 

If we want a marginal causal effect, we can average over group X. 

# Stratification & Standardization

### Stratification

Standardization is also known as "conditioning and marginalising". 

(put the image here)

**Notation**

* E(Y^a): the expected value of outcome given treatment a
* Summation x: The average value across all levels of X 
* E(Y|A=a, X=x): The expected value of outcome given treatment A=a, at level X=x
* P(X=x): the distribution of x across all levels of X (which you multiply by the summation to get the average) 

... This formula is known as standardization, or the standardized mean. This is basically just stratifying and then averaging:

* Obtain treatment effect at each level of x, or stratification
* Weigh by the probability of x (aka the sample size of each level) 
* Estimate treatment effect by computing the means with each stratum and treatment, then pooling across stratums

**Example**

* Treatment: Study compares two diabetics treatment, Saxagliptin (sat) vs. Sitagliptin (sit). 
* Outcome: Major Adverse Cardiac Event (MACE). 
* Challenge: Sax drug users were more likely to also have past use of other oral antidiabetic (OAD) drugs. OAD patients are at higher risk for MACE outcomes (ignorability assumption is at risk of being violated)  

**How to solve?**

* Compute rate of MACE for sax and sit in two subpopulations
	* Group 1: Patients with prior OAD use
	* Group 2: Patients with no prior OAD use 
* Take the weighted average, where weights are based on proportions of people in each group
* There will be a causal effect if, within levels of prior OAD use, treatment can be thought of as randomized (ie., ignoraibility assumption is addressed). 	

**Worked example**

(image 2) 

(image 3) 

(image 4)

... In conclusion, the effect of Sax on MACE rates (7.7%) is the same as the effects of Sit on MACE rates (7.7%), so there's the causal effect - they are equally likely to cause MACE. 

**Problems with Standardization**

Typically, there will be many many X variables needed to achieve ignorability. Stratification is laborious, and would lead to many empty cells (because there's no people with that combination).

Example: Age + blood pressure combination, there would be some combinations of age + blood that you simply have no data for. 

**Alternatives with standardization** 

This course focuses on alternatives: 

* Matching
* Inverse probability of treatment weighting
* Propensity score methods
* Natural experiments with a randomizer 
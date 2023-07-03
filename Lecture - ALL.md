# Lecture 1.1 -– Notations, Potential Outcomes, Counterfactuals

### Intro 

This course will focus on causal inference from *observational studies* and *natural experiments*. Excludes: Randomized control trials.

> "Observational studies are an interesting and challenging field which demands a good deal of humility, since we can claim only to be groping toward the truth." - Cochran, 1972

**Why study CI?**

Causal inference can be easily mistaken, sometimes because of personal anecdotes. People have strong beliefs about causal effects in their own lives, and like to tell us about us. 

* Playing video games and academic performance
* Prostate cancer and drinking beer
* Divorce rates and rates of margarine consumption in Maine 

Some correlations are clearly silly but others may appear to be seriously related, which is why we need the field of CI to determine what is what.  

**Remember, Causality is Directional**

Example of green spaces and physical fitness amongst citizens. If you have a green space, does that encourage people to exercise? Or do people who are physically fit actively prioritize living near a green space?

**Causal Modelling / Inference** 

1. Formal definitions of causal effects
2. Assumptions necessary to identify causal effects from data
3. Rules about which types of variables need to be controlled for
4. Sensitivity analysis on the impact of violations of assumptions on your conclusions

**Brief History & Milestones of Causal Inference (since 1970s)**

* Wright 1921 & Neyman 1923 
* Re-introduction of potential outcomes via Rubin Causal Model, 1974
* Causal diagrams creation by Greenland & Ruin, 1983 
* Propensity scores (Rosenbaum & Rubin, 1983)
* Time-dependent confounds (Robins 1986, Robins 1997)
* Optimal dynamic treatment strategies (Murphy 2003, Robins 2004)
* Targetted learning / ML approach (van der Laan 2009)

### Notation, Potential Outcomes

Suppose we are interested in the causal effects of treatment A on outcome Y. Treatment notation examples:

* `A = 1` if receive vaccine, `A = 0` otherwise
* `A = 1` if take statins, `A = 0` otherwise
* `A = 1` if receive active drug, `A = 0` for placebo

Outcome notation examples: 

* `Y = 1` if recovery, `A = 0` otherwise
* `Y = 1` if develop disease within 2 years, `Y = 0` otherwise
* `Y = time until death`

Notation of Potential Outcomes: 

> Y^a is the outcome that would be observed if treatment was set to A = a (a particular value). 

Each person would have two potential outcomes, Y0 or Y1. 

Applied notation example 1 (Note: I personally feel example 2 is better, example 1 was not explained well): 

> Suppose treatment is influenza vaccine and the outcome is the time until the individual gets the flu.

* A1: Gets influenza vaccine
* A0: No vaccine 
* Y1: time until indviidual would get the flu if they received vaccine
* Y0: Time until individual would get the flu if they did NOT receive vaccine 

Applied notation example 2: 

> Suppose treatment is regional vs. general anaesthesia for hip fracture surgery, and the outcome we're evaluating is major pulmonary complications. 

* A1: Regional anaesthesia
* A0: General anaesthetsia
* Y1 = 1: Given regional ats, gets complications
* Y1 = 0: Given regional ats, does NOT get complication
* Y0 = 1: Given general ats, gets complications 
* Y0 = 0: Given general ats, does NOT get complications 

### Counterfactual Outcomes 

Counterfactual outcomes are outcomes that would have been observed, had treatment been different. These are typically assumed to be the same as potential outcomes. Meaning: 

* If my treatment was A=1, then my counterfactual outcome is Y0 
* If my treatment was A=0, then my counterfactual outcome is Y1. 

Example: Did influenza vaccine (treatment A1) prevent me from getting the flu? We can write this using CI notation as:

* A1, got vaccine
* A0, no vaccine
* Y1=1, given vaccine, got flu
* Y1=0, given vaccine, no flu
* Y0=1, no vaccine, got flu 
* Y0=0, no vaccine, no flu 

Let's say I got the vaccine and did not get sick. 

* Treatment = got vaccine = `A1`
* Observed outcome = no flu, `Y1`

Rephrasing the question as a counterfactual: What would have happened (contrary to fact) -- had I NOT gotten the vaccine, would I have gotten sick?

* Treatment = no vaccine = `A0`
* Counterfactual outcome = got flu = `Y0`

**Link between Potential Outcomes and Counterfactuals**

Before any treatment decision is made, any outcome is a potential outcome, Y0 and Y1. 

After treatment, there is an observed outcome, `Y = Y^A`, and counterfactual outcomes `Y = Y^(1-A)`. 

---------------------------------------------------------------------

# Lecture 1.2 -- Hypothetical Interventions, FPCI, Subpopulations

### Hidden versions of treatment 

> "No causation without manipulation" - Holland (1986)

It is common to assume there are no **hidden versions** of treatment. 

For example, we're interested to know the causal effect of body mass index (BMI) on health outcomes. This creates a problem because there are many potential ways to achieve a BMI of a particular value, and each *way* might be associated with different *outcomes*: 

* Exercise = lower BMI = healthy
* Weight loss medication = lower BMI = but unhealthy 
* Severe illness = lower BMI = also unhealthy 

The **method** used to issue treatment might also affect the outcome! 

--> BMI is not directly manipulable, since it holds hidden versions of treatment. It is better instead to think of causal effects of interventions that *aim at manipulating BMI*. 

### Immutable Variables 

Immutable variables are ones that we can't change, like race, gender, age. It would be very difficult to find the causal effect of race on anything, since when we think of potential outcome `Y^a`, we imagine that we could hypothetically set treatment `A = a` then see an outcome. 

* "What if your race was different?" 
* "What if your age is different?" 

Yes, its widely recognised that there are causal effects with race, gender, obesity, but it doesnt fit cleanly into this kind of causal framework, and it's a very hard problem to solve, so we're going to focus this course on **hypothetical interventions** instead. 

Side note: We can try to manipulate them via proxy instead, for example: 

| No direct intervention | Intervention proxy | 
| ----- | ----- | 
| Race | Name on resume | 
| Obesity | Bariatric surgery | Socio-economic status | Gift of money | 

Q: How to know if its immutable or not? A: Imagine if its possible to have a hypothetical randomized trial, ethical or not. 

* Yes: A trial about smoking or not smoking
* No: A trial to change gender or BMI 

Also, it is better to focus on non-immutable variables because these produce hypothetical interventions that lead to **outputs that are potentially actionable and useful** instead. 

# Causal Effects 

### Definition

Variable A had a *causal effect* on outcome Y if Y1 differs from Y0 (ie., Y1 > Y0 or vice versa).

Yet another example: 

* A1: Take ibuprofen
* A0: No ibuprofen
* Y1: Headache went away one hour from now 
* Y0: Headache did not go away

"I took ibuprofen and my headache is gone, therefore the medicine caused my headache to go away"

- Not proper causal reasoning
- Y1 = 1. Given ibu, headache went away. A1, Y1. 

What would have happened if you did not take ibuprofen, or A0? 

- Y0 = 1. Given no ibu, headache still went away? 

There is only a causal effect if Y1 =/= Y0. Meaning, we can say a treatment has a causal effect, only if the likelihood of headache going away is DIFFERENT from the likelihood of headache not going away. 

### Fundamental problem of causal inference

The fundamental problem of causal inference is that **we can only observe ONE potential outcome for each person.**

However, with certain assumptions, we can estimate the population (average) causal effects. So, instead of asking if the treatment worked for me individuallly (unit level causes), we can look at it as a group. 

* Hopeless: What would happen to me if I took ibuprofen? 
* Possible: What would the rate of headache remission be if everyone took ibuprofen, vs. no one took ibuprofen?

# Subpopulations & Notations

*Hypothetical Worlds, Average Causal Effects, more notations.*

> E(Y^1 – Y^0)

* E = expected value 
* Y^1 = treatment with 1 
* Y^0 = treatment with 0

This average causal effect is the average value of Y if everyone was treated with A=1 minus A=0. 

If Y is binary, then this is a *risk difference*. A difference of potential outcomes.

**Example 1**

What's the difference in regional (A=1) vs. general (A=0) anaesthesia for hip fracture surgery on the risk of major complications? 

Let's say, `E(Y1 - Y0) = -0.1`. 

This means that the probability of major complications is lower by 0.1 if given regional anaesthesia than general anaesthesia. 

If 1,000 people were to go through this surgery, we would expect 100 fewer people to have complications under regional ats, than with general ats. 

**Example 2**

What's the difference in systolic blood pressure, if treated with thiazide diuretic medication (A=1) than with no treatment (A=0) amongst patients with hypertension? 

Let's say, `E(Y1 - Y0) = -20 mm Hg`.

This means the average blood pressure is -20 mm Hg lower, than if they did not take medicine. 

### Subpopulations, Whole populations, Conditioning vs. Setting Treatments

*Important distinction!*

> `E(Y^1 - Y^0) =/= E(Y|A=1) - E(Y|A=0)`

* E(Y^1) reads 'expected value of outcome Y, given the *whole population* was treated A=1'

* E(Y|A=1) reads 'expected value of outcome Y, given the *subpopulation* of treatment A=1'

In this case, `E(Y|A=1)` is different from `E(Y^1)` because we're **restricting** the *subpopulation* of people who actually had A=1. They might differ from the whole population in important ways. 

**Example**

For example, peole at higher risk of flu, might be more likely to get a flu shot. 

So if we're taking the expected value of Y=1 (get the flu), we're also taking it from a population of people more likely to seek treatment for it (A=1), and that's different from the expected outcome from Y=1, which is the whole population.

**More notes**

* E(Y|A=1) - E(Y|A=0) is generally **not a causal effect**, because it compares two *different subpopulations* of people who seek treatment 

* E(Y^1 - Y^0) is a **causal effect**, because it is comparing what would have happened for the same people who were treated with A=1 vs. the same people who were treated with A=0. (Hypothetical) 

### Other Causal Effects

We might be interested in even more refined causal effects, such as:

1. E(Y^1 / Y^0) reads, 'causal relative risk', aka the risk if everyone was treated instead of if everyone was untreated. 
* E(Y^1 - Y^0 | A=1) reads, the causal effect of treatment on the treated. Contrasting relative outcomes.  
* E(Y^1 - Y^0 | V=v) reads, the causal effect in the subpopulation with covariate V=v, like gender = m, age, race, or with certain biomarkers

**Fundamental Problem of Causal Inference**

Back to the real world, how do we use observed data to link observed outcomes to potential outcomes? What are the necessary assumptions to estimate causal effects from ONLY the observed data?  

----------------------------------------------------------

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

![alt text](https://github.com/valerielim/upenn_med_psm/raw/main/images/image 2.png)

![alt text](https://github.com/valerielim/upenn_med_psm/raw/main/images/image 3.png)

![alt text](https://github.com/valerielim/upenn_med_psm/raw/main/images/image 4.png)

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

# Lecture 1.1 -- Notations, Potential Outcomes, Counterfactuals

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


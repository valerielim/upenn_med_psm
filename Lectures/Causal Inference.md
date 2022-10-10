# Causal Inference -- Week 1 

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

# Hypothetical Interventions

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

Also, because sticking to hypothetical interventions lead to **outputs that are potentially actionable and useful** instead. 

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

# Causal Effects 
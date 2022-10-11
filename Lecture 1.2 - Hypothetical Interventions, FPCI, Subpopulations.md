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


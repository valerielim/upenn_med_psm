# Quiz 1.3 - Graded

**Question 1: The Fundamental
Problem of Causal Inference is that:**

1. we can only observe one potential outcome for each subject -- correct
* treatment is typically not randomly assigned
* causal effects are only well defined
for hypothetical interventions

*Discussion: The first option is the correct definition of FPCI. The second option is the definition of a violation of the ignorability assumption. The third option is a similar but incorrect statement about FPCI.*

**Question 2: Which of the following represents the causal effect of treatment on the treated?**

1. E(Y1)-E(Y0) 
2. E(Y1|A=1)-E(Y1|A=0)  
3. E(Y|A=1)-E(Y|A=0)
4. E(Y1|A=1)-E(Y0|A=1) -- correct

*Discussion: If you recall, the correct formula for causal effects of treatment on the treated is E(Y1-Y0|A=1). So, this fourth option is correct because it presents formula, albeit represented slightly differently. It shows the causal effect of treatment (E(Y1-Y0) on the treated "given (... |A1)".*

*In comparison, the first option represents the average causal effect for the WHOLE population with no specified treatment. The second option represents the difference in positive outcome effects between treated and untreated subpopulations. The third option represents the overall difference in effects between the entire treated and untreated population, regardless of positive or negative outcome.*

**Question 3: Which of the following represents the average causal effect for the population?**

1. E(Y1)-E(Y0) -- correct
2. E(Y1|A=1)-E(Y1|A=0)  
3. E(Y|A=1)-E(Y|A=0)
4. E(Y1|A=1)-E(Y0|A=1) 

*Discussion: See Question 2 for explanation.*

**Question 4: Which assumption would be violated if the effectiveness of treatment on an individual depended on the treatment status of other individuals?**

1. Ignorability
2. Positivity
3. Consistency
4. SUTVA -- correct

*Discussion: SUTVA, or Standard Unit of Treatment Value Assumption, has two main premises that (1) units do NOT interfere with each other, and (2) there should be only ONE version of treatment. Having one patient dependent on another would violate the first premise.*

**Question 5: Which assumption would be violated if we were interested in
the causal effect of treatment for people age 40-80, but everyone over age 70 received the treatment?**

1. Ignorability
2. Positivity -- correct
3. Consistency
4. SUTVA 

*Discussion: The assumption of Positivity states that for every set value of X, treatment assignment should not be deterministic, ie., there is a probability range of getting treated or not treated. In this question, everyone in a given age group received treatment, so there is no probability of not receiving treatment, therefore the positivity assumption is violated.*

**Question 6: If the consistency assumption holds, then the observed outcome for a treated subject is equal to their potential outcome under that treatment.**

* True -- correct 
* False

*Discussion: The consistency assumption requires that there be only one version of treatment, implying that an observed outcome would be expected to be similar to their own potential outcome.*

**Question 7: Which of the following can most easily be thought of as an intervention?**

* Changing medication -- correct
* Changing blood pressure
* Changing weight
* Changing ethnicity

*Discussion: Medication is the only option here that can be externally manipulated. It is not possible to change ethnicity. And it is not possible to change blood pressure or weight directly, except through other means, so these factors are proxies but changing them will not be a good intervention.*

**Question 8: Treatment assignment being ignorable given confounders, X, means:**

1. Treatment assignment is independent from X.
2. Treatment assignment is independent from the observed outcomes, given X.
3. Within levels of X, treatment assignment is independent from the potential outcomes. -- correct

*Discussion: The emphasis is on "given confounders X". This is referring to how treatment assignment should be randomised within different stratifications of X, or option 3.*

**Question 9: Computing means within levels of covariates and then combining these estimates is known as:**

1. Calibration
2. Standardisation -- correct
3. Factor Analysis

*Discussion: This is the formula for standardization. We have not covered calibration or factor analysis.*
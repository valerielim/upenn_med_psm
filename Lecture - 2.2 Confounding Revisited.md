# Lecture - 2.2 Confounding Revisited 

Reminder: Confounders affect both the treatment and the outcome. 

**Frontdoor paths**

Frontdoor paths capture effects we're interested in. Frontdoor paths are direct effects, so we don't want to control it. Examples:

```
A -->Y
A -->Z --> Y (causal mediation)
```
**Causal Mediation Analysis** is when we're interested in how much of the effect of A on Y, is through Z. In this type of analysis, we want to quantify that effect, but we still wouldn't control for Z. 

**Backdoor paths**

Backdoor paths are variables that affect both treatment and outcome, and are not originating from the treatment. 

```
X --> Y 
|     ^
v     |
A -----
```
*(imagine an arrow going from A to Y)*

In this example, A has a direct effect on Y, but A and Y are both *associated* with each other through X, a confound. 

**Descendents of treatment**

We also need to make sure we don't accidentally control for the descendents of treatment, since those are part of the causal effects we're trying to study.


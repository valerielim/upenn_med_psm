# Lecture - 2.2 Confounding Revisited, DAGs, Paths, Disjunctive Criterion Clause

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

```
A --------------> Y
A <-- V --> W --> Y 
```
*(imagine a rectangle, with the corners A,V,W,Y)*

In this example, there are 3 backdoor paths you can control for: 

* V alone
* W alone 
* V, W together 

There is also a frontdoor path from A-->Y but that's alright. 

```
V --> M <--- W 
|            |
v            V
A ---------> Y 
```

*(imagine an M-shaped diagram with M in the valley)*

In this example:

* M is a collider
* No need to adjust

There's a frontdoor path from A-->Y, which is good. There's no information that flows from A-->Y through V or W because its blocked by M, so we don't need to adjust our analysis.

* What if we adjust for M anyway? 

⚠️ **Warning!!** Unintentionally controlling for M (collider) will open a conditional dependent relationship between V and W. V and W are independent marginally, but dependent conditionally. 

* What if we adjust for V? 

This won't introduce bias since it's not related A-->Y.
 
 ```
 Z <0--+--- 0  
 ^     |    |
 |     z    |
 |     v    v
 W --> A -->Y
 ```
 *(Ugh I'm not even going to attempt to draw this complicated DAG out. Imagine Z-->A-->Y. Meanwhile 0-->Z and 0-->Y too. Lastly, W-->Z and W-->A. The symbols near the respective arrowhead indicates 0-->Z and Z-->A.)*
 
In the graph above, there's a collision at Z (because W and V are parents), so this is blocked. 

There's two backdoor routes from A-->Y:

1. A-Z-V-Y
2. A-W-Z-V-Y

To control for the first, we can control for either Z, V, or both Z&V. 

To control for the second... There's no need, because Z is a collider, so there's no more relationship between V and W. 

✅ Acceptable: 

* Control nothing
* Control Z and W both (bc Z opens the first path, so you need to control W too)
* Z, W, V all three together 

❌ Not acceptable: 

* Z only; because this opens a new backdoor path. 
* W only; because the first path A-Z-V-Y still exists. 

Since we want to control for as few variables as possible, the best option is to control for V only. 

**Descendents of treatment**

We also need to make sure we don't accidentally control for the descendents of treatment, since those are part of the causal effects we're trying to study.

### Oh no ... 

**Q: Why are these DAGs so complicated?** 

A: Because in real life literature reviews, many factors influence both our treatment and outcome variables. We have to be ready and prepared to deal with all of them. For example, does maternal pre-pregnancy weight status affect whether a cesarean delivery is required or not? Many variables like pre-existing diabetes, maternal age, povrty index, gestational hypertension and pre-eclampsia all could be involved in various ways. So back to this, the short answer is, be prepared. 

**Q: If there are so many factors involved in each DAG, its hard to know everything involved, so what happens if I miss some of them out?**

A: We try our best to include all possible factors through expert knowledge and a thorough literature review. We can check the accuracy and completion of our DAGs through **sensitivity analysis** (covered next). This covers whether our assumptions are wrong, and by how much. Or, we could try... Disjunctive Criterions. 

### Disjunctive Criterion Clause

**Disjunctive Criterion Clause:** Control for all OBSERVED causes of the exposure.

**Advantage**: Dont need to know the whole DAG graph, selecting variables based on the disjunctive cause criterion is sufficient to control for confounding. This accounts for unobserved variables. 

Play it safe: Select variables by controlling for everything.

Note: Sometimes there's just no set of variables that you can reasonably control for to prevent backdoor paths from A-->Y. Either because it's not possible to control for a given variable in the path, or because there's unobserved variables arranged in such a way that you'd undo a collision and open relationships otherwise. 

**Summary**

Disjunctive clauses: 

* Does not always select the smallest set of variables to control for 
* Advantage: Conceptually simpler 
* Is guaranteed to select a set of variables that are sufficient to control for confounding, IF:
	* Such a set exists
	* We correctly identify all the observed causes of A and Y. 


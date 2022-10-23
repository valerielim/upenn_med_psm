# Lecture 2.1 - Confounds, DAGs, D-separation, Joint probability Distribution

**Recap**

*Remember, in identifying causal effects, we're interested in the mean difference in outcome, if everybody was treated, vs if nobody was treated.*

> Ignorability Assumption: That treatment assignment must be independent of potential outcomes.

Acceptable: 

* Using a coin flip to determine treatment assignment (because coin flips are unlikely to affect outcomes)
* People with a family history of cancer to assign cancer treatments (this affects just the outcome, so its a risk factor, but not a confound). 

### Directed Acyclic Graphs (DAGs)

* Each edge/relationship MUST have a direction
* No un-directed paths allowed
* No cycles allowed (ie., A > B > C > A)

Terms to describe relationships: 

* Parent / Child
* Ancestor / Descent

**Relationships between DAGs and probability distributions**

```
D --> A --> B      C 
```
* C is independent of other variables
* P(C|A,B,D) = P(C) 

Also

* B is directly affected by A
* B is indirectly affected by D 
* Everything can be summed up with A
* P(B|A,C,D) = P(B|A) 

Also 

* D and A have different (direct, indirect) relationships on B 
* P(B|D) =/= P(B)

Also (not sure) 

* A is child of D
* B is only marginally related to D
* P(D|A,B,C) = P(D|A) 

```
D --> B --> C 
|         ^
|         |
v         |
A ------- |
```
*Shitty diagram but imagine A also points to C*

* A is parent of C
* D is parent of A 
* A is independent of B, and conditional on C and D. 

Also

* D is conditionally independent of C, given A and B 

### Decomposition of a joint distribution

We can depose joint distributions by sequentially conditioning only on a set of parents.

**Example 1**

```
D --> A --> B      C 
```
*(same example as above)* 

> Formula for joint distribution: P(A,B,C,D) = P(C) x P(D) x P(A|D) x P(B|A) 

**Example 2**

```
D --> B --> C 
|         ^
|         |
v         |
A ------- |
```
*(same example as above)* 

> Formula for joint distribution: P(A,B,C,D) = P(D) x P(A|D) x P(B|D) x P(C|A,B) 

Note that A and B are both the parents of C, so the condition of C has to be on both parents, P(C|A,B).

**Warning!**

A probability statement may have more than one correct DAG. Probability statements that are vague like "A and B are dependent" have more than one correct DAG. 

Instead, if you start with a particular DAG, you would be able to imply more specific probability statements. 

> DAG > probability statement!!! 

### Paths and Associations

Types:

1. Fork (A --> B, and A --> C)
1. Chain (A --> B --> C) 
1. Inverted fork (B --> A and C --> A) 
1. Collider (in an inverted fork, when two paths flow to the same node, that node is a collider)

Drawing out the DAG and identifying types of paths, helps us identify what variables to control for during causal inference. 

### Conditional Independence and D-separation

Paths can be **blocked** by conditioning on nodes in a chain. This makes remaining variables *independent*, which then allows us to explore if a relationship exists between them. 

```
D --> A --> B      C 
```
In this example, if we condition on A, we block the path from D to B. 

**Example**

```
Temperature --> Icy roads --> someone falls 
```
You can ask whether any icy road would affect the probability of a person falling. But what about temperature --> someone falls? 

Let's say we condition on A, icy-roads. 

Imagine a world where the sidewalk is always icy, even when temperature is warm. In this case, we've controlled for icy sidewalks, so we can clearly see the relationship between D and B, or whether temperature is related to people falling or not. 

**Conditioning on Colliders**

```
D --> A <-- B
```

In the example above, A is a collider. Here, D and B are already independent from each other, so we don't have to do anything. No path needs to be blocked. 

In fact, if we conditioned on A, we could create the opposite effect: D and B would now be related. 
 
**Example**

Let's say we have a lightbulb A, that will ONLY be turned on if switch D and switch B, which have state "On/Off", will be turned on if both in the "On" positiong. 

In this case, knowing information about switch B, whether it is on or off, will tell us nothing about the other switch. 

However, let's say we condition on A, or whether the lightbulb is turned on or off.

Given lightbulb A is turned on, and switch B is turned on, we can tell the status of switch D and vice versa. **This shows B and D have a dependent relationship after we condition on A.** 

### D-separated paths

**Case 1:** Does a set of variables remove the dependence between two nodes if we remove it?

Examples: 

* `D--> E--> F` (true)
* `D<-- E -->F` (true)
* `D -->E<-- F` (false)

**Case 2:** Does a set of variables block every path from A to B? If yes, A and B are said to be D-separated by that set of nodes. 

Examples: 

* (not provided in lecture) 

**Why does this matter? How is this used in PSM?**

Remember, ignorability is about having independent assignment of treatment conditions, in a way that doesn't affect the outcomes. For that assumption to be valid, there should be *conditional independence between treatment variables A and the outcome variables Y*. Here, we use DAGs to map and identify which set of nodes can D-separate two other groups of nodes in order to find opportunities to create conditional independence. 

We also use DAGs to make sure ignorability holds true.


 
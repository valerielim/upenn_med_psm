# Quiz 2.2 - Graded

**Question 1:** How many paths are there from D to B? 

Open answer = `3`

* D-A-B
* D-E-G-B
* D-E-G-A-B

**Question 2:** How many backdoor paths are there from G to B? 

Open answer = `2`

* G-A-B
* G-E-D-A-B

**Question 3:** Is G independent from D, given E? 

Answer: `No/ False` 

*My explanation: G is independent from D given A, which is a collider. However, G is the descendent of D through E, so they are not independent.*

**Question 4:** Is D independent from G? 

Answer: `Yes / True`

*My explanation: D is the ancestor of G through E, so D is independent of G. We can ignore D-A-G because A is a collider.*

**Question 5:** How many parents does B have? 

Answer: `2`

*My explanation: A and G are both parents.*

**Question 6:** Assume we are interested in the causal effects of A-->Y. How many backdoor paths are there from A to Y? 

Answer: `3`

*My explanation: There are three paths, A-B-Y, A-G-Y, A-G-C-B-Y (or A-B-C-G-Y). We can ignore H because it is unrelated to A. Technically, there are only two unblocked backdoor paths, as asked in the next question. The third path is blocked. But I'll include it here since the question didn't specify.*

**Question 7:** Assume we are interested in the causal effects of A--Y. How many unblocked backdoor paths are there from A to Y? 

*My explanation: Building on the answer in the previous Question 6, there are 3 paths, but 1 is blocked, leaving 2 unblocked paths. The path A-B-C-G-Y or anything that goes through C is blocked, because C is a collider, so there is no relational dependence between parents B and G.*

**Question 8:** Conditioning on C creates a link between which two nodes?

* B and G (correct) 
* C and A 
* G and H 

*My explanation: Read the answer for question 6 & 7.*

**Question 9:** Does conditioning on G,B satisfy the backdoor path criterion? 

Answer: `Yes/ True`

*My explanation: The backdoor path criterion requires blocking all backdoor paths between the treatment and observation variable of interest. In this case, there are two unblocked paths in Question 7. Conditioning on G and B would remove both of them.*

**Question 10:** The set of variables to control for based on the disjunctive cause criterion is: 

* C,B,G,H 
* B,G,H (correct)
* G,H
* G,B 

*My explanation: The disjunctive cause criterion selects all measured covariates that are causes of the treatment or the outcome. We do not select C because it is not directionally related to B or G which are related to A and Y. Frankly I am not sure since I'm on financial aid and cannot yet submit my quiz, so if you're reading this, come back in 4 weeks when my aid gets approved.*

**Question 11:** Does the set C,B satisfy the backdoor path criterion? 

Answer: `No`

*My explanation: There is another path, AA-B-Y, that is not accounted for, so the backdoor path criterion is not fulfiled yet.*



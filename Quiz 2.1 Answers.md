# Quiz 2.1 

```
A<-- X --> Y
```

**Question 1:** What type of path is this? 

* fork (correct)
* chain
* inverted fork 

```
A -->B -->C
```

**Question 2:** What type of path is this? 

* fork 
* chain (correct)
* inverted fork 

```
D -->B -->C
     ^
A -- |
```

*(shitty diagram but imagine A points to B too)*

**Question 3:** This DAG is consistent with which factorization of the joint distribution P(A,B,C,D)?

* P(D)P(A)P(B|D,A)P(C|B) (correct)
* P(D)P(A|D)P(B|A)P(C|A,B)
* P(D)P(A)P(B|D)P(C|A)

```
A -->B -->C
```

**Question 4:** Is there a collider on the path from A to C? 

* Yes
* No (correct) 
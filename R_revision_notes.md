# R Programming Notes

Contents: 

* 1: R Programming: The basics of programming in R
* 2: Regression Models: The basics of regression modeling in R
* 3: Statistical Inference: The basics of statistical inference in R
* 4: Exploratory Data Analysis: The basics of exploring data in R
* 5: Don't install anything for me. I'll do it myself.

### Basics

```
 1: Basic Building Blocks      2: Workspace and Files     
 3: Sequences of Numbers       4: Vectors                 
 5: Missing Values             6: Subsetting Vectors      
 7: Matrices and Data Frames   8: Logic                   
 9: Functions                 10: lapply and sapply       
11: vapply and tapply         12: Looking at Data         
13: Simulation                14: Dates and Times         
15: Base Graphics        
```

### Notes 

* Create a vector: use function `concat` like `z <- c(1.1, 9, 3.14)`
* square root func `sqrt()`
* absolute `abs()`
* Any arithmetic will apply on every element of the vector, like 

```
> z 
 1.10   9.00   3.14
 
> z * 2 + 100 
 102.20 118.00 106.28
 
> sqrt(z - 1)
 0.3162278 2.8284271 1.4628739
```
* When given two vectors of the same length, R simply performs the specified arithmetic operation (`+`, `-`, `*`, etc.) element-by-element
* If the vectors are of different lengths, R 'recycles' the shorter vector until it is the same length as the longer vector

Print 

* To print every running number, use `seq` like `seq(1, 10)`
* To print every running number at specific increments, use `seq(1, 10, by = 0.5)`
* To print every running number at a given length without regard for increments, use `seq(1, 10, length = 30)`
* To check length, use `length()`

```
> seq(1, 10) 1  2  3  4  5  6  7  8  9 10

> seq(1, 10, by = 0.5) 1.0  1.5  2.0  2.5  3.0  3.5  4.0  4.5  5.0  5.5  6.0 6.5  7.0  7.5  8.0  8.5  9.0  9.5 10.0

> seq(1, 10, length = 30)
1.000000  1.310345  1.620690  1.931034  2.241379 [6]  2.551724  2.862069  3.172414  3.482759  3.793103[11]  4.103448  4.413793  4.724138  5.034483  5.344828[16]  5.655172  5.965517  6.275862  6.586207  6.896552[21]  7.206897  7.517241  7.827586  8.137931  8.448276[26]  8.758621  9.068966  9.379310  9.689655 10.000000
```

Replicate 

* To repeat print a number, use `rep` like `rep(3, times = 5)` 
* To repeat print a vector, do the same `rep(z, times = 5)`
* To repeat print each element of the vector instead, use `rep(z, each = 5)`

```
> rep(3, times = 5)
 3 3 3 3 3 
> rep(NA, 1000)
 NA NA NA .... NA NA NA NA 
> rep(c(1,2,3), times = 5)
 1 2 3 1 2 3 1 2 3 1 2 3 1 2 3 
> rep(c(1,2,3), each = 5)
 1 1 1 1 1 2 2 2 2 2 3 3 3 3 3 
```

Vectors

* Atomic vectors have only ONE data type
* Lists (also a vector) can have more than one data type 
* Logical vectors have TRUE, FALSE, NA 
* Logical operators are `< > <= >= != inequality == exact equality`
* If we want to know whether at least one statement is true, we can use **union** written as `A | B` 
* If we want to know whether both statements are true, we can use **intersection** written as `A & B`
* If we want to know whether a statement is false, or a **negation**, we can use `!A`

String vectors 

* To join strings together with a separator, use `paste(my_char, collapse = " ")`
* You can join different vectors too 

```
> paste("Hello", "World!", sep = " ")
 Hello World! 

> paste(LETTERS, 1:4, sep = "-") "A-1" "B-2" "C-3" "D-4" "E-1" "F-2" "G-3" "H-4" "I-1" "J-2" "K-3" "L-4" "M-1" "N-2" "O-3" "P-4" "Q-1" "R-2" "S-3" "T-4" "U-1" "V-2" "W-3" "X-4" "Y-1" "Z-2" 
```

Random sample 

* Draw *n* random samples from given vector 

```
> sample(LETTERS, 5) 
 A I L S U 
> sample(1:10, 2) 
 2  6 
```

### Missing Values 

* `NA` is missing value
* Use `is.na()` on vectors to print bool of whether elements are NA or not 
* Use `sum(vector_variable)` on vectors to print number of NA present 
* `NaN` is Not a Number, like infinity 

### Subsetting Vectors

To remove missing NAs and subset all numbers >0: 

```
x[!is.na(x) & x>0]
```
To subset the 3rd, 5th, 7th number in a vector: 

```
x[c(3, 5, 7]
```
To subset every element except the 2nd and 10th in a vector:

```
x[c(-2, -10)] or 
x[-c(2, 10)]
```
To select a named element "foo":

```
> x <- c(foo = 11, bar =2, norf = NA)
> x["foo"]
 11 
> x[c("foo", "norf")]
 foo  norf
 11   NA 

```
### Matrix & Dataframes 

* Matrixes can only have one single data type; dataframes can have different datatypes

Create a simple matrix with numbers 1-20, 4 rows, 5 columns:

```
matrix(data = 1:20, nrow = 4, ncol = 5)
     [,1] [,2] [,3] [,4] [,5][1,]    1    5    9   13   17[2,]    2    6   10   14   18[3,]    3    7   11   15   19[4,]    4    8   12   16   20
```

Create a simple dataframe with column names: 

```
data.frame(c("Bill", "Gina", "Kelly", "Sean"), 
	matrix(data = 1:20, nrow = 4, ncol = 5,
	)
cnames <- c("patient", "age", "weight", "bp", "rating", "test")
colnames(my_data) <- cnames

  patient age weight bp rating test1    Bill   1      5  9     13   172    Gina   2      6 10     14   183   Kelly   3      7 11     15   194    Sean   4      8 12     16   20
```

### Rest of notes 

Logic 

* `&&` evaluates only the first member of the vector 
* `&` evaluates the entire set of the vector under AND 
* `==` means equal 
* `!=` means not equal 
* `||` evaluates only the first member of a vector
* `|` evaluates the entire set of the vector under OR 
* `xor` means Exclusive OR, that one argument evaluates to TRUE and the other to FALSE 
* Order: All **AND** operators are evaluated before **OR** operators

When evaluating across uneven vectors: 

```
> TRUE | c(TRUE, FALSE, FALSE) TRUE TRUE TRUE
 
> TRUE || c(TRUE, FALSE, FALSE) TRUE   -- note: only first item was evaluated
```


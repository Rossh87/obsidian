# List summation
There is a trick to calculating the sum of consecutive integers.  Where **I** is some positive integer, consider:
```
sum(1, 2, 3, 4, ..., I) 
```

This sum will equal `(I * (I + 1)) / 2` or `(I^2 + I) / 2`.  To shift this sequence to begin at some arbitrary positive integer **K** and include **I** terms, we can express this as 
```
K + 1, K + 2, K + 3, ..., K + I
```

which yields the formula
```
I * K + (I(I + 1) / 2)
```
(In other words, *I* occurences of *K* added together, plus the normal list summation for 1 through *I*).

For gimmicky math-based algorithm problems, manipulating this equation can help us figure out factors for numbers that are guaranteed to be the sum of consecutive integers sequences.
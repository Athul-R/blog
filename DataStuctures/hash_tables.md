# Hash Tables

Usually in python or javascript it would be something like this. 

```python
fruits[grapes] = 5
```

indicating that grapes are 5 in count.

say you want to add apples are in count 10 then
```python
fruits[apples] = 10
```
We say, that the key was `apple` and the `value` is 10. 

What actually happens is for each unique string (from characters in 256 ASCII encoding), 
the programming language takes that strings and inputs to a highly optimized hashing function. 

This hashing function output a number. This number would indicate the location of the value in the memory.

Hence hashes takes O(1) time to

- access an element 
- delete an element
- insert an element
- search an element 
- depending on the language, we have flexible key types (str, int etc.)

The hashing function would be highly optimized. Explore more about hashing functions. 
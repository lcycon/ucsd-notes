# Lecture 17 #

Hashing
-------

- Hash function is O(1)
- Therefore lookup is O(1), but collisions are possible
- Average number of collisions: birthday paradox

Hash Table Size
---------------

- Should be around 1.3 times the max number of keys in the table
- Size should be a prime number

Hash Functions
--------------

- Should be very fast to compute
- Should distribute keys uniformly
- If you know the keys in advance you can construct a "perfect" function

Hash Functions for Ints
-----------------------

- K mod M
  - Assumes table size is M and M is prime
- Hash function could be a RNG, using table creation date and key value as seed
  - This is random hashing
  - Not much use in practice

Hash Functions for Strings
--------------------------

- A good function will depend on all of the characters in the string
- Summing chars is a bad idea
- Better to use coefficients for each char
  - Horner's rule

Hash Functions in other contexts
--------------------------------

- Also used in password systems, message digest systems, etc
- Password: Probability of collision must be extremely low
- 128 bit values => 2^64 keys before collision
- 160 bit values => 2^80 keys before collision

Collision Resolution Strategies
-------------------------------

### Linear Probing ###

- If location is filled, increment index, check index mod M
- Easy to implement, and guaranteed to find an empty spot
- Forms clusters, which can degrade hashtable performance

### Double Hashing ###

- Make the offset in the probe system depend on the key value
- Use a second hash function to compute the offset
- Range should be defined for 1 .. M - 1
- If the offset fxn ever returns the original index location, the table is full

### Random Hashing ###

- Probe sequence is defined using an RNG
- RNG is expensive, double hashing works just as well

Open Addressing vs Seperate Chaining
------------------------------------

- Above collision strategies are ok if keys are entries in the hashtables
  - This is "open addressing" / "closed hashing"

- Another idea: entries are pointers to the head of a linked list that contain the keys
  - This is "seperate chaining" / "open hashing"

- Collision resolution becomes trivial

Analysis of Open-Addressing Hashing 
------------------------------------

- Load factor N / M
  - N = number of keys in the table
  - M = table size
- Best case is O(1), Worst case is O(n)




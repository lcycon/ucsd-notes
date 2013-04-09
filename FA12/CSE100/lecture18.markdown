# Lecture 18 #

Dictionary
----------

- Designed to hold pairs
- Can be implemented using a list, bst, hashtable, etc.

Hashtables vs BSTs
------------------

- BSTs guarantee O(log N)
- Hashtables have best case O(1), worst case O(N)
- Search trees require keys be well-ordered.
- Hashtables only require keys be tested for equality
- BSTs are good when you care about sorted data, smallest value, closest value, etc
- Hashtable does not deal with ordering
- BST delete is as efficient as insert
- Hashtable delete is inefficient if open addressing is used
- Balanced search trees are difficult to implement
- Hash tables are easier to implement

Java's Hashtable
----------------

- Hashtable is synchronized, HashMap is not synchronized

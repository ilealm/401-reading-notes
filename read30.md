[ HOME ](README.md)
# Read 30 - Hash Tables

- We use Hast tables to Hold unique values, Dictionary and Library. 
- Hasht ables are a data structure that utilize key value pairs.
- Since we are able to hash our key and determine the exact location where our value is stored, we can do a lookup in an O(1) time complexity. 

```
["Greenwood:98103", "Downtown:98101", "Alki Beach:98116", "Bainbridge Island:98110", ...]
```

## Hashing
> A hash is the result of some algorithm taking an incoming string and converting it into a value that could be used for either security or some other purpose. In the case of a hashtable, it is used to determine the index of the array.

-  Hash code turns a key into an integer. 
- It’s very important that hash codes are deterministic: their output is determined only by their input.
- A hashtable traditionally is created from an array. I always like the size 1024. this is important for index placement. 

## Collisions
> A collision is what happens when more than one key gets hashed to the same location of the hashtable.

- The hash map needs to be able to handle two keys resolving to the same index.
- Collisions are solved by changing the initial state of the buckets. 

## Buckets

> A bucket is what is contained in each index of the array of the hashtable. Each index is a bucket. An index could potentially contain multiple key/value pairs if a collision occurs.
- The load factor tells us something about how full the hash table is.
- Calculating load factors and choosing the optimal number of buckets, and determining the best hash functions is not within the scope of this class. 
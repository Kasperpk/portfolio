**Applicatons of hash data structure**
There are many applications of hash tables. For example when compilers parse the source code, it has to lookup if the token is a keyword or if it's a variable declared. The hash table data structure is used for that. 

Many high-level programming languages have in-built hash table data structures such as python's dictionary abstract data type. 

![](client%20server.png)
Consider a network where each client get's a unique IP address. Each IP address that tries to request your server is logged in the **service access log** a DDOS attack is when an IP address makes so many requests that the log fails and the server no longer work. We wan't to be able to detect patterns before they happen and block of the IP address that tries to access the server. 

We want a data structure that holds each IP address and the count of requests have made within the last hour. 
![](pseudocode%20log.png|center)
The pseudocode for the update access list
![](pseudo-code%20update%20access%20list.png|center)
It's really easy to answer the simple questions, was the IP address accessed in the last hour
![](Accessed%20last%20hour%20pseudocode.png|center)

**How do we implement the data structure C?**
A **map** is a data structure that maps on object to the other. For example a filename can be mapped to a location, a phone number to a name, a name to a phone number, a word to a translation and so on. This is a very common data structure to use for many real applications. 

The use of a *hashfunction* is one that takes a value, computes it has value and put in the *key* and *value* into the index of some array of objects.
![](Hash%20function.png)
It's possible that some values will evaluate to the same hash value and create a *collision*. To solve that we may use *chaining* where we store the key, values in list structures instead. 
![](Hash%20with%20chaining.png)
* Select hash function *h* of cardinality *m*
* Create array Chains of size *m*
* Each elements of Chains is a doubly-linked list of pairs (name, phoneNumber) called *chain*
* Pair (name, phoneNumber) goes into chain at position *h*(ConvertToInt(phoneNumber)) in the array chains

**Coming up with good hash functions**
In the hash table data structure we strive to have fast *insertions*, *lookups* and *deletions*. Consider the phone book example. Here we would store *n* contacts. *m* is the cardinality of the hash function, *c* is the length of the longest chain. The memory used is then O(*n* +*m*) and operations to run in time O(c+1). 

A good example is shown here. Here the longest chain is 2 even though it could be 1 if all the 8 objects were stored in a unique address. 

![](hash%20table%20good%20example.png)
A bad exampe would be that all 8 objects where stored in the same key so that the longest chain (c) would be 8. 

Let's consider the phone number application, where we select cardinality m to be 1000. We could take the last three digits of the phone number (so we avoid the area code), but that could be problematic if many numbers end with 000. A better solution would be to generate a random number between 0 and 999 so we **uniformly distribute** the numbers in the hash table. The problem is that we cannot replicate that when we want to retrieve the phone number again. It must be deterministic. 

The good hash functions have to be 
* Deterministic
* Fast to compute
* Distribute keys well 
* Few collisions

**Universal family of hash functions**
The universal family of hash functions are set of functions that where collisions between two different keys happens no more than 1/m 

* We select a random function *h* from the family of universally deterministic hash functions

The **load factor** is the ratio of the number of keys stored in the hash table to the size of the hash table. If larger than 1 we can be assured that there are atleast on collision, and if it's very large we know that there is alot of collisions. On the other hand if it's very small we know that our hash table takes up more space than necessary, and so we want it to be in some medium range. 

The *lemma* states that if *h* is chosen randomly from a universal family, the average length of the longest chain *c* is *O*(1+a), where a = n/m is the load factor of the hash table. So if there is a lot more objects than the size of the table, then a will be greater than 1 and the longest chain will be greater. The **corollary** from that is that the average runtime will be proportional to the load factor as well at *O*(1+a). 

**Hash table size**
We want a hash table size of such that the load factor is between 0.5 and 1. That means we choose a size n/a for some 0.5 < a < 1. However what if we don't know the number of objects *n* before hand? 

We can lend ideas of dynamic arrays and resize the hash table when *a* becomes to large. We choose new hash function and rehash the elements. Here we create a function *Rehash* to keep the load factor below 0.9. 
![](Rehashing%20with%20alpha%20at%200,9.png|center)

Rehashing should be rare, and so the amortized running time is still O(1) even if the rehashing itself is O(n).

**Hashing phone numbers**
What we can do is convert a phone number into an integer. As a result any phone number will be converted to an integer less than 10<sup>15</sup>. If we come up with a **universal family** for integers up to   10<sup>15</sup> then we will be able to map phone numbers to names efficiently using chaining. 

The following lemma states that there exists such a universal family *h[p]* for any prime number p and this family consist of a set of hash functions parameterized by two parameters a and b, so that for any pair a,b where a is between a and p-1 and b is between 0 and p-1 - there is one hash function in this family and this hash function takes the key x which is an integer between 0 and p-1, it multiplies it by a and adds b, then takes the result modular p and finally takes the result modular m. This is a universal family of the set of integers between 0 and p-1 if p is any prime integer number. 
![](lemma%20for%20hashing%20integers.png)
Example: Here we pick the prime number *p* to be a little more than 10 million. The prime number needs to be bigger than the numbers corresponding to the phone numbers. In this case we consider only 7-digit local numbers and they can at most be 10 million.
![](example%20hash%20function.png)
We select any a and b here 34 and 2. Consider the key 1 482 567 that corresponds to the number 148-25-67. What will happen when this key is hashed? (34 x 1482567 + 2) mod 10000019 = 407185. Finally we have to 407185 mod 1000 = 185, if the cardinality or the size of the hash table is 1000. Thus *h(x)* = 185. 

In this universal family there is a total of p(p-1) number of functions since we can choose p different b and p-1 different a options. The probablity that two keys have a collision is then 1/(p(p-1)). 

We can now try to solve the general case of mapping phone numbers to names. 
![](general%20case%20hash%20function.png)
**Mapping names to phone numbers**
We can also converse the operation to map from names to phone numbers. The requires us to create efficient hash functions that can work with strings and convert that into a hash key. In conclusion when we have that, we have an efficient data structure to implement a phone book, one that on average is very efficient in search and modification at O(1) even if the worst case can be really time complex. 

**Hash table exercises**
![](exercise%201.png)
Using direct addressing, there needs to be one array entry for each possible integer from 0 to 999999999999. That requires an array of size 10<sup>12</sup>. An array of size 2<sup>12</sup> only yiels 4096. 

![](exercise%202.png)
It's possible that some integers from 0 to 999999999999 will go into the same hash when it's only of size 1000. That will be 999999999999/10000 that is 999999999 or 10<sup>9</sup>. 

![](exercise%203.png)
p has to be larger than the highest possible key we want to hash. It's also wise that it's a prime number something that we lend from number theory therefore 10000003 is a good choice. 

![](exercise%204.png)
Our hash function works for positive integers and so to build the universal family of hash functions we need to add 1000000 and then select *p* as 2000003. 
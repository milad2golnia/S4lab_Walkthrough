I think we are supposed to solve this question by assuming a practical environment. So first of all we should simplify the problem and understand how much big it is.

If we consider every file as big as a byte we are gonna to process `2^48` bytes:

`2^48 = 2^18 * 2^30 = 2^18 GB`

It's obvious we can't bring all of these files to memory and we need to utilize the hard disk. 

We also know files are often more than one byte but we can pass their content to a hash function (e.g. `SHA3-512`) and process their digests instead theirselves.  
This operation reduce file's size too much but we should keep in mind if two hashes are equal, it doesn't mean the original files are equal too because it can be result of a *Collision*.  
So **we process hashes and if we found two identical hashes, we process the original files to make sure they are truly equal**.

Because it's allowed to do tasks as automatically as we can, I use a database to do I/O works because it's more smarter and faster than what I program.  
Hence we create a table as below:
```
------------------------------------
|               |                   |
| Content Hash  |   Path to File    |
|_______________|___________________|
```
At this design, the `Content Hash` is primary key. Most of DBMSs use index over primary key by default but if you're using a DBMS which doesn't do it make sure to define an index by yourself to speed up the process of checking hashes.

Now we are ready to introduce the algorithm as below:
1. Read a file and pass it to `SHA3-512`.
2. Store the output of hash function in DB.
3. If the storing was successful, continue to step 1.
4. If there was an error while saving the hash of file, extract path of similar hash in DB and compare the original files, if they are same, notify user and continue to step 1.
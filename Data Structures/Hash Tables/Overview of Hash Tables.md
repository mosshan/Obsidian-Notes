#hashtables
### Introduction
- quick key to value lookup
	- like for phone book
- Insertion, deletion, and get take (on avg) constant time
### How it Works
- hash stores values in array
- hash function used to convert key into a code (hash code) which is then made into index in array
	- must return same hash function for equal keys
- often more hash codes than indices in array
- ![[Pasted image 20230517114424.png]]
#### Collisions
- often num of hash codes > size of array, some keys will be assigned to same index -> COLLISION
- most common approach: instead of storing just the value at that index, linked list must contain both entire key + value in pairs instead of just value
#### Undating keys in hash table
- once updated, lookup will no longer work for the key
- if need updates, remove it, update the key and then reinsert into the table

### Runtimes
- for interviews, assumed that hash table is well formed w few collisions 
- worst case tho = all ops take linear time, 
	- if poor distribution, all objects could hash to same index in array and any op would require going through all other entries
- ![[Pasted image 20230517114939.png]]

### Key Takeaways
- best performance for lookups, inserts, and deletions with all on avg taking O(1) time

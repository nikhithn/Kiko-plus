## Table of Algorithms
Partitioning and Incremental Scaling - Consistent Hashing
DynamoDB is a key-value store, so it is essentially a distributed, persistent hash table.  Key operations for a distributed hash-table include ensuring that failures and additions of new servers to the hash-table is not computationally expensive. 

Let's look at a naive hash algorithm.  Suppose you have a hash function that takes any input and converts it to an integer.  You can distribute the hash table over n servers by computing hash(input) % n.  The output is necessarily between 0 and n-1, and this can then map to the server and inform where to store the information.  Assuming that the distribution of the hash is uniform (at least over %n) you will have an equal distribution of data across each server.  If some servers can take more load than others, you can increase the range of hash % n that you assign to that server.  For example, if a server can take 2x as much load as the average, you can assign 2 integers to the server, and then take the hash % n+1 of the value.  Then the server will receive 2x as much load as others.

The naive algorithm provides the lookup and write performance and distribution that we need; however, it does not provide the incremental scalability that we need.  To see this, suppose we add a server to the distributed hash-table.  In this case, the 

# P* - Parallel A* (Aditya Kannan + Gabriel Lee)

### Summary
We are going to implement a parallel implementation of A* and analyze the performance of the algorithm on both systems. We plan to implement our algorithm on both GPU and multi-core CPU platforms, for which we will use CUDA and OpenMP respectively.

### Background
A* is a single-source shortest path search algorithm used widely in AI and Robotics for graph search problems. It finds the fastest path in a (un)weighted (un)directed graph between two nodes and can therefore be useful for graph search and motion planning. With the right heuristic, A* has been proved to be a complete and optimal search algorithm.

A* is a variant of Dijkstra's algorithm that involves using a heuristic to reduce the number of nodes searched by the algorithm. Heuristics are generally hand-selected and must satisfy some properties for optimality. On general graphs, heuristics must be consistent (i.e. two adjacent nodes and the goal node must satisfy the triangle inequality).

The key aspect of this problem is to find an algorithm that can add and expand candidate nodes in the priority queue in parallel. A large bottleneck in general graph search algorithms is that they have a large set of nodes on the search frontier that are waiting to be explored. Being able to schedule candidate nodes effiently would be important to this project.

### The Challenge
Implementating A* in parallel will rely on an efficient implementation of a Priority Queue. A*, like Dijkstra's algorithm, uses a priority queue to select the "best" next node to search. In this way, it reduces the number of nodes to search and makes the search process more efficient in general. 

Repeatedly adding and choosing the best element in a priority queue is generally implemented as a sequential task due to its dependencies. This is because when the child nodes of the best node is added to the priority queue, they could potentially change the values in or the order of the queue. We will need to find a way to allocate nodes to threads such that A*'s completeness and optimality properties still hold. These two aspects (dealing with dependencies and scheduling) are the two aspects that make this problem difficult.

### Resources
We will start by implementing a vanilla, serial implementation of A* and use that to compare with parallel versions of A*. We have found some approaches people have published previously to tackle this problem [1] and we hope to compare our implementation performance with theirs.

### Goals and Deliverables
Our 100% goal is to implement parallel A* with similar speedup as in [1] for some of the applications that they suggested. In particular, for the Protein Design problem, we would like to achieve around 35-45x speedup on a GPU. We would like to see similar speedup on multi-core CPU, but this will be a function of how many cores we have access to.

Our 125% goal is to apply this algorithm to new problems not mentioned in [1] and see its performance in those settings. Another thing we could try is to implement parallel versions of other algorithms. One other algorithm that is widely used in Robotics is Rapidly Exploring Random Trees (RRT). Others have developed approaches for parallel search with RRT as well [2].

Our 75% goal is to have complete working version of parallel A*, although it might not be up to similar performance as the paper in [1]. For this goal, we would be able to implement it in either GPU or multi-core CPU, but perhaps not both.

For demos, we could potentially visualize the A* search algorithm on various problems by showing the nodes that were expanded in the order that they were by different threads. We would be able to color code the nodes by the thread that expanded the node.

### Platform Choice
We will be using both GPU and multi-core CPU platforms for our project. We would like to use the Gates GHC machines as well as the PSC machines for larger runs on the cluster. These would be useful as we have used them in class for CUDA and OpenMP programming in class homeworks previously.

### Schedule


### References

[1] https://yichaozhou.com/publication/1501massive/

[2] https://content.iospress.com/articles/integrated-computer-aided-engineering/ica190616

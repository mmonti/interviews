**What’s the difference between DFS and BFS?**

DFS (Depth First Search) and BFS (Breadth First Search) are search algorithms used for graphs and trees. When you have an ordered tree or graph, like a BST, it’s quite easy to search the data structure to find the node that you want. But, when given an unordered tree or graph, the BFS and DFS search algorithms can come in handy to find what you’re looking for. The decision to choose one over the other should be based on the type of data that one is dealing with.

In a breadth first search, you start at the root node, and then scan each node in the first level starting from the leftmost node, moving towards the right. Then you continue scanning the second level (starting from the left) and the third level, and so on until you’ve scanned all the nodes, or until you find the actual node that you were searching for. In a BFS, when traversing one level, we need some way of knowing which nodes to traverse once we get to the next level. The way this is done is by storing the pointers to a level’s child nodes while searching that level. The pointers are stored in FIFO (First-In-First-Out) queue. This, in turn, means that BFS uses a large amount of memory because we have to store the pointers.

**An example of BFS**

Here’s an example of what a BFS would look like. The numbers represent the order in which the nodes are accessed in a BFS:

![Alt BFS](http://www.programmerinterview.com/images/BFS.png)

In a depth first search, you start at the root, and follow one of the branches of the tree as far as possible until either the node you are looking for is found or you hit a leaf node ( a node with no children). If you hit a leaf node, then you continue the search at the nearest ancestor with unexplored children.

**An example of DFS**

Here’s an example of what a DFS would look like. The numbers represent the order in which the nodes are accessed in a DFS:

![Alt DFS](http://www.programmerinterview.com/images/DFS.png)

**Differences between DFS and BFS**

Comparing BFS and DFS, the big advantage of DFS is that it has much lower memory requirements than BFS, because it’s not necessary to store all of the child pointers at each level. Depending on the data and what you are looking for, either DFS or BFS could be advantageous.

For example, given a family tree if one were looking for someone on the tree who’s still alive, then it would be safe to assume that person would be on the bottom of the tree. This means that a BFS would take a very long time to reach that last level. A DFS, however, would find the goal faster. But, if one were looking for a family member who died a very long time ago, then that person would be closer to the top of the tree. Then, a BFS would usually be faster than a DFS. So, the advantages of either vary depending on the data and what you’re looking for.

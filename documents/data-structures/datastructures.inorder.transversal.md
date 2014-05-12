**Suppose that you are given a binary tree like the one shown in the figure below. Write some code in Java that will do an inorder traversal for any binary tree and print out the nodes as they are encountered. So, for the binary tree in the figure below, the algorithm will print the nodes in this order: 2, 7, 5, 6, 11, 2, 5, 4, 9 – note that the very first “2″ that is printed out is the left child of 7, and NOT the “2″ in the root node
When trying to figure out what the algorithm for this problem should be, you should take a close look at the way the nodes are traversed. In an inorder traversal If a given node is the parent of some other node(s) then we traverse to the left child. If there is no left child, then go to the right child, and traverse the subtree of the right child until you encounter the leftmost node in that subtree. Then process that left child. And then you process the current parent node. And then, the traversal pattern is repeated.**

![Alt BT](http://www.programmerinterview.com/images/BInaryTree.png)

So, it looks like each sub-tree within the larger tree is being traversed in the same pattern – which should make you start thinking in terms of breaking this problem down into sub-trees. And anytime a problem is broken down into smaller problems that keep repeating, you should immediately start thinking in recursion to find the most efficient solution. So, let’s take a look at the 2 largest sub-trees and see if we can come up with an appropriate algorithm. You can see in the figure above that the sub-trees of 7 and 5 (child nodes of the root at 2) are the 2 largest subtrees.

```java
1.  Go the left subtree, and perform an inorder traversal
on that node.

2.  Print out the value of the current node.

3.  Go to the right child node, and then perform
an inorder traversal on that right child node's subtree.
```

This sounds simple enough. Let’s now start writing some actual code. But first, we must have a Node class that represents each individual node in the tree, and that Node class must also have some methods that would allow us to go to the left and right nodes, and also a method that would allow us to print a Node’s value. This is what it would look like in Java psuedocode:

```java
public class Node {

  private Node right;
  private Node left;
  private int nodeValue;

  public Node() {
    // a Java constructor
  }

  public Node leftNode() {return left;}
  public Node rightNode() {return right;}
  public int getNodeValue() {return nodeValue;}
}
```

Given the Node class above, let’s write a recursive method that will actually do the inorder traversal for us. In the code below, we also assume that we have a method called printNodeValue which will print out the Node’s value for us.

```java
void inOrder (Node root) {

  if (root == null) {
    return;
  }

  inOrder(root.leftNode());
  root.printNodeValue();
  inOrder(root.rightNode());
}
```

Because every node is “examined” once, the running time of this algorithm is O(n).

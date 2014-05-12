**Suppose that you are given a binary tree like the one shown in the figure below. Write some code in Java that will do a preorder traversal for any binary tree and print out the nodes as they are encountered. So, for the binary tree in the figure below, the algorithm will print the nodes in this order: 2, 7, 2, 6, 5, 11, 5, 9, 4**

![Alt BT](http://www.programmerinterview.com/images/BInaryTree.png)

When trying to figure out what the algorithm for this problem should be, you should take a close look at the way the nodes are traversed – a preorder traversal keeps traversing the left most part of the tree until a leaf node (which has no child nodes) is encountered, then it goes up the tree, goes to the right child node (if any), and then goes up the tree again, and then as far left as possible, and this keeps repeating until all of the nodes are traversed.

So, it looks like each sub-tree within the larger tree is being traversed in the same pattern – which should make you start thinking in terms of breaking this problem down into sub-trees. And anytime a problem is broken down into smaller problems that keep repeating, you should immediately start thinking in recursion to find the most efficient solution. So, let’s take a look at the 2 largest sub-trees and see if we can come up with an appropriate algorithm. You can see in the figure above that the sub-trees of 7 and 5 (child nodes of the root at 2) are the 2 largest subtrees.

Let’s start by making observations and see if we can convert those observations into an actual algorithm. First off, you can see that all of the nodes in the subtree rooted at 7 (including 7 itself) are printed out before the subtree rooted at 5. So, we can say that for any given node, the subtree of it’s left child is printed out before the subtree of it’s right child. This sounds like a legitimate algorithm, so we can say that when doing a preorder traversal, for any node we would print the node itself, then follow the left subtree, and after that follow the right subtree. Let’s write that out in steps:

```java
1.  Print out the root's value, regardless of whether you are
at the actual root or just the subtree's root.

2.  Go to the left child node, and then perform a pre-order
traversal on that left child node's subtree.

3.  Go to the right child node, and then perform a
pre-order traversal on that right child node's subtree.

4.  Do this recursively.
```

This sounds simple enough. Let’s now start writing some actual code. But first, we must have a Node class that represents each individual node in the tree, and that Node class must also have some methods that would allow us to go to the left and right nodes. This is what it would look like in Java psuedocode:

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

Given the Node class above, let’s write a recursive method that will actually do the preorder traversal for us. In the code below, we also assume that we have a method called printNodeValue which will print out the Node’s value for us.

```java
void preOrder (Node root) {
  if (root == null) {
    return;
  }

  root.printNodeValue();

  preOrder( root.leftNode() );
  preOrder( root.rightNode() );
}
```

Because every node is “examined” once, the running time of this algorithm is O(n).

**Suppose that you are given a binary tree like the one shown in the figure below. Write some code in Java that will do a postorder traversal for any binary tree and print out the nodes as they are encountered. So, for the binary tree in the figure below, the algorithm will print the nodes in this order: 2, 5, 11, 6, 7, 4, 9, 5, 2 – where the very last node visited is the root node**

When trying to figure out what the algorithm for this problem should be, you should take a close look at the way the nodes are traversed – there is a pattern in the way that the nodes are traversed.

If you break the problem down into subtrees you can see that these are the operations that are being performed recursively at each node:

```java
1.  Traverse the left subtree
2.  Traverse the right subtree
3.  Visit the root
```

This sounds simple enough. Let’s now start writing some actual code. But first, we must have a Node class that represents each individual node in the tree, and that Node class must also have some methods that would allow us to go to the left and right nodes. This is what it would look like in Java:

```java
public class Node {
  private Node right;
  private Node left;
  private int nodeValue;

  public Node(){
    // a Java constructor
  }

  public Node leftNode() {return left;}
  public Node rightNode() {return right;}
  public int getNodeValue() {return nodeValue;}
}
```

Given the Node class above, let’s write a recursive method that will actually do the postorder traversal for us. In the code below, we also assume that we have a method called printNodeValue which will print out the Node’s value for us.

```java
void postOrder(Node root) {

  if (root == null) {
    return;
  }

  postOrder( root.leftNode() );
  postOrder( root.rightNode() );
  root.printNodeValue();
}
```
Because every node is “examined” once, the running time of this algorithm is O(n).

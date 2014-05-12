**How would you write a function to delete a node in the middle of a singly linked list? Assume that the only thing you get access to in the function is the node that needs to be deleted. We also want to reconstruct the linked list so that all of the node pointers are in place even after the deletion.**

In order to solve a question like this you should draw out a sample linked list because it makes the problem so much easier to solve. With that in mind, here is a sample singly linked list:

```java
v->w->x->y->z
```

**Finding an algorithm to delete a node in the middle**

Suppose we want to delete the node ‘x’ from the middle of the linked list above. After node x is deleted, we want the linked list to look like this:

```java
v->w->y->z
```

How should we come up with an algorithm to do this for us? If we just delete node x then we still need some way for node “w” to point to node y, which means that we will have to somehow get access to the w node. And because it is a singly linked list, we have no way of getting to the ‘w’ node unless we have access to the head node so that we can traverse the list from the beginning. Since the problem does not state we do have access to the head node we will have to assume we don’t.
So, we clearly have to come up with some alternative solution. What if we ‘swap’ the data in node X (the node to be deleted) with node Y (the very next node)? This way node X essentially becomes node Y. Then, we just set the necessary pointers so that the linked list stays in the form that we want it, and delete the original ‘Y’ node. Here’s the algorithm to solve the problem:

```java
- First we change the data in node X (the node
 that needs to be deleted) so that it essentially
becomes node Y (the node right after it)

- Then we delete the original Y node

- And finally, we set our 'new' Y node to point
 to the Z node so that the list is back in correct
 order
```

**Implementation of a function in Java to delete a node in the middle of a linked list**

Let’s write a function in Java pseudocode that implements the algorithm above.

```java
public boolean deleteMiddleNode(Node middleNode)
{
//error check:
if  (middleNode  ==  null  ||  middleNode.next  ==  null)
return false;

/*
middleNode is x in our example data above, but
is now changed to hold the data of node y:
*/
middleNode.data = middleNode.next.data;

/*tempNode now holds node z if following
the example above:  */
Node tempNode = middleNode.next.next;
//delete the old node Y from example above
delete(middleNode.next);
/*reset pointer so that the new "y" points
  to z
*/
middleNode.next = tempNode;
}
```

And there we have our solution!

**Suppose that you are given a linked list that is either circular or or not circular (another word for not circular is acyclic). Take a look at the figures below if you are not sure what a circular linked list looks like.
Write a function that takes as an input a pointer to the head of a linked list and determines whether the list is circular or if the list has an ending node. If the linked list is circular then your function should return true, otherwise your function should return false if the linked list is not circular. You can not modify the linked list in any way.**

This is an acyclic (non-circular) linked list:

![Alt non-circular](http://www.programmerinterview.com/images/singly-linked-list.png)

This is a circular linked list:

![Alt circular](http://www.programmerinterview.com/images/circular-linked-list.png)

You should start out this problem by taking a close look at the pictures of a circular linked list and a singly linked list so that you can understand the difference between the 2 types of lists.

The difference between the 2 types of linked lists is at the very last node of the list. In the circular linked list, you can see that the very last node (37) links right back to the first node in the list – which makes it circular. However, in the acyclic or non-circular linked list you can see that the end node does not point to another node in the linked list and just ends.

It is easy enough to know when you are in an acyclic linked list – the pointer in the end node will just be pointing to NULL. However, knowing when you are in a circularly linked list is more difficult because there is no end node, so your function would wind up in an infinite loop if it just searches for an end node. So, there has to be a solution other than just looking for a node that points to NULL, since that clearly will not work.

Take a closer look at the end node (37) in the circular linked list. Note that it points to the head node (12), and that there must also be a head pointer that points to the head node. This means that 12 is the only node that has 2 pointers pointing to it. And, suppose 37 pointed to 99, then this would still be a circularly linked list, and 99 would be the only node that has 2 pointers pointing to it. So, clearly, in a circular linked list there will always be a node that has 2 pointers pointing to it. Now the question is whether we can use that property to somehow provide a solution to this problem – by traversing the list and checking every node to determine whether 2 nodes are pointing at it? If true, the list is circular. If not true, the list is acyclic and you will eventually run into a NULL pointer at the last element.

**Too difficult a solution to find if a linked list is cyclical**

This sounds like a good solution, but unfortunately it is difficult to find out how many pointers each element has pointing to it. So, before we even try to implement this solution, we should eliminate it since it will be very messy and difficult to implement.

Another way of looking at a circular linked list is to say that if you are traversing the list and you have visited the same node twice, then you know that the linked list is circular. So, another possible algorithm is this: if we have already encountered a node, then we know the linked list is circular, but if we encounter a NULL pointer then we know that the linked list is acyclic. But, the big question here is how do we determine whether or not we have already visited a node in an algorithm?

One way of doing this would be to mark each node after visiting it and then check to see if a node that you are visiting already has a mark. But, we can not modify the list in any way. Another option is to put all the nodes that we have already visited in a separate data structure, and then we would compare the current node to all of the nodes in that separate data structure. If we have a match, then we know that we are in a circular linked list. This would definitely work, but in the worst case-scenario (where the last node points to the head node) it would require as much memory as the linked list that you are given. Can we somehow minimize the memory requirement?

Well, why bother replicating the linked list we are given, when we can just use the linked list itself to compare to. All we have to do is compare the current node’s pointer to the previous nodes directly. So, for the nth node, we just compare its next pointer to see if it points to any nodes from 1 to n – 1. If any of those nodes are equal then we know that we have a circular linked list.

Let’s figure out what the Big-O is of our algorithm is (for a refresher on Big-O Notation read this:Big O Notation Explained). If we are at the first node, then we examine 0 nodes; if we are at the 2nd node then 1 node is examined, if we are at the 3rd node then 2 nodes are examined. This means that the algorithm examines 0 + 1 + 2 + 3 + …. + n nodes. The sum of 0 + 1 + 2 +…+ n is equal to (n2)/2 + n/2. And when calculating the Big-O of an algorithm we take off everything except the highest order term, so this means our algorithm is O(n2).

**Try using 2 pointers to find if linked list is cyclic**

Can we do better than this solution? Well, yes there is a better solution – although it is very difficult to have come up with unless you were given some sort of hint. Suppose we had 2 pointers instead of just one. Then what we could do is advance the pointers at different speeds.

What happens if we advance 2 pointers at different speeds – so that one pointer is traversing the list faster than the other pointer? So, we can have one slower pointer just going through every item in the linked list, and the other faster pointer traversing every other item in the linked list. In an acyclic (non-circular) list, the faster pointer will eventually hit a null pointer. But in a circular list, the faster pointer will eventually catch up to the slower pointer because the pointers are going in a circle. Take a few seconds and think about that to make sure it makes sense to you – just imagine 2 pointers going in a circle, one faster and one slower. The faster one will eventually catch up to the slower one if it’s moving at twice the speed. Or, imagine two runners on a small circular jogging track – the faster runner will eventually cross the slower jogger again, and be one lap ahead (assuming of course that they jog log enough for this to happen) of the slower jogger. So, this is another solution, and here is the pseudocode for this problem:

```java
2 pointers travelling at different speeds start from the
head of the linked list
Iterate through a loop
If the faster pointer reaches a NULL pointer then return
saying that the list is acyclic and not circular
If the faster pointer is ever equal to the slower pointer or the
faster pointer's next pointer is ever equal to the slower pointer
then return that the list is circular

Advance the slower pointer one node
Advance the faster pointer by 2 nodes
```

**Solution to finding if linked list is circular using tortoise and hare algorithm**

The algorithm that we gave the pseudocode for above is actually known as the tortoise and hare algorithm – where the faster pointer is considered the “hare” (which is a rabbit, for those of you who learned English as a second language), and the slower pointer is considered the tortoise.

If we write the actual code for this, it would look like this:

```java
bool findCircular(Node *head)
{
   Node *slower, * faster;
   slower = head;
   faster = head->next; //start faster one node ahead
   while(true) {

     // if the faster pointer encounters a NULL element
     if( !faster || !faster->next)
       return false;
    //if faster pointer ever equals slower or faster's next
    //pointer is ever equal to slow then it's a circular list
     else if (faster == slower || faster->next == slower)
        return true;
     else{
       // advance the pointers
        slower = slower->next;
        faster = faster->next->next;
      }
   }
}
```

**The Big O of solution to find if linked list is circular**

And there is our solution. What is the Big-O of our solution? Well, what’s the worst case if we know that the list is circular? In this case, the slower pointer will never go around any loop more than once – so it will examine a maximum of n nodes. The faster pointer, however, will traverse through 2n nodes and examine half of those nodes (n nodes). The faster pointer will pass the slower pointer regardless of the size of the circle – which makes it a worse case of n +n, which equals 2n nodes. This is O(n).

**The Big O of the worst case when list is acyclic**

And what about the worst case when the list is not circular – acyclic? Then the faster pointer will have come to the end after traversing through n nodes and examining n/2 nodes since the faster pointer skips every other node. The slower pointer will have examined n/2 nodes, which means that combined the faster and slower pointer will have examined n/2 + n/2 nodes, which is also O(n). Thus, the algorithm is O(n) for both worst case scenarios.

**How would you find the nth to last element in a linked list?**

If this question were asked for a doubly linked list, it would be very easy to solve because you would simply go the end of the list and then go backwards “N” number of times by following the links to the previous nodes. Because of that fact, this question is almost always asked for singly linked lists – and if you are in an interview situation you should always ask your interviewer to clarify whether he/she means a singly or doubly linked list.

**Clarify all of the possible assumptions**

Another assumption in this problem is that you do NOT know how long the linked list is – because if you did, then you could simply go through the list “length – N” times to get to the Nth node, which will be the answer you want. That’s too easy. Also, you can safely assume that any linked list passed into your solution has at least N nodes, otherwise there would be no point in even trying to solve the problem.

**Using a singly linked list**

Now that we know we are going to use a singly linked list, we can see that there is a bit of a challenge to this problem. While problems with linked lists can almost always be solved with recursion, let’s first try to solve this problem using iteration and then later with recursion.

**Find nth to last node in a linked list using iteration**

Using iteration, there really is no way we can we can find the nth to last node just by simply using the linked list’s pointers and nothing else. Because we don’t know how long the linked list is, and if we iterate and get to the end of the linked list, then we really have no “extra” information that would allow us to find the nth to last node. So, it should be clear that we need some sort of extra programming construct that will allow us to store some information such that we can then the right answer.

One possibility is to create a separate doubly linked list that will always be just “N” nodes long. So, as we iterate through the linked list, we will construct another linked list that is N nodes long with the nodes we just passed through. And, once the separate linked list reaches a size of N, we keep replacing the top node with the most recently traversed node in our singly linked list. This way, we have a separate data structure with all of the last N nodes. And, once we reach the end of the singly linked list, we know that we can then find the very first entry in our separate doubly linked list and that will give us our answer!
The solution we explained above is quite memory and time intensive. Can we come up with something better? What if we just pointers instead? What can we do with pointers that would allow us to find the Nth to last node? It turns out that we can! What if we just use 2 pointers – call them pntr1 and pntr2. Let’s say that we advance pntr2 by N-1 nodes. After that, every time we iterate through the linked list, both pntr1 and pntr2 will be advanced to point to the very next node in the linked list. This means that there will always be a distance of exactly n-1 nodes between pntr1 and pntr2. So, when pntr2 is equal to null, this means that pntr2 has reached the very end of the list. And, most importantly, it means that pntr1 will be pointing at the nth to last node! So, we will have our answer!

**Algorithm to find the nth to last element in a linked list**

```java
- pntr1 and pntr2 start out by both pointing to the
   head node
- pntr2 is then advanced n-1 nodes.  pntr1 is still
   pointing to the head.  After this, we keep advancing
   pntr2 by one node and pntr 1 is also advanced by one
   node
- Once pntr2 is equal to null we know we  have reached
   the last node and pntr1 now points to the nth to last
   node, and we can return our answer as the node that
   pntr1 is pointing to.
```

And, here is what the actual code for the algorithm above will look like:

**Solution to finding the nth to last element in a linked list using iteration**

```java
Node  FindnthToLast(Node  head,  int  n)  {

if (n <1 || head == null)
  return null;

Node pntr1, pntr2 = head;

//advance pntr2 by n-1 nodes;
for  (int  i  =  0;  i  <  n  - 1;  ++i)  {

if  (pntr2  ==  null)  {
  /*this is an error condition to check to see if
     the linked list is less than n nodes long, in which
     case we just return null indicating an error
  */
  return null;
  }

else //go to the next node
   pntr2 = pntr2.nextNode;

}

/*Now, keep going until you hit a null node,
  and then you've reached the end, and
  pntr1 will be pointing to the nth from
 last node
*/

while(pntr2.nextNode != null)
{
  pntr1 = pntr1.nextNode;
  pntr2 = pntr2.nextNode;
}

return pntr1;

}
```

Clearly, this solution is a lot cleaner and far less memory intensive than our first solution. Now, let's move on to finding a solution for this problem using recursion.

**Find nth to last node in a linked list using recursion**

Now the question is how can we use recursion to solve this problem? The first thing we should ask ourselves since we want to create a recursive function is what will be our base case? Well, It should be clear from the iterative solution that we will have to go the end of the linked list in order to find the nth to last node, because we do not know the length of the singly linked list. So, we will know that we have come to the end of the linked list if the next node is null, which means that we should stop the recursion.

Now that we have a base case for the recursion, what about actually solving the problem - how do we find the nth to last node in the linked list? One thing we know about recursion is that it uses a call stack to store all recursive calls so that the program knows exactly at what point to return to when one recursive call ends. Each function call has its very own stack frame, which is basically stores the local function variables for that particular function call. You should read this article on recursion if you need a refresher on call stacks and stack frames: Recursion tutorial

Okay, that's great, you're thinking - but how does that information actually help us to solve this problem recursively? Well, think about it - using recursion we can get to the very end of the linked list right? But, because recursion essentially 'saves' each function call's information on the call stack, we can also just go the end of the list and then go back 'n' times down the recursive call stack. Of course, we will need to keep a count of how many times we 'pop' a stack frame after we have reached the end of the linked list. Once we have done it 'n' times, then we know that we have come to our nth to last node, for which we can print out the information we want.

Clearly we need to keep count of the number of times we have returned to a recursive call after we reach the end node in the linked list. And once that count reaches 'n' then we stop and print that node as our answer. But, how should we keep count? If we use a local variable, then it will lose it's value as soon as another recursive function call is made - because local variables by definition stay local to the function itself.

**Finding an alternative to local variables**

We need a variable that will hold it's value across multiple recursive function calls. Any ideas? What about using a static variable? That's actually perfect - because a static variable by definition will hold it's value across many different function calls, because static variables are not stored in the same area of memory as local variables. With that in mind, we will use a static variable to keep count of how many recursive calls have returned, and once it equals 'n' we will know that we are at the correct node element in the list - the nth to last.

Let's write a function to find the nth to last node in C. Here is what it will look like:

**Find nth to last element in a linked list recursion solution**

```java
void findNthFromLast(struct Node* headNode, int n)
{
   /*this has to be static so that it holds it's value from
     call to call because of the fact that a non-static variable
     will not hold it's value since the variable will just be local
     to the function if it's not static and will not be preserved
     across call stack:  */

    static int i = 0;
    //base case when we reach the end of linked list:
    if(headNode == NULL)
       return;
    //this is where head pointer is advanced (head->next)...
    findNthFromLast(headNode->next, n);
    //increment i and check to see if equals n
   //if it does equal n then print out the element's data
    if(++i == n)
       printf("%d", headNode->elementData);
}
```

**Understanding the recursive solution to find nth to last element in a linked list**

If you are having trouble understanding the recursive function above, then you should pay very close attention to the order in which things are done in the function - because that is very important. First off, the function will keep calling itself (which is recursion) until it reaches a node whose next pointer is NULL - which is the very last node in the linked list - and only then will it return. It will return to the line right after the call to findNthFromLast (in the most recent stack frame in the call stack), which checks to see if the integer i is equal to "n". The very first time it returns it will return to the 1st to last node, then the 2nd and so on and so forth. Once it returns to the "nth" from last node it will print out that node's contents and we will have our answer! It's a pretty cool answer to the problem, and shows the power of recursion.

**What are the differences between a hash table and a binary search tree? Suppose that you are trying to figure out which of those data structures to use when designing the address book for a cell phone that has limited memory. Which data structure would you use?
A hash table can insert and retrieve elements in O(1) (for a big-O refresher read here). A binary search tree can insert and retrieve elements in O(log(n)), which is quite a bit slower than the hash table which can do it in O(1).**

**A hash table is an unordered data structure**

When designing a cell phone, you want to keep as much data as possible available for data storage. A hash table is an unordered data structure – which means that it does not keep its elements in any particular order. So, if you use a hash table for a cell phone address book, then you would need additional memory to sort the values because you would definitely need to display the values in alphabetical order – it is an address book after all. So, by using a hash table you have to set aside memory to sort elements that would have otherwise be used as storage space.

**A binary search tree is a sorted data structure**

Because a binary search tree is already sorted, there will be no need to waste memory or processing time sorting records in a cell phone. As we mentioned earlier, doing a lookup or an insert on a binary tree is slower than doing it with a hash table, but a cell phone address book will almost never have more than 5,000 entries. With such a small number of entries, a binary search tree’s O(log(n)) will definitely be fast enough. So, given all that information, a binary search tree is the data structure that you should use in this scenario, since it is a better choice than a hash table.

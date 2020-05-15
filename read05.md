# Read 05, Linked Lists
> Linked list is a data structure that contains nodes that links/points to the next node in the list.

* linked lists are linear data structures.
* The biggest differentiator between arrays and linked lists is the way that they use memory in our machines. In a linked list the memory, can be scattered separely; contrary to an array, where all the data is allocaded in the same area.
* The fundamental difference between arrays and linked lists is that arrays are static data structures, while linked lists are dynamic data structures.
  * A **static data structure** needs all of its resources to be allocated when the structure is created. Always needs a given size and amount of memory.
  * A **dynamic data structure** can shrink and grow in memory. It doesn’t need a set amount of memory to be allocated in order to exist, and its size and shape can change, and the amount of memory it needs can change as well.
* Nodes are the individual items/links that live in a linked list. Each node contains the data for each link.
* A Head node is a reference type of type Node to the first node in a linked list.
* Linked List is a sequence of **Nodes**, which are connected to each other, but only to one next node, and in some cases, can have the relation of a node that refers to the node itself.


> A node only knows about what data it contains, and who its neighbor is.


### Types of Linked List:
  1. Singly:
      * Refers to the number of references the node has. 
      * A Singly linked list means that there is only one reference, and the reference points to the Next node in a linked list.
      * Starts at the head node.
      * The last node, which will end at an empty null value.
  1. Doubly
    * Refers to there being two (double) references within the node:
      * To the Next node,
      * To the Previous node.

> A linked list is usually efficient when it comes to adding and removing most elements, but can be very slow to search and find a single element.

### The next property
* We depend on the Next value in each node to guide us where the next reference is pointing. 
* The Next property is exceptionally important because it will lead us where the next node is and allow us to extract the data appropriately.

_Example for traversing a linked list_

```
Current <-- Head
			WHILE Current is not NULL
				IF Current.Value is equal to value
					return TRUE

				Current <-- Current.Next

			return FALSE
```

### Big O

The Big O of time for Includes would be O(n). This is because, at its worse case, the node we are looking for will be the very last node in the linked list. n represents the number of nodes in the linked list.

The Big O of space for Includes would be O(1). This is because there is no additional space being used than what is already given to us with the linked list input.

### Adding a node with an O(1) efficiency: On the head
  1. Set Current equal to Head. This will guarantee us that we are starting from the very beginning.
  1. We can then instantiate the new node that we are adding

```
ALGORITHM Add(newNode)
		// INPUT <-- Node to add 
		// OUTPUT<-- No output

			Current <-- Head
			newNode.Next <-- Head
			Head <-- newNode
			Current <-- Head
```
### Adding a Node O(n). Any position

```
ALGORITHM AddBefore(newNode, existingNode)
		// INPUT <-- New Node, Existing Node
		// OUTPUT <-- No Output

			Current <-- Head

			while Current.Next is not equal to NULL
				if Current.Next.Value is equal to existingNode.Value
					newNode.Next <-- existingNode
					Current.Next <-- newNode

				Current <-- Current.Next;
```

_Big O in this escenario_

The time efficiency of this transaction would be O(n) because we could be inserting the new node, worst case scenario, at the end. With n being the number of nodes possible, we would therefore have O(n) time efficiency.

Space efficiency would stay at an O(1) because, like before, no additional space is being used allocated outside of what is given to us on the input
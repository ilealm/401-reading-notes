[ HOME ](README.md)
# Read 10 - Stacks and Queues

> A stack is a data structure that consists of Nodes. Each Node references the next Node in the stack, but does not reference its previous.

* **_Push_** - Nodes or items that are put into the stack are pushed.
  * **Push O(1)**: Pushing a Node onto a stack will always be an O(1) operation. This is because it takes the same amount of time no matter how many Nodes (n) you have in the stack.
* **_Pop_** - Nodes or items that are removed from the stack are popped. When you attempt to pop an empty stack an exception will be raised.
  * **Pop O(1)**: Popping a Node off a stack is the action of removing a Node from the top.
* **_Top_** - This is the top of the stack.
* **_Peek_** - When you peek you will view the value of the top Node in the stack. When you attempt to peek an empty stack an exception will be raised.
  * **Peek O(1)**: When conducting a peek, you will only be inspecting the top Node of the stack.
* **_IsEmpty_** - returns true when stack is empty otherwise returns false.
  * *IsEmpty O(1)*:

### Stacks follow these Concepts:

* FILO - First In Last Out
* LIFO - Last In First Out

### Stacks Visualization
![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/stack1.PNG)


## Queue
* **Enqueue** 
  - Enqueue O(1)
  - Nodes or items that are added to the queue.  
* **Dequeue** 
  - O(1)
  - Nodes or items that are removed from the queue. If called when the queue is empty an exception will be raised.
* **Front** - This is the front/first Node of the queue.
* **Rear** - This is the rear/last Node of the queue.
* **Peek** 
  - O(1)
  - When you peek you will view the value of the **_front Node _**in the queue. 
  - If called when the queue is empty an exception will be raised.
* **IsEmpty** 
  - O(1)
  - Returns true when queue is empty otherwise returns false.



### Queues follow these concepts:
* FIFO : First In First Out
* LILO : Last In Last Out

### Queues Visualization
![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/Queue.PNG)


#### Source
[Source](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/stacks_and_queues.html)
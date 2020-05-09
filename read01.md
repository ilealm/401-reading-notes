# Big O notation

Is a way to evaluate how efficient something is. Is a way to evaluate how well something perform: how much time and memory needs. The ideal is to get constant time, which means that no matter how the input groes, always will be the same amount of time or space, 

Is a way to calculate the time and recourses that some execution will need to have or take to complete. This method can be change so the input can be bigger, and in this case, calculate the time or resources a load execution will take.


### O(1)
O(1) describes an algorithm that will always execute in the same time (or space) regardless of the size of the input data set.

### O(N)
O(N) describes an algorithm whose performance will grow linearly and in direct proportion to the size of the input data set. 

### O(N2)
O(N2) represents an algorithm whose performance is directly proportional to the square of the size of the input data set. This is common with algorithms that involve nested iterations over the data set.

### O(2N)
O(2N) denotes an algorithm whose growth doubles with each additon to the input data set. 


## Logarithms, binary search.
Is a sorting methodology where the search starts at the middle of all the elements, when the element is compared to the middle element, and for example, if I less than the middle, then the comparation continues to the left (less value), and then the comparation continues with the element to le left, and so on. If the value to compare is grater than the element, then it will be compared to the right, and a new comparation continues until the element finds it correct place. Is like a underground root, where the searching value moves to find this correct place

## Moving with Link list: 
- Current position in list only knows next position on list, and last position points to null as next position. 
- Current position in list knows previous and next position on list. 
- Current position in list only knows next position on list, and last position points to first position, making a "circle" shape. 

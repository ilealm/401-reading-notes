[ HOME ](README.md)
Read 35 - Graphs

> A graph is a non-linear data structure that can be looked at as a collection of vertices (or nodes) potentially connected by line segments named edges.

### Terminology

- **Vertex** 
  - A vertex, also called a “node”, is a data object that can have zero or more adjacent vertices.
- **Edge** 
  - An edge is a connection between two nodes.
- **Neighbor** 
  - The neighbors of a node are its adjacent nodes, i.e., are connected via an edge.
- **Degree** 
  - The degree of a vertex is the number of edges connected to that vertex.

  ### Undirected Graph

  > An Undirected Graph is a graph where each edge is undirected or bi-directional. This means that the undirected graph does not move in any direction.

![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/UndirectedGraph.PNG)

  ### Directed Graphs (Digraph)

  > A graph where every edge is directed.

  - Each node is directed at another node with a specific requirement of what node should be referenced next.
  - 

  ![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/DirectedGraph.PNG)


## Complete Graphs
> A complete graph is when all nodes are connected to all other nodes.

![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/CompleteGraph.PNG)

## Connected
> A connected graph is graph that has all of vertices/nodes have at least one edge.

![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/ConnectedGraph.PNG)

## Disconnected
> A disconnected graph is a graph where some vertices may not have edges.

![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/DisconnectedGraph.PNG)

## Acyclic Graph
> An acyclic graph is a directed graph without cycles. This means node can't be traversed through and potentially end up back at itself.

- A directed acyclic graph is also called a DAG. This can also be represented as what we know as a **tree**.

![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/threeAcyclic.png)

## Cyclic Graphs

> A cycle is defined as a path of a positive length that starts and ends at the same vertex.

- A Cyclic graph is a graph that has cycles.

![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/cyclic.PNG)

# Graph Representation

- We represent graphs through:

1. Adjacency Matrix
1. Adjacency List

## Adjacency Matrix
> An Adjacency matrix is represented through a 2-dimensional array. 
- If there are n vertices, then we are looking at an n x n Boolean matrix
- Each Row and column represents each vertex of the data structure. 
- The elements of both the column and the row must add up to 1 if there is an edge that connects the two, or zero if there isn’t a connection.
- A **sparse** graph is when there are very few connections. 
- A **dense** graph is when there are many connections
- **Within an adjacency matrix, an undirected graph will always be symmetric**. This is not the case for a directed graph.

![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/AdjMatrix.PNG)

## Adjacency List

> An adjacency list is a collection of linked lists or array that lists all of the other vertices that are connected.

- An adjacency list is the most common way to represent graphs. 
- Adjacency lists make it easy to view if one vertices connects to another.

![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/AdjList.PNG)

## Weighted Graphs
 > A graph with numbers assigned to its edges.
 
![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/weightGraph.PNG)

- When representing a weighted graph in a matrix, you set the element in the 2D array to represent the actual weight between the two paths. If there is not a connection between the two vertices, you can put a 0, although it is known for some people to put the infinity sign instead.

![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/weightMatrix.PNG)

- Within adjacency lists, you must include both the weight and the name of the adjacent vertex.

![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/weightList.PNG)

## Traversals

### Breadth First

In a breadth first traversal, you are starting at a specific vertex/node. This node must be specified when calling the BreadthFirst() method. The breadth-first traversal of a graph is like that of a tree, with the exception that graphs can have cycles. When a graph has cycles and we are trying to traverse, this leaves the possibility to be in an infinite loop….this is bad. To prevent such behavior, we need to have some sort of flag that specifies if we have already visited that vertices. Upon each visit, we just set the “visited” flag from false to true.

A few things to note about breadth-first traversals:

If there are any disconnected nodes (such as islands) with the graph data structure, they will not be traversed.
Breadth-first only outputs the nodes that are connected in some relation to the root that you pass in.

![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/BreadthFirst.PNG)

### Depth First

![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/Depth1.PNG)

### Source
[Source](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/graphs.html)
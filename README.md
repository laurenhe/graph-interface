## Intro
This is an implementation of a graph interface using an adjacency list representation. It is designed to represent various graph types (e.g., directed/undirected, weighted/unweighted, connected/disconnected, cyclic/acyclic, etc). This graph data structure uses an interface to decouple the abstraction from the implementation. An adjacency list class is used to implement the graph interface but an adjacency matrix could very well also be used. 

## Graph Representation
The ```AdjacencyList``` class has two attributes: an ```adj``` map to store the adjacency list and an ```isDirected``` boolean to indicate whether the adjacency list represents a directed or undirected graph. The map has ```Vertex``` objects as keys and a list of ```Edge``` objects as values. The list is implemented through a linked list. ```adj``` is declared as a hashmap in the constructor of the class. The constructor takes a boolean parameter to set the graph to be either directed or undirected. 

The ```AdjacencyList``` class consists of various methods used to perform basic graph operations, the most important of which being the ```addEdge()``` method. The ```addEdge()``` method is used to build the edges between source and destination vertices. Source and destination vertices are added to ```adj``` as keys. A new ```Edge``` object with the corresponding destination vertex is added to the value list of the source vertex. For undirected graphs, the source vertex is also added to the value list of the destination vertex. 
The ```Vertex```, ```Edge```, and ```AdjacencyList``` classes are defined with generic type. Type parameters allow for code reusability when working with different inputs. Type ```V``` is defined as a part of the ```Vertex``` class declaration. The ```Edge``` class is composed of the ```Vertex``` class and has a type parameter ```V, E```. The ```AdjacencyList``` class is composed of both the ```Vertex``` and ```Edge``` class and has type ```V, E```. 

The ```Vertex``` class has several attributes to aid in performing the graph traversal methods as well as other graph algorithms. The predecessor or parent of a vertex in a graph is set when performing BFS and Prim’s. The ```distFromSource``` attribute is set relative to the source vertex used in BFS and is initialized to be infinity. Given any source vertex, this value will reflect the shortest distance from a source vertex to the target vertex in an unweighted graph. The ```discoveredTimestamp``` and ```finishedTimestamp``` attributes mark when DFS starts and stops exploring from a vertex, respectively. The attribute ```minWeight``` is used for Prim’s and is initialized to infinity. 

The ```Edge``` class implements ```Comparable``` to enable sorting of weighted edges. Since edges depend on vertices, the source (u) vertex and destination (v) vertex are saved as attributes of an ```Edge``` object. The ```compareTo()``` method first checks if the weights of two edges are the same. If the weights are the same, it checks if the source vertices are the same using the ```toString()``` method of the ```Vertex``` class. Finally, it checks if the destination vertices are the same given equivalent source vertices.

## Graph Algorithms
The ```GraphAlgorithms``` class makes use of static methods and is dependent on the ```AdjacencyList```, ```Vertex```, and ```Edge``` classes. The methods in this class draw heavily from the pseudocode presented in CLRS. Starting with the search procedures, BFS computes the shortest-path distances from a given source vertex to any reachable vertex in the graph. The shortest-path distance is the minimum number of edges in any path. The ```predecessorSubgraph()``` method produces a breadth-first tree by printing out the vertices on the path from vertex s to vertex v. Since this method relies on the predecessor attribute being defined, BFS needs to be run first. The procedure for DFS uses a global time variable for timestamping discovery and finishing times. A depth-first tree can be traced using the timestamps printed out by the ```startFinishTimesDFS()``` method. Doing this by hand for simple examples and comparing afterwards to the program output makes for a captivating exercise!

For Kruskal's algorithm, the ```DisjointSet``` class was added to carry out union-find and ensure safe edges are added to the growing MST and no cycles are formed. It uses the ```p``` map for path compression and the ```rank``` map for efficient merging of connected components. Prim’s algorithm uses the ```minWeight``` and ```predecessor``` attributes of the destination vertex of the edge being considered. A priority queue is used to sort all the vertices in the graph except for the start vertex based on their ```minWeight``` in ascending order. Initially, all vertices have infinite ```minWeight```. The weight of a vertex is reassigned as it is visited from vertices that are dequeued under the condition that the weight of the connecting edge is less than the weight of the vertex. Once the queue is empty, all vertices should take on the minimum possible weight. Least-weight edges can then be extracted based on the ```minWeight``` values of the vertices.        

## How-to Guide
To use the graph data structure, create a graph object of the class ```AdjacencyList``` that implements the ```Graph``` interface in the ```Main``` class. Construct either a directed or undirected graph by passing in a boolean value to the constructor. Passing in true gives a directed graph while passing in false gives an undirected graph. After the graph is constructed, generate new ```Vertex``` objects with your type of choice. Once vertices are created, the ```addEdge()``` method can be used to add corresponding edges to your graph by passing in a source and destination vertex for each method call.

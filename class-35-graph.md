# Graph Data Stucture
A graph data structure is a collection of nodes that have data and are connected to other nodes.

Let's try to understand this through an example. On facebook, everything is a node. That includes User, Photo, Album, Event, Group, Page, Comment, Story, Video, Link, Note...anything that has data is a node.

Every relationship is an edge from one node to another. Whether you post a photo, join a group, like a page, etc., a new edge is created for that relationship.

In computer science, there are several common ways to represent a graph data structure. The choice of representation depends on the specific requirements and operations you need to perform on the graph. Here are some of the most widely used graph representations:

1. Adjacency Matrix:
   An adjacency matrix is a 2D array (or matrix) where the cell at row `i` and column `j` represents the presence of an edge between vertex `i` and vertex `j`. It uses 1s to denote the existence of an edge and 0s to denote no edge.

   Pros:
   - Simple representation for dense graphs.
   - Efficient for checking the presence of an edge.

   Cons:
   - Space-consuming for sparse graphs.
   - Inefficient for adding or removing vertices.

2. Adjacency List:
   An adjacency list is a collection of lists or arrays where each vertex has a list of its adjacent vertices. It can be implemented using an array of lists, a hash table, or a dictionary.

   Pros:
   - Compact representation for sparse graphs.
   - Efficient for adding or removing vertices.

   Cons:
   - Slower for checking the presence of an edge compared to the adjacency matrix.

3. Edge List:
   An edge list is a simple list of edges, where each edge is represented as a pair (u, v) denoting an edge between vertex `u` and vertex `v`.

   Pros:
   - Compact representation for sparse graphs.
   - Easy to implement and understand.

   Cons:
   - Slower for certain graph operations (e.g., checking the presence of an edge).

4. Incidence Matrix:
   An incidence matrix is a 2D array where the rows represent vertices, the columns represent edges, and the cells indicate the incidence of each vertex with each edge.

   Pros:
   - Suitable for certain graph algorithms and operations.

   Cons:
   - Space-consuming for large graphs.
   - Generally less intuitive compared to adjacency matrix or list.


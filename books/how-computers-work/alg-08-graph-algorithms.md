A graph is a data structure that can represent a wide range of problems. Networks of computers, people and devices can be represented using a graph. According to cormen there are two possible or standard ways of representing a graph $G = (V,E)$: as a collection of adjacency lists or as an adjacency matrix. An *adjacency matrix* with *n* vertices represents the graph as an *n x n* matrix where the $(i,j) = 1$ if there is an edge between the two vertices $i,j$ . 

An alternative representation is the *adjecency list* which have one linked list per vertex. If the graph is undirected each edge appears twice otherwise for undirected it appears "exactly once" (p 89.) Which representation is better depends on the relationship between |V| the number of vertices and |E| the number of edges. We call the graph dense when the number of edges is close to the upper limit, otherwise it's *sparse*. The adjency list is typically prefered when the graph is sparse whitle the adjecency matrix is greater for more dense graphs and also because it can access any edge in constant time. The drawback is that it takes up *O(n<sup>2</sup>)* space, "which is wasteful, if the graph does not have very many edges" (p. 88) 

**Searching through items in a graph**
In this section we will explore the perhaps most fundamental algorithms on graphs, those that look for specific items or traverse a graph which is very useful. The most fundamental ones are the *depth-first-search* and *breadth-first-search*. Exploring a graph can be compared to exploring a labyrinth. For example the graph below to the left is represented in the classic way with vertices and edges and to the right as a labyrinth where whenever there is an edge there is also a path. 
![](exploring%20a%20graph%20dfs.png)
Figure 1.1 Graph representation

The **breadth-first search** algorithm explores the graph layer by layer starting from some specific vertex which we might call the *start* or *source* vertex. From that vertex we systematically explore edges to visit first all neighbors of some vertex $s$, then all neighbors of those neighbors and so. It never revisits a vertex and we can think of it as ripples spreading out from a stone dropped in water. We can consider the graph as a tree and the breadth first search then explores all the nodes at each layer before going to the next. So it starts at the top node, goes to it's neighbors 2 and 3 and then it explores any potential neighbors of 2 and 3. In the sketch below we use the colors white, gray and black to keep track of progress where all vertices start out white. 

![[Sketches/BFS sketch|center]]
Figure 1.2 sketch of the breadth first search

There are other ways of showcasing the breadth first search algorithm. For example figure 20.3 in Cormen et al have the following depiction. 
![](breadth%20first%20search.png)

This algorithm can help find the shortest path calculated as the smallest number of edges needed to pass from one vertex to the other.  What remains now is an implementation in python or some other programming language. I've implemented a *queue* based solution here which tracks both the nodes visited but also the distance from the root node. The queue based method here has a running time of $O(V+E)$ because we visit each vertex once and examine each edge once — regardless of how connected the graph is.

Code example 1.1 breadth-first-search
```
from collections import deque  

def breadth_first_search(graph, source):  
   # initializing the data structure to keep track of which nodes has been visited.  
   visited = {key: False for key in graph.keys()}  
   distance = {key: None for key in graph.keys()}  
   # using a queue to manage the nodes that needs to be visited  
   queue = deque()  
   # start from the root node in a tree or the starting point in a graph  
   queue.append(source)  
   # keep traversing until queue is empty  
   distance[source] = 0  
   
   while queue:  
       # first-in first-out principle  
       vertex = queue.popleft()  
       
       if not visited[vertex]:  
           visited[vertex] = True  
           for neighbor in graph[vertex]:  
               if not visited[neighbor]:  
                   distance[neighbor] = distance[vertex] + 1  
                   queue.append(neighbor)  
                   
                   
   return visited, distance
```

**Depth-first-search** on the other hand explores from some point in the graph to all the reachable points from that original. This algorithm goes deep before going wide and uses a stack for recursion. In the sketch in figure 1.2 you might imagine how you would explore from the root node all the way to the leaf node before moving on to the next neighbor. It can be implemented using recursion or iteration. The recursive solution can work for smaller graphs and the iterative for larger graphs where stack overflow can be a problem. We can solve this implementation in two parts, first a main function that initializes what we need such as visited and variables to calculate and manage distances. It then starts looping over each vertex in the graph, represented as a adjacency list and calls the *helper* function for those vertices not visited. The helper function progresses the timer and sets the distance for that node equal to time, before adding it to the set of vertices which has been visited. Then we loop for all neighbors to the vertex and this is done recursively. This is where this algorithm differs from the one we saw previously. 

Code example 1.2 depth-first-search first part
```  
def depth_first_search(graph):  
    visited = set()  
    d,f,time = {}, {}, [0]  
    for vertex in graph:  
        if vertex not in visited:  
            depth_first_search_visit(graph, vertex, visited, d, f, time)  
    return d, f
```

Code example 1.3 depth-first-search second part
```
def depth_first_search_visit(graph, start, visited, d,f,time):  
    time[0] += 1  
    d[start] = time[0]  
    visited.add(start)  
    for neighbor in graph[start]:  
        if neighbor not in visited:  
            depth_first_search_visit(graph, neighbor, visited, d, f, time)  
    time[0] += 1  
    f[start] = time[0]
```

**BFS vs DFS — when to use which**
Both algorithms run in $O(V+E)$ and visit every reachable vertex, but they explore in fundamentally different orders and are suited to different problems.

| | BFS | DFS |
|---|---|---|
| Data structure | Queue (FIFO) | Stack / recursion (LIFO) |
| Explores | Wide first, layer by layer | Deep first, one path at a time |
| Finds shortest path? | Yes — in unweighted graphs | No |
| Memory usage | Higher — stores entire frontier | Lower — stores one path at a time |
| Natural use cases | Shortest path, social networks, web crawlers, GPS | Topological sort, cycle detection, dependency resolution |

The key intuition is this: if you care about **distance or proximity** from a source, use BFS. If you care about **ordering, reachability, or structure**, use DFS. For example, finding the shortest route between two cities is a BFS problem. Determining a valid order to take university courses given prerequisites is a DFS problem (topological sort).

**Topological sort**
Speaking of *topological sort*, it is a DAG $G = (V,E)$ a linear ordering of all it's vertices such that if $G$ contains an edge $(u,v)$ then $u$ appears before $v$ in the ordering. Topological sorting is defined only on directed graphs that are acyclic because when a graph contains a cycle we cannot make a linear ordering. A DAG is often used to represent some logical order of events socks before shoes while some can be put in any order like socks and pants. A topological sort of getting dressed can therefore be represnted by a graph. The same goes for things like dimensions before facts, love before everything else and so on. From figure 20.7 in Cormen et al we see the topological sort of getting dressed. Each directed edge means that garment $u$ must be put on before garment $v$. 
![](Topological%20sort.png)
Topological sort is a modification of depth first search

![[Sketches/Topological sort|center]]

**Djiksta's algorithm for finding fastest routes**
The Djiksta's algortihm is one that is known for finding the shortest path in weighted graphs in the case when all the weights of all the edges are non-negative. There are many practical applications for this type of algorithm. For example whenever someone is surfing the web or send emails, there is a lot of work going on behind the scenes, transfering the bits that make up whatever you send or retrieve over the internet. 

![[weighted undirected graph|center]]
Figure 1.1 Weighted undirected graph

A graph like that of figure 1.1 shows which paths are the shortest from the start node to every other vertex. This is what we are trying to determine with Djikstra's algorithm. 

Starting from the start node, we set it's distance to 0. Then we explore all it's neighbors starting with the one with the smallest weight. In this case we compare the sum of the distance with the initial distance and overwrite if it's it is smaller. Djikstra used something called a priority queue. That is because when we want to traverse the graph we need to do so with the edge's with the lowest weight first. 

```
import heapq 

def dijkstra(graph, start, goal):

    # Initialize distances with infinity for all vertices
    distances = {vertex_key: float('infinity') for vertex_key in graph.vertex_dict}
    
    distances[start] = 0
    # Priority queue: (distance, vertex_key)
    pq = [(0, start)]
    
    # Track visited vertices
    visited = set()
    
    while pq:
        current_distance, current_vertex_key = heapq.heappop(pq)
        # Skip if already visited
        if current_vertex_key in visited:
            continue
        visited.add(current_vertex_key)
        # Skip if we found a better path already
        if current_distance > distances[current_vertex_key]:
            continue
        # Get the vertex object
        current_vertex = graph.get_vertex(current_vertex_key)
        
        # Explore neighbors
        for neighbor_vertex in current_vertex.get_connections():
            neighbor_key = neighbor_vertex.key
            weight = current_vertex.get_weight(neighbor_vertex)
            distance = current_distance + weight
            
            # If we found a shorter path, update and add to queue
            if distance < distances[neighbor_key]:
                distances[neighbor_key] = distance
                heapq.heappush(pq, (distance, neighbor_key))
    
    # After processing all reachable vertices, check if goal is reachable
    if distances[goal] == float('infinity'):
        return -1
    else:
        return distances[goal]
```

**Transposing graphs**
Transposing a graph means reversing the edges such that for some graph $G = (V, E)$ there exists a graph $G^T (V, E^T)$ where $E^T = \{(v,u) \in V \times V : (u,v) \in E\}$. To develop an algorithm that can produce that transposition we would need to swap out the edge pairs which might be represented in a matrix as a row,column intersection. In the adjacency list representation where you have for example {1: (2,3)}, then you have to now make the swaps so you have {2: (1)} and {3: (1)} which means you have to create keys that points to the key of the linked list.

The adjacency list version runs in $O(V+E)$ — we visit each vertex and each edge exactly once. The adjacency matrix version requires scanning every cell in the $V \times V$ matrix and runs in $O(V^2)$.

```
def transpose_adjacency_list(graph):  
    transposed_graph = {key: [] for key in graph}  
    for vertex in graph.keys():  
        for neighbor in graph.get(vertex, []):  
            transposed_graph[neighbor].append(vertex)  
    return transposed_graph
```

# Solving problems with graphs
There are many practical applications and interesting problems which graph data structures and algorithms are very useful. Graphs are quite versatile and can represent a quite broad range of problems. Let's start with a simple graph, in this case we have a graph with two **strongly connected components**. 
![](strongly%20connected%20components.png|center)

In *the art and craft or problem solving* Paul Zeits also describes graph theory and explain that it is a **crossover** that connects different branches of math in surprising ways. He also describes how many situations where there are some relationship between objects "can be recast as a graph, where the vertices are the "objects" and we join vertices with edges if the corresponding objects are "related"" (p. 109). It's therefore a commen representation in computer science problems which deal with related objects such as social media databases. Zeitz highlights how graph algorithms might be used when he use a graph to solve a problem with two people starting from two separate places of a mountain. The challenge is then to figure out if the two people can swap positions by traveling along the mountain range and staying at the same elevation. 
![](Two%20men%20tibet.png)
We need some insights to solve this. The first insights is that we can actually construct this as a graph. If invent points on this mountain range we can plot them into the original figure. We can then see that the two men can walk from (a,c) and (s,q). Next the person starting at a can walk backwards to b and th other from p to q. 
![](Graph%20two%20men%20tibet.png)
To recast this problem into a graph we can essentially think about it this way: 
* Each point is a vertex
* Points that are reachable "in one step" from others are connected by edges that means a and b, b and c and so on. 
If we then can show that there is a path from the (a,s) to (s,a) then we're done. 

While the problem above is a fun puzzle graph algorothms are found in many places when it comes to applied computer science allowing us to solve interesting problems like the CSES test problem introduced below. 

This algorithms asks you to count based on a map that represents a building, the number of rooms. For example in the map or grid below there are three rooms which represented by the floors closed in by the hashtag symbols. This problem can be thought of as counting the number of connected components in a graph. 

map = ("########",  
       "#..#...#",  
       "####.#.#",  
       "#..#...#",  
       "########")

The algorithm for counting the number of rooms begins by initializing a variables rooms that hold the number of rooms. Secondly we initialize an empty set and a rows, cols object. A for loop then enumerates over the rows and columns to check if the cell is a floor and if so, it runs the bfs() algorithm with the coordinates for that cell which essentially checks the neighboring cells until it has visited all the '.' that are connected to this component. 

```
from collections import deque  
   
def counting_rooms(grid):  
    rooms = 0  
    rows, cols = len(grid), len(grid[0])  
    
    # use 2D grid to hold values for each coordinate 
    visited = [[False] * cols for _ in range(rows)]
      
    directions = [(-1,0),(1,0),(0,-1),(0,1)]  
    
    def bfs(start):  
        queue = deque([start])  
        visited[start[0]][start[1]] = True  
        while queue:  
            r, c = queue.popleft()  
            for dr, dc in directions:  
                nr, nc = r + dr, c + dc  
                if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == '.' and not visited[nr][nc]:  
                    visited[nr][nc] = True  
                    queue.append((nr, nc))  
    for r in range(rows):  
        for c in range(cols):  
            if grid[r][c] == '.' and not visited[r][c]:  
                bfs((r, c))  
                rooms += 1  
    return rooms  
  
if __name__ == '__main__':  
    n,m = map(int, input().split())  
    graph = [input() for _ in range(n)]  
    result = counting_rooms(graph)  
    print(result)
```
A problem like this can be somewhat overwhelming but the breadth first search algorithm makes it fairly efficient as we can search the grid.

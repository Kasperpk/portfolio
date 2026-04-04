
**Implementation in python**
```
class Vertex:

    def __init__(self,key):
        self.key = key
        self.connections = {}

    def add_adj(self, vertex, weight=0):
        self.connections[vertex] = weight
    
    def get_connections(self):
        return self.connections.keys()
    
    def get_weight(self, vertex):
        return self.connections[vertex]    
```

The graph class is initialized using the dictionary data structure to hold the vertices or nodes. That shows how more complex or abstract data structures can built untop of more primitive ones. The graph needs to be able to add vertices and edges between them. Here we can use the vertex method *add_adj* to assign connections. 
```
class Graph:

    def __init__(self):
        self.vertex_dict = {}
    
    def add_vertex(self, key):
        if key not in self.vertex_dict:
            new_vertex = Vertex(key)
            self.vertex_dict[key] = new_vertex
    
    def get_vertex(self, key):
        if key in self.vertex_dict:
            return self.vertex_dict[key]
        return None
    
    def add_edge(self, f,t, weight=0):
        if f not in self.vertex_dict:
            self.add_vertex(f)
        if t not in self.vertex_dict:
            self.add_vertex(t)
        self.vertex_dict[f].add_adj(self.vertex_dict[t], weight)
```
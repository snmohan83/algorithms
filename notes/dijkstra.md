==================================
Explanation of Dijkstra Algorithm:
==================================

Consider a graph represented with G = (V, E) where V is the set of all vertices
and E is the set of all edges joining adjacent vertices.

Adjacency list is a list of vertices sorted such that the consecutive vertices
form an edge.

-----------
Relaxation:
-----------

In simple terms, these are the steps taken:

From any vertex u, the edge to reach the next adjacent vertex v in the
adjacency list will be relaxed.

if d() is the distance of any vertex from the initial source where the path is
started.(For a general case, d() can represent the total path cost until the
vertex under consideration.)

- d(u) is the distance/path-cost from source to vertex u.
- d(v) is the distance/path-cost from source to vertex v.

The edge (u,v) which belongs to E is relaxed implies, that if the shortest path
that can be possible to reach v has to go through u, then the distance between
u and v is added to the distance of u to get the shortest distance to v. 

If d(v) is set to d(u) + w(u,v) (i.e the shortest path to v is through u), then
u should be the predecessor of v. So a predecessor funcion pi(v) is set to u.
if d(v) is less than the sum of d(u) and distance between u and v, then there
is another path to v which can be completed with shorter distance than going
through u. In this case, the d(v) remains as it is. 

In either case, the relaxation method makes sure that the distance to v, is the
shortest path from the source.


--------------------------------------------
A Sample implementation of relaxation method:
---------------------------------------------

// Function w somehow calculates the path-cost/distance from u to v.
w(u, v) {
    return distance_from_u_to_v;
}

u = s;  // u initialized to source vertex.
relax(u, V) {
    for each v in V {
       if d(v) > d(u) + w(u, v) {
           d(v) =  d(u) + w(u, v);
           pi(v) = u;
       }
    }
}
   
-------------------
Dijkstra Algorithm:
-------------------

A few variables:

G -> Representation of the graph
E -> set of all edges in the graph
V -> set of all vertices in the graph

S -> Set of all vertices whose minimum distance/path-cost is computed
Q -> Priority Queue that contains all vertices which are yet to be examined.

    Q = V - S

Initial S has not entry since no vertuces are examined yet. so Q = V - {}

The loop runs for all entries in the queue Q (i.e until Q is empty)

For each iteration, 
- initialize u to the first entry from Q (u = s)
- Compute the shortest distance to u from the source s (d(u) = 0 if u = s)
- Push the entry to set S (since the path is now available)
- For a shortest path, all paths from every vertex in the path to every
  other vertex will be the shortest possible.
- The iterations that run for the Q exactly achieve the above goal.
- For each entry in the Q: 
   - set the source as u
   - check every vertex in the adjacency list and apply relaxation
- The key is that each time we enter a vertex u in the set S, we are sure
that the path cost from source s to u is the shortest.
- At the end of the algorithm, S shall contain the set of vertices in the
exact order to be traversed in order to find the shortest path to the 
given destination vertex.

The Dijkstra algorithm always chooses the closest vertex and hence it is
considered to follow a Greedy Strategy.

------------------------
Dijkstra Implementation:
------------------------

dijkstra(G, s) {
    S = {};
    Q = V - S;
    while !Q.empty() {
        u = min(Q); // minimum distance from source
        for each v in adj[u] {
            relax(u, V);
        }
    }
}

   

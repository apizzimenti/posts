So I'm on a project at work that requires a little elbow grease (and lots of
Markdown). We are developing an app that sources its data from a big database of magazines,
articles, and other little periodicals. There's a backend database dev and a frontend dev,
and I'm the JavaScript glue in the middle. And, as such, the responsibility of describing
the correct API calls fell to me.

Initially I started out with a graph that describes the database at its most basic level:
<img src="https://dl.dropbox.com/s/t4zszpx9r8pg22v/ERD_Graph.png?dl=0" style="width: 300px; height: 150px"/>

This gives me a good idea of which individual databases are connected and the paths through
each. Each edge on the graph represents a common property between the two databases.

Let's outline some parameters of the graph $G$:

$\omega (G)$ = minimum degree of graph $G$

$\Delta (G)$ = maximum degree of graph $G$

$V$ = set of nodes (vertices)

$E$ = set of edges

$\rho (v)$ degree of a node $v \in V$

$G = (V, E) $

$G$ is a *connected* graph, meaning that any node is reachable from any other node. This means that
because of the way the database is set up, we can reach any property of any database in one call to a single database, not
multiple calls to multiple databases. Each edge represents a shared property, such as an `id` or `volume` number.

Since $G$ is connected, each database has access to all other databases either one step or two steps away, depending
on the nodes' adjacency (this graph's greatest path length is at most two, from `magazine` to `author` to `person` is two steps). 
This allows for very fast and efficient indexing and querying, as there do not have to be calls to an external (disconnected) database. However, it may produce
complications in querying the `magazine`, `volume`, `work`, and `author` databases (represented by the connected graph
$E = (V, E)$ such that $E \in G$). The paths between the databases are variable, and so the way we query them must be the
most efficient (i.e. the shortest path between the nodes).

I'll go into that stuff ^^ in a later post.

Now, I encouraged data persistence and big data dumps rather than mutable data and many small data
accesses. This saves energy on the part of the browser and user's computer and reduces traffic to 
the databases.

The hierarchy I wanted to establish was this:

`magazine`$\rightarrow$ `volume` $\rightarrow$ `work`

Where a call to `magazine` returns info about the magazine and a list of `volume` objects,
each containing information about that volume (year, number, etc.). Each `volume` object would
contain a list of `works`, which are the smallest subset of a magazine. This way, when a user
tries to access the `magazine` database (or search it), all data is present and can be immediately
written to the DOM instead of waiting on multiple API calls.
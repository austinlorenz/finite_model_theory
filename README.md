# finite_model_theory
A Maxima CAS package for finite model theory

This package uses Maxima's graph package to 
1) test whether a given graph is a model of a given first order formula
2) compute least and simultaneous fixed points of first order formulae on graphs
3. play Ehrenfeucht–Fraïssé games on graphs.

To test whether a given graph is a model of a given first order formula, load the file "MaximaLogic",
(%i) batch(MaximaLogic);
and assign the graph in question to the global variable G.  The first order formula which defines the completeness query is
"for all x and for all y, x != y implies E(x,y)"
that is, every pair of vertices which are not equal are connected by an edge of the graph.

To quantify, use 'fa' for universal and 'exz' for existential.  The maxima translation of the above formula is
fa(x, fa(y, x != y implies E(x,y)))

Now we assign a complete graph to G, and enter the above translation of our formula, which Maxima evaluates.
(%i) G : complete_graph(10);
(%o)                  GRAPH(10 vertices, 45 edges)
(%i) fa(x, fa(y, x != y implies E(x,y)));
(%o)                              true

We now set G to a graph which is not complete, and test again:

(%i) G : cycle_graph(10);
(%o)                  GRAPH(10 vertices, 10 edges)
(%i) fa(x, fa(y, x != y implies E(x,y)));
(%o)                              false

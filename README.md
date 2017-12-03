# finite_model_theory
A Maxima CAS package for finite model theory

This package uses Maxima's graph package to 
1) test whether a given graph is a model of a given first order formula
2) evaluate non-Boolean queries on graphs
2) compute least and simultaneous fixed points of first order formulae on graphs
3) play Ehrenfeucht–Fraïssé games on graphs.

1) test whether a given graph is a model of a given first order formula

To test whether a given graph is a model of a given first order formula, load the file "MaximaLogic",

(%i) batch(MaximaLogic);

and assign the graph in question to the global variable G.  The first order formula ψ which defines the completeness query is

ψ ≡ ∀x∀y(x≠y→E(x,y))

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

2) evaluate non-Boolean queries on graphs

To evaluate non-Boolean queries on graphs, use the LFP function.   Suppose we wish to define a query which returns all vertices of degree two or greater.  The first order formula defining this query is

ϕ(x) ≡ ∃y∃z(E(x,y)∧E(x,z)∧y≠z)

This reads "There exist vertices y and z such that there's an edge between x and y and an edge between x and z, and y and z are not the same vertices."  Note that x is not quantified--it is a free variable in the formula, and m-ary query  Q defined by ϕ(x) returns the set of a∈|G| such that G⊨ϕ(a). 

We translate the formula to Maxima code,

(%i132) phi : '(exz(y, exz(z, E(x,y) and E(x,z) and y!=z)));
(%o132)        exz(y, exz(z, E(x, y) and E(x, z) and (y != z)))

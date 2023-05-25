# God Files & Cohesion

We want to break apart a god file into smaller pieces. These smaller pieces should be extract class refactoring candidates. It would be nice if these smaller pieces fit some concept of "cohesion" that we also define.

In short, we want a score similar to modularity or CPM that is specific to cohesion within a god file. We have several "views" to work with: internal structure, downstream files, upstream files, and lexical.

- [ ] Review JDeodorant and identify shortcomings
- [ ] Review existing cohesion research

## Prior Work

### Community Detection

Many community detection methods operate by maximizing some quality function like modularity or CPM. They typically operate on very large undirected graphs. Because of the size of these graphs (i.e. networks) these optimization methods tend to emphasize scalability. Scalability is less important in this case because our graphs (the identifiers inside a god file) tend to be fairly small (a few thousand vertices at most). Additionally, DAGs are almost never explicitly considered.

**[From Louvain to Leiden: guaranteeing well-connected communities. (2019)](https://arxiv.org/pdf/1810.08473.pdf)** A recent state of the art community detection algorithm designed for undirected graphs. Intended to maximize modularity or Constant Potts Model (CPM), both of which have a resolution parameter. Can be adapted to maximize other metrics.

**[Narrow scope for resolution-limit-free community detection. (2011)](https://arxiv.org/pdf/1104.3083.pdf)** Introduces the Constant Potts Model (CPM) as an alternative to modularity.

**[Fast unfolding of communities in large networks. (2008)](https://arxiv.org/pdf/0803.0476.pdf)** Introduce the Louvain algorithm to optimize modularity.

**[Statistical Mechanics of Community Detection. (2006)](https://arxiv.org/pdf/cond-mat/0603718.pdf)** Interpret community detection as finding the ground state of an infinite range spin glass. Uses simulated annealing. Introduces the resolution parameter.

**[Finding and evaluating community structure in networks. (2004)](https://arxiv.org/pdf/cond-mat/0308217.pdf)** Very influential paper introducing the modularity score.

### Community Detection for Directed Graphs

There are some papers out there written on the topic of community detection in directed graphs and even less on community detection in directed acyclic graphs.

**[Making Communities Show Respect for Order. (2020)](https://arxiv.org/pdf/1908.11818.pdf)** Introduces the concept of antichains and a fast way to detect them.

**[Community detection in directed acyclic graphs. (2015)](https://arxiv.org/pdf/1503.05641.pdf)** A modularity measure for DAGs and a spectral algorithm to maximize it by extending the spectral algorithm developed for undirected networks. (Are discovered communities also acyclic?)

**[Directed Louvain: maximizing modularity in directed networks. (2015)](https://hal.science/hal-01231784v1/file/main.pdf)** A community detection method that is specific to directed graphs. Does not consider cycles.

### God File Refactoring

The only existing god file refactoring approach that I am aware of is provided by [JDeodorant](https://github.com/tsantalis/JDeodorant). JDeodorant is an Eclipse extension that includes many refactoring tools. The authors of JDeodorant have published several papers on their god file refactoring approach.

**[Identification and application of Extract Class refactorings in object-oriented systems. (2012)](http://users.encs.concordia.ca/~nikolaos/publications/JSS_2012.pdf)**

**[JDeodorant: Identification and Application of Extract Class Refactorings. (2011)](http://users.encs.concordia.ca/~nikolaos/publications/ICSE_2011.pdf)**

**[Decomposing Object-Oriented Class Modules Using an Agglomerative Clustering Technique. (2009)](http://users.encs.concordia.ca/~nikolaos/publications/ICSM_2009.pdf)**

### Cohesion

There is no singular definition of "cohesion."

**[Identification of Move Method Refactoring Opportunities. (2009)](https://users.encs.concordia.ca/~nikolaos/publications/TSE_2009.pdf)** Introduces the Entity Placement metric which is used by JDeodorant. This is the ratio of cohesion over coupling where cohesion and coupling are also defined. Has a good related work section containing other cohesion metrics.

**[Metrics Based Refactoring. (2001)](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=914965)** Introduces software quality metrics (including) cohesion based on Jaacard distance. Also discusses how to use them for refactoring (including move method and extract class.)

## Software

**[NetworkX](https://networkx.org/)**

**[CDlib](https://cdlib.readthedocs.io/)**

**[DirectedLouvain](https://github.com/nicolasdugue/DirectedLouvain)**

**[Mermaid](https://mermaid.js.org/)**

## Loose Ideas

### Information Theoretic Cohesion Metrics

How many bits of information does it take to describe a member of a given class or file with respect to a certain aspect? For instance, if a class has two fields and every method uses those two fields (directly or indirectly), it would take 0 bits of information to describe any of the methods (because they are all identical with respect to their field usage.) However, if one method used zero or one of the fields, it would now take 1 bit to describe each method.

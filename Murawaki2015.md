# Spatial Structure of Evolutionary Models of Dialects in Contact

## Yugo Murawaki (2015) - PLoS ONE

### Overview

Network topologies are used to model the influence that place X has on place Y. Population and distance are the two factors that determine the degree of influence, so that places with larger population have more influence and the influence decreases over distance. The network topologies are kept time-invariant, meaning that the the degree of influence stays constant over time.

The simulation adds a new cognate in each step and then calculates to what extent the new cognate gets adopted and diffused across the network. New cognates can only appear once and after their death they do not come back.

Issues in the model listed by the author as potentially violated in real language data:

* Two cognates can be in complementary distribution for a concept, so that there is no competition between them (e.g., Dutch words for 'head' are *hoofd* for humans and *kop* for animals)
* Borrowings from neighbours can mean that cognates can in fact 'come back from the dead'
* New cognates do no have to emerge per se, as semantic shifts can cause an existing cognates to acquire a new meaning

The goal of the simulation is then to compare the tree-like statistic of different types of network topology against statistics from existing language families, to see whether variation in the network is better explained by a temporal (tree) model or by a spatial model. The simulation is then run on five types of network topology:

* **GRID**: equivalent population sizes and equal distance between the nodes (spatially non-tree-like)
* **STAR**: a large centre node with smaller nodes all around it, i.e. a centre-periphery (spatially tree-like)
* **TWOSTARS**: two large nodes on opposite sides
* **BOTTLENECK**: two groups of nodes connected through a single node in the middle
* **COLONY**: two groups of nodes (East-West), in which the West creates a colony in the East that influences that part of the network after 3/4 of the time

### Results

NeighborNet is used to visualise the relationships between the varieties and a Bayesian phylogenetic model is run to see how the data is interpreted by these methods. The author uses *δ* scores to compare the simulated networks to:

* 0.22 for Indo-European
* 0.23 for Germanic
* 0.25 for Ainu
* 0.44 for Polynesian

The findings are:

* **GRID**: non-tree-like, with *δ* = 0.43, the network topology strongly reflected in the NeighborNet structure, and low clade stability in the phylogenetic tree
* **STAR**: moderately tree-like, with *δ* = 0.28, the network topology is well reflected in the NeighborNet structure, and the phylogenetic tree interprets the peripheral subgroups as temporal structure
* **TWO STARS**: tree-like, with *δ* = 0.19, although the NeighborNet structure does not look very tree-like, but the phylogenetic tree show two distinct dialect groups, where the two equidistant middle nodes are seen as outlier is the two groups (which shows the effect of randomness in the simulation)
* **BOTTLENECK**: very tree-like, with *δ* = 0.15, the NeighborNet structure show two distinct dialect groups, which is also reflected in the phylogenetic tree, with the connecting node as an outlier in one of the groups -- this situation reflects the findings for Ainu by Lee & Hasegawa
* **COLONY**: non-tree-like, with *δ* = 0.33, the NeighborNet structure puts the origin and the colony nodes close together, but the phylogenetic tree splits them early on, so that the models interprets dialects influenced by the colony node as if they emerged later even though they existed from the beginning -- this situation reflects the findings for Japanese by Lee & Hasegawa

So, in sum:

* Low *δ* scores can emerge from spatial tree-like structures and do not necessarily reflect temporal tree-like evolution
* Some spatial structures cause unnatural results in phylogenetic trees (e.g., the bottleneck and colony situations)



### Specifics of the simulation 

**work in progress**

w = degree of influence

if j is connected to i: w = population-j / distance i-j ^ 2
if j = i: w = s * popuation-i (self-influence; s is set at 2)
else: w  = 0 (if not connected)

C(t,i) is the set of cognates in node i at time t
V(t,i) is the power set of C(t,i) excluding the empty set

* a power set is all possible combination of a set

C(t,i) is constructed by combining a new cognate candidate with sets of cognates that node i’s neighbors had at time t − 1

= the union of {new word} and the power set of cognates used by the neighbours

### Random other points

Author questions the validity of the Lee & Hasegawa tree, but does not address that its main assumption is that all contemporary varieties evolved from Middle Japanese (MJ), which is questionable.

This is a good improvement over Lee & Hasegawa (2011):

* p.4 "A language may have multiple cognates for a single concept."
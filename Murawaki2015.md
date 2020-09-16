# Spatial Structure of Evolutionary Models of Dialects in Contact

## Yugo Murawaki (2015) - PLoS ONE

### Introduction

Author questions the validity of the Lee & Hasegawa tree, but does not address that its main assumption is that all contemporary varieties evolved from Middle Japanese (MJ), which is questionable.

This is a good improvement over Lee & Hasegawa (2011):

* p.4 "A language may have multiple cognates for a single concept."

The network topologies are kept time-invariant.

Population and distance are the two factors that determine the degree of influence.

w = degree of influence

if j is connected to i: w = population-j / distance i-j ^ 2
if j = i: w = s * popuation-i (self-influence; s is set at 2)
else: w  = 0 (if not connected)

C(t,i) is the set of cognates in node i at time t
V(t,i) is the power set of C(t,i) excluding the empty set

* a power set is all possible combination of a set

C(t,i) is constructed by combining a new cognate candidate with sets of cognates that node i’s neighbors had at time t − 1

= the union of {new word} and the power set of cognates used by the neighbours
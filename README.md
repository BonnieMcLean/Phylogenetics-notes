# Tutorial on computational linguistic phylogeny

## Trees
### Types

<Figure>

![](https://i.imgur.com/AyFMzd2.png)
<FigCaption>Rooted tree</FigCaption>
</Figure>


<Figure>

![](https://i.imgur.com/2lO8gGB.png)
<FigCaption>Unrooted tree</FigCaption>
</Figure>

### Terminology

* **Unresolved tree/high degree node**: when a node has many children, because you don't know what all the splits are (there was probably more than one separate splitting event to produce all those children, but you just don't know).

## Networks
<Figure>

![](https://i.imgur.com/MwmpR8N.png)
<FigCaption>Underlying genetic tree with distinct contact event. </FigCaption>
</Figure>

<Figure>

![](https://i.imgur.com/sYf9rUN.png)
<FigCaption>Phylogenetic network. It's not a tree because it's cyclic, i.e. there is more than one way to get to, e.g. a to c or e to g, etc. Internal nodes don't represent ancestors between given languages, but are introduced in order to represent the conflict between the different possible splits produced in the data analysis. </FigCaption>
</Figure>

Parallel lines in this network could represent: 

* contact events 
* homoplasy (i.e. independent evolution of the same traits)
* backmutation (the reappearance of a trait that occurred at an ancestor)
*  Or simply insufficient data to produce a comprehensible tree.

Because of this uncertainty, these types of graphs are called **implicit networks**.

-> see Huson and Bryant
(2006) for a discussion of these differences between implicit and explicit networks, and McMahon and McMahon
(2005: Chapter 6) for a comparison between different implicit phylogenetic
network methods.

## Character coding

Haven't read the first of this section

Strictly speaking, an unchanged cognate and one changed by derivation probably should be represented as different character changes -> I haven't done this

## Statistical models of language evolution
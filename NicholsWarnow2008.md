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
* **homoplasy** (i.e. independent evolution of the same traits)
* **backmutation** (the reappearance of a trait that occurred at an ancestor)
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

**Stochastic process**: How a set of traits evolves within a family of languages. Each trait can assume several states, and changes between states will occur with some probability on each branch of the tree.

The probability with which the trait will change its state can depend on the branch, and also on the character, so *stochasitc processes need not assume all characters evolve identically, nor that a given character evolves identically on all branches of the tree.*

The stochastic process will make explicit statements about:
* **Independence of character evolution**--do changes in one character impact the probability of change for another character, or do they evolve independently?
* **Degree of homoplasy** (if you don't allow homoplasy then all state changes produce new states).
* **Amount of polymorphism** (both in terms of percentage of characters that exhibit it and the number of states that are permitted to simutaneously be present in one language for one character)--**polymorphism** is when a character exhibits two or more states in one language, i.e. uses two or more different cognates for a given meaning
* **Amount of borrowing** (both in terms of the number of contact events and the percentage of characters that evolve with borrowing)
* **Degree to which different characters are allowed to evolve differently.**

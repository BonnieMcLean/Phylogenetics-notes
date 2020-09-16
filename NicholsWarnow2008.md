# Tutorial on computational linguistic phylogeny

## Trees

<Figure>

![](https://i.imgur.com/AyFMzd2.png)
<FigCaption>Rooted tree</FigCaption>
</Figure>


<Figure>

![](https://i.imgur.com/2lO8gGB.png)
<FigCaption>Unrooted tree</FigCaption>
</Figure>

**Unresolved tree/high degree node**: when a node has many children, because you don't know what all the splits are (there was probably more than one separate splitting event to produce all those children, but you just don't know what they were).

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

**More reading:** see Huson and Bryant
(2006) for a discussion of the differences between implicit and explicit networks, and McMahon and McMahon
(2005: Chapter 6) for a comparison between different implicit phylogenetic
network methods.

## Character coding

**Terminology**
|Biology        |Linguistics                                       |
|---------------|--------------------------------------------------|
|taxa           |languages                                         |
|characters     |words, grammatical features,etc.                  |
|character state|cognate sets, values of grammatical features, etc.|

**Lexicostatistics**: phylogenetic techniques that use the words of languages as characters. In comparison to the traditional comparative method, which usually tracks cognate forms and their development regardless of meaning shifts undergone, in lexicostatistics you track the glosses (meanings) and the cognacy of the glosses.

**Special types of characters:**
* **phyletic characters**--e.g. specific sound changes, which aren't likely to occur by chance in unrelated languages; cognates (which are by definition **non-homoplastic**--an accidental homophonous word may occur independently, but it is a historically unrelated word and not a cognate).
* **phenetic characters**--e.g. typological features, such as glottalised consonants, tone systems, accusative alignment in nouns, etc. These are **homoplastic** by definition, which means that they can independently appear in unrelated languages. Common phonological and/or morphological changes and semantic shifts can also be homoplastic.
* For more examples, a series of studies by Ringe and Warnow and their colleagues (Ringe et al. 2002; Nakhleh et al. 2005a) seek out cognates and diagnostic phyletic characters that are non-homoplastic. Dunn et al. survey exclusively typological characters that are quite homoplastic. Saunders (2005) and Wichmann and Saunders (2007) combine typological and lexical characters.







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

### Types of models
#### Parametric model for binary (two-state) characters
* There is a tree with the leaves labeled by the set of languages.
* You put into the model (for each character) the probability for the root to exhibit the cognate (i.e. to have the character state of 1), and substitution probabilities for each edge of the tree, which indicate the probability that the character will change its state on the edge.
* The character thus evolves down the tree and would assign states (either 0 or 1) to each node of the tree. A change on an edge from 0->1 indicates the appearance of the cognate (but not whether it is the first appearance or a reapparance), and a change from state 1->0 indicates the loss of the cognate. 
* Note that if a character changes twice on some path, then it will begin and end in the same state; thus, this model allows homoplastic events. Constraints on the model to prohibit homoplastic changes can be made, however. 
* Also note that in this model all characters are supposed to evolve under the same process (you don't have separate parameters for separate characters). However, in some cases some additional variation between characters is enabled--but is constrained so as to be able to be represented by just one additional parameter for the entire set of characters (i.e, the characters draw a rate of evolution from a distribution which can be described by that single parameter). 
* Multistate characters can be modelled in essentially the same way--however, you need to specify if the number of states is bounded (e.g. by saying that there are only four possible states, and all substitutions are between these for states) or unbounded (with an infinite number of possible states). Here too, homoplasy can be allowed or prohibited. 
* The tree and the values for the various parameters define the probability of any given set of sequences at the leaves of the tree. The **maximum likelihood estimation method** would try to `find the tree and parameter values that are most likely to produce the input sequences.`
* Examples: Gray and Atkinson on Indo-European w/ a Bayesian analysis is the original application of this model, The homoplasy-free version of the multistate character model has been used for simulation purposesin several studies (see, for example, Minett and Wang
2003; McMahon and McMahon 2005; Wang and Minett 2005). Extensions
of these models to allow for borrowing have also been considered,
with homoplasy-free versions studied by McMahon and McMahon
(2005), Minett and generally by Warnow et al. (2006) (who proposed a parametric model
allowing homoplasy) and Barbançon et al. (forthcoming) (who performed
a simulation study under the Warnow et al. 2006 model).Wang (2003), Wang and Minett (2005), and more
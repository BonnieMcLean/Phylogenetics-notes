# Tutorial on computational linguistic phylogeny

## Basics: trees and networks

### Trees
<Figure>

![](https://i.imgur.com/AyFMzd2.png)
<FigCaption>Rooted tree</FigCaption>
</Figure>


<Figure>

![](https://i.imgur.com/2lO8gGB.png)
<FigCaption>Unrooted tree</FigCaption>
</Figure>

**Polytomy**: When a node has many children. Such nodes are called *high degree nodes*, and trees containing such nodes are *unresolved trees*.

**Hard polytomy**: nodes with three or more daughters which represent a true radiation, i.e. an exception to the usual assumption that diversification is bifurcating. 

**Soft polytomy**: a high degree node where the large number of daughters represents a lack of information, so that the true history (which is probably bifurcating) is unclear. Soft polytomy is considered the default polytomy (hard polytomies are exceptions). 

Note that a soft polytomy is consistent with any more resolved analyses of its subbranches--soft polytomies assert that all refinements in the tree are viable candidates for the true evolutionary history--whereas a hard polytomy is not.

### Networks
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

**More reading:** See Eska and Ringe 2004 for mistakes people make when character coding.

Strictly speaking, an unchanged cognate and one changed by derivation probably should be represented as different character changes -> I haven't done this

## Phylogenetic analyses

### Maximum parsimony
Find a tree on which the minimum number of evolutionary changes occur. These analyses can be modified to allow the inclusion of characters with missing entries (semantic slots for which a language has no words). By default, MP produces unrooted trees, so if the location of the root is also desired you need to specify that. The usual way to root the tree is to use an **outgroup** (a language that is related to the rest of the languages in the set, but clearly is not as closely related to any language in the set as they are to eachother), which allows the tree to be rooted on the edge leading to the outgroup (e.g. the outgroup for my data could be Okinawan). For example, including a Germanic language with a group of Balto-Slavic languages allows the tree to be rooted on the edge leading to Germanic. Alternatively, including **directed characters** (i.e. ones where you know the ancestral state and therefore the direction of change, or can at least state the predicted direction based on things like phonological changes having a natural directionality) in the data matrix can be used to restrict the possible locations of the root to a subset of the tree. Maximum parsimony analyses are performed using heuristics (most often hill-climbing heuristics combined with some randomisation techniques to escape local optima), which are not guaranteed to find optimal solutions but perform reasonably well in practice. Software products that perform effective MP analyses include PAUP* and TNT.

### Maximum compatibility
Find a tree on which a maximum number of characters evolve without any homoplasy (back mutation or parallel evolution); these characters are said to be compatible on the output tree, and hence the number of such characters is the compatibility score of the tree. Characters can be weighted. MC also does not return rooted trees, and so outgroups or directed characters are used to help locate the root. Unfortunately, unlike MP, there are no readily available heuristics that are accurate in practice.

### Consensus trees
In both MP and MC, often several trees are found with the same best score. In this case, the usual practice is to return a concensus tree of some sort. To do this, the trees with the best scores are passed to an algorithm that examines the trees to determine the features that they either all share or which a majority share. It usually looks at the splits, or bipartitions, on the leaf set induced by the edges of each tree. A *strict consensus tree* has exactly those splits that are present in every one of the best trees. A *majority consensus tree* contains those edges whose corresponding bipartitions appear in strictly more than half of the input trees. A *greedy consensus tree* is formed by computing the majority consensus and then refining the tree by adding bipartitions from the input trees. By construction, `the strict consensus tree is the least resolved, the greedy consensus tree is the most resolved, and the majority consensus is in the middle.` Another way of looking at it is that the greedy tree refines the majority consensus tree, and the majority concensus tree refines the strict consensus tree. All these consensus trees can be computed in polynomial time. Frequently, the `edges of a majority or greedy consensus tree are annotated with the percentage of best trees containing that bipartition`. These edge annotations can be interpreted as the support for each edge.

### Edge annotation by bootstrapping
This is another technique sometimes used to produce these edge annotations (i.e. to estimate support values). Random datasets are created by randomly picking characters from the input data matrix and then these random datasets are analysed using the same method as the original phylogenetic analysis. Sometimes bootstrapping is just used to estimate support values for the edges in the final tree, where the support for an edge is the fraction of times that bipartition shows up in the bootrap analysis trees. Other times, the different bootstrap trees are used earlier as input to a consensus method (like the strict consensus, majority consensus, or greedy consensus) which is then annotated with the support estimates. 

The way the random matrices are produced is by  **sampling with replacement** in which each sample character is drawn randomly from the entire dataset (not the dataset minus characters already drawn). Rows of the dataset correspond to languages, and the columns represent characters (concepts). Sampling with replacement produces a new datamatrix with the same number of rows and columns, but where each column is obtained by picking one of the columns in the original matrix at random. Thus, `some columns from the original matrix will appear once, some two or more times, and some not at all, in the newly created random bootstrapped matrix`. The idea behind this is if a split is supported no matter what data you pick then its likely to be true of the true tree--but high boostrap support on a bipartition does not correspond to the actual probability that the bipartition is true.

### Maximum likelihood and Bayesian analyses
* Based on explicit parametric models of evolution
* Simulation studies of biomolecular evolution have shown that these methods produce good estimates of true evolutionary history--`provided that the sequences evolve under the same model used to estimate the history`. 
* An advantage over other methods is that they make explicit statements about the assumptions regarding the evolutionary process operating on the data.

#### Maximum likelihood methods
* Attempt to find the tree and associated model parameters so as to maximise the *probability* of producing the observed data.

#### Bayesian methods
* Do not try to find sepecific model parameters, or even the tree, but instead estimate the probability that each tree is the true tree--they produce not a single tree, but a probability distribution on the set of trees. See Gray & Atkinson 2003, Nicholls & Gray 2007 for examples.
* **Bayesian algorithm**: begin with an initial model tree (i.e. a rooted tree with initial values for each parameter), then go on a **random walk** through the **model tree space**, at each point computing the probability of the observed sequences being produced by the given model tree. If this probability is higher than the previously computed probability, the move to the new model tree is accepted; if it is lower, the move is accepted with some lower probability. After a **burn-in** period, the random walk is supposed to be in the stationary distribution. Then the algorithm randomly samples from the model tree space that it visits. This collection of model trees is used to produce a probability distribution on the space of model trees. A standard output of a Bayesian analysis is a **consensus tree** (usually the majority consensus tree) of the sampled trees. Sometimes, however, the tree appearing the most frequently (called the **maximum posterior probability tree**) is returned. The edges of the trees are annotated using the proportion of sampled trees in which that edge appears, which are interpreted as support for the edge.
* Bayesian analyses take a very long time, and depend very closely on the parametric model of evolution. Their accuracy thus depends on the fit between this model and the data. 
* The `main advantage of Bayesian analyses over other statistical methods is that they automatically provide support estimations`, whereas maximum likelihood or MP would normally use boostrapping (which is computationally intensive) to provide support estimates. 

### Network methods
* NeighbourNet (Byrant and Moulton 2004) is most popular, but Network, SplitsTree and Perfect Phylogenetic Networks are also used. Of these, Perfect Phylogenetic Networds are explicit phylogenetic networks, while the others are implicit phylogenetic networks.

### Distance-Based methods (Neighbour joining)

* The character based matrix is used to compute a distance matrix, for e.g., by defining the distance between two languages to be the proportion of the character matrix in which the two languages are different, or the Levenshtein distance. This distance matrix is then used to contruct a tree.
* Generally very fast and can also be quite accurate--but the accuracy depends both on how the distances are computed and how they are used to obtain the tree.
* The idea with the distance matrix is that it should be **additive on the true tree**, which means it's possible to assign lengths to the edges of the true tree so that the distance between any two leaves in the tree exactly equals the sum of the lengths of the edges in the path between the two leaves.
* Additive distances fit trees perfectly and enable exactly accurate trees to be reconstructed using simple and fast algorithms (Waterman et al.1977, see also Kim and Warnow 1999; page 18 of the slide presentation at http://www.cs.utexas.edu/users/tandy/nov26.ppt shows how an additive matrix defines the tree.
* Corrected distances account for hidden character state changes (e.g. where a character changes state twice) and so better approximate the actual number of changes that occured in the evolutionary pathway relating two languages--simulation studies suggest correcting distances to account for hidden character state changes produces improved phylogenetic estimations.
* An alternative to correcting distances is to assume that evolution is clocklike (i.e. the number of character state changes is proportional to time) so that even if the distances are not additive, they will be reasonable estimates of the time that has elapsed since the common ancestor. Under these conditions, even simple (uncorrected) distances will be suffiecient to ensure an accurate tree.
* Once the distance matrix is computed, methods like UPGMA (unweighted pair group method with arithmetic mean, Michener and Sokal 1957), or neighbour joining (NJ, Saitou and Nei 1987) are used to produce a tree.
* UPGMA works by repeatedly joining (as sister languages) the two languages in the group that have the smallest distance. It is guaranteed to perform correctly when the input distances are produced from a dataset that has evolved with clocklike evolution; but if not, it can make a mistake and infer that two languages are siblings when they are not.
* NJ operates by computing a transformation of the given distance matrix, and selecting as a pair the languages that minimise the transformed distance. `The transformation allows NJ to be correct even when the languages do not evolve under a lexical clock.`

## Evaluating phylogenetic analyses

Accuracy depends on:
* method used to analyse the data (estimation method)
* choice of languages (and how sparsely or densely sampled the set is)
* number and type of characters used and how these characters are encoded

The rest of this section discusses techniques for comparing and evaluating different methods.

### Compare to benchmark trees and known dates

1. **Compatible resolution**: the estimated tree may differ from the benchmark subgroupings (i.e. subgroupings we are sure about based on reliable lexical and grammatical data), but the estimated tree and benchmark tree (also called the constraint tree) must be compatible--so the estimated tree should not mix established subgroups (e.g. placing one Italic language in Germanic).
    - Note that undifferentiated groupings are compatible with differentiated ones, e.g. if the tree has a Germanic clade but fails to resolve it into North and West Germanic, that is okay (it's not okay if it does resolve it but mixes north and west germanic).
2. **No missing subgroupings**: the reconstructed tree should include all established subgroups. This is desirable but not essential. E.g. a good estimation method for Indo-European should not fail to return Germanic as a family, and should not fail to separate Baltic from Slavic.
3. **Calibration**: the reconstructed or computed date must be reasonably close to the established date. If it is not, the established date should be used to calibrate the method (rather than the method's output being announced as a new date for the family).

Any comparison between two methods should take the degree of failure of these criteria into account in order to make a recommendation between two methods. 

The problem is, often just using these benchmark trees and datasets is not enough to distinguish the methods (they may all produce the established subgroupings). The ability to match established subgroups is a relatively basic capability that can be accomplished by many methods, which can otherwise produce very different solutions. So you should look at more factors, as discussed in the rest of this section.

### Computational complexity and run time
* The techniques tell you their maximum run time (i.e. the slowest possible case). For example, the agglomerative clustering technique in glottochronology has a runtime to the order of n squared ($O*n^2$), where $n$ is the number of languages. This means that the run time is never more than some constant times $n^2$, no matter how big $n$ is. (**Agglomerative clustering** is a way of building trees from the bottom up, where each observation starts in its own cluster, and pairs of clusters are merged as one moves up the tree.)
* Algorithms that have worst-case run times bounded from above by some polynomial in the input size are said to be **polynomial time**, while algorithms that have worst-case run times that can be exponential in the input size are **exponential time**.
* An algorithm that runs on exponential time is likely to take a long time on all but very small inputs.
* While agglomerative clustering is simple, other algorithms (e.g. finding the tree with the minimum total number of evolutionary changes) are more complex and require us to consider run time. For example, strategies that examine every possible tree and then return the best one (with the minimal number of changes) will be provably optimal, but take forever. This is addressed with techniques that use **hill-climbing**--you start with an initial tree, then look at small changes to the tree (typically obtained by detaching one part of the tree and reattaching it elsewhere) to see if a better tree can be found. The process terminates when a tree is found that is better than all the previous trees, but where none of the 'neighbouring' trees are better.
* Hill-climbing strategies can find good solutions on big datasets relatively quickly, but are not guaranteed to find the globally optimal solution. They can get **stuck in local optima**--trees that are better than all the neighbouring trees, but not as good as the best tree for the dataset. 
* Techniques for escaping local optima are also part of these algorithms, and generally use randomness to move. Run time analyses of such hill cimbing algorithms (or heuristics) are difficult to obtain, so are usually given in terms of empirical experience. For example, Wichmann and Saunders (2007) report a run time of 41 hours to apply the Gray and Atkinson Bayesian analysis to a dataset consisting of 12 pairs of sister languages and 17 characters. 
* **NP-hard** (non-deterministic polynomial-time hardness): a problem is NP-hard if it is unlikely to be solvable in polynomial time.

### Statistical evaluation measures

* CI, RCI (rescaled consistency index): ranges from 0.0 to 1.0, and measures the amount of homoplasy in the data, with 1.0 indicating no homoplasy at all (Naylor and Kraus 1995: 559). Since MP performs well under conditions of low homoplasy, an MP analysis of a dataset with very little homoplasy (RCI close to 1.0) will potentially be highly accurate (and MP analyses of datasets with a lot of homoplasy may not be very accurate)
* When either the CI or RCI is very close to 1.0, the argument that the data are evolving in a tree-like fashion is probably reasonable. If there is no homoplasy at all, then no borrowing needs to be posited to explain the data.

### Theoretical guarantees
These are the conditions under which a method is *guaranteed* to produce an accurate estimation (note that these sufficient conditions may not be necessary in the sense that the method may produce the true tree even when the conditions do not hold). You should ask whether it is reasonable to assume the data being analysed will have the required properties. Below are the conditions for different methods:

* **MP and MC (weighted or unweighted)**: these are guaranteed to produce the true tree when characters evolve in such a way that the tree with the minimum number of events is the true tree. One condition under which this holds is if the characters evolve without any homoplasy at all (so no back mutation or parallel evolution) and without any borrowing. This is highly unrealistic. However, all gurantees regarding methods for MP and MC apply only if the optimisation problems are solved optimally, which basically never happens.
* **Maximum likelihood and Bayesian methods**: For most models considered in phylogenetics, maximum likelihood and Bayesian methods will produce the true tree provided the true evolutionary process matches the assumed model, the dataset contains enough characters, and the methods are run exactly instead of heuristically (i.e. run long enough). 
   - *How long is long enough?* It's not clear how long is 'long enough'. In practice, the methods are run until improvements have not been obtained for some period of time, but there is no reliable way to determine whether this is actually long enough. Heuristics for NP-hard optimisation problems need to be run 'long enough', as do Bayesian analyses. For Bayesian analyses, it's because they employ employ Markov Chain Monte Carlo (MCMC) techniques (which are based on randomization) to move through ‘model tree space’. These techniques have the theoretical guarantee that if run long enough, the random walk is supposed to have arrived at a stationary distribution, in which further random walking produces only temporary fluctuation, and when this happens the output from the Bayesian analysis will have the correct theoretical properties. When this happens, the maximum posterior probability tree produced by the analysis will be guaranteed to be the true tree. There are techniques that can be applied to detect that the method has not been run long enough, but these techniques do not allow the user to determine that the method has for sure been run long enough. `For the Bayesian analyses
used in linguistics, it is quite possible that runs of a few days are sufficient (for small enough datasets), but it is also possible that the phylogenetic analysis would be different in interesting and important ways if the analyses were allowed to run for longer. Until these questions are studied carefully, however, caution seems the best policy.`
   - Gray and Atkinson's Bayesian method is guranteed to be correct (with respect to estimations of tree topology) when all the binary characters (each based on a single cognate set) evolve **identically** and independently of each other--`this is may be a problem for me because the ideophones evolve differently from the non-ideophones... more likely for homoplasy to occur. I also don't know that the evolution of the meanings of ideophones are independent of each other... a new ideophone appearing for some concept may trigger a shift in meaning of another ideophone for the same concept`. The dating aspect of their method is guaranteed to be correct when the data evolve under a lexical clock.
* **Neighbour joining** is guaranteed to produce the true tree when the pairwise distance matrix is sufficiently close to an additive matrix defining the true tree. Typically, additive matrices in linguistic phylogenetics define the pairwise distance between two languages to be equal to the number of character state changes (e.g. word replacements) that occured in the evolutionary history between the two languages.
* **UPGMA**, used in glottochronology, is guaranteed to produce the true tree when evolution is sufficiently close to clocklike and there are enough characters. It is not guranteed to reconstruct the correct tree on additive matrices defining the true tree unless the true tree branch lengths obey the lexical clock.
   
**Drawback**: note however that datasets rarely meet these theoretical guarantees in real life, so they may not be that helpful.

### Simulation studies
* A model phylogony T (tree or network) is produced, along with the associatied parameters of evolution.
* Characters are evolved from the root of the phylogeny to the leaves, producing a set S of languages at the leaves of the phylogeny.
* The set S is given to a phylogeny estimation procedure, and a tree or network T' is produced by the analysis.
* The estimated phylogeny T' is compared to the true phylogeny T, and the error is computed.
* **Drawback**: the simulation study will be relevant to phylogeny estimation only to the extent that the simulation study is based on a sufficiently realistic model of language evolution.

## Recommended benchmark datasets
These are young families for which both dating and subgrouping are firm because of written evidence and/or historical records
* Germanic, Romance, and Slavic. Wikipedia has accurate trees for these, and Dyen et al (1992) includes lexical data for several languages of each of these branches. Grammatically and lexically divergent but recently formed creoles in Germanic and Romance provide well-known acid tests for methods of subgrouping and especially dating. Germanic also has extremely conservative Icelandic and extremely innovative (Romance-influenced) English as milder **acid tests**.
* Common Turkic. These are well dated on historical grounds.
* Chinese (lexical data in the appendix to Minett and Wang 2003).
* Mixe-Zoque (see Cysouw et al. 2006, with bibliography on the history of subgrouping; lexical data in the appendix).

Older groups for which subgrouping is well understood and dating clear from archaeological evidence include:

* Austronesian. See Blust 1985, 1995 for the received view of the higher level structure of the tree. 
* Oceanic. Very firmly dated, and the wide distribution of a number of discrete subgroups is due to well-understood episodes of migration and colonisation. See Ross (1997) for subgrouping. That Austronesian, and especially its Oceanic subgroup, presents linguists, geneticists, and archeologists with a near-ideal natural laboratory because of the well-understood age and subgrouping, large number of daughter languages, and good number of well-understood complex sociolinguistic situations, has been mentioned a number of times, since the beginning of serious comparative work on the family; a recent such mention is Gray et al. (2007).
* Indo-European. Date and place of origin are very clear from archaeology (e.g. Anthony 2007). Major subgroups are well understood. Dyen et al (1992) provides lexical data coded for cognacy. The larger set of characters, including lexical as well as phonological and morphological ones, assembled by Don Ringe and Ann Taylor for 24 Indo-European languages for the papers by Ringe, Warnow, and their colleagues, is available at http://www.cs.rice.edu/~nakhleh/CPHL/datasets. These two databases for Indo-European differ in several ways: the Dyen et al. data are based upon modern languages, while the Ringe-Taylor data are based upon the earliest well-attested languages in each branch; furthermore, the Dyen et al. data have not been checked carefully with respect to cognate judgments, and it is likely that there are false positives (words noted as cognates that are not true cognates) in that database.
* Two other families with some uncertainties in their subgrouping but high-quality datasets available on-line are: (i) Bantu (sub-subgroup of Benue-Kwa, a subgroup of the large and very old Niger-Congo, or Niger-Kordofanian, family); The Comparative Bantu On-line Dictionary has extensive lexical data (www.cbold.ddl.ish-lyon.cnrs.fr/); and (ii) Sino-Tibetan – a large and old family of which Chinese is one branch; The Sino-Tibetan Etymological Dictionary and Thesaurus has extensive lexical data (http://stedt.berkeley.edu).

## Comparing trees with benchmark trees (to assess accuracy)
**For regular trees:**
* the **Robinson-Foulds (RF) metric** (Robinson and Foulds 1981), is the standard measure when *both trees are binary (i.e., fully resolved)*. Here we consider each tree to be represented by the set of edges it contains, and each edge is defined by the way it splits the set of leaves into two parts. The RF metric measures the difference between these two sets, normalized to produce a number between 0 and 1. Thus, if the normalized RF distance between trees T1 and T2 is 10%, then this asserts that 90% of the edges of the two trees define the same splits, and they differ only in 10% of their edges. RF rates above 10% are generally considered poor, but sometimes the data are such that better estimates are not really possible. 
* Some studies have separated out the RF error into two types of errors: false positives (edges that appear in the estimated tree but not in the true tree) and false negatives (edges that are in the true tree but not the estimated tree). These studies allow the two types of error to be distinguished. When both the estimated tree and the true tree are bifurcating, there will be equal numbers of both types of errors; however, as one or both of these trees can be incompletely resolved, distinguishing between the two types of errors can be quite informative. These error rates too are normalized by the number of edges in the respective trees, and error rates above 10% are considered poor. --> `the RF error rate is the error rate of the comparison between the trees (I think)`

**For networks**
When either tree has reticulations (which means it's a network, not a tree) it's harder to compare them. However, when the model phylogeny is a network representing borrowing between languages without any creolisation or koine formation, and the estimated phylogenies are all trees, it is possible to compare them.
* The model phylogenetic network has an underlying genetic tree on top of which there are borrowing edges. In this case, the estimated trees can be compared to the genetic tree using the standard RF criterion given above.
* If there is creolisation or koine formation involved in the network, we don't have the methods yet to handle it.

## Miscellaneous terminology
**lateral transfer**: =borrowing, horizontal transfer, copying
**reticulation**: when a descent tree or phylogeny has notable amounts of copying (borrowing).
**stock**: biology term for a language family.

## Dealing with borrowing, language contact
**Undetected borrowing** is a big issue when doing phylogeny, which can arise when:
1. Borrowing occurs between close sister languages before sound changes occur that identify the clades later descending from those sisters.
2. Borrowing postdates diagnostic sound changes, but the borrowed word happens not to contain any sounds that undergo the diagnostic changes 
3. `The word is an ideophone and avoids those diagnostic changes` 
4. The borrowing is reshaped to 'nativise' it, undoing or adding diagnostic changes. 

**Dealing with undetected borrowing**:
* Embleton (1986) estimates the extent of undetected borrowing from such things as the number of sisters of each language, the number of neighbors, and indices of similarity (based on typological properties) between the compared languages.
* Minett and Wang (2003) assume that recurrent non-cognate lexemes are due to borrowing and use statistics to evaluate the probability that characters evolve through borrowing by examining incompatibility patterns on MP trees.
* Nakhleh et al. (2005a) proposed a model of language evolution whereby all characters evolve without any homoplasy but potentially with borrowing and showed how to use it to analyze the Indo-European family.
* A mathematically formal parametric model of language evolution with these properties was proposed in Warnow et al. (2006).
* Hinnebusch’s method (1996) of detecting borrowing through lexical skewing was studied in Wang and Minett (2005) and shown to be a reliable indicator of borrowing.

The graphical models best suited to represent linguistic evolution in the presence of borrowing are phylogenetic **networks rather than trees**, but there are no standards for measuring amounts of reticulation and no averages for comparison. As a consequence, commentators differ in whether they consider a given phylogenetic network to be basically reticulate or basically tree-like.

## Distance measures; dating (absolute chronology)

Some phylogenetic methods (largely distance-based methods like NJ and UPGMA, but also maximum likelihood) produce trees that indicate not
only subgrouping but also branch lengths. The interpretation of these branch lengths depends on the model assumptions, but in most cases these
lengths correspond to the expected number of changes that should occur for a randomly selected character. When evolution is clocklike, however,
these also correspond to the elapsed time for that edge. Thus, the algorithmic techniques involved in glottochronology produce estimates of branch length and family ages, because they make the assumption that the evolution is clocklike.

## Statistical models of language evolution

**Stochastic process**: How a set of traits evolves within a family of languages. Each trait can assume several states, and changes between states will occur with some probability on each branch of the tree.

The probability with which the trait will change its state can depend on the branch, and also on the character, so *stochasitc processes need not assume all characters evolve identically, nor that a given character evolves identically on all branches of the tree.*

The stochastic process will make explicit statements about:
* **Independence of character evolution**--do changes in one character impact the probability of change for another character, or do they evolve independently?
* **Degree of homoplasy** (if you don't allow homoplasy then all state changes produce new states).
* **Amount of polymorphism** (both in terms of percentage of characters that exhibit it and the number of states that are permitted to simutaneously be present in one language for one character)--**polymorphism** is when a character exhibits two or more states in one language, i.e. uses two or more different cognates for a given meaning
* **Amount of borrowing** (both in terms of the number of contact events and the percentage of characters that evolve with borrowing)
* **Degree to which different characters are allowed to evolve differently.**

### Parametric model for binary (two-state) characters
* There is a tree with the leaves labeled by the set of languages.
* You put into the model (for each character) the probability for the root to exhibit the cognate (i.e. to have the character state of 1), and substitution probabilities for each edge of the tree, which indicate the probability that the character will change its state on the edge.
* The character thus evolves down the tree and would assign states (either 0 or 1) to each node of the tree. A change on an edge from 0->1 indicates the appearance of the cognate (but not whether it is the first appearance or a reapparance), and a change from state 1->0 indicates the loss of the cognate. 
* Note that if a character changes twice on some path, then it will begin and end in the same state; thus, this model allows homoplastic events. Constraints on the model to prohibit homoplastic changes can be made, however. 
* Also note that in this model all characters are supposed to evolve under the same process (you don't have separate parameters for separate characters). However, in some cases some additional variation between characters is enabled--but is constrained so as to be able to be represented by just one additional parameter for the entire set of characters (i.e, the characters draw a rate of evolution from a distribution which can be described by that single parameter). 
* Multistate characters can be modelled in essentially the same way--however, you need to specify if the number of states is bounded (e.g. by saying that there are only four possible states, and all substitutions are between these for states) or unbounded (with an infinite number of possible states). Here too, homoplasy can be allowed or prohibited. 
* The tree and the values for the various parameters define the probability of any given set of sequences at the leaves of the tree. The **maximum likelihood estimation method** would try to `find the tree and parameter values that are most likely to produce the input sequences.`
* Examples: Gray and Atkinson on Indo-European w/ a Bayesian analysis is the original application of this model, The homoplasy-free version of the multistate character model has been used for simulation purposes in several studies (see, for example, Minett and Wang 2003; McMahon and McMahon 2005; Wang and Minett 2005). Extensions of these models to allow for borrowing have also been considered, with homoplasy-free versions studied by McMahon and McMahon (2005), Minett and Wang (2003), Wang and Minett (2005), and more generally by Warnow et al. (2006) (who proposed a parametric model allowing homoplasy) and Barbançon et al. (forthcoming) (who performed a simulation study under the Warnow et al. 2006 model).

The choice of characters used in phylogenetic analysis is of great importance, and has been one of the main issues involved in critiquing a phylogenetic analysis: `which characters did the authors use, and what are the consequences of that choice?`



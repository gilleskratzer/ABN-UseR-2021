
# Frequently asked question from the UseR! Conference workshop.

Please find some responses below:

* What are the differences between ABNs and bSEMs?

A closely related methodology is Structural Equation Modeling (SEM) (21). SEM includes different methodologies, such as confirmatory factor analysis, path analysis, partial least squares path modeling, and latent growth modeling. Although they share the same purpose, SEM and BN methodologies have significant differences (22). SEM uses a causal approach based on cause-and-effect thinking, whereas BN is based on a probabilistic approach. SEM is well-suited to latent variable modeling (i.e., variables that are not directly observed but are modeled from others), which is not possible in the BN methodology. This is often the primary motivation for using SEM. A BN model can take advantage of new data, whereas SEM cannot. (see this [paper](https://www.frontiersin.org/articles/10.3389/fvets.2020.00073/full) for a deeper discussion)

* Could you please explain the rational behind the selection of a prior? 

ABN relies on priors at different levels. In the structure learning phase, one needs to decide on a structural prior, which encodes how likely a given structure is. In ABN, a form of prior is used that assumes that the prior probabilities for a set of parents comprising the same number of parents are all equal. It favors parents sets with either a very low or very high number of parents, which may not be appropriate. Alternatively, an uninformative prior is used where parent combinations of all cardinalities are equally likely. When using the Bayesian implementation during the model parameters learning phase, priors are used for estimation. Those priors are designed to be uninformative. (see this [paper](https://www.frontiersin.org/articles/10.3389/fvets.2020.00073/full) for a deeper discussion)

* How does one decide on the inputs for mcmcabn? (mcmc.scheme, prob.rev, etc) ? Were values for num searches and max steps decided arbitrarily? do you update after running hill climber and seeing the diagnostic plot?

Please see this [vignette](https://www.math.uzh.ch/pages/mcmcabn/articles/mcmcabn.html) for more details about mcmcabn.

* Concerning the advanced ABN and the prevalence of each arc, how to present results when the same arc is reversed in different competing DAGs?

The output could be on signed arc (direction count) or unsigned graphs (no direction). This is a modelling choice.

* Do you always have to tune for max number of parents in that way, by exploring different possible values? Is there any risk that this is not computationally feasible? Should one start from a small number or a big one when tuning?

This is just to protect from heavy computations. We start with low complexity (i.e. low number of parents), check the mlik graph and potentially increase the maximum number of parents. It is possible to specify the number of parents for individual nodes.

* In our example, a limit on parents is selected to be 4. In the diagram, there is very little improvement from a 2 parent limit to a 4 parent limit. If we were to run this again using a 2 parent limit, what measure would we use to compare the resulting 2 parent graph to the 4 parent graph?

There is a function called 'abn::compareDag()' design exactly to compare two graphs. This function returns multiple metrics. 

* What are the limitations of using the additive bayesian network approach?

This is a very large questions, multiple directions of possible response are highlighted below:

1. One critical limitation of the scoring approach is that many different networks can have the same score. A score function that computes the same score to equivalent networks is said to be score-equivalent. (The BDeu is the only BD score-equivalent.) BDs are only asymptotically score- equivalent. One promising point is that BIC is also asymptotically score-equivalent for discrete BNs. In a causal perspective, i.e., when arc direction matters, equivalent scores are preferred.


2. A strong limitation of the ABN method is the fact that it does not model any interactions present in the data as it assumes additivity of the effect of parents on the link function scale. This is such strong assumption that it is explicitly written in the name of the method. There are some preliminary attempts to include statistical interactions in an ABN model as proxy for biological interactions from the data. Indeed, statistical interactions do not necessarily overlap with biological interactions(Greenland, 2009). Much care should be taken when considering statistical interactions, as in a fully automated method that requires to estimate a large amount of models, adding blindly interaction terms will augment massively the computation time. Hence, the only viable solution is some post processing adjustment of the model driven by prior field- specific knowledge. In a parametric bootstrapping step, this limitation could, however, becomes very problematic as it could simplify the complexity of the data and discard important data specificity when the purpose was originally to prune the model in keeping all important data features.

3. The additivity assumption is dependant on the link function used for each model. Indeed, the effect of parents could be additive on a certain scale and not on another. abn is very restrictive on this point in allowing only default link functions for the GLMs. The major challenge is to produce esti- mates that are biologically interpretable and to find optimal scale for the effect of the covariate. Further research is needed to identify methods to optimally select node specific link function for an ABN model.

* What are your next steps in the development of the abn package.

We do not have a plan set up yet.

* There are a couple of other r packages that do bayesian structural equation modelling, such as blavaan, bsem, etc. Do you have a comprehensive list on those and their pros and cons?

No. However, this [paper](https://arxiv.org/abs/1911.09006) discuss some alternative to ABN

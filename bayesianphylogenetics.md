---
inmenu: 0
layout: page
title: Bayesian Phylogenetics (1996-present)
permalink: /bayesianphylogenetics/
---
# Introduction
During the period from 1996 to 2000 I coauthored 2 papers (with Ziheng Yang) and authored another paper myself on the topic of [Bayesian phylogenetic inference](https://en.wikipedia.org/wiki/Bayesian_inference_in_phylogeny). This work began shortly after Ziheng Yang and I arrived as postdocs in Monty Slatkin's lab at UC Berkeley in the fall of 1995. My personal interest in Bayesian phylogenetic inference was driven mainly by the possibilities it allowed for dealing with phylogenetic uncertainty in a systematic way. I cannot speak for Ziheng with regard to his motivations.  That Bayesian inference offered an alternative approach to likelihood for parametric  inference in phylogenetics was very obvious by the 1990s. Indeed, ideas for both Bayesian and likelihood inference of phylogeny were widely explored in the 1960s and 1970s, although limited sequence data were available. I won't go into that history here but will instead just mention a paper by A.W.F. Edwards that influenced my thoughts on the problem.

In an early paper, A.W.F Edwards ([Edwards, 1970](https://www.jstor.org/stable/pdf/2984523.pdf)) developed an elegant model for gene frequency evolution on a population or species tree that included a prior for the tree based on a Yule (pure birth) model (although he did not describe it as such). Although Edwards outlined the basic model, he made little progress in deriving estimators for inferring the model parameters. Edwards pursued a likelihood approach to phylogenetic inference and was firmly opposed to the notion of applying Bayesian inference in this context:
 >It will be sufficient to state here my belief that,
 >however much a Bayesian solution would have simplified the approach to this problem
 >(by calling everything a conditional probability), it would be most improper for a
 >scientist to compromise his convictions by resorting to the most expedient approach
 >to inference for the problem at hand; and a detailed study of the present problem has,
 >if anything, strengthened my conviction that a Bayesian approach in this instance
 >would be a gross over-simplification. I am not prepared to give the true parameters
 >prior probability distributions because I can see no model which would justify them.
 
Bayesian phylogenetic inference appeared to us to potentially offer expedient solutions to several outstanding problems in the field. 
We therefore pursued a line of research focusing on the development of Bayesian phylogenetic inference methods
that resulted in the following papers. Because the debate between Bayesians and non-Bayesians lingers on (though in a somewhat attenuated form) I
feel I should clarify my personal views on statistical inference. I don't consider myself a Bayesian. I am happy to use any of the established approaches for inference
if they produce sensible estimators and are computationally efficient for the problem at hand.
My opinion is that priors in the field of phylogenetics will often be uninformed and it is thus important to insure that arbitrary choices of priors are not driving
outcomes and unduly influencing conclusions. The extreme example of this is a model with parameters that are non-identifiable. In that
case, the posterior distribution of those parameters will be completely determined by the (often arbitrary) prior. Developers and users of
Bayesian software should be wary of such situations. The problem of identifiability in Bayesian phylogenetic inference was the subject of
Rannala (2002).

I have coauthored several additional papers (after 2002) that focus on resolving specific problems that
have arisen in Bayesian phylogenetic inference over the years as the field has matured. Several of those papers are included here.
However, papers that apply Bayesian ideas to specific fields of inquiry (e.g., species tree inference, divergence time estimation) are included elsewhere.

# The papers

***

>[1] B. Rannala and Z. Yang. 1996. Probability distribution of molecular evolutionary trees: a new method of phylogenetic inference. Journal of Molecular Evolution 43: 304-311.
[Download](http://www.rannala.org/reprints/1996/Rannala1996a.pdf)

***

>[2] Z. Yang and B. Rannala. 1997. Bayesian phylogenetic inference using DNA sequences: a Markov Chain Monte Carlo method.
Molecular Biology and Evolution 14: 717-724. [Download](http://www.rannala.org/reprints/1997/Yang1997.pdf)


***

>[3] B. Rannala. 2002. Identifiability of parameters in MCMC Bayesian inference of phylogeny. Systematic Biology 51: 754-760.
[Download](http://www.rannala.org/reprints/2002/Rannala2002.pdf)

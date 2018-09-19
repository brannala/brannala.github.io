---
inmenu: 0
layout: page
title: Allele Age Inference (1997-2003)
permalink: /alleleages/
---
# Introduction
During the period from 1997 to 2003 I coauthored 5 papers on the topic of inferring [allele age](https://en.wikipedia.org/wiki/Allele_age) using linked genetic markers. 
Three of these papers present new theory and methods for inferring allele ages [1,2,3] and two are review articles [4,5]. The age of an allele refers to
the time in the past at which the mutation occurred that first created the allele. Obviously the notion of age is only meaningful when applied to a 
unique non-recurrent mutation. The concept of allele age goes back to the earliest days of
population genetics and lots of theoretical work during the 1970s focused on the relationship between the population frequency of an allele and its
age [4].
The methods used in the papers presented here use an additional source of information, the
so-called ``intra-allelic variability.'' The
basic principle underlying these methods is that a novel allele arises by [mutation](https://en.wikipedia.org/wiki/Mutation) on a particular chromosome at some time in the past
and is initially associated with a set of alleles at nearby [genetic markers](https://en.wikipedia.org/wiki/Genetic_marker). Thus, there is a characteristic [haplotype](https://en.wikipedia.org/wiki/Haplotype) associated with the allele. If the allele persists in the population then subsequent mutation and [recombination](https://en.wikipedia.org/wiki/Genetic_recombination) events in the descendent chromosomes can modify the surrounding markers. These modifications at nearby sites (intra-allelic variants) then carry potential information about the age of the mutation. 

The possibilities for using intra-allelic variation to estimate allele ages expanded explosively with the development of the [PCR](https://en.wikipedia.org/wiki/Polymerase_chain_reaction) method for targetted DNA amplification during the 1990s. This development came shortly after the first successful attempts to map and sequence the specific gene mutations causing simple Mendelian diseases in humans by [positional cloning](https://en.wikipedia.org/wiki/Genetic_screen#Positional_cloning) during the late 1980s and early 1990s. One of the earliest applications of intra-allelic variation to estimate allele age was the paper by Serre at al (1990); they used the RFLP variation flanking a common mutation in the CFTR gene causing cystic fibrosis to estimate the age of the mutation based on a simple method of moments estimator. Their age inference method inspired the series of coauthored papers presented here. 

If an allele is rare it can be approximated using a [birth-death (BD) process](https://en.wikipedia.org/wiki/Birth%E2%80%93death_process) model, similar to the way that R.A. Fisher approximated the dynamics of a rare allele using the closely-related [Galton-Watson branching process](https://en.wikipedia.org/wiki/Galton%E2%80%93Watson_process). The practical importance of this insight is that an appropriately parameterized BD process can be used to obtain the probability distribution of gene trees and branch lengths for a sample of individuals carrying a particular allele, even when the allele is under selection or the population is undergoing exponential growth. 
Given the probability distribution for the allelic genealogy (tree topology and branch lengths of the gene tree for the allele) it is possible to construct a parametric method for inferring allele age. If the allele arose by mutation at time *t* in the past the probability distribution of the number of copies *i* of the allele in a sample follows a geometric distribution; a maximum likelihood estimator is
derived in explicit form (equation 8 of [1]). The papers discussed below all employ the BD approximation for the intraallelic genealogy but make different assumptions about mutation and recombination
with the goal of estimating allele age using information from intraallelic variability.

# The papers

***

>[1] Slatkin, M., and B. Rannala. 1997. Estimating the age of alleles by use of intraallelic variability. American Journal of Human Genetics 60: 447-458. [Download](http://www.rannala.org/reprints/1997/SlatkinRannala1997.pdf)

In this paper, a numerical method for obtaining a maximum likelihood estimate of allele age using both the
frequency and the intra-allelic variation is developed. Here intra-allelic variation is measured by the number of segregating sites assuming a [infinite alleles model](https://en.wikipedia.org/wiki/Infinite_alleles_model) of mutation for completely linked markers (each mutation is unique and creates a new haplotype). 
This model is at one extreme in terms of the assumptions: relatively high mutation rates producing novel alleles at linked variants (such as [microsatellites](https://en.wikipedia.org/wiki/Microsatellite)) that are very close to the allele locus and do not undergo recombination. The model is
best suited for analyzing, for example, microsatellite markers that are closely linked to an allele locus. Under this
model the expected number of mutations follows a Poisson distribution with expectation and variance *u T* where *T* is the sum of the branch lengths on the genealogy and *u* is the overall rate of mutation for the region surrounding the allele locus. There is no analytical expression for the probability density of *T* and [Monte Carlo](https://en.wikipedia.org/wiki/Monte_Carlo_method) simulations were therefore used to evaluate the likelihood and obtain a [maximum likelihood](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation) estimate of the allele age.

***

>[2] Rannala, B., and M. Slatkin. 1998. Likelihood analysis of disequilibrium gene mapping and related problems. American Journal of Human Genetics 62: 459-473. [Download](http://www.rannala.org/reprints/1998/Rannala1998c.pdf)

The method developed in this paper uses the same BD approximation for the intra-allelic genealogy but considers a single linked locus with recurrent mutation between only two allele types and recombination
on the interval between the allele locus and the marker. A maximum likelihood estimator of allele age is again developed using Monte Carlo simulations. This method is most appropriate for markers with
few alleles (low mutation rates) such as [single nucleotide polymorphisms](https://en.wikipedia.org/wiki/Single-nucleotide_polymorphism) (SNPs) but sufficiently far from the allele locus that multiple recombination events occur over the intraallelic genealogy.

***

>[3] B. Rannala and J.P. Reeve. 2003. Joint Bayesian estimation of mutation location and age using linkage disequilibrium. Pacific Symposium on Biocomputing 8:526-534. [Download](http://www.rannala.org/reprints/2003/Rannala2003b.pdf)

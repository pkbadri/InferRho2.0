# InferRho2.0

InferRho is a MCMC based program for jointly estimating the crossing-over and gene-conversion parameters from population genomic datasets under a Bayesian framework. It uses a full-likelihood method to infer the posterior distribution of recombination rates along the sequence under a variable recombination rate model assuming that the ratio of gene- conversion to crossing-over rate ( f ) is uniform along the sequence. The program assumes a prior distribution for background recombination rates and hotspots. The starts, ends and intensities of hotspots are also output by the program in the posterior distribution generated by the MCMC chain.

References
Wang, Y., and B. Rannala, 2008 Bayesian inference of fine-scale recombination rates using population genomic data. Philos. Trans. R. Soc. B
Wang, Y., and B. Rannala, 2009 Population genomic inference of recombination rates and hotspots. Proc. Natl. Acad. Sci. USA
Badri Padhukasahasram and Bruce Rannala 2011 Bayesian population genomic inference of crossing-over and gene-conversion. Genetics
Badri Padhukasahasram and Bruce Rannala 2013 Meiotic gene-conversion rate and tract  length variation in the human genome. EJHG


Input File Format


1

h

10

15

A T T C C G A C G G A G A C A

T A G C G G C C G C A A A C T

A T T C G G A T G C A A A C A

A T G C C G C C G C A A A C A

A A G C C G C T C C A G C C A

A T T C C G A T G C C G C A T

A A G C C G C T C C A G C C A

A T G C G A A T G C C G C A T

T A G C G G C C G C A G C C T

A A G C G G C C G C A G C C T

1530 1607 2123 2695 2937 3859 5148 6017 6335 6568 6693 6705 7769 8206 9285




The input file has to be in the following format:

Line 1: Should always be 1.

Line 2: Character ‘h’ or ‘g’ to denote haplotype or genotype data respectively.

Line 3: Blank.

Line 4: Number of Individuals in the sample.

Lines 5: Number of Markers in the sample.

For haplotype data, each subsequent line represents the haplotype of an individual in the sample.
For genotype data, consecutive 2 lines represent a single individual with each base of a genotyped marker in each line corresponding to the marker location.
The bases at different marker positions should be separated by spaces. “N” must be used for denoting missing data at a base position.

Last line: Positions of markers in the sample separated by spaces.
We also suggest omitting SNPs with minor allele frequency < 10% from your data and applying the program to short windows in your dataset (e.g. 5-7 kb).

Command Line Options

IRv1 – Inference of Recombination Rates and Hotspots version: 1.0.0

Type Make to compile the program from the Makefile.

Usage: ./IRv1   inputfile    [options]

Options:

-burnin n Number of burnin iterations. Default is 20000.

-iter n Number of iterations. Default is 100000.

-thin n Thinning iterations. Default is 10. (This means we sample after every 10 iterations of the chains).

-dTheta x Mixing parameter for the mutation parameter theta. Default is 0.2.

-dRho x Mixing parameter for background recombination rate. Default is 100.

-dScale x Mixing parameter for background recombination rate. Default is 0.1.

-nChains n Number of chains. Default is 5.

-temp x Temperature of chains. Default is 1.05.

-seed x Seed. Default seed is set based on system time.

For example you can type on the command line:

./IRv1 input.txt -burnin 20000 -iter 100000 -thin 10 -dTheta 0.2 -dRho 100 -dScale 0.1 -nChains 5 -temp 1.05 -seed 10

Output Files

There are many output files generated by the program.

*.log: Contains the parameters with which the chain was run.

*.rho: Contains the values of f and {crossing-over rate, gene-conversion rate, mean tract length, theta} between adjacent markers along the chain.

*.hotsp: Contains the starts, ends and the intensity of hotspots along the chain.

*.rhoBackg: Contains the value of background crossing-over rates between markers at different steps in the chain.

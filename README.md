TriPoly, version 1.5, Ehsan Motazedi (ehsan.motazedi@gmail.com), last modified: March 28 2018

Introduction
============

**TriPoly** \(executable *main.py*\) is an efficient tool for haplotype estimation in polyploid F1 populations with two parents and one or several offspring, using next generation sequence reads. The method considers each offspring with the parents as a trio and tries to simultaneously maximize the likelihood of all of the trio haplotypes in the population, using a Bayesian framework that incorporates sequence data and recombination probability in the likelihood function. It can handle multi-allelic markers and discontinuous haplotype blocks.

The main parameters of the algorithm: variant calling error, recombination probability between adjacent markers, &#964;, branching threshold, &#961;, and pruning rate, &#954;, \(*Motazedi et al.* 2017\) can be passed as optional arguments to TriPoly. TriPoly accepts a multi-sample BAM file (assuming the first two sample names are that of the parents and the rest of the progeny), from which the so-called SNP-fragment matrix is constructed for haplotype estimation. To build this matrix from the sequence reads, the minimum acceptable mapping quality and base quality scores, as well as the maixmum acceptable insert-size to consider the reads as paired, could be passed as parameters. 


An extra option: -*a*, --*aggressive* has also been provided to specify an aggressive pruning rate, &#945;, so that at each step, (100&#215;&#945;)%; of the candidate extensions are pruned if the original pruning scheme is unable to rule-out at least (100&#215;&#945;)% of these extensions. Setting a high &#945; can greatly increase the speed of the algorithm. Finally, a warm-up length in base-pairs could be set along which, from the start of a haplotype block, no branching or pruning is performed. With --nogen option, it is also possible to estimate the haplotypes from the reads without restricting the dosages to those detected in the VCF file. 


By default, TriPoly reports all of the haplotypes that have survived the successive pruning steps, together with their relative likelihoods. The command line option -t, --top changes this behavior to report only the most likely haplotype (or a random haplotype if several haplotypes have a likelihood equal to the maximum).

TriPoly is written in *Python* and is compatible with both Python 2 and Python 3.



Citation:
=====================

To cite TriPoly, please refer to *TriPoly: a haplotype estimation approach for polyploids using sequencing data of related individuals*, Ehsan Motazedi, Dick de Ridder, Richard Finkers and Chris Maliepaard, 2017, bioRxiv 163162; *doi: https://doi.org/10.1101/163162*


Input parameters:
=====================

For the input parameters, see the help of the software:

./main.py --help, -h

***Example:***


./main.py bamfile vcffile output_dirname --kappa 0.85 -a 0.8 --rho 0.2 --top


Download:
=====================
The software is available at gitlab, Wageningen UR:

git clone git@git.wageningenur.nl:motaz001/TriPoly.git —recursive

Copyright and License:
=====================
Copyright (c) 2017, Ehsan Motazedi, Wageningen UR.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files \(the "Software"\), to deal in the Software without restriction, including without limitation the rights to use, copy, share and modify the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software. This permission is only valid for academic and personal use, i.e. not for commercial purposes.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

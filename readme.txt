STREAM VARIATIONAL BAYES FOR LATENT DIRICHLET ALLOCATION

Stream LDA implements a version of the LDA algorithm such that a continuous
stream of documents can be passed in. The classifier will continue to learn
new words and refine the topics over time, while maintaining a constant bound
on memory requirements. 

Original implementation by Matthew D. Hoffman (mdhoffma@cs.princeton.edu), (C)
Copyright 2009, Matthew D. Hoffman

Extensions by Jessy Cowan-Sharp (jessy.cowansharp@gmail.com) and Jordan
Boyd-Grader (jbg@umiacs.umd.edu)

------------------------------------------------------------------------

This is free software, you can redistribute it and/or modify it under
the terms of the GNU General Public License.

The GNU General Public License does not permit this software to be
redistributed in proprietary programs.

This software is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307
USA

------------------------------------------------------------------------

This Python code is based on the implementation of the online Variational Bayes
(VB) algorithm presented in the paper "Online Learning for Latent Dirichlet
Allocation" by Matthew D. Hoffman, David M. Blei, and Francis Bach,
to be presented at NIPS 2010. It has been extended to support arbitrary streams
of documents without constraining the vocabulary or requiring knowledge of the
total number of predicted documents. 

The algorithm uses stochastic optimization to maximize the variational
objective function for the Latent Dirichlet Allocation (LDA) topic model.
It only looks at a subset of the total corpus of documents each
iteration, and thereby is able to find a locally optimal setting of
the variational posterior over the topics more quickly than a batch
VB algorithm could for large corpora.


Files provided:
* streamlda.py: A package of functions for fitting LDA using stochastic
    optimization.
* dirichlet_words.py: A class to represent the evolving vocabulary as
    probability distributions over words and topics. Provides backoff estimates
    of unseen words. 
* stream_corpus.py: Applies streamLDA to test data, currently either 20 
    newsgroups or wikipedia. The wikipedia option downloads and analyzes
    a bunch of random Wikipedia articles using online VB for LDA. This 
    is nice for breadth of examples, but is not precisely repeatable 
    since the articles are random. 20 newsgroups provides data on which
    a repeatable run can be performed.
* twenty_news.py: A package of functions for processing a set of local
    data.
* wikirandom.py: A package of functions for downloading randomly chosen
    Wikipedia articles. 
* documentation.txt: More detailed commentary and implementation details. 
* readme.txt: This file.
* LICENSE: A copy of the GNU public license version 3.


Dependencies:
* numpy 
* scipy
* nltk


Example:
python stream_corpus.py wikipedia 101

This would run the algorithm for 101 iterations, and display the
(expected value under the variational posterior of the) topics fit by
the algorithm. (Note that the algorithm will not have fully converged
after 101 iterations---this is just to give an idea of how to use the
code.)

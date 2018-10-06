---
layout: single
title: PageRank 
excerpt: ""
header:
  overlay_color: "#333"
  
  teaser: /assets/images/google-logo.png
#date:   2015-11-17 16:16:01 -0600


---


In simple terms Page Rank is an intutive way of ranking web pages. Which formed the basis for Google's web indexing algorithm. Belive it or not Page Rank is very intutive algorithm. Which I will be explaing in this post. The challenging part about Page Rank is the scaling. But that isn't what this post is about. 

In this post I will be covering the following:
+ Basic Idea behind Page Rank 
+ Understanding the Pank Rank algorithm
+ Implementing Page Rank from scratch 

## Basic Idea behind Page Rank
The intutution behind the Page-Rank is based on the idea that popularity of a webpage is determined not only the number of incoming links but also by the kind on incomings links. Link from highly rank pages contribute more than lower rank webpages. In the end the page rank of the webpage is determined by the equation:
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">

\begin{equation}
 PR(A)=(1-d)+ d* P(B,A)*PR(B) 
\end{equation}

<p align="center">
 PR(A) : PageRank of Page A <br />
 PR(B) : PageRank of Page B <br />
 P(B,A): Probability going from B to A <br />
 d : is known as Damping factor, to add some randomness to the equation. 
</p>
## Page Rank Algorithm 
To understand how page is implement over the web graph, consider a graph of webpages having links shown by the arrow. Note if there are web pages with no out link then the do not contribute to the page ranking.
<p align='center'>
<img src="/assets/images/pg.png"></p>
Initially page rank of all the web pages is fixed to 1 and over an interative process the algorithm converges and page rank of each page is determined. Expressing the web graph in terms of probabilities we get a weighted graph.
<p align='center'>
<img src="/assets/images/Artboard.png"></p>
Weight of the edge is the probability of going from a web page X to Y ( The web page A has 2 out links therefore probability to go a single web page is 1/2 ). After expressing the web graph in terms of probabilities, the page rank of each web page can determined by applying the PageRank equation. This process is repeated until the algorithm converges i.e. the values of page rank do change beyond an small value ( know as epsilon usually fixed as 1e-4 ). The damping factor introduced to add randomness over the web graph is usually taken as 0.85. <br />
<br />
The interative process can also be expressed in terms of matrix operations. Where matrix C represents the probability transition graph ( C[i][j] = probability of the user transitioning from page i to page j ). The page rank equation is now expressed using dot products as:
\begin{equation}
 PR=(1-d)+ d* C^T.PR 
\end{equation}
The C matrix of our example can be expressed as the matrix represented below. Also the intial page ranks are assinged 1 for all the web pages.
<p align='center'>
<img src="/assets/images/matrix.png"></p>
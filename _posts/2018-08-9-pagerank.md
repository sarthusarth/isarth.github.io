---
layout: single
title: PageRank 
excerpt: "Indexing the web pages"
header:
  overlay_color: "#333"
  
  teaser: /assets/images/google-logo.png
#date:   2015-11-17 16:16:01 -0600


---


In simple terms, PageRank is an intuitive way of ranking web pages, which formed the basis for google's web indexing algorithm during its early phase. Believe it or not Page Rank is a very intuitive algorithm. In this article, you'll learn about the ituition behind page rank and implementing page rank in python. The article is divided into following sections:

+ Basic Idea behind Page Rank 
+ Understanding the Pank Rank algorithm
+ Implementing Page Rank from scratch 

## Basic Idea behind Page Rank
The intuition behind the Page-Rank is based on the idea that popularity of a webpage is determined not only the number of incoming links but also by the kind on incomings links. Citations from highly ranked pages contribute more than lower ranked web pages. The page rank of a web page A cited by web page B shown in Fig. 1 is given the equation:
<p align='center'>
<img src="/assets/images/Page_rank/ex.png">
<figcaption align='center'>Fig.1 Example of web graph.</figcaption>
</p>

<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
\begin{equation}
 PR(A)=(1-d)+ d* P(B,A)*PR(B) 
\end{equation}

<p align="left">
 PR(A) : PageRank of Page A <br />
 PR(B) : PageRank of Page B <br />
 P(B,A): Probability going from B to A (here it is one)<br />
 d : is known as Damping factor, to add some randomness to the equation. 
</p>
Page rank over the complete web graph is calculated until it converges to final values.
## Page Rank Algorithm 
To have a better understanding how page rank works, consider a graph (shown by Fig. 2) of webpages having links shown by the arrow. Note if there are web pages with no out link then the do not contribute to the page ranking (they are usually refered as dangling pages).
<p align='center'>
<img src="/assets/images/Page_rank/graph.png">
<figcaption align='center'>Fig.2</figcaption>
</p>
Initially page rank of all the web pages is taken as 1. Weight of the edge is the probability of going from a web page X to Y ( The web page A has 2 out links therefore probability to go a single web page is 1/2 ). After expressing the web graph in terms of probabilities the web graph looks something like shown in the Fig.3. The page rank of each web page is determined by applying the PageRank equation. This process is repeated until the algorithm converges i.e. the values of page rank do change beyond an small value ( know as epsilon usually fixed as 1e-4 ). The damping factor (d) introduced is to add some randomness over the web graph i.e. d is probability that a user will move to the linked web page and 1-d is the probablity of choosing a random web page, it is usually taken as 0.85.
<p align='center'>
<img src="/assets/images/Page_rank/graph_prob.png">
<figcaption align='center'>Fig.3</figcaption>
</p>
For iteration 1: <br />
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
 $$PR(C)=(1-d) + d*( P(A,C)*PR(A) + P(B,C)*PR(B) + P(D,C)*PR(D))$$
 <br />
 $$PR(C)=(0.15)+ 0.85*( 0.5*1 + 1*1 + 1*1) = 2.275$$
<br />
<br />
The PR(C) can also be calculated by matrix dot product. 
<p align='center'>
<img src="/assets/images/Page_rank/pr_c.png">
</p>
Similarly extendting this for all the web pages we end up with the equation:  <br />  ( * represents matrix multiplication)
<p align='center'>
<img src="/assets/images/Page_rank/eq.png">
</p>
<p align='center'>
<img src="/assets/images/page_rank/mat.png"></p>
\begin{equation}
 PR=(1-d)+ d* (C^T*PR) 
\end{equation}



Where matrix C represents the probability transition ( C[i][j] = probability of the user transitioning from page i to page j).
The C matrix of our example can be expressed as the matrix represented below. Also the intial page ranks are as assinged 1 for all the web pages. The PRs of web pages are calculated until the PRs converge to a certain value.

## Implementing Page Rank
Page Rank implementation in python:
```python
import numpy as np
def pagerank(C, eps=0.0001, d=0.85):
    P = np.ones(len(C)) 
    while True:
        P_ = np.ones(len(A)) * (1 - d) + d * C.T.dot(P)
        delta = abs(P_ - P).sum()
        if delta <= eps:
            return P_
        P = P_
p=pagerank(C)
#result
#p=[1.16, 0.644, 1.19, 0.15]
```
Final ranking of our example are C > A > B > D !

Notice: page rank of A is high even when it has only one incoming link.
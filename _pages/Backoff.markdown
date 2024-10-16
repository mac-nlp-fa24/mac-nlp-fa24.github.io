---
layout: post
title:  "Backoff in N-Gram LMs"
categories: Smoothing
---
In Homework 1, you are tasked with fitting a model using *real* backoff. J&M introduce the idea of backoff (substituting the extremely underspecified n-gram MLE probability estimates with the (likely less sparse) lower order estimates), but only provides the details of what they call **stupid backoff**, which gives up on the idea of having returning real probabilities and just returns the probability an MLE (n-1)-Gram model would return (if it's non-zero, of course --- if it is 0 we back off further. See the textbook for the details!). 

The reason the textbook gives up on returning real probabilities because, to keep it brief, making the math work out is *tricky*. This also happens to be why I ask you to implement it for real! Figure out how the math works, implement it, and then understand why no one wants to do this. The other reason I ask you to do this is because it acts as a good test of whether you understand some of the probabilistic reasoning behind N-Gram Modeling, which sounds less cruel. 

## Backing Off

Note that I will be intentionally terse with the idea behind backoff. Make sure you understand the discussion of backoff from the reading first!

So, the first key idea is that stupid backoff will fail to be a probability distribution because the conditional ``probability distribution'' estimated by the model will often sum to over $1$ --- Not a real probability distribution after all. Consider that if we consider only $n$-grams with count $>0$, we will have an MLE estimate of the probability distribution that will sum to 1. Recall that this estimate is...

$$\begin{aligned}
p(w_k \mid w_{k-n+1} \dots w_{k-1}) &= \frac{c(w_{k-n+1} \dots w_k)}{\sum_{w_k \in V}c(w_{k-n+1} \dots w_k)}  \\
\sum_{w_k \in V} p(w_k \mid w_{k-n+1} \dots w_{k-1}) &= \sum_{w_k \in V}\frac{c(w_{k-n+1} \dots w_k)}{\sum_{w_k \in V}c(w_{k-n+1} \dots w_k)} = 1
\end{aligned}$$

If we add any more probability to n-grams with $0$ counts, we'll have this sum go above 1! This is why stupid backoff does not allow us to have a real probability distribution.

Our solution in *real* backoff is to apply *discounting*: We'll take some probability from n-grams with non-zero probability in our MLE estimates and give that to those with 0 probability. How much we reserve will be a hyperparameter of our model. In the instructions, I suggest you discount the MLE estimates by a factor of $0 < \delta < 1$, and reserve $1 - \delta$ for unseen n-grams. Thus, we partition the sample space into two pieces: the probability of $w_k$s where we've seen the corresponding n-gram (that is, $w_k$ where $c(w_{k-n+1} \dots w_{k}) > 0$) and those which we haven't seen ($c(w_{k-n+1}\dots w_k) = 0$). For the ones we have seen, we use the MLE estimates above and just add the discount factor!

$$\begin{aligned}
p(w_k \mid w_{k-n+1} \dots w_{k-1}) &= \delta\frac{c(w_{k-n+1 \dots w_k})}{\sum_{w_k \in V}c(w_{k-n+1} \dots w_k)}  \\
\sum_{w_k \in V} p(w_k \mid w_{k-n+1} \dots w_{k-1}) &= \sum_{w_k \in V}\delta\frac{c(w_{k-n+1 \dots w_k})}{\sum_{w_k \in V}c(w_{k-n+1} \dots w_k)} = \delta
\end{aligned}$$

So we need the sum for all *unseen* $w_k$s to sum to $1-\delta$. There is a subtle trick here if you try and take too many shortcuts in assembling this equation though: You can't just take the MLE estimate of the (n-1)-gram model! Consider that the (n-1)-gram MLE model will have $\sum_{w_k \in V} p(w_k \mid w_{k-n+2} \dpts w_{k-1) = 1$, but we are only summing over $w_k$ *if* $c(w_{k-n+1} \dots w_{k-1}) = 0$. That means we might come in under $1$ when we sum over all $w_k \in V$ for our backoff model. 

The trick is to not try and be clever, and just work out the right probabilities from first principles: We want $\sum_{w_k \in V, c(w_{k-n+1} \dots w_{k-1}) = 0} p_{bo}(w_k \mid w_{k-n+2} \dots w_{k-1}) = 1$. We want each probability to be proportional to the (n-1)-gram count, so we also want $p_{bo}(w_k \mid w_{k-n+2} \dots w_{k-1}) = \alpha c(w_{k-n+2} \dots w_{k-1})$ for some $\alpha$. Now just do a little algebra to find $\alpha$:

$$\begin{aligned}
    \sum_{w_k \in V, c(w_{k-n+1} \dots w_{k}) = 0} \alpha c(w_{k-n+2} \dots w_{k-1}) &= 1 \\
    \alpha \sum_{w_k \in V, c(w_{k-n+1} \dots w_{k}) = 0} c(w_{k-n+2} \dots w_{k-1}) &= 1 \\
    \alpha &= \frac{1}{\sum_{w_k \in V, c(w_{k-n+1} \dots w_{k}) = 0} c(w_{k-n+2} \dots w_{k-1})} 
\end{aligned}$$

Now that's not a *nice* thing to compute, but this (typos aside --- let me know!) should give you a real conditional probabilitiy distribution. 

Now, you just need to incorporate multiple *stages* of backoff. What if the relevant (n-1)-gram has no observations, we should backoff even further! Discount the (n-1)-gram backoff estimate (so we weight $p_{bo}$ not by $(1-\delta)$, but by $\delta(1-\delta)$, reserving that last $(1-\delta)^2$ for the lower order ($1\dots(n-1)$-gram) backoff models. This is what the instructions are getting at when they give you the $\delta(1-\delta)^{m-1}$ figure! 

Good luck coding, and please come to OH or ask for help as you come closer to the deadline!

---
layout: post
title:  "Matrices for ML"
categories: 
---

Though this class does not require Linear Algebra as a pre-req, there are a few concepts in linear algebra that you'll need to be familiar with. My advice here is not to be intimidated --- while there are deep and interesting connections between the substance of linear algebra course and what we're doing, what I expect you to know is merely notation and terminology: I'll be using the words vector and matrix (and tensor), but you can replace those with various sorts of n-dimensional arrays of floating point numbers. The remainder of linear algebra content consists of two operations: the dot product and matrix multiplication. Luckily, these concepts, despite their importance, are straightforward notation for familiar operations. Their purpose, for us, is to save a couple of lines of text, and to present things in a language that allows for optimization via GPU.

### The Dot Product

You should be exceptionally familiar with the idea of a weighted sum. We have a number of things $x_1, \dots x_n$ and weights $w_1, \dots, w_n$, and we want to compute the sum of each thing multiplied by it's corresponding weight. Mathematically, we can write this as 

$$ \sum_{i=1}^n w_i \cdot x_i $$

You can also imagine writing this out in code as a single for-loop. In fact, sum/product notation translates pretty straightforwardly to a for-loop with an accumulator variable:

```python
out = 0
for i in range(n):
    out += w[i] * x[i]
```

The dot product simply presents a simple notation for this kind of weighted sum! We can bundle the $n$ values that are weights as $\vec{w}$ and the $n$ values that are the things being weighted as $\vec{x}$, we can say that

$$ \vec{w} \cdot \vec{x} = \sum_{i=1}^n w_i \cdot x_i $$

That's the dot product! It's also helpful to think about this as an *function*, particularly in the CS sense. This is a function that takes 2 vectors of equal length (i.e., 2 arrays of equal length) and returns a single float (what we call a *scalar* value. Thinking about these operations in terms of their function signatures allows us to think about *composing* functions together. If one operation in a neural network we build uses a dot product, we should be able to reason about whether the things we give as inputs are the right types and the output is the right type for the next step in the pipeline. 

### Matrix Multiplication

Unfortunately, writing out how a matrix multiplication works is both tedious and complex-looking (despite it's straightforwardness). To approach this in a more accessible way, we'll start with a special case: Matrix-Vector multiplication.

We typically notate matrices with capital letters like $M$. Here, I'm careful to represent vectors with an arrow like $\vec{v}$, but in general I will be fast and loose with this typically using $v$ or $w$ when context makes it clear that $v$ and $w$ are vectors. When in doubt, you should think about what makes sense in context --- does the math only work out when $v$ is a vector? Then assume it is! 

Given that notation, we depict matrix-vector multiplication like

$$ Mv = w $$ 

where $M$ is an $k$ x $l$ matrix that contains $m_{i,j}$ at row $i$ and column $j$. Multiplication is defined such that

$$ w_i = \sum_{j=1}^l m_{i, j} \cdot v_j $$

First, let's think about the dimensions. Note that I didn't mention what the lengths of the vectors were! That's because, for the summation to work, $v$ needs to have length $l$. Then note that $w$ must have the same length as $M$ (i.e., the number of rows in $M$, $k$)! This tells us that we can multiply a $k$ x $l$ matrix by a $l$-dim vector to get of vector of dimension $k$. Be aware that the term dimension will be used in a strange way: When referring to a vector, dimension refers to a vector's length. when referring to a tensor or array, dimension will refer to (essentially) the number of times you can index it. A 1-dimensional tensor is a vector, but that vector can be, say, 2-dimensional. Be careful!

Second, observe that this is just a nested for-loop in mathematical notation! An inner loop with index $j$ to compute each entry in $w$, and an outer for loop over $i$ to compute a value for every entry in $w$. 

```python
w = np.zeros(k)
for i in range(k):
    for j in range(l):
        w[i] += M[i][j] * v[j]
```

Third, observe that the inner for-loop is just a dot product between $v$ and the $i$th *row-vector* in $M$. If you think about matrices are 2D arrays, you can think about this as `dot(M[i], v)`, assuming row-major indexing for $M$. In this way, Matrix-Vector multiplication is just $k$ dot products in parallel, where the rows of $M$ represent the first vector and the second vector is fixed as $v$.

This gets us to Matrix-Matrix multiplication, which generalizes this further. Formally, you'll see it writted as 

$$ AB = C $$

for $l$ x $m$ A and $m$ x $n$ B where

$$ c_{i,j} = \sum_{k=1}^m a_{i, k} \cdot b_{k, j} $$

This should look familiar! This say's that the entry at index $i, j$ in C is the dot product between the $i$th row of $A$ and the $j$th column of $B$. You can represent this naively (there is a faster algorithm!) as a triply-nested for-loop: 2 outer loops over $i$ and $j$, finding an entry of $C$ to compute, and an inner for-loop to compute the relevant dot-product.

```python
C = np.zeros((l,n))
for i in range(l):
    for j in range(n):
        for k in range(m):
            C[i][j] = A[i][k] * B[k][j]
```

One deeply useful aspect of this being able to think through the dimensions necessary to make matrix muliplication work. The key observation is that the *inner dimensions must match*. An $n$ x $m$ matrix must be multiplied by an $m$ x $l$ matrix so the dot product we compute has two vectors of equal length! 

Again, there are a lot of cool, meaningful interpretations of these operations along with useful theory about matrices and the *linear transformations* they are equivalent to. However, for this class, you need only think about matrix operations as terminology and notation for doing these fancy weighted-sum computations.

### Matrix Operations for NLP

Let's take a look at where these show up for our purposes!

The most classic is the dot-product in something like a perceptron or logistic regression. The idea is that we're doing a *weighted-sum* over our features to compute a score for our input. For features $f_1, \dots f_n$ and weights $w_1, \dots w_n$, we compute

$$ s = \sum_{i=1}^n w_i \cdot f_i $$

which is typically written as a dot product, $\vec{w} \cdot \vec{f}$! This with a threshold is a perceptron, wrapped in a sigmoid becomes logistic regression. Again, the dot-product is not much more that a notational shorthand. 

Matrix vector multiplication is just the extension of this to the idea of a feedforward network. Remember that a feedforward network is simply a number of parallel logistic regression models organized into a leyer (with perhaps a different non-linearity), and so we are just applying the dot product to a number of different weight vectors to the same feature vector. This is exactly what matrix multiplication is --- parallel dot products of this form! Consider that a if we run $k$ logistic regressions in parallel, we can just index the equation above:

$$ s_i = \sum_{i=j}^n w_{i, j} \cdot f_i $$

and observe this fits our definition of matrix-vector multiplication above, so we can write it as 

$$ \vec{s} = W\vec{f} $$

Conceptually, it's just notation! Notation that let's us know what we're doing can be parallelized easily, and accelerated with a GPU! 

The one time a property from linear algebra is relevant is the one case the Matrix-Matrix multiplication is relevant: When stacking layers without non-linearities in-between:

If we apply no non-linearities after a layer in a neural-network (i.e., just stacking perceptrons), we can simplify the computation as something like

$$ W_2(W_1\vec{x}) $$

which can be re-written as 

$$ (W_2W_1)\vec{x} $$

Which we know will just result in a single more complex matrix, $C = W_2W_1$, multiplied by $\vec{x}$. This tells us that two layers without a non-linearity are equivalent to a single layer network with weights equal to the product of the two layers' weights. I.e., if we trained the single and 2 layer networks, we should theoretically be able to learn equivalent models. The same is *not* true if we place a non-linearity (ReLU, tanh, sigmoid, etc.) between the two layers!



# Fully differentiable deep neural decision forest

This is an implementation of a simple modification to the deep-neural decision
forest [Kontschieder et al.] usng TensorFlow. The modification allows the joint
optimization of decision nodes and leaf nodes which speeds up the training
(haven't compared yet).


## Motivation:

Deep Neural Deicision Forest, ICCV 2015, proposed a great way to incorporate a
neural network with a decision forest. During the optimization (training), the
terminal (leaf) node has to be updated after each epoch.

This alternative optimization scheme is usually slower than joint optimization
since other variable that is not being optimized slows down the optimization.

This code is just a proof-of-concept that

1. one can train both decision nodes and leaf nodes $\pi$ jointly using
parametric formulation of leaf node.

2. one can implement the idea in a symbolic math library very easily.


## Formulation

The leaf node probability can be parametrized using a $softmax(W_{leaf})$.
i.e. let a vector $W_{leaf} \in \mathbb{R}^N$ where N is the number of classes.

Then taking the soft max operation on W_{leaf} would give us

$$
softmax(W_{leaf}) = \frac{e^{-w_i}}{\sum_j e^{-w_j}}
$$

which is always in a simplex. Thus, without any constraint, we can parametrize
the leaf nodes and can compute the gradient of $L$ w.r.t $W_{leaf}$. This
allows us to jointly optimize both leaf nodes and decision nodes.


## Experiment

Test accuracy after each epoch

```
0 0.942307692308
1 0.968349358974
2 0.978966346154
3 0.983774038462
4 0.985276442308
5 0.987680288462
6 0.989282852564
7 0.988481570513
8 0.991185897436
9 0.99078525641
10 0.990885416667
11 0.990685096154
12 0.991987179487
13 0.991185897436
14 0.992387820513
15 0.99078525641
16 0.992287660256
17 0.992788461538
18 0.993088942308
19 0.99358974359
20 0.993289262821
21 0.992688301282
```

## References
[Kontschieder et al.] Deep Neural Decision Forests, ICCV 2015


## License

The MIT License (MIT)

Copyright (c) 2016 Christopher B. Choy (chrischoy@ai.stanford.edu)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.



+++
title = "Topic Bytt #2 - How entropy got its formula? (Part I)"
date = "2019-05-26"
markup = "md"
+++

Cross-entropy is a measure that pops up at many places within machine learning. 
So, we should be aware of the the connection between entropy (Information theory) and product-rule (Probability theory).

Let \\(X\\) be a discrete random variable and \\(x_1, x_2, ...,x_m\\) be the values (events) that \\(X\\) can take.

Let's look at a case of observing any \\(x_i\\).

We are told that the probability of observing \\(x_1\\) is \\(0.01\\). Whereas, other \\(x_j\\) have high probabilities
in the range \\([0.2, 0.5]\\). 

Assume we are in trial number \\(3\\). With the given information \\(p(x_1)\\), we expect that \\(x_1\\) might not be occuring. But to our surpise, it has occured.

\\(h(x)\\) is a function that is now brought into picture to handle such surprises (information gains).

Let's say such a surprise has occured for two independent events \\(X=x_1\\) and \\(X=x_2\\). So, total gain \\(h(x_1, x_2) = h(x_1) + h(x_2)\\). By product-rule, we know that \\(p(x_1, x_2) = p(x_1).p(x_2)\\).

As we might be knowing only \\(p(x_i, x_j)\\), we shall try to represent \\(h(x_i, x_j)\\) in terms of \\(p(x_i, x_j)\\).

Think of some function \\(f(x)\\) such that, \\(h(x_i, x_j) = f(p(x_i, x_j))\\).

Hint: \\(log_b(u.v) = log_b(u) + log_b(v)\\)

So, something like the following may be good,\\
\\(h(x_i, x_j) = log_b(p(x_i, x_j)) = log_b(p(x_i)) + log_b(p(x_j))\\). 

Now, we shall just consider a single event \\(x\\), \\(h(x) = log_b(p(x))\\).

Hold on, we know gains can be high when we observe a highly unlikely event like \\(x_1\\).
Does, current \\(h(x)\\) capture it?

\\(h(x_1) = log_b(0.01) = -2 \\), when \\(b=10\\)

A gain represented by a positive number could look neat. So, why not\\
\\(h(x) = - log_b(p(x))\\)?

It doesn't affect any of the preconditions. Thus, we have reached close to the actual formula of entropy.













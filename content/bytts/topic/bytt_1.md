+++
title = "Topic Bytt #1 - Derivatives for backpropagation in a simple Logistic Regression Network"
date = "2017-08-25"
markup = "md"
+++

Assuming the readers to be aware of a logistic regression model, where-in,

* \\( z = \boldsymbol w^T\boldsymbol x + b \\)
is the weighted sum of the input features, where, \\(\boldsymbol x\\) is the feature vector \\([x_1,x_2 ... x_n]\\), \\(\boldsymbol w\\) is the weight vector \\([w_1,w_2...w_n]\\) corresponding to the input features and \\(b\\) is the bias value.

* \\(\boldsymbol y\\) is the actual output vector and
\\( \hat{\boldsymbol y} = a = \sigma(\boldsymbol z) = {1 \over (1+e^{-\boldsymbol z})}\\) is the target output vector.

For simiplicity, we shall consider only one training example with two input features \\( x_1, x_2\\) and its corresponding weights \\( w_1, w_2 \\) along with the bias \\( b \\). Then,
\\( \mathcal{L}(a,y) = -( y\cdot log(a)) - ((1-y)\cdot log(1-a)) \\) would be the loss (or) error function.


_Change in the value of loss \\( (\mathcal{L}) \\) when the value \\(a\\) is changed can be represented as,_


<div>
$$
\eqalignno{
    {\partial \, \mathcal{L}(a,y) \over \partial a}
    &
    =
    - {\partial \, (y\cdot log(a)) \over \partial a}
    - {\partial \, ((1-y)\cdot log(1-a)) \over \partial a}
    &
    \longrightarrow
    &
    (1)
    \cr
}

$$
</div>

_Below are some of the formulas and notations which would be used in the calculation of derivatives,_

<div>
$$

\eqalignno{
    {d \over dx} \cdot f(x)
    &
    = f'(x)
    &
    \longrightarrow (a)
    \cr
    When\,f(x) = g(x)\cdot h(x),\, f'(x)
    &
    = g(x)\cdot h'(x) + g'(x)\cdot h(x)
    &
    \longrightarrow (b)
    \cr
    When\,f(x) = {g(x) \over h(x)}, \, f'(x)
    &
    =
    {{g'(x)\cdot h(x) - g(x)\cdot h'(x)} \over [h(x)]^2}
    &
    \longrightarrow (c)
    \cr
    When\,f(x) = g(h(x)),\, f'(x)
    &
    = g'(h(x))\cdot h'(x)
    &
    \longrightarrow (d)
    \cr
    When\,f(x) = log(x),\, f'(x)
    &
    = {1 \over x}
    &
    \longrightarrow (e)
    \cr
    When\,f(x) = e^x,\, f'(x)
    &
    = e^x
    &
    \longrightarrow (f)
    \cr
    When\,f(x) = a\cdot g(x),\, f'(x)
    &
    = a\cdot g'(x)
    &
    \longrightarrow (g)
    \cr
}

$$
</div>


_Now, let's come back to the calculation,_

<div>
$$
\eqalignno{
    {\partial \, (y\cdot log(a)) \over \partial a}
    &
    =y\cdot (log(a))' +(log(a))\cdot y'
    \cr
    &
    \,\,\,[\,by \, using \, (b)\,] \uparrow
    \cr
    &
    = y\cdot {1 \over a} + log(a)\cdot 0
    \cr
    &
    = {y \over a}
    &
    \longrightarrow
    &
    (2)
    \cr
    {\partial \, ((1-y).log(1-a)) \over \partial a}
    &
    =(1-y) \cdot (log(1-a))' + (1-y)' \cdot (log(1-a))
    \cr
    &
    \,\,\,[\,by \, using \, (b)\,] \uparrow
    \cr
    &
    =(1-y)\cdot {1 \over (1-a)} \cdot (1-a)' + 0\cdot log(1-a)
    \cr
    &
    \,\,\,[\,by \, using \, (d)\, and\,(e)\,] \uparrow
    \cr
    &
    =(1-y) \cdot {1 \over (1-a)} \cdot (0-1)
    \cr
    &
    =-{(1-y) \over (1-a)}
    &
    \longrightarrow
    &
    (3)
    \cr
}
$$
</div>

_Substituting (2) and (3) in (1),_

<div>
$$
\eqalignno{
    {\partial \, \mathcal{L}(a,y) \over \partial a}
    &
    =
    - {y \over a}
    - ({- {(1-y) \over (1-a)}})
    \cr
    &
    = - {y \over a} + {(1-y) \over (1-a)}
    &
    \longrightarrow (4)
    \cr
}
$$
</div>

_Change in the value of \\(a\\) when the value \\(z\\) is changed can be represented as,_

<div>
$$
\eqalignno{
    {da \over dz}
    &
    = { {d \over dz} \cdot {\sigma (z)} }
    &
    \longrightarrow (5)
    \cr
}
$$
</div>

_Solving (5),_

<div>
$$
\eqalignno{
    {da \over dz}
    &
    = { {d \over dz} \left( {1 \over (1+e^{-z}) } \right) }
    \cr
    &
    = { {(1)' \cdot (1+e^{-z}) - 1 \cdot (1+e^{-z})'} \over { (1+e^{-z})^2 } }
    \cr
    &
    \,\,\,[\,by \, using \, (c)\,] \uparrow
    \cr
    &
    = { {0 \cdot (1+e^{-z}) - 1 \cdot (0 - e^{-z})} \over { (1+e^{-z})^2} }
    \cr
    &
    \,\,\,[\,by \, using \, (d)\, and\,(f)\,] \uparrow
    \cr
    &
    \boxed{
        {d \over dx} \cdot e^{-x} = e^{-x} \cdot (-x)' = -e^{-x}
    }
    \cr
    &
    = - {(0 - e^{-z}) \over (1+e^{-z})^2}
    \cr
    &
    = { e^{-z} \over (1+e^{-z})^2 }
    \cr
    &
    = {1 \over (1+e^{-z})} \cdot { e^{-z} \over (1+e^{-z})}
    \cr
    &
    = a \cdot (1-a)
    &
    \longrightarrow (6)


}
$$
</div>

_Change in the value of loss \\( (\mathcal{L}) \\) when the value \\(z\\) is changed can be represented as,_

<div>
$$
{\partial \mathcal{L} \over \partial z} = {
    {\partial \mathcal{L} \over \partial a} \cdot
    {da \over dz}
} \longrightarrow (7)
$$
</div>

_Substituting (4) and (6) in (7) and solving it,_

<div>
$$
\eqalignno{
    {\partial \mathcal{L} \over \partial z}
    &
    = \left( {-{y \over a}} + {(1-y) \over (1-a)}  \right) \cdot a \cdot (1-a)
    \cr
    &
    = a-y
    &
    \longrightarrow (8)


}
$$
</div>

As we are considering only one training case with two features, the vectorized form \\( z = \boldsymbol w^T\boldsymbol x + b \\) can be expanded and written as
\\( z = w_1 \cdot x_1 + w_2 \cdot x_2 + b \\)


_Change in the value of \\(z\\) when the value \\(w\_1\\) is changed can be represented as,_

<div>
$$
\eqalignno{
    {dz \over dw_1}
    &
    = {d \over dw_1} \left( {w_1 \cdot x_1 + w_2 \cdot x_2 + b} \right)
    \cr
    &
    = x_1 \cdot 1 + 0 + 0
    \cr
    &
    \,\,\,[\,by \, using \, (g)\,] \uparrow
    \cr
    &
    = x_1
    &
    \longrightarrow (9)
    \cr
}
$$
</div>

_Change in the value of loss \\( (\mathcal{L}) \\) when the value \\(w\_1\\) is changed can be represented as,_


<div>
$$
\eqalignno{
    {\partial \mathcal{L} \over \partial w_1}
    &
    = {\partial \mathcal{L} \over \partial z} \cdot {dz \over dw_1}
    &
    \longrightarrow (10)
    \cr
}
$$
</div>


_Substituting (8) and (9) in (10),_

<div>
$$
\eqalignno{
    {\partial \mathcal{L} \over \partial w_1}
    &
    = (a-y) \cdot x_1
    &
    \longrightarrow (11)
}
$$
</div>

_Similar to (9) and (10), we can also calculate the change in the value of loss \\( (\mathcal{L}) \\) when the value \\(w\_2\\) is changed_

Thus, with the help of gradient values like \\( (11) \\) and the learning rate \\(\alpha \\), we can change the weights during multiple iterations and choose the ones which results in minimum loss across the whole training set.

### Credits

First of all, thank you Coursera for providing me the financial aid for _Andrew Ng's course on Neural Networks and Deep Learning_. I wrote this bytt as a detailed add-on to Ng's video lecture about _Logistic Regression as a Neural Network_ where he asks the viewers to work on the derivatives.

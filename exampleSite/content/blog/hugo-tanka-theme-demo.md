---
title: "Tanka Theme Demo"
author: "Nan Xiao"
date: "2020-11-21T12:00:00"
meta_img: images/example.jpg
---

[Tanka](https://github.com/nanxstats/hugo-tanka) is a Bootstrap-based minimalist theme for Hugo.

<div class="figure">

![](/images/example.jpg)

<p class="caption">Vik, Iceland. Photo by <a href="https://unsplash.com/photos/MLKrf51NV8w">Adam Jang</a>.</p>

</div>

## Typography

Follows the Bootstrap typography.

# h1 Heading

## h2 Heading

### h3 Heading

#### h4 Heading

##### h5 Heading

###### h6 Heading

---

**This is bold text**

__This is bold text__

*This is italic text*

_This is italic text_

~~Deleted text~~

> Block quotes are
> written like so.
>
> They can span multiple paragraphs,
> if you like.

Some text, and some `code` and then a nice plain [link with title](https://nanx.me "title text!").

and then

+ Create a list by starting a line with `+`, `-`, or `*`
+ Sub-lists are made by indenting 2 spaces:
  - Marker character change forces new list start:
    * Ac tristique libero volutpat at
+ Very easy!

vs.

1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa

## Math

Inline formula `$S_n = \sum_{i=1}^n X_i$` example.

$$S(n, k) = \frac{1}{k!}\sum_{i=0}^{k} (-1)^{i} \binom{k}{i} (k-i)^n.$$

## Code

Inline `code` example

### R

```r
library("msaenet")

dat = msaenet.sim.gaussian(
  n = 150, p = 500, rho = 0.5,
  coef = rep(1, 10), snr = 5, p.train = 0.7,
  seed = 1001
)

msaenet.fit = msaenet(
  dat$x.tr, dat$y.tr,
  alphas = seq(0.1, 0.9, 0.1),
  nsteps = 10L, tune.nsteps = "ebic",
  seed = 1005
)

msaenet.fit$best.step
msaenet.nzv(msaenet.fit)
plot(msaenet.fit, label = TRUE)
plot(msaenet.fit, type = "criterion")
plot(msaenet.fit, type = "dotplot", label = TRUE, label.cex = 1)
```

### Python

```python
@requires_authorization(roles=["ADMIN"])
def somefunc(param1='', param2=0):
    r'''A docstring'''
    if param1 > param2: # interesting
        print 'Gre\'ater'
    return (param2 - param1 + 1 + 0b10l) or None

class SomeClass:
    pass

>>> message = '''interpreter
... prompt'''
```

### Stan

```stan
// Multivariate Regression Example
// Taken from stan-reference-2.8.0.pdf p.66

data {
  int<lower=0> N;             // num individuals
  int<lower=1> K;             // num ind predictors
  int<lower=1> J;             // num groups
  int<lower=1> L;             // num group predictors
  int<lower=1,upper=J> jj[N]; // group for individual
  matrix[N,K] x;              // individual predictors
  row_vector[L] u[J];         // group predictors
  vector[N] y;                // outcomes
}
parameters {
  corr_matrix[K] Omega;       // prior correlation
  vector<lower=0>[K] tau;     // prior scale
  matrix[L,K] gamma;          // group coeffs
  vector[K] beta[J];          // indiv coeffs by group
  real<lower=0> sigma;        // prediction error scale
}
model {
  tau ~ cauchy(0,2.5);
  Omega ~ lkj_corr(2);
  to_vector(gamma) ~ normal(0, 5);
  {
    row_vector[K] u_gamma[J];
    for (j in 1:J)
      u_gamma[j] <- u[j] * gamma;
    beta ~ multi_normal(u_gamma, quad_form_diag(Omega, tau));
  }
  {
    vector[N] x_beta_jj;
    for (n in 1:N)
      x_beta_jj[n] <- x[n] * beta[jj[n]];
    y ~ normal(x_beta_jj, sigma);
  }
}

# Note: Octothorpes indicate comments, too!
```

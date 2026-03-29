---
layout: post
title: "Monte Carlo error propagation"
categories: statistics
author: Brandon Barker
---

> "A computation is a temptation that should be resisted as
> long as possible." - J. P. Boyd, paraphrasing T. S. Eliot

* * *

There is no such thing as a perfect measurement.
Inevitably we are met with the need to propagate measurement 
uncertainty on to some derived quantity. Given a measurement of 
a star's surface temperature and luminosity we may seek to 
estimate its radius. Given measurement uncertainty on the 
effective temperature and luminosity, how much can we trust 
the estimated radius?

In propagating the error of some quantity with an uncertain observation, 
we are faced with estimating the error for a
function of potentially multiple variables: $$z = f(u,v,w),$$ where the number of
variables can be thought of as the number of "things with error." Here
we consider three variables. There are a number of "standard" methods 
for propagating error typically learned early in the career -- 
when to add in quadrature, or inverses, or when to scale multiplicatively.
A number of questions arise: Where do these rules come from? 
When are they appropriate? We will examine these questions and, ultimately,
propose an alternative methods -- Monte Carlo error propagation.

## Derivation of the tradiational method

The true variance of our quantity $z$ is given by

$$\label{eq:true_error}
\sigma_z^2 = \iiint (z-\mu_z)^2 P(u,v,w)du\,dv\,dw$$

Where $P(u,v,w)$ is the true distribution that $z$ comes from and
$\mu_z$ is its mean. Similarly, the covariance of two variables is given
by

$$\label{eq:cov}
    \sigma_{uv} = \iint (u-\mu_u)(v-\mu_v)P(u,v)du\,dv.$$

For many applications of interest, we don't have knowledge of
the underlying distribution $P(u,v,w)$, so we must resort to
approximations. 
Ultimately, we seek to estimate $\sigma_z^2$.
Let us begin by Taylor expanding $z$ about $\mu_z$.

$$z - \mu_z \approx (u - \mu_u) (\partial_u z)\vert_{\mu_u} + (v - \mu_v) (\partial_v z)\vert_{\mu_v}
+ (w - \mu_w) (\partial_w z)\vert_{\mu_w}$$

Then we see that

$$\begin{aligned}
\begin{split}
(z - \mu_z)^2 &\approx (u - \mu_u)^2 (\partial_u z)^2 + (v - \mu_v)^2 (\partial_v z)^2\\
          &+ (w - \mu_w)^2 (\partial_w z)^2 + 2 (u-\mu_u)(v-\mu_v)(\partial_u z) (\partial_v z) \\
          &+ 2 (u-\mu_u)(w-\mu_w)(\partial_u z) (\partial_w z) + 2 (v-\mu_v)(w-\mu_w)(\partial_v z) (\partial_w z)
\end{split}          
\end{aligned}$$

Inserting the above into the expression for $\sigma_z^2$ 
we find the following expression:

$$\begin{aligned}
\begin{split}
\label{eq:long}
\sigma_z^2 &\approx \iiint (u - \mu_u)^2 (\partial_u z)^2 P(u,v,w)du\, dv\, dw\\
           &+ \iiint (v - \mu_v)^2 (\partial_v z)^2 P(u,v,w)du\, dv\, dw \\
           &+ \iiint (w - \mu_w)^2 (\partial_w z)^2 P(u,v,w)du\, dv\, dw\\
           &+ 2\iiint (u-\mu_u)(v-\mu_v) (\partial_u z) (\partial_v z) P(u,v,w)du\, dv\, dw\\
           &+ 2\iiint (u-\mu_u)(w-\mu_w) (\partial_u z) (\partial_w z) P(u,v,w)du\, dv\, dw\\
           &+ 2\iiint (v-\mu_v)(w-\mu_w) (\partial_v z) (\partial_w z) P(u,v,w)du\, dv\, dw
\end{split}
\end{aligned}$$

Now, recalling that the derivatives about have all been evaluated at
their respective means and are constants here, we may make use of two
simple definitions to finish simplifying our expression. First, notice
from the expression for $\sigma_z^2$ that the first three terms in the above
expression are proportional to $\sigma_u^2$, $\sigma_v^2$, and
$\sigma_w^2$ scaled by the squared partial derivatives. For the final
three terms, we may use the expression for the covariance
in the same way. Then we may simplify as follows

$$\begin{aligned}
\begin{split}
\label{eq:error}
\sigma_z^2 &\approx \sigma_u^2 (\partial_u z)^2 + \sigma_v^2 (\partial_v z)^2 + \sigma_w^2 (\partial_w z)^2\\
           &+ 2 \sigma_{uv}(\partial_u z)(\partial_v z) + 2 \sigma_{uw}(\partial_u z)(\partial_w z)\\
           &+ 2 \sigma_{vw}(\partial_v z)(\partial_w z) 
\end{split}
\end{aligned}$$

Then we have an expression to approximate error that depends on the
variances, covariances, and functional form of the fit. This may be
generalized to any number of variables.

+ **Exercise**: Let $z = uv$ where $u$ and $v$ are uncorrelated variables ($\sigma_{uv} = 0$). 
  Using the relationship above derive the error propagation rule for multiplicative 
  error propagation.

We may make a few observations this expression for the error.
* First, this form for error propagation assumes Gaussianity. $z$, $u$, and $v$ are 
  all described by normal distributions. This form **cannot treat non-Gaussian 
  posteriors.** This means that asymmetric uncertainties, $x = \mu^{+a}_{-b}$, 
  cannot be treated.
* Next, we derived this using a Taylor expansion. The usual caveats apply: 
  the first order series assumes that that magnitudes are small
  and that the function is approximately linear in the neighborhood of interest.

We will explore the implications of these assumptions in a future article but it 
is worth noting that these assumptions are readily broken in astronomy where one 
regularly needs to propagate error from logarithmic functions, for example.

## Monte Carlo error propagation
Next we will seek an alternative process for propagating error that 
removes the assumptions from the previous section and can be implemented 
trivially -- the *Monte Carlo* method.

The Monte Carlo method involves random sampling of the underlying distribution
and constructing an approximation of the distribution of out quantity of interest 
$z$. Begin by observing that if we have a measurement $u$ with variance
$\sigma_u^2$ and mean $\mu_u = u$ then $u$ is expected to be normally distributed.

The Monte Carlo procedure is then simple:

* Draw a sample $u_i$ from the Normal distribution: $u \sim N(\mu_u, \sigma_u)$.
* Construct and store $z_i = f(u_i)$.
* Repeat $N$ times, where $N$ is sufficiently large.

After this process we will have the posterior distribution for $z$ in our hands
and statistics such as the mean, median, and percentiles (uncertainties) can 
be read off directly. This process is attractive as it makes no assumptions about 
the underlying magnitudes or distributions and can be implemented in two lines of Python 
(which we will see below).

# Example: Absolute magnitudes from parallax
It is a common exercise in astronomy to estimate the absolute magnitude, the 
total brightness in magnitudes, of a star. Using the *distance modulus* we can 
do this simply as

$$ M - m - 5 log_{10}(d) + 5 $$

where $M$ is the absolute magnitude, $m$ is the apparent magnitude, and 
$d$ is the distance to the star in parsecs. 
Simply, this computes the actual brightness of a star adjusted for 
its distance.
There are a number of ways to measure
distance, but an early method is using [parallax][parallax]:

$$ d = 1 / \varpi $$

where $\varpi$ is the parallax in arcseconds.
Let's consider the familiar star [Lalande 21185][lalande]. 
Lalande 21185 has a parallax of 0.39275 $\pm$ 0.0000321 arcsec.
It has a V-band apparent magnitude of roughly 7.52 -- for this 
exercise we will take the error in the apparent magnitude to be zero 
for demonstration purposes. We can approximate the uncertainty in the 
absolute magnitude in the Taylor expansion form as

$$\begin{aligned}
\begin{split}
\sigma_M^2 &\approx \sigma_m^2 (\partial_m M)^2 + \sigma_d^2 (\partial_d M)^2 \\
           & = \sigma_m^2 + \sigma_d^2 (\frac{5}{ln(10)d})^2
\end{split}
\end{aligned}$$

with

$$\sigma_d^2 = \sigma_{\varpi}^2 (\partial_{\varpi}d)^2 = \frac{\sigma_d^2}{\varpi^2}.$$

This provides us with the estimate $M$ = 10.49 $\pm$ 6.97x10$^{-5}$

We can implement the Monte Carlo procedure with Python as

```python
def absolute_magnitude(m: np.ndarray | float, d: np.ndarray | float) -> np.ndarray | float:
    return m - 5.0 * np.log10(d) + 5.0

def distance(pi: np.ndarray | float) -> np.ndarray | float:
    return 1.0 / pi

def extract_stats(vals: np.ndarray | float) -> tuple[float, float, float]:
  percentiles = np.percentile(vals, [16, 50, 84])
  q = np.diff(percentiles)
  err_lo = q[0]
  err_hi = q[1]
  nominal = percentiles[1]
  return nominal, err_hi, err_lo

def monte_carlo_error_mag(
        pi: float, dpi: float, m: float, dm: float
) -> tuple[float, float, float]:
  n_mc = 25000
  # draw parallax and apparent mag distributions
  pis = np.random.normal(pi, dpi, n_mc)
  ms = np.random.normal(m, dm, n_mc)

  # construct distance distribution
  ds = distance(pis)

  # compute absolute magnitudes
  ys = absolute_magnitude(ms, ds)

  return extract_stats(ys)


def main() -> int:
  pi = 0.39275
  dpi = 3.21e-5

  m = 7.520
  dm = 0

  mean, hi, lo = monte_carlo_error_mag(pi, dpi, m, dm)
  print(f"M = {mean} + {hi} - {lo}")
  return os.EX_OK
```

This, in turn, provides the estimate $M$ = 10.49 $\pm$ 0.000176 -- 
more than a factor of 2x different! In this case the Taylor expansion based 
error estimate underestimated the actual variance by a factor of about 2.5.
All in all this example was relatively mild: the magnitudes small and nonlinearities 
not too severe. Even still, with only a few lines of Python we could improve our 
estimate by a factor of 2!

## Example: exponentiation
It is common in astronomy, and many other fields, to produce log quantities 
with uncertainties on the logged quantity. This is a great use case for 
the deficiency of the Taylor expansion procedure: given a quantity $x = log_{10}(z)$ 
with uncertainty $\sigma_x$, what is the uncertainty of $z = 10^x$?
Consider $x$ = 51.125 with $\sigma_x$ = 0.1. These numbers might be 
reasonable for the log of the exponsion energy of a supernova, 
for example.

The Taylor expansion procedure follow as 

$$ \sigma_z^2 = \sigma_x^2 (\partial_x z)^2 = \sigma_x^2(ln(10)10^x)^2.$$

The Monte Carlo procedure proceeds similarly to before:

```python
def f(x: np.ndarray | float) -> np.ndarray | float:
    return np.power(10.0, x)

def extract_stats(vals: np.ndarray | float) -> tuple[float, float, float]:
  percentiles = np.percentile(vals, [16, 50, 84])
  q = np.diff(percentiles)
  err_lo = q[0]
  err_hi = q[1]
  nominal = percentiles[1]
  return nominal, err_hi, err_lo


def monte_carlo_error(
        x: float, dx: float
) -> tuple[float, float, float]:
  n_mc = 500000 # 25000
  # draw x from normal distribution
  xs = np.random.normal(x, dx, n_mc)
  ys = f(xs)
  return extract_stats(ys)


def main() -> int:
  x = 51.125
  dx = 0.1

  mean, hi, lo = monte_carlo_error(x, dx)
  print(f"M = {mean} + {hi} - {lo}")
  return os.EX_OK
```
This time the Taylor expansion procedure give $z$ = 1.33352x10$^{51}$ $\pm$ 
3.0705x10$^{50}$. The Monte Carlo process, on the other hand, gives
$z$ = 1.33345x10$^{51}$ + 3.43x10$^{50}$ - 2.72x10$^{50}$. Notice the asymmetric 
uncertainties! Exponentiating a normal distribution does not produce 
a normal distribution, producing instead a distribution with a long tail.
The Taylor expansion based procedure cannot capture this.

## Summary
We have demonstrated how the traditional form of error propagation
arises from a Taylor expansion approximation of the actual variance.
This comes with a wealth of assumptions of the underlying distribution 
that are rarely met. 

We presented an alternative approach: the Monte Carlo procedure that works 
via sampling from the underlying posterior distributions. This process 
is trivial to implement in Python. 

We showed through two simple examples the failures of the traditional 
process for error propagation. The Taylor method may under- (or over-)
estimate the variance. Moreover, when nonlinearities are strong it fails 
to recover the actual distribution, forcing the assumption of Gaussianity 
on the posterior.

[lalande]: https://en.wikipedia.org/wiki/Lalande_21185
[parallax]: https://en.wikipedia.org/wiki/Stellar_parallax

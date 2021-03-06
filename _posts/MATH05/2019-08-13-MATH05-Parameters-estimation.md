---
layout : post
title : MATH05, Parameters estimation
categories: [MATH05]
comments : true
tags : [MATH05]
---
[Back to the previous page](https://userdyk-github.github.io/Study.html) ｜ <a href="https://userdyk-github.github.io/math05/MATH05-Contents.html" target="_blank">Statistics</a> <br>
List of posts to read before reading this article
- <a href='https://userdyk-github.github.io/pl03/PL03-Libraries.html' target="_blank">Python Libraries</a>
- <a href='https://en.wikipedia.org/wiki/List_of_probability_distributions' target="_blank">List of probability distributions</a>
- <a href='https://userdyk-github.github.io/math06/MATH06-Contents.html' target="_blank">Optimization</a>

---

## Contents
{:.no_toc}

* ToC
{:toc}

<hr class="division1">

## **Point estimation : Method of moment**
<div style="font-size: 70%; text-align: center;">
    Asumption : parameter is determined by sample statistic(population moment = sample moment)<br>
    Weekness : it is difficult to determine whether a parameter is accurate<br>
    Weekness : it's hard to figure out the confidence level and interval<br>
</div>
<br><br><br>

### ***estimate for beta distribution***

<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/5fc18388353b219c482e8e35ca4aae808ab1be81" class="mwe-math-fallback-image-inline" aria-hidden="true" style="vertical-align: -14.049ex; margin-bottom: -0.289ex; width:38.853ex; height:29.843ex;" alt="{\displaystyle {\begin{aligned}f(x;\alpha ,\beta )&amp;=\mathrm {constant} \cdot x^{\alpha -1}(1-x)^{\beta -1}\\[3pt]&amp;={\frac {x^{\alpha -1}(1-x)^{\beta -1}}{\displaystyle \int _{0}^{1}u^{\alpha -1}(1-u)^{\beta -1}\,du}}\\[6pt]&amp;={\frac {\Gamma (\alpha +\beta )}{\Gamma (\alpha )\Gamma (\beta )}}\,x^{\alpha -1}(1-x)^{\beta -1}\\[6pt]&amp;={\frac {1}{\mathrm {B} (\alpha ,\beta )}}x^{\alpha -1}(1-x)^{\beta -1}\end{aligned}}}">
<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/e03c03f31b903a1bc73ea8b637e3134b110a85a2" class="mwe-math-fallback-image-inline" aria-hidden="true" style="vertical-align: -3.005ex; width:36.574ex; height:7.343ex;" alt="\operatorname{E}[X^k]= \frac{\alpha^{(k)}}{(\alpha + \beta)^{(k)}} = \prod_{r=0}^{k-1} \frac{\alpha+r}{\alpha+\beta+r}">

```python
from scipy import stats
import numpy as np

def estimate_beta(x):
    x_bar = x.mean()
    s2 = x.var()
    a = x_bar * (x_bar * (1 - x_bar) / s2 - 1)
    b = (1 - x_bar) * (x_bar * (1 - x_bar) / s2 - 1)
    return a, b
    
np.random.seed(0)
x = stats.beta(15, 12).rvs(10000)
estimate_beta(x)
```
<span class="jb-medium">(15.346682046700685, 12.2121537049535)</span>
<br><br><br>
<hr class="division2">



## **Point estimation : Maximum Likelihood Estimation(MLE)**
<div style="font-size: 70%; text-align: center;">
    Caution : parameter ≠ random variable<br>
    Weekness : it's hard to figure out the confidence level and interval<br>
</div>
<br><br><br>

### ***likelihood for normal distribution about single sample data***

<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/4abaca87a10ecfa77b5a205056523706fe6c9c3f" class="mwe-math-fallback-image-inline" aria-hidden="true" style="vertical-align: -2.838ex; width:29.801ex; height:7.176ex;" alt="{\displaystyle f(x\mid \mu ,\sigma ^{2})={\frac {1}{\sqrt {2\pi \sigma ^{2}}}}e^{-{\frac {(x-\mu )^{2}}{2\sigma ^{2}}}}}">
<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/fa485e7acf98b3a0ce236ce7293f63dd89f84b96" class="mwe-math-fallback-image-inline" aria-hidden="true" style="vertical-align: -0.838ex; width:27.746ex; height:2.843ex;" alt="{\displaystyle L_{n}(\theta )=L_{n}(\theta ;\mathbf {y} )=f_{n}(\mathbf {y} ;\theta )}">
<div style="font-size: 70%; text-align: center;">
    $$given\ dataset\ x\ :\ \{0\}$$
    $$given\ parameter\ \sigma \ =\ 1$$
    $$likelihood\ :\ L(\theta = \mu ;x) = \frac{1}{\sqrt{2 \pi \sigma}}e^{-\frac{(\mu-x)^{2}}{2\sigma^{2}}}$$
</div>
`for mu`
```python
import numpy as np
from scipy import optimize

# objective function(= -likelihood)
def objective(MU, SIGMA2=1):
    return - np.exp(-(MU) ** 2 / (2 * SIGMA2)) / np.sqrt(2 * np.pi * SIGMA2)

# optimize
optimize.brent(objective, brack=(-10,10))
```
<span class="jb-medium">optimal point for mu = 1.3008039364016205e-11</span>
<details markdown="1">
<summary class='jb-small' style="color:blue">Visualization</summary>
<hr class='division3'>
```python
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
import numpy as np

# range of mu and sigma^2 at x = 0
x = 0
mus = np.linspace(-5, 5, 1000)
sigma2s = np.linspace(0.1, 10, 1000)
MU, SIGMA2 = np.meshgrid(mus, sigma2s)

# likelihood
L = np.exp(-(MU-x) ** 2 / (2 * SIGMA2)) / np.sqrt(2 * np.pi * SIGMA2)

# plot
fig = plt.figure()
ax = Axes3D(fig)
ax = fig.gca(projection='3d')
ax.plot_surface(MU, SIGMA2, L, linewidth=0.1)
plt.xlabel('$\mu$')
plt.ylabel('$\sigma^2$')
plt.title('likelihood $L(\mu, \sigma^2)$')
plt.show()
```
![download](https://user-images.githubusercontent.com/52376448/66691348-9f364f00-ecd0-11e9-8d18-074f932e3776.png)
<hr class='division3'>
</details>
<br><br><br>

### ***likelihood for normal distribution about multi-sample data***
<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/1b75a50d0a600772fcca460d04f1e3673f2a3c1f" class="mwe-math-fallback-image-inline" aria-hidden="true" style="vertical-align: -3.171ex; width:78.984ex; height:7.509ex;" alt="{\displaystyle f(x_{1},\ldots ,x_{n}\mid \mu ,\sigma ^{2})=\prod _{i=1}^{n}f(x_{i}\mid \mu ,\sigma ^{2})=\left({\frac {1}{2\pi \sigma ^{2}}}\right)^{n/2}\exp \left(-{\frac {\sum _{i=1}^{n}(x_{i}-\mu )^{2}}{2\sigma ^{2}}}\right).}">
<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/fa485e7acf98b3a0ce236ce7293f63dd89f84b96" class="mwe-math-fallback-image-inline" aria-hidden="true" style="vertical-align: -0.838ex; width:27.746ex; height:2.843ex;" alt="{\displaystyle L_{n}(\theta )=L_{n}(\theta ;\mathbf {y} )=f_{n}(\mathbf {y} ;\theta )}">
<div style="font-size: 70%; text-align: center;">
    $$given\ dataset\ x\ :\ \{-3,\ 0,\ 1\}$$
    $$given\ parameter\ \sigma \ =\ 1$$
    $$likelihood\ :\ L(\theta = \mu ;x) = \frac{1}{(\sqrt{2 \pi \sigma})^{3/2}}e^{-\frac{3(\mu+\frac{2}{3})^{2}+\frac{26}{3}}{2\sigma^{2}}}$$
</div>
```python
import numpy as np
from scipy import optimize

def objective(mu, sigma2=1):
    return - (2 * np.pi * sigma2) ** (3 / 2) * np.exp(-(3 * mu ** 2 + 4 * mu + 10) / (2 * sigma2))

# optimize
optimize.brent(objective, brack=(0,1))
```
<span class="jb-medium">optimal point for mu = -0.6666666665981932</span>
<br><br><br>
<hr class="division2">




## **Interval estimation : Bayesian estimation**
<div style="font-size: 70%; text-align: center;">
    Asumption : parameter = random variable
</div>
<hr class="division1">

List of posts followed by this article
- [post1](https://userdyk-github.github.io/)
- <a href='https://userdyk-github.github.io/'>post2</a>
- <a href='https://userdyk-github.github.io/'>post3</a>

---

Reference
- <a href='https://datascienceschool.net/view-notebook/87b67dafd7544e3380af278ff4f22d77/' target="_blank">method of moment</a>
- <a href='https://datascienceschool.net/view-notebook/864a2cc43df44531be32e3fa48769501/' target="_blank">likelihood function</a>
- <a href='https://datascienceschool.net/view-notebook/ae35a40deb884cf88e85135b4b5a1130/' target="_blank">Bayesian estimation</a>

---

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
    <details markdown="1">
    <summary class='jb-small' style="color:red">OUTPUT</summary>
    <hr class='division3_1'>
    <hr class='division3_1'>
    </details>
<hr class='division3'>
</details>


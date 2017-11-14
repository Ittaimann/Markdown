# cs 115 lecture proof testing?
[created in markdown with katex](https://khan.github.io/KaTeX/function-support.html)
 

 $F=\frac{Gm_1 m_2 }{r^2}$ is the equation for relative gravity and it is *very* accurate **however we can only  prove it is false, but we can't prove its true**

 mistake from last  lecture: something about the distributions? for a probablity density function  
 ****you can't accept anything as true except apperantly wayne is awesome?**** 
 
 $t^{n} = \frac {x(n) -\mu_0}{\sqrt{S^2(n)/n}}$  
 $|t^n|>t_{n-1, 1-\frac{\alpha}{2}}$-> reject at level α  
  <=  cannot reject

## 2 types of errors
- test positive: truth (unkown of hypothesis): this is a table of wherther the test was posisitive or negative, and if te hypothesis is correct or not


||+|-
|-|--------------|--------------|  
|+|true positive   (hypothesis is right and test was right) | false positive|  
|-|false negative| true negative (hypothesis was wrong, and test returned wrong|


- +- false positive : fail to reject ("or accept")  $h_0$ when it is actually false, probability is $\delta , 1-\delta \triangleq power$ (you have tested it and it was positive, but its wrong)    
- -- false negative: we reject $h_0$ when actually true, probability is α (type 1 error?)

- [here is the wiki pedia but he apperantly had shit flipped around](https://en.wikipedia.org/wiki/Type_I_and_type_II_errors)

## review a big picture
- choosing input distributions
    1) pick a distribution
        - evidence, intution, whatever
    2) Fit parameters to observations
    3) Goodness of fit test (if bad go to one)    

- so far we have harped on 3 via confidence intervals and hypothesis testing, but now we need 1 and 2
 - note: there are many distributions tabulated in text books, and all of them have well understood properties
    -   typical of distributions: they have 2-3 generalized     parameters  
         A) the location parameters  
          B) scale   
         C) and shape

## [maximum likelyhood estimators (MLE)](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation)
- fit parameter $\theta$ from empirical data to a theoretical distribution 

  **definition** : MLE is the value of $\theta$ that maximizes the $probability^y$ that you get the observed data  
  ex:  likely hood function:
  $L(\theta)= p_\theta(x_1)p_\theta(x_2)p_\theta(x_3)p_\theta(x_4)...p_\theta(x_n) =	\prod_{i=1}^{n}$ $p_\theta(x_i)$= joint pmf of observing $x_1->x_n$ given parameter $\theta$ 

  solve for $\hat{\theta}$ so that L($\hat{\theta}$)>= lecture
  ($\theta$) for all theta 


  EX:
    assume {$X_i$} are uniform on [a,b]   
    Q: MLE for a? b? 
    clearly $\hat{a}<=minX_i, \hat{b}>=maxX_i$  and $F_{a,b}(x)=\frac{1}{b-a}$  
    L(a,b)= $F_{a,b})(x_1)... F_{a,b}(X_n)= \frac{1}{b-a}^n$
    note this is a decreasing function of (b-a) if says       
    $\hat{a}=minX_i, \hat{b}=maxX_i$

## some example distributions
|  name | symbol   | pmf  |cdf   | mean | var| comments|
|---|---|---|---|---|---|---|
| uniform  |U(a,b) |$\frac{1}{b-a}$   |$\frac{x-a}{b-a}$   |$\frac{a+b}{2}$  | $\frac{(b-a)^2}{12}$| max entropy sal^ h when no info is known|
|exponoential   | rate r=1/$\beta$, beta =average   inter arrival  |$f(x)=re^{-rt}$,   t>=0   |$F(x)=1-e^{-rt}$   |$\beta$   |$\beta^2$  |mle $\hat{\beta}=\bar{X}$, def: coefficient of variation = $\frac{\alpha}{\mu}= \sigma$ for exp distribution =1 $\approx \frac{\sqrt{S^2(n)}}{\bar(X)(n)}$ |
|   |   |   |   |   |||

**short proof that MLE $\hat{\beta}=\bar{X}(n)$**
 - suppose that we observe sequence of interarrival times $X_1...X_n$.
 ## L($\beta$)=($1/ \beta e^{-X_1/\beta}*(1/ \beta e^{-X_2/\beta})...(1/ \beta e^{-X_n/\beta}=1/\beta^n e^{-1/\beta \sum {x_i}}$ )   
## take Ln($\beta$) = L($\beta$) = -nln $\beta$ - 1/$\beta  \sum x_i ->\frac{dl(\beta)}{d\beta}= -n/\beta+ 1/\beta^2 \sum x_i=0$

## $\beta= \infty$ or $\beta =1/n \sum x_i     \equiv \bar{x}n$ 

note  therefore ln (x) is monotonic max L($\beta$) occurs at same $\beta$ as maxL($\beta$)


## $\frac{d^2l(\beta)}{d\beta}=\frac{n}{\beta^2}-\frac{2}{\beta^3}\sum{x_i} = \frac{1}{\beta^3}[n\beta-2\sum{x_i}]=\begin{cases} 0 (?) \beta=\infty\\-\frac{n\bar{x}(n)}{(\bar{x}(n))^3}=\frac{-n}{\bar{x}(n)}<0 \end{cases}$ therefore(?) $\beta=\bar{x}$->QED


|  name | symbol   | pmf  |cdf   | mean | var| comments| cov|
|---|---|---|---|---|---|---|---|
|erlang -k also known as (gamma (k,$\beta$)) == sum of k exponentials each with rate 1/$\beta$ (gamma (k,$\beta$)) ||$\frac{1}{\beta^k}\frac{x^{K-1}e^{x/\beta}}{(k-1)!}=\frac{1}{\beta}\frac{(x/\beta)^{k-1}}{(k-1)!}e^{-x/\beta}$|cdf:$1- e^{-x/\beta} \displaystyle\sum_{j=0}^{k-1} \frac{(x\beta)^2}{j!}$ is the sum of k interarrivals|mean: k$\beta$| $\beta^2$|="stages of service " ="jump ahead k interarrivals".  used to sample arrivals $k^{arrivals}$ apart | $\sigma = \frac{1}{\sqrt(k)}<1$| 




hyper-exponential: choosing one of *R* exponentials with rate $1/\beta_i$ with probability $P_i$   
### f(x)=$\displaystyle\sum_{i=1}^n \frac {P_i}{\beta_i}e^\frac{-x}{\beta_i}$
mean:$\displaystyle\sum_{i=1}^n P_i\beta_i$
variance(?): $\sigma >= 1$




#
# Lecture 2 with these

## more distributions       
- choose distributions   

    1 -  pick  
    2 - fit(MLE)  
    3 - check for goodness  
- [Bernoulli distribution (p)](https://en.wikipedia.org/wiki/Bernoulli_distribution)
    - coin toss 
    - P(k)= {p,k=0 "heads }  
            {1-p, k=1 "tails }  
    - mean: p -> $\bar(x)$
    - variance: p(1-p)
    - $\delta$: $\sqrt{(1-p)/p}$
    - $\bar(x)(1-\bar(x))= S^2(n)$
- [binomial distribution(n,p)](https://en.wikipedia.org/wiki/Binomial_distribution)
    - nuber of succsess in i Bernoulli trials
    - p(k)=$n\choose{k}$ $p^k (1-p)^{n-k}$
    - mean: $np$ n trials, each with p probability
    - variance: $np(1-p)$

- [geometric distribution](https://en.wikipedia.org/wiki/Geometric_distribution)
    - number of failures before the first Bernoulli trial
    - p(k)= $(1-p^k)p$, k =0,1,...
    - mean: $\frac{1-p}{p}$
    - variance: $\frac{1-p}{p^2}$
    - MLE: $\hat{p}= \frac{1}{1+\bar{x}(n)}$
- [possion distribution](https://en.wikipedia.org/wiki/Poisson_distribution)
    - number of events in an interval(area or volume) where events are independent i.d. uniformly distributed
    - P(k)=$\frac{\lambda^k}{k!}e^-\lambda$
    - mean: $\lambda$
    - variance: $\lambda$
    - MLE: $\hat{\lambda}=\bar{x}(n)$

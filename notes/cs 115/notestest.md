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

## coefficient of variation
## - $\delta \hat{=} \frac{\sqrt{var}}{E[x]}\approx \frac{\sqrt{S^n}}{\bar{x}(n)}$ 
 - notice dimensionaless number because is measure of standard deviation in units of the mean 
 - not well defined if E[X]=0
 - **but** value can give us strong hints on what is the underlying distribution
 - EX:
    - the $\delta$ is always 1 for exponential distribution 
    - $\delta$ always greater then 1 for hyper exponential (?)
    -  $\delta$ always less then 1 for erlang-k

## how to pick a distribution
- how to pick from all these choices  
1 - from outside reasoning  
2 - Look for characteristic values of "point" (means, variances, coefficient of variation) statistics  
    - non negative?  
    - fall in range?
      
    3 - histograms  
    - a) partition frequency in each range
    - b) count frequency in each range
    - c) inspect histogram: what does it look like? try MLE?
    - d) compare visually for goodness of fit

### testing for goodness of fit
1) ad hoc method  
    a) do key point values mathc?  
    b)density or histogram plots and compare to theoreticla fit. "Looks similar"
2) graphical methods   
    A) q-q plots  
    b) p-p plots
3) formal statistics test   
    A) chi-sq  
    b) k-s tests

# Lecture before midterm

## [fermies paradox](https://en.wikipedia.org/wiki/Fermi_paradox)
- life occured as single cell almost as soon as possible, took a while to go from single to multi celluar
- We then discovered other planets, 
- we then find other planets and interterestrial travel
- in a few million years, even at 1 light year a 1000 years we will traverse the entire galaxy.
- if this is the case... where is everyone? why do the alieans who have had so much longer to traverse the galaxy 

## Chooisng distribution (for the 11th time)
 1) choose
 2) fit parameters
 3) test for goodness of fit ( if bad go back to 1 ) 

## probability plots (p-p, Q-Q plots)
 - take set of data and compare it to our distributions. We can even look at a theoretical distribution and sort it  
 1) sort $X_1...X_n$ into non decreasing order $\hat{X_1}...\hat{X_n}$ where the hat means its sorted. $\hat{X_i}=i^{th}$ order statistic   
    -  set $y=\frac{i}{n}$ for $x=\hat{X_i}$ 

    -    one disadvantage is that cdf's tend to just look like S - shaped curves.   
        **INSERT THE PICTURE OF THE GRAPH**
        **INSERT THE PICTURE OF THE GRAPH**  
     -   say we have two sorted sample of points  $\hat{X_1}...\hat{X_n}$ and  $\hat{Y_1}...\hat{Y_n}$  
     -   this creates two graphs, we must now take the difference. We choose a point p on the horizontal and relate it to the vertical distance. this gets you an $F_x(p)$ and $F_y(p)$     **(This will be used for the pp plots)**
### Q-Q plots
   -   We can also place a *q* on the vertical and do a similar thing to get the horizontal distances  $F_{x}^{-1}(q)$ and $F_{y}^{-1}(q)$. This gives you a q-q plot  
        **INsert the pic**   
   -   March through each values of q, and plot the (X,Y) of the q for each q   
      -  EX:  
            A) 45 degree line thru origin if $F_x=F_y$  
            B) 45 dgree line not thru the origin if $F_X$ and $F_Y$ differ by a location parameter (y=x+q)  
            C) straight line not at 45 degrees if they differ by a scale parameter.  
            - through orign -> y=mx
            - not through orign -> y=mx+b 

         d) Funny curve -otherwise

### PP plots 
- march along the horizontal axis through values called p and simply plot $F_x(p),F_y(p)$

### notes  
 - Q-Q plots emphasis differences in the tails of the distributions.
 - P-P plots emphasise the differences in the middle of the distribution 

### [Chi (ki, or the flem sound) - squared tests](https://en.wikipedia.org/wiki/Chi-squared_distribution)
- let $Y_1...Y_n$ be independent and identically distributed standard normal N(0,1) random variables
- then $X=Y{_1}^2 +... +Y{_n}^2$ is non negative and defines te $\chi$ square distribution with n degrees of freedom
- PDF and CDF are tabulated in many [places](https://en.wikipedia.org/wiki/Chi-squared_distribution) 
- **Chi squared test**
    - take your data $X_1...X_n$ and place them into histogram bins $(-\infty$ or $a_0 ,a_1),[a_1,a_2),[a_2,a_3)...[a_{k-1},\infty$ or $a_k)$
    the $a_i$'s represent k-1 "Cut points" so $B_1,B_2,...B_k$ which means we have k-1 degrees of freedom 
    - Define $N_J$ = # samples that fall in $B_i$ note $\epsilon N_j=n$
    - Q: given theoretical distribution f(x), let $p_j=\int_{a_j-1}^{_j} F(x) dx=F(a_j)-F(a_j-1)=$ probability of sample from f falling into bin back
    - IF $X_i$'s came from F, we expect $p_J*n$ samples in $B_j$
    - ### DEFINE $\chi^2=\sum_{j=1}^{k}\frac{(N_j-np_j)^2}{np_j}$
        - ### what: recall Z(N)=$\frac{\bar{X}(n)-\mu}{\sqrt{\sigma^2/n}}$ => n(0,1) as n->$\infty$
        - ### so  $(Z(N))^2=\frac{\bar{X}(n)-\mu}{\sigma^2}\bar{=}\frac{(N_j-np_j)^2}{np_j(1-p_i)}$ where $p_j$ is small $1-p_i \approx 1$
    - recall binomial distribution distinct(n,p)=# heads in n flips with p heads,
        -  mean is np
        - variance is np(1-p)
    - AS N GOES TO INFINITY AND BINS GO TO INFINITY CHI SQUARED IS THE SUM OF THE SQUARES OF N STANDARD NORMAL VARIBLES
    - if the difference between n standard normal variables are close to  chi squared is small enough, you have chosen the right F(x)
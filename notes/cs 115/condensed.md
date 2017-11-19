# Simulations:
- ****SIMULATIONS MUST ANSWER A QUESTION AND THE QUESTION MUST DRIVE THE SIMULATION****
              
                    system
                    /    \
                   real->model
                        /     \ 
                phys models   math models
                               /        \
                            analytic  simulations
                            models  
- flavors of simulations
    - 3 axes
        - static or dynamic
            - no changes with time | changes with times
        - deterministic vs stochiastic
            - is there no randomness or is there?
        - discrete vs continous 
            - variables change instantly vs variables changing constaly when they changes
- static   
    - [monte carlo integration](https://en.wikipedia.org/wiki/Monte_Carlo_integration)
    - numerical integration
    - load calculation on bridge
- deterministic
    - Newtonian physics
    - long and hard composition?
    - output determined by input
- stochastic   
    - randomness is involved. Input can vary sometimes
    - output is also randomness (this can be measured via confidence interval)
- discrete
    - in time, space, entities, events
- continuous
    - motion in physics (?)
    - Things do not suddenly change, think of a gradient(?)
# Error in simulations
- evaluating error is vital, however a deterministic and discrete system can be modeled exactly, its no an approximation

- error in simulating a continous system
    - $\int_a^b \mathrm{F(x)}\mathrm{d}x$ 
    - Reimansums calculate the area under a curve via rectangles checking under the curve, and the slimmer the rectangles the better our approximation is.
    - there is some large amount of error in this though (I don't know exactly what it was cause I typed the original badly)
    - so instead we use a *trapezoidal approximation* 
        - the error is only $\alpha\frac{1}{n^2}$
    - using trapezoidal approximate and midpoint we can get a approximate error amount of $\alpha\frac{1}{n^3}$
    - Trade off here is more human work, less cpu
    
    ### [ordinary differential equations](https://en.wikipedia.org/wiki/Ordinary_differential_equation)

# Simulation of stochastic Modes
 - sampling error, no exact right answer, all issues are caused by randomness. There is no way to directly fix this, but we can take more samples to even it all out
 - one sample tells you almost nothing, many are needed to get a good estimate and confidence
 - one simulation = "run" once run =1 sample of all stats
    - many runs to get confidence in answers (assumes no bugs)
    - ex: deterministic system, Monte Carlo integration
# Poisson process models time of events
 - Poisson process arrivals of events are distributed uniformly at random time.
 - if a system is dynamic then you need to model time, but there are 2 schools for this
    -  time driven sim, EG $\Delta$ time and a loop that iterates it. So if you had a simulation you would go literally minute by minute
    - ***Event driven***: No need to have a $\Delta$ time, as we model the next event based on when they would happen, but the moments between are discarded. Everything not directly related to the simulation, such as statistics, starting, and ending are handled outside.

# random Variables
 - Random Variable *RV* is the value associated with some random event
 - discrete random variable *X* can only have one of finitely many possible values, there is a fixed finite probabily p(*X*) tht the variable with have a particular value *x* for each *X* 
 - **Probability distribution** : given Random variable *x*, a probability distribution function is $f_x$ that assigns probability $F_X(x)$ to each value *x*
    ### $\sum_{possible x}{f_X(x)}=1$
- some common distributions 
    - uniform 
    - normal
- continous random variable x can have one of infinitley many values, so x being any single value has the probability of 0. So we can only really talk about it as an interval
- This is when we want a *Probability Density Function (PDF)* 
- $F_x$ represents the probabilty that the value x lies within the interval [a,b]
# multiple streams for the randomizer
 - The way most computers handle random variables means that we are going to need to seperate how we handle each random variable or stream. We shouldn't be using the same random seed for train arrivals hogouts, and everything else. We need to create multple random streams for each of these.
 - how to proberly generate random numbers:
    - way 1) generate a sequence of integers 0->n where each integer X is based on $X_{i_1}(A_{X_i}+B)$ mod MAX_UNIT->Randint(). where A, B constants are chosen very carefully. $X_0$ acts as our seed, and sequences with the same seed are equivalent.
- properties we want in a sequence
    - a finite number of integers, the ints must at some point repeat
    -long term average we want is MAX_UNIT/2
- **streams**
    - choosing: sometimes the computer will pick a certain statistic that is always in flux (system time, process id, hostname ip)

# Simulation language / csim stuff ( read the book? )
- simulation langauges describe entites, how they interact, and what they do all as a function of time.
- historical note: first sim language was gpss
- *facility*: resouces, queue, service
- *storage*: certain available space, like seats in a theatre
- *Events*: signals that can be set\unset by a particular entity
    - these can be queueed and waited upon
- *processes(threads)*: repressents active entites in the model all running simultaneously 
- gathering statistics: table for keeping track of certain things, and report to keep track of mins, max, range, standard deviation, and average
- *Q-table*: Time average of a discrete value
    - must call update function any time value changes
- meter: used to record where and when processes are called on entites.
# [quick mafs](https://www.youtube.com/watch?v=X09oxyIeGuY)
 - variance
    - given n samples $X_1,X_2...X_n$
    - sample mean is $\bar {X}(n)=\frac{1}{n}*\sum X_i$ where x bar is the sample mean from n samples
    -sample variance var(n)= $\frac{1}{n-1}*\sum (X_i-\bar {X}(n))^2$
    - n must be at least 2 to make the formula valid
        - var(n)=$\frac{1}{n-1}*\sum (X_i^2- 2*\bar {X}(n)*X_i+\bar{X}^2)^2$
        -=$\frac{1}{n-1}*\sum (X_i^2)- 2*\bar {X}(n)*\sum (X_i)+ n*\bar{X}^2)$
    - computing $\bar{x}$ and variance 'online'
        -  var(n)=$\frac{1}{n-1}*\sum(X_i^2)-\frac{1}{n-1} *\bar{X}^2)$
        - this method is unstable however and sometimes the answer might be very distant from reality
    - numeric instability
        - worry if sum(Xi^2) is close to n(X_bar^2)
    			if var(n) / n(Xi^2) is approx less than 10^-16 (machine precision)
    				bad sign
    			if logbase10(var(n) / n(X_bar^2)) is -k, then you have 16 - k digits of precision
    - properties of variance
        - variance of mean != variance of individual samples
        - varx(n)>=0
        - var(cX)=C^2*var(x)
        - var($\sum X_i$)= $\sum(var(X_i))$
    - variance($\bar{X}$)=$\frac{1}{n}*var(x)$
        - standard deviation = square root of 

# Confidence intervals
 - $\mu$ = actual mean 
 - $\sigma^2$= actual variance
 - $\bar{X}$=mean of n samples
 - var(n)= variance of n samples
- Given a sequence of independent, identically distributed random variables $X_1, X_2...X_n$ 
    - variance assume true mean $\mu$ , variance $\sigma^2$, both finite 
    - what do we know about $\bar{X}$ and $varx(n)$= $S^2(n)$ where S is an estimate of sigma
- steps
    1) we'll find $\mu$ if we are patient enough
        - law of large numbers. if x is an any distribution, then the limit of $\bar{x}(n)$  as n goes to infinity is $\mu$ 
    2) everything looks normal after a while
        - central limit theorem
            - $\sigma^2$= var(n)
            - if x is any distribution, can define (but not compute) new variable Z(n)
            Z(n):= $\frac{\bar{x}(n)-\mu}{\sqrt{\sigma^2/n}}$
            - as n-> infinite, Z(n) is the standard normal distribution N(0,1) bell curve\gaussian distribution, mean $\mu = 0$, variance $\sigma^2=1$
            - [The standard normal distribution has been tabulated for ever.](https://financetrain.com/assets/cp1.png)
        - $\alpha$=1-confidence; =risk
        - $P(|Z(n)| < Z(1 - \alpha/2)) = 1 - \alpha$
            - $P(-Z(1-\alpha/2)< Z(n)<+Z(1-\alpha/2))=1-\alpha$
            - $P(\bar{X}(n) -Z(1-\alpha/2)*\sqrt{\sigma^2/n}$<$\mu<\bar{X}(n)+Z(1-\alpha/2)*\sqrt{\sigma^2/n}=1-\alpha$

        - if the number of samples is sub 30, use Student T distribution with n-1 degree of freedom and not the normal distribution
        - 3 Elements:  
            N samples  
            +/-  error interval
            x%  confidence  
            if given 2, calculate the other one.
    - if unknown $\mu$ and $\sigma$, only have $\bar{x}$ and var(n) must coorect for additional uncertainty from var(n) instead of $\sigma^2$ 
        - if using var(n) in the Z(n) equation then Z(n) is no longer gaussian 

        
# finite state machines
 - State diagram: a directed graph where nodes are states, and edges are events that cause state changes. Each entity has its own state diagram
 - state Diagrams: all the "action" occurs along the arrows that define events because by definition: a state is static between events, nothing happens.
    - event handling routines must handle all changes to all entites effected
# Poisson arrival process 
- We use the Exponential distribution for the arrival process, if we have an arrival rate *r* then on average r arrivals per unit time.
- Recall the poisson distribution is discrete, so the number of arrivals *k* in an interval of length 1 is 
    ### $p(k)=e^{-r}\frac{r^k}{k!}$
- thus arrival rate across interval L is lr 
- let n(t) be cumulative number of arrivals up to time t (start at t=0), so that 
    ### $P(N(T)=k)=e^{-rt}\frac{rt^k}{k!}$
- particular for k=0
    - P(N(T)=0)=$e^{-rt}$, so that $P^y$ is the probability that the first arrival is before time T is (N(T)>0)=$ 1-e^{-rt}

# Properties of Distributions

## [coefficient of variation](https://en.wikipedia.org/wiki/Coefficient_of_variation)
## - $\delta \hat{=} \frac{\sqrt{var}}{E[x]}\approx \frac{\sqrt{S^n}}{\bar{x}(n)}$ 
 - notice dimensionaless number because is measure of standard deviation in units of the mean 
 - not well defined if E[X]=0
 - **but** value can give us strong hints on what is the underlying distribution
 - EX:
    - the $\delta$ is always 1 for exponential distribution 
    - $\delta$ always greater then 1 for hyper exponential (?)
    -  $\delta$ always less then 1 for erlang-k

## [maximum likelyhood estimators (MLE)](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation)
- fit parameter $\theta$ from empirical data to a theoretical distribution 

  **definition** : MLE is the value of $\theta$ that maximizes the $probability^y$ that you get the observed data 
- ex: likely hood function:  
  $L(\theta)= p_\theta(x_1)p_\theta(x_2)p_\theta(x_3)p_\theta(x_4)...p_\theta(x_n) =	\prod_{i=1}^{n}$ $p_\theta(x_i)$= joint pmf of observing $x_1->x_n$ given parameter $\theta$ 

  solve for $\hat{\theta}$ so that L($\hat{\theta}$)>= lecture
  ($\theta$) for all theta 


- EX:
    assume {$X_i$} are uniform on [a,b]   
    Q: MLE for a? b? 
    clearly $\hat{a}<=minX_i, \hat{b}>=maxX_i$  and $F_{a,b}(x)=\frac{1}{b-a}$  
    L(a,b)= $F_{a,b})(x_1)... F_{a,b}(X_n)= \frac{1}{b-a}^n$
    note this is a decreasing function of (b-a) if says       
    $\hat{a}=minX_i, \hat{b}=maxX_i$

# Distributions
## [Uniform](https://en.wikipedia.org/wiki/Uniform_distribution_(continuous))
 - symbol: U(a,b)
 - pmf: $\frac{1}{b-a}$  
 - cdf: $\frac{x-a}{b-a}$
 - mean: $\frac{a+b}{2}$
 - variance: $\frac{(b-a)^2}{12}$
 - comments: Max entropy is sal^h when no info is known
## [Exponential](https://en.wikipedia.org/wiki/Exponential_distribution) 
 - symbol:  rate r=1/$\beta$, beta =average   inter arrival 
 - pmf: $f(x)=re^{-rt}$, t>=0  
 - cdf: $F(x)=1-e^{-rt}$
 - mean: $\beta$
 - variance: $\beta^2$
 - comments: mle $\hat{\beta}=\bar{X}$, def: coefficient of variation = $\frac{\alpha}{\mu}= \sigma$ for exp distribution =1 $\approx \frac {\sqrt{S^2(n)}}{\bar(X)(n)}$
    - "short" proof for MLE of exponential:
        -  suppose that we observe sequence of interarrival times $X_1...X_n$.
        ## L($\beta$)=($1/ \beta e^{-X_1/\beta}*(1/ \beta e^{-X_2/\beta})...(1/ \beta e^{-X_n/\beta}=1/\beta^n e^{-1/\beta \sum {x_i}}$ )   
        ## take Ln($\beta$) = L($\beta$) = -nln $\beta$ - 1/$\beta  \sum x_i ->\frac{dl(\beta)}{d\beta}= -n/\beta+ 1/\beta^2 \sum x_i=0$

        ## $\beta= \infty$ or $\beta =1/n \sum x_i     \equiv \bar{x}n$ 

        note  therefore ln (x) is monotonic max L($\beta$) occurs at same $\beta$ as maxL($\beta$)


        ## $\frac{d^2l(\beta)}{d\beta}=\frac{n}{\beta^2}-\frac{2}{\beta^3}\sum{x_i} = \frac{1}{\beta^3}[n\beta-2\sum{x_i}]=\begin{cases} 0 (?) \beta=\infty\\-\frac{n\bar{x}(n)}{(\bar{x}(n))^3}=\frac{-n}{\bar{x}(n)}<0 \end{cases}$ therefore(?) $\beta=\bar{x}$->QED
## [Erlang-k](https://en.wikipedia.org/wiki/Erlang_distribution)
-  also known as (gamma (k,$\beta$)) == sum of k exponentials each with rate 1/$\beta$ (gamma (k,$\beta$)) 
- pmf:
    ### $\frac{1}{\beta^k}\frac{x^{K-1}e^{x/\beta}}{(k-1)!}=\frac{1}{\beta}\frac{(x/\beta)^{k-1}}{(k-1)!}e^{-x/\beta}$ 
- cdf: $1- e^{-x/\beta} \displaystyle\sum_{j=0}^{k-1} \frac{(x\beta)^2}{j!}$ is the sum of k interarrivals
- mean: $k\beta$
- variance: $\beta^2$
- COV(?): $\sigma = \frac{1}{\sqrt(k)}<1$
- ="stages of service" = "jump ahead k interarrivals" used to sample $k^{arrivals}$ apart

## hyper-exponential
- choosing one of *R* exponentials with rate $1/\beta_i$ with probability $P_i$   
- ### f(x)=$\displaystyle\sum_{i=1}^n \frac {P_i}{\beta_i}e^\frac{-x}{\beta_i}$
- mean:$\displaystyle\sum_{i=1}^n P_i\beta_i$  
- variance(?): $\delta >= 1$


## [Bernoulli distribution (p)](https://en.wikipedia.org/wiki/Bernoulli_distribution)
- coin toss 
- P(k)= {p,k=0 "heads }  
         {1-p, k=1 "tails }  
- mean: p -> $\bar(x)$
- variance: p(1-p)
- $\delta$: $\sqrt{(1-p)/p}$
- $\bar(x)(1-\bar(x))= S^2(n)$
## [binomial distribution(n,p)](https://en.wikipedia.org/wiki/Binomial_distribution)
 - nuber of succsess in i Bernoulli trials
 - p(k)=$n\choose{k}$ $p^k (1-p)^{n-k}$
 - mean: $np$ n trials, each with p probability
 - variance: $np(1-p)$

## [geometric distribution](https://en.wikipedia.org/wiki/Geometric_distribution)
  - number of failures before the first Bernoulli trial
  - p(k)= $(1-p^k)p$, k =0,1,...
  - mean: $\frac{1-p}{p}$
  - variance: $\frac{1-p}{p^2}$
  - MLE: $\hat{p}= \frac{1}{1+\bar{x}(n)}$
## [possion distribution](https://en.wikipedia.org/wiki/Poisson_distribution)
  - number of events in an interval(area or volume) where events are independent i.d. uniformly distributed
  - P(k)=$\frac{\lambda^k}{k!}e^-\lambda$
  - mean: $\lambda$
  - variance: $\lambda$
  - MLE: $\hat{\lambda}=\bar{x}(n)$
# Choosing distribution
 - choose
    1) pick based on on intuition or something
    2) fit based on MLE maybe
    3) check for goodness

- how to pick a distribution
    - how to pick from all the choices

        1) from outside reasoning
        2) look for characteristic values of "Point" (means, variance, COV ) statistics
            - non negative?
            - fall in range?
        3) histograms  
            a) partition frequency in each range
            b) count frequency in each range
            c) inspect histogram: what does it look like try MLE?
            d) compare visually for goodness fit
-  testing for goodness of fit   
    1) ad hoc method
        a) do key  
# 2 types of errors
- test positive: truth (unkown of hypothesis): this is a table of wherther the test was posisitive or negative, and if te hypothesis is correct or not


||+|-
|-|--------------|--------------|  
|+|true positive   (hypothesis is right and test was right) | false positive|  
|-|false negative| true negative (hypothesis was wrong, and test returned wrong| 
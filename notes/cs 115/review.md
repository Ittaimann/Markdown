# cs 115 review doc
## **Simulation must answer a question**
  - The question must drive the Simulation  
                  
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
    - monte carlo integration
    - numerical integration
    - load calculation on bridge
- deterministic
    - newtonian physics
    - long and hard composition?
    - output determined by input
- stochiastic   
    - randomness is involved. Input can vary sometimes
    - output is also randomness (this can be measured via confidence interval)
- discrete
    - in time, space, entites, events
- continous
    - motion in physics (?)
    - Things do not suddenly change, think of a gradient(?)

### simulations almost always provide an approximate answers to questions
- evaluating error is vital, owever a deterministic and discrete system can be modeled exactly, its no an approximation

- error in simulating a continous system
    - $\int_a^b \mathrm{F(x)}\mathrm{d}x$ 
    - Reimansums calculate the area under a curve via rectangles checking under the curve, and the slimmer the rectangles the better our approximation is.
    - there is some large amount of error in this though (I don't know exactly what it was cause I typed the original badly)
    - so instead we use a *trapezoidal approximation* 
        - the error is only $\alpha\frac{1}{n^2}$
    - using trapezoidal approximate and midpoint we can get a approximate error amount of $\alpha\frac{1}{n^3}$
    - Trade off here is more human work, less cpu

### [ordinary differential equations](https://en.wikipedia.org/wiki/Ordinary_differential_equation)

### Simulation of stochiastic Modes
 - sampling error, no exact right answer, all issues are caused by randomness. There is no way to directly fix this, but we can take more samples to even it all out
 - one sample tells you almost nothing, many are needed to get a good estimate and confidence
 - one simulation = "run" once run =1 sample of all stats
    - many runs to get confidence in answers (assumes no bugs)
    - ex: deterministic system, monte carlo integration

## Possion process models time of events
 - poisson process arrivals of events are distributed uniformly at random time.
 - if a system is dynamic then you need to model time, but there are 2 schools for this
    -  time driven sim, EG $\Delta$ time and a loop that iterates it. So if you had a simulation you would go literally minute by minute
    - ***Event driven***: No need to have a $\Delta$ time, as we model the next event based on when they would happen, but the moments between are discarded. Everything not directly related to the simulation, such as statistics, starting, and ending are handled outside.
## random numbers
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

### Common distributions
 - [Uniform distribution](https://en.wikipedia.org/wiki/Uniform_distribution_(continuous)) over an interval [a,b], which represents a distribution where X has equal probability of having any single value [a,b]

### multiple streams for the randomizer
 - The way most computers handle random variables means that we are going to need to seperate how we handle each random variable or stream. We shouldn't be using the same random seed for train arrivals hogouts, and everything else. We need to create multple random streams for each of these.
 - how to proberly generate random numbers:
    - way 1) generate a sequence of integers 0->n where each integer X is based on $X_{i_1}(A_{X_i}+B)$ mod MAX_UNIT->Randint(). where A, B constants are chosen very carefully. $X_0$ acts as our seed, and sequences with the same seed are equivalent.
- properties we want
 ### finite state machines
 - State diagram: a directed graph where nodes are states, and edges are events that cause state changes. Each entity has its own state diagram
 - state Diagrams: all the "action" occurs along the arrows that define events because by definition: a state is static between events, nothing happens.
    - event handling routines must handle all changes to all entites effected
### Poisson arrival process 
- We use the Exponential distribution for the arrival process, if we have an arrival rate *r* then on average r arrivals per unit time.
- Recall the poisson distribution is discrete, so the number of arrivals *k* in an interval of length 1 is 
    ### $p(k)=e^{-r}\frac{r^k}{k!}$
- thus arrival rate across interval L is lr 
- let n(t) be cumulative number of arrivals up to time t (start at t=0), so that 
    ### $P(N(T)=k)=e^{-rt}\frac{rt^k}{k!}$
- particular for k=0
    - P(N(T)=0)=$e^{-rt}$, so that $P^y$ is the probability that the first arrival is before time T is (N(T)>0)=$ 1-e^{-rt}

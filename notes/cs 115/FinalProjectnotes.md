# Final Project plans\write up
## project 1 Monte carlo vs deterministic volume integration
 - You are going to take an *n* dimension sphere and calculate the volume of the sphere where the radius is **1** 
    - so for d=1 we have a plan and its volume is 2
    - for d=2 we have $\pi r^2= \pi (1^2)= \pi$
    - for d=3 we have $4\pi r^3/3$ and so on
- monte carlo style
    - create an **n** dimensional hyper cube of length 2. plot random points within the cube and see how many fall <= to 1 from the center. 6
    - calculate to 4 digits of percision and 99% confidence
 - Cube based integration
    - subdivide the hyper cube into K segments, so that the hypercube is disected into K^d small hyper cubes.
    - this smal hyper cubes either fall in, out, or on the edge of the hyper sphere.
    - calculate to 4 digits of percision, no need for confidence,
    - MAybe ask hayes about this one, it seems like you are missing something
- part1: Push the number of dimensions up, and which method has the higher overall accuracy, what happens if we demand 8 digit precision with 99.99% confidence (he might change that and it only applies to monte carlo)
- part 2: Up the number of random value points on the monte carlo, and increase the number of hyper cubes to about the same as that number. Show the difference as a function of d. Based on part 1 which is giving the more accurate answer? 
- part 3: given a fixed value N what is the the most accurate that you can compute $\pi$? which method should you use if the N is unknown.  Think about using variance reduction techniques to increase the accuracy of your answer

### This actually doesn't seem to hard? the bigger problem is going to be the hypothetical stuff at the end where your going to need to calculate quiet a bit in order to get to a point you want.

## Project 2: numerical simulation of the ideal spring using euler (oiler), LF, and RK4
- we are integrating X(t+$\Delta=x(t)+\Delta tf(x(t))$) or in compsci terms $x_{i+1}=x_i+\Delta t*F(x_i)$ or an infinitesimal duration H that we then divide into n segments. the integration method is k, and the error of the numerical method across duration H compared to the exact solution across the same interaval scales as 1/(n^k)
- euler(oiler) is a first order method,as the time step delta T gets smaller, the solution you get from the equation differs from the exact solution, step-by-step by about (Delta T^2). 
- we need to add an intiail velocity to our intial conditions, and then eulers method becomes 
    $x_{i+1}=x_i+\Delta t*v_i$
    $v_{i+1}=v_i+\Delta t*a_i$
- now we talk about LEAP FROG which is a second order method.     $v_{0.5}=v_i+(.5)\Delta t*a_o$
- Update $x_{i+1} = x_i + Δt*v_{0.5+i}$  
    Compute $a_{i+1}$ from $x_{i+1}$  
    Update $v_{i+1.5} = v_{i+0.5} + Δt*a_{i+1}$
- RUNGE-KUTTA LOOK IT UP
- part 1: Demonstrate the orders of the above numerical integration methods. show that each one is a 1st, 2nd, and 4th order solving the spring equation F=-kx. that is x''(t)=-k*x(t). integrate from 0 to h=1. show that Delta T= H/n where n is the number of steps taken to get from t=0 to t=1. The total error goes as $\Delta t^k$ for k=1,2, and 4 respectively.
- part 2: perform an integration of duration 1000. try all three integrators and various timesteps, plot all three of them as a function of time using the timestep that appears best of all three. Which one provides the most accurate solution in the least amount of cpu time
- part 3: using all 3 integrators, try performing integrations of increasing durations 10^j for j going from 1->9. based on these plot the difference from the conservation of energy. Which one provides the best long term conservation of energy, 
### uh talk to vincent and see if you can actually understand this
## project 2
- all packets are same length 1
- assume there are n hosts that is globally known
- assume there is only one medium
- if two packets fly at the same time they collide and kill each other
- every host transmits whenever it feels like it even if another packet is in transmission
- ... how are we dealing collisions
- every packet destroyed must be retransmitted
- packets arrive globally as a poisson process at an average rate R where R is in [0,1]. 1 represents a medium that is 100% busy. each packed is assigned to transmit to host with equal probability. 
- When a packet is involved in a collision, the host that was trying to transmit the packet retries the same packet again at a later time. After waiting a random amount of time that is exponetially distributed with mean n (the rate 1/n). Bevery host had a packet to transmit, then on average one host will be trying to retransmit every 1 unity of time. 
- part 1: what is the maximum global arrival rate of packets. show this as a plot with throughput as a function of R.
- part 2: is there a better choice than 1/n for the retry rate? can we get a better R max that we found in part 1? 
- part3 : Slotted aloha, transmissions are only allowed to start at integer values of time. Redo parts 1 and 2 but for slotted aloha, in other words find R max and a different retry rate that maximizes R for slotted aloha.  
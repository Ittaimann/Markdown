# New Lecture notes 
## Bonus question on lab2 
 - look at it from the perspective of the dock
    - create a graph where x is interarrival time and y is the fraction of time not spent unloading
    - as long as the system is not overloaded, doubling the time of arrival means the doc will have twice the amount of idle time
    - and where that linear line is above a vertical line (?) then it is overloaded.
    - *Analytical sal*: assume system is grossly overloaded and compute mean unloading time
- from crews perspective
    - create a timeline of the crews in the queue. 
    - A=time train arrives to front of Q + loading dock is ready to take it.
    - A is distributed uniformly at random in the 12-hour shift
        - note that this is true even if the train is hogged out
    - 3 cases:
        1)  firsts 3 hours 1/4, crew is hogged out, and unloading time (the average) will be the average remaining crew travel time + unloading time. average crew return time is 1.5, average unload time is 4 hours, so this averages to 5.5 hours
        2) Hours 3->8 with probability 5/12, the crew is already there an there will be enough time to unload the train. unloading time is 4 hours
        3) hours 8->12 with probability 4/12, unload time + full crew travel time 3h = 7h.  
    - Average unload time = 1/4*5*5+5/12*4+1/3*7=5.375 hours = 0.186 trains/hour

## FINAL PROJECT NOTES
 - Project 1
    - compare monte carl integration to deterministic integration, and measure the dimensions of a D dimensional hyper sphere. 
    - step 0: enclose the circle in a square and sample a million points in the square and see how many are less then 1 away from the center.
    - do this with a 3d cube and sphere. 
    - uh I stopped paying a attention... um... um...Cube based integration? READ OVER AND MAYBE ASK HIM
- Project 2
    - simulation of an ideal spring 
    - do a numerical integration of euler. 
    - based on the assignment, the delta T to the k is a global error
    - second order differential equations just requires second deriviates. third means third...               
    - RK 4 is a fourth order Runge-Kutta method. 
- Project 3
    - every packet is same size 1 (b,kb,mb doesnt matter). Packets can however collide and destroy each other. 
    - because each packet is length 1 its not hard to detect a packet collision. 
            
            |----| packet 1
                |----| packet 2 
                    both are destroyed
            |---| P1
                  |---| P2 
                    pakckets transmit?                             
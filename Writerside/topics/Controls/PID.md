# PID

PID is a type of closed loop control. It stands for proportion, integral, and derivative. 

1. Proportion: Essentially it is how much to move by based on the error
2. Integral: Accumulated error over time, useful for getting to the goal after D is applied
3. Derivative: Change in error, useful to eliminate oscillations (up and down graphs)

To tune a mechanism to PID, the general rule is to use only P until oscillation occurs. Then, D is applied to smooth out the graph.
Afterward, if the goal is never reached, (I and D is not always used) I can be used to give it just enough power.

> **Warning**
>
> Start with tiny P values (0.0001) and make your way up slowly. 
> Exercise caution as to not break anything. 
>
{style="warning"}
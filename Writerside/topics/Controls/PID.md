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

## Example Graphs

![pidchangegraph.png](pidchangegraph.png)

In this example, it shows different graphs. Even though it does not show exact PID values, we can see the first graph is decent, but now D needs to be added. 
Green has too much D which causes it to be too slow getting to the setpoint. Red is what we are aiming for with a combination of D and I tuning after P alone. 

## Example Code
There are multiple classes in FRC that utilize PID, and we will show you a few examples. 

```java
// Need some code lol
```
## Further Reading
+ [PIDController](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/pidcontroller.html)
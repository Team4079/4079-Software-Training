# Types of Encoders

## Relative Encoders
Relative encoders measure position, but do not have an exact way of always knowing where it is.

## Absolute Encoders
Absolute encoders measure position, but use magnets, etc to reliably know where it is at all times. 

## Relative vs Absolute
Take an elevator for example. Using relative encoders requires that you set a certain known position as the "zero". 
Often times, this would be the hardstop at the bottom which is a reliable way to base all future measurements of the elevator off of.
> **Note**
>
> Relative encoders do not save their position and are set on deploys and reboots.
> Absolute encoders will always know their position (Unless something goes wrong then ur screwed anyway)
>
{style="note"}
With an absolute encoder, there is no need for this "zero" because all measurements will persist. 
This means that at each certain point, the value read will always be the same. 
An absolute encoder on an elevator will act similarly to a relative, except it does not need to be calibrated to a "zero" (aka hardstop) each time. 

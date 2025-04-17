# Intro To Swerve

## What is a swerve drive?

A swerve drive is a type of drivetrain that allows for omnidirectional movement. That is, it allows the driver to move it in all directions including while rotating it. This is incredibly valuable because swerve has much more maneuverability and speed compared to a tank drive which can only move forward and backward. 

## What is a swerve module?

First, imagine a shopping cart wheel or a wheel on a chair. They can move and rotate in any direction. This same concept is applied to a swerve drive. 

A swerve module is what makes up a swerve drive. There are one module on each corner of a traditional swerve drive. They contain one motor for driving and one for steering. The drive motor spins the wheel while the steering motor rotates the wheel. 

A swerve module also needs an absolute encoder. We currently used CanCoders which measure rotation. Absolute encoders, without going into too much detail, measure the rotation of the wheel. They do not reset when turned off and are extremely accurate. This makes them ideal as we can rely on them to tell us the current orientation of the wheel (whether it is forward, backwards, or some other orientation).

> **Note**
>
> Try to spin the swerve drive wheel. You will notice that the wheel will only move one motor's gears indicating that motor is the drive motor.
> Rotating the other wheel will move on the steer motor's gears indicating that motor is the steering motor.
>
{style="note"}

![Create new topic options](MK4iPhoto8_grande.png){ width=290 }{border-effect=line}

We will have guide that goes over swerve code eventually.

[Set up your project](Tank-Drive-Tutorial.md#creating-a-new-wpilib-project)
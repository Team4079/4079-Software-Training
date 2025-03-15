# Why Kotlin for FRC

**Author:** Om Gupta  
**Class:** D1 Kotlin Glazer

## Introduction

Kotlin offers several advantages over Java for FRC robotics programming. Here's why it might be a better choice for your team's codebase.

## Key Advantages

### 1. Conciseness and Readability

Kotlin's syntax is more concise than Java, which leads to fewer lines of code and improved readability. This can be very helpful in an FRC environment where you want to minimize the risk of errors and write cleaner, easier-to-maintain code. For example, Kotlin eliminates boilerplate code like getters, setters, and null checks, which can make it easier to focus on the logic of your robot.

**Kotlin example (concise):**
```kotlin
val motor = Motor(1).apply { speed = 0.5 }
```

**Java equivalent (more verbose):**
```java
Motor motor = new Motor(1);
motor.setSpeed(0.5);
```

### 2. Null Safety

Kotlin has built-in null safety, which reduces the chances of NullPointerException (a common issue in Java). In FRC, this can be particularly useful when dealing with sensors, motors, and other hardware components that may return null values under certain conditions (e.g., connection errors).

Kotlin distinguishes between nullable (?) and non-nullable types at the language level, which helps prevent null-related crashes:
```kotlin
var motor: Motor? = null  // Nullable Motor object
```

### 3. Functional Programming Features

Kotlin supports both object-oriented and functional programming paradigms. Features like lambdas, higher-order functions, and extension functions allow you to write more expressive code, which can be especially useful when working with repetitive tasks in robotics, such as event-driven programming or handling multiple subsystems.

**Example: Using lambdas for event handling in Kotlin**
```kotlin
button.whenPressed { motor.speed = 1.0 }
```

### 4. Coroutines for Concurrent Programming

Kotlin's coroutines provide a simpler way to handle asynchronous and concurrent programming compared to Java's traditional Thread model. In FRC, where managing tasks such as sensor updates, motor control, and state management concurrently is crucial, coroutines can simplify the handling of such tasks without complex threading.

**Example: Running tasks asynchronously in Kotlin**
```kotlin
GlobalScope.launch {
    // Asynchronously control robot behavior
    motor.speed = 0.5
    delay(1000)
    motor.stop()
}
```

### 5. Seamless Java Interoperability

Kotlin is fully interoperable with Java, meaning that you can use existing Java libraries, including the WPILib library that is commonly used in FRC, without any issues. If your team already has Java code, you can incrementally switch to Kotlin, or mix and match Kotlin and Java files in the same project.

Kotlin can call Java libraries or vice versa without much friction.

### 6. Type Inference

Kotlin has a powerful type inference system that reduces verbosity, allowing you to omit explicit type declarations when they can be inferred. This results in cleaner, more readable code.

**Kotlin example:**
```kotlin
val motor = Motor(1)  // Type inferred as Motor
```

**Java equivalent:**
```java
Motor motor = new Motor(1);
```

### 7. Smart Casts

Kotlin's smart casting mechanism allows for fewer explicit type checks and casts, which can simplify the control logic in FRC. If the compiler can guarantee that a variable is of a certain type, it automatically casts it, removing the need for manual casting.

**Example:**
```kotlin
if (sensor is UltrasonicSensor) {
    sensor.measure()  // No need to cast sensor to UltrasonicSensor
}
```

### 8. Better Support for DSLs (Domain-Specific Languages)

Kotlin is well-suited for building DSLs, which can make your FRC robot code more intuitive and readable. A DSL allows you to create custom language features or syntax that fit your specific domain—in this case, robot programming.

This can help create more human-readable and organized code for robot actions, trajectories, and behaviors.

## Real-World Examples

I've already translated SwerveBase into Kotlin, and it's a lot more readable. Here are some differences:

### Kotlin [SwerveModule constructor]: Repeat-proof code

```kotlin
/** Configuration for the drive motor */
val driveConfigs =
  TalonFXConfiguration().apply {
    Slot0.apply {
      kP = BasePIDGlobal.DRIVE_PID.p
      kI = BasePIDGlobal.DRIVE_PID.i
      kD = BasePIDGlobal.DRIVE_PID.d
    }
    MotorOutput.apply {
      NeutralMode = NeutralModeValue.Brake
      Inverted = SwerveGlobalValues.DRIVE_MOTOR_INVERETED
    }
  }

/** Configuration for the steer motor */
val steerConfigs =
  TalonFXConfiguration().apply {
    Slot0.apply {
      kP = BasePIDGlobal.STEER_PID.p
      kI = BasePIDGlobal.STEER_PID.i
      kD = BasePIDGlobal.STEER_PID.d
    }
    MotorOutput.apply {
      NeutralMode = NeutralModeValue.Brake
      Inverted = SwerveGlobalValues.STEER_MOTOR_INVERTED
    }
    Feedback.apply {
      FeedbackRemoteSensorID = canCoderID
      FeedbackSensorSource = FeedbackSensorSourceValue.FusedCANcoder
      RotorToSensorRatio = MotorGlobalValues.STEER_MOTOR_GEAR_RATIO
    }
    ClosedLoopGeneral.ContinuousWrap = true
  }
```

### Java [SwerveModule constructor]

```java
driveConfigs.Slot0.kP = BasePIDGlobal.DRIVE_PID.p;
driveConfigs.Slot0.kI = BasePIDGlobal.DRIVE_PID.i;
driveConfigs.Slot0.kD = BasePIDGlobal.DRIVE_PID.d;

steerConfigs.Slot0.kP = BasePIDGlobal.STEER_PID.p;
steerConfigs.Slot0.kI = BasePIDGlobal.STEER_PID.i;
steerConfigs.Slot0.kD = BasePIDGlobal.STEER_PID.d;

driveConfigs.MotorOutput.NeutralMode = NeutralModeValue.Brake;
steerConfigs.MotorOutput.NeutralMode = NeutralModeValue.Brake;

driveConfigs.MotorOutput.Inverted = SwerveGlobalValues.DRIVE_MOTOR_INVERETED;
steerConfigs.MotorOutput.Inverted = SwerveGlobalValues.STEER_MOTOR_INVERTED;

steerConfigs.Feedback.FeedbackRemoteSensorID = canCoderID;
steerConfigs.Feedback.FeedbackSensorSource = FeedbackSensorSourceValue.FusedCANcoder;
steerConfigs.Feedback.RotorToSensorRatio = MotorGlobalValues.STEER_MOTOR_GEAR_RATIO;
steerConfigs.ClosedLoopGeneral.ContinuousWrap = true;

driveConfigs.CurrentLimits.SupplyCurrentLimit = MotorGlobalValues.DRIVE_SUPPLY_LIMIT;
driveConfigs.CurrentLimits.SupplyCurrentThreshold = MotorGlobalValues.DRIVE_SUPPLY_THRESHOLD;
driveConfigs.CurrentLimits.SupplyTimeThreshold = MotorGlobalValues.DRIVE_TIME_THRESHOLD;
driveConfigs.CurrentLimits.SupplyCurrentLimitEnable = true;

steerConfigs.CurrentLimits.SupplyCurrentLimit = MotorGlobalValues.STEER_SUPPLY_LIMIT;
steerConfigs.CurrentLimits.SupplyCurrentThreshold = MotorGlobalValues.STEER_SUPPLY_THRESHOLD;
steerConfigs.CurrentLimits.SupplyTimeThreshold = MotorGlobalValues.STEER_TIME_THRESHOLD;
steerConfigs.CurrentLimits.SupplyCurrentLimitEnable = true;
```

### Kotlin [SwerveModule.getState & setState]: Getters and setters inside vars

```kotlin
/** State of the swerve module */
var state = SwerveModuleState(0.0, Rotation2d.fromDegrees(0.0))
  get() {
    field.angle = Rotation2d.fromRotations(steerMotor.position.valueAsDouble)
    field.speedMetersPerSecond =
      (driveMotor.velocity.valueAsDouble *
        (MotorGlobalValues.DRIVE_MOTOR_GEAR_RATIO / MotorGlobalValues.METERS_PER_REVOLUTION))
    return field
  }
  set(value) {
    val newPosition = position
    val optimized = SwerveModuleState.optimize(value, newPosition.angle)

    val angleToSet = optimized.angle.rotations
    SmartDashboard.putNumber(
      "desired state after optimize " + canCoder.deviceID,
      optimized.angle.rotations,
    )

    steerMotor.setControl(positionSetter.withPosition(angleToSet))

    val velocityToSet =
      (optimized.speedMetersPerSecond *
        (MotorGlobalValues.DRIVE_MOTOR_GEAR_RATIO / MotorGlobalValues.METERS_PER_REVOLUTION))
    driveMotor.setControl(velocitySetter.withVelocity(velocityToSet))

    field = value
  }
```

### Java [SwerveModule.getState & setState]

```java
private SwerveModuleState state = new SwerveModuleState(0.0, Rotation2d.fromDegrees(0.0));

public SwerveModuleState getState() {
    state.angle = Rotation2d.fromRotations(steerMotor.getPosition().getValueAsDouble());
    state.speedMetersPerSecond =
        driveMotor.getVelocity().getValueAsDouble()
            * (MotorGlobalValues.DRIVE_MOTOR_GEAR_RATIO / MotorGlobalValues.MetersPerRevolution);
    return state;
}

public void setState(SwerveModuleState state) {
 SwerveModulePosition newPosition = getPosition();
 SwerveModuleState optimized = SwerveModuleState.optimize(state, newPosition.angle);

 double angleToSet = optimized.angle.getRotations();
 SmartDashboard.putNumber(
     "desired state after optimize " + canCoder.getDeviceID(), optimized.angle.getRotations());

 steerMotor.setControl(positionSetter.withPosition(angleToSet));

 double velocityToSet =
     optimized.speedMetersPerSecond
         * (MotorGlobalValues.DRIVE_MOTOR_GEAR_RATIO / MotorGlobalValues.MetersPerRevolution);
 driveMotor.setControl(velocitySetter.withVelocity(velocityToSet));

 this.state = state;
}
```

## Conclusion

Kotlin provides numerous advantages for FRC programming, including more concise syntax, better safety features, and powerful language constructs. The real-world examples above demonstrate how Kotlin can make your robot code more readable and maintainable while reducing the potential for errors.
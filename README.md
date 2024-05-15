# Part 1: Introduction

## 1.1 What is Rose?

Rose is a programming language designed for temporal turtle graphics. It allows users to create animations by defining the movements and behaviors of "turtles" on a canvas.

## 1.2 Overview of Rose Script Authoring

Rose scripts are typically authored on PCs, using tools like the visualizer to preview and debug the animations. The scripts define how turtles move and draw on the canvas, resulting in complex animations.

# Part 2: Getting Started

## 2.1 Setting Up the Rose Scripting Environment

- **Overview:** Instructions for installing and configuring the Rose scripting environment on a PC.
- **Key Files:**
    - `README.txt`
    - `RoseConfig.S`

## 2.2 Creating Your First Rose Script

- **Overview:** Step-by-step guide to writing a basic Rose script.
- **Example:** Simple script to draw a shape.

## 2.3 Running and Previewing Rose Scripts

- **Overview:** How to use the visualizer to run and preview scripts.
- **Key Files:**
    - `visualizer/main.cpp`



# Part 3: Rose Language Fundamentals

This part covers the basic elements and syntax of the Rose scripting language, providing a foundation for writing and understanding Rose scripts. Here's a detailed outline for each subsection to ensure comprehensive coverage.

## 3.1 Script Structure

- **Overview:**
  - A Rose script is composed of various declarations, commands, and procedures that define the behavior of turtles on a canvas.
  - The script typically starts with global declarations (e.g., `form`, `fact`) followed by procedural definitions.

- **Components:**
  - **Global Declarations:** Define the canvas, constants, and color scripts.
  - **Procedures:** Contain sequences of commands that control turtle actions.

- **Example:**
  ```rose
  form 352 280 1 4
  fact maxSpeed = 5
  
  proc main
    move 10
    draw
  ```

## 3.2 Comments and Whitespace

- **Comments:**
  - Comments in Rose start with `#` and extend to the end of the line.
  - **Example:**
    ```rose
    # This is a comment
    move 10  # Move forward
    ```

- **Whitespace:**
  - Rose is whitespace-agnostic, meaning line breaks can be inserted or omitted anywhere between tokens.
  - Indentation and spaces do not affect the script’s execution but can be used for readability.

- **Example:**
  ```rose
  move 10
  turn 64
  draw
  ```

## 3.3 Identifiers and Keywords

- **Identifiers:**
  - Used for naming variables, constants, and procedures.
  - Must start with a letter and can contain letters, digits, and underscores.
  - **Example:**
    ```rose
    fact maxSpeed = 5
    proc moveForward distance
    ```

- **Keywords:**
  - Reserved words in Rose that have specific meanings.
  - Examples include `form`, `fact`, `proc`, `move`, `jump`, `turn`, etc.
  - **Example:**
    ```rose
    proc main
      move 10
    ```

## 3.4 Data Types

- **Overview:**
  - Rose primarily uses fixed-point numbers, colors, and coordinates.

### 3.4.1 Numbers

- **Fixed-point Numbers:**
  - Represented as 16.16 bits fixed-point values.
  - Can be written in decimal or hexadecimal format.
  - **Examples:**
    ```rose
    fact speed = 10.5
    fact hexValue = $00010000
    ```

### 3.4.2 Colors

- **Color Representation:**
  - Colors are specified using three-digit hexadecimal values.
  - Each digit represents red, green, and blue components respectively.
  - **Example:**
    ```rose
    0:fff  # White color
    ```

### 3.4.3 Coordinates

- **Coordinate System:**
  - The canvas is defined with an origin (0,0) at the top-left corner.
  - Coordinates are used to position turtles on the canvas.
  - **Example:**
    ```rose
    jump 50 50
    ```

## 3.5 Variables and Constants

- **Variables:**
  - Temporary and wire variables can be used within procedures to store and manipulate data.
  - **Example:**
    ```rose
    temp tempVar = 5
    wire globalVar = 10
    ```

- **Constants:**
  - Defined using `fact` and cannot be changed once set.
  - **Example:**
    ```rose
    fact maxSpeed = 5
    ```

## 3.6 Expressions and Operators

- **Expressions:**
  - Can include constants, variables, and function calls.
  - Support arithmetic, logical, and comparison operations.
  - **Example:**
    ```rose
    fact result = (speed + 5) * 2
    ```

- **Operators:**
  - **Arithmetic:** `+`, `-`, `*`, `/`
  - **Logical:** `&`, `|`
  - **Comparison:** `==`, `!=`, `<`, `<=`, `>`, `>=`
  - **Bitwise:** `<<`, `>>`, `>>>`, `><`, `><<`
  - **Negation:** `~`
  - **Conditional:** `<expression> ? <expression> : <expression>`
  - **Example:**
    ```rose
    temp tempVar = ~speed
    temp isFast = speed > maxSpeed ? 1 : 0
    ```

- **Functions:**
  - **sine:** `sine(<expression>)` computes the sine of 2π times the argument.
  - **rand:** `rand` generates a random number between 0 and 1.
  - **Example:**
    ```rose
    temp angle = sine(0.5)
    temp randomValue = rand
    ```



# Part 4: Rose Script Commands

This part covers the various commands available in Rose scripts, providing detailed explanations and examples for each command category. The commands are organized into eight subsections: Form Declaration Commands, Plan Declaration Commands, Fact Declaration Commands, Procedure Declaration Commands, Movement Commands, Drawing Commands, Control Flow Commands, and Miscellaneous Commands.

## 4.1 Form Declaration Commands

These commands define the canvas and its properties.

### 4.1.1 `form`

- **Syntax:** `form <width> <height> <layers> <colors_per_layer>`
- **Description:** Specifies the dimensions, number of layers, and colors per layer for the canvas.
- **Example:**
  ```rose
  form 352 280 1 4
  ```

### 4.1.2 `size`

- **Syntax:** `size <expression>`
- **Description:** Sets the pen size (radius) for drawing operations. This command is used within procedures.
- **Example:**
  ```rose
  proc setSize
    size 2.5
  ```

### 4.1.3 `layers`

- **Syntax:** `layers <expression>`
- **Description:** Sets the number of layers on the canvas. This is typically specified in the `form` command.
- **Example:**
  ```rose
  form 352 280 3 4  # Three layers, each with four colors
  ```

### 4.1.4 `colors_per_layer`

- **Syntax:** `colors_per_layer <expression>`
- **Description:** Sets the number of colors available in each layer. This is typically specified in the `form` command.
- **Example:**
  ```rose
  form 352 280 1 8  # One layer with eight colors
  ```



## 4.2 Plan Declaration Commands

These commands define the color script and its events, allowing you to control the timing, layering, and color transitions of your animations. The `plan` command is particularly powerful for scripting complex sequences of visual events.

### 4.2.1 `plan`

- **Syntax:** `plan <event>*`
- **Description:** Defines the main color script for the animation. The `plan` command can include multiple events such as color changes, waits, and transitions.
- **Example:**
  ```rose
  plan
    0:445
    1:D7F wait 96
    1:68F wait 96
    1:5E5 wait 96
    1:FD4 wait 84
  ```
  **Explanation:**
  - This example sets the initial color of layer 0 to `445` and layer 1 to `D7F`.
  - The color of layer 1 then transitions through several values, each followed by a `wait` command specifying the duration in frames.

### 4.2.2 `wait`

- **Syntax:** `wait <expression>`
- **Description:** Pauses the script for a specified number of frames before continuing with the next event. This is essential for timing events within the color script.
- **Example:**
  ```rose
  plan
    0:445
    wait 50
    1:D7F
  ```
  **Explanation:**
  - This example changes the color of layer 0 to `445`, waits for 50 frames, and then changes the color of layer 1 to `D7F`.

### 4.2.3 `time`

- **Syntax:** `time <expression>`
- **Description:** Sets a specific time for an event within a color script. This is used to synchronize events precisely.
- **Example:**
  ```rose
  plan
    time 50 0:FFF
    time 100 1:000
  ```
  **Explanation:**
  - This example sets the color of layer 0 to `FFF` at time 50 and the color of layer 1 to `000` at time 100.

### 4.2.4 `layer`

- **Syntax:** `layer <expression>`
- **Description:** Specifies a layer for subsequent color events. This is useful when you need to control multiple layers independently within the same plan.
- **Example:**
  ```rose
  plan
    layer 1 0:0ff
    wait 20
    layer 2 1:ff0
  ```
  **Explanation:**
  - This example sets the color of layer 1 to `0ff`, waits for 20 frames, and then sets the color of layer 2 to `ff0`.

### 4.2.5 `color`

- **Syntax:** `color <tint>:<color>`
- **Description:** Sets a specific tint to a color in the color script. This directly assigns a color value to a layer.
- **Example:**
  ```rose
  plan
    0:FFF
    1:D7F
  ```
  **Explanation:**
  - This example sets the color of layer 0 to `FFF` and layer 1 to `D7F`.

### 4.2.6 `movement`

- **Syntax:** `movement <identifier>`
- **Description:** Inserts events from a named movement look. This allows for modular and reusable code within your plans.
- **Example:**
  ```rose
  look start
    0:FFF wait 10
    1:000 wait 10

  plan
    movement start
  ```
  **Explanation:**
  - This example defines a look named `start` with a sequence of color changes and waits.
  - The `plan` then includes this look using the `movement` command, inserting the events from `start`.

### Expanded Examples

#### Example 1: Complex Color Transition

```rose
plan
  0:123 wait 10
  1:456 wait 20
  2:789 wait 30
  3:ABC wait 40
  0:DEF wait 50
  1:012 wait 60
  2:345 wait 70
  3:678
```
**Explanation:**
- This plan transitions through various colors across four layers, each layer waiting a different amount of time before changing color.

#### Example 2: Synchronizing Events with Music

```rose
plan
  time 0 0:FFF
  time 96 1:D7F
  time 192 1:68F
  time 288 1:5E5
  time 384 1:FD4
```
**Explanation:**
- This plan uses the `time` command to precisely control color changes, which is useful for synchronizing with a music track.

#### Example 3: Using Layers and Colors

```rose
plan
  layer 0 0:AAA
  wait 10
  layer 1 1:BBB
  wait 10
  layer 2 2:CCC
  wait 10
  layer 3 3:DDD
```
**Explanation:**
- This plan demonstrates setting colors on different layers, each followed by a wait to control the timing of the transitions.

 

## 4.3 Fact Declaration Commands

These commands define constants in Rose scripts.

### 4.3.1 `fact`

- **Syntax:** `fact <identifier> = <expression>`
- **Description:** Defines a global constant that cannot be changed.
- **Example:**
  ```rose
  fact maxSpeed = 5
  ```

### 4.3.2 `const`

- **Syntax:** `const <identifier> = <expression>`
- **Description:** Similar to `fact`, used to define a constant.
- **Example:**
  ```rose
  const maxHeight = 200
  ```

## 4.4 Procedure Declaration Commands

These commands define procedures and their parameters.

### 4.4.1 `proc`

- **Syntax:** `proc <name> <param>* <statement>*`
- **Description:** Defines a procedure with a name, parameters, and a series of statements.
- **Example:**
  ```rose
  proc moveForward distance
    move distance
    draw
  ```

### 4.4.2 `param`

- **Syntax:** `param <name> <expression>`
- **Description:** Defines a parameter for a procedure.
- **Example:**
  ```rose
  proc drawCircle radius
    size radius
    draw
  ```

### 4.4.3 `return`

- **Syntax:** `return <expression>`
- **Description:** Returns a value from a procedure.
- **Example:**
  ```rose
  proc calculateArea radius
    return (radius * radius * 3.1415)
  ```

## 4.5 Movement Commands

These commands control the movement of turtles.

### 4.5.1 `move`

- **Syntax:** `move <expression>`
- **Description:** Moves the turtle forward by a specified number of pixels.
- **Example:**
  ```rose
  move 10
  ```

### 4.5.2 `jump`

- **Syntax:** `jump <x_expression> <y_expression>`
- **Description:** Jumps the turtle to a specific pixel coordinate.
- **Example:**
  ```rose
  jump 50 50
  ```

### 4.5.3 `turn`

- **Syntax:** `turn <expression>`
- **Description:** Turns the turtle clockwise by a specified number of degrees (256-on-a-circle).
- **Example:**
  ```rose
  turn 64
  ```

### 4.5.4 `face`

- **Syntax:** `face <expression>`
- **Description:** Sets the turtle's direction to a specified number of degrees clockwise from horizontal right.
- **Example:**
  ```rose
  face 128
  ```

## 4.6 Drawing Commands

These commands control the drawing actions of turtles.

### 4.6.1 `size`

- **Syntax:** `size <expression>`
- **Description:** Sets the pen radius in pixels (rounded to the nearest integer-and-a-half).
- **Example:**
  ```rose
  size 2.5
  ```

### 4.6.2 `tint`

- **Syntax:** `tint <expression>`
- **Description:** Sets the current tint (rounded down to an integer).
- **Example:**
  ```rose
  tint 3
  ```

### 4.6.3 `draw`

- **Syntax:** `draw`
- **Description:** Draws a circular dot at the turtle's current position.
- **Example:**
  ```rose
  draw
  ```

### 4.6.4 `plot`

- **Syntax:** `plot`
- **Description:** Draws a square dot at the turtle's current position.
- **Example:**
  ```rose
  plot
  ```

## 4.7 Control Flow Commands

These commands control the flow of execution in Rose scripts.

### 4.7.1 `wait`

- **Syntax:** `wait <expression>`
- **Description:** Waits a specified number of frames.
- **Example:**
  ```rose
  wait 20
  ```

### 4.7.2 `fork`

- **Syntax:** `fork <procedure> <expression>*`
- **Description:** Creates a new turtle with the current state, running the specified procedure with the given arguments.
- **Example:**
  ```rose
  fork moveForward 15
  ```

### 4.7.3 `temp`

- **Syntax:** `temp <variable> = <expression>`
- **Description:** Assigns a value to a local variable.
- **Example:**
  ```rose
  temp tempVar = 5
  ```

### 4.7.4 `wire`

- **Syntax:** `wire <variable> = <expression>`
- **Description:** Assigns a value to a global variable inherited through forks.
- **Example:**
  ```rose
  wire globalVar = 10
  ```

### 4.7.5 `seed`

- **Syntax:** `seed <expression>`
- **Description:** Seeds the random number generator.
- **Example:**
  ```rose
  seed 1234
  ```

### 4.7.6 `when`

- **Syntax:** `when <expression> <statement>* done`
- **Description:** Conditionally executes a block of statements if the expression is non-zero.
- **Example:**
  ```rose
  when x > 10
    move 5
  done
  ```

### 4.7.7 `defy`

- **Syntax:** `defy`
- **Description:** Suppresses warnings for the current source line.
- **Example:**
  ```rose
  defy
  ```

## 4.8 Miscellaneous Commands

These commands provide additional functionality in Rose scripts.

### 4.8.1 `print`

- **Syntax:** `print <expression>`
- **Description:** Outputs the value of an expression (if supported by the visualizer).
- **Example:**
  ```rose
  print "Hello, World!"
  ```

### 4.8.2 `assert`

- **Syntax:** `assert <expression>`
- **Description:** Asserts that an expression is true, and may halt execution if it is not.
- **Example:**
  ```rose
  assert x > 0
  ```

### 4.8.3 `halt`

- **Syntax:** `halt`
- **

Description:** Halts the execution of the script.
- **Example:**
  ```rose
  halt
  ```

# Part 5: Advanced Rose Scripting Techniques

## 5.1 Procedural Generation

Procedural generation in Rose scripting involves creating complex patterns and animations by writing procedures that use recursion, loops, and conditional logic. This technique allows you to generate intricate designs and dynamic behaviors efficiently.

### Overview

Procedural generation techniques leverage the ability of Rose scripts to define and call procedures recursively, creating self-similar structures and animations. By using variables and conditions, you can control the depth and complexity of the generated patterns.

### Key Concepts

- **Recursion:** A procedure that calls itself to create repeating patterns.
- **Loops and Conditionals:** Using `when` and `fork` statements to control the flow of execution and generate iterative designs.
- **Dynamic Variables:** Utilizing `temp` and `wire` to manage state across recursive calls and iterations.

### Examples

#### Recursive Animation: Circle Pattern

The `circle.rose` script demonstrates how to use recursion to create a circular pattern. The main procedure sets up the initial state and forks a new turtle running the `circle` procedure.

**Script: `circle.rose`**

```rose
part "rose_config.rose"

fact radius = 50

proc main
  jump 100 100
  size radius
  tint 3
  draw
  turn 45
  fork circle 45 10  # Start the recursive pattern

proc circle b n
  draw
  move 2
  turn b
  wait 0.5
  when n > 0
    fork circle b n-1
  done
```

**Explanation:**
- **`main`:**
  - Moves the turtle to coordinates (100, 100).
  - Sets the pen size to `radius` and tint to 3.
  - Draws a dot and turns 45 degrees.
  - Forks a new turtle running `circle` with parameters `b = 45` and `n = 10`.
- **`circle`:**
  - Draws a dot, moves forward by 2 pixels, and turns `b` degrees.
  - Waits for 0.5 frames.
  - If `n` is greater than 0, forks a new turtle running `circle` with `n` decremented by 1.

#### Iterative Animation: Bouncing Ball

The `ball.rose` script shows how to use loops and conditionals to create an animation of a bouncing ball. The `ball` procedure changes the position of the turtle, draws the ball, and then recursively forks itself to create a continuous animation.

**Script: `ball.rose`**

```rose
form 352 240 1 4

fact ballRadius = 20
fact ballColor = 2

proc main
  turn 45
  move 100
  turn 180
  move 100
  fork ball  # Start the bouncing ball animation

proc ball
  tint ballColor
  size ballRadius
  draw
  move 10
  wait 1
  turn 15
  fork ball  # Continue the animation
```

**Explanation:**
- **`main`:**
  - Turns the turtle 45 degrees and moves forward by 100 pixels.
  - Turns the turtle 180 degrees and moves forward by 100 pixels.
  - Forks a new turtle running `ball` to start the animation.
- **`ball`:**
  - Sets the tint to `ballColor` and size to `ballRadius`.
  - Draws a dot, moves forward by 10 pixels, waits for 1 frame, and turns 15 degrees.
  - Forks a new turtle running `ball` to continue the animation.

#### Complex Procedural Patterns: Starburst

The following example demonstrates a more complex procedural pattern, creating a starburst effect using multiple recursive forks.

**Script: `starburst.rose`**

```rose
form 352 240 1 4

fact numRays = 8
fact rayLength = 50

proc main
  jump 176 120  # Center of the canvas
  fork rays numRays rayLength

proc rays n length
  when n > 0
    turn 360 / numRays
    fork ray length
    fork rays n-1 length
  done

proc ray length
  move length
  draw
  move -length
```

**Explanation:**
- **`main`:**
  - Moves the turtle to the center of the canvas.
  - Forks a new turtle running `rays` with `numRays` and `rayLength` as parameters.
- **`rays`:**
  - If `n` is greater than 0, turns the turtle by an angle calculated as `360 / numRays`.
  - Forks a new turtle running `ray` with `length` as a parameter.
  - Forks itself with `n` decremented by 1.
- **`ray`:**
  - Moves the turtle forward by `length`, draws a dot, and then moves back by `length`.
 
## 5.2 Animations and Transitions

- **Overview:** How to create smooth animations and transitions.

## 5.3 Interaction and User Input

- **Overview:** Handling user interactions and input in Rose scripts.

## 5.4 Syncing with Music

- **Overview:** Techniques for synchronizing animations with music.

## 5.5 Optimizing Performance

- **Overview:** Tips and techniques for optimizing the performance of Rose scripts.

# Part 6: Example Rose Scripts

## 6.1 Basic Shapes and Patterns

- **Example:** Simple scripts to create basic shapes and patterns.

## 6.2 Animated Scenes

- **Example:** Scripts for creating animated scenes.

## 6.3 Interactive Visualizations

- **Example:** Scripts for creating interactive visualizations.

## 6.4 Generative Art

- **Example:** Scripts for creating generative art.

## 6.5 Music Visualizers

- **Example:** Scripts for creating music visualizers.

# Part 7: Appendices

## 7.1 Rose Language Quick Reference

- **Overview:** A quick reference guide for the Rose language syntax and commands.

## 7.2 Frequently Asked Questions (FAQ)

- **Overview:** Answers to common questions about Rose scripting.

## 7.3 Troubleshooting Guide

- **Overview:** Solutions to common issues encountered while scripting with Rose.

## 7.4 Additional Resources and Community

- **Overview:** Links to additional resources and community forums for Rose scripting.
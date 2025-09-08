03-08-2025  16:28

Status:

Tags: [[Machine Learning]] [[Maths for Machine Learning]]

Pages: 19 - 22
# Systems of Linear Equations

## What is a Linear Equation?

-> In mathematics, a linear equation is an equation that may be put in the form ${\displaystyle a_{1}x_{1}+\ldots +a_{n}x_{n}+b=0,}$ 
where ,
${\displaystyle x_{1},\ldots ,x_{n}}$ are the variables (or unknowns), and 
${\displaystyle b,a_{1},\ldots ,a_{n}}$ are the coefficients, which are often real numbers.

-> The coefficients may be considered as parameters of the equation and may be arbitrary expressions, provided they do not contain any of the variables.

https://en.wikipedia.org/wiki/Linear_equation


## System of Linear Equation

-> System of linear equations (or linear system) is a collection of two or more linear equations involving the same variables.

->For example,
${\displaystyle {\begin{cases}3x+2y-z=1\\2x-2y+4z=-2\\-x+{\frac {1}{2}}y-z=0\end{cases}}}$ 
is a system of three equations in the three variables x, y, z.

-> A solution to a linear system is an assignment of values to the variables such that all the equations are **simultaneously satisfied**.

-> In the example above, a solution is given by the ordered triple ${\displaystyle (x,y,z)=(1,-2,-2),}$ since it makes all three equations valid.

https://en.wikipedia.org/wiki/System_of_linear_equations


## Geometric Interpretation of Systems of Linear Equations

-> In a system of linear equations with two variables ${\displaystyle x_{1}, x_{2}}$ , each linear equation defines a line on the $x_1 x_2$-plane.

-> Since a solution to a system of linear equations must satisfy all equations simultaneously, the solution set is the intersection of these lines.

-> This intersection set can be a line (if the linear equations describe the same line), a point, or empty (when the lines are parallel).

-> Example,
An illustration for this system of linear equation is,
$x - y = -1$
$3x + y = 9$

![[Pasted image 20250803165039.png]]

where the solution space is the point $(x , y) = (2, 3)$.


## Compact Notation

-> For a systematic approach for solving a system of linear equations, we can store the coefficients into vectors and collect those vectors into the matrices.

-> Example,
$2x - y = 0$
$-x + 2y = 3$

$x\begin{bmatrix}2 \\ -1\end{bmatrix} + y\begin{bmatrix}-1 \\ 2\end{bmatrix} = \begin{bmatrix}0 \\ 3\end{bmatrix}$

$\begin{bmatrix}2 & -1 \\ -1 & 2\end{bmatrix} \begin{bmatrix}x \\ y\end{bmatrix} = \begin{bmatrix}0 \\ 3\end{bmatrix}$





# References

Download Link: https://assignmentchef.com/product/solved-math567-homework-5
<br>
1.   Conjugate gradients

(a)    Implement the conjugate gradient (CG) method given on page 87 of the textbook. Replace the termination criteria “if krkk is less than some tolerance then stop” with “if krkk2 &lt; tolkfk2 then stop”, where tol is a user input parameter. Your code should be written as a function that can called with any symmetric positive definite matrix A, right hand side b, and tolerance. Turn in a listing of your code.

(b)   Use your code from part (a) to (approximately) solve the model problem from problem 2 of homework 4,

∇2u(x,y) = 10π2esin(2π(x+2y))(−2sin(2π(x + 2y)) + cos(4π(x + 2y)) + 1)

(1) u(x,y) = esin(2π(x+2y)) for (x,y) ∈ ∂Ω,

using the second-order accurate finite difference method. Use m = 27 − 1 and tol = 10−8 in your CG code and plot the error in the solution you obtain to the model problem. Report the number of iterations your code takes to converge, the time it takes to run, and the norm of the final residual when the solution converged. Compare the timing of your code to the SOR method from the previous homework (run with the same tolerance).

(c)    Extra credit (5 points): Implement a specific CG algorithm for the model problem that does not involve constructing the A matrix.

2.   Cell-centered Poisson solver So far we have focused on so called vertex-centered finite difference methods for solving boundary value problems like the Poisson equation. For the unit square Ω = [0,1] × [0,1], these methods use the grid (xj,yk) = (jh,kh), j,k = 0,1,…,m + 1, with h = 1/(m+1). Another strategy that is often used (especially in finite volume methods) is to use a cellcentered grid. For these methods the grid over the unit square is (xj,yk) = ((j−1/2)h,(k−1/2)h), j,k = 1,…,m, with h = 1/m. The figure below illustrates this grid for the case of m = 8. The solid red dots mark the grid locations where the unknowns ujk are to be determined.

One big difference between the vertex-centered and cell-centered approaches is that for the latter there are no grid points on the boundary of the domain, which means Dirichlet boundary conditions have to be handled differently.

Consider the Poisson problem with mixed boundary conditions

(2)

In this problem you will develop a second-order accurate finite difference method for solving this problem. Note that the exact solution to this Poisson problem is u(x,y) = cos(5πx)sin(3πy).

(a)    Suppose you want to solve u00(y) = f(y), 0 ≤ y ≤ 1, with u(0) = α1, u(1) = α2 on a cellcentered grid yk = (k − 1/2)h, k = 1,…,m, h = 1/m. Use the fictitious point method (see homework 3) to develop a second-order accurate approximation to this problem. State the discretization of the boundary value problem at the interior points yk, k = 2,…,m − 1, and at the boundary points y1 and ym. You don’t need to write any code here.

(b)   Suppose you want to solve u00(x) = f(x), 0 ≤ x ≤ 1, with u0(0) = β1, u0(1) = β2 on a cellcentered grid xk = (k −1/2)h, k = 1,…,m, h = 1/m. Similar to part (a), develop a secondorder accurate approximation to this problem using the fictitious point method. Again, state the discretization of the boundary value problem at the interior points xk, k = 2,…,m − 1, and at the boundary points x1 and xm. You don’t need to write any code here.

(c)    Using the results from part (a) and (b), develop a second-order accurate approximation for solving the Poisson problem (2). Write a code to solve this problem and demonstrate that your code produces a second-order accurate approximation by some means. Produce a plot of the error in your solution for m = 128. You can use whatever method you want to solve the linear system that arises for solving this boundary value problem (e.g. SOR, Conjugate Gradient, Direct sparse solver, FFT based solver, block Thomas, Bartels-Stewart, etc.)

3.   Linear multi-step methods The following are six suggestions for linear multistep methods for solving the initial value problem y0 = f(t,y(t)), a ≤ t ≤ b, y(a) = y0:

Here k is the time-step, i.e. k = (b − a)/N for some positive integer N.

The (incomplete) table below summarizes their properties. Complete the missing entries of this table (you need not supply any derivations), draw the corresponding stencil, state the generating polynomials ρ(w) and σ(w), and state the number of steps r.

2

casechar. eq

roots

stab-accu-consis-leadingconver-

ilityracytencyerror termgence(a)w2 −

= 0

Yes0

(b)

0No

No(c)

Yes

Yes(d)

3

Yes(e)w4 −

6

(f)

2Yes

4.   Predictor-Corrector method

(a)    Implement a function in the language of your choosing for numerically solving the general vector-valued IVP

y0 = f(t,y),        a ≤ t ≤ b,          y(a) = y0 (y ∈Rn),

using the fourth-order, predictor-corrector method of AB4 (4-step method) and AM4 (3-step method):

y                                                                                    )] (AB4 predictor)

y         )] (AM4 corrector)

j = 3,4,…,N − 1 .

Your function should be called abm4, and take as input a function that represents the vectorvalued function f(t,y), a, b, the initial condition y0, and the number of steps to take N. The output of your function should be a vector t containing all of the time-steps, and a matrix y containing the numerical solution of all the components of the system y at each time-step.

You will need to obtain the three values y1, y2, and y3 to get your abm4 function started. These values should be obtained with a fourth-order accurate method to keep the scheme consistent. The easiest approach is to use the standard fourth-order Runge-Kutta method (see Example 5.13 on p. 126 of the book).

Turn in a printed listing and e-mail me your program(s).

Note: Your function must be entirely general. This means that I should be able to create my own function for any f(t,y), the values a, b, and y0, and use your program abm4 to try and solve the problem. Furthermore, your program should minimize the number of times the function f(t,y) needs to be called.

(b) Consider the initial value problem

,

where the exact solution is y(t) = ttan(log(t)). Use your abm4 method from part (a) to numerically solve this IVP for 1 ≤ t ≤ 3 for the different N values [50,100,200,400]. Compute the error in the numerical solution at t = 3 and make either a table or a graph clearly showing fourth-order convergence of the solution. On a single graph, plot the solution for N = 100 over the interval 1 ≤ t ≤ 3.
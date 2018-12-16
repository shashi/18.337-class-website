KIB is a framework to run immersed boundary fluid dynamics simulation in two dimensions with rigid bodies whose motion is prescribed. See the attached presentation and the following references for details about immersed boundary simulations:

- Bao et al., J. Comp. Phys. 347 (2017).
- Griffith et al., J. Comp. Phys. 208 (2005).
- Kallemov  et al., Comm. in Appl. Math. and Comp. Science, 11 (2016).

However, there are a few differences between this package and the algorithms detailed in the literature above. First, in KIB, boundary conditions are implemented via ghost cells and are not dealt with explicitly in the matrix computations. Second, no-slip boundary conditions are available instead of only periodic boundary conditions. Third, the nonlinear term in the Navier-Stokes equation is dealt with via Picard iteration as opposed to an explicit approximation.

-----------------------

The code in KIB.jl is broken up into several parts:
1) Structure definitions
2) Helper functions
3) Operator functions
4) Temporal Integrator

Structure definitions
	Defines the types that hold information about the discretized grids and physical constants

Helper functions
	Functions that aid with indexing as well as the "kernel" used in the spreading operators

Operator functions
	Functions that represent the discrete gradient, the discrete laplacian, and the spreading
	operators between the Eulerian and Lagrangian grids.

Temporal integrator
	The main function. The "integrate" function constructs the set of (implicit) equations to be solved 
	using the above operators and solves them via a Krylov subspace method. For Picard iteration, several
	iterations of solves are performed. Thus, the integrate function solves for object and fluid 
	motion, as well as the associated pressure and force fields, as a function of time.

-----------------------

An example file, "example.jl" is included to demonstrate how objects are constructed and how a simulation is performed as well as a simple visualization of fluid flow using the Plots package.

-----------------------

Future improvements should involve optimizing the iterative solver (i.e., testing different preconditioners) and optimizing the efficiency of certain frequently called functions.

Required packages:
- LinearMaps (2.2.2)
- IterativeSolvers (0.8.0)
- Statistics
- Plots (0.21.0)
- PyPlot (2.6.3)

This code was tested using Julia 1.0.0 and the versions of the packages listed here.
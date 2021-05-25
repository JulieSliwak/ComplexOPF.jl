# ComplexOPF.jl

J. Sliwak, M. Ruiz, M. F. Anjos, L. Létocart et E. Traversi, "A julia module for polynomial optimization with complex variables applied to optimal power flow," dans 2019 IEEE Milan PowerTech, June 2019, p. 1-6


## A Julia module to construct OPF problems
We have defined a generic structure where the user can define network elements himself.
The network =  a set of buses plus a set of links between buses. Several elements can be associated to each bus and to each link.

A bus element of the power network is defined by specifying:
* the variables this element needs
* its contribution into the power balance
* the constraints associated with this element
* its contribution into the cost function

A link element is defined by specifying:
* the variables this element needs
* the power at the origin of the link
* the power at the destination of the link
* the constraints associated with this element
* its contribution into the cost function

Input data:
* Matpower format
* Grid Optimization competition format

This module is based on the package MathProgComplex.jl. The OPF problems are first constructed with complex variables and then converted into real variables using rectangular form.

Example:
```
typeofinput = MatpowerSimpleInput
   OPFpbs = load_OPFproblems(typeofinput, matpower_instance_path)
   # Bulding optimization problem
   pb_global = build_globalpb!(OPFpbs)
   pb_global_real = pb_cplx2real(pb_global)
   export_to_dat(pb_global_real, output_path, filename="$(instance_name).dat")
```

# Finite element simulation of the 3D printing of scaffolds

This repository includes a numerical framework for the 3D printing simulation of hydrogel scaffolds.
The available .inp files are compatible with ABAQUS finite element software

<img width="700" alt="3Dprint" src="https://user-images.githubusercontent.com/95075305/197178767-0dbb6cb3-8fa2-4f3c-aab3-7ba99f1dba92.gif">


```bash
├── geometry
│   ├──  geometry_meshed.inp   ----->  nodal coordinates, nodal conections, node and element
│   │                                  set and surface definition
├── constitutive model
│   ├── umat_yeoh_visco_m.for  ----->  UMAT file with the visco-hyperelastic constitutive model
│   │                                   (Yeoh model with the generalized maxwell model)
│   ├── PARAM_UMAT.for   ----------->  file with parameters for the UMAT
│   ├── fibers1.inp   -------------->  files to define the 1st family of fibers orientation (currently not in use)
│   ├── fibers2.inp   -------------->  files to define the 2nd family fibers orientation (currently not in use)
├── print_10mmps  ------------------> ABAQUS steps to 'print' at 10mm/s
│   ├── step1.inp
│   ├── step2.inp
│   ├── step3.inp
│   ├── step4.inp
│   ├── step5.inp
├── print_5mmps  ------------------> ABAQUS steps to 'print' at 5mm/s
│   ├── step1.inp
│   ├── step2.inp
│   ├── step3.inp
│   ├── step4.inp
│   ├── step5.inp
└── .gitignore
```

To run the simulation, add all the files to a directory (choose only one of the printing speeds) and
run the steps in sequence, with the commands:

```abaqus job=step1 user=umat_yeoh_visco_m.for cpus=cpus_number```

wait to finish before running step2

```abaqus job=step2 oldjob=step1 user=umat_yeoh_visco_m.for cpus=cpus_number```

repeat until step5

###### Note: the files fibers1.inp and fibers2.inp need to be in the directory although they are not influencing the material model


## Geometry and Boundary Conditions

- The geometry represents a 4 layer scaffold, with a filament of 0.2mm, 6 filaments per layer and pore size of 0.8mm. Overall, a 5x5x0.8mm scaffold.
- The mesh includes 2255044 cubic finite elements (C3D8H)
- The nodes in red are fixed in the three directions

<img width="862" alt="geometry" src="https://user-images.githubusercontent.com/95075305/197171755-4a2cc10b-e6cd-434b-9db1-945690ba0625.png">

## 3D printing simulation

The material deposition is simulated using the ABAQUS *Model Change option, which allows to add element sets during the simulation.
We divided each filament into 5 element sets and added each one in a different step. The only considered load is the self-weigh, which actuates
almost immedialy after the element deposition.

The printing velocity is defined by the timing of the addition of each filament element section.

This simulation allows to predict the deformations that can arise due to the printing process of bioinks, such as hydrogels. These deformations can  be significative and have an impact in the overall mechanical properties of the final configuration. This tool can be used as a predictive tool to choose the best printing speed and printing sequence, in terms of minimizing unwanted deformations.

The submitted files within the folder print_10mmps or print_5mmps can be easily changed to consider different printing velocities. We hope this tool will facilitate future analysis and can serve as a starting point for researchers, to further improve this work.


###### Please, cite this notebook if you use it withiin your research


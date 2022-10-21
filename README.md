# Finite element simulation of the 3D printing of scaffolds

This repository includes a numerical framework for the 3D printing simulation of hydrogel scaffolds.
The available .inp files are compatible with ABAQUS finite element software

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


## Geometry

The geometry represents a 4 layer scaffold, with a filament of 0.2mm, 6 filaments per layer and pore size of 0.8mm. Overall, a 5x5x0.8mm scaffold.

[scaffold_BC.pdf](https://github.com/mcpvilapouca/alginate-scaffold-3Dprint/files/9837986/scaffold_BC.pdf)

# Finite element simulation of scaffold 3D print

This repository includes a numerical framework for the 3D printing simulation of hydrogel scaffolds.
The available .inp files are compatible with ABAQUS finite element software


```bash
├── geometry
│   ├──  geometry_meshed.inp
├── constitutive model
│   ├── umat_yeoh_visco_m.for
│   ├── PARAM_UMAT.for
│   ├── fibers1.inp
│   ├── fibers2.inp
├── print_10mmps
│   ├── step1.inp
│   ├── step2.inp
│   ├── step3.inp
│   ├── step4.inp
│   ├── step5.inp
├── print_5mmps
│   ├── step1.inp
│   ├── step2.inp
│   ├── step3.inp
│   ├── step4.inp
│   ├── step5.inp
└── .gitignore
```

|--- geometry ------------> includes the .inp with the nodal coordinates, nodal conections, node and element set and surface definition
|
|--- constitutive model --> includes the UMAT file with the visco-hyperelastic constitutive model (Yeoh model with the generalized maxwell model)
|
|--- print_10mmps --------> includes the .inp files with the ABAQUS step definition to 'print' at 10mm/s
|
|--- print_5mmps ---------> includes the .inp files with the ABAQUS step definition to 'print' at 5mm/s

To run the files, create a directory and add all the .inp files (choose only one of the printing speeds).

Run in sequence, with the commands:

```abaqus job=step1 user=umat_yeoh_visco_m.for cpus=cpus_number```

wait to finish before running step2

```abaqus job=step2 oldjob=step1 user=umat_yeoh_visco_m.for cpus=cpus_number```

repeat until step5


## Geometry
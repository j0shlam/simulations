# [mehringer_etal_2020](https://www.sciencedirect.com/science/article/pii/S266638642100028X?via%3Dihub)   

# forcefield prep
mehringer uses AMBER03 FF with modifications, the modifications by mehringer (2020) follows as below:

## [meagher_etal_2002](https://onlinelibrary.wiley.com/doi/10.1002/jcc.10262) 

**Development of polyphosphate parameters for use with the AMBER force field**

Meagher (2003) produced new parameters for AMBER 94/99 as original AMBER parameters for monopohsphates did not extend well to polyphorylated molecules such as ATP. Also noted that the new parameters are in excellent agreement with CHARMM by Meagher. 

## [steinbrecher_etal_2012](https://pubs.acs.org/doi/pdf/10.1021/ct300613v)  

**Revised AMBER parameters for bioorganic phosphates**

Steinbrecher (2012) reported changing the phosphate oxygen radii (manipulating the VDW radii to shield the electrostatic interactions with water) prevented the water from getting too close to the oxygen atoms reducing problems from overly strong electrostatic interactions and oversolvation. This also reproduced experimental data such as solvation free energies.

| radius | $\epsilon$ $_{lj}$ | $r_{orig}$ | $r_{opt}$ |
|-  | - | -| -|
| r(OP) | 0.2100 | 1.6612 | 1.7493 | 
| r(OQ) | 0.2100 | 1.7210 | 1.8091 |
| r(OR) | 0.1700 | 1.6837 | 1.7718 |

## Leontyev_etal_[2011](https://doi.org/10.1039/C0CP01971B) and [2010](https://pubs.acs.org/doi/pdf/10.1021/ct9005807) 

**Electronic Continuum Model for Molecular Dynamics, Simulations of Biological Molecules and Accounting for electronic polarization in non-polarizable force fields**

Exaggerated electrostatic interactions in MD between ionized groups by a factor or 2. Leontyev states the charges of ionized groups and ions should be scaled by 0.7 which results in significant changes in protein dynamics. 

# mehringer ATP aggregation simulation 
10x10x10 nm\$^3$ box over 50ns for concentrations of 100,200,300 and 400 mM ATP. For the determination of the potential of mean force, the dimensions of the boxes are 4x4x4. (50mM ATP equals 2 ATP molecules in box.)

##### Other MD NOTES
###### md notes from paper - cutoff of 1.4nm, v-rescale (300K), Parrinello-Rahman barostat (1bar). AmberFF03 and tip4p2005. 
###### md notes from SI - gromacs for simulations and trajectory analysis. For the ATP, modified charge parameter, steinbrecher. Sodium Ion parameters developed by [Horinek_etal_2009](https://aip.scitation.org/doi/pdf/10.1063/1.3081142). Tip4p2005 for description of solvent. Energy minimized by l-bfgs minimization alogrithm. Cutoff of LJ and Coulombic of 0.85nm.
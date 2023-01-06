# pandey_et_al_2022
## overview 
Reproduction of MD ATP and ATP Pyrene simulation from *pandey et al (2022)*'s work. (https://pubs.acs.org/doi/full/10.1021/acs.jpcb.2c06077)
| System | ATP | Mg 2+ | Pyrene | NA + | CL -  | Simulation time (ns) | replicas |
|-  | - | -| -| - | - | - | - |
| ATP | 30 | 30 | 0 | 68 | 8 | 1000| 1 |
| ATP & pyrene  | 30 | 30 | 10 | 68 | 8 | 1000 | 3 |

# files
* `forcefield.ff` - CHARMM36 forcefield 
* atp_pan
   * `old_topol.top` - original topology file without modified nucleotide charges
   * `atp.pdb` - ATP PDB sourced from CHARMM-GUI Archive - Small molecule database: https://charmm-gui.org/?doc=archive&lib=csml

# ATP simulation
* `gmx insert-molecules -ci atp.pdb -o atp_30box.pdb -box 5 5 5 -nmol 30`
* `gmx pdb2gmx -f atp_30box.pdb -o atp30_pro.gro -water tip3p`
# modified nucleotide charges (charmm36)
charges required to be scaled within `topol.top`: 

| nr | type | resnr | residue | atom | cgnr  | charge | mass |
|-  | - | -| -| - | - | - | - |
| 28 | CN8B | 1 | ATP | C5' | 5 | -0.08 | 12.011 |
| 28 new charge | CN8B | 1 | ATP | C5' | 5 | -0.048 | 12.011 |

This is performed for all cgnr groups of multiple of 5s. (this represents the phosphate group) 



# ATP Pyrene Simulation

# pandey_et_al_2022
## overview 
Reproduction of MD ATP and ATP Pyrene simulation from *pandey et al (2022)*'s work. (https://pubs.acs.org/doi/full/10.1021/acs.jpcb.2c06077)
| System | ATP | Mg 2+ | Pyrene | NA + | CL -  | Simulation time (ns) | replicas |
|-  | - | -| -| - | - | - | - |
| ATP | 30 | 30 | 0 | 68 | 8 | 1000| 1 |
| ATP & pyrene  | 30 | 30 | 10 | 68 | 8 | 1000 | 3 |

# files
* `forcefield.ff` - CHARMM36 forcefield 

# ATP simulation
* `gmx insert-molecules -ci atp.pdb -o atp_30box.pdb -box 5 5 5 -nmol 30`
* `gmx pdb2gmx -f atp_30box.pdb -o atp30_pro.gro -water tip3p`
# Modified nucleotide parameters 



# ATP Pyrene Simulation

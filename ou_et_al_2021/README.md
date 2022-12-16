# ou_et_al_2021
Reproduction of MD ATP simulation with lysozyme from *Ou et al (2021)*'s work. (https://pubs.acs.org/doi/10.1021/jacsau.1c00316)

# files
* `charmm36_ljpme-jul2021.ff` - CHARMM36 force field - 2021
* `atp_pro` - ATP simulation files
   * `1iee_clean.pdb`- lyzozyme from PDB code: 1IEE, with removed crystallized water and ions using the grep command on HOH CL NA respectively.
   * `atp.pdb`- ATP PDB file downloaded from the CHARMM-GUI Archive - Small molecule database:
    https://charmm-gui.org/?doc=archive&lib=csml 
   * `ions.mdp` - ions mdp to create a tpr to add ions within PDB. 
   * `minim.mdp` - mdp file for energy minizimation, for 10,000 steps. 
   * `nvt.mdp` - mdp file for equilibration for NVT ensemble at 300K.
   * `npt.mdp` - mdp file for equilibration for NPT ensemble at 1 bar.
   * `md.mdp` - mdp file for production MD for 400ns. 
 
notes from *ou_et_al* for mdp: 
- barostat - parrinello-rahman
- thermostat - berendsen
- 12 Angstrom cutoff distance
- LINCS algorithm to restrain bonds

# prep.

# gromacs
Gromacs Version - 2021.5

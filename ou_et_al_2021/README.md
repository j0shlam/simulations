# ou_et_al_2021
Reproduction of MD ATP simulation with lysozyme from *Ou et al (2021)*'s work. (https://pubs.acs.org/doi/10.1021/jacsau.1c00316)

# files
* `charmm36_ljpme-jul2021.ff` - CHARMM36 force field - 2021
* `atp_pro` - ATP simulation files (without Mg 2+)
   * `1iee_clean.pdb` - lyzozyme from PDB code: 1IEE, with removed crystallized water and ions using the grep command on HOH CL NA respectively.
   * `atp.pdb` - ATP PDB file downloaded from the CHARMM-GUI Archive - Small molecule database:
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

# method.
notes from *ou_et_al* for prep: 20 ATP molecules are added, using a cubic box of 12.6nm per side and solvated with TIP3P water model. 
  * Setting up the simulation within gromacs via:
  1. Initial structure of lysozyme and ATP `gmx insert-molecules -f 1iee_clean.pdb -ci atp.pdb -o 1iee_atp.gro -nmol 20 `
  2. Generate topology files using `gmx pdb2gmx -f 1iee_atp.gro -o 1iee_processed.gro -water tip3p`
  3. Generate box `gmx editconf -f 1iee_processed.gro -o 1iee_newbox.gro -c -d 1.0 -bt cubic -box 12.6 12.6 12.6`
  4. Solvate with TIP3P water `gmx solvate -cp 1iee_newbox.gro -cs spc216.gro -o 1iee_solv.gro -p topol.top`
  5. Generate starting structure to add ions `gmx grompp -f ions.mdp -c 1iee_solv.gro -p topol.top -o ions.tpr`
  6. Add 150mM NaCl to system `gmx genion -s ions.tpr -o 1iee_solv_ions.gro -p topol.top -pname SOD -nname CLA -conc 0.15 -neutral`
  7. Generate starting structure for energy minimization `gmx grompp -f minim.mdp -c 1iee_solv_ions.gro -p topol.top -o em.tpr`
  8. Run `gmx mdrun -v -deffnm em`
  9. Repeat with equilibration with restraints `gmx grompp -f nvt.mdp -c em.gro -r em.gro -p topol.top -o nvt.tpr`
  10. `gmx mdrun -v -deffnm nvt`
  11. `gmx grompp -f npt.mdp -c nvt.gro -r nvt.gro -t nvt.cpt -p topol.top -o npt.tpr`
  12. `gmx mdrun -v -deffnm npt`
  * production:
  13. `gmx grompp -f md.mdp -c npt.gro -t npt.cpt -p topol.top -o md_0_1.tpr`
  14. `gmx mdrun -v -deffnm md_0_1`
  15. Correct for periodicity and trajectory `gmx trjconv -s md_0_1.tpr -f md_0_1.xtc -o md_0_1_noPBC.xtc -pbc mol -center`
  
# gromacs
Gromacs Version - 2021.5

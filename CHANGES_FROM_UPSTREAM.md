# Changes from upstream msld-py-prep

These changes sit on top of upstream `main`
(`82584c116863a7b45cce7c36ea573c322012ff11`) of
https://github.com/Vilseck-Lab/msld-py-prep. The three files touched here are
byte-identical between that commit and `a375d8cb`, the commit the work was
originally done against, so the changes apply to either.

Every change is marked `[pyprep_update]` in the code.


| File | Change | Why |
|---|---|---|
| `msld_mcs.py` | `MsldMCS(..., refname=None)`: an optional name of the reference ligand | choose the reference instead of the automatic pick (fewest fragment atoms) |
| `msld_mcs.py` | fragments are compared by stereochemistry too (RDKit reads R/S and E/Z from the mol2 3D coordinates); a warning is printed for a core atom whose stereochemistry differs between ligands | the original compares only atom types and bonds, so a stereoisomer was treated as the same fragment and dropped from the site. Needs RDKit; without it, a warning and the old behavior |
| `msld_crn.py` | one-site panels: each fragment's charge offset = its molecule's net charge minus the reference's | the original rounds each fragment's partial-charge sum, which can pick the wrong integer and erase a real charge difference (e.g. a neutral vs a protonated ligand). No effect when all ligands have the same charge |
| `Lg_Solvate.sh` | `more` -> `cat` when reading the system name | some `more` versions add banner lines and corrupt the name |
| `Lg_Solvate.sh` | the offset `awk` stops after the first match | otherwise it can print several translation vectors |

Files from upstream that are **not** included because this notebook does not use them: `msld_py_prep.py`
(the notebook runs each step itself), `msld_mcs_rdecomp.py` and `CGenFF_atomtypes.txt` (RDKit-based MCS
variant), `vis_check.py` (PyMOL viewer; the notebook draws the core itself), `NOTES`, the `CRN_Plugin/`
PyMOL plugin and the `examples/`, `bookending_corrections/` folders.

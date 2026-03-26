[![Version Badge](https://anaconda.org/conda-forge/phonopy/badges/version.svg)](https://anaconda.org/conda-forge/phonopy)
[![Downloads Badge](https://anaconda.org/conda-forge/phonopy/badges/downloads.svg)](https://anaconda.org/conda-forge/phonopy)
[![PyPI](https://img.shields.io/pypi/dm/phonopy.svg?maxAge=2592000)](https://pypi.python.org/pypi/phonopy)
[![codecov](https://codecov.io/gh/phonopy/phonopy/branch/develop/graph/badge.svg)](https://codecov.io/gh/phonopy/phonopy)

# Phonopy (Custom Version for Isotope/Defect Studies)

**Note:** This is a forked version of the official Phonopy repository. It contains specific modifications to simplify workflows for studying isotope effects and defects.

The official upstream repository can be found at: [https://github.com/phonopy/phonopy](https://github.com/phonopy/phonopy)

---

### Key Modifications in This Version

The primary enhancement in this fork is an **intelligent mass expansion feature**.

* **Problem Solved**: Standard Phonopy requires providing a mass for every atom in a pre-expanded supercell. This is impractical for large systems with isotopic or elemental substitutions.
* **Solution**: The code in `phonopy/api_phonopy.py` (@masses.setter) has been modified. Now, you only need to provide a short list of masses in the `MASS` tag, corresponding to the unique atom types in your `POSCAR`. The code will automatically expand this to a full mass list for the supercell.

### New Usage Example

For a 64-atom supercell containing C-14 and N-14 (where C appears first in `POSCAR`), your `phonopy.conf` can now be written simply as:

```ini
ATOM_NAME = C N
# No need to repeat the mass 64 times.
# Just list the mass for each unique atom type in order of appearance.
MASS = 14.003241989 14.003074004

DIM = 1 1 1
CREATE_DISPLACEMENTS = .TRUE.
```


# Phonopy

Phonon code mainly written in python. Phonopy user documentation is found at
http://phonopy.github.io/phonopy/

## Installation

See https://phonopy.github.io/phonopy/install.html.

## Mailing list for questions

Usual phonopy questions should be sent to phonopy mailing list
(https://sourceforge.net/p/phonopy/mailman/).

## Development

The development of phonopy is managed on the `develop` branch of github phonopy
repository.

- Github issues is the place to discuss about phonopy issues.
- Github pull request is the place to request merging source code.

### Formatting

Formatting rules are found in `pyproject.toml`.

### pre-commit

Pre-commit (https://pre-commit.com/) is mainly used for applying the formatting
rules automatically. Therefore, it is strongly encouraged to use it at or before
git-commit. Pre-commit is set-up and used in the following way:

- Installed by `pip install pre-commit`, `conda install pre_commit` or see
  https://pre-commit.com/#install.
- pre-commit hook is installed by `pre-commit install`.
- pre-commit hook is run by `pre-commit run --all-files`.

Unless running pre-commit, pre-commit.ci may push the fix at PR by github
action. In this case, the fix should be merged by the contributor's repository.

### VSCode setting
- Not strictly, but VSCode's `settings.json` may be written like below

  ```json
  "ruff.lint.args": [
      "--config=${workspaceFolder}/pyproject.toml",
  ],
  "[python]": {
      "editor.defaultFormatter": "charliermarsh.ruff",
      "editor.codeActionsOnSave": {
          "source.organizeImports": "explicit"
      }
  },
  ```

## Documentation

Phonopy user documentation is written using python sphinx. The source files are
stored in `doc` directory. Please see how to write the documentation at
`doc/README.md`.

## How to run tests

Tests are written using pytest. To run tests, pytest has to be installed. The
tests can be run by

```bash
% pytest
```

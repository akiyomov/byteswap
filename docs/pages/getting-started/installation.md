# Installation

## 1. Download or clone the repository

**1.1.** Prepare projects directory (if not exists):

```sh
# Create projects directory:
mkdir -pv ~/workspaces/projects

# Enter into projects directory:
cd ~/workspaces/projects
```

**1.2.** Follow one of the below options **[A]** or **[B]**:

**A.** Clone the repository:

```sh
git clone git@github.com:akiyomov/byteswap.git byteswap && \
    cd byteswap
```

**B.** Download source code (for **offline** environment):

1. Download archived **zip** file from [**releases**](https://github.com/akiyomov/byteswap/releases).
2. Extract it into the project directory.
3. Rename the extracted directory from **`byteswap`** to **`byteswap`**.

### 2. Install the module

> [!NOTE]
> Choose one of the following methods to install the module **[A ~ G]**:

**A.** Install with **pip**:

```sh
# Install directly from the source code:
pip install .
# Or install with editable mode:
pip install -e .
```

**B.** Install for **DEVELOPMENT** environment:

```sh
pip install -r ./requirements/requirements.dev.txt
```

**C.** Install directly from git repository:

```sh
pip install git+https://github.com/akiyomov/byteswap.git
```

**D.** Install from **pre-built package** files (for **PRODUCTION**):

1. Download **`.whl`** or **`.tar.gz`** file from [**releases**](https://github.com/akiyomov/byteswap/releases).
2. Install with pip:

```sh
# Install from .whl file:
pip install ./byteswap-[VERSION]-py3-none-any.whl
# Or install from .tar.gz file:
pip install ./byteswap-[VERSION].tar.gz
```

**E.** Build the **package** and install with **pip**:

```sh
# Install python build tool:
pip install -U pip build

# Build python package:
python -m build

# Install from .whl file:
pip install ./dist/byteswap-[VERSION]-py3-none-any.whl
# Or install from .tar.gz file:
pip install ./dist/byteswap-[VERSION].tar.gz
```

**F.** Copy the **module** into the project directory (for **testing**):

```sh
# Install python dependencies:
pip install -r ./requirements.txt

# Copy the module source code into the project:
cp -r ./src/byteswap [PROJECT_DIR]
# For example:
cp -r ./src/byteswap /some/path/project/
```

**G.** Manually add module path into **PYTHONPATH** (not recommended):

```sh
# Add current path to PYTHONPATH:
export PYTHONPATH="${PWD}/src:${PYTHONPATH}"

# Or add the module path to PYTHONPATH:
export PYTHONPATH="[MODULE_PATH]:${PYTHONPATH}"
# For example:
export PYTHONPATH="/some/path/byteswap/src:${PYTHONPATH}"
```

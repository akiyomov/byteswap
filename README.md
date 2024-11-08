# ByteSwap

This is a ByteSwap project.

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit)
[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/akiyomov/byteswap/2.build-publish.yml?logo=GitHub)](https://github.com/akiyomov/byteswap/actions/workflows/2.build-publish.yml)
[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/akiyomov/byteswap?logo=GitHub)](https://github.com/akiyomov/byteswap/releases)

This is a template repo for AI/ML model module.

## Features

- AI/ML model
- Python module/package
- Jupyter notebook
- Research
- Project Structure
- Template
- CI/CD

---

## Installation

### 1. Prerequisites

- Install **Python (>= v3.9)** and **pip (>= 23)**:
    - **[RECOMMENDED] [Miniconda (v3)](https://docs.anaconda.com/miniconda)**
    - *[arm64/aarch64] [Miniforge (v3)](https://github.com/conda-forge/miniforge)*
    - *[Python virutal environment] [venv](https://docs.python.org/3/library/venv.html)*
- *[OPTIONAL]* For **GPU (NVIDIA)**:
    - **NVIDIA GPU driver (>= v452.39)**
    - **NVIDIA CUDA (>= v11)** and **cuDNN (>= v8)**

For **DEVELOPMENT** environment:

- Install [**git**](https://git-scm.com/downloads)
- Setup an [**SSH key**](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh) ([video tutorial](https://www.youtube.com/watch?v=snCP3c7wXw0))

### 2. Download or clone the repository

**2.1.** Prepare projects directory (if not exists):

```sh
# Create projects directory:
mkdir -pv ~/workspaces/projects

# Enter into projects directory:
cd ~/workspaces/projects
```

**2.2.** Follow one of the below options **[A]** or **[B]**:

**A.** Clone the repository:

```sh
git clone git@github.com:akiyomov/byteswap.git byteswap && \
    cd byteswap
```

**B.** Download source code (for **offline** environment):

1. Download archived **zip** file from [**releases**](https://github.com/akiyomov/byteswap/releases).
2. Extract it into the project directory.
3. Rename the extracted directory from **`byteswap`** to **`byteswap`**.

### 3. Install the module

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

## Usage/Examples

### Simple

[**`examples/simple/main.py`**](https://github.com/akiyomov/byteswap/blob/main/examples/simple/main.py):

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

## Standard libraries
import sys
import logging
from typing import Any

## Third-party libraries
import numpy as np
from numpy.typing import NDArray

## Internal modules
from byteswap import SimpleModel


logging.basicConfig(stream=sys.stdout, level=logging.INFO)
logger = logging.getLogger(__name__)


if __name__ == "__main__":

    # Pre-defined variables (for customizing and testing)
    _model_dir = "./models"
    _model_name = "linear_regression.v0.0.1-24"

    _X_train = np.array([[1], [2], [3], [4], [5]])
    _y_train = np.array([2, 4, 6, 8, 10])

    _X_test = np.array([[6], [7], [8]])
    _y_test = np.array([10, 14, 16])

    # Create the model instance
    _config = {"models_dir": _model_dir, "model_name": _model_name}
    _model = SimpleModel(config=_config)

    # Train or load the model
    if not SimpleModel.is_model_files_exist(**_config):
        _model.train(X=_X_train, y=_y_train)
    else:
        _model.load()

    # Predict the target values
    _y_pred: NDArray[Any] = _model.predict(X=_X_test)
    logger.info(f"Predicted values for {_X_test.flatten()}: {_y_pred.flatten()}")

    # Evaluate the model
    _r2_score: float = _model.score(y_true=_y_test, y_pred=_y_pred)
    logger.info(f"R^2 score: {_r2_score}")

    _is_similar: bool = _model.is_similar(X=_X_test, y=_y_test)
    logger.info(f"Is similar: {_is_similar}")

    # Save the model
    if _model.is_trained() and (not SimpleModel.is_model_files_exist(**_config)):
        _model.save()

    logger.info("Done!")
```

:thumbsup: :sparkles:

---

## Configuration

[**`templates/configs/config.yml`**](https://github.com/akiyomov/byteswap/blob/main/templates/configs/config.yml):

```yaml
byteswap:                                       # Just an example to group the configs (Not necessary)
  models_dir: "./models"                              # Directory where the models are saved
  model_name: "linear_regression.v0.0.1-240101"     # Name of the model as sub-directory
  threshold: 0.5                                    # Threshold for similarity check
```

### Environment Variables

[**`.env.example`**](https://github.com/akiyomov/byteswap/blob/main/.env.example):

```sh
# ENV=development
# DEBUG=true
```

## Running Tests

To run tests, run the following command:

```sh
# Install python test dependencies:
pip install -r ./requirements/requirements.test.txt

# Run tests:
python -m pytest -sv -o log_cli=true
# Or use the test script:
./scripts/test.sh -l -v -c
```

## Build Package

To build the python package, run the following command:

```sh
# Install python build dependencies:
pip install -r ./requirements/requirements.build.txt

# Build python package:
python -m build
# Or use the build script:
./scripts/build.sh
```

## Generate Docs

To build the documentation, run the following command:

```sh
# Install python documentation dependencies:
pip install -r ./requirements/requirements.docs.txt

# Serve documentation locally (for development):
mkdocs serve
# Or use the docs script:
./scripts/docs.sh

# Or build documentation:
mkdocs build
# Or use the docs script:
./scripts/docs.sh -b
```

## Documentation

- [Docs](https://github.com/akiyomov/byteswap/blob/main/docs)
- [Home](https://github.com/akiyomov/byteswap/blob/main/docs/README.md)

### Getting Started

- [Prerequisites](https://github.com/akiyomov/byteswap/blob/main/docs/pages/getting-started/prerequisites.md)
- [Installation](https://github.com/akiyomov/byteswap/blob/main/docs/pages/getting-started/installation.md)
- [Configuration](https://github.com/akiyomov/byteswap/blob/main/docs/pages/getting-started/configuration.md)
- [Examples](https://github.com/akiyomov/byteswap/blob/main/docs/pages/getting-started/examples.md)
- [Error Codes](https://github.com/akiyomov/byteswap/blob/main/docs/pages/getting-started/error-codes.md)

### [API Documentation](https://github.com/akiyomov/byteswap/blob/main/docs/pages/api-docs/README.md)

### Development

- [Test](https://github.com/akiyomov/byteswap/blob/main/docs/pages/dev/test.md)
- [Build](https://github.com/akiyomov/byteswap/blob/main/docs/pages/dev/build.md)
- [Docs](https://github.com/akiyomov/byteswap/blob/main/docs/pages/dev/docs.md)
- [CI/CD](https://github.com/akiyomov/byteswap/blob/main/docs/pages/dev/cicd.md)
- [Scripts](https://github.com/akiyomov/byteswap/blob/main/docs/pages/dev/scripts/README.md)
- [File Structure](https://github.com/akiyomov/byteswap/blob/main/docs/pages/dev/file-structure.md)
- [Sitemap](https://github.com/akiyomov/byteswap/blob/main/docs/pages/dev/sitemap.md)
- [Contributing](https://github.com/akiyomov/byteswap/blob/main/docs/pages/dev/contributing.md)
- [Roadmap](https://github.com/akiyomov/byteswap/blob/main/docs/pages/dev/roadmap.md)

### Research

- [Reports](https://github.com/akiyomov/byteswap/blob/main/docs/pages/research/reports.md)
- [Benchmarks](https://github.com/akiyomov/byteswap/blob/main/docs/pages/research/benchmarks.md)
- [References](https://github.com/akiyomov/byteswap/blob/main/docs/pages/research/references.md)

### [Release Notes](https://github.com/akiyomov/byteswap/blob/main/docs/pages/release-notes.md)

### [Blog](https://github.com/akiyomov/byteswap/blob/main/docs/pages/blog/README.md)

### About

- [FAQ](https://github.com/akiyomov/byteswap/blob/main/docs/pages/about/faq.md)
- [Authors](https://github.com/akiyomov/byteswap/blob/main/docs/pages/about/authors.md)
- [Contact](https://github.com/akiyomov/byteswap/blob/main/docs/pages/about/contact.md)
- [License](https://github.com/akiyomov/byteswap/blob/main/docs/pages/about/license.md)

---

## References

- <https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html>
- <https://packaging.python.org/en/latest/tutorials/packaging-projects>
- <https://python-packaging.readthedocs.io/en/latest>

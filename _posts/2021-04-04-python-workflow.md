---
layout: post
title: Upgrading my Python workflow with black, flake8 and pre-commit
description: 
summary: 
---

```python
# install
pip install pre-commit

# generate sample config yaml
pre-commit sample-config > .pre-commit-config.yaml

# install black
pipenv install black --pre --dev

# add to precommit config
-   repo: https://github.com/psf/black
    rev: 21.6b0
    hooks:
      - id: black
      

# install black
pipenv install flake8 --dev

# decide that flake8 is shit and abandon it

```
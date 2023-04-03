# Exercice 1
## b
```
# This workflow will install Python dependencies, run tests and lint with a single version of Python
# For more information see: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-python

name: Python application

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

permissions:
  contents: read

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: Set up Python 3.10
      uses: actions/setup-python@v3
      with:
        python-version: "3.10"
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install flake8 pytest
        if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
    - name: Lint with flake8
      run: |
        # stop the build if there are Python syntax errors or undefined names
        flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
        # exit-zero treats all errors as warnings. The GitHub editor is 127 chars wide
        flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics
    - name: Test with pytest
      run: |
        pytest
```

Quelles étapes sont réalisées par cette action ?
1. Lors d'un push ou d'une pull request, l'application va être copiée dans un container ubuntu.
2. Les dépendances du projet vont être installées ainsi que flake8 et pytest 
3. flake8 est lancé pour le linting du code (vérifie s'il y a des erreurs de syntaxe et s'il n'y en a pas, on vérifie la longueur des lignes et compte le nombre de problèmes repérés)
4. Les tests sont effectués avec pytest


Une étape est définie au minimum par 2 paramètres, lesquels sont-ils et à quoi servent-ils ?
Une condition: `on` qui permet d'indiquer quelles opérations vont lancer l'action
Une action à effectuer: `job` qui définit ce qui doit être fait



La première étape contient un paramètre ‘with’, a quoi sert-il ?
```
uses: actions/setup-python@v3
with:
        python-version: "3.10"
```
Permet d'indiquer quelle version de python est utilisée pour dans la ligne de commande (ajout aux variables PATH). Dans ce cas, c'est la version 3.10 qui est utilisée.

DOING: voir pourquoi le build-docker-image ne marche pas Token ne fonctionne pas...


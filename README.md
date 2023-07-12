# pypi_in_pages_example
Use github pages to host python packages index. Deploy everything using github actions. 

Github does not offer a Python Package feature, but it is possible to tweak github pages
to use it as a simple Python Packages Index following [PEP503](https://peps.python.org/pep-0503/).

View it here: https://zckv.github.io/pypi_in_pages_example/

This work is based on https://github.com/ceddlyburge/python-package-server/
with this tutorial https://www.freecodecamp.org/news/how-to-use-github-as-a-pypi-server-1c3b0d07db2

## Pypi in pages

Use "[Deploy static content to Pages](.github/workflows/static.yml)" workflow from marketplace to deploy a folder
as the root of the pypi. In this repository, it's the "pypackages" folder.

Use the "[Add Python Package](.github/workflows/addrepo.yml)" workflow from this repository to allow the adition of
a package to your package index. This workflow must be called with the name, the version
and a link do download your python package.

This worflow use the "[update_packaging_folder.py](update_packaging_folder.py)" script. Many environnement variables
are set there.

As this Python Package Index follow the PEP503, it is fully compatible with pip:
```sh
pip install --index-url="https://zckv.github.io/pypi_in_pages_example/" example-package 
```

## Example-package

This is a most simple python package. It is built automaticaly when a new version is tagged.
On a tag push, the "[Python Package](.github/workflows/python-package.yml)" workflow is triggered.
The workflow build the package, make a github release. Then it use the name, version and browser
download link of the release asset to deploy it to the Python Package Index.

The built package is not necessarily stored on the Python Package Index repository. The workflows
communicate using curl and the github actions API.


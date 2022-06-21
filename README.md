# Conda-cheatsheet

Managing Conda and Anaconda, Environments, Python, Configuration, Packages. Removing Packages or Environments


## Managing Conda and Anaconda

`conda info`	 Verify conda is installed, check version

`conda update conda`	Update conda package and environment manager

`conda update anaconda`	Update the anaconda meta package

`conda update --all` Update all packages in the environments

## Managing Environments

`conda info --envs`

`conda info -e`	Get a list of all my environmentsActive environment shown with *

`conda create --name snowflakes biopython`

`conda create -n snowflakes biopython`	Create an environment and install program(s)

`conda activate snowflakes`	Activate the new environment to use it

`conda deactivate`	Deactivate the environment

`conda create -n bunnies python=3.4 astroid`	Create a new environment, specify Python version

`conda create -n flowers --clone snowflakes`	Make exact copy of an environment

`conda remove -n flowers --all`	Delete an environment

`conda env export > puppies.yml`	Save current environment to a file

`conda env create -f puppies.yml`	Load environment from a file

`conda env update -n coolbase --file environment.yml`	install and/or update packages from environment.yml

`CONDA_SUBDIR=osx-arm64 conda create -n test_env --dry-run python=3.8 llvm-openmp cython numpy pip "matplotlib-base>=3.0.3" "protobuf >=3.11.2,<4.0.0" "scipy >=1.3.2,<2.0.0"`	Conda dry run environment on a specific platform

`for py in 3.8 3.9 3.10; do echo -e "\n*****  python $py  *****"; conda create --dry-run --quiet -n __test__ python=$py pandas=1.4.2; done`	Conda dry run creating an environment and installing packages (pandas 1.4.2) for different python versions

## Managing Python

`conda search --full-name python`

`conda search -f python`	Check versions of Python available to install

`conda create -n snakes python=3.4`	Install different version of Python in new environment

## Managing .condarc Configuration

`conda config --get`	Get all keys and values from my .condarc file

`conda config --get channels`	Get value of the key channels from .condarc file

`conda config --add channels pandas`	Add a new value to channels so conda looks for packages in this location

`conda config --set anaconda_upload yes`

## Managing Packages, Including Python

`conda list`	View list of packages and versions installed in active environment

`conda search beautiful-soup`	Search for a package to see if it is available to conda install

`conda install -n bunnies beautiful-soup`	Install a new package NOTE: If you do not include the name of the environment, it will install in the current active environment.

`conda update beautiful-soup`	Update a package in the current environment

`conda search --override-channels -c pandas bottleneck`	Search for a package in a specific location (the pandas channel on Anaconda.org)

`conda install -c pandas bottleneck`	Install a package from a specific channel

`conda search --override-channels -c defaults beautiful-soup`	Search for a package to see if it is available from the Anaconda repository

`conda install iopro accelerate`	Install commercial Continuum packages

`conda install black isort flake8`	install python linter

`conda install conda-build`

`conda install m2-patch posix`	Windows only

`conda install --use-local click`	

`conda skeleton pypi pyinstrument`

`conda build pyinstrument`	Build a package from a Python Package Index (PyPi) Package

## Removing Packages or Environments

`conda remove --name bunnies beautiful-soup`	Remove one package from any named environment

`conda remove beautiful-soup`	Remove one package from the active environment

`conda remove --name bunnies beautiful-soup astroid`	Remove multiple packages from any environment

`conda remove --name snakes --all`	Remove an environment

## Conda World

### conda-build 

`conda-build .`

`conda build --test /home/user/miniconda3/conda-bld/noarch/pytest-cov-2.12.1-py_0.tar.bz2`	test the package in your environment (for regression testing)

`conda build gdal-feedstock	`

`conda build sep`	

`conda-build --python 2.7 click`

`conda build gdal-feedstock --variant-config-file conda_build_config.yaml`

### conda convert

`conda convert --platform all ~/anaconda/conda-bld/linux-64/click-7.0-py37_0.tar.bz2 -o outputdir/`

`conda convert package-1.0-py33.tar.bz2 -p win-64`

### conda sekeleton

`conda skeleton pypi --pypi-url <mirror-url> package_name`
  
`conda skeleton pypi <package name on pypi>`
  
`conda skeleton pypi click`
  
`conda skeleton pypi --recursive pyinstrument`

### conda + jake

`conda install -y conda-forge::jake && conda list | jake ddt`	A helpful oneliner to check your conda environments for vulnerable Open Source packages

### conda + boa + mambasolver

`conda install boa -c conda-forge`	Install boa. Use the mamba solver through mambabuild. It not only has a faster solve speed but also prints better error messages that make debugging simpler.

`conda mambabuild .`	build the recipe with mambasolver

`conda mambabuild myrecipe`	build the recipe with mambasolver

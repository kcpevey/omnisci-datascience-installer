# omnisci-datascience-installer
Installer configuration for OmniSci stack

## Setup

There are a couple of things to do to get started here.

1. First install constructor:

```sh
conda install constructor
```

Also, you can install the dependencies from the environment-dev.yml file:

```sh
conda env create -n omnisci-ds-installer --file environment-dev.yml
```

This command creates an environment called `omnisci-ds-installer` (you can use
another name if you want) and installs the packages listed in `environment-dev.yml`.

2. Second, grab a copy of conda-standalone that you want to use.
   It is sometimes the case (especially on Windows) that the versions of
   conda-standalone that come when you install constructor (from step 1)
   are actually pretty broken. It is more stable to rely on the official
   standalone releases. These can be found at https://repo.anaconda.com/pkgs/misc/conda-execs/
   You'll want to grab a recent version of one of these and stash it somewhere.
   For example:

```sh
wget https://repo.anaconda.com/pkgs/misc/conda-execs/conda-latest-osx-64.exe
```

3. On Mac, building pkg installers can often result in using too many file handles.
   To get around this, please run the following commands. Note that you will need
   have root access for some of these:

```sh
# perform as regular user
ulimit -S -n 204800

# perform as root
sudo sysctl -w kern.maxfiles=204800
sudo sysctl -w kern.maxfilesperproc=245670
```


## Running Constructor

Now you may run constructor with the following command:

```sh
constructor --conda-exe /path/to/conda.exe constructor/
```

Be aware that, on Mac, whether you are creating a sh-based or pkg-based installer
depends on the contents of the `constructor/construct.yaml` file.  Simply change
the `installer_type` key to have a value of `pkg` or `sh` depending on what you want.

## Gotchas

The pkg installer seems to need to have `conda` itself listed as a spec right now.


## Releasing

For releasing, after the PR is merged, create a tag with the last commit from master and 
push it to the repository, for example:

```sh
git fetch upstream
git checkout upstream/master
rever check
rever 0.0.3
```


## Installation

OmniSci Data Science package installs OmniSci stack that includes intake/intake-omnisci, omnisci-pytools, pymapd, ibis-framework, etc.


### MacOS Instructions

According to your environment follow one of the steps below:

**If you have Anaconda and are using the Anaconda GUI or conda/miniconda:**

Create a new conda environment from the environment.yml available [here](https://github.com/Quansight/omnisci-examples/blob/master/environment.yml), either using the Anaconda Navigator GUI or the command line.


**If you don't have either Anaconda or conda, use the bash installer:**

First, download the `sh` package from the GitHub `omnisci-datascience-installer` [realese page](https://github.com/Quansight/omnisci-datascience-installer/releases/) and add execution permission to it:

```sh
wget https://github.com/Quansight/omnisci-datascience-installer/releases/download/0.0.2/omnisci-0.0.2-MacOSX-x86_64.sh
chmod +x omnisci-0.0.2-MacOSX-x86_64.sh
```

Now, you can install it, executing that file:

```sh
./omnisci-0.0.2-MacOSX-x86_64.sh
```


**If you have installed the Mac Preview we need to tell them how to connect to an Omnisci database from your local machine**


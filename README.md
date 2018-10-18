## Install Dependencies
To run the examples locally, we recommend installing Anaconda and the Jupyter notebook library.

### Anaconda
https://www.anaconda.com/download/

### Python Dependencies
All dependencies needed to run the demos have been saved in a conda requirements file. Create a new conda environemnt with all the dependencies by typing:

```
conda env create -f requirements.yml
```

This will create a new conda environment called `api-examples`


## Run Notebooks
Under the project directory, start the notebooks by activating the environment and running the Jupyter command:

```
source activate api-examples
jupyter notebook
```

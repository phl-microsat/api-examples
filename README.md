## Install Dependencies
To run the examples locally, we recommend installing Anaconda and the Jupyter notebook library.

### Anaconda
https://www.anaconda.com/download/

### Python Dependencies
Create a new conda environemnt with all the dependencies by typing:

```
conda env create -n api-examples jupyter pip
activate api-examples
pip install requests folium geojson
```

## Run Notebooks
Under the project directory, start the notebooks by activating the environment and running the Jupyter command:

```
activate api-examples
jupyter notebook
```

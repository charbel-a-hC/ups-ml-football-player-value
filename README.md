# Football Player Market Value Prediction

## Dataset
In this project, we perform EDA, Feature Engineering and Data Cleaning on a dataset provided by [data.world](https://data.world/) called "Football Data from Transfermarkt" which can be found [here](https://data.world/dcereijo/player-scores). The dataset contains the following:
- 55,000+ games from many seasons on all major competitions
- 400+ clubs from those competitions
- 20,000+ players from those clubs
- 300,000+ player market valuations historical records
- 1,000,000+ player appearance records from all games

All this data is structured in multiple CSV files with information on competitions, games, clubs, players and appearances that is automatically updated once a week. Each file contains the attributes of the entity and the IDs that can be used to join them together. For example, the appearances file contains one row per player appearance, i.e. one row per player per game played. For each appearance you will find attributes such as `goals`, `assists` or `yellow_cards` and IDs referencing other entities within the dataset, such as `player_id` and `game_id`.

More information on the dataset maintenance can be found on the official website and [Github Repository](https://github.com/dcaribou/transfermarkt-datasets)

## Repo Structure
- `dcerejio-players-scores`: full dataset downloaded from g-drive using `dvc pull -r dataset`
- `scripts`: contains formating script for py-files
- `Makefile`: Makefile where you can create a virtual env or create a docker container to run the notebook
- `Dockerfile`: Dockerfile to build a docker image with GPU support (tested on NVIDIA TITAN RTX with Ubuntu 18.04). More information on how to download docker can be found [here](https://docs.docker.com/get-docker/). nvidia-docker installation can also be found [here](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)
- `PlayerMarketValuePrediction.ipynb`: Notebook containing all the code
- `poetry.lock`/`pyproject.toml`: Python Poetry files to install a development environment with all dependencies handled
- `envrionment.yml`: YAML file containing conda exported environment for development (you can use either poetry or conda)

## Running the Notebook
Clone and `cd` in the repository before running any of the commands:
```bash
git clone https://github.com/charbel-a-hC/ups-ml-football-player-value.git
cd ups-ml-football-player-value
```
You also need to install `python3.8` locally if you wish to run the notebook on a **local** environment. For Ubuntu:
```bash
sudo apt-get install python3.8 \
    python3-pip \
    python3.8-venv \
    python3.8-dev \
    python3.8-distutils
```
And you need to update your `pip`:
```bash
/usr/bin/python3.8 -m pip install --upgrade pip
```
### Docker
If you have docker installed:
```bash
docker build . -t ups-football-value
docker run -it --rm -v --runtime=nvidia ${PWD}:/ups-ml-football-player-value ups-football-value bash
```
After launching the container, a notebook will be open in the following ip/port; `localhost:8888`.

### Local Environment (Ubuntu-18.04) - Poetry

Simply run the make command in the repository:
```bash
make env
```
A virtual environment will be created after running the above command. In the same shell, run:
```bash
poetry shell
```
This will activate the environment and then you can open a jupyter notebook:
```bash
jupyter notebook --ip 0.0.0.0 --port 8888 --allow-root
```

### Local Environment - Conda
You can download Anaconda [here](https://docs.anaconda.com/anaconda/install/index.html).
After the download, open an anaconda navigator prompt if you're on windows and run the following commands:
```bash
conda env create -f environment.yml
conda activate ml
```
**Note**: If you're on Linux, you can open a normal terminal and run the following command before creating the environment:
```bash
conda activate base
```
You can then open a jupyter notebook similarly: 
```bash
jupyter notebook
```
### Google Colaboratory
You can open the notebook in Google Colab here: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/charbel-a-hC/ups-ml-football-player-value/blob/main/PlayerMarketValuePrediction.ipynb)

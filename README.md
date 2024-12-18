# Query Benchmarking for Spark and Trino

## 1. Folder Structure
- `datasets` 
- `notebooks` for storing notebooks


## 2. Instruction of use:

### 2.1 Dataset:
1. Download data from [this](https://www.kaggle.com/datasets/zakariaeyoussefi/cell-towers-worldwide-location-data-by-continent) repository. For this project we are using `Asia Towers.csv` and place it on dataset folder. 

2. Start up the different containers individually (on different terminal tabs). We can also do `docker-compose up` to start everything at once but will need to search for access token to start `jupyter notebook`

```
docker-compose up nessie
docker-compose up notebook
docker-compose up trino
docker-compose up minio
```

3. Login to minio at `http://localhost:9001/` with username `admin` and password `password`. Then create a bucket called warehouse.

4. Go to jupyter notebook (see output of docker-compose up notebook) to run the spark code to load the data and to run the benchmarking queries.

5. Open new tab on terminal to initialize trino with this command `docker exec -it trino trino`. Run the queries on `trino-sql.md`

## Queries

#### Simple query
- Calculate the average signal strength for each country and network.

#### Complex query
- Count the unique units in each country.
- Calculate the maximum, minimum, and average range for each network per country.
- Combine these results in a single output.

## Results:

### Spark:
#### Unpartitoned table:
- Simple query: 6.97 Sec
- Complex query: 19.00 Sec

#### Partitioned table:
- Simple query: 6.13 seconds
- Complex query: 15.26

### Trino:
#### Unpartitoned table:
- Simple query: 1.52 Sec
- Complex query: 4.83 Sec

#### Partitioned table:
- Simple query: 1.15 Sec
- Complex query: 4.01 Sec


## Analysis and Report



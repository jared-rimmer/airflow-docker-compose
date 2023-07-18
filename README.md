## Background

I created this code repository to explore Apache Airflow in greater detail as I read articles online as well as following along with the book [Data Pipelines with Apache Airflow ](https://www.manning.com/books/data-pipelines-with-apache-airflow).

It's purpose is as a building block to be able to spin up an Airflow instance and experiment with it locally using Docker.

## Requirements

- Docker
- Basic understanding of Docker Compose

### Setting Up Apache Airflow With Docker Compose

The official Apache Airflow docs have a great tutorial for [Running Airflow in Docker](https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html) which is what I followed.

I made a few additional changes to the docker-compose.yml file based on notes in the Running Airflow in Docker docs with my intended use case in mind.

These were:

- Adding `extra_hosts: - "host.docker.internal:host-gateway"` in the airflow-worker service. 
- Added a Docker proxy service in order to use the Airflow DockerOperator to launch Docker images on my local machine.

### Creating a .env file for setting AIRFLOW_UID

Bringing up the services will work without setting AIRFLOW_UID in a .env file. 

However, It's best practice to do so as you can control what USER owns files.

Create a `.env` file in the root of this reposistory

Add the following too it 

```yml 
AIRFLOW_UID=501
```

### Bringing up the services

Before doing this ensure that Docker Desktop is running on your machine.

Then in your terminal at the root of the repository run the following command:

```
docker-compose up -d
```

This will bring up all of the defined services in the ```docker-compose.yml```

This process will take a while when you first run it as it needs to download all the necessary Docker images and run the Airflow initialisation process.

It will also create some directories in the root of the repository for dags, logs and plugins

### Logging into the Airflow UI

Once the docker compose process has completed and all the services are runnin you can login into the Apache Airflow UI.

This will be available on http://localhost:8080/

The username and password are both **airflow**

### Bringing down the services

In your terminal at the root of the repository run the following command:

```
docker-compose down
```

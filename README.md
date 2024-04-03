![Logo](https://github.com/mtahiraslan/python-api-with-docker-and-postgres/blob/main/architecture.png)

# Python RestfulAPI(CoincapAPI) with Docker & PostgreSQL

The project leverages Docker, PostgreSQL, pgAdmin, and Python to integrate cryptocurrency market data into a PostgreSQL database using the CoincapAPI. Its primary purpose is to provide an efficient and streamlined process for fetching, transforming, and storing live cryptocurrency market data. By utilizing Docker containers for the database and admin tool, the solution ensures a consistent and isolated environment, making it highly portable and easy to set up across different machines or environments. This project is particularly useful for data analysts, financial technologists, and cryptocurrency enthusiasts looking to harness the power of real-time market data for analysis, reporting, or integration into financial software and applications.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to install the software and how to install them:

- Docker
- Postgres Container
- PgAdmin Container
- Python 3.x
- Python libraries (pandas, requests, sqlalchemy, psycopg2)

### Installation

A step-by-step series of examples that tell you how to get a development environment running.

1. **Install Docker:**
   - Follow the instructions on the [official Docker website](https://docs.docker.com/get-docker/) to install Docker on your system.

2. **Create the Docker-compose file:**
   - Create a `docker-compose.yaml` file in the root directory of your project with the necessary configurations to stand up PostgreSQL and pgAdmin4 containers.

    ```yaml
    version: '3.8'
    
    services:
      db:
        container_name: postgres_container
        image: postgres
        restart: always
        environment:
          POSTGRES_USER: root
          POSTGRES_PASSWORD: root
          POSTGRES_DB: postgres_db
        ports:
          - "5432:5432"
      
      pgadmin:
        container_name: pgadmin4_container
        image: dpage/pgadmin4
        restart: always
        environment:
          PGADMIN_DEFAULT_EMAIL: admin@admin.com
          PGADMIN_DEFAULT_PASSWORD: root
        ports:
          - "5050:80"
    ```

3. **Start your Docker containers:**
   - Run the following command in your terminal:

    ```
    docker-compose up
    ```

4. **Access pgAdmin:**
   - Open your web browser and enter `localhost:<port number>` as defined in your `docker-compose.yaml` file.
   - Login to pgAdmin with your email and password specified in the docker-compose file.

5. **Add a new server in pgAdmin:**
   - Enter the same database and host information as in your `docker-compose.yaml` file.

6. **Prepare your Python environment:**
   - Install necessary libraries using pip:

    ```
    pip install pandas sqlalchemy requests psycopg2
    ```

   - Write your Python script to interact with the CoincapAPI and PostgreSQL. Ensure you define your database connection strings, CoincapAPI URL, and handle data transformation appropriately.

### Running the Script

Run the cells in the Coincap_api.ipynb file one by one and make sure it works correctly.


## RESTful API documentation

```http
  GET /assets
```

#### Request

| Key | Requirement     | Value                | Description                |
| :-------- | :------- | :------------------------- | :------------------------- |
| `search` | `optional` | `bitcoin` | search by asset id (bitcoin) or symbol (BTC) |
| `ids` | `optional` | `bitcoin` | query with multiple ids=bitcoin,ethereum,monero |
| `limit` | `optional` | `5` | max limit of 2000 |
| `offset` | `optional` | `1` | offset |

#### Response

| Key | Description     |
| :-------- | :------- | 
| `id`           | unique identifier for asset | 
| `rank`         | rank is in ascending order - this number is directly associated with the marketcap whereas the highest marketcap receives rank 1 | 
| `symbol`       | most common symbol used to identify this asset on an exchange | 
| `name`         | proper name for asset | 
| `supply`       | available supply for trading | 
| `maxSupply`    | total quantity of asset issued | 
| `marketCapUsd` | supply x price | 
| `volumeUsd24Hr` | quantity of trading volume represented in USD over the last 24 hours | 
| `priceUsd`     | volume-weighted price based on real-time market data, translated to USD | 
| `changePercent24Hr` | the direction and value change in the last 24 hours | 
| `vwap24Hr`     | Volume Weighted Average Price in the last 24 hours | 

## Congratulations!

If you've come this far and reviewed or completed all the steps, you can help me by giving this repository a star ⭐

## Contribution Guideline

You can fork this repo and send a pull request to fix any mistakes that you have found.

## Final Result

![Result](https://github.com/mtahiraslan/python-api-with-docker-and-postgres/blob/main/result.png)

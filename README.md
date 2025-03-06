# SonarQube with PostgreSQL using Docker Compose

This repository contains a `docker-compose.yml` file to set up SonarQube with a PostgreSQL database.

## Overview

This Docker Compose configuration defines two services:

* **PostgreSQL:** A PostgreSQL 14 database container to store SonarQube data.
* **SonarQube:** A SonarQube Community Edition container, configured to connect to the PostgreSQL database.

## Prerequisites

* Docker installed.
* Docker Compose installed.

## Usage

1.  **Clone the repository:**

    ```bash
    git clone <repository_url>
    cd <repository_directory>
    ```

    Replace `<repository_url>` and `<repository_directory>` with your repository's URL and local directory name.

2.  **Start the containers:**

    ```bash
    docker-compose up -d
    ```

    This will download the necessary images and start the containers in detached mode.

3.  **Access SonarQube:**

    Open your web browser and navigate to `http://localhost:9000`.

4.  **Login:**

    Use the default credentials:

    * Username: `admin`
    * Password: `admin`

    You will be prompted to change the password after logging in.

5.  **Stop the containers:**

    ```bash
    docker-compose down
    ```

## Configuration

* **PostgreSQL:**
    * The PostgreSQL container uses the `postgres:14` image.
    * Environment variables are used to configure the database user, password, and database name.
    * A volume `postgresql_data` is used to persist the database data.
* **SonarQube:**
    * The SonarQube container uses the `sonarqube:community` image.
    * It depends on the PostgreSQL container.
    * Environment variables are used to configure the JDBC URL, username, and password to connect to the PostgreSQL database.
    * Port 9000 is exposed to access the SonarQube web interface.
    * Volumes are used to persist SonarQube data, extensions, and logs.
* **Networks:**
    * A network `sonarnet` is created to allow communication between the PostgreSQL and SonarQube containers.
* **Volumes:**
    * The volumes `postgresql_data`, `sonarqube_data`, `sonarqube_extensions`, and `sonarqube_logs` are defined for data persistence.

## Volumes

* `postgresql_data`: Stores the PostgreSQL database data.
* `sonarqube_data`: Stores the SonarQube data.
* `sonarqube_extensions`: Stores SonarQube extensions.
* `sonarqube_logs`: Stores SonarQube logs.

## Networks

* `sonarnet`: A Docker network for communication between the containers.

## Notes

* This configuration uses the default credentials for SonarQube. It is highly recommended to change the default password immediately after logging in.
* This setup is suitable for development and testing. For production environments, consider using a managed PostgreSQL service and configuring SonarQube for production use.
* If you need to change the port that SonarQube is exposed on, modify the ports section of the sonarqube service in the docker-compose.yml file.
* Ensure that the used ports are available on your system.

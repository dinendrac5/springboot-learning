# BizFlow — Business Operations Platform

BizFlow is a business operations platform built using
Java, Spring Boot, PostgreSQL, and eventually Angular.

## Technology Stack

- Java 21
- Spring Boot 4.1.2
- Maven
- PostgreSQL 17
- Docker Compose
- Spring Data JPA
- Flyway

## Prerequisites

- JDK 21
- Docker Desktop with Docker Compose
- IntelliJ IDEA (recommended)

## Local Database Setup

### 1. Configure environment variables

Create a `.env` file in the project root:

DB_USERNAME=bizflow
DB_PASSWORD=<your-local-password>

Do not commit `.env` to Git.

### 2. Start PostgreSQL

Run:

    docker compose up -d

Check container health:

    docker compose ps

### 3. Configure Spring Boot

Set the following environment variable in your
IntelliJ run configuration:

DB_PASSWORD=<same-local-password>

The database URL defaults to:

    jdbc:postgresql://localhost:5432/bizflow

### 4. Run the application

Run `SpringbootLearningApplication` from IntelliJ.

Flyway automatically applies pending database migrations.

### 5. Verify Flyway history

Run:

    docker exec -it bizflow-postgres psql -U bizflow -d bizflow

Then execute:

    SELECT * FROM bizflow.flyway_schema_history;

### 6. Stop PostgreSQL

    docker compose stop

To restart:

    docker compose start

## Database Migrations

Migration scripts are stored in:

    src/main/resources/db/migration/

Flyway tracks applied migrations in:

    bizflow.flyway_schema_history

Hibernate uses `ddl-auto=validate`, so schema changes
must be managed through Flyway.

## Important Notes

- Docker named volumes preserve PostgreSQL data.
- `docker compose down -v` deletes database data.
- Never commit passwords or other secrets.
- Set the IntelliJ VM option
  `-Duser.timezone=Asia/Kolkata` if the PostgreSQL
  driver rejects the JVM's default time zone.
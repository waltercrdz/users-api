# Users API

API to handle user registration, authentication, and retrieval of user information.

## Prerequisites
- Python 3.13+
- Poetry
- Docker (optional)

## Getting Started

1. Clone the repository:

    ```bash
    git clone https://github.com/waltercrdz/users-api.git
    ```
2. Navigate into the project directory:
    
    ```bash
    cd users-api
    ```

3. Install the dependencies using Poetry:
    
    ```bash
    poetry install --no-root
    ```

4. Run the database migrations using Alembic:

    Before running the database migrations, ensure you have a PostgreSQL container running. You can start a PostgreSQL container using the following command:

    ```bash
    docker run --name my_postgres -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=admin -e POSTGRES_DB=mypostgres -p 5432:5432 -d postgres
    ```

    Then you can run the migration:

    ```bash
    poetry run alembic upgrade head
    ```

    > For more information on using Alembic, refer to the [Alembic tutorial](https://alembic.sqlalchemy.org/en/latest/tutorial.html).


5. Run the FastAPI server:
    ```bash
    poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
    ```

## Running with Docker Compose

1. Clone the repository:

    ```bash
    git clone https://github.com/waltercrdz/users-api.git
    ```

2. Navigate into the project directory:
    
    ```bash
    cd users-api
    ```

3. Run the database migrations using Alembic:

    Before running the database migrations, ensure you have a PostgreSQL container running. You can start a PostgreSQL container using the following command:

    ```bash
    docker run --name my_postgres -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=admin -e POSTGRES_DB=mypostgres -p 5432:5432 -d postgres
    ```

    Then you can run the migration:

    ```bash
    poetry run alembic upgrade head
    ```

    > For more information on using Alembic, refer to the [Alembic tutorial](https://alembic.sqlalchemy.org/en/latest/tutorial.html).


4. Run the application using Docker Compose:
    
    ```bash
    docker-compose up --build
    ```

## Environment Variables

Create a `.env` file in the `dev` directory to declare environment variables for the development stage. Below is an example of the required environment variables:

```
# DB
DATABASE_URL=postgresql://admin:admin@localhost:5432/mypostgres

# JWT
SECRET_KEY=your_secret_key
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
```
Make sure to replace `your_secret_key` with a secure key of your choice.

## Project Structure

The project follows a Hexagonal Architecture, also known as Ports and Adapters.

## Packages

### application

This package is dedicated to the application layer of the microservice. It contains the Application Service classes that orchestrate the business logic and interactions between other modules.

### domain

This package contains domain models of the microservice.

### infrastructure

This package contains the infrastructure layer of the microservice, including the REST controllers, repositories, and other classes that interact with external systems.

## API Endpoints

### User Registration

Register a new user.

```bash
curl -X POST "http://127.0.0.1:8000/users" -H "Content-Type: application/json" -d '{"email": "john.doe@gmail.com", "password": "newpassword123"}'
```

#### Parameters

- `email` (required): The user email.
- `password` (required): The login password.

#### Response

```json
{
    "id": "fd7cbf70-d7ea-490b-87a2-e4a1597653f2",
    "email": "john.doe@gmail.com"
}
```

### Get a User by Id

Retrieves a user by their unique identifier.

```bash
curl -X GET "http://127.0.0.1:8000/users/{id}" -H "accept: application/json"
```

#### Path Parameters

- `id` (required): The unique identifier of the user.

#### Response

```json
{
    "id": "fd7cbf70-d7ea-490b-87a2-e4a1597653f2",
    "email": "john.doe@gmail.com"
}
```

### User Authentication

Authenticate a user and returns a JWT token.

```bash
curl -X POST "http://127.0.0.1:8000/auth" -H "Content-Type: application/json" -d '{"email": "john.doe@gmail.com", "password": "newpassword123"}'
```

#### Parameters

- `email` (required): The user email.
- `password` (required): The login password.

#### Response

In your JSON response, the token value is a JWT. Here is an example of how it might look:

```json
{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE3MzA5MTI0OTEsInN1YiI6ImpvaG4uZG9lQGdtYWlsLmNvbSIsImV4cCI6MTczMDkxMzM5MSwidXNlcl9pZCI6ImVjOTM0ZTk4LTAzMzUtNGMwZS1iNDZjLTg4ZDZiYWNhZmE0NyJ9.wdQHEX1Y0kyi2XWdPWXOuzFhsUJvU72NR3lYOrEu4qw"
}
```

> For more details, please refer to the OpenAPI documentation, hosted at `http://127.0.0.1:8000/docs`

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## License

This project is licensed under the MIT License.
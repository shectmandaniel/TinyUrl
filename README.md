# TinyURL Java Project

This project is a URL shortening service built with Java and Spring Boot. It utilizes Redis for temporary storage, MongoDB for user data management, and Cassandra for scalable data storage.

## Project Structure

### AppController.java

This is the main controller of the application, handling various endpoints related to user creation, URL shortening, and URL redirection.

- **User Endpoints**
  - `POST /user`: Create a new user.
  - `GET /user/{name}`: Retrieve user information by name.
  - `GET /user/{name}/clicks`: Retrieve click data for a specific user.

- **TinyURL Endpoints**
  - `POST /tiny`: Generate a new shortened URL.
  - `GET /{tiny}/`: Redirect to the original URL based on the shortened code.
 
### SwaggerConfig.java

The `SwaggerConfig` class sets up Swagger for API documentation and testing.

- **Swagger Configuration**
  - The Swagger configuration is set up in `SwaggerConfig.java` using the `Docket` bean.
  - The API documentation is accessible at `/swagger-ui.html` once the application is running.


### Docker-Compose

The `docker-compose.yml` file sets up the necessary services for the application:

- **Redis**: In-memory data store for quick lookups of shortened URLs.
- **MongoDB**: NoSQL database for storing user data and URL click counts.
- **Cassandra**: NoSQL database for scalable data storage.

## Getting Started

### Prerequisites

- Java 11 or higher
- Docker and Docker Compose

### Running the Application

1. **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2. **Build the project:**
    ```bash
    ./mvnw clean install
    ```

3. **Start the services using Docker Compose:**
    ```bash
    docker-compose up -d
    ```

4. **Run the application:**
    ```bash
    java -jar target/<your-jar-file>.jar
    ```

### Endpoints

- **Create User**
  - `POST /user`
    ```json
    {
      "name": "exampleName"
    }
    ```

- **Get User**
  - `GET /user/{name}`
    ```json
    {
      "name": "exampleName"
    }
    ```

- **Generate Tiny URL**
  - `POST /tiny`
    ```json
    {
      "longUrl": "http://example.com",
      "userName": "exampleName"
    }
    ```

- **Redirect Tiny URL**
  - `GET /{tiny}/`

- **Get User Clicks**
  - `GET /user/{name}/clicks`
    ```json
    [
      {
        "tiny": "abc123",
        "longUrl": "http://example.com",
        "clickTime": "2024-07-07T12:00:00Z"
      }
    ]
    ```

### Swagger API Documentation

Swagger is used for API documentation and testing. To access the Swagger UI:

1. Run the application.
2. Navigate to [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html) in your web browser.

The Swagger UI provides a user-friendly interface to explore and test the API endpoints.

## Configuration

The application properties can be configured in `application.properties` or through environment variables:

- `base.url`: The base URL for the shortened links.
- `spring.redis.host`: The host you want to connect to redis.
- `spring.data.mongodb.uri`: The mongodb cluster you want to connect.
- `spring.data.cassandra.contact-points`: The cassandra conneection node.

## Contributing

Contributions are welcome! Please submit a pull request or open an issue to discuss your changes.

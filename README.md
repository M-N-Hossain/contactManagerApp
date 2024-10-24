# Contact Manager App

This is a Node.js-based Contact Manager application where users can register, authenticate, and perform CRUD (Create, Read, Update, Delete) operations on their contacts. The app handles user authentication, data validation, and ensures that contacts are managed in a secure manner with token-based authentication.

## Features

- User Registration & Login
- Authentication via JWT (JSON Web Tokens)
- CRUD operations for managing contacts
- Secure API access, allowing only authenticated users to interact with their own contacts
- Validation of cross-user access to prevent unauthorized modifications to other users' contacts
- Error handling and appropriate status codes for different scenarios
- Docker support for easy setup and deployment

## Technology Stack

- Node.js
- Express.js
- MongoDB (with Mongoose)
- JWT for authentication
- bcrypt for password hashing
- Docker & Docker Compose


## Prerequisites

Before running the project, make sure you have the following installed:

- [Node.js](https://nodejs.org/en/) (v14+)
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)


## Getting Started

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/contact-manager-app.git

2. Navigate into the project directory:

    ```bash
    cd contact-manager-app

3. Install dependencies:

    ```bash
    npm install

4. Create a .env file in the root directory and add the following environment variables:

    ```bash
    ACCESS_TOKEN_SECRET=your_secret_key
    MONGO_URI=your_mongodb_uri

4. Running the App with Docker
      This project is fully dockerized. You can run the app using Docker and Docker Compose.
      
      Step 1: Build and Run the Containers
      
          
          docker-compose up --build
      
      Step 2: Access the Application
      Once the containers are up, the application will be running on:
          
          http://localhost:5001
      
      MongoDB will be exposed on port 27017

   #### Docker Compose Configuration
   
   The Docker Compose file defines two services: the Node.js app and MongoDB.
   
   ```yaml
       version: '3'
       services:
       app:
           build: .
           ports:
           - "5001:5001"
           env_file:
           - .env
           environment:
           NODE_ENV: docker
           depends_on:
           - mongo
       mongo:
           image: mongo:latest
           ports:
           - "27017:27017"
   ```
   
   #### Dockerfile
   
   The Dockerfile for the Node.js application builds an image based on Alpine Linux, installs the necessary dependencies, and exposes port 5001 for the app.
   
   ```dockerfile
   
       FROM alpine:3.19
   
       RUN apk add --no-cache nodejs npm python3 make g++
   
       WORKDIR /app
   
       COPY . /app
   
       RUN npm install
   
       # Rebuild bcrypt to match the correct architecture
       RUN npm rebuild bcrypt --build-from-source
   
       EXPOSE 5001
   
       CMD ["npm", "run", "start"]
   ```



6. Running Locally Without Docker:

    ```bash
    npm start

## API Endpoints
### Authentication Routes
#### Register a new user

- URL: /api/users/register
- Method: POST
- Access: Public
- Description: Allows a new user to register by providing an email, username, and password.

    ```
    {
        "email": "user@example.com",
        "username": "username123",
        "password": "securePassword"
    }

#### User Login
- URL: /api/users/login
- Method: POST
- Access: Public
- Description: Authenticates a user and returns a JWT token.

    ```bash
    {  
        "email": "user@example.com",
        "password": "securePassword"
    }

#### Get Current User Info

- URL: /api/users/current
- Method: POST
- Access: Private (JWT token required)
- Description: Returns the currently authenticated user's information.

### Contact Routes

#### Get All Contacts

- URL: /api/contacts
- Method: GET
- Access: Private (JWT token required)
- Description: Retrieves all contacts for the authenticated user.

#### Get a Single Contact

- URL: /api/contacts/:id
- Method: GET
- Access: Private (JWT token required)
- Description: Retrieves a specific contact by its ID.

#### Create a New Contact

- URL: /api/contacts
- Method: POST
- Access: Private (JWT token required)
- Description: Allows an authenticated user to create a new contact.

    ```bash
     {
        "name": "John Doe",
        "email": "john@example.com",
        "phone": "123-456-7890"
     }

#### Update a Contact

- URL: /api/contacts/:id
- Method: PUT
- Access: Private (JWT token required)
- Description: Allows an authenticated user to update a contact. The contact must belong to the logged-in user.

#### Delete a Contact

- URL: /api/contacts/:id
- Method: DELETE
- Access: Private (JWT token required)
- Description: Allows an authenticated user to delete a contact. The contact must belong to the logged-in user.

## Error Handling
The application includes comprehensive error handling, returning appropriate error messages and status codes for:

- Validation errors
- Unauthorized access
- Not found resources
- Forbidden actions
- Server errors

## Middleware
### JWT Validation
JWT tokens are used to validate and authenticate users for secure access to protected routes. Tokens must be provided in the Authorization header as a Bearer token.

### Error Handling
Custom error handling middleware is used to ensure that any exceptions are caught and appropriate error responses are sent to the client.

## License
This project is licensed under the MIT License. See the LICENSE file for more details.

    ```bash
    
        You can adjust the repository link, environment variable names, or any other specific details as needed.

Thank's for coming so far.
Wish you a great time AHEAD.



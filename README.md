# Trading Terminal RBAC API

A FastAPI-based backend API for a trading terminal with Role-Based Access Control (RBAC). This API provides secure authentication and authorization, user and role management, and trade execution capabilities.

## Features

- **Authentication and Authorization**: Uses JWT tokens for secure authentication and checks permissions for each request.
- **Role-Based Access Control (RBAC)**: Defines roles and permissions, allowing users to be assigned roles with inherited permissions.
- **Storage Abstraction**: An abstract storage interface allows for easy swapping of database backends.
- **Middleware**: Middleware checks permissions for each request to ensure users have the appropriate access.
- **API Endpoints**: Provides endpoints for user management, role management, and trade execution.
- **Health Checks**: Includes a health check endpoint to verify the status of the API and storage backend.

## Authentication and Authorization

The API uses JWT (JSON Web Tokens) for authentication. When a user logs in, they receive a JWT token which they must include in the headers of subsequent requests. This token is used to verify the user's identity and permissions.

Permissions are checked for each request to ensure the user has the necessary access rights.

## RBAC (Role-Based Access Control)

The API implements a Role-Based Access Control (RBAC) system where roles and permissions are defined. Users are assigned roles, and roles can inherit permissions from parent roles.

### Roles and Permissions

- **Roles**: Define a set of permissions. Examples include "viewer", "trader", and "admin".
- **Permissions**: Granular access rights such as "market:read", "trade:execute", etc.
- **Inheritance**: Roles can inherit permissions from parent roles. For example, the "trader" role inherits permissions from the "viewer" role.

## Storage Abstraction

The API uses an abstract storage interface that allows for easy swapping of database backends. This abstraction layer ensures that the API can work with different databases without changing the core logic.

### StorageInterface

An abstract base class defines the contract for storage operations. Concrete implementations, such as `RedisStorage`, implement these methods for specific databases.

## Middleware

Middleware is used to check permissions for each request. It skips public endpoints and verifies the JWT token for protected endpoints. The middleware ensures that users have the required permissions to access specific endpoints.

## API Endpoints

The API provides several endpoints for user management, role management, and trade execution.

### Authentication

- **POST /login**: Authenticate a user and receive a JWT token.

### Users

- **POST /users**: Create a new user.
- **GET /me**: Get information about the current user.
- **GET /my-permissions**: Get the permissions of the current user.

### Roles

- **POST /roles**: Create a new role.
- **POST /assign-role**: Assign a role to a user.

### Trading

- **POST /execute-trade**: Execute a trade.

### Health Checks

- **GET /health**: Check the health of the API and storage backend.
- **GET /**: Get the root endpoint information.

## Health Checks

The health check endpoint verifies the status of the API and storage backend.

- **GET /health**: Returns the status of the API and storage backend.

Example response:
```json
{
  "api": "running",
  "storage": "ok",
  "timestamp": "2023-10-01T12:00:00Z"
}

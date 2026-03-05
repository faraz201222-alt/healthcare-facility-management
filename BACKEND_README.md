# BACKEND_README

## Prerequisites
- Node.js v14 or higher
- npm (Node Package Manager)
- MongoDB or any relational database
- Postman or any API client for testing endpoints

## Installation Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/faraz201222-alt/healthcare-facility-management.git
   cd healthcare-facility-management
   ```
2. Install dependencies:
   ```bash
   npm install
   ```

## Environment Setup
1. Create a `.env` file in the root directory:
   ```bash
   cp .env.example .env
   ```
2. Fill in the `.env` file with your environment variables, such as:
   - `DB_URI`: MongoDB connection string
   - `PORT`: Port on which the server will run

## Database Configuration
- Ensure your database is running.
- For MongoDB, set `DB_URI` in the `.env` file as follows:
  ```bash
  DB_URI=mongodb://localhost:27017/your_database_name
  ```

## Running the Server
- To start the server, run:
  ```bash
  npm start
  ```
- The server will be running on the port specified in your `.env` file.

## API Endpoints
| Method | Endpoint                 | Description              |
|--------|--------------------------|--------------------------|
| GET    | /api/v1/health           | Check server health      |
| POST   | /api/v1/users            | Create a new user       |
| GET    | /api/v1/users/:id        | Get user by ID          |
| PUT    | /api/v1/users/:id        | Update user by ID       |
| DELETE | /api/v1/users/:id        | Delete user by ID       |

## Troubleshooting Guide
- **Server not starting:**
  - Check if the port is already in use.
  - Ensure your database is running and the connection string is correct.
- **API not responding:**
  - Use Postman to test your endpoints.
  - Check server logs for any errors.
- **Dependency issues:**
  - Run `npm install` again to ensure all dependencies are installed correctly.

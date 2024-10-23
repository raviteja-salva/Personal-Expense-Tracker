# Personal Expense Tracker API

A RESTful API built with Node.js and Express.js for managing personal financial records. Users can track their income and expenses, manage categories, and view financial summaries.

## Technologies Used

- Node.js
- Express.js
- MongoDB
- JWT for Authentication

## Prerequisites

Before running this project, make sure you have the following installed:
- Node.js (v14 or higher)
- MongoDB
- Postman (for testing APIs)

## Project Setup

1. Clone the repository
```bash
git clone https://github.com/yourusername/personal-expense-tracker.git
cd personal-expense-tracker
```

2. Install dependencies
```bash
npm install
```

3. Create a `.env` file in the root directory with the following variables:
```
PORT=3000
MONGODB_URI=mongodb://localhost:27017/expense-tracker
JWT_SECRET=your_jwt_secret_key
```

4. Start the server
```bash
node server.js
```

The API will be available at `http://localhost:3000`

## API Documentation

### Authentication

All API endpoints (except signup and login) require JWT authentication. Include the token in the request header:
```
Authorization: Bearer <your_jwt_token>
```

#### Authentication Endpoints

##### 1. User Signup
- **Endpoint**: `POST /api/auth/register`
- **Body**:
```json
{
    "email": "user@example.com",
    "password": "your_password"
}
```
- **Response**:
```json
{
    "message": "User created successfully",
    "userId": "user_id"
}
```
![Description of Image](./src/screenshots/Screenshot%20(505).png)


##### 2. User Login
- **Endpoint**: `POST /api/auth/login`
- **Body**:
```json
{
    "email": "user@example.com",
    "password": "your_password"
}
```
- **Response**:
```json
{
    "token": "jwt_token",
    "userId": "user_id"
}
```
![Description of Image](./src/screenshots/Screenshot%20(506).png)


### Categories

#### 1. Create Category
- **Endpoint**: `POST /categories`
- **Body**:
```json
{
    "name": "Groceries",
    "type": "expense"
}
```
- **Response**: Returns the created category object
![Description of Image](./src/screenshots/Screenshot%20(507).png)

#### 2. Get All Categories
- **Endpoint**: `GET /categories`
- **Response**: Returns array of all categories

#### 3. Get Category by ID
- **Endpoint**: `GET /categories/:id`
- **Response**: Returns single category object

#### 4. Update Category
- **Endpoint**: `PUT /categories/:id`
- **Body**:
```json
{
    "name": "Updated Category Name"
}
```
- **Response**: Returns updated category object

#### 5. Delete Category
- **Endpoint**: `DELETE /categories/:id`
- **Response**: Returns success message

### Transactions

#### 1. Create Transaction
- **Endpoint**: `POST /transactions`
- **Body**:
```json
{
    "type": "expense",
    "category": "category_id",
    "amount": 50.00,
    "date": "2024-03-15",
    "description": "Weekly groceries"
}
```
- **Response**: Returns created transaction object
![Description of Image](./src/screenshots/Screenshot%20(511).png)


#### 2. Get All Transactions
- **Endpoint**: `GET /transactions`
- **Response**: Returns array of transactions
![Description of Image](./src/screenshots/Screenshot%20(508).png)

#### 3. Get Transaction by ID
- **Endpoint**: `GET /transactions/:id`
- **Response**: Returns single transaction object
![Description of Image](./src/screenshots/Screenshot%20(509).png)

#### 4. Update Transaction
- **Endpoint**: `PUT /transactions/:id`
- **Body**:
```json
{
    "amount": 45.00,
    "description": "Updated description"
}
```
- **Response**: Returns updated transaction object
![Description of Image](./src/screenshots/Screenshot%20(513).png)

#### 5. Delete Transaction
- **Endpoint**: `DELETE /transactions/:id`
- **Response**: Returns success message
![Description of Image](./src/screenshots/Screenshot%20(509).png)


### Summary

#### Get Financial Summary
- **Endpoint**: `GET /summary`
- **Query Parameters**:
  - `startDate`: Start date for summary (YYYY-MM-DD)
  - `endDate`: End date for summary (YYYY-MM-DD)
  - `category`: Filter by category ID
- **Response**:
```json
{
    "totalIncome": 1000.00,
    "totalExpenses": 450.00,
    "balance": 550.00,
}
```
![Description of Image](./src/screenshots/Screenshot%20(514).png)

## Screenshots
- Postman screenshots added in './src/screenshots' file

## Error Handling

The API returns appropriate HTTP status codes:
- 200: Success
- 201: Created
- 400: Bad Request
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 500: Internal Server Error

Error responses follow this format:
```json
{
    "error": "Error message here"
}
```

## Collection Structure

### Transactions Collection
```json
{
    "_id": "ObjectId",
    "type": "income|expense",
    "category": "ObjectId (reference to categories collection)",
    "amount": "Number",
    "date": "Date",
    "description": "String",
    "userId": "ObjectId (reference to users collection)",
    "createdAt": "Date",
    "updatedAt": "Date"
}
```

### Categories Collection
```json
{
    "_id": "ObjectId",
    "name": "String",
    "type": "income|expense",
    "userId": "ObjectId (reference to users collection)",
    "createdAt": "Date",
    "updatedAt": "Date"
}
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request


## License

This project is licensed under the MIT License - see the LICENSE file for details.

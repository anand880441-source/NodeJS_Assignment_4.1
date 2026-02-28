# State Statistics Management API  
## Assignment 3 – Full REST Implementation (GET, POST, PUT, PATCH, DELETE)

---

## Objective

Build a complete REST API using Express.js that manages statistical data of Indian states stored inside an in-memory JSON array.

The application:

- Uses GET, POST, PUT, PATCH, and DELETE routes  
- Includes static and dynamic routes  
- Follows REST architecture principles  
- Uses proper HTTP status codes  
- Demonstrates the difference between PUT and PATCH  
- Performs dynamic array manipulation  

No database is used.  
No authentication.  
No validation libraries.  

All operations modify the in-memory array directly.

---

## State Record Structure

Each state object follows this structure:

```js
{
  id: 1,
  name: "Gujarat",
  population: 63872399,
  literacyRate: 78.03,
  annualBudget: 243965,
  gdp: 21000000
}
```

### Field Description

- `id` → Unique identifier (Number)  
- `name` → State name (String)  
- `population` → Total population (Number)  
- `literacyRate` → Literacy percentage (Number)  
- `annualBudget` → Annual state budget in crores (Number)  
- `gdp` → State GDP in crores (Number)  

The project initializes 28 Indian states inside the `states` array in `index.js`.

---

# Implemented Routes

---

## 1. GET /

Checks if the server is running.

Response:

```
State Statistics API is running
```

Status Code: 200

---

## 2. GET /states

Returns all states.

- Status Code: 200  
- Returns full JSON array  

---

## 3. GET /states/:id

Returns a state by ID.

Example:

```
GET /states/5
```

- If state exists → 200  
- If not found → 404  

Error Response:

```json
{
  "message": "State not found"
}
```

---

## 4. GET /states/highest-gdp

Returns the state with the highest GDP.

- Uses reduce() or sorting  
- Returns a single object  
- Status Code: 200  

---

## 5. POST /states

Creates a new state.

Request Body:

```json
{
  "name": "Haryana",
  "population": 25351462,
  "literacyRate": 75.55,
  "annualBudget": 180000,
  "gdp": 10000000
}
```

Response:

```json
{
  "message": "State created",
  "state": {
    "id": 29,
    "name": "Haryana",
    "population": 25351462,
    "literacyRate": 75.55,
    "annualBudget": 180000,
    "gdp": 10000000
  }
}
```

- Status Code: 201  
- ID is generated automatically  

---

## 6. PUT /states/:id

Replaces an entire state record (except ID).

Example:

```
PUT /states/3
```

- If state exists → 200  
- If not found → 404  

Success Response:

```json
{
  "message": "State replaced",
  "state": { ... }
}
```

---

## 7. PUT /states/:id/budget

Replaces only the annualBudget value.

Example:

```
PUT /states/7/budget
```

Request Body:

```json
{
  "annualBudget": 260000
}
```

- Status Code: 200  
- If not found → 404  

---

## 8. PUT /states/:id/population

Replaces only the population value.

Example:

```
PUT /states/4/population
```

Request Body:

```json
{
  "population": 110000000
}
```

- Status Code: 200  
- If not found → 404  

---

## 9. PATCH /states/:id/literacy

Updates only literacyRate.

Example:

```
PATCH /states/6/literacy
```

Request Body:

```json
{
  "literacyRate": 90.5
}
```

- Status Code: 200  
- If not found → 404  

---

## 10. PATCH /states/:id/gdp

Updates only gdp.

Example:

```
PATCH /states/10/gdp
```

Request Body:

```json
{
  "gdp": 5000000
}
```

- Status Code: 200  
- If not found → 404  

---

## 11. PATCH /states/:id

Partially updates any provided fields.

Example:

```
PATCH /states/12
```

Request Body:

```json
{
  "annualBudget": 280000
}
```

Only provided fields are updated.

- Status Code: 200  
- If not found → 404  

---

## 12. DELETE /states/:id

Deletes a state by ID.

Example:

```
DELETE /states/8
```

- If found → 204  
- If not found → 404  

---

## 13. DELETE /states/name/:stateName

Deletes a state by name (case-insensitive).

Example:

```
DELETE /states/name/Goa
```

- Status Code: 204  
- If not found → 404  

---

## 14. DELETE /states/low-literacy/:percentage

Deletes all states where literacyRate is less than the given percentage.

Example:

```
DELETE /states/low-literacy/70
```

Response:

```json
{
  "deletedCount": 2
}
```

- Status Code: 200  

---

# Steps to Run Locally

1. Clone the repository  
2. Run:

```
npm install
```

3. Install required packages:

```
npm install express cors
```

4. Start the server:

```
node index.js
```

5. Server runs on:

```
http://localhost:3000
```

---

# Notes

- Data is stored in-memory (array), so restarting the server resets all changes  
- No database is connected  
- No validation is implemented  
- ID is generated dynamically  
- Proper HTTP status codes are used (200, 201, 204, 404)  

---

# Tools for Testing

- Postman  
- Thunder Client  
- cURL  
- Any REST client  

---

# GitHub Repository

https://github.com/anand880441-source/NodeJS_Assignment_4.1

---

# Postman Documentation

https://documenter.getpostman.com/view/50840839/2sBXcHheVE

---

# Render Deployment

https://nodejs-assignment-4-1.onrender.com/states

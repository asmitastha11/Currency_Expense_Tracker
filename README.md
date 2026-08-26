# 💰 Currency Expense Tracker

A full-stack expense tracking application built with **React** and **Node.js + Express**.

This application allows users to add expenses in different currencies, select a home currency, convert expenses into the selected currency, and view the running total.

This project was developed as part of the **Tech LeadHers Fellowship Take-Home Assignment**.

---

## 🚀 Features

- Add new expenses
- View all expenses
- Delete expenses
- Select expense currency
- Select a home currency
- Convert expenses into the selected home currency
- Calculate the running total
- Input validation
- Loading states
- Error handling
- Graceful handling of exchange-rate API failures
- Responsive user interface
- Plain CSS styling
- In-memory expense storage
- Backend-proxied currency conversion

---

## 🛠️ Tech Stack

### Frontend

- React
- JavaScript
- CSS
- Fetch API

### Backend

- Node.js
- Express.js
- JavaScript

### Currency API

The backend uses the **Frankfurter Exchange Rate API**:

`https://api.frankfurter.dev/v2/rate/{from}/{to}`

No API key is required.

The React frontend does **not** call Frankfurter directly. Instead, it calls the application's `/convert` endpoint, and the Express server makes the external API request.

## Project Structure

```text
Currency_Expese_Tracker-main/
│
├── backend/
│   ├── package.json
│   ├── package-lock.json
│   └── server.js
│
├── frontend/
│   ├── package.json
│   ├── package-lock.json
│   ├── vite.config.js
│   └── src/
│       ├── components/
│       │   ├── currency_selector.jsx
│       │   ├── expense_form.jsx
│       │   └── expense_list.jsx
│       ├── services/
│       │   └── api.js
│       ├── App.jsx
│       ├── App.css
│       ├── index.css
│       └── main.jsx
│
├── .gitignore
└── README.md
```

## Requirements

Make sure the following are installed:

- Node.js
- npm

The backend and frontend are separate Node.js projects, so dependencies must be installed in both directories.

## Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/asmitastha11/Currency_Expense_Tracker.git
cd Currency_Expense_Tracker
```
### 2. Install backend dependencies

Open a terminal in the project root and run:

```bash
cd backend
npm install
```

### 3. Start the backend

From the `backend` directory:

```bash
npm start
```

The backend runs at:

```text
http://localhost:5000
```

The API can be checked at:

```text
http://localhost:5000/
```

Expected response:

```json
{
  "message": "Expense Tracker API is running"
}
```

### 4. Install frontend dependencies

Open another terminal and run:

```bash
cd frontend
npm install
```

### 5. Start the frontend

From the `frontend` directory:

```bash
npm start
```

Vite will provide the local frontend URL in the terminal, normally:

```text
http://localhost:5173
```

Keep both the backend and frontend running at the same time.

## API Endpoints

### GET `/expenses`

Returns all expenses currently stored in memory.

Example:

```text
GET http://localhost:5000/expenses
```

### POST `/expenses`

Adds a new expense.

Example request:

```json
{
  "title": "Lunch",
  "amount": 500,
  "currency": "NPR"
}
```

Example:

```text
POST http://localhost:5000/expenses
```

The backend validates:

- Title must not be empty
- Amount must be a valid positive number
- Currency must be supported

### DELETE `/expenses/:id`

Deletes an expense by its ID.

Example:

```text
DELETE http://localhost:5000/expenses/1
```

### GET `/convert`

Converts an amount from one supported currency to another.

Example:

```text
GET http://localhost:5000/convert?from=USD&to=NPR&amount=100
```

The Express backend calls the Frankfurter API and returns the converted amount.

## Supported Currencies

The application currently supports:

- USD
- NPR
- EUR
- INR
- GBP

These currencies are validated by the backend before an expense is stored or a conversion is requested.

## Error Handling

The application handles several failure cases.

### Backend validation

Invalid requests return appropriate HTTP error responses for cases such as:

- Missing title
- Empty title
- Missing amount
- Invalid or non-positive amount
- Missing currency
- Unsupported currency
- Invalid expense ID
- Expense not found

### Currency API failures

The `/convert` endpoint handles external service failures without crashing the Express server.

A request timeout is also configured. If the external service takes too long, the backend returns an appropriate error response.

The frontend displays a conversion error when one or more expenses cannot be converted.

## Data Storage

No database is used.

Expenses are stored in an in-memory JavaScript array inside the Express server. This follows the assignment requirement and means that expenses are cleared whenever the backend server is restarted.

## Design Decisions

### Backend-proxied currency conversion

The frontend communicates only with the application's `/convert` endpoint. The Express server is responsible for communicating with Frankfurter.

This keeps the external API interaction on the backend and follows the assignment requirement.

### In-memory storage

A simple JavaScript array is used instead of introducing a database because persistent storage was explicitly excluded from the assignment.

### Component structure

The React application separates the main responsibilities into components:

- `ExpenseForm` handles adding expenses
- `ExpenseList` displays and deletes expenses
- `CurrencySelector` handles home-currency selection
- `App` manages the main application state and conversion workflow

## Assumptions

- Only USD, NPR, EUR, INR, and GBP are required and therefore supported.
- Expense data does not need to persist after restarting the backend.
- The backend and frontend run locally on separate ports during development.
- Frankfurter is available through the user's network connection when conversion is required.
- When the selected home currency is the same as an expense's currency, the backend returns the original amount without making an external conversion request.

## Possible Improvements

With more development time, the application could be extended with:

- Conversion-result caching to reduce repeated API requests
- Automated frontend and backend tests
- More extensive currency support
- A configurable backend URL through environment variables
- Improved offline fallback or cached exchange rates
- Pagination for a large number of expenses
- More detailed expense categories and filtering
- Persistent storage if the application requirements were expanded

## Running the Application

Two terminals are required.

### Terminal 1 — Backend

```bash
cd backend
npm install
npm start
```

### Terminal 2 — Frontend

```bash
cd frontend
npm install
npm start
```

Then open the frontend URL provided by Vite.

## Assignment Submission

This project was created for the **Tech LeadHers Fellowship Take-Home Assignment**.



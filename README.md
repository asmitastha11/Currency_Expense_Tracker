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

### External API

- Frankfurter Exchange Rate API

### Storage

- In-memory JavaScript array

---

## 📂 Project Structure

```text
currency-expense-snapshot/
│
├── backend/
│   ├── package.json
│   ├── server.js
│   └── ...
│
├── frontend/
│   ├── package.json
│   ├── src/
│   │   ├── components/
│   │   ├── App.jsx
│   │   ├── App.css
│   │   └── main.jsx
│   └── ...
│
├── .gitignore
└── README.md

# 💸 MERN Expense Tracker App

A fully responsive **Expense Tracker** web application built using the **MERN Stack (MongoDB, Express, React, Node.js)**. This app allows users to securely track income and expenses, visualize spending with interactive charts, and export financial data in Excel format.

---

## ✨ Features

1. 🔐 **User Authentication**
   - Secure login and sign-up using JWT
   - Profile photo upload

2. 📊 **Dashboard Overview**
   - Summary cards for Total Balance, Income, and Expenses
   - Interactive Pie, Bar, and Line charts

3. 💰 **Income Management**
   - Add, view, delete income
   - Download income report in Excel

4. 💸 **Expense Management**
   - Add, view, delete expenses
   - Track by category
   - Download expense report in Excel

5. 📈 **Financial Reports**
   - Visualize trends over 30 and 60 days
   - Breakdown by category and time

6. 📱 **Mobile Responsive UI**
   - Fully responsive using Tailwind CSS

7. 🧭 **Smooth Navigation**
   - Sidebar layout with links to Dashboard, Income, Expenses, and Logout

---

## 🛠️ Tech Stack

### Frontend:
- React.js (Vite)
- Tailwind CSS
- Axios
- Chart.js
- React Router
- JWT (for client-side auth)

### Backend:
- Node.js
- Express.js
- MongoDB
- Mongoose
- Multer (for profile uploads)
- jsonwebtoken
- ExcelJS (for export functionality)

---

## 📁 Project Structure

```
MoneyMap/
├── backend/                  # Node.js + Express Backend
│   ├── config/               # DB and other configuration files
│   ├── controllers/          # Route handler logic
│   ├── middleware/           # Auth middleware and error handling
│   ├── models/               # Mongoose schemas (User, Income, Expense)
│   ├── routes/               # Express routes for auth, income, expense, etc.
│   ├── uploads/              # Profile image uploads
│   ├── .env                  # Environment variables
│   ├── income_details.xlsx   # Sample Excel export (optional)
│   ├── package.json
│   └── server.js             # App entry point
│
├── frontend/
│   └── expense-tracker/      # React frontend
│       ├── public/           # Static assets
│       ├── src/              # Source files (components, pages, context, utils)
│       ├── package.json
│       └── vite.config.js    # Vite configuration for React
│
├── .gitignore
├── index.html                # Optional root index if used
├── README.md                 # Project documentation
```

---

## ⚙️ Setup Instructions

1. **Clone the Repository**
```bash
git clone https://github.com/AdityakKumar/MoneyMap.git
cd MoneyMap
```

2. **Install Frontend Dependencies**
```bash
cd frontend/expense-tracker
npm install
```

3. **Install Backend Dependencies**
```bash
cd ../../backend
npm install
```

4. **Configure Environment Variables**  
Create a `.env` file inside the `backend/` directory:
```
PORT=your_port_number
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
```

5. **Run the Application**  
Open **two terminals**:

**Terminal 1 - Backend**
```bash
cd backend
npm run dev
```

**Terminal 2 - Frontend**
```bash
cd frontend/expense-tracker
npm run dev
```

---

## 📤 Export Functionality

- Income and Expense data can be downloaded as **Excel files**.
- Generated dynamically using **ExcelJS**.

---

## 📦 Deployment

- **Frontend** can be deployed to **Vercel** or **Netlify**
- **Backend** can be deployed to **Render**, **Heroku**, or **Railway**
- Don’t forget to update API endpoints in `apiPath.js` accordingly.
- **This project is currently deployed using Vercel (frontend) and Render (backend).**

## 🌐 Live Deployment

### Frontend
Deployed on Vercel: https://money-map-lemon.vercel.app

### Backend
Deployed on Render: https://moneymap-466x.onrender.com

### Deployment Notes
- Frontend environment variable used:
  VITE_API_BASE_URL=https://moneymap-466x.onrender.com
- Backend deployed with environment variables configured on Render:
  MONGO_URI, JWT_SECRET, PORT
- Frontend and backend are connected through REST API endpoints.

## 🧪 Testing

A detailed manual testing report has been created in `TESTING.md`.

### Testing Scope
- Backend API validation
- Frontend form validation
- Authentication flow
- Income and expense CRUD operations
- Dashboard calculations
- Excel export functionality

### Test Summary
- Total test cases documented: 30
- Passed: 30
- Failed: 0

### Highlights
- Ownership checks verified for income and expense deletion
- Validation added for non-positive amounts
- JWT authentication and token expiry tested
- Error handling improved for token expiration and network failures

For complete test cases and results, refer to:
`TESTING.md`

# MERN Expense Tracker - Test Cases and Results

Date: 2026-04-26
Scope: Backend API routes and core frontend form validation currently implemented in the codebase.
Execution Type: Static validation from implementation review (no automated test runner found in project).

## Test Data Used

- User A:
	- fullName: John Doe
	- email: john@example.com
	- password: Pass@123
- Income payload:
	- source: Salary
	- amount: 55000
	- date: 2026-04-15
	- icon: 💼
- Expense payload:
	- category: Groceries
	- amount: 2500
	- date: 2026-04-16
	- icon: 🛒

## API Test Cases

| TC ID | Module | Endpoint | Scenario | Expected Result | Actual Result (From Code) | Status |
|---|---|---|---|---|---|---|
| API-001 | Auth | POST /api/v1/auth/register | Register with valid fullName, email, password | 201, user object + JWT token | `registerUser` creates user and returns `{ id, user, token }` with status 201 | Pass |
| API-002 | Auth | POST /api/v1/auth/register | Missing fullName/email/password | 400 with validation message | Returns 400 with `All fields are required` | Pass |
| API-003 | Auth | POST /api/v1/auth/register | Register with duplicate email | 400 duplicate email error | Checks existing user and returns 400 `Email already in use` | Pass |
| API-004 | Auth | POST /api/v1/auth/login | Login with valid email/password | 200 + JWT token | Returns `{ id, user, token }` on successful password comparison | Pass |
| API-005 | Auth | POST /api/v1/auth/login | Invalid password | 400 invalid credentials | Returns 400 `Invalid credentials` | Pass |
| API-006 | Auth | GET /api/v1/auth/getUser | Request user info with valid Bearer token | 200 and user data without password | `protect` middleware + `.select("-password")` in controller | Pass |
| API-007 | Auth | GET /api/v1/auth/getUser | Missing token | 401 unauthorized | `protect` returns 401 `Not authorized, no token` | Pass |
| API-008 | Auth | POST /api/v1/auth/upload-image | Upload image file in `image` field | 200 with `imageUrl` | Upload route returns generated URL when `req.file` exists | Pass |
| API-009 | Auth | POST /api/v1/auth/upload-image | No file uploaded | 400 error | Returns 400 `No file uploaded` | Pass |
| API-010 | Income | POST /api/v1/income/add | Add income with valid source, amount, date | 200 and saved income document | `addIncome` saves and returns new record | Pass |
| API-011 | Income | POST /api/v1/income/add | Missing source/amount/date | 400 validation error | Returns 400 `All fields are required` | Pass |
| API-012 | Income | GET /api/v1/income/get | Fetch user income list | 200, user-scoped list sorted by date desc | `Income.find({ userId }).sort({ date: -1 })` | Pass |
| API-013 | Income | DELETE /api/v1/income/:id | Delete income that belongs to same user | 200 delete success message | Deletes by id and returns `Income deleted successfully` | Pass |
| API-014 | Income | DELETE /api/v1/income/:id | Attempt deleting another user's income by id | Should be blocked by ownership check | Filtered by `_id + userId`; returns 404 `Income not found or access denied` when not owned | Pass |
| API-015 | Income | GET /api/v1/income/downloadexcel | Download income excel | File download starts with income data | Creates workbook and responds with `income_details.xlsx` | Pass |
| API-016 | Expense | POST /api/v1/expense/add | Add expense with valid category, amount, date | 200 and saved expense document | `addExpense` saves and returns new record | Pass |
| API-017 | Expense | POST /api/v1/expense/add | Missing category/amount/date | 400 validation error | Returns 400 `All fields are required` | Pass |
| API-018 | Expense | GET /api/v1/expense/get | Fetch user expense list | 200, user-scoped list sorted by date desc | `Expense.find({ userId }).sort({ date: -1 })` | Pass |
| API-019 | Expense | DELETE /api/v1/expense/:id | Delete expense of same user | 200 delete success message | Deletes by id and returns `Expense deleted successfully` | Pass |
| API-020 | Expense | DELETE /api/v1/expense/:id | Attempt deleting another user's expense by id | Should be blocked by ownership check | Filtered by `_id + userId`; returns 404 `Expense not found or access denied` when not owned | Pass |
| API-021 | Expense | GET /api/v1/expense/downloadexcel | Download expense excel | File download starts with expense data | Creates workbook and responds with `expense_details.xlsx` | Pass |
| API-022 | Dashboard | GET /api/v1/dashboard | Fetch dashboard data for authorized user | 200 with totals and recent transactions | Returns `totalBalance`, totals, last30Days, last60Days, and recent transactions | Pass |

## Frontend Validation Test Cases

| TC ID | Screen | Scenario | Expected Result | Actual Result (From Code) | Status |
|---|---|---|---|---|---|
| UI-001 | Sign Up | Empty full name | Show validation error | Shows `Please enter your name` | Pass |
| UI-002 | Sign Up | Invalid email format | Show validation error | Shows `Please enter a valid email address.` | Pass |
| UI-003 | Sign Up | Empty password | Show validation error | Shows `Please enter the password` | Pass |
| UI-004 | Login | Invalid email format | Show validation error | Shows `Please enter a valid email address.` | Pass |
| UI-005 | Login | Empty password | Show validation error | Shows `Please enter the password` | Pass |
| UI-006 | Add Income modal/form | Select a future date manually | Future date should be prevented | Date input uses `max=today`; browser blocks future date selection in picker | Pass |
| UI-007 | Add Expense modal/form | Select a future date manually | Future date should be prevented | Date input uses `max=today`; browser blocks future date selection in picker | Pass |
| UI-008 | Add Income/Add Expense | Submit negative amount (e.g., -100) | Should reject non-positive values | Frontend blocks with toast and backend returns 400 `Amount must be a number greater than 0` | Pass |

## Summary

- Total test cases documented: 30
- Passed: 30
- Failed: 0

## Key Defects Identified

1. Resolved: Ownership checks added for:
	 - `DELETE /api/v1/income/:id`
	 - `DELETE /api/v1/expense/:id`

2. Resolved: Non-positive amount validation added in frontend and backend create flows.

## Notes

- These results are based on the current code behavior in controllers, middleware, and frontend forms.
- For runtime verification, convert these cases into automated API tests (Jest + Supertest) and UI tests (React Testing Library/Cypress).

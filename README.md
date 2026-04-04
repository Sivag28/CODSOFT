# CODSOFT
Web Development Internship (MERN STACK)
# 1)ECOMMERCE APPLICATION
## ShopVerse

ShopVerse is a MERN e-commerce project for browsing and ordering handmade-style products. The app includes authentication, category-based product browsing, cart and wishlist management, checkout with shipping details, order history, invoice download, and post-purchase reviews.

This README is based on the code currently present in this repository.

## What the project does

- Users can sign up and log in with JWT-based authentication.
- After login, users land on a home page with 12 product categories.
- Products are fetched from MongoDB and filtered by category.
- Each product has a details page with price, stock, rating, description, and quantity selection.
- Users can add products to cart and save products to a wishlist.
- Users can place an order by entering shipping information and choosing `COD` or `online` as the payment method.
- After checkout, the app stores the order, shows an invoice view, and lets the user download the invoice as PDF.
- Users can view past orders and submit one review per purchased product.
- There is also a separate flash deals page with hardcoded deal items stored on the frontend.

## Implemented modules

### Frontend

- React 19 + Vite
- React Router for page routing
- Redux Toolkit for cart, wishlist, and user state
- Axios for API calls
- SweetAlert2 for alerts
- `html2canvas` + `jspdf` for invoice PDF download

### Backend

- Node.js + Express
- MongoDB + Mongoose
- JWT authentication
- Product, cart, wishlist, order, and review APIs

## Main user flows

1. Register or log in
2. Browse categories from the home page
3. Open a category to see products from MongoDB
4. View a product and add it to cart or buy now
5. Save products to wishlist
6. Checkout with shipping address and payment method
7. View orders and download invoices
8. Leave a review for ordered products

## Routes in the app

Frontend routes:

- `/login`
- `/signup`
- `/`
- `/category/:name`
- `/product/:id`
- `/cart`
- `/checkout`
- `/wishlist`
- `/orders`
- `/deals`

Backend API routes:

- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/products`
- `GET /api/products/deals`
- `GET /api/products/:id`
- `POST /api/products/:id/reviews`
- `GET /api/products/:id/reviews`
- `GET /api/products/:id/check-review`
- `GET /api/cart`
- `POST /api/cart`
- `GET /api/wishlist`
- `POST /api/wishlist/:id`
- `GET /api/orders`
- `POST /api/orders`

## Project structure

```text
.
|-- README.md
|-- TODO.md
|-- ecomm_mern
|   |-- backend
|   |   |-- config
|   |   |-- controllers
|   |   |-- middleware
|   |   |-- models
|   |   |-- routes
|   |   |-- server.js
|   |   `-- seedProducts.js
|   `-- frontend
|       |-- public
|       |-- src
|       |-- package.json
|       `-- vite.config.js
`-- project_management
```

The e-commerce app described here lives in `ecomm_mern/backend` and `ecomm_mern/frontend`.

## Tech stack

- Frontend: React, Vite, React Router, Redux Toolkit, Tailwind CSS
- Backend: Node.js, Express, Mongoose
- Database: MongoDB
- Utilities: Axios, SweetAlert2, jsPDF, html2canvas

## Setup

### Prerequisites

- Node.js
- MongoDB connection string

### Backend

```bash
cd ecomm_mern/backend
npm install
```

Create `ecomm_mern/backend/.env` with:

```env
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
```

Start the backend:

```bash
node server.js
```

The backend listens on `http://localhost:5000`.

### Seed products

To populate the database:

```bash
cd ecomm_mern/backend
node seedProducts.js
```

The seed script creates an admin user if needed and inserts products based on the available product images.

### Frontend

```bash
cd ecomm_mern/frontend
npm install
npm run dev
```

The frontend expects the backend API at `http://localhost:5000/api`.

## Notes about current behavior

- The `/deals` page uses hardcoded frontend data rather than database-backed products.
- Deal items are stored differently from MongoDB products, so cart and review handling contains special-case logic for them.
- The checkout form lets users choose `COD` or `online`, but the backend currently stores the selected method only. There is no working payment gateway flow in the present code.
- The backend imports `razorpay`, but no active Razorpay payment flow is wired into the checkout process.
- There are no automated tests configured in the current project.
- User login state is kept in Redux, while only the token is saved to `localStorage`, so a browser refresh may require logging in again in the UI.

## Sample features visible in code

- Category browsing across 12 categories
- Product reviews with duplicate-review prevention
- Order history page with invoice modal and PDF export
- Wishlist and cart persistence using API plus `localStorage` handling

## Scripts currently available

Backend:

- No dedicated start script is defined in `package.json`
- Run with `node server.js`

Frontend:

- `npm run dev`
- `npm run build`
- `npm run lint`
- `npm run preview`

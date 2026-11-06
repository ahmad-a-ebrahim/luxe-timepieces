# Luxe Timepieces

A full-stack e-commerce web app for luxury watches: browse products, save favorites, manage a shopping basket, and administer products and users through an admin dashboard.

## Project Status

| Area | Status |
| --- | --- |
| Authentication (register / login / logout) | ✅ Done |
| Product catalog (browse, details) | ✅ Done |
| Favorites | ✅ Done |
| Shopping basket (add, remove, quantity) | ✅ Done |
| Admin dashboard (products CRUD, users) | ✅ Done |
| Dark / light theme | ✅ Done |
| Checkout / payments | ❌ Not implemented |
| Automated tests | ❌ Only Laravel example tests |
| Deployment configuration | ❌ Local development only |

_Last updated: 2026-11-06_

## Tech Stack

**Frontend** (`frontend/`)
- React 18 + Vite
- Redux Toolkit, React Router 6
- Material UI 5, Swiper
- Formik + Yup, Axios, universal-cookie

**Backend** (`backend/laravel/`)
- Laravel (PHP) REST API
- Laravel Sanctum token authentication
- SQLite by default (configurable via `.env`)

## Project Structure

```
Luxe-Timepieces/
├── frontend/             # React SPA
│   └── src/
│       ├── components/   # Reusable UI (navbar, cart, admin tables, ...)
│       ├── views/        # Pages (Home, Products, Login, Admin, ...)
│       ├── store/        # Redux slices: auth, cart, favs, products, users
│       └── utils/        # Axios instance, logos
└── backend/laravel/      # Laravel API
    ├── app/Http/Controllers/
    ├── app/Models/       # User, Product, Basket, Favourite
    ├── database/migrations/
    └── routes/api.php
```

## Getting Started

### Backend

```bash
cd backend/laravel
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
php artisan serve        # http://127.0.0.1:8000
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```

The frontend expects the API at `http://127.0.0.1:8000/api` (see [frontend/src/utils/axios.js](frontend/src/utils/axios.js)).

## Frontend Routes

| Path | Page |
| --- | --- |
| `/` | Home |
| `/products` | Product listing |
| `/products/details` | Product details |
| `/favorites` | Favorites |
| `/login`, `/signup` | Authentication |
| `/admin-dashboard` | Admin dashboard (products & users) |
| `/admin-dashboard/add-product` | Add product |
| `/admin-dashboard/edit-product` | Edit product |

## API Endpoints

Endpoints marked 🔒 require a Sanctum bearer token.

| Method | Endpoint | Description |
| --- | --- | --- |
| POST | `/api/register`, `/api/login` | Authenticate |
| POST | `/api/logout` 🔒 | Log out |
| GET | `/api/products`, `/api/products/{id}` | List / show products |
| POST | `/api/products` | Create product |
| PUT | `/api/products/{id}` | Update product |
| DELETE | `/api/products/{id}` | Delete product |
| GET | `/api/user` 🔒 | Current user |
| GET | `/api/users` 🔒 | List users |
| DELETE | `/api/users/{id}` 🔒 | Delete user |
| PUT | `/api/users/{id}/type` 🔒 | Change user type |
| POST | `/api/products/favorite/{productId}` 🔒 | Toggle favorite |
| GET | `/api/users/favorites` 🔒 | List favorites |
| POST | `/api/products/{productId}/basket` 🔒 | Add to basket |
| GET | `/api/users/Basket` 🔒 | List basket items |
| DELETE | `/api/basket/{basketId}` 🔒 | Remove basket item |
| PATCH | `/api/basket/increase/{basketId}`, `/api/basket/decrease/{basketId}` 🔒 | Change quantity |

## Known Gaps

- Product create/update/delete routes are not behind `auth:sanctum` in `routes/api.php`; admin checks appear to be client-side only.
- API base URL is hard-coded in the frontend.
- No checkout or payment flow.

## Maintaining This README

Update the **Project Status** table, routes and endpoint lists whenever a commit changes features, routes or setup.

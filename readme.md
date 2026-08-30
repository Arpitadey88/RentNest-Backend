# RentNest 🏠
**Find & List Rental Properties with Ease**

RentNest is a backend API for a rental property marketplace where tenants can find rental properties, landlords can manage their listings and rental requests, and administrators can manage users, properties, categories, and rental activities.

---

## 🚀 Live API

**Backend API:** `https://rent-nest-neon-ten.vercel.app`

---

## 🛠️ Technology Stack

- **Node.js**
- **Express.js**
- **TypeScript**
- **PostgreSQL**
- **Prisma ORM**
- **JWT Authentication**
- **bcrypt**
- **Stripe**
- **REST API**
- **CORS**

---

## 👥 User Roles

### 🧑 Tenant

Tenants can:

- Register and login
- Browse rental properties
- Search and filter properties
- Submit rental requests
- View rental request history
- Cancel rental requests
- Make payments after landlord approval
- View payment history
- Leave reviews after completing a rental
- Manage their profile

### 🏠 Landlord

Landlords can:

- Register and login
- Create rental properties
- Update properties
- Delete properties
- Manage property availability
- View rental requests
- Accept or reject rental requests
- View reviews for their properties

### 👨‍💼 Admin

Admins can:

- View all users
- Ban/unban users
- Manage property categories
- View all properties
- View all rental requests
- Monitor the platform

---
## 🔐 Admin Credentials

For testing and demonstration purposes:

```json
{
  "email": "admin@admin.com",
  "password": "Password123!"
}
```

> ⚠️ **Security:** These credentials are intended for development/testing only. Change the password before using the application in production.

---

# 📌 API Endpoints

## 🔑 Authentication

| Method | Endpoint                  | Description                 |
| ------ | ------------------------- | --------------------------- |
| POST   | `/api/auth/login`         | Login user                  |
| POST   | `/api/auth/refresh-token` | Generate a new access token |

### Login Request

```json
{
  "email": "admin@admin.com",
  "password": "Password123!"
}
```

---

# 👤 Users

| Method | Endpoint                | Access        | Description                   |
| ------ | ----------------------- | ------------- | ----------------------------- |
| POST   | `/api/users/register`   | Public        | Register tenant/landlord      |
| GET    | `/api/users/me`         | Authenticated | Get current user's profile    |
| PUT    | `/api/users/my-profile` | Authenticated | Update current user's profile |

### Register User

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "Password123!",
  "role": "TENANT",
  "phone": "01712345678",
  "address": "Dhaka, Bangladesh",
  "profilePhoto": "https://example.com/profile.jpg"
}
```

---

# 🏠 Properties

Property listing endpoints are publicly accessible.

| Method | Endpoint              | Description          |
| ------ | --------------------- | -------------------- |
| GET    | `/api/properties`     | Get all properties   |
| GET    | `/api/properties/:id` | Get property details |

---

# 🏷️ Categories

| Method | Endpoint          | Access | Description        |
| ------ | ----------------- | ------ | ------------------ |
| GET    | `/api/categories` | Public | Get all categories |

### Admin Category APIs

| Method | Endpoint                    | Description     |
| ------ | --------------------------- | --------------- |
| POST   | `/api/admin/categories`     | Create category |
| PATCH  | `/api/admin/categories/:id` | Update category |
| DELETE | `/api/admin/categories/:id` | Delete category |

### Category Request

```json
{
  "name": "Apartment",
  "description": "Modern apartments available for rent."
}
```

---

# 🏡 Landlord APIs

All landlord endpoints require a valid landlord JWT.

| Method | Endpoint                               | Description                  |
| ------ | -------------------------------------- | ---------------------------- |
| POST   | `/api/landlord/properties`             | Create property              |
| PUT    | `/api/landlord/properties/:id`         | Update property              |
| DELETE | `/api/landlord/properties/:id`         | Delete property              |
| GET    | `/api/landlord/requests`               | Get rental requests          |
| PATCH  | `/api/landlord/requests/:id`           | Accept/reject rental request |
| GET    | `/api/landlord/properties/:id/reviews` | Get property reviews         |

### Rental Request Status

```text
REQUESTED
ACCEPTED
REJECTED
CANCELLED
ACTIVE
COMPLETED
```

---

# 🧑‍💻 Tenant / Rental APIs

| Method | Endpoint                  | Description                  |
| ------ | ------------------------- | ---------------------------- |
| POST   | `/api/rentals`            | Create rental request        |
| GET    | `/api/rentals`            | Get tenant's rental requests |
| GET    | `/api/rentals/:id`        | Get rental request details   |
| PATCH  | `/api/rentals/:id/cancel` | Cancel rental request        |

### Create Rental Request

```json
{
  "propertyId": "PROPERTY_ID",
  "startDate": "2026-09-01T00:00:00.000Z",
  "endDate": "2027-08-31T00:00:00.000Z",
  "message": "I am interested in renting this property for one year.",
  "monthlyRent": 25000,
  "totalAmount": 300000
}
```

---

# 💳 Payment APIs

Payments are processed using **Stripe Checkout**.

| Method | Endpoint                    | Access | Description                    |
| ------ | --------------------------- | ------ | ------------------------------ |
| POST   | `/api/payments/checkout`    | Tenant | Create Stripe checkout session |
| GET    | `/api/payments/history`     | Tenant | Get payment history            |
| GET    | `/api/payments/history/:id` | Tenant | Get payment details            |
| POST   | `/api/payments/webhook`     | Stripe | Handle Stripe webhook          |

### Payment Flow

```text
Tenant submits rental request
          ↓
Landlord accepts request
          ↓
Tenant creates checkout session
          ↓
Stripe Checkout
          ↓
Payment completed
          ↓
Stripe Webhook
          ↓
Payment status = PAID
```

---

# ⭐ Review APIs

| Method | Endpoint                               | Access   | Description              |
| ------ | -------------------------------------- | -------- | ------------------------ |
| POST   | `/api/reviews`                         | Tenant   | Create review            |
| GET    | `/api/reviews`                         | Public   | Get all reviews          |
| GET    | `/api/reviews/:id`                     | Public   | Get single review        |
| GET    | `/api/landlord/properties/:id/reviews` | Landlord | Get reviews for property |

### Create Review

```json
{
  "rentalRequestId": "RENTAL_REQUEST_ID",
  "rating": 5,
  "comment": "Excellent property and a great rental experience."
}
```

A tenant can only submit a review when:

- The rental belongs to the logged-in tenant
- The rental is completed
- Payment has been completed
- The tenant has not already reviewed the property

---

# 👨‍💼 Admin APIs

All admin endpoints require an authenticated admin account.

| Method | Endpoint                      | Description             |
| ------ | ----------------------------- | ----------------------- |
| GET    | `/api/admin/users`            | Get all users           |
| PATCH  | `/api/admin/users/:id/status` | Ban/unban user          |
| POST   | `/api/admin/categories`       | Create category         |
| PATCH  | `/api/admin/categories/:id`   | Update category         |
| DELETE | `/api/admin/categories/:id`   | Delete category         |
| GET    | `/api/admin/rentals`          | Get all rental requests |
| GET    | `/api/admin/properties`       | Get all properties      |

---

# 🔒 Authorization

Protected APIs require a JWT access token.

Add the following header in Postman:

```text
Authorization: Bearer YOUR_ACCESS_TOKEN
```

Example:

```text
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

---

# 🔄 Main Application Flow

```text
                    ┌──────────────┐
                    │    Register  │
                    └──────┬───────┘
                           ↓
                    ┌──────────────┐
                    │     Login    │
                    └──────┬───────┘
                           ↓
              ┌────────────┴────────────┐
              ↓                         ↓
          🧑 Tenant                 🏠 Landlord
              │                         │
              ↓                         ↓
      Browse Properties          Create Properties
              │                         │
              ↓                         ↓
      Submit Rental Request      Manage Requests
              │                         │
              └──────────┬──────────────┘
                         ↓
                  Landlord Accepts
                         ↓
                   Stripe Payment
                         ↓
                    Rental Active
                         ↓
                     Completed
                         ↓
                      Review
```

---

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

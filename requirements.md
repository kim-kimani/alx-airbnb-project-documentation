# 📋 Requirement Specifications – Airbnb Clone Backend

This document outlines the **technical and functional requirements** for the Airbnb Clone backend system. It covers three core features: **User Authentication**, **Property Management**, and **Booking System**, with detailed descriptions of API endpoints, input/output specifications, validation rules, and performance criteria.

## 🔐 User Authentication

Users must be able to securely register, log in, and manage their accounts using JWT-based authentication. OAuth2 support allows login via Google or Facebook. Each user has a role: Guest, Host, or Admin.

### API Endpoints

| Method | Endpoint                  | Description                   |
|--------|---------------------------|-------------------------------|
| POST   | `/api/auth/register`      | Register a new user           |
| POST   | `/api/auth/login`         | Log in with email/password    |
| POST   | `/api/auth/oauth/google`  | Log in with Google            |
| POST   | `/api/auth/logout`        | Invalidate JWT token          |

### Input Specifications

**Register:**
```json
{
  "email": "string",
  "password": "string",
  "role": "string (guest/host/admin)"
}

**Login:**
```json
{
  "email": "string",
  "password": "string"
}

### Output Specifications

**Success Response:  :**
```json
{
  "token": "JWT string",
  "user": {
    "id": "string",
    "email": "string",
    "role": "string"
  }
}

**Error Response:  :**
```json
{
  "message": "string"
}
```

### Validation Rules

- User registration:
  - Email must be unique
  - Password must be at least 8 characters long
  - Role must be one of: guest, host, admin
- Login:
  - Email must be valid
  - Password must be at least 8 characters long

### Performance Criteria

- Registration:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Login:
  - Time complexity: O(1)
  - Space complexity: O(1)

---

## 🏡 Property Management

Hosts can create, edit, and delete property listings. Each listing includes details such as title, description, location, price, and amenities. Hosts can also upload images for their listings.

### API Endpoints

| Method | Endpoint                  | Description                   |
|--------|---------------------------|-------------------------------|
| POST   | `/api/properties`         | Create a new property         |
| PUT    | `/api/properties/:id`     | Edit/update a property        |
| DELETE | `/api/properties/:id`     | Delete a property             |
| POST   | `/api/properties/:id/images` | Upload images for a property |

### Input Specifications

**Create:**
```json
{
  "title": "string",
  "description": "string",
  "location": {
    "city": "string",
    "country": "string",
    "coordinates": {
      "latitude": "float",
      "longitude": "float"
    }
  },
  "price": "float",
  "amenities": ["string"],
  "images": ["string"]
}

**Update/Edit:**
```json
{
  "title": "string",
  "description": "string",
  "location": {
    "city": "string",
    "country": "string",
    "coordinates": {
      "latitude": "float",
      "longitude": "float"
    }
  },
  "price": "float",
  "amenities": ["string"],
  "images": ["string"]
}

**Delete:**
```json
{
  "id": "string"
}

### Output Specifications

**Success Response:  :**
```json
{
  "id": "string",
  "title": "string",
  "description": "string",
  "location": {
    "city": "string",
    "country": "string",
    "coordinates": {
      "latitude": "float",
      "longitude": "float"
    }
  },
  "price": "float",
  "amenities": ["string"],
  "images": ["string"],
  "created_at": "ISO 8601 datetime",
  "updated_at": "ISO 8601 datetime"
}

**Error Response:  :**
```json
{
  "message": "string"
}
```

### Validation Rules

- Create:
  - Title must be at least 5 characters long
  - Description must be at least 10 characters long
  - Location must be valid
  - Price must be at least $10
  - Amenities must be valid
  - Images must be valid
- Update/Edit:
  - Title must be at least 5 characters long
  - Description must be at least 10 characters long
  - Location must be valid
  - Price must be at least $10
  - Amenities must be valid
  - Images must be valid
- Delete:
  - Property must exist

### Performance Criteria

- Create:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Update/Edit:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Delete:
  - Time complexity: O(1)
  - Space complexity: O(1)

---

## 🔍 Search and Filtering

Guests can search for properties by location, price, and amenities. The search results can be filtered by number of guests, available dates, and property type (e.g., listings, vacation rentals).

### API Endpoints

| Method | Endpoint                  | Description                   |
|--------|---------------------------|-------------------------------|
| GET    | `/api/properties`         | Search for properties         |
| GET    | `/api/properties/:id`     | Get a specific property       |

### Input Specifications

**Search:**
```json
{
  "location": {
    "city": "string",
    "country": "string",
    "coordinates": {
      "latitude": "float",
      "longitude": "float"
    }
  },
  "price": {
    "min": "float",
    "max": "float"
  },
  "num_guests": {
    "min": "int",
    "max": "int"
  },
  "available_dates": {
    "min": "date",
    "max": "date"
  },    
  "type": "string (listings/vacation_rentals)"
}

**Filter:**
```json
{
  "location": {
    "city": "string",
    "country": "string",
    "coordinates": {
      "latitude": "float",
      "longitude": "float"
    }
  },
  "price": {
    "min": "float",
    "max": "float"
  },
  "num_guests": {
    "min": "int",
    "max": "int"
  },
  "available_dates": {
    "min": "date",
    "max": "date"
  },    
  "type": "string (listings/vacation_rentals)"
}

### Output Specifications

**Success Response:  :**
```json
{
  "properties": [
    {
      "id": "string",
      "title": "string",
      "description": "string",
      "location": {
        "city": "string",
        "country": "string",
        "coordinates": {
          "latitude": "float",
          "longitude": "float"
        }
      },
      "price": "float",
      "amenities": ["string"],
      "images": ["string"],
      "created_at": "ISO 8601 datetime",
      "updated_at": "ISO 8601 datetime"
    }
  ]
}

**Error Response:  :**
```json
{
  "message": "string"
}
```

### Validation Rules

- Search:
  - Location must be valid
  - Price must be valid
  - Number of guests must be valid
  - Available dates must be valid
  - Type must be valid
- Filter:
  - Location must be valid
  - Price must be valid
  - Number of guests must be valid
  - Available dates must be valid
  - Type must be valid

### Performance Criteria

- Search:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Filter:
  - Time complexity: O(1)
  - Space complexity: O(1)

---

## 📅 Booking System

Guests can book a property for selected dates. The booking system prevents double bookings and ensures cancellation policies are followed.

### API Endpoints

| Method | Endpoint                  | Description                   |
|--------|---------------------------|-------------------------------|
| POST   | `/api/bookings`           | Create a new booking          |
| DELETE | `/api/bookings/:id`       | Cancel a booking              |

### Input Specifications

**Create:**
```json
{
  "property_id": "string",
  "check_in_date": "ISO 8601 datetime",
  "check_out_date": "ISO 8601 datetime"
}

**Cancel:**
```json
{
  "id": "string"
}

### Output Specifications

**Success Response:  :**
```json
{
  "id": "string",
  "property_id": "string",
  "check_in_date": "ISO 8601 datetime",
  "check_out_date": "ISO 8601 datetime",
  "created_at": "ISO 8601 datetime",
  "updated_at": "ISO 8601 datetime"
}

**Error Response:  :**
```json
{
  "message": "string"
}
```

### Validation Rules

- Create:
  - Property must exist
  - Check-in date must be valid
  - Check-out date must be valid
  - Check-in date must be before check-out date
  - Check-in date must not be in the past
  - Check-out date must not be in the past
  - Check-in date must not be greater than check-out date
- Cancel:
  - Booking must exist

### Performance Criteria

- Create:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Cancel:
  - Time complexity: O(1)
  - Space complexity: O(1)

---

## 💰 Payment Integration

Hosts can receive automatic payouts after a guest's stay. The payment system supports multiple currencies and supports payment gateways such as Stripe and PayPal.

### API Endpoints

| Method | Endpoint                  | Description                   |
|--------|---------------------------|-------------------------------|
| POST   | `/api/payments`           | Create a new payment          |

### Input Specifications

**Create:**
```json
{
  "guest_id": "string",
  "host_id": "string",
  "amount": "float",
  "currency": "string (USD/EUR/GBP)",
  "payment_method": "string (stripe/paypal)"
}

### Output Specifications

**Success Response:  :**
```json
{
  "id": "string",
  "guest_id": "string",
  "host_id": "string",
  "amount": "float",
  "currency": "string (USD/EUR/GBP)",
  "payment_method": "string (stripe/paypal)",
  "created_at": "ISO 8601 datetime",
  "updated_at": "ISO 8601 datetime"
}

**Error Response:  :**
```json
{
  "message": "string"
}
```

### Validation Rules

- Create:
  - Guest must exist
  - Host must exist
  - Amount must be at least $10
  - Currency must be valid
  - Payment method must be valid
- Cancel:
  - Payment must exist

### Performance Criteria

- Create:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Cancel:
  - Time complexity: O(1)
  - Space complexity: O(1)

---

## ⭐ Reviews and Ratings

Guests can leave reviews and ratings after stays. Hosts can respond to reviews and manage ratings.

### API Endpoints

| Method | Endpoint                  | Description                   |
|--------|---------------------------|-------------------------------|
| POST   | `/api/reviews`            | Create a new review           |
| PUT    | `/api/reviews/:id`        | Edit/update a review          |
| DELETE | `/api/reviews/:id`        | Delete a review               |
| POST   | `/api/reviews/:id/responses` | Respond to a review           |

### Input Specifications

**Create:**
```json
{
  "property_id": "string",
  "rating": "int",
  "review": "string"
}

**Update/Edit:**
```json
{
  "id": "string",
  "rating": "int",
  "review": "string"
}

**Delete:**
```json
{
  "id": "string"
}

**Respond:**
```json
{
  "id": "string",
  "response": "string"
}

### Output Specifications

**Success Response:  :**
```json
{
  "id": "string",
  "property_id": "string",
  "rating": "int",
  "review": "string",
  "created_at": "ISO 8601 datetime",
  "updated_at": "ISO 8601 datetime"
}

**Error Response:  :**
```json
{
  "message": "string"
}
```

### Validation Rules

- Create:
  - Property must exist
  - Rating must be between 1 and 5
  - Review must be at least 10 characters long
- Update/Edit:
  - Review must be at least 10 characters long
- Delete:
  - Review must exist
- Respond:
  - Review must exist

### Performance Criteria

- Create:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Update/Edit:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Delete:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Respond:
  - Time complexity: O(1)
  - Space complexity: O(1)

---

## 📨 Notifications

The notification system sends notifications to users regarding booking confirmations, payment updates, cancellation alerts, and guest reviews.

### API Endpoints

| Method | Endpoint                  | Description                   |
|--------|---------------------------|-------------------------------|
| POST   | `/api/notifications`      | Send a notification           |

### Input Specifications

**Send:**
```json
{
  "type": "string (booking_confirmation/payment_update/cancellation_alert/review)",
  "recipient_id": "string",
  "property_id": "string",
  "guest_id": "string",
  "host_id": "string",
  "amount": "float",
  "currency": "string (USD/EUR/GBP)",
  "payment_method": "string (stripe/paypal)",
  "review_id": "string",
  "response": "string"
}

### Output Specifications

**Success Response:  :**
```json
{
  "id": "string",
  "type": "string (booking_confirmation/payment_update/cancellation_alert/review)",
  "recipient_id": "string",
  "property_id": "string",
  "guest_id": "string",
  "host_id": "string",
  "amount": "float",
  "currency": "string (USD/EUR/GBP)",
  "payment_method": "string (stripe/paypal)",
  "review_id": "string",
  "response": "string",
  "created_at": "ISO 8601 datetime",
  "updated_at": "ISO 8601 datetime"
}

**Error Response:  :**
```json
{
  "message": "string"
}
```

### Validation Rules

- Send:
  - Type must be valid
  - Recipient must exist
  - Property must exist
  - Guest must exist
  - Host must exist
  - Amount must be at least $10
  - Currency must be valid
  - Payment method must be valid
  - Review must exist
  - Response must be valid

### Performance Criteria

- Send:
  - Time complexity: O(1)
  - Space complexity: O(1)

---

## 👤 Admin Dashboard

Admins can manage users, listings, reports, and moderate content.

### API Endpoints

| Method | Endpoint                  | Description                   |
|--------|---------------------------|-------------------------------|
| GET    | `/api/users`              | Get all users                 |
| GET    | `/api/users/:id`          | Get a specific user           |
| POST   | `/api/users`              | Create a new user             |
| PUT    | `/api/users/:id`          | Edit/update a user            |
| DELETE | `/api/users/:id`          | Delete a user                 |
| GET    | `/api/listings`           | Get all listings              |
| GET    | `/api/listings/:id`       | Get a specific listing         |
| POST   | `/api/listings`           | Create a new listing          |
| PUT    | `/api/listings/:id`       | Edit/update a listing         |
| DELETE | `/api/listings/:id`       | Delete a listing              |
| GET    | `/api/reports`            | Get all reports               |
| GET    | `/api/reports/:id`        | Get a specific report          |
| POST   | `/api/reports`            | Create a new report           |
| PUT    | `/api/reports/:id`        | Edit/update a report          |
| DELETE | `/api/reports/:id`        | Delete a report               |
| POST   | `/api/reports/:id/moderate`| Moderate a report             |

### Input Specifications

**Get All:**
```json
{
  "type": "string (users/listings/reports)"
}

**Get Specific:**
```json
{
  "id": "string",
  "type": "string (users/listings/reports)"
}

**Create:**
```json
{
  "type": "string (users/listings/reports)",
  "email": "string",
  "password": "string",
  "role": "string (guest/host/admin)"
}

**Update/Edit:**
```json
{
  "id": "string",
  "type": "string (users/listings/reports)",
  "email": "string",
  "password": "string",
  "role": "string (guest/host/admin)"
}

**Delete:**
```json
{
  "id": "string",
  "type": "string (users/listings/reports)"
}

**Moderate:**
```json
{
  "id": "string",
  "type": "string (reports)"
}

### Output Specifications

**Success Response:  :**
```json
{
  "id": "string",
  "type": "string (users/listings/reports)",
  "email": "string",
  "password": "string",
  "role": "string (guest/host/admin)",
  "created_at": "ISO 8601 datetime",
  "updated_at": "ISO 8601 datetime"
}

**Error Response:  :**
```json
{
  "message": "string"
}
```

### Validation Rules

- Get All:
  - Type must be valid
- Get Specific:
  - Type must be valid
- Create:
  - Type must be valid
  - Email must be valid
  - Password must be at least 8 characters long
  - Role must be valid
- Update/Edit:
  - Type must be valid
  - Email must be valid
  - Password must be at least 8 characters long
  - Role must be valid
- Delete:
  - Type must be valid
- Moderate:
  - Report must exist

### Performance Criteria

- Get All:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Get Specific:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Create:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Update/Edit:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Delete:
  - Time complexity: O(1)
  - Space complexity: O(1)
- Moderate:
  - Time complexity: O(1)
  - Space complexity: O(1)

---

## 📊 Performance Criteria

The following performance criteria are based on the assumptions of a typical web application. The actual performance may vary depending on the specific use case and database schema.
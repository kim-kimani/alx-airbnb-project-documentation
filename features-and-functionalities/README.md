# 🏠 Airbnb Clone Backend Features and Functionalities

This document outlines the key backend features and functionalities for the Airbnb Clone project. The corresponding diagram illustrating these features was created using [Draw.io](https://www.draw.io/) and exported as a PNG file located in the `features-and-functionalities/` directory.

## 📁 Directory Structure


## 🔧 Core Backend Features

### 1. 🔐 User Authentication & Management

- **User Registration**
  - Sign up with email/password
  - Select user role: Guest or Host
- **Login & JWT Authentication**
  - Secure login using JSON Web Tokens (JWT)
  - OAuth2 support (e.g., Google, Facebook)
- **Profile Management**
  - Edit personal information
  - Upload and update profile picture

### 2. 🏡 Property Management

- **Create Property Listings**
  - Title, description, location, price, availability
  - Amenities selection (Wi-Fi, pool, kitchen, etc.)
- **Edit/Delete Listings**
  - Hosts can edit or delete their own listings
- **Image Upload**
  - Store images using cloud storage (e.g., AWS S3, Cloudinary)

### 3. 🔍 Search and Filtering

- Search by:
  - Location (city, country, coordinates)
  - Price range
  - Number of guests
  - Available dates
  - Amenities
- Pagination for large result sets

### 4. 📅 Booking System

- **Create Booking**
  - Select check-in/check-out dates
  - Prevent double bookings via date validation
- **Cancel Booking**
  - Based on cancellation policy
- **Booking Status Tracking**
  - Pending, Confirmed, Completed, Canceled

### 5. 💰 Payment Integration

- Integrate payment gateways such as:
  - Stripe
  - PayPal
- Handle:
  - Guest payments
  - Automatic host payouts after stay completion
- Support multiple currencies

### 6. ⭐ Reviews and Ratings

- Guests can leave reviews and ratings after stays
- Hosts can respond to reviews
- Reviews are linked to confirmed bookings only

### 7. 📨 Notifications

- Email and in-app notifications for:
  - Booking confirmation
  - Payment updates
  - Cancellation alerts

### 8. 👤 Admin Dashboard

- Admin functions include:
  - Manage users (guests and hosts)
  - Monitor property listings
  - View booking history
  - Track payments
  - Moderate content and reports

---

## 🖼️ Backend Features Diagram

Here is the visual representation of all backend features:

![Backend Features Diagram](features-and-functionalities/backend-features-diagram.png)

> *Diagram created using [Draw.io](https://www.draw.io) and exported as PNG.*

---

## 🛠️ Technical Stack (Overview)

| Component              | Technology Used             |
|-----------------------|------------------------------|
| Backend               | Python (Flask/Django), Node.js |
| Database              | PostgreSQL / MySQL           |
| Authentication        | JWT + OAuth2                 |
| APIs                  | RESTful APIs (GraphQL optional) |
| File Storage          | AWS S3 / Cloudinary          |
| Email Service         | SendGrid / Mailgun           |
| Payments              | Stripe / PayPal              |
| Caching               | Redis                        |
| Logging               | Winston / Python logging     |

---
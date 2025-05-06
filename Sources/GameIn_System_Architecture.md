
# GameIn Platform - System Architecture

## 🧱 Overview

GameIn is a scalable web + mobile platform enabling collaboration between gamers (creators) and brands through sponsorships, social engagement, and real-time interaction.

---

## 🔹 Client Layer

### Web Client
- **Technology**: React.js / Next.js
- **Functions**: Dashboards, sponsorships, chats, profiles, admin

### Mobile Client
- **Technology**: React Native
- **Functions**: Full platform access optimized for mobile

---

## 🔹 Backend Layer

### Node.js Backend (NestJS or Express)
- Acts as the central API server
- Handles all business logic, routing, and service orchestration

### Connected Services
- **Auth Service**:
  - JWT-based login
  - 2FA (e.g. Twilio/Firebase)
  - Role-based Access Control (Admin, Creator, Brand, Community)

- **Chat Service**:
  - Real-time messaging via WebSocket

- **Payment Service**:
  - Integrated with Stripe or Razorpay
  - Fee Calculation: 5% platform fee + 15.3% tax

- **Social Integration Service**:
  - Fetches followers and activity from Instagram, Twitch

- **Admin Panel**:
  - Internal SPA for managing users, content, campaigns, and platform activity

---

## 🔹 Data Layer

### PostgreSQL
- Primary relational database for structured data
- Tables: Users, Sponsorships, Messages, Teams, Ratings, Ads

### Redis
- Stores session tokens, chat state, and frequently accessed data

### File Storage
- Cloudinary or AWS S3 for:
  - Profile images
  - Media assets
  - Chat attachments

### ElasticSearch
- Enables advanced full-text search
- Indexed with PostgreSQL data

---

## 🔄 Component Interaction

| Component        | Connects To                                      |
|------------------|--------------------------------------------------|
| Web Client       | Backend API (HTTPS)                              |
| Mobile Client    | Backend API (HTTPS)                              |
| Backend          | AuthService, ChatService, PaymentService, etc.   |
| Admin Panel      | Backend (via restricted routes)                  |
| Backend          | PostgreSQL, Redis, Cloud Storage, ElasticSearch  |

---

## ✅ Summary

This architecture ensures:
- High scalability via service decoupling
- Real-time interaction (chat, insights)
- Seamless third-party integration (social + payments)
- Optimized performance with Redis and ElasticSearch

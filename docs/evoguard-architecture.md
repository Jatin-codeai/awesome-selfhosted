# EvoGuard — Full Stack Architecture (Web + Mobile App)

## Product Overview

EvoGuard is a:

- QR Emergency Rescue System
- Wrong Parking Contact Platform
- Vehicle Identity Infrastructure
- Fleet Emergency SaaS

Users attach QR stickers to vehicles. Anyone can scan a QR code to contact the owner, call an ambulance, share location, or send a parking alert.

## Full Tech Stack

### Web Stack

#### Frontend

- Next.js 16
- React
- TypeScript
- Tailwind CSS
- shadcn/ui
- Framer Motion

#### Backend

- Next.js API Routes
- Node.js
- Prisma ORM
- JWT Authentication
- Socket.io

#### Database

- PostgreSQL
- Supabase

#### Deployment

- Vercel
- Supabase Cloud
- Cloudinary

### Mobile App Stack

#### Recommended: React Native + Expo

- React Native
- Expo
- TypeScript
- NativeWind

Why:

- Android + iPhone from a single codebase
- Fast startup development
- Scalable architecture

### Mobile Libraries

#### QR

- expo-camera
- react-native-qrcode-svg

#### Navigation

- expo-router
- react-navigation

#### State Management

- zustand

#### Notifications

- Firebase Cloud Messaging
- Expo Notifications

#### Maps

- react-native-maps
- Google Maps SDK

## Full Project Structure

### Web

```text
web/
 ├── app/
 │    ├── dashboard/
 │    ├── emergency/
 │    ├── auth/
 │    ├── fleet/
 │    ├── analytics/
 │    └── admin/
 │
 ├── api/
 │    ├── vehicles/
 │    ├── emergency-profile/
 │    ├── auth/
 │    ├── parking-alert/
 │    └── notifications/
 │
 ├── components/
 ├── lib/
 ├── prisma/
 └── public/
```

### Mobile

```text
mobile/
 ├── app/
 │    ├── login/
 │    ├── register/
 │    ├── dashboard/
 │    ├── vehicles/
 │    ├── scan/
 │    ├── emergency/
 │    ├── parking-alert/
 │    └── settings/
 │
 ├── components/
 ├── services/
 ├── hooks/
 ├── store/
 └── utils/
```

## Database Models

### User

```prisma
model User {
  id        String @id @default(cuid())
  name      String
  email     String @unique
  password  String
  vehicles  Vehicle[]
}
```

### Vehicle

```prisma
model Vehicle {
  id               String @id @default(cuid())
  userId           String
  ownerName        String?
  phoneNumber      String?
  whatsappNumber   String?
  vehicleNumber    String
  vehicleType      String
  qrCode           String
  createdAt        DateTime @default(now())
  emergencyProfile EmergencyProfile?
}
```

### EmergencyProfile

```prisma
model EmergencyProfile {
  id                String @id @default(cuid())
  vehicleId         String @unique
  bloodGroup        String
  allergies         String
  medicalConditions String
  emergencyPhone    String

  vehicle Vehicle @relation(
    fields: [vehicleId],
    references: [id]
  )
}
```

## Core Features

1. **QR Emergency Rescue**
   - Shows blood group, allergies, medical conditions, emergency contacts.
2. **Wrong Parking Alert**
   - Call owner, WhatsApp owner, share location.
3. **Live GPS Sharing**
   - Uses `navigator.geolocation`.
4. **SOS System**
   - One tap to call ambulance, notify family, and send GPS.
5. **Push Notifications**
   - Triggered by QR scans, SOS events, and parking alerts.
6. **Fleet Dashboard**
   - Manage drivers, vehicles, and alerts.

## Mobile App Screens

### Public Scan Screen

No login required. Shows emergency info, call buttons, and GPS actions.

### User App

- Login
- Dashboard
- My Vehicles
- QR Codes
- Scan History
- Notifications
- Emergency Profile
- SOS Screen

## Notification Workflow

### QR Scan Event

1. QR scanned
2. Backend logs event
3. Owner receives:
   - Push notification
   - SMS
   - WhatsApp

## Deployment Stack

- Web: Vercel
- Database: Supabase PostgreSQL
- Mobile App: Expo EAS Build, Google Play Store

## Recommended MVP

### Web MVP

- Vehicle registration
- QR generation
- Emergency page
- Medical profile
- Wrong parking alerts

### Mobile MVP

- QR scanner
- SOS button
- GPS sharing
- Push notifications

## Business Model

### B2C

- QR stickers
- Subscriptions

### Fleet SaaS

- Per-vehicle pricing

### Enterprise APIs

- Insurance companies
- Smart city systems
- Logistics companies

## Final Positioning

EvoGuard is:

- Emergency infrastructure
- Vehicle identity network
- Roadside rescue system
- Public emergency communication layer
- Fleet emergency SaaS platform

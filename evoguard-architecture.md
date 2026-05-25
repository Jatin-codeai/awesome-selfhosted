# EvoGuard — Full Stack Architecture (Web + Mobile App)

## Product overview

EvoGuard is designed as:

- QR Emergency Rescue System
- Wrong Parking Contact Platform
- Vehicle Identity Infrastructure
- Fleet Emergency SaaS

Each vehicle carries a QR sticker that lets bystanders scan and quickly:

- contact the owner,
- call ambulance services,
- share location,
- send parking alerts.

## Web stack

### Frontend

- Next.js 16
- React
- TypeScript
- Tailwind CSS
- shadcn/ui
- Framer Motion

### Backend

- Next.js API Routes
- Node.js
- Prisma ORM
- JWT authentication
- Socket.io

### Database

- PostgreSQL
- Supabase

### Deployment

- Vercel
- Supabase Cloud
- Cloudinary

## Mobile stack

### Recommended baseline

- React Native + Expo
- TypeScript
- NativeWind

Rationale:

- one codebase for Android and iOS,
- rapid MVP iteration,
- long-term scalability.

### Mobile libraries

- QR: `expo-camera`, `react-native-qrcode-svg`
- Navigation: `expo-router`, `react-navigation`
- State management: `zustand`
- Notifications: Firebase Cloud Messaging, Expo Notifications
- Maps: `react-native-maps`, Google Maps SDK

## Project structure

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
 ├── api/
 │    ├── vehicles/
 │    ├── emergency-profile/
 │    ├── auth/
 │    ├── parking-alert/
 │    └── notifications/
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
 ├── components/
 ├── services/
 ├── hooks/
 ├── store/
 └── utils/
```

## Initial Prisma models

```prisma
model User {
  id        String @id @default(cuid())
  name      String
  email     String @unique
  password  String
  vehicles  Vehicle[]
}

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

model EmergencyProfile {
  id                String @id @default(cuid())
  vehicleId         String @unique
  bloodGroup        String
  allergies         String
  medicalConditions String
  emergencyPhone    String

  vehicle Vehicle @relation(fields: [vehicleId], references: [id])
}
```

## Core features

1. QR emergency rescue details (blood group, allergies, medical conditions, emergency contacts).
2. Wrong parking alerts (call, WhatsApp, and location share options).
3. Live GPS sharing.
4. SOS one-tap emergency workflow.
5. Push notifications for scan/SOS/parking events.
6. Fleet dashboard (driver/vehicle/alert management).

## Mobile app screens

### Public scan screen (no login)

- emergency information
- call actions
- GPS actions

### User app

- Login
- Dashboard
- My Vehicles
- QR Codes
- Scan History
- Notifications
- Emergency Profile
- SOS Screen

## Notification workflow

1. QR scan event occurs.
2. Backend logs the scan.
3. Owner receives push notification, SMS, and WhatsApp alert.

## Deployment

- Web: Vercel
- Database: Supabase PostgreSQL
- Mobile: Expo EAS Build → Google Play / App Store delivery pipeline

## MVP recommendation

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

## Business model

- B2C: QR stickers + subscriptions
- Fleet SaaS: per-vehicle pricing
- Enterprise APIs: insurance, smart-city, logistics integrations

## Positioning

EvoGuard as:

- emergency infrastructure,
- vehicle identity network,
- roadside rescue system,
- public emergency communication layer,
- fleet emergency SaaS platform.

# EvoGuard — Full Stack Architecture (Web + Mobile App)

## Product overview

EvoGuard combines:

- QR emergency rescue flows.
- Wrong parking contact workflows.
- Vehicle identity and ownership access.
- Fleet emergency alert tooling.

Users attach a QR sticker on a vehicle. Scanners can:

- contact the owner,
- call emergency services,
- share GPS location,
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

- Next.js API routes
- Node.js
- Prisma ORM
- JWT authentication
- Socket.io

### Data and infrastructure

- PostgreSQL (Supabase)
- Vercel (web)
- Cloudinary (assets)

## Mobile stack

### Recommended base

- React Native + Expo
- TypeScript
- NativeWind

### Key libraries

- QR: `expo-camera`, `react-native-qrcode-svg`
- Navigation: `expo-router`, `react-navigation`
- State: `zustand`
- Notifications: Firebase Cloud Messaging + Expo Notifications
- Maps: `react-native-maps` + Google Maps SDK

## Suggested project structure

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

## Core data models (Prisma)

```prisma
model User {
  id        String   @id @default(cuid())
  name      String
  email     String   @unique
  password  String
  vehicles  Vehicle[]
}

model Vehicle {
  id               String             @id @default(cuid())
  userId           String
  ownerName        String?
  phoneNumber      String?
  whatsappNumber   String?
  vehicleNumber    String
  vehicleType      String
  qrCode           String
  createdAt        DateTime           @default(now())
  emergencyProfile EmergencyProfile?
}

model EmergencyProfile {
  id                String  @id @default(cuid())
  vehicleId         String  @unique
  bloodGroup        String
  allergies         String
  medicalConditions String
  emergencyPhone    String

  vehicle Vehicle @relation(fields: [vehicleId], references: [id])
}
```

## Core features

1. **QR Emergency Rescue**: expose medical and emergency-contact details after scan.
2. **Wrong Parking Alert**: quick call/WhatsApp/location share to owner.
3. **Live GPS Sharing**: geolocation-assisted incident context.
4. **SOS Workflow**: one-tap emergency trigger to ambulance/family with location.
5. **Push Notifications**: scan, SOS, and parking alert events.
6. **Fleet Dashboard**: driver/vehicle admin and alert tracking.

## MVP scope

### Web MVP

- Vehicle registration
- QR generation
- Emergency page
- Medical profile management
- Wrong parking alerts

### Mobile MVP

- QR scanner
- SOS button
- GPS sharing
- Push notifications

## Business model

- **B2C**: QR stickers + subscriptions.
- **Fleet SaaS**: per-vehicle pricing.
- **Enterprise APIs**: insurance, smart city, logistics.

## Positioning

EvoGuard can be positioned as emergency infrastructure plus a vehicle identity and rescue communication layer for both individuals and fleets.

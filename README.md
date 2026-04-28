# SafeTrip AI - Smart Trip Planner with Emergency Assistance

A full-stack MVP application for intelligent trip planning with integrated safety features and emergency assistance.

## Tech Stack

### Frontend
- React 18
- TypeScript
- TailwindCSS
- Wouter (routing)
- Radix UI components

### Backend
- Node.js
- Express.js
- TypeScript
- Drizzle ORM
- PostgreSQL

## Project Structure

```
SafeTrip-AI/
├── client/              # React frontend
│   └── src/
│       ├── components/  # UI components
│       ├── pages/       # Page components
│       ├── services/    # API service layer
│       └── context/     # React context
├── server/              # Express backend
│   ├── controllers/     # Route controllers
│   ├── models/          # Data models
│   ├── db.ts           # Database connection
│   ├── routes.ts       # API routes
│   └── index.ts        # Server entry
├── shared/              # Shared types/schemas
│   ├── db-schema.ts    # Database schema
│   ├── schema.ts       # Validation schemas
│   └── routes.ts       # API route definitions
└── script/              # Utility scripts
    └── seed.ts         # Database seeding
```

## Setup Instructions

### 1. Environment Variables

Create a `.env` file in the root directory:

```env
DATABASE_URL=postgresql://user:password@host:5432/safetrip
PORT=5000
GOOGLE_MAPS_API_KEY=your_google_maps_api_key_here
NODE_ENV=development
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Database Setup

Generate and push database schema:

```bash
npm run db:generate
npm run db:push
```

Seed with sample data:

```bash
npm run db:seed
```

### 4. Run Development Server

```bash
npm run dev
```

The app will run on:
- Frontend: http://localhost:5173
- Backend: http://localhost:5000

## API Endpoints

### Authentication
- `POST /api/users/register` - Register new user
- `POST /api/users/login` - User login
- `GET /api/users/:id` - Get user details

### Trips
- `POST /api/trips/create` - Create new trip
- `GET /api/trips/:userId` - Get user's trips
- `GET /api/trips/details/:tripId` - Get trip details with timeline

### Transport
- `GET /api/transport/options` - Get transport options
- `POST /api/transport/select` - Select transport

### Emergency
- `GET /api/emergency/nearby?lat=&lng=` - Get nearby help centers

## Database Schema

### Tables
- **users** - User accounts
- **trips** - Trip information
- **trip_places** - Places in trip itinerary
- **transport_options** - Transport options for each place
- **safety_info** - Safety information (hospitals, police)
- **emergency_contacts** - User emergency contacts

## Features

✅ User registration and authentication
✅ Trip creation and management
✅ Interactive trip workspace
✅ Transport options for each destination
✅ Safety information integration
✅ SOS emergency button
✅ Nearby hospitals and police stations
✅ Real-time trip timeline
✅ Database persistence

## Sample Credentials

After seeding:
- Email: demo@safetrip.com
- Password: demo123

## Development

### Type Checking
```bash
npm run check
```

### Build for Production
```bash
npm run build
npm start
```

## Next Steps

- [ ] Integrate real Google Maps API
- [ ] Add Google Places API for emergency centers
- [ ] Implement JWT authentication
- [ ] Add real-time location tracking
- [ ] Integrate actual transport APIs (Uber, Rapido)
- [ ] Add payment integration
- [ ] Deploy to production

## License

MIT
"# safetrip" 

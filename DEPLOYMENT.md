# SafeTrip AI - Complete Setup & Deployment Guide

## Quick Start (5 Minutes)

### Step 1: Database Setup

**Option A: Supabase (Recommended)**
1. Go to https://supabase.com
2. Create new project
3. Copy the connection string from Settings > Database
4. Format: `postgresql://postgres:[password]@[host]:5432/postgres`

**Option B: Neon**
1. Go to https://neon.tech
2. Create new project
3. Copy connection string

### Step 2: Configure Environment

Create `.env` file:
```env
DATABASE_URL=your_database_connection_string
PORT=5000
NODE_ENV=development
```

### Step 3: Initialize Database

```bash
# Generate migrations
npm run db:generate

# Push schema to database
npm run db:push

# Seed with sample data
npm run db:seed
```

### Step 4: Start Development

```bash
npm run dev
```

Visit http://localhost:5173

## Database Schema Overview

### Users Table
- Stores user accounts
- Fields: id, name, email, password

### Trips Table
- Stores trip information
- Links to user via userId
- Tracks status, dates, location

### Trip Places Table
- Individual destinations in trip
- Ordered itinerary items
- Links to trip via tripId

### Transport Options Table
- Available transport for each place
- Price, time, type information
- Recommended flag

### Safety Info Table
- Nearby hospitals and police
- Linked to each place

## API Integration Guide

### Frontend API Calls

Import the API service:
```typescript
import { api } from "@/services/api";
```

Example usage:
```typescript
// Login
const user = await api.login(email, password);

// Create trip
const trip = await api.createTrip({
  userId: 1,
  destination: "Chennai",
  startDate: "2024-02-01",
  endDate: "2024-02-03",
  budget: "moderate",
  places: [...]
});

// Get trip details
const tripData = await api.getTripDetails(tripId);
```

## Adding Google Maps

### Step 1: Get API Key
1. Go to Google Cloud Console
2. Enable Maps JavaScript API
3. Enable Places API
4. Create API key

### Step 2: Install Package
```bash
npm install @react-google-maps/api
```

### Step 3: Add to Environment
```env
VITE_GOOGLE_MAPS_API_KEY=your_api_key
```

### Step 4: Use in Component
```typescript
import { GoogleMap, LoadScript, Marker } from '@react-google-maps/api';

<LoadScript googleMapsApiKey={import.meta.env.VITE_GOOGLE_MAPS_API_KEY}>
  <GoogleMap center={{ lat: 13.0827, lng: 80.2707 }} zoom={12}>
    <Marker position={{ lat: 13.0827, lng: 80.2707 }} />
  </GoogleMap>
</LoadScript>
```

## Production Deployment

### Backend Deployment (Railway/Render)

1. Push code to GitHub
2. Connect to Railway/Render
3. Set environment variables
4. Deploy

### Frontend Deployment (Vercel/Netlify)

1. Build command: `npm run build`
2. Output directory: `dist`
3. Set environment variables
4. Deploy

### Environment Variables for Production

```env
DATABASE_URL=production_database_url
NODE_ENV=production
VITE_API_URL=https://your-backend-url.com
GOOGLE_MAPS_API_KEY=your_key
```

## Testing the MVP

### Test User Registration
```bash
curl -X POST http://localhost:5000/api/users/register \
  -H "Content-Type: application/json" \
  -d '{"name":"Test User","email":"test@test.com","password":"test123"}'
```

### Test Trip Creation
```bash
curl -X POST http://localhost:5000/api/trips/create \
  -H "Content-Type: application/json" \
  -d '{
    "userId": 1,
    "destination": "Mumbai",
    "startDate": "2024-03-01",
    "endDate": "2024-03-05",
    "budget": "moderate"
  }'
```

### Test Emergency API
```bash
curl "http://localhost:5000/api/emergency/nearby?lat=13.0827&lng=80.2707"
```

## Common Issues & Solutions

### Database Connection Failed
- Check DATABASE_URL format
- Ensure database is accessible
- Verify credentials

### Port Already in Use
- Change PORT in .env
- Kill process using port 5000

### CORS Errors
- Backend already has CORS enabled
- Check API_BASE URL in frontend

## Next Features to Add

1. **Real-time Updates**: WebSocket for live trip updates
2. **Payment Integration**: Stripe/Razorpay for bookings
3. **AI Trip Generation**: OpenAI API for smart itineraries
4. **Photo Upload**: Cloudinary for trip photos
5. **Social Features**: Share trips with friends
6. **Notifications**: Email/SMS alerts for trip updates

## Performance Optimization

- Add Redis for caching
- Implement pagination for trips list
- Optimize database queries with indexes
- Add CDN for static assets
- Implement lazy loading for images

## Security Enhancements

- Hash passwords with bcrypt
- Implement JWT tokens
- Add rate limiting
- Validate all inputs
- Sanitize user data
- Add HTTPS in production

## Monitoring & Analytics

- Add Sentry for error tracking
- Implement Google Analytics
- Add logging with Winston
- Monitor database performance
- Track API response times

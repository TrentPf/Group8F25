# Group8F25 — DriveTracker

**Project:** DriveTracker is a React Native / Expo app that records driving trips, computes driving scores, and provides historical trip visualizations. This repository contains the mobile app code, a small demo database connector using Supabase, and utility scripts for testing connectivity.

**Key Features**

- **Trip Recording:** Records start/end times and GPS traces via the device and stores them as `trips`.
- **Scoring:** Computes driving scores and shows an overall score badge for each trip.
- **History View:** Browse past trips with summaries and map previews.
- **Supabase Integration:** Stores users, trips, and driving scores in Supabase; includes a diagnostic script to verify connectivity.

**How It Works**

- **Frontend:** Built with React Native + Expo. Screens live in `drivetracker/app` and `drivetracker/views`.
- **Data Layer:** Uses `@supabase/supabase-js` to read/write `users`, `trips`, and `driving_scores` in Supabase. The model/DB helper code is in `drivetracker/models` and `drivetracker/database`.
- **Scripts / Tools:** Quick diagnostic script at `drivetracker/scripts/check_supabase.js` checks environment variables and queries the demo user.

**Data & Analytics Overview**

**DriveTracker** implements an end-to-end data pipeline:
- Captures GPS telemetry from mobile devices
- Persists structured trip and driving score data in Supabase (SQL)
- Computes KPI-style performance scores from raw sensor data
- Enables historical trend analysis via trip summaries and visualizations

**Repository Layout**

- **`drivetracker/app`**: Router and top-level screens (`index.jsx`, `history.jsx`, `track.jsx`).
- **`drivetracker/components`**: Reusable UI (e.g., `TripCard.jsx`, `OverallScoreBadge.jsx`).
- **`drivetracker/controllers`**: Screen controllers that handle logic and coordinate services.
- **`drivetracker/services`**: Scoring, storage, and threshold logic.
- **`drivetracker/database`**: Supabase client helpers, demo seed SQL.
- **`drivetracker/scripts`**: Tools such as `check_supabase.js`.

**Screenshots**

Home

![Home Screenshot](drivetracker/assets/HomeScreenshot.jpg)

History

![History Screenshot](drivetracker/assets/HistoryScreenshot.jpg)

Track / Trip View

![Track Screenshot](drivetracker/assets/TrackScreenShot.jpg)

**Developer Setup**

- **Prerequisites:**

  - Node.js (16+ recommended)
  - `npm` or `yarn`
  - Expo CLI (optional global): `npm install -g expo-cli` or use `npx expo` commands

- **Install dependencies:**

```bash
cd drivetracker
npm install
```

- **Environment variables:** Create a `.env` file in `drivetracker/` (not checked into git). Required variables:

```
SUPABASE_URL=<your-supabase-url>
SUPABASE_ANON_KEY=<your-supabase-anon-key>
DEMO_USER_EMAIL=demo@example.com   # optional
```

The project `package.json` declares `"type": "module"`, so node scripts use ESM imports.

**Running the App (Development)**

- Start the Expo dev server:

```bash
cd drivetracker
npx expo start
```

- Run on Android emulator:

```bash
npx expo run:android
```

- Run on iOS simulator (macOS):

```bash
npx expo run:ios
```

**Useful Scripts**

- **Check Supabase connectivity:**

```bash
cd drivetracker
node scripts/check_supabase.js
```

This script reads `.env` and queries the `users` and `trips` tables for the demo user. If you get an ESM-related error, ensure Node is recent and `drivetracker/package.json` contains `"type": "module"` (it does).

- **Unit tests (if present):**

```bash
cd drivetracker
npm run test:unit
```

**Contribution & Notes**

- Keep secrets out of git: add `drivetracker/.env` to `.gitignore` if you add any credentials locally.
- If you change the Supabase schema, update `drivetracker/models/supabaseModel.js` and `drivetracker/database/demo_seed.sql` accordingly.
- For UI changes, follow existing component conventions in `drivetracker/components`.



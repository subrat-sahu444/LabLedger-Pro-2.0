# 🧪 LabLedger Pro 2.0

**An offline-first mobile laboratory notebook.** Capture experiments, record numerical readings, visualize trends, export PDF reports, and optionally back up your notebook to a private Supabase account.

![Expo](https://img.shields.io/badge/Expo-SDK%2054-4630EB)
![TypeScript](https://img.shields.io/badge/TypeScript-strict-3178C6)
![Platform](https://img.shields.io/badge/platform-Android%20%7C%20iOS-55D6BE)
![License](https://img.shields.io/badge/license-MIT-green)

## Features

- Create, browse, and organize experiments by subject
- Search experiment titles, subjects, objectives, methods, observations, and results
- Add numerical measurements with labels and units
- Visualize measurement trends in a line chart
- Generate and share PDF experiment reports
- Mark experiments as draft or completed
- Offline-first SQLite database
- Optional authenticated cloud backup with Supabase Row Level Security
- Automated validation tests

## Download the complete source

The complete Expo/React Native TypeScript project is included in **[labledger-pro-2.0.zip](./labledger-pro-2.0.zip)**. Download the ZIP and extract it to get the app source, SQL schema, tests, and configuration files.

## Tech stack

React Native, Expo SDK 54, Expo Router, TypeScript, Expo SQLite, React Native SVG, Expo Print, Expo Sharing, Supabase JS, Vitest.

## Windows setup

### Requirements

- Windows 10/11
- Node.js LTS: https://nodejs.org/
- Git: https://git-scm.com/
- Android phone with Expo Go, or Android Studio emulator

### Install dependencies

Extract the ZIP, open PowerShell in the extracted `labledger-pro` folder, and run:

```powershell
npm.cmd install
npx.cmd expo install --fix
```

### Run on your phone

Install Expo Go from the Play Store. Connect your phone and PC to the same Wi-Fi, then run:

```powershell
npx.cmd expo start
```

Scan the QR code with Expo Go. If LAN discovery fails, try:

```powershell
npx.cmd expo start --tunnel
```

### Run checks

```powershell
npm.cmd run typecheck
npm.cmd test
```

## Optional cloud backup setup

Cloud backup is disabled until you configure Supabase.

1. Create a project at https://supabase.com/.
2. In Supabase Dashboard, open SQL Editor.
3. Run the SQL in `supabase/schema.sql`.
4. Open Project Settings → API and copy the Project URL and anon/public key.
5. Copy `.env.example` to `.env`.
6. Set the values:

```env
EXPO_PUBLIC_SUPABASE_URL=https://YOUR_PROJECT.supabase.co
EXPO_PUBLIC_SUPABASE_ANON_KEY=YOUR_SUPABASE_ANON_PUBLIC_KEY
```

7. Restart Expo:

```powershell
npx.cmd expo start -c
```

8. In the app, open Backup, create an account or sign in, then choose **Back up this device**.

### Security and current limitations

- The app uses Supabase Auth and Row Level Security. Each backup row is scoped to `auth.uid()`.
- Only the anon/public key belongs in a client app. Never use the Supabase `service_role` key in a mobile app or commit secrets to Git.
- Enable email confirmation and configure Supabase Auth settings for your deployment.
- Cloud backup currently snapshots experiment records only; measurement rows are not synced.
- End-to-end encryption and conflict-aware merging are not implemented. Treat Supabase as a trusted processor and do not store sensitive research until these protections are added.
- Restoring replaces the local experiment list. Export important records before restoring.

## Project structure

```text
labledger-pro/
├── app/
│   ├── _layout.tsx
│   ├── index.tsx
│   ├── new-entry.tsx
│   ├── backup.tsx
│   └── entry/[id].tsx
├── src/
│   ├── components/MeasurementChart.tsx
│   ├── db/database.ts
│   ├── db/entries.ts
│   ├── services/cloud.ts
│   ├── services/pdf.ts
│   └── ui.tsx
├── supabase/schema.sql
├── tests/entries.test.ts
├── vitest.config.ts
├── .env.example
└── README.md
```

## Roadmap

- [ ] Include measurement data in cloud snapshots
- [ ] End-to-end encrypted backup
- [ ] Conflict-aware incremental sync
- [ ] Photo attachments and CSV export
- [ ] More chart types and units
- [ ] UI and integration test coverage
- [ ] GitHub Actions CI and release builds

## Disclaimer

LabLedger is a record-keeping tool, not a laboratory safety guide or substitute for approved protocols and instructor supervision.

## License

MIT.

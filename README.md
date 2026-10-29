# Galaxy AI

Galaxy AI is a JavaScript learning companion built with React, Vite, Tailwind, Supabase, Groq, Electron, and Capacitor. It can be packaged as a Windows installer/portable executable and an Android APK from the same source.

## Configure Supabase

1. Copy `.env.example` to `.env` in this project folder.
2. Set `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` to your Supabase project URL and public anon key. Never use a `service_role` key in the app.
3. Run the SQL in [`sql/schema.sql`](sql/schema.sql) in the Supabase SQL Editor. Email/password authentication must be enabled.
4. Restart Vite or rebuild after changing `.env`; Vite embeds these public values at build time.

The Supabase anon key is public by design. Row Level Security policies in the schema limit each user to their own rows.

## Install and develop

```powershell
npm install
npm run dev            # browser preview at http://localhost:5173
npm run electron:dev   # Windows desktop development
```

In browser development, API secrets use localStorage and are **not encrypted**. Electron uses OS safeStorage; Android uses the secure-storage plugin. Configure a Groq key under Settings before using chat or roadmaps. The YouTube key is optional.

## Build

```powershell
npm run build
npm run electron:build # release\Galaxy AI Setup.exe and portable executable
npm run android:debug  # android\app\build\outputs\apk\debug\app-debug.apk
npm run android:release
npm run icons
```

For Android, install Android Studio/Android SDK and configure `android/local.properties` with `sdk.dir`. The recommended build JDK is 17. Release APKs must be signed with your own keystore; never commit keystore files or passwords.

## Features

- Supabase email/password sign-in, sign-up, password recovery, session persistence, user-scoped RLS data.
- AI chat with Groq streaming, stop/regenerate/copy, history, model picker, favourites/custom models, compare replies, web-search routing, six study modes, Markdown and code highlighting.
- Two-stage study roadmap research and structured generation, YouTube link verification, progress tracking, saved roadmaps, and Tutor-mode step handoff.
- Encrypted device secret storage for Groq and optional YouTube keys, responsive white/obsidian interface, locally bundled Inter font, knight icon.

## Verification

Run `npm test` for unit coverage of JSON parsing, YouTube ID extraction, SSE parsing, model filtering, and history trimming.

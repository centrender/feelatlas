
# FeelAtlas – Track A MVP Plan

**Goal:** Implement Track A MVP for FeelAtlas (Emotion Atlas AI) with three screens.

**Stack:** Expo React Native (TypeScript) · Supabase (Postgres + Edge Functions) · Expo Maps (Track A) · Zustand.

---

## Tasks

1. **Supabase Integration**
   - Create Supabase client, anon auth, and API wrapper in `src/lib/api.ts`.
   - Use `.env` for `EXPO_PUBLIC_SUPABASE_URL` and `EXPO_PUBLIC_SUPABASE_ANON_KEY`.

2. **CheckinScreen**
   - 6 emotion buttons (joy, calm, sad, angry, love, awe)
   - Note input and submit to `/ingest_checkin`
   - Location permission and optional 300 m fuzzing

3. **MapScreen**
   - Use Expo Maps with a heat layer visualizing `/get_tiles` data for last 24 h
   - Include a time slider to filter by hour

4. **JournalScreen**
   - Call `/me` endpoint
   - List recent 30 check-ins
   - Tap on any item → navigate to `MapScreen` with that pin selected

5. **Zustand Store**
   - Keep userId, settings, tiles, and journal
   - Persist locally using `zustand/persist`

6. **Error / Empty / Loading States**
   - Every screen must handle network failure, no-data, and loading transitions gracefully.

7. **Environment Configuration**
   - `.env` variables wired via `app.config.ts`
   - Example:
     ```
     EXPO_PUBLIC_SUPABASE_URL=...
     EXPO_PUBLIC_SUPABASE_ANON_KEY=...
     EXPO_PUBLIC_CITY=los_angeles
     ```

---

## Development Commands

```bash
# App setup
npx create-expo-app feelatlas --template blank-typescript
npm i @supabase/supabase-js zustand
npx expo install expo-maps

# Supabase
supabase init
supabase functions new ingest_checkin
supabase functions new get_tiles
supabase functions new me

# Local run
npx expo start
supabase start

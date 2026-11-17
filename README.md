# Cargo Express Shipping Company

A responsive React/Vite logistics website starter with a separate `/admin` administrator portal, shared Supabase backend, customer chat, image/video uploads, shipment lookup and a live ADS-B aircraft map.

## 1. Configure the persistent backend
1. Create a Supabase project.
2. Open **SQL Editor** and run `supabase/schema.sql`.
3. In Supabase > Project Settings > API, copy the Project URL and anon/public key.
4. Copy `.env.example` to `.env` and fill in `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`.
5. Create your first admin account using Supabase Authentication. Insert that user's UUID into `public.profiles` as role `admin` using the SQL at the bottom of `schema.sql`.
6. For customers, create Auth users through a controlled sign-up/invitation flow. Do not expose a service-role key in the browser.

## 2. Run locally
```bash
npm install
npm run dev
```

## 3. Deploy
Push this folder to a private GitHub repository and import it into Vercel. The included `vercel.json` rewrites `/admin` to the app so the separate admin portal works after deployment. Set the same two `VITE_SUPABASE_*` environment variables in the hosting dashboard, then deploy. Supabase remains the database/auth/storage/realtime service independently of the frontend host, so records and chat media persist across redeploys.

## 4. Features and limitations
- Chat uses Supabase Auth, Postgres Realtime and Supabase Storage. Both sides can send images/videos (30 MB max, configured MIME types). Admins sign in separately at `/admin`, can view customer message threads and select a customer in the support inbox. Customers can only read their own messages. Admin replies are stored against the selected customer's user ID and marked as admin messages. Both interfaces use the same Supabase project.
- Shipment tracking is backed by the `shipments` table. Admins can create shipment records from the admin panel.
- Aircraft positions are fetched from the public ADS-B feed at adsb.lol and refreshed every 15 seconds for the selected area. Coverage and aircraft visibility vary; ADS-B positions are not guaranteed exact or complete and do not prove cargo is aboard a plane.
- This is source code, not a deployed live service. It becomes persistent only after you create/configure Supabase and deploy the frontend. Use a company domain, privacy policy, terms, verified contact details and a tested admin account before accepting customers.

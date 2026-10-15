# Max’s Auto Shop — Website starter

Responsive frontend for general auto repair, performance work, and classic restoration. Includes a repair estimator, appointment form, Supabase customer auth/history, admin appointment status management, basic parts inventory, and database foundations for repair orders, invoices, service history, and gallery content.

## Local preview
Requires Node.js 20+.
```bash
npm install
npm run dev
```
Open the local URL Vite prints. A static preview can also be opened from `public/index.html`, but real database features require Supabase configuration.

## Connect the backend
1. Create a project at https://supabase.com/
2. Open Supabase SQL Editor and run `supabase/schema.sql`.
3. In Project Settings → API, copy the project URL and anon/publishable key.
4. Put those values into `public/config.js`. The anon key is intended for browser use with the row-level security policies; never expose the service-role key.
5. In Supabase Authentication, set the Site URL and allowed redirect URLs to your eventual website domain.
6. Register the shop owner's account through the customer portal. Then run this SQL, replacing the email:
```sql
update public.user_roles set role='admin'
where user_id=(select id from auth.users where email='YOUR_OWNER_EMAIL@example.com');
```
7. Sign out and sign in again. The admin dashboard should then load appointments and inventory.

## Publish online
Beginner-friendly hosting: Netlify or Vercel.
- Push the project to a Git repository and import it into Netlify/Vercel.
- Build command: `npm run build`
- Output directory: `dist`
- Add your custom domain and HTTPS.
- Update Supabase Auth Site URL/redirect URLs to the live domain.

## Feature status
Working after backend configuration: appointment inserts, customer sign-in/sign-up, own appointment history, admin appointment status updates, inventory add/delete, and database tables with access policies.
The current UI does not yet include full repair-order creation/editing, invoice PDF generation, inventory movement/parts consumption, restoration gallery admin uploads, or complete service-record editing. Those need additional frontend screens.
Online payment is not activated. To accept payments safely, deploy a server-side Supabase Edge Function that validates invoice ownership and amount, creates a Stripe Checkout Session, and a signed Stripe webhook that marks invoices paid after verified events. Never put Stripe secret keys in browser code. See https://stripe.com/payments/checkout.
For shop notifications, configure an Edge Function plus a transactional email provider; database inserts alone do not email the shop.

## Before launch
Replace placeholder details and visual tiles, add real contact details, verified reviews, privacy policy and repair authorization terms, configure email notifications, add spam protection, test row-level security with separate anonymous/customer/admin accounts, configure backups, and review local tax/privacy/payment obligations. The included SQL is a starter schema and should be security-reviewed before storing real customer data.

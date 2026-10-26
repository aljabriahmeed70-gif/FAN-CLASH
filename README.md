# FAN CLASH — website starter

Arabic/English football fan voting site, black/purple theme, $1 USD per vote, live aggregate leaderboard, and server-side payment verification.

## Payment rule
- Server creates a checkout at a fixed price of 100 USD cents.
- The backend verifies the payment provider webhook signature.
- The vote is recorded only when the provider says `payment_status=paid`, amount is exactly 100 cents, and currency is USD.
- Unique checkout-session and payment-intent IDs prevent duplicate counting.
- Cancelled or failed payments never count. A browser redirect to the success page does not itself create a vote.

## Before launch
This is deployable starter code, not a live payment account. Verify that your payment provider accepts merchants in Yemen, your paid-voting business model, your bank/payout details, and your target customers. Stripe may not onboard a Yemen-based merchant; confirm eligibility with the provider. Do not use a false address or someone else's account to bypass restrictions. The sample player images are placeholders and are not guaranteed to depict the named players; replace them with licensed images.

## Setup
1. Install Node.js 20+ and create a Supabase project.
2. Run `supabase/schema.sql` in Supabase SQL Editor.
3. Copy `.env.example` to `.env`; fill in Supabase credentials and payment provider keys. Keep `SUPABASE_SERVICE_ROLE_KEY` server-only; never use it in frontend variables.
4. Configure webhook endpoint `https://YOUR-DOMAIN/api/stripe-webhook` for `checkout.session.completed` and `checkout.session.async_payment_succeeded`, then set `STRIPE_WEBHOOK_SECRET`.
5. Set `PUBLIC_BASE_URL` and `VITE_API_BASE_URL` to the deployed origin.
6. Run `npm install`, `npm run build`, `npm start`.
7. Test with provider test mode and verify webhook delivery before live launch.

## Local development
`npm run dev` serves the Vite frontend; run `npm start` separately for API on port 4242. Configure `VITE_API_BASE_URL=http://localhost:4242`.

## Important limitations
No user accounts, anti-bot/rate limiting, refund/chargeback vote reversal, privacy/terms pages, or full production monitoring are included. Check legal requirements and provider rules for paid voting before opening globally. Images and results are demo placeholders until connected to the database/payment setup.

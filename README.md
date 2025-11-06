# AI Launch Plan - Landing Page

Complete landing page with Stripe Checkout integration and n8n webhook automation.

## Features

- ✅ Modern, responsive design
- ✅ Stripe Checkout payment integration ($280)
- ✅ Custom intake form submission to n8n
- ✅ PDF preview with navigation
- ✅ Serverless backend (Vercel Functions)
- ✅ No external dependencies or branding

## User Flow

1. User lands on landing page
2. Clicks "Generate my launch plan" CTA
3. Redirects to Stripe Checkout (pays $280)
4. Returns to success page with intake form
5. User fills form and submits
6. Form data sends to n8n webhook
7. n8n workflow generates AI report and emails customer

## Tech Stack

- **Frontend**: HTML, CSS, JavaScript
- **Payment**: Stripe Checkout
- **Backend**: Vercel Serverless Functions
- **Automation**: n8n webhook
- **Hosting**: Vercel (free tier)

## Deployment to Vercel

### Prerequisites

1. Vercel account (sign up at https://vercel.com)
2. Stripe account with test mode enabled
3. n8n instance with webhook endpoint

### Step 1: Push to GitHub

```bash
git add .
git commit -m "Complete Stripe integration and n8n webhook"
git push origin main
```

### Step 2: Deploy to Vercel

**Option A: Vercel CLI (Recommended)**

1. Install Vercel CLI:
```bash
npm install -g vercel
```

2. Login to Vercel:
```bash
vercel login
```

3. Deploy:
```bash
cd /path/to/ai-launch-plan-landingpage
vercel
```

4. Follow prompts:
   - Set up and deploy? **Y**
   - Which scope? Select your account
   - Link to existing project? **N**
   - Project name? **ai-launch-plan-landingpage**
   - Directory? **./**
   - Override settings? **N**

**Option B: Vercel Dashboard (Easy)**

1. Go to https://vercel.com/new
2. Click "Import Git Repository"
3. Select your GitHub repo: `brett4bouchard/ai-launch-plan-landingpage`
4. Click "Import"
5. Vercel will auto-detect settings
6. Click "Deploy"

### Step 3: Add Environment Variables

After deployment, add these environment variables in Vercel:

1. Go to your project in Vercel Dashboard
2. Click "Settings" → "Environment Variables"
3. Add these variables (use your actual keys from Stripe Dashboard):

```
STRIPE_SECRET_KEY=sk_test_YOUR_SECRET_KEY_HERE
STRIPE_PRICE_ID=price_YOUR_PRICE_ID_HERE
```

4. Click "Save"
5. Redeploy (Vercel → Deployments → Click "..." → Redeploy)

**Note:** Find your actual keys at https://dashboard.stripe.com/test/apikeys

### Step 4: Test the Flow

1. Visit your Vercel URL (e.g., `https://ai-launch-plan-landingpage.vercel.app`)
2. Click "Generate my launch plan"
3. Use Stripe test card: `4242 4242 4242 4242`
   - Expiry: Any future date
   - CVC: Any 3 digits
   - ZIP: Any 5 digits
4. Complete payment
5. Fill out intake form
6. Verify data reaches n8n webhook
7. Check that n8n workflow triggers

## Going Live (Production)

When ready to accept real payments:

### Step 1: Create Live Stripe Product

1. Go to https://dashboard.stripe.com/products (no "test" in URL)
2. Create product: "AI Launch Plan Report"
3. Set price: $280 USD
4. Copy the **Live Price ID** (starts with `price_`)

### Step 2: Get Live Stripe Keys

1. Go to https://dashboard.stripe.com/apikeys
2. Copy your **Live Secret Key** (starts with `sk_live_`)

### Step 3: Update Vercel Environment Variables

1. Go to Vercel Dashboard → Your Project → Settings → Environment Variables
2. Update both variables with LIVE keys:
   - `STRIPE_SECRET_KEY`: Your live secret key
   - `STRIPE_PRICE_ID`: Your live price ID
3. Save and redeploy

### Step 4: Update n8n Webhook (if needed)

If using a different n8n webhook URL for production, update it in:
- `success.html` line 184

## Custom Domain (Optional)

1. Go to Vercel Dashboard → Your Project → Settings → Domains
2. Add your custom domain (e.g., `ailaunchplan.com`)
3. Follow Vercel's DNS instructions
4. SSL certificate is automatically provisioned

## File Structure

```
ai-launch-plan-landingpage/
├── index.html                          # Landing page
├── success.html                        # Post-payment form page
├── api/
│   └── create-checkout-session.js     # Stripe Checkout API
├── package.json                        # Dependencies
├── vercel.json                         # Vercel configuration
├── .env.example                        # Environment variables template
├── README.md                           # This file
├── ailaunchplan-logo.png              # Logo
├── AI_Launch_Plan_-_visual_for_landing_page.png  # Workflow diagram
├── Arrows-Go-to-Market-Plan-PDFpreview.pdf       # Sample PDF
└── ailaunchplan-terms-of-service.md   # Terms of service

```

## Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `STRIPE_SECRET_KEY` | Stripe secret key (test or live) | `sk_test_...` or `sk_live_...` |
| `STRIPE_PRICE_ID` | Stripe price ID for $280 product | `price_...` |

## Testing

### Test Cards (Stripe Test Mode)

| Card Number | Result |
|-------------|--------|
| 4242 4242 4242 4242 | Success |
| 4000 0000 0000 0002 | Decline |
| 4000 0025 0000 3155 | Requires authentication |

### n8n Webhook Test

Manually test the webhook:
```bash
curl -X POST https://brettbouchard.app.n8n.cloud/webhook/ai-launch-plan-intake \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Test User",
    "email": "test@example.com",
    "company_name": "Test Co",
    "company_type": "B2B",
    "product_name": "Test Product",
    "product_description": "Test description",
    "launch_goal": "Test goal",
    "target_audience": "Test audience",
    "submittedAt": "2025-01-01T00:00:00.000Z",
    "formMode": "test",
    "stripeSessionId": "cs_test_123"
  }'
```

## Troubleshooting

### Payment not redirecting

1. Check browser console for errors
2. Verify Vercel environment variables are set
3. Check Vercel function logs: Dashboard → Functions → View Logs

### Form not submitting to n8n

1. Check n8n webhook is active
2. Verify webhook URL in `success.html` line 184
3. Check n8n workflow execution logs

### Vercel deployment failed

1. Check `package.json` is valid JSON
2. Verify all files are committed to git
3. Check Vercel deployment logs for specific errors

## Support

For issues:
- Check Vercel function logs
- Verify Stripe Dashboard for payment records
- Check n8n workflow execution history

Built by Brett Bouchard | BBvisory LLC

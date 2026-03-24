# Lead Scoring Tool

Intelligent multi-channel lead scoring and routing system that consolidates leads from HubSpot, ads platforms, and phone systems into a unified scoring engine.

## What this does

This project centralizes lead generation from multiple channels (HubSpot CRM, Facebook Ads, Google Ads, Glowcom phone system, website forms, and email/SMS campaigns) into a unified scoring system. It validates contact information, enriches lead profiles with business data, and automatically routes qualified leads to sales teams based on configurable scoring criteria.

**Built for:** Sales and marketing departments managing high-volume lead generation
**Users:** Sales managers, analysts, and sales representatives

## Tech Stack

- **Framework:** Next.js 15 with App Router
- **Database:** Supabase (PostgreSQL with real-time subscriptions)
- **Language:** TypeScript
- **Styling:** Tailwind CSS
- **Authentication:** Supabase Auth with role-based access control
- **Deployment:** Vercel
- **Integrations:** Slack, ChatGPT, Replicate, Gmail, HubSpot, Facebook Ads, Google Ads, Glowcom

## Prerequisites

- Node.js 18+
- npm or yarn
- Supabase account
- Vercel account (for deployment)
- Integration API keys (HubSpot, Facebook, Google, etc.)

## Local Development Setup

1. **Clone and install dependencies:**
   bash
   git clone <repo-url>
   cd lead-scoring-tool
   npm install
   

2. **Environment setup:**
   bash
   cp .env.example .env.local
   # Edit .env.local with your values
   

3. **Start Supabase:**
   bash
   npx supabase start
   

4. **Run database migrations:**
   bash
   npx supabase db push
   

5. **Start development server:**
   bash
   npm run dev
   

6. **Visit:** http://localhost:3000

## Environment Variables

| Variable | Description | Required |
|----------|-------------|---------|
| `NEXT_PUBLIC_SUPABASE_URL` | Supabase project URL | Yes |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase anonymous key | Yes |
| `SUPABASE_SERVICE_ROLE_KEY` | Supabase service role key (server-only) | Yes |
| `HUBSPOT_ACCESS_TOKEN` | HubSpot API access token | Yes |
| `FACEBOOK_ACCESS_TOKEN` | Facebook Ads API token | Yes |
| `GOOGLE_ADS_DEVELOPER_TOKEN` | Google Ads API developer token | Yes |
| `GOOGLE_ADS_CLIENT_ID` | Google Ads OAuth client ID | Yes |
| `GLOWCOM_API_KEY` | Glowcom phone system API key | Yes |
| `CHATGPT_API_KEY` | OpenAI API key for ChatGPT integration | Yes |
| `REPLICATE_API_TOKEN` | Replicate API token | Yes |
| `SENDGRID_API_KEY` | SendGrid API key for email validation | Yes |
| `SLACK_BOT_TOKEN` | Slack bot token for notifications | Yes |
| `EMAIL_VALIDATION_API_KEY` | Third-party email validation service key | Yes |
| `PHONE_VALIDATION_API_KEY` | Third-party phone validation service key | Yes |

## Database Setup

The database schema includes 15 tables for comprehensive lead management:

- **Core:** `users`, `organizations`, `user_organizations`
- **Leads:** `lead_sources`, `leads`, `lead_activities`
- **Scoring:** `scoring_criteria`, `lead_scores`, `lead_total_scores`
- **Processing:** `validations`, `enrichment_jobs`
- **Routing:** `routing_rules`, `lead_assignments`
- **System:** `api_integrations`, `reports`

Run migrations with: `npx supabase db push`

## Deploy to Vercel

1. **Connect repository to Vercel**
2. **Set environment variables in Vercel dashboard**
3. **Deploy:** Vercel will automatically build and deploy on push to main

## Project Structure


├── app/                    # Next.js 15 App Router
│   ├── (auth)/            # Authentication pages
│   ├── (protected)/       # Protected dashboard pages
│   └── api/               # API routes
├── components/            # Reusable React components
│   ├── ui/               # Base UI components
│   └── features/         # Feature-specific components
├── db/                   # Database access layer
├── lib/                  # Business logic and utilities
├── actions/              # Server actions
├── integrations/         # External API integrations
├── types/                # TypeScript type definitions
├── supabase/            # Database migrations and config
└── public/              # Static assets


## Key Features

- **Multi-channel lead ingestion** from HubSpot, ads platforms, and phone systems
- **Real-time lead scoring** with configurable weighted criteria
- **Email and phone validation** with third-party verification
- **Lead enrichment** via business databases and social media scraping
- **Automated routing** to sales teams based on scoring thresholds
- **Analytics dashboard** with performance tracking and conversion metrics

## License

Private project - All rights reserved
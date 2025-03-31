# Dog Grooming Management Software - Deployment Guide

This document provides instructions for deploying the Dog Grooming Management Software application.

## Prerequisites

- Node.js 18+ and npm installed
- Cloudflare account (for production deployment)

## Local Development Deployment

1. Navigate to the project directory:
   ```
   cd /home/ubuntu/dog-grooming-app
   ```

2. Install dependencies:
   ```
   npm install
   ```

3. Initialize the database:
   ```
   npx wrangler d1 execute DB --local --file=migrations/0001_initial.sql
   ```

4. Start the development server:
   ```
   npm run dev
   ```

5. Access the application at http://localhost:3000

## Production Deployment

The application can be deployed to Cloudflare Pages with D1 database:

1. Log in to Cloudflare:
   ```
   npx wrangler login
   ```

2. Create a D1 database (if not already created):
   ```
   npx wrangler d1 create dog-grooming-db
   ```

3. Update the wrangler.toml file with your database ID

4. Apply database migrations:
   ```
   npx wrangler d1 migrations apply DB
   ```

5. Deploy the application:
   ```
   npm run deploy
   ```

6. The deployment will provide a URL where the application can be accessed.

## Environment Configuration

For production deployment, you'll need to set up the following environment variables in Cloudflare Pages:

- `DB`: The D1 database binding
- `SMS_API_KEY`: Your SMS gateway API key
- `WHATSAPP_API_KEY`: Your WhatsApp Business API key

## Post-Deployment Steps

1. Access the application using the provided URL
2. Create an admin user account
3. Configure VAT settings
4. Set up service pricing
5. Create message templates for appointment reminders

## Troubleshooting

If you encounter any issues during deployment:

1. Check the Cloudflare Pages deployment logs
2. Verify database connections using the /api/status endpoint
3. Run the application tests at /test to identify any specific issues

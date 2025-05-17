# Using Supabase with n8n Stack

This guide explains how to access and use Supabase in your n8n stack.

## What is Supabase?

Supabase is an open-source Firebase alternative providing all the backend features you need to build a product:

- PostgreSQL Database
- Authentication
- Auto-generated APIs
- Realtime subscriptions
- Storage
- Functions

## Accessing Supabase Studio

Supabase Studio is a web-based administration tool for Supabase. It's included in your n8n stack and can be accessed at:

```
http://n8n-stack:3333
```

## Authentication

Use the following credentials for Supabase services:

- **Username**: alwazw
- **Password**: WaficWazzan!2

## Supabase Services

The Supabase stack includes several services:

1. **supabase-db**: PostgreSQL database (port 5432)
2. **supabase-auth**: Authentication service (port 9999)
3. **supabase-rest**: RESTful API (port 3001)
4. **supabase-storage**: File storage service (port 5000)
5. **supabase-meta**: Database metadata service (port 8082)
6. **supabase-studio**: Web-based admin interface (port 3333)

## Connecting to Supabase from n8n

To connect n8n to Supabase:

1. Create a new workflow in n8n
2. Add a Supabase node
3. Configure the connection:
   - **Host**: http://supabase-rest:3000
   - **API Key**: Use the SUPABASE_ANON_KEY or SUPABASE_SERVICE_KEY from your .env file
   - **JWT Secret**: Use the SUPABASE_JWT_SECRET from your .env file

## Using Supabase with pgAdmin

You can also manage your Supabase database using pgAdmin:

1. Access pgAdmin at http://n8n-stack:5050
2. Add a new server connection:
   - **Host**: supabase-db
   - **Port**: 5432
   - **Database**: supabase
   - **Username**: alwazw
   - **Password**: WaficWazzan!2

## Environment Variables

The following environment variables are used by Supabase:

- `SUPABASE_DB`: Database name
- `SUPABASE_DB_USER`: Database username
- `SUPABASE_DB_PASSWORD`: Database password
- `SUPABASE_JWT_SECRET`: Secret key for JWT tokens
- `SUPABASE_ADMIN_EMAIL`: Admin email address
- `SUPABASE_ANON_KEY`: Anonymous API key
- `SUPABASE_SERVICE_KEY`: Service role API key

## Troubleshooting

If you encounter issues with Supabase:

1. Check that all Supabase containers are running:
   ```
   docker compose ps supabase-db supabase-auth supabase-rest supabase-storage supabase-meta supabase-studio
   ```

2. View logs for specific services:
   ```
   docker compose logs supabase-db
   docker compose logs supabase-auth
   ```

3. Verify environment variables are correctly set in your .env file

## Security Note

For production environments, consider:

1. Generating new JWT secrets and API keys
2. Restricting access using a firewall
3. Setting up proper backup procedures for your data

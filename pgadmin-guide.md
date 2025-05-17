# Using pgAdmin with n8n Stack

This guide explains how to access and use pgAdmin to manage your PostgreSQL database in the n8n stack.

## Accessing pgAdmin

pgAdmin is a web-based administration tool for PostgreSQL. It's included in your n8n stack and can be accessed at:

```
http://n8n-stack:5050
```

## Login Credentials

Use the following credentials to log in to pgAdmin:

- **Email**: admin@n8n-stack.local
- **Password**: The same as your PostgreSQL password (defined in your .env file)

## Connecting to Your PostgreSQL Server

After logging in, you need to add a connection to your PostgreSQL server:

1. Right-click on "Servers" in the left panel and select "Create" → "Server..."

2. In the "General" tab:
   - Name: n8n-postgres (or any name you prefer)

3. In the "Connection" tab:
   - Host name/address: postgres
   - Port: 5432
   - Maintenance database: postgres
   - Username: Your PostgreSQL username (from .env file)
   - Password: Your PostgreSQL password (from .env file)
   - Save password: Checked

4. Click "Save"

## Accessing Your n8n Database

After connecting to the PostgreSQL server:

1. Expand "Servers" → "n8n-postgres" → "Databases"
2. Find and click on your n8n database (typically named "n8n")
3. You can now browse tables, run queries, and manage your database

## Features

pgAdmin provides many features for PostgreSQL database management:

- SQL query tool with syntax highlighting
- Table data viewing and editing
- Schema browser
- Server configuration
- Backup and restore functionality
- Performance monitoring

## Troubleshooting

If you cannot connect to the PostgreSQL server:

1. Ensure the PostgreSQL container is running:
   ```
   docker compose ps postgres
   ```

2. Check that the network connection is working:
   ```
   docker compose exec pgadmin ping postgres
   ```

3. Verify your credentials in the .env file match what you're using in pgAdmin

## Security Note

pgAdmin is accessible on port 5050 without HTTPS. For production environments, consider:

1. Putting pgAdmin behind the Nginx reverse proxy with HTTPS
2. Restricting access using a firewall
3. Using strong, unique passwords

# N8N Stack with Nginx and Traefik

This document provides an overview of the updated n8n stack configuration with Nginx and Traefik for HTTPS access.

## Stack Components

The stack now includes the following services:

1. **n8n**: The main workflow automation platform
2. **n8n-worker**: Worker service for n8n
3. **PostgreSQL**: Database for n8n
4. **Redis**: Queue management for n8n
5. **Adminer**: Database management interface
6. **Grafana**: Monitoring and visualization
7. **Nginx**: Reverse proxy for HTTPS access to n8n
8. **Traefik**: Alternative reverse proxy for future internal/external HTTPS termination

## Configuration Overview

### Nginx Configuration

Nginx is configured as a reverse proxy for n8n with HTTPS support:
- Redirects HTTP to HTTPS
- Uses self-signed certificates for local development
- Properly forwards headers and supports WebSockets

### Traefik Configuration

Traefik is set up as an alternative reverse proxy:
- Configured for both internal and external access
- Supports HTTPS termination
- Includes dashboard for monitoring and management
- Ready for future expansion with automatic certificate management

## Network Configuration

All services are connected through a dedicated bridge network (`n8n-network`), ensuring proper communication between containers.

## Host Configuration

To access the stack using the hostname `n8n-stack`, you need to update your host system's configuration. See the `host-configuration.md` file for detailed instructions.

## Accessing Services

- n8n: https://n8n-stack/
- Adminer: http://192.168.2.104:8080
- Grafana: http://192.168.2.104:3000
- Traefik Dashboard: http://192.168.2.104:8081

## Security Notes

- The stack uses self-signed certificates for local development
- For production use, consider using proper CA-signed certificates
- Traefik is configured for future automatic certificate management with Let's Encrypt

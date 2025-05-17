# N8N Stack with Nginx and Traefik

This repository contains a Docker Compose setup for n8n workflow automation platform with Nginx and Traefik for HTTPS access.

## Stack Components

The stack includes the following services:

1. **n8n**: The main workflow automation platform
2. **n8n-worker**: Worker service for n8n
3. **PostgreSQL**: Database for n8n
4. **Redis**: Queue management for n8n
5. **Adminer**: Database management interface
6. **Grafana**: Monitoring and visualization
7. **Nginx**: Reverse proxy for HTTPS access to n8n
8. **Traefik**: Alternative reverse proxy for future internal/external HTTPS termination

## Getting Started

### Prerequisites

- Docker and Docker Compose installed
- Basic understanding of networking and DNS

### Setup Instructions

1. Clone this repository:
   ```
   git clone https://github.com/alwazw/n8n-stack.git
   cd n8n-stack
   ```

2. Configure hostname resolution (see [Host Configuration Guide](host-configuration.md))
   - For Windows: Update C:\Windows\System32\drivers\etc\hosts
   - For Linux: Update /etc/hosts

3. Start the stack:
   ```
   docker compose up -d
   ```

4. Access n8n securely at:
   ```
   https://n8n-stack/
   ```

5. For browser certificate warnings, see [Certificate Trust Guide](certificate-trust-guide.md)

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

## Accessing Services

- n8n: https://n8n-stack/
- Adminer: http://n8n-stack:8080
- Grafana: http://n8n-stack:3000
- Traefik Dashboard: http://n8n-stack:8081

## Troubleshooting

If you encounter issues:

1. Verify hostname resolution:
   ```
   ping n8n-stack
   ```

2. Check if containers are running:
   ```
   docker compose ps
   ```

3. View logs:
   ```
   docker compose logs nginx
   docker compose logs n8n
   ```

4. For certificate issues, see [Certificate Trust Guide](certificate-trust-guide.md)

## Security Notes

- The stack uses self-signed certificates for local development
- For production use, consider using proper CA-signed certificates
- Traefik is configured for future automatic certificate management with Let's Encrypt

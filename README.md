# N8N Stack with Complete Service Suite

This repository contains a comprehensive Docker Compose setup for n8n workflow automation platform with a complete suite of supporting services for monitoring, security, data processing, API management, backup, visualization, and secure tunneling.

## Stack Components

The stack includes the following services:

### Core Services
1. **n8n**: The main workflow automation platform (latest)
2. **n8n-worker**: Worker service for n8n (latest)
3. **PostgreSQL**: Database for n8n and other services (v16)
4. **Redis**: Queue management for n8n (6-alpine)

### Database Management
5. **pgAdmin**: Web-based PostgreSQL administration tool (latest)
6. **Adminer**: Simple database management interface (latest)

### Backend Services
7. **Supabase**: Open-source Firebase alternative with authentication, storage, and more
   - Supabase PostgreSQL database (latest)
   - Authentication service (latest)
   - RESTful API (latest)
   - Storage service (latest)
   - Database metadata service (latest)
   - Supabase Studio (latest)

### Monitoring & Observability
8. **Prometheus**: Metrics collection and monitoring (latest)
9. **Alertmanager**: Alert handling for Prometheus (latest)
10. **Loki**: Log aggregation system (latest)
11. **Promtail**: Log collector for Loki (latest)
12. **Grafana**: Monitoring and visualization dashboard (latest)
13. **cAdvisor**: Container resource usage and performance analysis (latest)

### Security & Secrets Management
14. **HashiCorp Vault**: Secrets management (latest)
15. **Keycloak**: Identity and access management (latest)

### Message Queue & Data Processing
16. **RabbitMQ**: Advanced message queuing protocol broker (3-management)
17. **Apache NiFi**: Data flow automation (latest)
18. **Minio**: S3-compatible object storage (latest)

### Development & API Management
19. **Kong**: API gateway (latest)
20. **Portainer**: Container management UI (latest)

### Backup & Disaster Recovery
21. **Duplicati**: Automated backups (latest)

### Frontend & Visualization
22. **Metabase**: Business intelligence and analytics (latest)
23. **Node-RED**: Visual workflow automation (latest)

### Networking & Proxy
24. **Nginx**: Reverse proxy for HTTPS access (alpine)
25. **Traefik**: Alternative reverse proxy for future internal/external HTTPS termination (v2.10)
26. **Cloudflared**: Secure tunneling to expose services to the internet (latest)

## Getting Started

### Prerequisites

- Docker and Docker Compose installed
- Basic understanding of networking and DNS
- Cloudflare account (for Cloudflared tunnel setup)

### Setup Instructions

1. Clone this repository:
   ```
   git clone https://github.com/alwazw/n8n-stack.git
   cd n8n-stack
   ```

2. Configure hostname resolution (see [Host Configuration Guide](host-configuration.md))
   - For Windows: Update C:\Windows\System32\drivers\etc\hosts
   - For Linux: Update /etc/hosts

3. Create necessary directories for configuration files:
   ```
   mkdir -p prometheus alertmanager loki promtail vault/config nifi/flow grafana/{provisioning,dashboards} backups source cloudflared
   ```

4. Set up Cloudflared tunnel:
   - Log in to your Cloudflare account
   - Create a tunnel in the Zero Trust dashboard
   - Copy the tunnel token
   - Update the `CLOUDFLARED_TUNNEL_TOKEN` in your `.env` file
   - Configure your tunnel in the Cloudflare dashboard to route to your services

5. Start the stack:
   ```
   docker compose up -d
   ```

6. Access services:

   | Service | URL | Default Credentials |
   |---------|-----|---------------------|
   | n8n | https://n8n-stack:5678/ | N/A |
   | pgAdmin | http://n8n-stack:5050/ | Email: admin@n8n-stack.local<br>Password: WaficWazzan!2 |
   | Adminer | http://n8n-stack:8080/ | Server: postgres<br>Username: alwazw<br>Password: WaficWazzan!2 |
   | Grafana | http://n8n-stack:3000/ | Username: alwazw<br>Password: WaficWazzan!2 |
   | Supabase Studio | http://n8n-stack:3333/ | Email: admin@n8n-stack.local<br>Password: WaficWazzan!2 |
   | Prometheus | http://n8n-stack:9090/ | N/A |
   | Alertmanager | http://n8n-stack:9093/ | N/A |
   | cAdvisor | http://n8n-stack:8085/ | N/A |
   | RabbitMQ Management | http://n8n-stack:15672/ | Username: alwazw<br>Password: WaficWazzan!2 |
   | Vault | http://n8n-stack:8200/ | Token: 8ae8234234h243294324 |
   | Keycloak | http://n8n-stack:8090/ | Username: alwazw<br>Password: WaficWazzan!2 |
   | NiFi | http://n8n-stack:8070/ | Username: alwazw<br>Password: WaficWazzan!2 |
   | Minio | http://n8n-stack:9001/ | Username: alwazw<br>Password: WaficWazzan!2 |
   | Kong Admin | http://n8n-stack:8001/ | N/A |
   | Portainer | https://n8n-stack:9443/ | Create on first login |
   | Duplicati | http://n8n-stack:8200/ | Create on first login |
   | Metabase | http://n8n-stack:3030/ | Create on first login |
   | Node-RED | http://n8n-stack:1880/ | Create on first login |
   | Traefik Dashboard | http://n8n-stack:8081/ | N/A |

7. For browser certificate warnings, see [Certificate Trust Guide](certificate-trust-guide.md)

## Service Documentation

### Database Management

- For detailed instructions on using pgAdmin, see the [pgAdmin Guide](pgadmin-guide.md)
- Adminer provides a simpler alternative to pgAdmin and can be accessed at http://n8n-stack:8080

### Supabase

For detailed instructions on using Supabase, see the [Supabase Guide](supabase-guide.md).

### Monitoring & Observability

The stack includes a complete monitoring solution:

- **Prometheus**: Collects metrics from all services
- **Alertmanager**: Handles alerts from Prometheus
- **Loki**: Collects and indexes logs
- **Promtail**: Forwards logs to Loki
- **Grafana**: Visualizes metrics and logs
- **cAdvisor**: Provides container resource usage and performance analysis

Grafana is pre-configured to connect to Prometheus and Loki, providing dashboards for monitoring all services.

### Message Queue & Data Processing

- **RabbitMQ**: Advanced message broker for reliable communication between services
- **NiFi**: Visual data flow automation for complex data processing
- **Minio**: S3-compatible object storage for files and backups

### Security & Secrets Management

- **Vault**: Securely store and manage secrets
- **Keycloak**: Centralized authentication and authorization

### Development & API Management

- **Kong**: API gateway for managing and securing APIs
- **Portainer**: Web-based interface for managing Docker containers

### Backup & Disaster Recovery

- **Duplicati**: Automated backup solution for all data

### Frontend & Visualization

- **Metabase**: Business intelligence and analytics platform
- **Node-RED**: Visual programming for event-driven applications

### Cloudflared Tunnel

Cloudflared provides secure tunneling to expose your services to the internet without opening ports on your firewall:

1. **Setup**: 
   - Create a tunnel in the Cloudflare Zero Trust dashboard
   - Configure the tunnel to route to your services
   - Add the tunnel token to your `.env` file

2. **Usage**:
   - Access your services through the Cloudflare tunnel URLs
   - Manage your tunnel in the Cloudflare Zero Trust dashboard

3. **Benefits**:
   - No need to open ports on your firewall
   - End-to-end encryption
   - DDoS protection
   - Access control through Cloudflare Zero Trust

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

## Environment Variables

All services use shared credentials defined in the `.env` file:
- Username: alwazw
- Password: WaficWazzan!2
- Encryption keys and secrets are shared where appropriate

## Image Version Notes

All services have been configured to use the latest stable versions of their respective Docker images. This ensures compatibility and access to the most recent features and security updates. Key version details:

- **n8n**: Using the latest official image from docker.n8n.io/n8nio/n8n
- **PostgreSQL**: Using version 16
- **Redis**: Using 6-alpine for lightweight performance
- **Supabase**: All components updated to latest versions
- **Traefik**: Using v2.10
- **RabbitMQ**: Using 3-management for the management UI

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
   docker compose logs <service-name>
   ```

4. For certificate issues, see [Certificate Trust Guide](certificate-trust-guide.md)

5. If you encounter image pull errors, ensure you have the latest images:
   ```
   docker compose pull
   ```

## Security Notes

- The stack uses self-signed certificates for local development
- For production use, consider using proper CA-signed certificates
- Default credentials are shared across services for simplicity; consider changing for production
- Traefik is configured for future automatic certificate management with Let's Encrypt
- Cloudflared provides secure access to your services without exposing ports

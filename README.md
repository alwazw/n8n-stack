# N8N Stack with Complete Service Suite

This repository contains a comprehensive Docker Compose setup for n8n workflow automation platform with a complete suite of supporting services for monitoring, security, data processing, API management, backup, and visualization.

## Stack Components

The stack includes the following services:

### Core Services
1. **n8n**: The main workflow automation platform
2. **n8n-worker**: Worker service for n8n
3. **PostgreSQL**: Database for n8n and other services
4. **Redis**: Queue management for n8n

### Database Management
5. **pgAdmin**: Web-based PostgreSQL administration tool
6. **Adminer**: Simple database management interface

### Backend Services
7. **Supabase**: Open-source Firebase alternative with authentication, storage, and more
   - Supabase PostgreSQL database
   - Authentication service
   - RESTful API
   - Storage service
   - Database metadata service
   - Supabase Studio (web interface)

### Monitoring & Observability
8. **Prometheus**: Metrics collection and monitoring
9. **Alertmanager**: Alert handling for Prometheus
10. **Loki**: Log aggregation system
11. **Promtail**: Log collector for Loki
12. **Grafana**: Monitoring and visualization dashboard

### Security & Secrets Management
13. **HashiCorp Vault**: Secrets management
14. **Keycloak**: Identity and access management

### Data Processing & Integration
15. **Apache NiFi**: Data flow automation
16. **Minio**: S3-compatible object storage

### Development & API Management
17. **Kong**: API gateway
18. **Portainer**: Container management UI

### Backup & Disaster Recovery
19. **Duplicati**: Automated backups

### Frontend & Visualization
20. **Metabase**: Business intelligence and analytics
21. **Node-RED**: Visual workflow automation

### Networking & Proxy
22. **Nginx**: Reverse proxy for HTTPS access
23. **Traefik**: Alternative reverse proxy for future internal/external HTTPS termination

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

3. Create necessary directories for configuration files:
   ```
   mkdir -p prometheus alertmanager loki promtail vault/config nifi/flow grafana/{provisioning,dashboards} backups source
   ```

4. Start the stack:
   ```
   docker compose up -d
   ```

5. Access services:

   | Service | URL | Default Credentials |
   |---------|-----|---------------------|
   | n8n | https://n8n-stack:5678/ | N/A |
   | pgAdmin | http://n8n-stack:5050/ | Email: admin@n8n-stack.local<br>Password: WaficWazzan!2 |
   | Adminer | http://n8n-stack:8080/ | Server: postgres<br>Username: alwazw<br>Password: WaficWazzan!2 |
   | Grafana | http://n8n-stack:3000/ | Username: alwazw<br>Password: WaficWazzan!2 |
   | Supabase Studio | http://n8n-stack:3333/ | Email: admin@n8n-stack.local<br>Password: WaficWazzan!2 |
   | Prometheus | http://n8n-stack:9090/ | N/A |
   | Alertmanager | http://n8n-stack:9093/ | N/A |
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

6. For browser certificate warnings, see [Certificate Trust Guide](certificate-trust-guide.md)

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

Grafana is pre-configured to connect to Prometheus and Loki, providing dashboards for monitoring all services.

### Security & Secrets Management

- **Vault**: Securely store and manage secrets
- **Keycloak**: Centralized authentication and authorization

### Data Processing & Integration

- **NiFi**: Visual data flow automation for complex data processing
- **Minio**: S3-compatible object storage for files and backups

### Development & API Management

- **Kong**: API gateway for managing and securing APIs
- **Portainer**: Web-based interface for managing Docker containers

### Backup & Disaster Recovery

- **Duplicati**: Automated backup solution for all data

### Frontend & Visualization

- **Metabase**: Business intelligence and analytics platform
- **Node-RED**: Visual programming for event-driven applications

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

## Security Notes

- The stack uses self-signed certificates for local development
- For production use, consider using proper CA-signed certificates
- Default credentials are shared across services for simplicity; consider changing for production
- Traefik is configured for future automatic certificate management with Let's Encrypt

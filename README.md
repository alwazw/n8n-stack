# N8N Stack with Complete Service Suite

This repository contains a comprehensive Docker Compose stack for n8n workflow automation with a complete suite of supporting services.

## Services Overview

### Core Services
- **n8n**: Workflow automation platform
- **PostgreSQL**: Primary database
- **Redis**: In-memory data store and message broker
- **Adminer**: Database management UI
- **pgAdmin**: PostgreSQL management UI

### Backend Services
- **Supabase**: Backend-as-a-Service platform including:
  - PostgreSQL database
  - Authentication service
  - RESTful API
  - Storage service
  - Database metadata service
  - Studio web interface

### Monitoring & Observability
- **Prometheus**: Metrics collection and alerting
- **Grafana**: Visualization and dashboards
- **Loki**: Log aggregation
- **Promtail**: Log collection agent
- **cAdvisor**: Container resource usage and performance metrics
- **Jaeger**: Distributed tracing system

### Security & Secrets Management
- **Vault**: Secrets management
- **Keycloak**: Identity and access management
- **ClamAV**: Antivirus scanning
- **Falco**: Runtime security monitoring

### Message Queue & Data Processing
- **RabbitMQ**: Advanced message broker
- **NiFi**: Data flow automation
- **Minio**: S3-compatible object storage

### Development & API Management
- **Kong**: API gateway
- **Portainer**: Container management UI
- **Terraform**: Infrastructure as Code
- **Selenium**: Browser automation

### Backup & Disaster Recovery
- **Duplicati**: Backup solution

### Frontend & Visualization
- **Metabase**: Business intelligence and analytics
- **Node-RED**: Visual programming for event-driven applications

### Networking & Proxy
- **Nginx**: Web server and reverse proxy
- **Traefik**: Modern reverse proxy and load balancer
- **Cloudflared**: Secure tunneling to Cloudflare
- **Consul**: Service discovery and configuration
- **Keepalived**: High availability for IP failover
- **Postfix**: Mail transfer agent

## Access Information

| Service | URL | Default Credentials |
|---------|-----|---------------------|
| n8n | https://n8n-stack:5678/ | N/A |
| Adminer | http://n8n-stack:8080/ | Server: postgres, Username: alwazw, Password: WaficWazzan!2 |
| pgAdmin | http://n8n-stack:5050/ | Email: admin@n8n-stack.local, Password: WaficWazzan!2 |
| Grafana | http://n8n-stack:3000/ | Username: alwazw, Password: WaficWazzan!2 |
| Supabase Studio | http://n8n-stack:3333/ | Email: admin@n8n-stack.local, Password: WaficWazzan!2 |
| Prometheus | http://n8n-stack:9090/ | N/A |
| Alertmanager | http://n8n-stack:9093/ | N/A |
| Loki | http://n8n-stack:3100/ | N/A |
| cAdvisor | http://n8n-stack:8085/ | N/A |
| Vault | http://n8n-stack:8200/ | Token: 8ae8234234h243294324 |
| Keycloak | http://n8n-stack:8090/ | Username: alwazw, Password: WaficWazzan!2 |
| RabbitMQ | http://n8n-stack:15672/ | Username: alwazw, Password: WaficWazzan!2 |
| NiFi | http://n8n-stack:8070/ | Username: alwazw, Password: WaficWazzan!2 |
| Minio | http://n8n-stack:9001/ | Username: alwazw, Password: WaficWazzan!2 |
| Kong | http://n8n-stack:8001/ | N/A |
| Portainer | https://n8n-stack:9443/ | Create on first login |
| Duplicati | http://n8n-stack:8200/ | Create on first login |
| Metabase | http://n8n-stack:3030/ | Create on first login |
| Node-RED | http://n8n-stack:1880/ | Create on first login |
| Traefik | http://n8n-stack:8081/ | N/A |
| Jaeger | http://n8n-stack:16686/ | N/A |
| Consul | http://n8n-stack:8500/ | N/A |
| Selenium | http://n8n-stack:4444/ | N/A |
| Selenium VNC | http://n8n-stack:7900/ | No password |

## Deployment Instructions

1. Clone this repository:
   ```
   git clone https://github.com/alwazw/n8n-stack.git
   cd n8n-stack
   ```

2. Create necessary directories:
   ```
   mkdir -p prometheus alertmanager loki promtail vault/config nifi/flow grafana/{provisioning,dashboards} backups source cloudflared keepalived terraform
   ```

3. Update host configuration:
   - Follow instructions in `host-configuration.md`

4. Start the stack:
   ```
   docker compose up -d
   ```

5. Access services using the URLs listed above

## Image Version Notes

All services use the latest stable versions of their respective images. If you encounter image pull errors, you may need to update the image tags in the docker-compose.yml file.

For Supabase components, we use the latest tags to ensure compatibility between components.

## Troubleshooting

### Docker Compose Errors

If you encounter a "concurrent map writes" error when running `docker compose up -d`, try the following:

1. Run with limited parallelism:
   ```
   COMPOSE_PARALLEL_LIMIT=1 docker compose up -d
   ```

2. Start services in groups:
   ```
   docker compose up -d postgres redis
   docker compose up -d n8n grafana
   docker compose up -d supabase-db supabase-auth supabase-rest supabase-storage supabase-meta supabase-studio
   docker compose up -d prometheus alertmanager loki promtail cadvisor
   docker compose up -d vault keycloak rabbitmq
   docker compose up -d nifi minio
   docker compose up -d kong portainer
   docker compose up -d duplicati
   docker compose up -d metabase node-red
   docker compose up -d nginx traefik cloudflared
   docker compose up -d jaeger consul terraform clamav falco selenium postfix keepalived
   ```

### Service-Specific Issues

#### Keepalived
- Requires host networking and privileged mode
- May conflict with existing Keepalived instances on the host
- Virtual IP must be on the same subnet as the host

#### Falco
- Requires privileged mode and kernel modules
- May not work in all environments, especially containerized hosts

#### ClamAV
- Initial database download may take time
- High memory usage during database updates

#### Selenium
- Requires significant memory (2GB+ recommended)
- VNC viewer available on port 7900 for debugging

#### Consul
- Configured for development mode (single node)
- For production, adjust for multi-node cluster

## Security Notes

- Default credentials are used across services for simplicity
- For production use, change all passwords and secrets
- Consider using Vault for secret management
- Enable TLS for all services in production

## Maintenance

- Regular updates are recommended for security
- Back up volumes regularly
- Monitor resource usage, especially for memory-intensive services

## License

This project is licensed under the MIT License - see the LICENSE file for details.

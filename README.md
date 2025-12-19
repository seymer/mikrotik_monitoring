# Mikrotik Monitoring

A comprehensive monitoring solution for Mikrotik devices using Prometheus, Grafana, and MKTXP exporter.

## Overview

This project sets up a monitoring stack to collect and visualize metrics from Mikrotik routers using:
- **MKTXP**: Mikrotik exporter for Prometheus
- **Prometheus**: Time-series database for metrics storage and querying
- **Grafana**: Dashboard for metrics visualization

## Features

- Real-time monitoring of Mikrotik device metrics
- Pre-configured dashboards for system stats, network interfaces, CPU, memory, etc.
- Docker-based deployment for easy setup
- Configurable retention and alerting rules

## Prerequisites

- Docker and Docker Compose installed on your system
- Access to Mikrotik devices with API enabled

## Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/seymer/mikrotik_monitoring.git
   cd mikrotik_monitoring
   ```

2. **Configure MKTXP:**
   Edit `mktxp/mktxp.conf` to add your Mikrotik device details:
   ```ini
   [Mikrotik-Router]
   enabled = True
   hostname = your-router-ip
   username = your-username
   password = your-password
   ```

3. **Start the services:**
   ```bash
   docker-compose up -d
   ```

4. **Access the interfaces:**
   - Grafana: http://localhost:3000 (admin/admin)
   - Prometheus: http://localhost:9090

## Configuration

### MKTXP Configuration
- Main config: `mktxp/mktxp.conf`
- Additional config: `mktxp/_mktxp.conf`

### Prometheus Configuration
- Config file: `prometheus/prometheus.yml`
- Retention: 200 hours (configurable in docker-compose.yml)

### Grafana Configuration
- Dashboards: `grafana/dashboards/`
- Datasources: `grafana/datasources/`
- Default admin password: `admin` (set in docker-compose.yml)

## Dashboards

The project includes pre-configured Grafana dashboards:
- `monitor.json`: Comprehensive monitoring dashboard
- `grafana.json`: Merged dashboard with additional panels

Dashboards are automatically provisioned and organized in the "Mikrotik Monitoring" folder.

## Services

### Prometheus
- Port: 9090
- Data retention: 200 hours
- Scrapes metrics from MKTXP every 30 seconds

### Grafana
- Port: 3000
- Admin credentials: admin/admin
- Auto-provisions datasources and dashboards

### MKTXP
- Exports Mikrotik metrics to Prometheus format
- Supports multiple routers
- Configurable metrics collection

## Troubleshooting

### Common Issues

1. **Grafana not loading dashboards:**
   - Ensure dashboard files are in `grafana/dashboards/`
   - Check `grafana/dashboards/dashboard.yml` for correct folder configuration
   - Restart Grafana: `docker-compose restart grafana`

2. **No metrics in Prometheus:**
   - Verify MKTXP configuration and router connectivity
   - Check MKTXP logs: `docker-compose logs mktxp`
   - Ensure router API is enabled and accessible

3. **Public IP not showing:**
   - Disable public IP collection in `mktxp/mktxp.conf` if behind NAT
   - Set `public_ip = False`

### Logs
```bash
# View all logs
docker-compose logs

# View specific service logs
docker-compose logs prometheus
docker-compose logs grafana
docker-compose logs mktxp
```

## Customization

### Adding New Dashboards
1. Place JSON files in `grafana/dashboards/`
2. Update `grafana/dashboards/dashboard.yml` if needed
3. Restart Grafana

### Modifying Metrics
- Edit MKTXP config to enable/disable specific metrics
- Update Prometheus scrape intervals in `prometheus/prometheus.yml`

## Security Notes

- Change default Grafana admin password in production
- Use secure passwords for Mikrotik devices
- Consider network isolation for monitoring stack

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

This project is open source. Please check individual component licenses.

## Support

For issues and questions:
- Check the troubleshooting section
- Review Docker and component documentation
- Open an issue on GitHub</content>
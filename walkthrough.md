# Guacamole Installation Walkthrough

I have installed Apache Guacamole using Docker Compose. This setup includes:
- **Guacamole Client**: The web interface (port 8080).
- **Guacd**: The proxy daemon.
- **PostgreSQL**: Database for connection settings and users.

## Changes Made
- Removed the conflicting `guac` container (ID `17a68aac620c`).
- Created `C:\Users\MBStudios\.gemini\antigravity\scratch\guacamole-docker`.
- Generated `initdb.sql` for PostgreSQL initialization.
- Created `docker-compose.yml` defining the service stack.

## verification Results

### Automated Tests
- [x] Docker services running (`docker-compose ps`)
- [x] Port 8080 accessible
- [x] Login page is visible (Fixed 500 Error)

![Guacamole Login Page](images/guacamole_login_page.png)

## Troubleshooting / Fixes Applied
- **500 Error Fix**: The initial 500 error was caused by a missing database schema. The `initdb.sql` was regenerated with the correct `--postgresql` flag (instead of `--postgres`) and the database was reset.
- **Environment Variables**: Updated to use `POSTGRESQL_*` instead of deprecated `POSTGRES_*`.

## How to Access

### From Inside the VM
1. Open your browser to [http://localhost:8080/guacamole/](http://localhost:8080/guacamole/).

### From Your Host PC
1. Use the VM's IP address: **http://172.30.88.228:8080/guacamole/**
   *(Note: If this doesn't work, ensure your VM's network is set to "Bridged" or check if you have a VPN/Tailscale IP like 100.66.224.55)*
2. Login with `guacadmin` / `guacadmin`.
3. Configure your connections (RDP, VNC, SSH) in the Guacamole settings.
2. Login with default credentials:
    - Username: `guacadmin`
    - Password: `guacadmin`
3. **IMPORTANT**: Change the password immediately after logging in.

## Troubleshooting
If you cannot access the page:
- Ensure the containers are running: `docker-compose ps` in the `guacamole-docker` directory.
- Check logs: `docker-compose logs -f`.

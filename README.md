# mcpena (Make Container/Pod Enabled)
*Read this in other languages: [Indonesian (Bahasa Indonesia)](README-id.md)*

**Why does this exist when we already have `--restart=always`?**
While native restart policies work for basic setups, they fall short in robust environments. **Podman** (especially in rootless mode) heavily relies on `systemd` integration and `enable-linger` to reliably start containers on boot and support `podman auto-update`. Furthermore, advanced Sysadmins often need container lifecycles to strictly depend on OS-level services (e.g., waiting for a VPN or network mount to be ready).

`mcpena` is a powerful shell script that solves these complexities by acting as a **Systemd Orchestration Tool**. It seamlessly bridges your OS init system with your container engines (**Podman** and **Docker**), turning your containers into true, reliable first-class citizens of your server.

## Key Features
1. **OS & Init System Detection**: Supports automatic detection of your Linux operating system's init system (supports `systemd`, `OpenRC`, and `SysVinit`).
2. **Podman & Docker Support**: Automatically detects whether your target container is running on Podman or Docker. 
3. **Podman Version Compatibility**: Supports the legacy `podman generate systemd` command (for older podman versions) and features a fallback mechanism for newer podman versions (v5+) where the command is deprecated/removed.
4. **User Level Detection**: Automatically adjusts execution to either `root` (system-wide service) or a regular user (`rootless` using `systemctl --user`).
5. **Docker Customization**: Allows you to choose whether to use Docker's native *Restart Policy* (recommended by default) or force the creation of a *Systemd Service* for Docker.
6. **Smart Naming & Collision Guard**: Automatically simplifies generated service names (stripping `container-` or `pod_`), prevents accidental overwrites, and supports fully custom service names via the `--name` flag.

## Installation

Download the `mcpena` script, make it executable, and place it in your system's bin folder so it can be called from anywhere.

```bash
curl -O https://raw.githubusercontent.com/salmankalista/mcpena/master/mcpena
chmod +x mcpena
sudo mv mcpena /usr/local/bin/
```

## Usage

Basic usage (the script will auto-detect engine, init system, and user context):
```bash
mcpena your-container-name
```

Start the service immediately (after enabling it via the `--now` option):
```bash
mcpena your-container-name --now
```

### Advanced Options

You can explicitly define the container engine, method, or service name if needed:

```bash
# Set a custom service name (e.g., creates 'my-app.service' instead of 'web-server.service')
mcpena web-server --name my-app

# Force using Podman engine
mcpena web-server --engine podman

# Force using Docker engine
mcpena db-server --engine docker

# For Docker, the script uses the 'restart policy' feature by default. 
# If you want to force the creation of a systemd service for Docker:
mcpena cache-server --engine docker --method systemd
```

## Support & Buy me a Coffee ☕

If this script helped you and saved your time, please consider supporting the developer via the links below:
- **Ko-fi**: [https://ko-fi.com/abgtg](https://ko-fi.com/abgtg)
- **Saweria**: [https://saweria.co/abggtg](https://saweria.co/abggtg)

Thank you for your support!

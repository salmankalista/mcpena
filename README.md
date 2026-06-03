# mcpena (Make Container/Pod Enabled)
*Read this in other languages: [Indonesian (Bahasa Indonesia)](README-id.md)*

`mcpena` is a shell script to automate the process of creating startup services (to automatically run on boot/reboot) for containers or pods created using **Podman** or **Docker**. 

## Key Features
1. **OS & Init System Detection**: Supports automatic detection of your Linux operating system's init system (supports `systemd`, `OpenRC`, and `SysVinit`).
2. **Podman & Docker Support**: Automatically detects whether your target container is running on Podman or Docker. 
3. **Podman Version Compatibility**: Supports the legacy `podman generate systemd` command (for older podman versions) and features a fallback mechanism for newer podman versions (v5+) where the command is deprecated/removed.
4. **User Level Detection**: Automatically adjusts execution to either `root` (system-wide service) or a regular user (`rootless` using `systemctl --user`).
5. **Docker Customization**: Allows you to choose whether to use Docker's native *Restart Policy* (recommended by default) or force the creation of a *Systemd Service* for Docker.

## Installation

Download the `mcpena` script, make it executable, and place it in your system's bin folder so it can be called from anywhere.

```bash
curl -O https://raw.githubusercontent.com/salmankalista/podman-auto-services/main/mcpena
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

You can explicitly define the container engine or method if needed:

```bash
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

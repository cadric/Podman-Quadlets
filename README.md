```markdown
# Quadlet Container Files for Podman (Rootless Setup)

This repository contains `.container` files for use with Podman and Quadlets in a rootless environment.

## Installation Instructions

### Step 1: Place the Files
Move the container files to the following directory:

```bash
/home/YOURUSERNAME/.config/containers/systemd
```

> Note: You may need to create the `containers` and `systemd` directories if they don't exist. To do this, navigate to `/home/YOURUSERNAME/.config/` and run the following commands:

```bash
mkdir -p containers/systemd
```

### Step 2: Reload Systemd Daemon

To allow `systemd` to find your user files, run the following command:

```bash
systemctl --user daemon-reload
```

### Step 3: Start Your Quadlet Services

Use the following commands to start the specific Quadlet services you need. Replace `jellyfin` and `jellyseerr` with the appropriate service names for your containers:

```bash
systemctl --user start jellyfin
systemctl --user start jellyseerr
```

### Step 4: Enable Auto-Restart After Reboot

To ensure that your Quadlet services restart automatically after a reboot, run the following command:

```bash
loginctl enable-linger
```

## Additional Notes

- Make sure you are using Podman in a rootless environment to take advantage of this setup.
- You only need to start the Quadlet services you want to run.

Feel free to reach out if you encounter any issues!
```

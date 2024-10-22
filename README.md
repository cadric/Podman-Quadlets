# Quadlet Container Files for Podman (Rootless Setup)

This repository contains `.container` files for use with Podman and Quadlets in a rootless environment. 

## Installation Instructions

### Step 1: Place the Files

Move the container files to the following directory:

```bash
/home/YOURUSERNAME/.config/containers/systemd
```

> **Important:** Replace `YOURUSERNAME` with your actual username on the system.

If the directories don't exist, create them by navigating to `/home/YOURUSERNAME/.config/` and running the following commands:

```bash
mkdir -p containers/systemd
```

Make sure to also update any paths inside the `.container` files to match your username.

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

- Ensure that you update all instances of `YOURUSERNAME` in the commands and `.container` files to match your actual username.
- This setup has been tested on **Fedora 40**.

Feel free to reach out if you encounter any issues!
```

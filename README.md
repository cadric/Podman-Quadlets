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

### Step 2: Create Local Folders for Volumes

Before starting the Quadlet services, you need to create the local directories that the `Volume=` entries point to. For example, if you have the following in your `.container` files:

```bash
Volume=/home/YOURUSERNAME/jellyfin/config:/config:Z
Volume=/home/YOURUSERNAME/jellyfin/cache:/cache:Z
Volume=/home/YOURUSERNAME/jellyfin/media:/media:Z
```

You will need to create these directories on your system. Run the following commands:

```bash
mkdir -p /home/YOURUSERNAME/jellyfin/config
mkdir -p /home/YOURUSERNAME/jellyfin/cache
mkdir -p /home/YOURUSERNAME/jellyfin/media
```

> **Reminder:** Replace `YOURUSERNAME` with your actual username.

### Step 3: Reload Systemd Daemon

To allow `systemd` to find your user files, run the following command:

```bash
systemctl --user daemon-reload
```

### Step 4: Start Your Quadlet Services

Use the following commands to start the specific Quadlet services you need. Replace `jellyfin` and `jellyseerr` with the appropriate service names for your containers:

```bash
systemctl --user start jellyfin
systemctl --user start jellyseerr
```

### Step 5: Enable Auto-Restart After Reboot

To ensure that your Quadlet services restart automatically after a reboot, run the following command:

```bash
loginctl enable-linger
```

### Step 6: Open Firewall Ports (If Applicable)

If you have a firewall running on your server (Fedora 40 has `firewalld` running by default), make sure to open the necessary ports for the services you are running. For example:

```bash
# Open ports for Sonarr, Jellyfin, and Jellyseerr
firewall-cmd --add-port=8989/tcp --permanent  # Sonarr
firewall-cmd --add-port=8096/tcp --permanent  # Jellyfin
firewall-cmd --add-port=5055/tcp --permanent  # Jellyseerr
firewall-cmd --add-port=13378/tcp --permanent # Audiobookshelf

# Reload the firewall for the changes to take effect
firewall-cmd --reload
```

> **Note:** Replace the port numbers with those used by your services if they differ from the examples above.

## Additional Notes

- Ensure that you update all instances of `YOURUSERNAME` in the commands and `.container` files to match your actual username.
- Make sure to create all the necessary local directories for any `Volume=` entries before starting the Quadlet services.
- Open the required ports on your firewall if it's running.
- This setup has been tested on **Fedora 40**.

# Docker VNC Server

This repository contains a Docker setup for running a VNC server with XFCE4 desktop environment.

## Prerequisites

- Docker
- Docker Compose
- VNC Viewer client

## Setup Instructions

### 1. Clone Repository

```bash
git clone https://github.com/LuongManhLinh/docker-vnc-server.git
cd docker-vnc-server
```

### 2. Build Docker Image

Build and start the container using docker-compose:

```bash
docker-compose up -d --build
```

### 3. Attach to Container

First, get the container ID:
```bash
docker ps
```

Then attach to the container:
```bash
docker exec -it <container_id> sh
```

### 4. Install Desktop Environment and VNC Server

Once inside the container, follow these steps:

1. Update package list:
```bash
apt update
```

2. Install XFCE4 desktop environment:
```bash
apt install xfce4 xfce4-goodies
```

3. Start VNC server:
```bash
vncserver
```

4. Kill existing VNC server (if needed):
```bash
vncserver -kill :1
```

5. Backup original VNC startup file:
```bash
mv ~/.vnc/xstartup ~/.vnc/xstartup.bak
```

6. Create new VNC startup file:
```bash
nano ~/.vnc/xstartup
```

7. Add the following content to the startup file:
```bash
#!/bin/bash
xrdb $HOME/.Xresources
startxfce4 &
```

8. Set proper permissions for the startup file:
```bash
chmod +x ~/.vnc/xstartup
```

9. Set VNC password:
```bash
vncpasswd
```

### 5. Connect to VNC Server

1. Use your VNC viewer to connect to:
```
localhost:5901
```

2. Enter the password you set with vncpasswd

### Troubleshooting

If you see a blank/black screen after connecting:

1. Connect to the container:
```bash
docker exec -it <container_id> sh
```

2. Reinstall dbus:
```bash
apt install --reinstall dbus
```

3. Restart the VNC server:
```bash
vncserver -kill :1
vncserver
```

## Notes

- Default VNC port is 5901 (display :1)
- Make sure to use a secure password when running vncpasswd
- The XFCE4 desktop environment provides a lightweight and user-friendly interface

## Security Considerations

- Change the default VNC password immediately after setup
- Consider using SSH tunneling for secure remote access
- Keep the container and packages updated regularly
 

# Raspberry Pi Home Server for Video Streaming & Game Playing

This guide will walk you through the process of setting up a home server on your Raspberry Pi (RPI) to stream video and play games over your local network.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Setting Up the Raspberry Pi](#setting-up-the-raspberry-pi)
3. [Installing Video Streaming Software](#installing-video-streaming-software)
    - [1. Plex Media Server](#1-plex-media-server)
    - [2. Jellyfin](#2-jellyfin)
4. [Setting Up Game Streaming](#setting-up-game-streaming)
    - [1. Steam Link](#1-steam-link)
    - [2. Moonlight (NVIDIA GameStream)](#2-moonlight-nvidia-gamestream)
5. [Accessing Your Server](#accessing-your-server)
6. [Optional: Remote Access Setup](#optional-remote-access-setup)
7. [Useful Tips](#useful-tips)
8. [Troubleshooting](#troubleshooting)

---

## Prerequisites

### Hardware Requirements
- Raspberry Pi 4 or 3 (4 GB RAM or more recommended)
- MicroSD card (16 GB minimum, 32 GB+ recommended)
- Power supply for Raspberry Pi
- Ethernet cable (optional but recommended for better streaming)
- External storage (USB drive or NAS) for storing videos and games

### Software Requirements
- Raspbian OS (preferably Raspberry Pi OS Lite for a headless setup)
- Access to a PC/Mac for initial setup

### Network Requirements
- A stable WiFi or Ethernet connection
- Local network access (port forwarding for remote access)

---

## Setting Up the Raspberry Pi

1. **Install Raspberry Pi OS**  
   Download Raspberry Pi OS from [here](https://www.raspberrypi.org/software/operating-systems/) and flash it to your MicroSD card using [Raspberry Pi Imager](https://www.raspberrypi.org/software/).

2. **Enable SSH for headless setup**  
   After flashing, create an empty file named `ssh` (without extension) in the `/boot` directory of the SD card. This will enable SSH on first boot.

3. **Boot the Pi**  
   Insert the SD card into your Pi, power it on, and connect via SSH using its local IP:
   ```bash
   ssh pi@<YOUR_RPI_IP>
   ```
   Update & Upgrade
Run the following commands to update the system:
bash
Copy code
sudo apt update
sudo apt upgrade -y
Installing Video Streaming Software
1. Plex Media Server
Install Plex
Add the Plex repo and install Plex Media Server:

bash
Copy code
curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -
echo deb https://downloads.plex.tv/repo/deb public main | sudo tee /etc/apt/sources.list.d/plexmediaserver.list
sudo apt update
sudo apt install plexmediaserver -y
Enable and Start Plex

bash
Copy code
sudo systemctl enable plexmediaserver
sudo systemctl start plexmediaserver
Access Plex
Open your web browser and navigate to http://<YOUR_RPI_IP>:32400/web to set up your media server.

2. Jellyfin
Install Jellyfin
Run the following commands to install Jellyfin:

bash
Copy code
sudo apt install apt-transport-https
wget -O - https://repo.jellyfin.org/debian/jellyfin_team.gpg.key | sudo apt-key add -
echo "deb [arch=$( dpkg --print-architecture )] https://repo.jellyfin.org/debian buster main" | sudo tee /etc/apt/sources.list.d/jellyfin.list
sudo apt update
sudo apt install jellyfin -y
Enable and Start Jellyfin

bash
Copy code
sudo systemctl enable jellyfin
sudo systemctl start jellyfin
Access Jellyfin
Open your web browser and navigate to http://<YOUR_RPI_IP>:8096 to set up Jellyfin.

Setting Up Game Streaming
1. Steam Link
Install Steam Link
Install Steam Link from the Raspbian package repository:

bash
Copy code
sudo apt install steamlink
Launch Steam Link
Run:

bash
Copy code
steamlink
This will open the Steam Link interface, where you can pair with your Steam account and begin game streaming.

2. Moonlight (NVIDIA GameStream)
Install Moonlight
Add Moonlight repo and install:

bash
Copy code
sudo apt-add-repository ppa:moonlight-stream/moonlight
sudo apt update
sudo apt install moonlight -y
Pair with GameStream
Use the following command to pair with your gaming PC (make sure you have an NVIDIA GPU):

bash
Copy code
moonlight pair <Your PC IP>
Start Streaming
Once paired, stream your games with:

bash
Copy code
moonlight stream <Your PC IP>
Accessing Your Server
Once your server is up and running:

Plex Media Server: http://<YOUR_RPI_IP>:32400/web
Jellyfin: http://<YOUR_RPI_IP>:8096
Steam Link: Can be accessed via the Pi’s desktop or directly from a TV/monitor connected to the Pi.
Moonlight: Use Moonlight’s commands to stream from a client device.
Optional: Remote Access Setup
To access your media server from outside your home:

Set up port forwarding on your router for:
Plex: Port 32400
Jellyfin: Port 8096
Use a dynamic DNS service like No-IP to assign a hostname to your public IP.
Useful Tips
For better performance, always use Ethernet over WiFi, especially for game streaming.
External storage is highly recommended for storing large video libraries.
Keep your Raspberry Pi updated:
bash
Copy code
sudo apt update && sudo apt upgrade -y
Troubleshooting
Video lag on Plex/Jellyfin: Ensure you're using a fast connection and try transcoding the video to a lower resolution for smoother playback.
Steam Link connection issues: Make sure both the Pi and your PC are on the same network and firewall rules allow traffic.
Moonlight not pairing: Verify that NVIDIA GameStream is enabled on your PC.
With this setup, you'll have a fully functional home server for both media and game streaming on your Raspberry Pi!
sudo apt update && sudo apt upgrade -y
Troubleshooting
Video lag on Plex/Jellyfin: Ensure you're using a fast connection and try transcoding the video to a lower resolution for smoother playback.
Steam Link connection issues: Make sure both the Pi and your PC are on the same network and firewall rules allow traffic.
Moonlight not pairing: Verify that NVIDIA GameStream is enabled on your PC.
With this setup, you'll have a fully functional home server for both media and game streaming on your Raspberry Pi!

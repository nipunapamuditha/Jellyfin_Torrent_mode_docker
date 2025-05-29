# Jellyfin with qBittorrent

A Docker Compose setup for running a custom Jellyfin media server with integrated qBittorrent for downloading content.

## Overview

This project combines:
- **Jellyfin**: A free, open-source media server
- **qBittorrent**: A BitTorrent client with web interface

Both services are preconfigured to work together, sharing the same media directory for seamless content management.

## Custom Code Repositories

This project uses custom-modified versions of Jellyfin with integrated torrenting capabilities:

- **Frontend Modifications**: [jellyfin-torrent-integrator_frontEnd-mod](https://github.com/nipunapamuditha/jellyfin-torrent-integrator_frontEnd-mod)
  - Custom Jellyfin UI with integrated torrent search and management features
  
- **Backend Modifications**: [jellyin_torrenting_backend](https://github.com/nipunapamuditha/jellyin_torrenting_backend-)
  - Backend service to handle integration between Jellyfin and qBittorrent
  - API endpoints for torrent management

These modifications allow for searching, adding, and managing torrents directly from the Jellyfin interface.

## Prerequisites

- Docker and Docker Compose installed
- Sufficient storage space for your media files


## Quick Start

1. Clone this repository
2. Adjust media paths in `docker-compose.yml` if needed
3. Run the containers:

```bash
docker-compose up -d
```

## Access Your Services

- **Jellyfin**: http://localhost:8096
- **qBittorrent**: http://localhost:8099

## Configuration Details

### Volume Mounts

Both containers share these key directories:
- `/home/nipuna/Personal_Projects:/media` - Main media storage location
- `./config` - Jellyfin configuration
- `./cache` - Jellyfin cache
- `./temp` - Temporary processing files

### Port Mappings

- Jellyfin: 8096 (HTTP), 8920 (HTTPS), 1900 (DLNA discovery)
- qBittorrent: 8099 (WebUI), 6881 (BitTorrent)

## Usage

1. Access Jellyfin at http://localhost:8096 and set up your media libraries
2. Access qBittorrent at http://localhost:8099 to configure and manage downloads
3. Configure qBittorrent to save downloads to appropriate media folders
4. Jellyfin will automatically discover new media as it's downloaded


## Notes

- This setup uses custom Docker images: `nipunak/jellyfin-torrent` and `nipunak/qbittorrent-custom`
- qBittorrent WebUI authentication is disabled by default (intended for local networks)
- Both containers are configured to restart automatically unless manually stopped

## Troubleshooting

If you encounter issues:
- Check container logs with `docker-compose logs jellyfin` or `docker-compose logs qbittorrent`
- Verify correct file permissions on media directory
- Ensure ports aren't already in use by other services
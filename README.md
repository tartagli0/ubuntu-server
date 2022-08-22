# Background
These are notes based on issues or difficulties I encountered while configuring services on [Ubuntu Server 22.04 LTS](https://ubuntu.com/download/server).

# Plex Media Server
[Plex Media Server](https://www.plex.tv/media-server-downloads/#plex-media-server) can be installed on Linux-based distros by activating the Plex repository. The [official documentation](https://support.plex.tv/articles/235974187-enable-repository-updating-for-supported-linux-server-distributions/) requires adjustments for Ubuntu 22.04.

The `apt-key` utility used in the **DEB-based distros** section of the official Plex documentation is [deprecated](https://manpages.ubuntu.com/manpages/impish/man8/apt-key.8.html) beginning with [Ubuntu 21.10](https://ubuntu.com/blog/ubuntu-21-10-has-landed). Use the following steps instead:
1. Download the Plex repository's signed GPG key:
```bash
sudo curl -o /etc/apt/keyrings/plexmediaserver.asc \
  https://downloads.plex.tv/plex-keys/PlexSign.key
```
2. Add the Plex repository as an APT data source (see the man pages for [apt-key](https://manpages.ubuntu.com/manpages/jammy/man8/apt-key.8.html) and [sources.list](https://manpages.ubuntu.com/manpages/jammy/man5/sources.list.5.html) for reference):
    1. Create the file `/etc/apt/sources.list.d/plexmediaserver.sources`.
    
    2. Add the lines:
    ```bash
    Types: deb
    URIs: https://downloads.plex.tv/repo/deb
    Suites: public
    Components: main
    Signed-By: /etc/apt/keyrings/plexmediaserver.asc
    ```
3. Install Plex Media Server:
```bash
sudo apt update
sudo apt install plexmediaserver
```
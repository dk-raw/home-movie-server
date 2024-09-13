# Home Movie Server
Replacement for $60 a month worth of streaming services subscriptions running on your own hardware using Docker!

# Requirements
1. x86 or ARM based computer (old laptop, pc or anything really)
2. a usable amount of internal or external storage (1tb is good for a start)
3. a usb stick

> [!NOTE]  
> The more storage, the more movies and series you can store and stream at the same time


# Set up
1. Download Debian 12 from https://www.debian.org/distrib/
> [!CAUTION]
> Do not install a Desktop with Debian!
3. Flash it on the usb stick using https://rufus.ie/en/
4. Install Debian on the server and update repositories
5. Install OpenMediaVault following this guide https://docs.openmediavault.org/en/latest/installation/on_debian.html
6. Enable OMV plugins and install docker-compose
7. (optional) If you have another drive for the storage, mount it with the `Storage` menu
> [!IMPORTANT]  
> If you wish to use an array of disks, you are on your own. I had troubles using mergefs with docker
8. Create a new user named `docker` that has access to docker
9. Create 5 shared folders `backup`, `data`, `compose`, `movies` and `series`
10. Make sure user `docker` has read/write access to all
11. Add the first 3 shared folders respectively to the Docker Compose settings under `Services`
12. Find out the UID and GID of the `docker` user (you might need to ssh to the server)
13. Grab the `docker-compose.yml` file from this repo and replace the `PUID` and `PGID` everywhere with the one of your `docker` user
14. Find out the absolute path of the `data` shared folder in the shared folders menu and copy it
15. In the `docker-compose.yml` file replace all instances of `/path/to/data/folder` with the absolute path
16. Replace the timezone `TZ` everywhere on the file with your own. The list is here https://docs.diladele.com/docker/timezones.html
17. Sign up on https://www.plex.tv/sign-up/
18. Visit https://www.plex.tv/claim/ copy the token and replace `xxxxxxx` with it on the compose file
19. Under services, compose, files add a new one and paste the edited compose file. Name it as you wish and Save it
20. Click it and click the `up` icon to start all the containers

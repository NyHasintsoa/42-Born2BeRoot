# Server Configuration

## Apt Sources Configuration

Go to the file to update

```bash
cd /etc/apt
nano sources.list
```

Update the content to be appropriate to the version of debian

```ini
# deb cdrom:[Debian GNU/Linux 12.9.0 _Bookworm_ - Official amd64 DVD Binary-1 with firmware 20250111-10:55]/ bookworm contrib main non-free-firmware

deb https://ftp.debian.org/debian/ bookworm contrib main non-free non-free-firmware
# deb-src https://ftp.debian.org/debian/ bookworm contrib main non-free non-free-firmware

deb https://ftp.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware
# deb-src https://ftp.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware

deb https://ftp.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware
# deb-src https://ftp.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware

deb https://ftp.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware
# deb-src https://ftp.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware

deb https://security.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
# deb-src https://security.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
```
Update command to update sources to apt, update all packages

```bash
sudo apt update
sudo apt upgrade
```
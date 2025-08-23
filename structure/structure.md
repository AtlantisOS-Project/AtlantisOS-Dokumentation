# Structure of AtlantisOS
## Main System
1. `bootloader.img` → bootloader (`Grub`) and some extra tools for Grub
2. `system.img` → the full system, based on Ubuntu (RO, two copies)
3. `desktop.img` → the desktop for the system (`Gnome`, `Kde`, `XFCE`, `Mate`) (RO, two copies)
4. opt: `app-base.img` → the base for the app-container → `squashfs` RO
5. `app-container.img` → the main Container for all User Apps, managed by ATL → RW

### Location
- `bootloader.img` installed to a partition
- all the other images are mounted dynamic

#### Images

- `system_a.img` → `/atlantis/system/system_a.img`
- `system_b.img` → `/atlantis/system/system_b.img`
- `desktop_a.img` → `/atlantis/system/desktop_a.img`
- `desktop_b.img` → `/atlantis/system/desktop_b.img`
- `app-base.img` → `/atlantis/app/app-base.img`
- `app-container.img` → `/atlantis/app/app-container.img`

#### Main system
- Update Cache → `/atlantis/cache/system/` → new `system.img`, `bootloader.img`, `desktop_${NAME}.img`
- `atlantis.conf` → Config for the images (`/boot/atlantis.conf`) → backup: `/atlantis/system/atlantis.conf`

#### App-Container
- App Config → `/atlantis/app/conf/app-install.conf`
- Usage App-Base → `/atlantis/app/conf/app-base.conf`
- `atl` → `/atlantis/atl/`
- main configfile for `atl` → `/atlantis/atl/atl.conf`
- `atl` App-Whiteliste → standard tools and some system apps → `/atlantis/atl/app/system-whitelist.conf`, `/atlantis/atl/app/system-blacklist.conf`
- Container name: **`atl-app`**

#### Filesystem
- `/etc` → RW → Symlink: `/atlantis/etc`
- `/var` → RW → Symlink: `/atlantis/var`
- `/home` → RW → Symlink: `/atlantis/home`

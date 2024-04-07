# Linux Foundation's Introduction to Linux Course
## 1. The Linux Foundation
There are broadly speaking three main families of Linux Distributions.
1. Red Hat based: Including CentOs and Fedora
2. Suse based: Including OpenSuse and SLES
3. Debian based: Including Ubuntu and Linux Mint

### The Red Hat Family
- Fedora is used as a testing bed for Red Hat Enterprise Linux.
- CentOS is a close clone of Red Hat Enterprise Linux (RHEL)
- Uses the RPM based DNF package manager

### The Suse Family
- Suse Linux Enterprise Serve (SLES) and OpenSuse have a similar relationship as RHEL and Fedora
- SLES is widely used in retail and other sectors
- Uses the RPM based zypper package manager
- Includes YAST (Yet another setup tool) for sysadmin purposes

### The Debian Family
- Significantly bigger repository of software than either the Red Hat or the Suse families
- A pure open source project with no ties to any corporation
- A focus on stability
- Uses the DPKG-based APT package manager

## 2. Linux Philosophy and Concepts

- Linux was created in the mid 90s
- In 1998 major companies Oracle and IBM announced their support
- It is currently used on 96% of webservers and most smartphones through Android

## 3. Linux Basics and System Startup
- BIOS stands for Basic Input Output System
- The BIOS first initialised the hardware including the screen and keyboard and tests the memory
  - This is called: "Power on self test" or POST
  - The BIOS is stored on a ROM (Read only memory) chip on the motherboard
- After the BIOS is finished, the remainder of the boot process is controlled by the operating system
- Once the POST is completed the system control is passed to the boot loader

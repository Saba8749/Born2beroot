# Born2beRoot

*This project has been created as part of the 42 curriculum by segribas.*

## Description

Born2beRoot is a system administration project focused on virtualization and server configuration. A Debian virtual machine is set up with encrypted partitions, strict security policies, and automated monitoring.
## Instructions

### Requirements
* VirtualBox
* Debian 13 ISO

### Setup Steps
1. Create VM with encrypted LVM partitions
2. Configure sudo with logging and restrictions
3. Set up SSH on port 4242 (root login disabled)
4. Configure UFW firewall (only port 4242 open)
5. Implement password policy
6. Create monitoring script (`/home/segribas/monitoring.sh`)
7. Set up cron job (every 10 minutes from boot)

### Evaluation
* VM must boot without snapshots
* Signature in `signature.txt` must match VM disk
* Demonstrate all configurations during defense
## Operating System Choice

**Debian** was chosen for:
* Beginner-friendly with excellent documentation
* Large community support
* Stable and reliable for servers
* Simple package management with apt

**Debian vs Rocky:**
* Debian: Community-driven, apt package manager, AppArmor
* Rocky: Enterprise RHEL-based, dnf package manager, SELinux

## Main Design Choices

### Partitioning
* `/boot` (955M, unencrypted) - Required for bootloader
* Encrypted LVM:
  * root (7.5G)
  * swap (1G) 
  * home (10.5G)

### Security Policies
* Password expires after 30 days, minimum 2 days between changes
* Passwords require 10+ chars, uppercase, lowercase, and digits
* sudo limited to 3 attempts, all commands logged
* SSH on port 4242 only, root login disabled
* UFW firewall active (only port 4242 open)

### User Management
* User `segribas` in groups: `sudo`, `user42`
* Principle of least privilege

### Services
* SSH (port 4242)
* UFW firewall
* AppArmor security module
* Monitoring script (runs every 10 minutes via cron)

## Comparisons

**AppArmor vs SELinux:** AppArmor is path-based and simpler (Debian default). SELinux is label-based and more complex (Rocky default).

**apt vs aptitude:** apt is simpler and faster. aptitude has text UI and better dependency resolution.

**UFW vs firewalld:** UFW is simple iptables frontend (Debian). firewalld is zone-based and dynamic (Rocky).

**VirtualBox vs UTM:** VirtualBox is cross-platform and mature. UTM is macOS-focused with Apple Silicon support.

---

**Author:** segribas | **School:** 42 Heilbronn

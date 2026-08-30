# Headley Lab — What I Built and Lessons Learned

## Overview

I built Headley Lab to turn certification study into practical experience.

Instead of only memorizing commands and definitions, I used Windows 11 Pro, Hyper-V, Windows Server, Ubuntu Linux, Raspberry Pi OS, and my home network to practice installation, administration, networking, security, troubleshooting, recovery, automation, and documentation.

My normal workflow is:

**Plan → Build → Test → Troubleshoot → Verify → Document**

I create checkpoints before risky virtual machine changes, make one change at a time, verify results with commands or management tools, and document both successful and unsuccessful outcomes.

---

## Virtualization and Windows Administration

- Configured Hyper-V on Windows 11 Pro.
- Created and managed Windows 11, Windows Server, and Ubuntu virtual machines.
- Used Hyper-V checkpoints before configuration changes and troubleshooting exercises.
- Practiced Windows administration with Task Manager, Services, Event Viewer, Task Scheduler, Device Manager, Disk Management, Windows Recovery Environment, Microsoft Defender, Windows Firewall, local users, permissions, and PowerShell.
- Created scheduled maintenance tasks for Defender updates and scans, DISM health checks, file-health checks, backup reminders, and system monitoring.
- Enabled PowerShell transcription so administrative commands could be reviewed later.
- Applied least privilege by removing unnecessary administrative access and verifying account configuration.

---

## Active Directory, DNS, and Domain Administration

- Installed Active Directory Domain Services and DNS on Windows Server.
- Created a Windows Active Directory domain.
- Configured a domain controller and Windows client on an isolated lab network.
- Joined Windows clients to the domain and authenticated using domain accounts.
- Created administrator and standard-user accounts for permission and policy testing.
- Worked with DNS forward and reverse lookup zones, domain name resolution, account permissions, password policy, and Remote Desktop access.
- Practiced the difference between local and domain accounts.
- Learned how DNS affects domain authentication, Group Policy, and access to network resources.

---

## Networking and Infrastructure

- Built and administered a centrally managed network using a dedicated gateway, managed multi-gigabit switching, Power over Ethernet, and wired wireless access points.
- Configured DHCP reservations for important infrastructure devices.
- Worked with VLAN segmentation, tagged uplinks, access ports, subnetting, and controlled communication between trusted and IoT devices.
- Created an IoT VLAN with restricted access to the primary LAN.
- Allowed only required DNS traffic from the IoT VLAN to the centralized DNS server over TCP and UDP port 53.
- Deployed Pi-hole as a centralized DNS filtering service for devices across multiple network segments.
- Enabled dual-stack IPv4 and IPv6 networking.
- Configured IPv6 prefix delegation, Router Advertisements, SLAAC, and RDNSS.
- Assigned the Pi-hole server a stable IPv6 address for consistent DNS resolution.
- Worked with ICMPv6 and Neighbor Discovery while validating IPv6 connectivity.
- Used separate trusted, guest, and IoT wireless networks.
- Investigated WPA3 compatibility problems and used WPA2 where device support required it.
- Used a Wi-Fi analyzer to evaluate signal conditions and improve access-point placement.
- Installed Ethernet cabling and wired backhaul for wireless access points.

---

## DNS and IPv6 Troubleshooting

- Used `ipconfig`, `ping`, `nslookup`, `tracert`, `pathping`, `netstat`, `dig`, `tcpdump`, and `Test-NetConnection` to isolate network problems.
- Diagnosed a Windows client that received an APIPA address and corrected its IPv4 and DNS configuration.
- Learned to troubleshoot networking in layers: addressing, local connectivity, routing, DNS, ports, services, firewall rules, and applications.
- Diagnosed an IPv6 issue where the client could successfully ping the Pi-hole server but DNS queries over IPv6 timed out.
- Verified that Pi-hole could resolve DNS locally over IPv6 using `dig`.
- Used `tcpdump` to confirm that IPv6 DNS requests were reaching the Linux server.
- Used `Test-NetConnection` to confirm that TCP port 53 was blocked even though ICMPv6 connectivity worked.
- Reviewed UFW and nftables firewall rules and identified missing IPv6 DNS permissions.
- Added IPv6 TCP and UDP port 53 firewall rules for the local IPv6 prefix.
- Verified successful end-to-end IPv6 DNS resolution using `nslookup`, `Test-NetConnection`, Pi-hole query logs, and packet captures.
- Learned that successful IPv6 connectivity does not automatically mean an IPv6 application or service is reachable.

---

## Remote Administration

- Used Remote Desktop to access Windows systems and verified account, service, and firewall requirements.
- Configured Windows Remote Management and PowerShell Remoting.
- Installed and used OpenSSH on Linux systems.
- Configured SSH public-key authentication for remote Linux administration.
- Connected to Linux systems from Windows Terminal and used SSH for command-line administration and file work.
- Learned to verify remote access by checking reachability, listening ports, firewall rules, service status, and user authorization instead of assuming the remote tool itself was broken.

---

## Linux Administration and Scripting

- Practiced Linux navigation, file creation, copying, moving, deletion, permissions, package management, networking, processes, and services.
- Used commands including `ls`, `cd`, `mkdir`, `cp`, `mv`, `rm`, `chmod`, `ip`, `dig`, `nslookup`, `curl`, `ps`, `top`, `systemctl`, `apt`, and `tcpdump`.
- Learned the difference between a process snapshot with `ps` and live monitoring with `top`.
- Used `systemctl status` to investigate services before restarting them.
- Created Bash scripts using variables, user input, conditionals, loops, command substitution, output redirection, and error redirection.
- Created and executed storage and system-check scripts.
- Practiced making scripts executable with `chmod`.
- Learned that interface display commands show state, while commands such as `ip link set` change interface configuration.

---

## ARM Linux Home Server

- Deployed and administered a Raspberry Pi 5 Linux server.
- Configured network-wide DNS filtering, shared storage, automated backups, remote administration, and service monitoring.
- Configured SSH public-key authentication from Windows.
- Created a local SSH host shortcut for easier administration.
- Verified storage mounts, system services, kernel logs, and system health.
- Investigated a firmware warning and confirmed that the system had no undervoltage or thermal throttling.
- Updated the Raspberry Pi EEPROM bootloader, rebooted the system, and verified the completed firmware update.
- Configured a stable IPv6 address for network services.
- Reviewed UFW, nftables, and service listeners while troubleshooting IPv6 DNS.

---

## Security, Malware Response, and Recovery

- Practiced Microsoft Defender scans, Windows Firewall review, Controlled Folder Access testing, protection history review, and offline scanning concepts.
- Performed a simulated malware-removal workflow: identify symptoms, isolate the system, remediate and scan, update antimalware protection, schedule future scans and updates, restore recovery settings, create a clean restore point, and educate the user.
- Practiced the difference between quarantine, removal, recovery, and rebuilding.
- Learned that after a serious compromise, a reset, reimage, or clean installation may be safer than attempting to trust the existing installation.
- Investigated Defender detections inside Hyper-V backup archives and verified that the detections were associated with backed-up virtual machine files rather than immediately assuming the host had an active infection.
- Practiced least privilege, MFA, password-manager use, and hardware-backed authentication.

---

## Storage, Backup, and Recovery

- Worked with Windows backup locations, restore points, recovery options, virtual disks, and system-image concepts.
- Practiced the correct order for preparing a new disk: initialize it, create a volume, assign a drive letter, format it, label it, and verify it.
- Used Windows Recovery Environment to identify Startup Repair, Startup Settings, System Restore, Command Prompt, and other recovery options.
- Learned that System Restore is not a complete file backup.
- Practiced disabling and recreating restore points during malware-remediation scenarios.
- Deployed a Raspberry Pi 5 Linux server providing shared storage and automated backup functions.
- Verified storage mounts, file access, and service availability after configuration changes.

---

## Troubleshooting Results and Failures

Not every lab ended with a clean fix, and I documented those results instead of pretending otherwise.

- Fixed an APIPA and DNS problem that prevented a Windows client from communicating correctly with the Active Directory domain.
- Learned that a client can have basic IP connectivity while DNS or domain services are still broken.
- Confirmed that incorrect DNS settings can cause domain login, Group Policy, and network-resource failures.
- Learned that the HOSTS file can override DNS and that flushing the DNS cache does not remove a bad HOSTS entry.
- Practiced NTFS and share permissions and learned that network access is controlled by the most restrictive effective combination.
- Troubleshot Windows Sandbox errors by checking Windows features, services, system files, containers, and related configuration. The issue remained unresolved, but the process improved my ability to document attempted fixes and stop making random changes.
- Investigated Windows activation and virtual-machine licensing issues and learned to separate licensing problems from operating-system or network problems.
- Diagnosed an IPv6 DNS failure by proving connectivity first, then testing the DNS service, port access, packet flow, and firewall rules until the root cause was identified.
- Learned that packet capture can show whether a failure exists on the client, network path, host firewall, or application layer.

---

## HeadleyLab.com Portfolio Deployment

- Purchased and configured the `headleylab.com` domain.
- Created a public GitHub repository for the portfolio.
- Deployed the site using GitHub Pages.
- Configured DNS records for the root domain and `www`.
- Corrected custom-domain and HTTPS issues until the site worked properly.
- Organized the site into sections for projects, lessons learned, completed labs, certifications, screenshots, and technical experience.
- Used Git and GitHub as both version control and public documentation of technical work.

---

## Main Lessons Learned

1. **DNS is foundational.** A system can have working IP connectivity and still fail authentication, name-based access, or application communication because DNS is wrong.

2. **Troubleshoot one layer at a time.** Check addressing, connectivity, routing, name resolution, ports, services, firewall rules, permissions, and the application in order.

3. **IPv6 requires service-level testing.** Successful ICMPv6 connectivity does not prove that DNS, web services, or other application ports are allowed.

4. **Packet capture is one of the fastest ways to isolate a network problem.** It can show whether traffic reaches the destination and whether a response leaves.

5. **Create a checkpoint before risky changes.** Recovery is part of administration, not an afterthought.

6. **Verification matters more than clicking.** Commands, logs, packet captures, service status, account context, and repeat tests provide evidence that a configuration actually works.

7. **Least privilege reduces risk.** Administrative access should be used only when necessary.

8. **Security includes deciding whether a system is still trustworthy.** Sometimes removal is enough; sometimes rebuilding is the safer option.

9. **A failed lab still produces useful evidence.** Recording symptoms, attempted fixes, errors, and the final state is better than hiding an unresolved problem.

10. **Documentation turns practice into experience.** Screenshots, commands, diagrams, packet captures, Git commits, and lessons learned make technical work explainable during an interview.

---

## Current Status and Next Steps

Completed work includes Hyper-V virtualization, Windows and Linux administration, Active Directory and DNS, remote administration, scripting and automation, Raspberry Pi server deployment, managed switching, VLAN segmentation, Pi-hole DNS filtering, IPv4 and IPv6 networking, wireless deployment, security exercises, backup and recovery practice, network troubleshooting, and deployment of headleylab.com.

Planned next steps include expanding the lab with additional infrastructure and redundancy:

- Deploy a dedicated mini PC as a router/firewall platform to gain more hands-on experience with routing, firewall policy, VLANs, and network services.
- Add a secondary DNS service on separate hardware to provide DNS redundancy if the primary Pi-hole server becomes unavailable.
- Build out a dedicated NAS for centralized storage, backups, and file sharing.
- Convert an existing laptop to Linux for additional daily-use Linux administration, networking, scripting, and troubleshooting practice.
- Continue expanding IPv6 and VLAN design across additional network segments.
- Document routing, ACL, firewall, and DNS behavior in more detail.
- Add network diagrams, packet-capture examples, and dedicated project pages for the strongest infrastructure projects.
- Repurpose the current router as a separate lab router on its own VLAN or isolated network segment for routing, firewall, NAT, DHCP, VPN, and troubleshooting practice without disrupting the primary network.

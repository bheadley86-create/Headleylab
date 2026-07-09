# Headley Lab — What I Built and Lessons Learned

## Overview

I built Headley Lab to turn certification study into practical experience. Instead of only memorizing commands and definitions, I used Windows 11 Pro, Hyper-V, Windows Server, Ubuntu Linux, and my home network to practice installation, administration, security, troubleshooting, recovery, and documentation.

My normal workflow became: **Plan → Do → Verify → Explain**. I created checkpoints before risky VM changes, changed one item at a time, verified the result with a command or management tool, and documented what worked or failed.

## Virtualization and Windows Administration

- Configured Hyper-V on Windows 11 Pro.
- Created and managed two Windows 11 virtual machines, an Ubuntu virtual machine, and a Windows Server virtual machine.
- Used Hyper-V checkpoints before configuration changes and troubleshooting exercises.
- Practiced Windows administration with Task Manager, Services, Event Viewer, Task Scheduler, Device Manager, Disk Management, Windows Recovery Environment, Defender, Windows Firewall, local users, permissions, and PowerShell.
- Created scheduled maintenance tasks for Defender updates and scans, DISM health checks, file-health checks, and backup reminders.
- Enabled PowerShell transcription so administrative commands could be reviewed later.
- Applied least privilege by removing an unnecessary administrator account and confirming that the built-in Administrator account was disabled.

## Active Directory, DNS, and Domain Administration

- Installed Active Directory Domain Services and DNS on Windows Server.
- Created the **batcave.local** domain.
- Configured the domain controller at **10.10.10.10** and a Windows client at **10.10.10.20**.
- Joined Windows clients to the domain and signed in using domain accounts.
- Created and tested accounts such as Batman and Joker for administrator and standard-user scenarios.
- Worked with DNS forward and reverse lookup zones, domain name resolution, account permissions, password policy, and Remote Desktop access.
- Practiced the difference between local accounts and domain accounts and learned how DNS affects domain authentication, Group Policy, and access to network resources.

## Networking and Connectivity Troubleshooting

- Used `ipconfig`, `ping`, `nslookup`, `tracert`, `pathping`, `netstat`, and `Test-NetConnection` to isolate connectivity problems.
- Diagnosed a Windows client that received an APIPA address and corrected its static IPv4 and DNS configuration.
- Learned to test the network in layers: IP configuration, local connectivity, gateway or route, DNS resolution, service port, and application.
- Configured DHCP reservations for important devices on my home network.
- Worked with a TP-Link Wi-Fi 7 router, Deco access points, and an Omada managed switch.
- Used separate primary, guest, and IoT wireless networks and practiced device isolation and Wi-Fi security settings.
- Investigated WPA3 compatibility problems and used WPA2 where device support required it rather than leaving devices unable to connect.
- Reviewed VLAN and subnetting concepts as the next stage of network segmentation without claiming they were already fully deployed.

## Remote Administration

- Used Remote Desktop to access Windows systems and verified account and firewall requirements.
- Configured Windows Remote Management and PowerShell Remoting, including TrustedHosts where required, and successfully opened remote PowerShell sessions.
- Installed and used OpenSSH on Ubuntu.
- Connected to Ubuntu through SSH from Windows Terminal and used the SSH session for command-line administration and file work.
- Learned to verify remote access by checking reachability, the listening port, firewall rules, service status, and user authorization instead of assuming the remote tool itself was broken.

## Linux Administration and Scripting

- Practiced Linux navigation, file creation, copying, moving, deletion, permissions, package management, networking, processes, and services.
- Used commands including `ls`, `cd`, `mkdir`, `cp`, `mv`, `rm`, `chmod`, `ip`, `dig`, `nslookup`, `curl`, `ps`, `top`, `systemctl`, and `apt`.
- Learned the difference between a process snapshot with `ps` and live monitoring with `top`.
- Used `systemctl status` to investigate services before restarting them.
- Created Bash scripts using variables, user input, conditionals, `for` loops, `while` loops, command substitution, output redirection, and error redirection.
- Created and executed a storage-check script and practiced making scripts executable with `chmod`.
- Learned that interface display commands only show status, while `ip link set <interface> up` changes the interface state.

## Security, Malware Response, and Recovery

- Practiced Microsoft Defender scans, Windows Firewall review, Controlled Folder Access testing, protection history review, and offline scanning concepts.
- Performed a simulated CompTIA malware-removal scenario: identify symptoms, isolate the computer, disable System Restore, remediate and scan, update antimalware protection, schedule future scans and updates, re-enable System Restore, create a clean restore point, and educate the user.
- Decided that after a serious infection I would prefer a Windows reset, refresh, reimage, or clean installation when the system could no longer be trusted.
- Practiced the difference between quarantine, removal, recovery, and rebuilding.
- Investigated Defender detections located inside Hyper-V backup archives and confirmed the detections were associated with backed-up VM files rather than blindly assuming the host computer had an active infection.
- Used Bitwarden, MFA, and a YubiKey as part of my personal account-security practices.

## Storage, Backup, and Recovery

- Worked with Windows backup locations, restore points, recovery options, virtual disks, and system-image concepts.
- Practiced the correct order for preparing a new disk: initialize it, create a volume, assign a drive letter, format it, label it, and verify it.
- Used Windows Recovery Environment to identify Startup Repair, Startup Settings, System Restore, Command Prompt, and other recovery options.
- Learned that System Restore is not a complete file backup and that restore points may need to be disabled during malware remediation and recreated afterward.
- Planned a Raspberry Pi 5 NAS project using SSD and HDD storage. The hardware and design work are part of my next phase and are not listed as a completed NAS deployment yet.

## Troubleshooting Results and Failures

Not every lab ended with a clean fix, and I documented those results instead of pretending otherwise.

- Fixed an APIPA and DNS problem that prevented a Windows client from communicating correctly with the BATCAVE domain.
- Learned that a client can have basic IP connectivity while DNS or domain services are still broken.
- Confirmed that incorrect DNS settings can cause domain login, Group Policy, and network-resource failures.
- Learned that the HOSTS file can override DNS and that flushing the DNS cache does not remove a bad HOSTS entry.
- Practiced NTFS and share permissions and learned that access over the network is controlled by the most restrictive effective combination.
- Troubleshot Windows Sandbox errors `0x80070003` and `0x80070002` by checking Windows features, services, system files, containers, and related settings. The issue remained unresolved, but the process improved my ability to document attempted fixes and stop making random changes.
- Investigated Windows activation and VM licensing issues and learned to separate licensing problems from operating-system or network problems.

## HeadleyLab.com Portfolio Deployment

- Purchased and configured the **headleylab.com** domain.
- Created a public GitHub repository and added the initial `index.html` and `README.md`.
- Deployed the site with GitHub Pages.
- Configured the required GoDaddy DNS A records and the `www` CNAME record.
- Corrected custom-domain and DNS issues until both the root domain and HTTPS worked.
- Began organizing the site into sections for the homelab, networking, security, certifications, and individual projects.
- Used Git and GitHub as both version control and proof that I can document technical work publicly.

## Main Lessons Learned

1. **DNS is foundational.** A machine can ping an IP address and still fail domain login, Group Policy, or name-based access because DNS is wrong.
2. **Troubleshoot one layer at a time.** Check configuration, connectivity, name resolution, ports, services, permissions, and the application in order.
3. **Create a checkpoint before making risky changes.** Recovery is part of administration, not an afterthought.
4. **Verification matters more than clicking.** I use commands, logs, service status, account context, and repeat tests to prove the final state.
5. **Least privilege reduces risk.** Administrator rights should be used only when necessary.
6. **Security includes deciding whether a system is still trustworthy.** Sometimes removal is enough; sometimes a reset or clean installation is the safer answer.
7. **A failed lab still produces useful evidence.** Recording symptoms, attempted fixes, errors, and the final state is better than hiding an unresolved problem.
8. **Documentation turns practice into experience.** Screenshots, commands, diagrams, Git commits, and lessons learned make the lab explainable during an interview.

## Current Status and Next Steps

Completed work includes the Hyper-V environment, Windows and Ubuntu virtual machines, the BATCAVE Active Directory and DNS lab, Windows and Linux administration practice, remote access, security exercises, backup and recovery practice, home-network administration, and deployment of headleylab.com.

Next steps include improving the site's CSS and JavaScript, adding screenshots and diagrams, creating individual project pages, completing the Raspberry Pi NAS build, and implementing more advanced network segmentation after validating the design safely.

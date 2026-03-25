# OSS Audit — Apache HTTP Server
**Student Name:** Abhilash Singh  
**Registration Number:** 24BCE10706  
**Course:** CSE0002 — Open Source Software | VIT Bhopal University  
**Software Audited:** Apache HTTP Server (Apache License 2.0)  
**Repository:** `oss-audit-24BCE10706`

---

## About This Project

This repository contains the five shell scripts for the Open Source Software Capstone Project — *The Open Source Audit*. The project audits **Apache HTTP Server**, examining its origin story (NCSA patch collection, 1995), Apache License 2.0 (including its patent grant clause), philosophy, Linux footprint, FOSS ecosystem, and a comparison with proprietary and open source alternatives (Nginx, Microsoft IIS).

---

## Repository Contents

| File | Description |
|------|-------------|
| `script1_system_identity.sh` | Displays system info: Apache version, distro, kernel, uptime, user, and Apache License 2.0 details |
| `script2_package_inspector.sh` | Checks if a FOSS package is installed, shows version/metadata, and prints a philosophy note (case statement) |
| `script3_disk_permission_auditor.sh` | Audits system directories and Apache-specific paths: permissions, ownership, and disk usage using a for loop |
| `script4_log_analyzer.sh` | Reads a log file line by line, counts keyword matches, and displays the last 5 matches |
| `script5_manifesto_generator.sh` | Interactively generates and saves a personalised open-source philosophy statement |
| `README.md` | This file |

The project report PDF is submitted separately via the VITyarthi portal.

---

## Environment Requirements

- **OS:** Ubuntu 22.04 LTS or any Debian-based Linux
- **Shell:** Bash (version 4.0+)
- **Dependencies:** `apache2`, `uname`, `whoami`, `uptime`, `dpkg`, `apt-cache`, `ls`, `du`, `grep`, `awk`, `cut`, `date` — install Apache with `sudo apt install apache2`
- **Permissions:** Script 4 requires `sudo` to read `/var/log/apache2/access.log` (owned by root:adm)

---

## Setup Instructions

### Step 1 — Clone the repository
```bash
git clone https://github.com/[your-github-username]/oss-audit-24BCE10706.git
cd oss-audit-24BCE10706
```

### Step 2 — Install Apache (if not already installed)
```bash
sudo apt update && sudo apt install apache2
sudo systemctl start apache2
```

### Step 3 — Make all scripts executable
```bash
chmod +x *.sh
```

---

## Running Each Script

### Script 1 — System Identity Report
Displays system info and Apache license details.
```bash
./script1_system_identity.sh
```
**Expected output:** Apache version, distribution name, kernel, uptime, user info, date/time, and Apache License 2.0 statement.

---

### Script 2 — FOSS Package Inspector
Checks if a package is installed and prints a philosophy note.
```bash
# Inspect apache2 (default)
./script2_package_inspector.sh

# Inspect a specific package
./script2_package_inspector.sh apache2
./script2_package_inspector.sh nginx
./script2_package_inspector.sh python3
```
**Expected output:** Package install status, version, and a philosophy note about the package.

---

### Script 3 — Disk and Permission Auditor
Audits system directories and Apache-specific installation paths.
```bash
./script3_disk_permission_auditor.sh
```
**Expected output:** Formatted table of directories with permissions, owner, group, and size. Also checks `/etc/apache2`, `/etc/apache2/sites-enabled`, `/var/log/apache2`, `/var/www/html`, `/usr/lib/apache2/modules`, and `/usr/sbin/apache2`.

---

### Script 4 — Log File Analyzer
Reads a log file and counts keyword matches. **Apache logs require sudo.**
```bash
# Analyse Apache access log for 404 errors (default)
sudo ./script4_log_analyzer.sh /var/log/apache2/access.log 404

# Analyse Apache error log
sudo ./script4_log_analyzer.sh /var/log/apache2/error.log error

# Search access log for POST requests
sudo ./script4_log_analyzer.sh /var/log/apache2/access.log POST

# Fallback: use syslog
sudo ./script4_log_analyzer.sh /var/log/syslog apache
```
**Expected output:** Match count and the last 5 matching lines.

> **Note:** Apache logs are in group `adm`. Add your user: `sudo usermod -aG adm $USER` (then log out and back in) to read without sudo.

---

### Script 5 — Open Source Manifesto Generator
Interactive — asks three questions and saves a personalised manifesto.
```bash
./script5_manifesto_generator.sh
```
**Follow the prompts:**
1. Enter a tool you use every day (e.g., `Apache`, `bash`, `git`)
2. Enter one word for what open infrastructure means (e.g., `trust`, `stability`)
3. Enter something you would build and share (e.g., `a student portal`)

**Expected output:** A manifesto printed to the terminal and saved as `manifesto_[yourusername].txt`.

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| `Permission denied` on script | Run `chmod +x scriptname.sh` |
| `apache2: command not found` | Install with `sudo apt install apache2` |
| `apache2 -v` returns nothing | Apache may not be running: `sudo systemctl start apache2` |
| Log file not accessible (Script 4) | Use sudo: `sudo ./script4_log_analyzer.sh /var/log/apache2/access.log 404` |
| Empty Apache log (Script 4) | Generate a request first: `curl http://localhost` then re-run Script 4 |
| `dpkg: not found` (Script 2) | Replace `dpkg -l` with `rpm -qa` for RPM-based systems |

---

## License

These scripts are written for educational purposes as part of the VIT Bhopal OSS course. They may be freely used and modified.

---

*VIT Bhopal University | CSE0002 — Open Source Software | Capstone Project*

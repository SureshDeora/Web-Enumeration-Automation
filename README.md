# Web-Enumeration-Automation

A streamlined bash script designed to automate the initial reconnaissance and enumeration phases of a penetration test or bug bounty hunt. This script ties together popular command-line tools to discover subdomains, filter for active hosts, and perform basic port scanning.

## 🚀 Features

- **Automated Directory Structuring:** Automatically creates organized folders for your target to keep scan results tidy.
- **Subdomain Harvesting:** Uses `assetfinder` to quickly gather potential subdomains.
- **Alive Host Probing:** Filters the gathered subdomains with `httprobe` to identify which hosts are actively responding on HTTPS (port 443).
- **Port Scanning:** Passes the live hosts to `nmap` for a rapid initial port scan.
- *(Optional/Commented)*: Built-in hooks for `amass` if you want to expand subdomain discovery.

## 🛠️ Prerequisites

Ensure you have the following tools installed and accessible in your system's `$PATH`:

* [assetfinder](https://github.com/tomnomnom/assetfinder)
* [httprobe](https://github.com/tomnomnom/httprobe)
* [nmap](https://nmap.org/)
* *(Optional)* [amass](https://github.com/owasp-amass/amass) - Currently commented out in the script, but can be uncommented for deeper enumeration.

## 📥 Installation

1. Clone the repository:
   ```bash
   git clone [https://github.com/SureshDeora/Web-Enumeration-Automation.git](https://github.com/SureshDeora/Web-Enumeration-Automation.git)

   Navigate to the directory:

Bash
cd Web-Enumeration-Automation
Make the script executable:

Bash
chmod +x run.sh
💻 Usage
Run the script by passing the target domain as an argument:

Bash
./run.sh example.com
📂 Output Structure
When you run the script against example.com, it generates the following directory structure in your current working directory:

Plaintext
[example.com/](https://example.com/)
└── recon/
    ├── final.txt                 # Final list of raw subdomains
    ├── httprobe/
    │   └── alive.txt             # List of active subdomains (HTTPS)
    └── scans/
        ├── scanned.txt.nmap      # Nmap scan output files
        ├── scanned.txt.gnmap
        └── scanned.txt.xml
⚙️ How It Works (Under the Hood)
Initialization: Checks if a directory for the target domain exists; if not, creates one along with a recon/ subdirectory.

Subdomain Enumeration: Runs assetfinder against the target and greps for the domain to filter out noise.

Probing: Pipes the sorted, unique subdomains into httprobe to check for active connections on port 443, stripping the protocol headers for clean IP/domain lists.

Scanning: Uses nmap -T4 against the active hosts to quickly identify open ports and outputs the results in all formats (-oA).

⚠️ Disclaimer
This tool is intended for educational purposes, bug bounty hunting, and authorized penetration testing only. Do not run this script against targets you do not have explicit permission to test.
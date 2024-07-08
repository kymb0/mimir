
# Mimir Scanner


**mimir**
░▒▓██████████████▓▒░░▒▓█▓▒░▒▓██████████████▓▒░░▒▓█▓▒░▒▓███████▓▒░       
░▒▓█▓▒░░▒▓█▓▒░░▒▓█▓▒░▒▓█▓▒░▒▓█▓▒░░▒▓█▓▒░░▒▓█▓▒░▒▓█▓▒░▒▓█▓▒░░▒▓█▓▒░      
░▒▓█▓▒░░▒▓█▓▒░░▒▓█▓▒░▒▓█▓▒░▒▓█▓▒░░▒▓█▓▒░░▒▓█▓▒░▒▓█▓▒░▒▓█▓▒░░▒▓█▓▒░      
░▒▓█▓▒░░▒▓█▓▒░░▒▓█▓▒░▒▓█▓▒░▒▓█▓▒░░▒▓█▓▒░░▒▓█▓▒░▒▓█▓▒░▒▓███████▓▒░       
░▒▓█▓▒░░▒▓█▓▒░░▒▓█▓▒░▒▓█▓▒░▒▓█▓▒░░▒▓█▓▒░░▒▓█▓▒░▒▓█▓▒░▒▓█▓▒░░▒▓█▓▒░      
░▒▓█▓▒░░▒▓█▓▒░░▒▓█▓▒░▒▓█▓▒░▒▓█▓▒░░▒▓█▓▒░░▒▓█▓▒░▒▓█▓▒░▒▓█▓▒░░▒▓█▓▒░      
░▒▓█▓▒░░▒▓█▓▒░░▒▓█▓▒░▒▓█▓▒░▒▓█▓▒░░▒▓█▓▒░░▒▓█▓▒░▒▓█▓▒░▒▓█▓▒░░▒▓█▓▒░      
                                                                     


# Overview

Mimir Scanner is a comprehensive scanning tool designed to perform an initial sweep using Rustscan, followed by targeted Nmap scans against open ports. Additionally, it performs vulnerability scans using Nuclei and Nikto against web ports (80, 443, 8080, 8443) and includes an SSL scan for enhanced security assessment.

## Features

- **Initial Rustscan Sweep**: Quickly identify open ports across multiple hosts.
- **Targeted Nmap Scans**: Perform detailed scans against identified ports with various Nmap options (stealth, aggressive, vulnerability, comprehensive).
- **Web Port Scans**: Utilize Nuclei and Nikto to scan common web ports for vulnerabilities.
- **SSL Scan**: Perform SSL/TLS assessments using SSLScan.

## Requirements

- Python 3.6+
- aiofiles
- rich

### Installing Dependencies

```sh
pip install aiofiles rich
```

## Installation on Ubuntu EC2

1. **Install Python 3 and pip**:

```sh
sudo apt install python3 python3-pip -y
```

2. **Install Rustscan**:

```sh
curl https://sh.rustup.rs -sSf | sh
source $HOME/.cargo/env
cargo install rustscan
```

3. **Install Nmap, Nikto, and SSLScan**:

```sh
sudo apt install nmap nikto sslscan -y
```

4. **Install Python Dependencies**:

```sh
pip3 install aiofiles rich
```

## Usage

### Initial Scan

Perform an initial scan using Rustscan, followed by targeted Nmap scans, web scans, and SSL scans:

```sh
python3 main.py client_name targets.txt --initial_scan --web --ssl --nmap-all --report-file report.json
```

### Scanning Against Existing Results

If Rustscan results already exist, run specified scans against these results by omitting the `--initial_scan` flag:

```sh
python3 main.py client_name targets.txt --web --ssl --nmap-aggressive --report-file report.json
```

### Full Scan with All Options

Run a full scan with all available options:

```sh
python3 main.py client_name targets.txt --initial_scan --web --ssl --nmap-all --report-file report.json
```

### Aggressive Scan with Web Scanning Against Existing Results

Perform an aggressive and comprehensive Nmap scan and web scans against existing Rustscan results:

```sh
python3 main.py client_name targets.txt --initial_scan --web --ssl --nmap-aggresive --nmap-comprehensive --report-file report.json
```

### Stealth Scan with SSL Scanning

Perform a stealth Nmap scan and SSL scans:

```sh
python3 main.py client_name targets.txt --ssl --nmap-stealth --report-file report.json
```

## Reporting

The scanner consolidates findings from all scans into a comprehensive report, highlighting critical vulnerabilities and providing actionable insights.

## Future Plans

- **Enhanced Reporting**: Include more detailed analysis and visualization options.
- **Additional Scans**: Integrate more scanning tools and scripts for a wider range of assessments.
- **Automated Remediation Suggestions**: Provide guidance on fixing identified vulnerabilities.

## Contribution

Feel free to contribute to the project by submitting issues or pull requests on GitHub.

---

Built with ❤️ by the Mimir Scanner team (kymb0 and chatGPT)

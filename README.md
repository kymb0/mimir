
# Mimir

<pre style="color: red;">
                                
  _ __ (_)_ __ (_)_ _        / ̄ ̄/
 | '  \| | '  \| | '_|      /  / 
 |_|_|_|_|_|_|_|_|_|      <  <  
                            \  \ 
                             \__\
</pre>
                         

- [Overview](#Overview)
- [Features](#Features)
- [Requirements](#Requirements)
- [Installation on Ubuntu EC2](#Installation-on-Ubuntu-EC2)
- [Usage](#Usage)

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


## Installation on Ubuntu EC2

1. **Install Rustscan**:

```sh
sudo snap install rustscan
```

2. **Install Nmap, Nikto, and SSLScan**:

```sh
sudo apt install nmap nikto sslscan -y
```

3. **Install Python Dependencies**:

```sh
sudo apt install python3-full
sudo apt install python3-aiofiles
sudo apt install python3-rich
```
4. Install GOlang and set PATH

```sh
wget https://golang.org/dl/go1.20.5.linux-amd64.tar.gz && sudo tar -C /usr/local -xzf go1.20.5.linux-amd64.tar.gz && echo -e '\n# Go environment variables\nexport GOROOT=/usr/local/go\nexport GOPATH=$HOME/go\nexport PATH=$PATH:$GOROOT/bin:$GOPATH/bin' >> ~/.bashrc && source ~/.bashrc && go version

```

5. Install Nuclei

```sh
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
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
python3 main.py client_name --target-file targets.txt --web --ssl --nmap-aggressive --report-file report.json
```

### Full Scan with All Options

Run a full scan with all available options:

```sh
python3 main.py client_name --target-file targets.txt --initial_scan --web --ssl --nmap-all --report-file report.json
```

### Aggressive Scan with Web Scanning Against Single Host

Perform an aggressive and comprehensive Nmap scan and web scans against existing Rustscan results:

```sh
python3 main.py client_name hostname.com.au --initial_scan --web --ssl --nmap-aggresive --nmap-comprehensive --report-file report.json
```

### Stealth Scan with SSL Scanning

Perform a stealth Nmap scan and SSL scans:

```sh
python3 main.py client_name --target-file targets.txt --ssl --nmap-stealth --report-file report.json
```

## Reporting

The scanner consolidates findings from all scans into a comprehensive report, highlighting critical vulnerabilities and providing actionable insights.

## Future Plans

- **Enhanced Reporting**: Include more detailed analysis and visualization options.
- **Additional Scans**: Integrate more scanning tools and scripts to generate more leads for testers to check manually.
- **Automated Remediation Suggestions**: Provide guidance on fixing identified vulnerabilities.
- **Proxycannon implementation** implement a terraform component to spin up micro instances and routing for network load balancing and IDS/WAF evasion.
- **API to feed results into ML models/AI/`<insert buzzword here>`

## Contribution

Feel free to contribute to the project by submitting issues or pull requests on GitHub.

---

Built with ❤️ by the Mimir Scanner team (kymb0 and chatGPT)

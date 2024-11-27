
# 📝 Proof OF Concept (POC): SharePoint Vulnerability Detection

This repository contains a step-by-step guide to identify SharePoint installations and validate vulnerabilities. The goal is to automate the process of finding vulnerable SharePoint instances and testing them for potential security issues.

## ⌛ Requirements

- **Tools**:  
  - [Subfinder](https://github.com/projectdiscovery/subfinder)  
  - [Httpx](https://github.com/projectdiscovery/httpx)  
  - [Nuclei](https://github.com/projectdiscovery/nuclei)  
  - [wget](https://www.gnu.org/software/wget/)  

---

## 🔍 Steps

### 1. Find Target Subdomains
Use `subfinder` to enumerate subdomains of the target domain. Save the output to a file for further processing.
```bash
subfinder -d target.com -o subdomain_targets.txt
```

### 2. Identify Active SharePoint Instances
Use `httpx` to check for live hosts and store potential SharePoint candidates.
```bash
httpx -l subdomain_targets.txt -o active_sharepoints.txt
```

### 3. Detect SharePoint Technology
Run `nuclei` to confirm if the hosts in the list use SharePoint.
```bash
nuclei -l active_sharepoints.txt -t Exposed-Sharepoint.yaml
```

### 4. Validate Vulnerability
Retrieve the `lists.wsdl` file to check for potential vulnerabilities in SharePoint services.
```bash
wget "https://example.sharepoint.com/_vti_bin/lists.asmx?WSDL" -O lists.wsdl
cat lists.wsdl
```
You can also view FrontPage Configuration Information via (_vti_inf.html)
---

## 📝 Alternative Methods to Identify SharePoint Sites

### Using Search Engines
- **FOFA**:  
  Query: `header="MicrosoftSharePointTeamServices"`

- **Shodan**:  
  Query: `http.title:"Microsoft SharePoint"`

- **ZoomEye**:  
  Query: `app:"Microsoft-SharePoint"`

---

## ⭐ References

Here are real-world examples of SharePoint vulnerabilities reported on HackerOne :

- [HackerOne Report 761617](https://hackerone.com/reports/761617)  
- [HackerOne Report 2180018](https://hackerone.com/reports/2180018)  
- [HackerOne Report 300539](https://hackerone.com/reports/300539)  
- [HackerOne Report 761158](https://hackerone.com/reports/761158)  
- [HackerOne Report 920401](https://hackerone.com/reports/920401)  

---
## ⚠️ Disclaimer

This repository is intended for **educational purposes only**. Use of these exploits on systems or websites without explicit permission is illegal and unethical. The creator is not responsible for any misuse of this information.

## 💰 Support Me  

If you find this work helpful, you can support me:  
- [![Buy Me a Coffee](https://www.buymeacoffee.com/assets/img/custom_images/yellow_img.png)](https://buymeacoffee.com/ghost_sec)  

Thanks for your support! ❤️

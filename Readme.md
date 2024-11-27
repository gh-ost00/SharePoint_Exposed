
# Proof of Concept (POC): SharePoint Vulnerability Detection

This repository contains a step-by-step guide to identify SharePoint installations and validate vulnerabilities. The goal is to automate the process of finding vulnerable SharePoint instances and testing them for potential security issues.

## Requirements

- **Tools**:  
  - [Subfinder](https://github.com/projectdiscovery/subfinder)  
  - [Httpx](https://github.com/projectdiscovery/httpx)  
  - [Nuclei](https://github.com/projectdiscovery/nuclei)  
  - [wget](https://www.gnu.org/software/wget/)  

- **Accounts for Search Engines**:  
  - FOFA  
  - Shodan  
  - ZoomEye  

---

## Steps

### 1. Find Target Subdomains
Use `subfinder` to enumerate subdomains of the target domain. Save the output to a file for further processing.
```bash
subfinder -d target.com -o subdomains.txt
```

### 2. Identify Active SharePoint Instances
Use `httpx` to check for live hosts and store potential SharePoint candidates.
```bash
httpx -l subdomains.txt -o active_sharepoints.txt
```

### 3. Detect SharePoint Technology
Run `nuclei` to confirm if the hosts in the list use SharePoint.
```bash
nuclei -l active_sharepoints.txt -t nuclei-templates/technologies/sharepoint-detection.yaml
```

### 4. Validate Vulnerability
Retrieve the `lists.wsdl` file to check for potential vulnerabilities in SharePoint services.
```bash
wget "https://example.sharepoint.com/_vti_bin/lists.asmx?WSDL" -O lists.wsdl
cat lists.wsdl
```

---

## Alternative Methods to Identify SharePoint Sites

### Using Search Engines
- **FOFA**:  
  Query: `header="MicrosoftSharePointTeamServices"`

- **Shodan**:  
  Query: `http.title:"Microsoft SharePoint"`

- **ZoomEye**:  
  Query: `app:"Microsoft-SharePoint"`

---

## References

Here are real-world examples of SharePoint vulnerabilities reported on HackerOne:

- [HackerOne Report 761617](https://hackerone.com/reports/761617)  
- [HackerOne Report 2180018](https://hackerone.com/reports/2180018)  
- [HackerOne Report 300539](https://hackerone.com/reports/300539)  
- [HackerOne Report 761158](https://hackerone.com/reports/761158)  
- [HackerOne Report 920401](https://hackerone.com/reports/920401)  

---

## Notes
Ensure you have proper authorization before testing any domains. Unauthorized access or testing may violate laws and regulations.

# ZAP Scanning Report – Round 1

Site: http://localhost:8000  
Generated on: 28.11.2025  
ZAP Version: 2.16.1

## Summary of Alerts

| Risk Level    | Number of Alerts |
| ------------- | ---------------- |
| High          | 0                |
| Medium        | 3                |
| Low           | 1                |
| Informational | 1                |

## Alerts

| Name                                         | Risk Level    | Number of Instances |
| -------------------------------------------- | ------------- | ------------------- |
| Content Security Policy (CSP) Header Not Set | Medium        | 3                   |
| Directory Browsing                           | Medium        | 1                   |
| Missing Anti-clickjacking Header             | Medium        | 1                   |
| X-Content-Type-Options Header Missing        | Low           | 2                   |
| User Agent Fuzzer                            | Informational | 12                  |

## Alert Detail

### 1. Content Security Policy (CSP) Header Not Set

Risk level: Medium  

Description:  
The server responses do not include a Content Security Policy header. Without CSP, the application is more exposed to script injection and similar attacks. :contentReference[oaicite:1]{index=1}  

Affected URLs (examples):  
- http://localhost:8000/  
- http://localhost:8000/robots.txt  
- http://localhost:8000/sitemap.xml  

Instances: 3  

Recommendation:  
Configure the web server or application to send a suitable `Content-Security-Policy` header for all pages.

---

### 2. Directory Browsing

Risk level: Medium  

Description:  
It is possible to view a directory listing under the images path. This can expose files such as images, backups, or other resources that should not be directly listed. :contentReference[oaicite:2]{index=2}  

Affected URL:  
- http://localhost:8000/images/  

Evidence:  
The response shows a directory index, including “Parent Directory”.

Instances: 1  

Recommendation:  
Disable directory browsing for this path. If directory listing is required, ensure there are no sensitive or unnecessary files in the directory.

---

### 3. Missing Anti-clickjacking Header

Risk level: Medium  

Description:  
The responses do not include headers that protect against clickjacking. There is no `X-Frame-Options` header or equivalent protection via CSP frame-ancestors. :contentReference[oaicite:3]{index=3}  

Affected URL:  
- http://localhost:8000/  

Parameter mentioned by ZAP:  
- x-frame-options  

Instances: 1  

Recommendation:  
Add either a suitable `X-Frame-Options` header (for example `DENY` or `SAMEORIGIN`) or configure CSP with a `frame-ancestors` directive to control framing.

---

### 4. X-Content-Type-Options Header Missing

Risk level: Low  

Description:  
The responses do not include the `X-Content-Type-Options: nosniff` header. Without this, some browsers may try to MIME-sniff content types, which can increase the risk of certain attacks. :contentReference[oaicite:4]{index=4}  

Affected URLs (examples):  
- http://localhost:8000/  
- http://localhost:8000/images/edblogo.png  

Instances: 2  

Recommendation:  
Set the header `X-Content-Type-Options: nosniff` on all relevant responses.

---

### 5. User Agent Fuzzer

Risk level: Informational  

Description:  
ZAP sent different User-Agent header values and compared the responses. This alert is informational and shows that the application responded to various User-Agent strings during testing. :contentReference[oaicite:5]{index=5}  

Affected URL (example):  
- http://localhost:8000/images  

Parameter:  
- Header User-Agent  

Examples of User-Agent values used:  
- Internet Explorer style user agents  
- Chrome and Firefox user agents  
- Crawler / bot user agents (such as Googlebot, Yahoo, etc.)

Instances: 12  

Recommendation:  
No immediate change is required. If needed, monitor and control how different User-Agent values are handled, and log suspicious patterns.

---

End of ZAP Round 1 report.

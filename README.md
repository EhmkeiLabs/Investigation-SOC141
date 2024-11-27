# Walkthrough: Investigation of SOC141  

## **Objective**  
This lab focuses on identifying and mitigating a phishing attempt involving a suspicious URL accessed within the network. The investigation aims to analyze the behavior of the request, identify associated risks, and recommend measures to prevent similar incidents.

### **Skills Learned**  
- Network traffic analysis and log review.  
- Identification and handling of malicious URLs.  
- Containment and mitigation of potentially compromised systems.  
- Documentation of Indicators of Compromise (IOCs) for proactive threat defense.  

### **Tools Used**  
- Log Management Systems for traffic analysis.  
- Threat Intelligence Platforms (e.g., VirusTotal) to assess domain reputation.  
- Networking tools to trace and isolate malicious connections.  


## **Steps**  

### Introduction  

Details provided:  

![Alert Details](https://i.imgur.com/pU70gyL.png)  

After reviewing the alert summary, it is clear that a phishing URL was sent to the victim.  


### Case Creation  

We create a case to begin investigation:  

![Case Creation](https://i.imgur.com/9Um2fXo.png)  


### **Collection of Data**  

![Alert Collection](https://i.imgur.com/Y8iTImP.png)  

**Questions:**  

1. **Source Address**  
2. **Destination Address**  
3. **User-Agent**  

**Findings:**  

- **Source Address**: `172.16.17.49`  
- **Destination Address**: `91.189.114.8`  
- **User-Agent**:  
  `Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36`  


### **Search Log**  

![Search Log](https://i.imgur.com/e589pAt.png)  

**Question:** Search Log Management for details.  

We searched the **Source IP Address** in the Log Management system and found seven corresponding entries:  

![Log Entry 1](https://i.imgur.com/iWAOEco.png)  
![Log Entry 2](https://i.imgur.com/2qkzqbd.png)  
![Log Entry 3](https://i.imgur.com/pPCRAvr.png)  
![Log Entry 4](https://i.imgur.com/pxYqGTI.png)  

Upon expanding the logs for the **destination address**, we noted the malicious activity timestamps.  


### **Analyze URL Address**  

![URL Analysis](https://i.imgur.com/os6Nf6S.png)  

**Question:** Is the URL malicious?  

Using VirusTotal and Hybrid Analysis to investigate the URL:  
`http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php?email=ellie@letsdefend.io`.  

**VirusTotal Results:**  

![VirusTotal Results](https://i.imgur.com/TuwnQ0m.png)  

The URL is flagged as **Malicious**.  

**Conclusion:**  
We classify the URL as **Malicious** and proceed with the next steps.  


### **Has Anyone Accessed the URL Domain?**  

![Access Details](https://i.imgur.com/81PB9T7.png)  

**Findings:**  

- **Access Time**: `March 22, 2021, 09:23 PM`.  
- **Source IP**: `172.16.17.49`.  
- **Destination IP**: `91.189.114.8`.  
- **User**: Ellie.  
- **User-Agent**:  
  `Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36`.  
- **Blocked**: No.  


### **Containment**  

![Containment Step](https://i.imgur.com/nDQDUFq.png)  

The victim host was immediately isolated:  

![Host Containment](https://i.imgur.com/B9WLTGJ.png)  


### **Submission of Case Artifacts**  

![Case Artifacts Submission](https://i.imgur.com/5vYXfyc.png)  

The following artifacts were submitted:  

1. Indicators of Compromise (IOCs):  
    - **Domain**: `mogagrocol.ru`.  
    - **IP Address**: `91.189.114.8`.  
    - **URL**:  
      `http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php?email=ellie@letsdefend.io`.  


### **Analyst Note**  

The phishing attempt was confirmed as a **true positive**, and appropriate containment measures were implemented. Artifacts were submitted for further analysis and organizational defense improvements.  


### **Close Alert**  

![Close Alert](https://i.imgur.com/qX9n45h.png)  


### **Alert Scorecard**  

We successfully addressed the alert:  

![Alert Scorecard](https://i.imgur.com/zDTxE9A.png)  


## **Summary of Findings**  

The alert flagged a phishing URL accessed by user **ellie** from source IP `172.16.17.49` to destination IP `91.189.114.8`. Analysis revealed that the URL (`http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php?email=ellie@letsdefend.io`) was malicious, associated with campaigns targeting WordPress vulnerabilities. The victim host was contained to prevent further communication with the malicious domain.  

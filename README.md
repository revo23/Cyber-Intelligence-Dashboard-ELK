# Cyber-Fraud-Intelligence-Dashboard-ELK  

<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/5d22db57-3413-4ea4-9e33-462bc87579bf" />  

<img width="400" height="399" alt="image" src="https://github.com/user-attachments/assets/961d96f3-c1e8-4f7e-8f6f-7a8369379c2d" />  



**Overview**  
Configure the abuse.ch integration (via the Elastic Agent) in Data management and tailor it for cyber‑fraud intelligence use‑cases. I’ll also highlight tuning and mapping that are specific to fraud/intel rather than purely malware.  


**Sign up Elastic Cloud**  

**Install Agent on Endpoint**  

**Abuse.ch Integration**  

<img width="1623" height="847" alt="image" src="https://github.com/user-attachments/assets/e9077936-f6c2-41d9-a117-b0e6fb2f3571" />  
get Auth Key from abuse.ch account



**Abuse URLs**  
<img width="1854" height="805" alt="image" src="https://github.com/user-attachments/assets/c3d73b0c-c2d0-4e44-8371-cd0cc850d1d7" />  


Correlate with internal signals: For example, if you see a malicious URL in threat.indicator.url.full and you have a payment attempt that reached that URL/domain, you can escalate.  

Use “indicator match” rules: The built‑in detection rule type Threat Intel IP/URL/Domain indicator match is a strong base. Modify to include your fraud‑relevant data sources.  

Monitoring & dashboards: Use dashboards to track how many indicator matches occur, which accounts/devices are involved, trends over time.  

**References**  
https://www.elastic.co/cloud  

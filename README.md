# Cyber-Intelligence-Dashboard-ELK  

<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/5d22db57-3413-4ea4-9e33-462bc87579bf" />  

<img width="748" height="201" alt="image" src="https://github.com/user-attachments/assets/fb6c7d91-36d4-4339-aab8-7a3bda691b7c" />  

<img width="400" height="399" alt="image" src="https://github.com/user-attachments/assets/961d96f3-c1e8-4f7e-8f6f-7a8369379c2d" />  

**Overview**  

1. Configure the abuse.ch integration (via the Elastic Agent) in Data management and tailor it for cyber‑fraud intelligence use‑cases.  
2. I’ll also highlight mapping that are specific to fraud/intel and example correlations.  

STIX = the message content, TAXII = the delivery mechanism



**Sign up Elastic Cloud**  

**Install Agent on Endpoint**  

<img width="1267" height="467" alt="image" src="https://github.com/user-attachments/assets/5dc1db03-1333-40a4-a087-e37321b5e812" />  



**Abuse.ch Integration**  

Get Auth Key from abuse.ch account and input  

<img width="885" height="792" alt="image" src="https://github.com/user-attachments/assets/3c695aa1-9c90-4232-9a0f-2d58baacf4dd" />  

<img width="1456" height="351" alt="image" src="https://github.com/user-attachments/assets/0ea12259-5adf-4c03-9f7e-272cce768438" />

Indicator lifecycle: The integration supports IoC expiration (via transforms) so you don’t rely on stale data.



**Abused URLs**  

<img width="1854" height="805" alt="image" src="https://github.com/user-attachments/assets/c3d73b0c-c2d0-4e44-8371-cd0cc850d1d7" />  

Correlate with internal signals: For example, if you see a malicious URL in `threat.indicator.url.full` and you have a payment attempt that reached that URL (e.g. x2.ew-w3[.]ru), you can investigate the customer further.  

<img width="1792" height="964" alt="image" src="https://github.com/user-attachments/assets/f0911ca5-2907-4074-88a9-98a9fbcef9fd" />

Use “indicator match” rules: The built‑in detection rule type Threat Intel IP/URL/Domain indicator match is a strong base. Modify to include your fraud‑relevant data sources.  

<img width="1870" height="939" alt="image" src="https://github.com/user-attachments/assets/f104e8ce-522d-42b8-ace4-5b36dcc303ab" />  

<img width="1202" height="692" alt="image" src="https://github.com/user-attachments/assets/2aff26ae-8f62-4b39-8f87-954ffa57ce4f" />  

Monitoring & dashboards: Use dashboards to track how many indicator matches occur, which accounts/devices are involved, trends over time.  

**Credential Leak / Dark Web Exposure**

External signal: threat.indicator.email = "user@example[.]com"

Internal signal: Successful login attempts from unusual geolocation that is not the customer's city/country

**Account Takeover**

External signal: threat.indicator.ip = "185.42.42[.]42"

Internal signal: Multiple failed logins from that IP across different bank accounts due to credential stuffing campaign

**Further work**

Setup MISP (Threat Intel Platform) server for better results

1. Threat feed → Elastic directly (current)

You push indicators (IPs, domains, hashes) straight into Elastic as a Threat Intel index, and use detection rules like “Threat Intel IP/URL/Domain Indicator Match” to detect matches in logs.  

This is simpler, but much more limited:

- You only get raw indicators.

- No correlation between feeds.

- No event context (campaigns, TTPs, threat actor info).

- No sharing / MISP taxonomies / galaxy clusters.

- Harder to manage expiry, deduplication, or trust levels.

2. Threat feed → MISP → Elastic (recommended for most)

```
[Feeds / Sources]
   ↓
[MISP] — enrichment, deduplication, tagging, correlation, sharing
   ↓
[Elastic Security / SIEM] — indicator matching, alerting, dashboards
```

You ingest threat intel feeds (STIX/TAXII, CSV, JSON, etc.) into MISP for enrichment, correlation, and sharing hub, and then forward curated or correlated IOCs to Elastic Security.  

**References**  
https://www.elastic.co/cloud  

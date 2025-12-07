# PRODUCT_SCOPE_V0_V02.md
ThreatFusion — Product Scope Document  
Version: 0.2  
Last Updated: 2025-12-07  
Owner: ThreatFusion Product Team

---

## 1. Product Overview
**ThreatFusion** is an AI-assisted Threat Intelligence Platform (TIP) designed to collect, normalize, enrich, and visualize threat intelligence from multiple sources. It targets SOC teams, MSSPs, and enterprises seeking to proactively detect and respond to cyber threats.

**Key Objectives:**
- Centralize threat intelligence feeds
- Automate enrichment using AI/LLMs
- Provide actionable insights to SOC teams
- Integrate seamlessly with existing security tools

---

## 2. MVP Features (Version 0.1)
1. **Data Collection**
   - OSINT sources: abuse.ch, AlienVault OTX, MalwareBazaar
   - Feed ingestion via API and scheduled tasks
2. **Normalization**
   - Unified IOC schema (JSON)
   - Deduplication and validation
3. **AI Enrichment**
   - Threat summarization
   - Risk scoring
   - Category tagging
4. **Storage**
   - PostgreSQL for structured data
   - Elasticsearch for search and analytics
5. **Dashboard**
   - IOC search, filter, timeline
   - Basic export functionality
6. **API Access**
   - REST endpoints for IOC query and statistics

---

## 3. Version 0.2 Planned Features
1. **Additional Data Sources**
   - Integration with commercial threat intelligence feeds
   - Optional Dark Web monitoring (legal OSINT)
2. **Advanced AI Capabilities**
   - Threat actor attribution
   - Campaign detection
   - Suggested SOC response actions
3. **Enhanced Dashboard**
   - Interactive threat timeline
   - AI-generated threat summaries
   - Custom alert notifications
4. **Automation & Integration**
   - Connectors for SIEM (Splunk, QRadar, Elastic)
   - EDR integration (optional)
5. **Security Enhancements**
   - Role-Based Access Control (RBAC)
   - Audit logging
   - TLS encrypted communication

---

## 4. Out-of-Scope (V0-V0.2)
- Malware sandboxing & dynamic analysis
- Full-scale STIX/TAXII 2.1 server
- Predictive threat modeling
- Direct integration with private/hacked databases
- Automated response & remediation

---

## 5. Target Users
- **SOC Analysts:** Quickly identify and act on relevant threats  
- **Threat Hunters:** Enrich and visualize IOC data for campaigns  
- **MSSPs:** Centralized threat intelligence distribution for clients  
- **Enterprises:** Actionable insights to improve security posture

---

## 6. Success Metrics
1. MVP Ingestion Rate: 1000+ IOCs/day  
2. Enrichment Accuracy: 85%+  
3. Dashboard Query Response: <2 seconds  
4. API Availability: 99% uptime  
5. Integration Completion: At least 2 SIEM/EDR connectors

---

## 7. Deployment Considerations
- Docker-based containers for dev & prod  
- Kubernetes-ready for horizontal scaling  
- Local/offline AI inference for privacy-sensitive environments  
- Configurable feed schedule and retention policies

---

## 8. Roadmap to V1
| Phase | Milestone | Estimated Timeline |
|-------|-----------|-----------------|
| V0.1  | MVP Launch | Month 1-2 |
| V0.2  | AI & Integration | Month 3-5 |
| V0.3  | Dark Web Feed & Alerting | Month 6-8 |
| V1    | Full Platform w/ Graph Explorer | Month 9-12 |

---

## 9. Notes
- Legal compliance must be maintained (no private/hacked data collection)  
- All AI models must have fallback logic for offline or unavailable inference  
- Product should remain modular and extensible for future TIP features  

---


# ARCHITECTURE.md
ThreatFusion — System Architecture Document  
Version: 1.0  
Last Updated: 2025-02-19  
Owner: ThreatFusion Engineering

## 1. Overview
ThreatFusion is a modular Threat Intelligence Platform (TIP) designed to collect, normalize, enrich, and distribute threat intelligence data from OSINT and commercial sources. The platform follows a service-oriented architecture (SOA) optimized for scalability, low operational overhead, and AI-assisted threat analysis.

ThreatFusion consists of five core subsystems:

1. Collector Layer — OSINT & API ingestion  
2. Normalizer & Processing Pipeline — unified IOC schema  
3. AI Enrichment Engine — LLM-based interpretation  
4. Storage Layer — structured and searchable data  
5. UI, API & Integration Layer — Dashboard, REST API, connectors

## 2. High-Level Architecture Diagram (Textual)

```
         ┌──────────────────────────────────────────┐
         │              UI / Dashboard               │
         └───────────────▲───────────────▲──────────┘
                         │               │
                         │               │ REST API
                         │               │
           ┌─────────────┴───────────────┴────────────┐
           │         API Gateway / Backend Service      │
           └─────────────▲───────────────▲────────────┘
                         │               │
                ┌────────┘               └───────────┐
                │                                     │
     ┌──────────┴─────────────┐         ┌────────────┴─────────────┐
     │   Normalizer Pipeline   │         │     AI Enrichment Engine │
     └──────────▲─────────────┘         └────────────▲─────────────┘
                │                                     │
     ┌──────────┴─────────────┐         ┌────────────┴─────────────┐
     │   Collector Services    │         │  Analytics & Correlation  │
     └──────────▲─────────────┘         └────────────▲─────────────┘
                │                                     │
                └──────────────┬───────────┬─────────┘
                               │           │
                        ┌──────┴───┐   ┌───┴──────────┐
                        │ Database │   │ Search Engine │
                        └──────────┘   └──────────────┘
```

## 3. Subsystem Architecture

### 3.1 Collector Layer
Purpose: Ingest raw threat intel from OSINT, TAXII, commercial feeds, and malware repositories.

Components:
- collector-abusech  
- collector-otx  
- collector-threatfox  
- collector-malwarebazaar  
- collector-sdk (plugin framework)

Data Flow:
1. Fetch feed  
2. Convert to internal raw format  
3. Push to message queue → Normalizer pipeline

Tech Choices:
- Python FastAPI  
- Scheduler (Celery or APScheduler)

### 3.2 Normalizer & Processing Pipeline
Purpose: Convert heterogeneous IOC formats into a unified schema.

Unified IOC Schema Example:
```json
{
  "indicator": "1.2.3.4",
  "type": "ip",
  "threat_family": "c2",
  "confidence": 75,
  "source": "abuse.ch",
  "first_seen": "2025-02-19T08:00:00Z",
  "tags": ["malware", "c2"],
  "raw": {}
}
```

Stages:
- Validation  
- Canonicalization  
- Deduplication  
- Correlation  
- Tagging  

Tech:
- Python  
- RabbitMQ or Redis Streams

### 3.3 AI Enrichment Engine
Purpose: Add semantic understanding and context to each IOC.

Functions:
- Threat summarization  
- Campaign attribution  
- Severity scoring  
- Suggested SOC actions  

Architecture:
- Local LLM (Llama/DeepSeek) or API LLM  
- Prompt templates  
- Embedding index

### 3.4 Correlation Engine
Purpose: Identify relationships across indicators.

Mechanisms:
- Graph correlation (Neo4j optional)  
- Rule-based correlation (YARA-like)

### 3.5 Storage Layer
- PostgreSQL (structured IOC records)  
- Elasticsearch/OpenSearch (search + analytics)

### 3.6 API & Integration Layer
REST API (FastAPI):
- /search  
- /lookup/ioc  
- /stats  
- /feeds/export  

Outbound Connectors:
- Splunk, Ela

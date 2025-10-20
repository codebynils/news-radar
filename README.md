# news-radar

**news-radar** is a small but enterprise-styled learning project built to explore how a modern, cloud-ready architecture fits together:  
Spring Boot + Kafka (Event Hubs) + Cosmos DB + React + Grafana on Azure.

It collects articles from public RSS feeds, normalizes them, and serves them through an OpenAPI backend to a simple web UI.  
For now, all articles are shown as a continuous, infinitely-scrolling list.  
Later phases will add AI-based classification and personalized relevance scoring.

> Because this is a learning project, the main goal is to learn enterprise patterns on a manageable scale —
> clean structure, clear contracts, working observability, and good documentation.

---

## ✨ Features (Phase 1)

- **Ingest** of RSS feeds via a Spring Boot scheduler  
- **Streaming pipeline** using Kafka (with Event Hubs)  
- **Cosmos DB Serverless** for normalized article storage  
- **OpenAPI 3.1 REST API** (contract-first)  
- **React frontend** with infinite scroll and filter options  
- **Prometheus + Grafana** for metrics (`items/hour`, latency, errors)  
- **Containerized deployment** on Azure Container Apps  
- **Cost-efficient and secure by default** — all serverless, minimal throughput

---


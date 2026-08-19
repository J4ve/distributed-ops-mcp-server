# Distributed Infrastructure Operations Cockpit & MCP Server (Case Study)

> [!NOTE]
> **Confidentiality Disclaimer**: This repository is an architectural case study of an internal operations tooling and AI integration platform built for a distributed digital media and management agency. Proprietary source code, specific business logic, internal database connection strings, server IPs, and company data have been omitted in compliance with non-disclosure agreements (NDA).

---

## Executive Summary
Engineered a unified, read-only Model Context Protocol (MCP) server that acts as an "AI-driven Ops Cockpit." The system empowers AI coding and operations assistants (Claude Code, Claude Desktop, Cursor) to diagnose system health, inspect workforce records, and query distributed multi-tier infrastructure in natural language without opening manual SSH sessions or web dashboards.

---

## The Problem Solved
* **Fragmented Operations Tooling**: Diagnosing operational bottlenecks previously required engineers to manually log into cloud SQL consoles, SSH into remote application VMs, and run manual `docker exec` queries across containerized clusters.
* **Operational Risk of Ad-Hoc Scripts**: Running ad-hoc SQL or bash queries during live incidents posed risk of accidental data mutation.
* **Context Switching Overhead**: Support and operations leads had to manually cross-reference data across three separate isolated datastores.

---

## System Architecture

```
                                  ┌───────────────────────────────┐
                                  │      AI Assistant Client      │
                                  │  (Claude Desktop, CLI, Cursor)│
                                  └───────────────┬───────────────┘
                                                  │ (Stdio Protocol)
                                                  ▼
                                  ┌───────────────────────────────┐
                                  │     FastMCP Server Engine     │
                                  │      (Strict Read-Only)       │
                                  └───────┬───────┬───────┬───────┘
                                          │       │       │
                 ┌────────────────────────┘       │       └────────────────────────┐
                 ▼                                ▼                                ▼
  ┌──────────────────────────────┐ ┌──────────────────────────────┐ ┌──────────────────────────────┐
  │      Cloud PostgreSQL DB     │ │     Remote VM SQLite DB      │ │ Containerized MongoDB Cluster│
  │ (Direct Read-Only Connection)│ │ (Read-Only Session over SSH) │ │ (Docker Exec Query Filtering)│
  └──────────────────────────────┘ └──────────────────────────────┘ └──────────────────────────────┘
```

---

## Key Modules & Engineering Contributions

### 1. Unified Multi-Backend Tool Registry
* **Heterogeneous Data Unification**: Integrated 3 distinct storage paradigms into a unified namespace schema:
  * `hr_*` ➔ Cloud PostgreSQL telemetry using pure-Python drivers (`pg8000`).
  * `bot_*` ➔ Remote application state via non-interactive OpenSSH tunnels executing `sqlite3 -readonly`.
  * `infra_*` ➔ Containerized MongoDB diagnostic stats via safe `docker exec` query isolation.

### 2. Strict Read-Only Security Model
* **Zero Mutation Guarantee**: Enforced read-only transaction isolation across all database connections, guaranteeing that AI assistant interactions cannot accidentally write, update, or delete production data.
* **Credential & Secret Scrubbing**: Sanitized all query outputs before transmission to the LLM client, automatically redacting authentication tokens and sensitive environment values.

### 3. Structured LLM Tooling & FastMCP
* **Schema-Validated Tool Definitions**: Designed type-safe tool parameters using Pydantic models for predictable LLM argument generation.
* **Zero-Friction Stdio Transport**: Lightweight, self-contained server implementation using FastMCP, requiring zero external server hosting overhead.

---

## Tech Stack

| Layer | Technologies |
| :--- | :--- |
| **Language & Core SDK** | Python 3.12, FastMCP (`mcp` SDK) |
| **Relational Drivers** | `pg8000` (Pure-Python PostgreSQL), `sqlite3` |
| **Infrastructure & Remote** | OpenSSH, Docker API / `mongosh` |
| **Validation & Types** | Pydantic v2, Python Type Annotations |

---

## Impact & Key Outcomes
* **Single-Interface Incident Response**: Reduced multi-system diagnostic query times from several minutes across 3 tabs to a single plain-English prompt.
* **Guaranteed Safety**: Zero risk of operational data mutation through hardware- and protocol-enforced read-only channels.

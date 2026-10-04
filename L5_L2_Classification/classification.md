# L5 Narrow / L2 General Classification — docker-compose
**Platform:** Anticloud | **PAX:** 27B | **IP:** USPTO pending 2026, Anticloud FZ LLE
**Domain:** Sovereign Docker Compose deployment: full Anticloud stack in containers

## L5 Narrow
docker-compose specializes in sovereign docker compose deployment: full anticloud stack in containers within the Anticloud sovereign deployment boundary. All operations stay local — no cloud services, no external APIs, no data exfiltration. The narrow scope ensures deterministic, auditable behavior that PAX 27B can reason about precisely.

## L2 General
L2 General means docker-compose is available to all 9 Anticloud tiers without per-tier configuration. The same API serves hospital, defense, robotics, and research deployments.

## PAX Integration
PAX 27B validates the Docker Compose configuration: checks that no container has external network access, all volumes are encrypted, and AIOSS chains are correctly mounted.

## AIOSS Audit Relevance
Every container event (image hash + container ID + start/stop + network policy hash) is AIOSS-chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Tamper-evident, offline-verifiable, zero cloud dependency.

## Regulatory / Compliance
NIST SP 800-190 (container security), CIS Docker Benchmark

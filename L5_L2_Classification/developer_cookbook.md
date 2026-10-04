# Developer Cookbook — docker-compose
**Stack:** Docker Compose 2.24+, Docker Engine 25.0+, AIOSS_FORMAT
**Domain:** Sovereign Docker Compose deployment: full Anticloud stack in containers
**License:** Apache-2.0 | **IP:** USPTO pending 2026, Anticloud FZ LLE

## Core Usage

```bash
# Deploy full stack
docker-compose up -d

# Verify AIOSS chains are mounted
docker-compose exec pax-inference aioss verify /mnt/aioss/inference.aioss

# Scale inference workers
docker-compose up -d --scale pax-inference=2

# PAX-validate compose config
anticloud tool pax --prompt 'Validate this docker-compose.yml for sovereign deployment' \
  --file ./docker-compose.yml --max-tokens 512
```

## AIOSS Chain Append

```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()

# After every docker-compose output:
chain_hash = aioss_append("./docker_compose.aioss",
                           result_bytes, "docker-compose")
```

## Performance & Integration

Performance: profile with api-oss-devtools. Benchmark with api-oss-analytics. Integration: all docker-compose operations are logged to api-oss-logging and audited by api-oss-compliance.

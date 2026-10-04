# Deploy Guide — docker-compose
**Platform:** Anticloud sovereign infrastructure | Air-gap capable
**Stack:** Docker Compose 2.24+, Docker Engine 25.0+, AIOSS_FORMAT

## Prerequisites
Python 3.11+. See stack: Docker Compose 2.24+, Docker Engine 25.0+, AIOSS_FORMAT. AIOSS_FORMAT required. PAX 27B weights for AI-assisted features.

## AIOSS Integration
```bash
aioss init --module docker-compose --output ./docker_compose.aioss
aioss append --chain ./docker_compose.aioss --payload ./output.bin --module docker-compose
aioss verify --chain ./docker_compose.aioss
```

## Air-Gap Deployment
```bash
# On networked machine:
pip download -r requirements.txt -d ./wheels/
# Transfer wheels/ to air-gap host, then:
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX 27B Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(
    model_path="./pax-27b-q4.gguf",
    module="docker-compose",
    aioss_chain="./docker_compose.aioss",
    classification="L5_NARROW_L2_GENERAL"
)
result = harness.process(input_data)
```

## Verification
```bash
aioss verify --chain ./docker_compose.aioss --verbose
python -m docker_compose.tests.smoke
```

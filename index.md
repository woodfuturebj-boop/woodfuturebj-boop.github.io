# Surplus Value Router

This public GitHub Pages site is used for AntSeed domain verification and buyer connection instructions.

- AntSeed peer: `c50de6922b00677c93007c01924586de887ced7b`
- Agent ID: `56687`
- Domain proof: `/.well-known/antseed.json`
- GitHub proof repo: `woodfuturebj-boop/antseed-proof`
- Settlement network: Base mainnet USDC
- Provider profile: Surplus-backed OpenAI-compatible value router
- Public endpoint: `192.220.28.51:6882`

## Connect

AntSeed buyer auto-selection is disabled, so buyers must pin a peer explicitly.

```bash
antseed buyer connection set --peer c50de6922b00677c93007c01924586de887ced7b
```

Per-request routing:

```bash
curl -H "x-antseed-pin-peer: c50de6922b00677c93007c01924586de887ced7b" http://127.0.0.1:8377/v1/models
```

Model-prefix routing:

```text
c50de6922b00677c93007c01924586de887ced7b@gpt-5.4
```

## Primary Services

- `gpt-5.4`
- `gpt-5.4-mini`
- `gpt-5.2-codex`
- `gpt-5.3-codex`
- `opus-4.7`
- `opus-4.8`
- `glm-5`
- `glm-5.1`
- `grok-4.3`

Inspect live services and current prices:

```bash
antseed network peer c50de6922b00677c93007c01924586de887ced7b
```

No private keys, API keys, or credentials are stored in this repository.

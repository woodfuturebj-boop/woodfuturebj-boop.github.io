# Surplus Value Router

Public AntSeed provider connection, verification, and beta onboarding site.

Live site: https://woodfuturebj-boop.github.io/

## Connect

AntSeed buyer auto-selection is disabled in the default flow. Start a buyer and pin this peer explicitly:

```bash
npm install -g @antseed/cli
antseed buyer start
antseed payments
antseed buyer connection set --peer c50de6922b00677c93007c01924586de887ced7b
curl -s http://127.0.0.1:8377/v1/models | jq '.data[].id'
```

## Featured services

- `opus-4.7`
- `opus-4.8`
- `claude-sonnet-5`
- `gpt-5.4`
- `glm-5.2`

The provider still advertises its broader catalog. Inspect signed live metadata and current pricing with:

```bash
antseed network peer c50de6922b00677c93007c01924586de887ced7b
```

## Verification

- Domain proof: `/.well-known/antseed.json`
- GitHub proof: `woodfuturebj-boop/antseed-proof`
- Settlement: Base mainnet USDC
- Response authentication: `verification.response-auth.v1`

No private keys, API keys, or provider credentials are stored in this repository.

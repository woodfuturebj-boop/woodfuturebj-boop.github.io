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

Run one real workload through the high-demand `gpt-5.4` route without changing
your saved connection:

```bash
curl http://127.0.0.1:8377/v1/chat/completions \
  -H "content-type: application/json" \
  -d '{"model":"c50de6922b00677c93007c01924586de887ced7b@gpt-5.4","messages":[{"role":"user","content":"REPLACE WITH YOUR REAL TASK"}]}'
```

The live page also provides copy-ready selectors for `glm-5.2`,
`claude-opus-4.8`, and the lowest-cost featured route, `minimax-m2.7`. All four
use the one-request `peer@model` prefix and do not replace the buyer's saved
connection.

## Featured services

- `gpt-5.4` - active high-demand rank-one pricing experiment
- `glm-5.2` - active multilingual rank-one pricing experiment
- `claude-opus-4.8` - active high-demand frontier coding pricing experiment
- `minimax-m2.7` - lowest-cost first workload
- `opus-4.7`
- `claude-sonnet-5`

The provider still advertises its broader catalog. Inspect signed live metadata and current pricing with:

```bash
antseed network peer c50de6922b00677c93007c01924586de887ced7b
```

## AntFeed MCP

This seller is indexed by AntFeed under wallet
`0xc50DE6922b00677c93007c01924586dE887ced7b`. MCP-compatible agents can install
`@antfeed/mcp`, look up `Surplus Value Router`, inspect pricing, and connect a
local AntSeed buyer after explicit user confirmation.

See the [24-hour external buyer guide](https://github.com/woodfuturebj-boop/antseed-proof/blob/main/BETA.md).

## Verification

- Domain proof: `/.well-known/antseed.json`
- GitHub proof: `woodfuturebj-boop/antseed-proof`
- Settlement: Base mainnet USDC
- Response authentication: `verification.response-auth.v1`

No private keys, API keys, or provider credentials are stored in this repository.

External buyer beta: https://github.com/woodfuturebj-boop/antseed-proof/issues/1

# Surplus Value Router

Public AntSeed provider connection, verification, and beta onboarding site.

Live site: https://woodfuturebj-boop.github.io/

## Connect

The shortest visual path is the official [AntStation desktop app](https://github.com/AntSeed/antseed/releases/latest):

1. Fund the buyer with Base USDC.
2. Open **Discover** and search for `Surplus Value Router`.
3. Choose `Surplus Value Router | GPT/GLM/Claude`, select a service, and start a real chat.

Selecting a Discover result pins both the provider and service. For CLI buyers,
start a buyer and pin this peer explicitly:

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
`gpt-5.5`, `claude-opus-4.8`, `claude-sonnet-5`, `gemini-3.1-pro-preview`, `claude-fable-5`, and the
lowest-cost featured route, `minimax-m2.7`. All six
use the one-request `peer@model` prefix and do not replace the buyer's saved
connection.

Model-specific public links preselect the matching route and keep the workload
command ready to copy:

- [`gpt-5.4`](https://woodfuturebj-boop.github.io/?model=gpt-5.4#first-workload)
- [`gpt-5.5`](https://woodfuturebj-boop.github.io/?model=gpt-5.5#first-workload)
- [`glm-5.2`](https://woodfuturebj-boop.github.io/?model=glm-5.2#first-workload)
- [`claude-opus-4.8`](https://woodfuturebj-boop.github.io/?model=claude-opus-4.8#first-workload)
- [`claude-sonnet-5`](https://woodfuturebj-boop.github.io/?model=claude-sonnet-5#first-workload)
- [`gemini-3.1-pro-preview`](https://woodfuturebj-boop.github.io/?model=gemini-3.1-pro-preview#first-workload)
- [`claude-fable-5`](https://woodfuturebj-boop.github.io/?model=claude-fable-5#first-workload)
- [`minimax-m2.7`](https://woodfuturebj-boop.github.io/?model=minimax-m2.7#first-workload)

## Featured services

- `gpt-5.4` - active high-demand rank-one pricing experiment
- `gpt-5.5` - active high-demand rank-one adoption route
- `glm-5.2` - active multilingual rank-one pricing experiment
- `claude-opus-4.8` - active high-demand frontier coding pricing experiment
- `gemini-3.1-pro-preview` - active rank-one Gemini reasoning experiment
- `claude-fable-5` - active rank-one long-form and coding experiment
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

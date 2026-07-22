# NovaRoute AI

Public AntSeed provider connection, verification, and production support site.

Live site: https://woodfuturebj-boop.github.io/

## Connect

The shortest visual path is the official [AntStation desktop app](https://github.com/AntSeed/antseed/releases/latest):

1. Fund the buyer with Base USDC.
2. Open **Discover** and search for `gpt-5.6-sol-pro`, `kimi-k3`, or `NovaRoute AI`.
3. Choose `NovaRoute AI`, select a service, and start a real chat.

Selecting a Discover result pins both the provider and service. For CLI buyers,
start a buyer and pin this peer explicitly:

```bash
npm install -g @antseed/cli
antseed buyer start
antseed payments
antseed buyer connection set --peer c50de6922b00677c93007c01924586de887ced7b
curl -s http://127.0.0.1:8377/v1/models | jq '.data[].id'
```

When a foreground buyer workload is finished, press `Ctrl+C` and wait for
`Disconnected. All channels finalized.` before closing the terminal. Avoid
force-killing the buyer process; graceful shutdown lets AntSeed finalize the
payment channel normally and release unused deposit.

Run one real workload through the pinned `gpt-5.5` route without changing your
saved connection:

```bash
curl http://127.0.0.1:8377/v1/chat/completions \
  -H "content-type: application/json" \
  -d '{"model":"c50de6922b00677c93007c01924586de887ced7b@gpt-5.5","messages":[{"role":"user","content":"REPLACE WITH YOUR REAL TASK"}]}'
```

The live page also provides copy-ready selectors for `gpt-5.6-sol-pro`,
`gemini-3-5-flash`, `kimi-k3`, `glm-5.2`, `gpt-5.5`, `claude-opus-4-7-fast`, `novaroute-code-audit-v1`, `claude-opus-4-8-fast`, `claude-opus-4.8`, `claude-opus-4.6`,
`claude-sonnet-5`, and `claude-fable-5`. All routes use the one-request
`peer@model` prefix and do not replace the buyer's saved
connection.

Model-specific public links preselect the matching route and keep the workload
command ready to copy:

- [`gpt-5.4`](https://woodfuturebj-boop.github.io/?model=gpt-5.4#first-workload)
- [`gpt-5.5`](https://woodfuturebj-boop.github.io/?model=gpt-5.5#first-workload)
- [`gpt-5.6-sol-pro`](https://woodfuturebj-boop.github.io/?model=gpt-5.6-sol-pro#first-workload)
- [`gemini-3-5-flash`](https://woodfuturebj-boop.github.io/routes/gemini-3-5-flash/) - demand-backed route; inspect signed live pricing before use
- [`glm-5.2`](https://woodfuturebj-boop.github.io/?model=glm-5.2#first-workload)
- [`kimi-k3`](https://woodfuturebj-boop.github.io/?model=kimi-k3#first-workload)
- [`claude-opus-4-7-fast`](https://woodfuturebj-boop.github.io/routes/claude-opus-4-7-fast/) - stable demand-backed route; inspect signed live pricing before use
- [`novaroute-code-audit-v1`](https://woodfuturebj-boop.github.io/routes/novaroute-code-audit-v1/) - read-only specialist agent for findings-first code, Web3 transaction-safety, and release-readiness reviews
- [`claude-opus-4-8-fast`](https://woodfuturebj-boop.github.io/routes/claude-opus-4-8-fast/) - current-demand rank-one route; inspect signed live pricing before use
- [`claude-opus-4.8`](https://woodfuturebj-boop.github.io/?model=claude-opus-4.8#first-workload)
- [`claude-opus-4.6`](https://woodfuturebj-boop.github.io/?model=claude-opus-4.6#first-workload)
- [`claude-sonnet-5`](https://woodfuturebj-boop.github.io/?model=claude-sonnet-5#first-workload)
- [`claude-fable-5`](https://woodfuturebj-boop.github.io/?model=claude-fable-5#first-workload)

## Featured services

- `gpt-5.4` - active high-demand rank-one route
- `gpt-5.5` - active high-demand route with signed live directory pricing
- `claude-opus-4-7-fast` - active stable demand-backed fast Opus route at 50% raw cost
- `novaroute-code-audit-v1` - active read-only specialist agent backed by the same verified 50% raw-cost upstream
- `gpt-5.6-sol-pro` - active high-demand rank-one reasoning route
- `gemini-3-5-flash` - active demand-backed 20% raw-cost rank-uplift route
- `glm-5.2` - active multilingual rank-one route
- `kimi-k3` - active rank-one agent and coding route
- `claude-opus-4-8-fast` - active current-demand rank-one fast Opus route
- `claude-opus-4.8` - active high-demand frontier coding route
- `claude-opus-4.6` - active high-demand rank-one coding route
- `claude-fable-5` - active rank-one long-form and coding route
- `opus-4.7`
- `claude-sonnet-5`

The provider still advertises its broader catalog. Inspect signed live metadata and current pricing with:

```bash
antseed network peer c50de6922b00677c93007c01924586de887ced7b
```

## AntFeed MCP

This seller is indexed by AntFeed under wallet
`0xc50DE6922b00677c93007c01924586dE887ced7b`. MCP-compatible agents can install
`@antfeed/mcp`, look up `NovaRoute AI`, inspect pricing, and connect a
local AntSeed buyer after explicit user confirmation. AntFeed refreshes its
provider directory hourly, so compare newly published launch prices with the
signed live catalog before approving a session.

See the [external buyer connection guide](https://github.com/woodfuturebj-boop/antseed-proof/blob/main/BETA.md).

## Verification

- Domain proof: `/.well-known/antseed.json`
- GitHub proof: `woodfuturebj-boop/antseed-proof`
- Settlement: Base mainnet USDC
- Response authentication: `verification.response-auth.v1`

No private keys, API keys, or provider credentials are stored in this repository.

External buyer support: https://github.com/woodfuturebj-boop/antseed-proof/issues/1

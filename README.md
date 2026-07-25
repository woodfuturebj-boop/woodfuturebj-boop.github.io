# NovaRoute AI

Public AntSeed provider connection, verification, and production support site.

Live site: https://woodfuturebj-boop.github.io/

## Connect

The shortest visual path is the official [AntStation desktop app](https://github.com/AntSeed/antseed/releases/latest):

1. Fund the buyer with Base USDC.
2. Open **Discover** and search the exact provider name `NovaRoute AI` first.
3. Choose `NovaRoute AI`, select a service, and start a real chat.

Searching by service name such as `claude-opus-4.6` is a useful fallback, but it
can return several peers; the exact provider name narrows the list directly.

Selecting a Discover result pins both the provider and service. For CLI buyers,
fund first, then start the proxy with this peer pinned in the startup command:

```bash
npm install -g @antseed/cli
antseed payments
antseed buyer start --peer c50de6922b00677c93007c01924586de887ced7b
```

If the buyer proxy is already running, change its session pin without a
restart:

```bash
antseed buyer connection set --peer c50de6922b00677c93007c01924586de887ced7b
```

When a foreground buyer workload is finished, press `Ctrl+C` and wait for
`Disconnected. All channels finalized.` before closing the terminal. Avoid
force-killing the buyer process; graceful shutdown lets AntSeed finalize the
payment channel normally and release unused deposit.

In a second terminal, run one real workload through the pinned
`claude-opus-4.6` route. It ranks first in AntSeed's July 25 official
model-sales snapshot and has the lowest indexed exact-offer price:

```bash
curl http://127.0.0.1:8377/v1/chat/completions \
  -H "content-type: application/json" \
  -d '{"model":"c50de6922b00677c93007c01924586de887ced7b@claude-opus-4.6","messages":[{"role":"user","content":"REPLACE WITH YOUR REAL TASK"}]}'
```

For coding-agent workloads, the official wrappers avoid hand-written provider
configuration:

```bash
antseed codex --model claude-opus-4.6
antseed opencode --model claude-opus-4.6
```

Aider can use the same local proxy without changing the saved buyer pin. Its
documented OpenAI-compatible path accepts the one-request `peer@model` route:

```bash
export OPENAI_API_BASE=http://127.0.0.1:8377/v1
export OPENAI_API_KEY=antseed-local
aider --model openai/c50de6922b00677c93007c01924586de887ced7b@claude-opus-4.6
```

The live page also includes a Continue `config.yaml` entry that uses the same
explicit peer route. See the official [Aider OpenAI-compatible
guide](https://aider.chat/docs/llms/openai-compat.html) and [Continue OpenAI
provider guide](https://docs.continue.dev/customize/model-providers/top-level/openai).

The live page also provides copy-ready selectors for `gpt-5.6-sol`, `gpt-5.6-sol-pro`,
`gemini-3-5-flash`, `kimi-k3`, `glm-5.2`, `minimax-m2.7`, `gpt-5.5`, `claude-opus-4-7-fast`, `novaroute-code-audit-v1`, `claude-opus-4-8-fast`, `claude-opus-4.6`,
`claude-sonnet-5`, and `claude-fable-5`. All routes use the one-request
`peer@model` prefix and do not replace the buyer's saved
connection.

Model-specific public links preselect the matching route and keep the workload
command ready to copy:

- [`gpt-5.4`](https://woodfuturebj-boop.github.io/?model=gpt-5.4#first-workload)
- [`gpt-5.5`](https://woodfuturebj-boop.github.io/?model=gpt-5.5#first-workload)
- [`gpt-5.6-sol`](https://woodfuturebj-boop.github.io/routes/gpt-5.6-sol/) - highest upstream dollar volume in the current sample; inspect signed live pricing before use
- [`gpt-5.6-sol-pro`](https://woodfuturebj-boop.github.io/?model=gpt-5.6-sol-pro#first-workload)
- [`gemini-3-5-flash`](https://woodfuturebj-boop.github.io/routes/gemini-3-5-flash/) - demand-backed route; inspect signed live pricing before use
- [`glm-5.2`](https://woodfuturebj-boop.github.io/?model=glm-5.2#first-workload)
- [`minimax-m2.7`](https://woodfuturebj-boop.github.io/routes/minimax-m2.7/) - eighth in AntSeed's official token-volume snapshot; inspect signed live pricing before use
- [`kimi-k3`](https://woodfuturebj-boop.github.io/?model=kimi-k3#first-workload)
- [`claude-opus-4-7-fast`](https://woodfuturebj-boop.github.io/routes/claude-opus-4-7-fast/) - stable demand-backed route; inspect signed live pricing before use
- [`novaroute-code-audit-v1`](https://woodfuturebj-boop.github.io/routes/novaroute-code-audit-v1/) - read-only specialist agent for findings-first code, Web3 transaction-safety, and release-readiness reviews
- [`claude-opus-4-8-fast`](https://woodfuturebj-boop.github.io/routes/claude-opus-4-8-fast/) - current-demand rank-one route; inspect signed live pricing before use
- [`claude-opus-4.6`](https://woodfuturebj-boop.github.io/routes/claude-opus-4.6/) - first in AntSeed's July 25 official model-sales snapshot and lowest-priced indexed exact offer
- [`claude-sonnet-5`](https://woodfuturebj-boop.github.io/?model=claude-sonnet-5#first-workload)
- [`claude-fable-5`](https://woodfuturebj-boop.github.io/?model=claude-fable-5#first-workload)

## Featured services

- `claude-opus-4.6` - first in the latest official model-sales snapshot; lowest-priced indexed exact offer
- `gpt-5.6-sol` - highest upstream dollar volume in the current market sample; exact rank one
- `gpt-5.6-sol-pro` - second-highest current reasoning volume; exact rank one
- `claude-sonnet-5` - high-value coding demand; exact rank one
- `claude-fable-5` - high-value long-form demand; exact rank one
- `kimi-k3` - agent and coding demand; exact rank one
- `glm-5.2` - highest request count in the latest upstream sample
- `minimax-m2.7` - eighth in AntSeed's official top models by token-volume snapshot
- `gpt-5.5` - strong request demand with signed live directory pricing
- `gpt-5.4` - general reasoning demand; exact rank one
- `novaroute-code-audit-v1` - read-only specialist agent

The provider still advertises its broader catalog. Inspect signed live metadata and current pricing with:

```bash
antseed network peer c50de6922b00677c93007c01924586de887ced7b
```

## AntFeed MCP

This seller is indexed by AntFeed under wallet
`0xc50DE6922b00677c93007c01924586dE887ced7b`. Buyers can open the
[direct AntFeed seller profile](https://www.antfeed.org/sellers/0xc50de6922b00677c93007c01924586de887ced7b)
without relying on directory ordering. MCP-compatible agents can install
`@antfeed/mcp`, look up `NovaRoute AI`, inspect pricing, and connect a
local AntSeed buyer after explicit user confirmation. AntFeed refreshes its
provider directory hourly, so compare newly published launch prices with the
signed live catalog before approving a session.

Use `http://localhost:8377` for the CLI buyer or `http://localhost:8378` for
AntStation Desktop. Start the selected buyer before restarting Claude Code,
Claude Desktop, Cursor, Cline, or another MCP host because AntFeed performs
buyer detection once at startup.

See the [external buyer connection guide](https://github.com/woodfuturebj-boop/antseed-proof/blob/main/BETA.md).
Agents can load the guarded
[`novaroute-antseed-buyer` skill](https://github.com/woodfuturebj-boop/antseed-proof/blob/main/skills/novaroute-antseed-buyer/SKILL.md)
for read-only verification and an explicit-confirmation paid workflow.

## Verification

- Domain proof: `/.well-known/antseed.json`
- GitHub proof: `woodfuturebj-boop/antseed-proof`
- Settlement: Base mainnet USDC
- Response authentication: `verification.response-auth.v1`

No private keys, API keys, or provider credentials are stored in this repository.

External buyer support: https://github.com/woodfuturebj-boop/antseed-proof/issues/1

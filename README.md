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
install the CLI, then run the foreground payment portal in its own terminal:

```bash
npm install -g @antseed/cli
antseed payments
```

After funding, stop the portal with `Ctrl+C` and confirm the deposit from that
terminal, or keep it open and use another terminal:

```bash
antseed buyer balance
```

Then start the proxy with this peer pinned:

```bash
antseed buyer start --peer c50de6922b00677c93007c01924586de887ced7b
```

If the buyer proxy is already running, change its session pin without a
restart:

```bash
antseed buyer connection set --peer c50de6922b00677c93007c01924586de887ced7b
```

Before opening a paid session, run the read-only preflight. These commands do
not call a model or open a paid inference session:

```bash
antseed --version
antseed network peer c50de6922b00677c93007c01924586de887ced7b
antseed buyer balance
```

When a foreground buyer workload is finished, press `Ctrl+C` and wait for
`Disconnected. All channels finalized.` before closing the terminal. Avoid
force-killing the buyer process; graceful shutdown lets AntSeed finalize the
payment channel normally and release unused deposit.

In a second terminal, run one real workload through the pinned
`claude-opus-4.6` route. It ranks first in AntSeed's July 25 official
model-sales snapshot and exposes signed live directory pricing:

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
explicit peer route. Cline can select **OpenAI Compatible** with base URL
`http://127.0.0.1:8377/v1`, API key `antseed-local`, and model ID
`c50de6922b00677c93007c01924586de887ced7b@claude-opus-4.6`. See the official
[Aider OpenAI-compatible guide](https://aider.chat/docs/llms/openai-compat.html),
[Continue OpenAI provider guide](https://docs.continue.dev/customize/model-providers/top-level/openai),
and [Cline OpenAI Compatible guide](https://docs.cline.bot/provider-config/openai-compatible).

Kilo Code can add a custom provider named `antseed` with provider API
**OpenAI Compatible**, base URL `http://127.0.0.1:8377/v1`, API key
`antseed-local`, and a manually added model ID using the explicit
`c50de6922b00677c93007c01924586de887ced7b@<service-id>` route. See the
[Kilo OpenAI Compatible guide](https://kilo.ai/docs/ai-providers/openai-compatible).

Zoo Code can select **OpenAI Compatible** with the same local Base URL and
placeholder API key, then choose a custom model ID using the explicit
`c50de6922b00677c93007c01924586de887ced7b@<service-id>` route. Its settings
refresh performs only a free local `/v1/models` read; the first paid request
must be a real coding task. The selected service must support native OpenAI
tool calling. See the
[Zoo Code OpenAI Compatible guide](https://docs.zoocode.dev/providers/openai-compatible).

Goose can add a custom **OpenAI Compatible** provider with API URL
`http://127.0.0.1:8377/v1`, API-key requirement disabled, streaming enabled,
and model `c50de6922b00677c93007c01924586de887ced7b@<service-id>`. Goose may read
the free local `/v1/models` catalog for discovery or context metadata. Keep
the peer prefix, skip the provider test, and begin with a real repository task.
See the [Goose provider guide](https://goose-docs.ai/docs/getting-started/providers/#configure-custom-provider).

Cherry Studio can add a custom **OpenAI** provider with API address
`http://127.0.0.1:8377`, placeholder API key `antseed-local`, and a manually
added model ID using the explicit
`c50de6922b00677c93007c01924586de887ced7b@<service-id>` route. Cherry Studio
appends `/v1` to this root address. Adding or listing models reads only the
free local catalog, but **Check** or **Detect** sends an inference probe. Skip
both checks, keep the peer prefix, and make the first paid request a real task.
For MCP-backed work, choose a service with native OpenAI tool calling. See the
[Cherry Studio custom provider guide](https://docs.cherry-ai.com/docs/en-us/pre-basic/providers/zi-ding-yi-fu-wu-shang).

Chatbox can import a reviewed custom provider through its official
`chatbox://provider/import` flow. The live page generates a route-specific
preview with provider ID `novaroute-antseed`, API host
`http://127.0.0.1:8377`, placeholder key `antseed-local`, and the explicit
`c50de6922b00677c93007c01924586de887ced7b@<service-id>` model marked for
native tool use. Import remains read-only until the buyer chooses **Save**;
re-importing the same ID shows an overwrite warning. Do not click **Check** or
**Test Model**, because Chatbox sends separate text, vision, and tool probes.
The optional **Fetch** action reads only the free local `/v1/models` catalog
but is unnecessary for the imported route. See the
[Chatbox custom provider guide](https://docs.chatboxai.app/en/guides/providers).

Jan supports OpenAI-compatible custom endpoints. Add provider `NovaRoute AI`
with base URL `http://127.0.0.1:8377/v1`, placeholder key `antseed-local`, and
the exact `c50de6922b00677c93007c01924586de887ced7b@<service-id>` model. Jan
reads only the free local `/v1/models` catalog while creating the provider or
testing the placeholder key. Custom-model capabilities are not inferred, so
open the model editor and enable **Tools** locally before MCP-backed work.
Keep individual MCP tool approvals enabled and make the first paid request a
real task. See the [Jan custom endpoint guide](https://jan.ai/docs/desktop/remote-models/custom-endpoint).

The live page also provides copy-ready selectors for `gpt-5.6-sol`, `gpt-5.6-sol-pro`,
`gemini-3-5-flash`, `kimi-k3`, `glm-5.2`, `minimax-m2.7`, `gpt-5.5`, `claude-opus-4-7-fast`, `novaroute-code-audit-v1`, `claude-opus-4-8-fast`, `claude-opus-4.6`,
`claude-sonnet-5`, and `claude-fable-5`. All routes use the one-request
`peer@model` prefix and do not replace the buyer's saved
connection.

Model-specific public links preselect the matching route and keep the workload
command ready to copy:

- [`gpt-5.4`](https://woodfuturebj-boop.github.io/routes/gpt-5.4/)
- [`gpt-5.5`](https://woodfuturebj-boop.github.io/?model=gpt-5.5#first-workload)
- [`gpt-5.6-sol`](https://woodfuturebj-boop.github.io/routes/gpt-5.6-sol/) - highest upstream dollar volume in the current sample; inspect signed live pricing before use
- [`gpt-5.6-sol-pro`](https://woodfuturebj-boop.github.io/?model=gpt-5.6-sol-pro#first-workload)
- [`gemini-3-5-flash`](https://woodfuturebj-boop.github.io/routes/gemini-3-5-flash/) - demand-backed route; inspect signed live pricing before use
- [`glm-5.2`](https://woodfuturebj-boop.github.io/routes/glm-5.2/)
- [`minimax-m2.7`](https://woodfuturebj-boop.github.io/routes/minimax-m2.7/) - eighth in AntSeed's official token-volume snapshot; inspect signed live pricing before use
- [`kimi-k3`](https://woodfuturebj-boop.github.io/?model=kimi-k3#first-workload)
- [`claude-opus-4-7-fast`](https://woodfuturebj-boop.github.io/routes/claude-opus-4-7-fast/) - stable demand-backed route; inspect signed live pricing before use
- [`novaroute-code-audit-v1`](https://woodfuturebj-boop.github.io/routes/novaroute-code-audit-v1/) - read-only specialist agent for findings-first code, Web3 transaction-safety, and release-readiness reviews; [compare on AntFeed](https://www.antfeed.org/services/novaroute-code-audit-v1)
- [`claude-opus-4-8-fast`](https://woodfuturebj-boop.github.io/routes/claude-opus-4-8-fast/) - current-demand rank-one route; inspect signed live pricing before use
- [`claude-opus-4.6`](https://woodfuturebj-boop.github.io/routes/claude-opus-4.6/) - first in AntSeed's July 25 official model-sales snapshot; inspect signed live pricing before use
- [`claude-sonnet-5`](https://woodfuturebj-boop.github.io/routes/claude-sonnet-5/)
- [`claude-fable-5`](https://woodfuturebj-boop.github.io/routes/claude-fable-5/)

## Featured services

The public service table links each service name to its exact AntFeed provider
comparison. Confirm the selected peer and signed live pricing before opening a
paid session.

- `claude-opus-4.6` - first in the latest official model-sales snapshot; signed live directory pricing
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
`@antfeed/mcp`, look up `NovaRoute AI`, and inspect pricing before switching
to the direct pinned AntSeed buyer path for an approved real workload. AntFeed refreshes its
provider directory hourly, so compare newly published launch prices with the
signed live catalog before approving a session.

Use AntFeed MCP `0.2.5` as read-only discovery with the current AntSeed CLI.
CLI `0.1.136` does not expose the MCP bridge's `/health` and `/sessions`
endpoints, so do not call `create_session`; use the verified direct buyer
instructions for the paid workload.

See the [external buyer connection guide](https://github.com/woodfuturebj-boop/antseed-proof/blob/main/BETA.md).
Agents can load the guarded
[`novaroute-antseed-buyer` skill](https://github.com/woodfuturebj-boop/antseed-proof/tree/main/skills/novaroute-antseed-buyer)
for read-only verification and an explicit-confirmation paid workflow.

## Verification

- Domain proof: `/.well-known/antseed.json`
- GitHub proof: `woodfuturebj-boop/antseed-proof`
- Settlement: Base mainnet USDC
- Response authentication: `verification.response-auth.v1`

No private keys, API keys, or provider credentials are stored in this repository.

External buyer support: https://github.com/woodfuturebj-boop/antseed-proof/issues/1

# Using Clippy Vision with LM Studio

This guide explains how to connect Clippy Vision to LM Studio using the Model Context Protocol (MCP), allowing a local language model to query your recorded activity.

## Prerequisites

- Clippy Vision installed and running.
- LM Studio version **0.3.17 or later**.
- A local language model that supports tool calling.
- Some activity recorded by Clippy Vision to use for testing.

For general setup information, see the [LM Studio MCP documentation](https://lmstudio.ai/docs/app/mcp).

## 1. Copy the Clippy Vision configuration

1. Open Clippy Vision.
2. Go to **Settings → Connect apps**.
3. Copy the configuration provided for MCP clients.
4. Keep the generated command, arguments, and paths unchanged.

The configuration is generated for your computer. Do not copy another user's paths, because they may be different on your system.

## 2. Add Clippy Vision to LM Studio

1. Open LM Studio.
2. In the right sidebar, open **Program**.
3. Select **Install → Edit mcp.json**.
4. Add the Clippy Vision configuration you copied under `mcpServers`.
5. Save the file and check whether Clippy Vision connects.

If `mcp.json` already contains other MCP servers, preserve their entries and add Clippy Vision as another entry inside `mcpServers`. Do not replace the existing configuration.

For additional details, see [Use MCP Servers in LM Studio](https://lmstudio.ai/docs/app/mcp).

## 3. Choose a local model

Choose a model that supports tool calling and has a sufficiently large context window. Clippy Vision tools may return long results, so a model with a small context window might not have enough space to process them.

**Model recommendation: Pending verification.**

A specific model should be recommended only after it has been tested with Clippy Vision in LM Studio. Once verified, record the exact model name, version or revision if available, quantization, and LM Studio version used.

The model must successfully call a Clippy Vision tool and use the returned information. Model support for tool calling alone does not guarantee that the integration will work correctly.

## 4. Test the connection

Ensure Clippy Vision has been running long enough to record some activity. Then ask the model in LM Studio:

> What was I working on in the last hour?

A good answer should summarize relevant activity found in the recorded history, such as applications or tasks, based on the information available to the tools.

The model should not invent events if no matching activity is available. Confirm that it actually calls a Clippy Vision tool and uses the returned result. A plausible answer without a tool call does not prove that the integration works.

## 5. What stays on your computer?

- Clippy Vision records and stores activity locally.
- LM Studio runs the selected model locally.
- The MCP connection allows the model to query Clippy Vision's available tools.
- Tool responses may contain activity information, subject to Clippy Vision's privacy protections.

**Important:** Running these components locally does not automatically guarantee that the entire workflow is offline. If you need a fully local workflow, avoid cloud-based services and verify the relevant application and network settings. Review the [Clippy Vision MCP guide](../mcp.md) and its access-permission information before connecting a client.

## Troubleshooting

- **The server does not connect:** Copy the configuration again from Clippy Vision and check that the generated paths are valid.
- **The model answers without calling a tool:** Check the MCP connection and choose a model that supports tool calling.
- **No recent activity is found:** Ensure Clippy Vision is running and has recorded activity during the requested period.
- **LM Studio rejects the configuration:** Check the JSON syntax and consult the [LM Studio MCP documentation](https://lmstudio.ai/docs/app/mcp).

---

**Verification status:** The setup and model tool-calling behavior have not yet been verified hands-on. The specific model recommendation remains pending verification.

# @weaaare/mcp-virtual-screen-reader-auditor

MCP (Model Context Protocol) server for **headless virtual screen reader accessibility audits**. Works on any OS — no native screen reader required. Launches a real browser, injects a virtual screen reader, and navigates the live accessibility tree including dynamic/SPA content.

Can help cover up to **12 WCAG 2.2 success criteria** using the same audit, findings, and reporting framework as `@weaaare/mcp-voiceover-auditor`.

> **Important:** This tool does **not** replace a manual audit by an accessibility specialist, nor does it substitute real testing with assistive-technology users. It is a fast feedback loop that catches common issues early — a complement, never a replacement.

## Tools

| Tool | Description |
| --- | --- |
| `virtual_start` | Start the Virtual Screen Reader on a URL or raw HTML (launches headless browser) |
| `virtual_stop` | Stop the Virtual Screen Reader and release resources |
| `virtual_next` | Move cursor to the next item in the accessibility tree |
| `virtual_previous` | Move cursor to the previous item in the accessibility tree |
| `virtual_act` | Perform default action for the current item (e.g., activate a link/button) |
| `virtual_interact` | Interact with the current container item |
| `virtual_stop_interacting` | Stop interacting with the current container item |
| `virtual_press` | Press a key on the focused item (e.g. `Enter`, `Tab`, `ArrowDown`) |
| `virtual_type` | Type text into the currently focused item |
| `virtual_perform` | Semantic navigation by element type: headings, links, landmarks, forms, figures |
| `virtual_item_text` | Get text of the item under the Virtual Screen Reader cursor |
| `virtual_last_spoken_phrase` | Get the last phrase spoken by the Virtual Screen Reader |
| `virtual_spoken_phrase_log` | Get full spoken phrase history for this session |
| `virtual_item_text_log` | Get full visited item text history for this session |
| `virtual_clear_spoken_phrase_log` | Clear the spoken phrase log |
| `virtual_clear_item_text_log` | Clear the visited item text log |
| `virtual_click` | Click the mouse at the current position |
| `start_audit` | Start a structured audit session with metadata |
| `log_finding` | Log violations/warnings/passes with WCAG criteria and recommendations |
| `get_audit_status` | Get current audit progress and finding counters |
| `get_findings` | Retrieve findings from current or latest session |
| `end_audit` | End audit session and return summary data |
| `generate_report` | Generate reports in Markdown, JSON, or CSV |

## Getting started

**Standard config** works in most MCP clients:

```json
{
  "mcpServers": {
    "virtual-screen-reader-auditor": {
      "command": "npx",
      "args": ["-y", "@weaaare/mcp-virtual-screen-reader-auditor"]
    }
  }
}
```

<details>
<summary>VS Code</summary>

Add to your project's `.vscode/mcp.json` (or user-level `settings.json` under `"mcp"`):

```json
{
  "servers": {
    "virtual-screen-reader-auditor": {
      "command": "npx",
      "args": ["-y", "@weaaare/mcp-virtual-screen-reader-auditor"]
    }
  }
}
```

Or install via the VS Code CLI:

```bash
code --add-mcp '{"name":"virtual-screen-reader-auditor","command":"npx","args":["-y","@weaaare/mcp-virtual-screen-reader-auditor"]}'
```

</details>

<details>
<summary>Claude Desktop</summary>

Follow the MCP install [guide](https://modelcontextprotocol.io/quickstart/user). Add to your `claude_desktop_config.json` using the standard config above.

</details>

<details>
<summary>Claude Code</summary>

```bash
claude mcp add virtual-screen-reader-auditor npx -y @weaaare/mcp-virtual-screen-reader-auditor
```

</details>

<details>
<summary>Cursor</summary>

Go to `Cursor Settings` → `MCP` → `Add new MCP Server`. Use `command` type with `npx -y @weaaare/mcp-virtual-screen-reader-auditor`.

Or add to `.cursor/mcp.json` using the standard config above.

</details>

<details>
<summary>Windsurf</summary>

Follow Windsurf MCP [documentation](https://docs.windsurf.com/windsurf/cascade/mcp). Use the standard config above.

</details>

<details>
<summary>Cline</summary>

Add to your [`cline_mcp_settings.json`](https://docs.cline.bot/mcp/configuring-mcp-servers#editing-mcp-settings-files):

```json
{
  "mcpServers": {
    "virtual-screen-reader-auditor": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@weaaare/mcp-virtual-screen-reader-auditor"],
      "disabled": false
    }
  }
}
```

</details>

<details>
<summary>Kiro</summary>

Follow the MCP Servers [documentation](https://kiro.dev/docs/mcp/). Add to `.kiro/settings/mcp.json` using the standard config above.

</details>

<details>
<summary>Codex</summary>

```bash
codex mcp add virtual-screen-reader-auditor npx "-y" "@weaaare/mcp-virtual-screen-reader-auditor"
```

Or edit `~/.codex/config.toml`:

```toml
[mcp_servers.virtual-screen-reader-auditor]
command = "npx"
args = ["-y", "@weaaare/mcp-virtual-screen-reader-auditor"]
```

</details>

<details>
<summary>Goose</summary>

Go to `Advanced settings` → `Extensions` → `Add custom extension`. Use type `STDIO` and set the command to `npx -y @weaaare/mcp-virtual-screen-reader-auditor`.

</details>

<details>
<summary>Warp</summary>

Go to `Settings` → `AI` → `Manage MCP Servers` → `+ Add`. Use the standard config above.

</details>

<details>
<summary>Gemini CLI</summary>

Follow the MCP install [guide](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md#configure-the-mcp-server-in-settingsjson). Use the standard config above.

</details>

## WCAG criteria covered

| SC | Name | Tools |
| --- | --- | --- |
| 1.1.1 | Non-text Content | `virtual_item_text`, `virtual_last_spoken_phrase`, `log_finding` |
| 1.3.1 | Info and Relationships | `virtual_perform`, `virtual_item_text`, `log_finding` |
| 2.1.1 | Keyboard | `virtual_press`, `virtual_act`, `log_finding` |
| 2.1.2 | No Keyboard Trap | `virtual_press`, `virtual_next`, `log_finding` |
| 2.4.1 | Bypass Blocks | `virtual_perform`, `virtual_next`, `log_finding` |
| 2.4.2 | Page Titled | `virtual_item_text`, `virtual_last_spoken_phrase`, `log_finding` |
| 2.4.3 | Focus Order | `virtual_next`, `virtual_previous`, `log_finding` |
| 2.4.4 | Link Purpose (In Context) | `virtual_perform`, `virtual_item_text`, `log_finding` |
| 2.4.6 | Headings and Labels | `virtual_perform`, `virtual_item_text`, `log_finding` |
| 3.3.1 | Error Identification | `virtual_last_spoken_phrase`, `virtual_item_text`, `log_finding` |
| 3.3.2 | Labels or Instructions | `virtual_item_text`, `virtual_perform`, `log_finding` |
| 4.1.2 | Name, Role, Value | `virtual_last_spoken_phrase`, `virtual_item_text`, `log_finding` |

## Acknowledgements

- **[W3C](https://www.w3.org/WAI/)** — for the [WCAG 2.2](https://www.w3.org/TR/WCAG22/) guidelines, [WAI-ARIA](https://www.w3.org/TR/wai-aria/) specification, and the [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/). W3C content is used under the [W3C Software and Document License](https://www.w3.org/copyright/software-license/).
- **[a11ysupport.io](https://a11ysupport.io/)** — community-driven assistive-technology support data by Michael Fairchild, available under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## License

MIT - [weAAAre](https://weAAAre.com)

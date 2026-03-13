# @weaaare/mcp-voiceover-auditor

MCP (Model Context Protocol) server for **screen reader accessibility audits on macOS**. Drives VoiceOver through AppleScript, letting an AI agent navigate pages exactly as a screen-reader user would: read element announcements, check focus order, detect keyboard traps, and log structured WCAG findings — all without a human manually operating VoiceOver.

Can help cover up to **12 WCAG 2.2 success criteria** (1.1.1, 1.3.1, 2.1.1, 2.1.2, 2.4.1, 2.4.2, 2.4.3, 2.4.4, 2.4.6, 3.3.1, 3.3.2, 4.1.2).

> **Important:** This tool does **not** replace a manual audit by an accessibility specialist, nor does it substitute real testing with assistive-technology users. It is a fast feedback loop that catches common issues early — a complement, never a replacement.

## Tools

| Tool | Description |
| --- | --- |
| `check_setup` | Verify VoiceOver environment setup (support, default screen reader, AppleScript readiness) |
| `voiceover_start` | Start VoiceOver before running navigation and audit commands |
| `voiceover_stop` | Stop VoiceOver and clean up the session |
| `voiceover_commander` | Execute native VoiceOver commander commands for robust navigation |
| `voiceover_perform` | Execute keyboard-based VoiceOver navigation commands |
| `voiceover_next` | Move the VoiceOver cursor to the next item |
| `voiceover_previous` | Move the VoiceOver cursor to the previous item |
| `voiceover_act` | Perform default action for focused item (VO-Space equivalent) |
| `voiceover_interact` | Start interacting with the current container item |
| `voiceover_stop_interacting` | Stop interacting with the current container item |
| `voiceover_press` | Press a key on the focused item (e.g. `Enter`, `Tab`, `ArrowDown`) |
| `voiceover_type` | Type text into the currently focused item |
| `voiceover_item_text` | Get text of the currently focused VoiceOver item |
| `voiceover_last_spoken_phrase` | Get the most recent phrase spoken by VoiceOver |
| `voiceover_spoken_phrase_log` | Get full spoken phrase history for this session |
| `voiceover_item_text_log` | Get full visited item text history for this session |
| `voiceover_clear_spoken_phrase_log` | Clear the spoken phrase log for this session |
| `voiceover_clear_item_text_log` | Clear the item text log for this session |
| `voiceover_click` | Perform a mouse click at the current position |
| `voiceover_detect` | Detect whether VoiceOver is supported on the current system |
| `voiceover_default` | Check whether VoiceOver is the default screen reader |
| `macos_activate_application` | Activate a macOS application by name |
| `macos_get_active_application` | Get the currently active macOS application |
| `focus_ensure_browser` | Ensure browser is focused before page interaction |
| `focus_record` | Save a focus breadcrumb for recovery during audits |
| `focus_last_known` | Retrieve the last known focus position |
| `focus_history` | Retrieve complete focus breadcrumb history |
| `start_audit` | Start a new audit session with URL, WCAG level, and screen reader |
| `log_finding` | Log `violation`, `warning`, or `pass` with WCAG criteria and recommendation |
| `get_audit_status` | Get current audit progress, counts, and duration |
| `get_findings` | Retrieve findings from current or last session |
| `end_audit` | End audit session and generate summary statistics |
| `generate_report` | Generate audit report in `markdown`, `json`, or `csv` |

## Requirements

- macOS with VoiceOver
- AppleScript enabled for VoiceOver: `VoiceOver Utility → General → Allow VoiceOver to be controlled with AppleScript`
- Node.js >= 18

## Getting started

**Standard config** works in most MCP clients:

```json
{
  "mcpServers": {
    "voiceover-auditor": {
      "command": "npx",
      "args": ["-y", "@weaaare/mcp-voiceover-auditor"]
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
    "voiceover-auditor": {
      "command": "npx",
      "args": ["-y", "@weaaare/mcp-voiceover-auditor"]
    }
  }
}
```

Or install via the VS Code CLI:

```bash
code --add-mcp '{"name":"voiceover-auditor","command":"npx","args":["-y","@weaaare/mcp-voiceover-auditor"]}'
```

</details>

<details>
<summary>Claude Desktop</summary>

Follow the MCP install [guide](https://modelcontextprotocol.io/quickstart/user). Add to your `claude_desktop_config.json` using the standard config above.

</details>

<details>
<summary>Claude Code</summary>

```bash
claude mcp add voiceover-auditor npx -y @weaaare/mcp-voiceover-auditor
```

</details>

<details>
<summary>Cursor</summary>

Go to `Cursor Settings` → `MCP` → `Add new MCP Server`. Use `command` type with `npx -y @weaaare/mcp-voiceover-auditor`.

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
    "voiceover-auditor": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@weaaare/mcp-voiceover-auditor"],
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
codex mcp add voiceover-auditor npx "-y" "@weaaare/mcp-voiceover-auditor"
```

Or edit `~/.codex/config.toml`:

```toml
[mcp_servers.voiceover-auditor]
command = "npx"
args = ["-y", "@weaaare/mcp-voiceover-auditor"]
```

</details>

<details>
<summary>Goose</summary>

Go to `Advanced settings` → `Extensions` → `Add custom extension`. Use type `STDIO` and set the command to `npx -y @weaaare/mcp-voiceover-auditor`.

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
| 1.1.1 | Non-text Content | `voiceover_item_text`, `voiceover_last_spoken_phrase`, `log_finding` |
| 1.3.1 | Info and Relationships | `voiceover_perform`, `voiceover_commander`, `log_finding` |
| 2.1.1 | Keyboard | `voiceover_press`, `focus_record`, `log_finding` |
| 2.1.2 | No Keyboard Trap | `voiceover_press`, `focus_last_known`, `log_finding` |
| 2.4.1 | Bypass Blocks | `voiceover_commander`, `voiceover_perform`, `log_finding` |
| 2.4.2 | Page Titled | `voiceover_item_text`, `voiceover_last_spoken_phrase`, `log_finding` |
| 2.4.3 | Focus Order | `focus_record`, `focus_history`, `log_finding` |
| 2.4.4 | Link Purpose (In Context) | `voiceover_perform`, `voiceover_commander`, `log_finding` |
| 2.4.6 | Headings and Labels | `voiceover_perform`, `voiceover_item_text`, `log_finding` |
| 3.3.1 | Error Identification | `voiceover_last_spoken_phrase`, `voiceover_item_text`, `log_finding` |
| 3.3.2 | Labels or Instructions | `voiceover_item_text`, `voiceover_perform`, `log_finding` |
| 4.1.2 | Name, Role, Value | `voiceover_last_spoken_phrase`, `voiceover_item_text`, `log_finding` |

## Acknowledgements

- **[W3C](https://www.w3.org/WAI/)** — for the [WCAG 2.2](https://www.w3.org/TR/WCAG22/) guidelines, [WAI-ARIA](https://www.w3.org/TR/wai-aria/) specification, and the [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/). W3C content is used under the [W3C Software and Document License](https://www.w3.org/copyright/software-license/).
- **[a11ysupport.io](https://a11ysupport.io/)** — community-driven assistive-technology support data by Michael Fairchild, available under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## License

MIT - [weAAAre](https://weAAAre.com)
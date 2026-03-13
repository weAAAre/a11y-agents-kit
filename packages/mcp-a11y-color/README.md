# @weaaare/mcp-a11y-color

MCP (Model Context Protocol) server for **color accessibility**. Gives AI coding agents the ability to verify, simulate, and suggest accessible colors in real-time while writing code.

Can help cover up to **5 WCAG 2.2 success criteria** (1.4.1, 1.4.3, 1.4.6, 1.4.11, 2.4.7).

## Tools

| Tool | Description |
| --- | --- |
| `check-contrast` | WCAG 2.2 contrast ratio between fg/bg — pass/fail for AA/AAA, normal/large/UI |
| `get-color-info` | Parse any CSS color → hex, RGB, HSL, luminance, contrast on B/W |
| `suggest-contrast-fix` | Given a failing pair, suggest the minimal change to meet target level |
| `simulate-color-blindness` | Simulate colors under 8 types of color vision deficiency |
| `find-accessible-color` | Given background + hue, find a color meeting a target contrast ratio |
| `apca-contrast` | APCA Lc (WCAG 3.0 draft) perceptual contrast score with polarity and usage recommendation |
| `nearest-color-name` | Find the closest CSS named color(s) using perceptual Delta E distance |
| `analyze-palette-contrast` | N×N contrast matrix for a set of colors — essential for design system audits |
| `generate-cvd-safe-palette` | Generate a palette of N colors distinguishable under all CVD types |
| `analyze-design-tokens` | Audit design tokens for WCAG compliance, auto-classify and suggest fixes |

## Getting started

**Standard config** works in most MCP clients:

```json
{
  "mcpServers": {
    "a11y-color": {
      "command": "npx",
      "args": ["-y", "@weaaare/mcp-a11y-color"]
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
    "a11y-color": {
      "command": "npx",
      "args": ["-y", "@weaaare/mcp-a11y-color"]
    }
  }
}
```

Or install via the VS Code CLI:

```bash
code --add-mcp '{"name":"a11y-color","command":"npx","args":["-y","@weaaare/mcp-a11y-color"]}'
```

</details>

<details>
<summary>Claude Desktop</summary>

Follow the MCP install [guide](https://modelcontextprotocol.io/quickstart/user). Add to your `claude_desktop_config.json` using the standard config above.

</details>

<details>
<summary>Claude Code</summary>

```bash
claude mcp add a11y-color npx -y @weaaare/mcp-a11y-color
```

</details>

<details>
<summary>Cursor</summary>

Go to `Cursor Settings` → `MCP` → `Add new MCP Server`. Use `command` type with `npx -y @weaaare/mcp-a11y-color`.

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
    "a11y-color": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@weaaare/mcp-a11y-color"],
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
codex mcp add a11y-color npx "-y" "@weaaare/mcp-a11y-color"
```

Or edit `~/.codex/config.toml`:

```toml
[mcp_servers.a11y-color]
command = "npx"
args = ["-y", "@weaaare/mcp-a11y-color"]
```

</details>

<details>
<summary>Goose</summary>

Go to `Advanced settings` → `Extensions` → `Add custom extension`. Use type `STDIO` and set the command to `npx -y @weaaare/mcp-a11y-color`.

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
| 1.4.1 | Use of Color | `simulate-color-blindness`, `generate-cvd-safe-palette` |
| 1.4.3 | Contrast (Minimum) | `check-contrast`, `suggest-contrast-fix`, `find-accessible-color`, `analyze-design-tokens` |
| 1.4.6 | Contrast (Enhanced) | `check-contrast`, `suggest-contrast-fix`, `find-accessible-color`, `apca-contrast` |
| 1.4.11 | Non-text Contrast | `check-contrast`, `analyze-palette-contrast` |
| 2.4.7 | Focus Visible | Planned: `check-focus-indicator` |

## Acknowledgements

- **[W3C](https://www.w3.org/WAI/)** — for the [WCAG 2.2](https://www.w3.org/TR/WCAG22/) guidelines and color contrast success criteria. W3C content is used under the [W3C Software and Document License](https://www.w3.org/copyright/software-license/).
- **[a11ysupport.io](https://a11ysupport.io/)** — community-driven assistive-technology support data by Michael Fairchild, available under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## License

MIT — [weAAAre](https://weAAAre.com)

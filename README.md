<div align="center">

<img src="assets/banner.png" alt="ZeroMark for Gemini" width="100%">

# ZeroMark for Gemini CLI

**Your saved X posts and your Living Memory, inside Gemini.**

[![Validate](https://github.com/asheus/zeromark-gemini-extension/actions/workflows/validate.yml/badge.svg)](https://github.com/asheus/zeromark-gemini-extension/actions/workflows/validate.yml)
[![Gemini CLI extension](https://img.shields.io/badge/Gemini_CLI-extension-4285F4?style=flat-square&logo=googlegemini&logoColor=white)](#install)
[![MCP](https://img.shields.io/badge/MCP-Streamable_HTTP-1c1917?style=flat-square)](https://modelcontextprotocol.io)
[![Read-only](https://img.shields.io/badge/access-read--only-2f6b3f?style=flat-square)](#privacy-and-security)
[![License: MIT](https://img.shields.io/badge/license-MIT-f0472c?style=flat-square)](LICENSE)

[Website](https://www.zeromark.io) · [Connector guide](https://www.zeromark.io/docs/connector) · [Privacy](https://www.zeromark.io/privacy) · [Report a bug](https://github.com/asheus/zeromark-gemini-extension/issues/new/choose)

</div>

---

[ZeroMark](https://www.zeromark.io) reads every post you bookmarked on X and helps you clear the pile. The posts you mark Done become your **Living Memory**: notes that grow as you keep more.

This extension connects [Gemini CLI](https://github.com/google-gemini/gemini-cli) to ZeroMark's hosted MCP server, `https://www.zeromark.io/api/mcp`, and adds a `GEMINI.md` context file that tells Gemini how to use it well.

### What you can ask

- *"What did I save about GLP-1 trials last month? Link the posts."*
- *"Which of my open saves have gone stale?"*
- *"Read my Living Memory on fundraising and tell me what I keep coming back to."*
- *"From my saves, what is the one thing worth acting on this week?"*

---

## Install

```bash
gemini extensions install https://github.com/asheus/zeromark-gemini-extension
```

Start `gemini` and ask something about your saves. The first call opens ZeroMark's sign-in in your browser; approve read-only access and Gemini carries on. Run `/mcp` to see the server and its tools.

To update or remove it:

```bash
gemini extensions update zeromark
gemini extensions uninstall zeromark
```

### Prefer a key?

Make a key in ZeroMark under **Settings → Connect to Claude, ChatGPT or Gemini**, then add the server to `~/.gemini/settings.json` yourself instead of installing the extension:

```json
{
  "mcpServers": {
    "zeromark": {
      "httpUrl": "https://www.zeromark.io/api/mcp",
      "headers": {
        "Authorization": "Bearer $ZEROMARK_KEY"
      }
    }
  }
}
```

Keys start with `zm_mcp_`, are shown once, and can be revoked in Settings at any time.

### Using Claude?

Use the companion marketplace: [`asheus/zeromark-plugins`](https://github.com/asheus/zeromark-plugins).

---

## Tools

Eight tools, all read-only. None of them can mark a save Done, let it go, edit, delete, or touch your X account.

| Tool | What it does |
| --- | --- |
| `library_overview` | Counts by stage and field, your top voices, and how many Living Memory notes you have. A good first call. |
| `search_saves` | Search your saves by meaning and by words, with optional `status`, `since` and `until` filters. Up to 25 a page. |
| `get_save` | One save in full, by its id, its x.com URL or its post id. |
| `list_by_stage` | Your saves at one stage of their life, newest first, with a cursor for the next page. |
| `get_memory` | Your Living Memory as Markdown: every note, your own thoughts on it, and its sources. |
| `weekly_question` | Asks ZeroMark which one save is worth acting on this week, and why. |
| `search` | A plain search over the same library, returning ids and titles. |
| `fetch` | One result from `search`, in full. |

### Stages

| Stage | Means |
| --- | --- |
| `fresh` | Open and saved in the last two weeks. |
| `still_useful` | Marked Done, pinned, or still current. |
| `fading` | Open and older, or past its moment. |
| `snoozed` | Hidden until a date you chose. |
| `let_go` | You let it go. |

---

## Privacy and security

- **Read-only, by design.** The server exposes no write tools, and an OAuth grant or key carries the `read` scope only.
- **Your library only.** Every call is scoped to the account that approved it.
- **You decide, and you can undo it.** Disconnect the app or revoke a key in ZeroMark's Settings and the next call is refused.
- **What is logged.** Which tool ran, when, and how many rows came back. Never the question, never the content.
- **Posts are other people's words.** Results tell Gemini that saved posts are content to read, never instructions to follow.

Full policy: [zeromark.io/privacy](https://www.zeromark.io/privacy). Found a vulnerability? See [SECURITY.md](SECURITY.md).

## Plans and limits

The connector is on every ZeroMark plan, the free plan included. `weekly_question` counts as one Chat question against the free plan's daily allowance. Each key or app may make 120 calls every 15 minutes.

## Troubleshooting

| You see | Try |
| --- | --- |
| `401 Unauthorized` | Run `/mcp auth zeromark` to sign in again, or check the key has not been revoked. |
| `429` | You passed 120 calls in 15 minutes. Wait a few minutes. |
| Empty results | Connect X in ZeroMark first, so there is a library to read. |

---

## Repository layout

```text
.
├── gemini-extension.json   # The extension manifest Gemini CLI reads
├── GEMINI.md               # Context: which tool fits which question
└── assets/
```

There is no code to run on your machine: Gemini CLI talks to ZeroMark's hosted server.

## Development

```bash
git clone https://github.com/asheus/zeromark-gemini-extension
cd zeromark-gemini-extension
gemini extensions link .
gemini
```

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

The files in this repository are released under the [MIT License](LICENSE). The ZeroMark service they connect to is governed by the [ZeroMark terms](https://www.zeromark.io/terms).

<div align="center">
<sub>Made by <a href="https://www.zeromark.io">ZeroMark</a> · Tellurave LLC</sub>
</div>

# Contributing

Thanks for helping make ZeroMark work better inside Gemini.

## What belongs here

This repository holds the Gemini CLI extension: its manifest and the `GEMINI.md` context file. The connector itself runs on ZeroMark's servers, so a change to what a tool returns is a feature request, not a pull request here.

## Making a change

1. Fork the repository and create a branch.
2. Make your change.
3. Try it locally:

   ```bash
   gemini extensions link .
   gemini
   ```

   Ask something that should use your change, and check `/mcp` lists the zeromark server.
4. If users will notice, add a line under **Unreleased** in [CHANGELOG.md](CHANGELOG.md).
5. Open a pull request and fill in the template.

## Style

- Plain words, short sentences. No em dashes.
- `version` in `gemini-extension.json` follows [Semantic Versioning](https://semver.org).

For anything security related, follow [SECURITY.md](SECURITY.md).

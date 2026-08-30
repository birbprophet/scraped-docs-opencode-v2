---
url: https://opencode.ai/v2/docs
title: "Intro"
description: "Intro documentation for OpenCode."
access_date: 2026-08-30T17:46:54.764Z
current_date: 2026-08-30T17:46:54.764Z
---

# Intro

These docs are for the beta version of OpenCode, which will become OpenCode 2.0. The beta is still changing: things may
break, and APIs, configuration, and plugin APIs may change.

OpenCode 2 installs and runs as `opencode2`. It does not replace OpenCode 1's `opencode` binary, so you can keep both
versions installed and run them side by side.

## Install

<div data-install-code>
  <CodeBlock
    code={`$ npm install -g @opencode-ai/cli@beta
$ bun install -g --trust @opencode-ai/cli@beta
$ pnpm add -g --allow-build=@opencode-ai/cli @opencode-ai/cli@beta
$ yarn global add @opencode-ai/cli@beta
$ curl -fsSL https://opencode.ai/v2/install | bash`}
  />
</div>

The package uses a trusted postinstall script to select the native `opencode2` binary for your platform. The Bun and pnpm
commands above explicitly allow that script to run.

Homebrew, Arch Linux, Windows package managers, Docker, and standalone binaries are not supported during the beta.

---

## Connect

OpenCode has built in support for many LLM providers - you can connect to them
directly [in the TUI](cli/providers.md) with `/connect`.

See [Providers](providers.md) to configure custom providers.

If you'd like easy access to all the best coding models you can try out
[OpenCode Console](https://console.opencode.ai).

You can also try [OpenCode Go](https://opencode.ai/go) a $10/month subscription
plan that grants you access to the best open source models.

---

## Customize

Make OpenCode your own by editing the [OpenCode config](config.md), [loading plugins](plugins.md), [connecting MCP
servers](mcp-servers.md), or [creating commands](commands.md). For terminal interface themes and keybindings, see [CLI
configuration](cli/config.md).

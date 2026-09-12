---
url: https://opencode.ai/v2/docs
title: "Intro"
description: "Intro documentation for OpenCode."
access_date: 2026-09-12T05:29:58.668Z
current_date: 2026-09-12T05:29:58.668Z
---

# Intro

These docs describe OpenCode and its APIs, configuration, and plugin system.

OpenCode installs and runs as `opencode`.

## Install

<div data-install-code>
  <CodeBlock
    code={`$ npm install -g @opencode/cli
$ bun install -g --trust @opencode/cli
$ pnpm add -g --allow-build=@opencode/cli @opencode/cli
$ yarn global add @opencode/cli
$ curl -fsSL https://opencode.ai/v2/install | bash`}
  />
</div>

The npm package uses a trusted postinstall script to select the native `opencode` binary for your platform. The Bun and pnpm
commands above explicitly allow that script to run.

Docker images use versioned tags, for example `ghcr.io/anomalyco/opencode:2.0.0`.

Homebrew, AUR, Windows package managers, and standalone binaries are not supported.

---

## Connect

OpenCode has built in support for many LLM providers - you can connect to them
directly [in the TUI](cli/providers.md) with `/connect`.

See [Providers](providers.md) to configure custom providers.

If you'd like easy access to all the best coding models you can try out
[OpenCode Console](console.md).

You can also try [OpenCode Go](console/go.md) a $10/month subscription
plan that grants you access to the best open source models.

---

## Customize

Make OpenCode your own by editing the [OpenCode config](config.md), [loading plugins](plugins.md), [connecting MCP
servers](mcp-servers.md), or [creating commands](commands.md). For terminal interface themes and keybindings, see [CLI
configuration](cli/config.md).

---
url: https://opencode.ai/v2/docs
title: "Intro"
description: "Intro documentation for OpenCode."
access_date: 2026-09-11T05:30:56.426Z
current_date: 2026-09-11T05:30:56.426Z
---

# Intro

These docs describe OpenCode 2 and its released APIs, configuration, and plugin system.

OpenCode 2 installs and runs as `opencode2`. It does not replace OpenCode 1's `opencode` binary, so you can keep both
versions installed and run them side by side.

## Install

<div data-install-code>
  <CodeBlock
    code={`$ npm install -g @opencode/cli@beta
$ bun install -g --trust @opencode/cli@beta
$ pnpm add -g --allow-build=@opencode/cli @opencode/cli@beta
$ yarn global add @opencode/cli@beta
$ paru -S opencode-beta
$ curl -fsSL https://opencode.ai/v2/install | bash`}
  />
</div>

The npm package uses a trusted postinstall script to select the native `opencode2` binary for your platform. The Bun and pnpm
commands above explicitly allow that script to run.

On Arch Linux, install [`opencode-beta`](https://aur.archlinux.org/packages/opencode-beta) from the AUR with `paru`.
It provides the `opencode2` command; manage updates through your AUR helper.

Homebrew, Windows package managers, Docker, and standalone binaries are not supported in V2.

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

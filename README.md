# typescript-native-lsp

Claude Code plugin that gives Claude LSP code intelligence (go to definition, find references, symbols, …) for TypeScript/JavaScript using **TypeScript 7's native language server** (`tsc --lsp --stdio`).

## Why

TypeScript 7 (the native Go port) no longer ships `tsserver.js`. The official `typescript-lsp` plugin starts `typescript-language-server`, which needs `tsserver.js`, so in TS 7 workspaces it fails with:

> The TypeScript of the workspace (TypeScript 7.x …) provides no tsserver.js.

This plugin talks to the language server built into TS 7 instead.

## Requirements

- TypeScript 7 installed globally so `tsc` on your `PATH` is 7.x: `npm i -g typescript@7`
  (Claude Code starts the server from the repository root, which may not have a local `node_modules`.)
- Check: `tsc --version` → `Version 7.x`

## Install

In Claude Code:

```
/plugin marketplace add lplotni/claude-typescript-native-lsp
/plugin install typescript-native-lsp@typescript-native-lsp
/plugin disable typescript-lsp@claude-plugins-official
```

or from a shell:

```
claude plugin marketplace add lplotni/claude-typescript-native-lsp
claude plugin install typescript-native-lsp@typescript-native-lsp --scope user
claude plugin disable typescript-lsp@claude-plugins-official --scope user
```

Restart Claude Code afterwards. Disable the official plugin so the two servers don't compete for the same file types.

## Caveats

- Uses whichever `tsc` is on `PATH`. With nvm, a Node version without a global TS 7 means no LSP.
- If your global TS major version differs from the project's, diagnostics may differ from `tsc` in CI.

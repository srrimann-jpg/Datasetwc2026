# Google-Flow MCP setup notes

Source: https://github.com/Mitanshp5/Google-Flow_MCP

## Install

```
git clone https://github.com/Mitanshp5/Google-Flow_MCP.git
cd Google-Flow_MCP
npm install
npm run build   # produces dist/index.js
```

`.mcp.json` in this repo points `node` at `<install-dir>/dist/index.js`.

## Config path bug

The built `dist/index.js` is a single bundled file, so `src/utils/config.js`'s
`__dirname`-based path resolution ends up one directory too high: instead of
reading `<install-dir>/config/flow.config.json`, it reads
`<parent-of-install-dir>/config/flow.config.json`.

Workaround: copy `flow.config.example.json` (from this folder, or the
upstream repo's `config/flow.config.example.json`) to
`<parent-of-install-dir>/config/flow.config.json` and fill in:

- `expectedAccount` — the Google account signed into Chrome that Flow should use
- `chromeUserDataDir` / `chromeProfile` — point at a Chrome profile already
  signed into that account

Without a real Chrome install and signed-in profile, the server starts fine
but browser-automation tool calls will fail.

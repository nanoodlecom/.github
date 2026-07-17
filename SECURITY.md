# Security Policy

This policy covers every repository in the [nanoodlecom](https://github.com/nanoodlecom) org — the nanoodle editor and site, the JS/Python executors, the MCP server, and the supporting tools.

## Reporting a vulnerability

Please **do not open a public issue** for security problems.

- Preferred: use GitHub's private vulnerability reporting ("Report a vulnerability" under the repo's Security tab), or
- Email **mikkel@255bits.com** with the details.

You'll get a response as fast as a one-maintainer project allows — normally within a few days. Please include a reproduction if you can.

## What counts as high-impact here

nanoodle's whole pitch is *no servers, no analytics, bring your own key* — so the crown jewels are on the user's machine:

- **API key exposure** — any path where a NanoGPT key could leak to a third party, appear in logs/stdout, or be exfiltrated by a shared app or graph.
- **Wallet secrets** — `nanoodle-mcp`'s x402 wallet mode holds a Nano seed/private key in-process; anything that could leak the secret or sign an unintended send block is critical.
- **Unwanted spend** — a graph, share link, or imported app triggering paid API calls without a real user gesture (the consent gate in the app player exists for exactly this).
- **Share-link payloads** — `#g=`/`#j=`/`#a=` fragments execute in the viewer's browser; sandbox or decoding escapes matter.

## Scope notes

- Third-party services (nano-gpt.com, Nano RPC nodes, Cloudflare) have their own programs — report issues in *our* use of them here, and issues in the services to their owners.
- There is no bug bounty; there is honest credit in release notes if you want it.

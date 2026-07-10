# pi-better-messages-cache

> **Deprecated for Pi 0.80.6+.** Remove this extension unless you specifically
> need its MiniMax/Kimi dual-cache-breakpoint workaround.

Pi 0.80.6's built-in Anthropic provider now owns raw SSE parsing, repairs
malformed tool-call JSON, and safely parses partial tool arguments. This
extension's former streaming control-character fix is therefore no longer
needed.

The extension still adds a `cache_control` marker to the last assistant
`tool_use` block. That workaround can improve cache-hit rates for providers
with MiniMax/Kimi-style cache windows, but it replaces Pi's full Anthropic
provider and bypasses its newer transport, caching, retry, and thinking support.
It is not recommended for native Anthropic use.

## Uninstall

```bash
pi remove npm:@mcowger/pi-better-messages-cache
```

This restores the built-in Anthropic stream handler automatically.

## Legacy use only

The extension implements the dual-cache-breakpoint strategy proposed in
[pi#1737](https://github.com/earendil-works/pi/pull/1737): it marks both the
last assistant `tool_use` block and the last user/tool-result block. Pi 0.80.6
does not add the assistant marker, but does cache the system prompt, latest tool
definition, and latest user block.

If you still use a provider affected by the cache-window issue, install this
extension only after verifying that its cache-hit improvement outweighs losing
Pi's built-in Anthropic-provider updates.

## Requirements

- [Pi 0.80.6+](https://github.com/earendil-works/pi)
- `@earendil-works/pi-coding-agent` and `@earendil-works/pi-ai` (bundled with Pi)

---

## License

MIT © mcowger

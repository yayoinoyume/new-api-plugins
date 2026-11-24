---
changelogVersion: 1
plugin: "typesafe"
version: "1.3.0"
locale: "en"
translations:
  zh-CN: "CHANGELOG.zh-CN.md"
---
# Changelog

## [1.3.0]

### Added

- Load the current Jev model list from TypeSafe with "Fetch models" in the channel form. The plugin reads `GET /v1/models` from the upstream and lists every model TypeSafe offers, so a model TypeSafe adds appears without a plugin update.

### Changed

- Send a request for any Jev model, not only the four models listed by default. A request may name a model from the fetched list or a channel model alias, and the gateway sends the upstream model it maps to. A request without a model is still rejected.

### Migration

- Set a price for each model you add from the upstream list before offering it. Use task usage expression billing, as for the built-in models: at TypeSafe's current price of 0.042 USD per 1 million input tokens, the expression is `tier("base", u("input_tokens") * 0.042 / 1000000)`.
- Enter the channel API address without a trailing `/v1` to fetch the model list. System One requests still accept an address that ends in `/v1`.
- Install this version on a gateway that serves the plugin `/v1/models` route. Earlier New API releases do not support the plugin's relay routes.

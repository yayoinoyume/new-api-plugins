---
changelogVersion: 1
plugin: "typesafe"
version: "1.3.0"
locale: "zh-CN"
---
# Changelog

## [1.3.0]

### Added

- 渠道配置里可以用“获取模型列表”从 TypeSafe 读取当前可用的 Jev 模型。插件向上游请求 `GET /v1/models`，把 TypeSafe 提供的模型逐个列出，TypeSafe 新增模型后不需要再更新插件。

### Changed

- 提交请求时可以使用任意 Jev 模型，不再只限默认列出的四个模型。请求里的模型可以来自获取到的模型列表，也可以是渠道里配置的模型别名，网关会按映射发送对应的上游模型。模型为空的请求仍会被拒绝。

### Migration

- 从上游列表里新增的模型要先用任务用量表达式定价，再提供给用户，内置模型也是如此。按 TypeSafe 目前每 100 万输入 token 0.042 美元的价格，表达式为 `tier("base", u("input_tokens") * 0.042 / 1000000)`。
- 要获取模型列表，渠道的 API 地址末尾不要带 `/v1`。System One 请求仍然兼容末尾带 `/v1` 的地址。
- 请在支持插件 `/v1/models` 路由的网关上安装这个版本。更早的 New API 版本不支持插件的转发路由。

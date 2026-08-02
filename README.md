# Shadowrocket AI Routing

这个模块把 Claude、Anthropic 以及 yfamilys 的 AI 规则集优先路由到 Shadowrocket 中自建的 `美国` 策略组，不直接修改订阅配置，因此原配置仍可正常自动更新。

## 使用前提

Shadowrocket 中需要存在一个名称完全一致的策略组：`美国`。建议只把经过筛选的纯净美国节点放入该组。

## 安装

在 Shadowrocket 的“配置 → 模块”中通过下面的 Raw URL 添加并启用模块：

```text
https://raw.githubusercontent.com/ethanfyx0423-del/shadowrocket-ai-routing/main/ai-pure-us-override.sgmodule
```

启用后可在“配置 → 测试规则”中分别测试 `claude.ai` 和 `anthropic.com`，结果应显示策略为 `美国`。

## 后续更新

模块地址保持不变。仓库中的模块文件更新后，在 Shadowrocket 中更新远程模块即可获取新版本，不需要重新修改订阅配置。

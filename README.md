# Shadowrocket AI Routing

这个模块把 Claude、Anthropic 固定路由到 Shadowrocket 中的 `美国 3` 节点，同时把 yfamilys 的其他 AI 规则优先路由到自建的 `美国` 策略组。模块不直接修改订阅配置，因此原配置仍可正常自动更新。

## 使用前提

Shadowrocket 中需要同时存在：

- 名称完全一致的节点 `美国 3`，供 Claude/Anthropic 固定使用；
- 名称完全一致的策略组 `美国`，供其他 AI 服务使用。

如果机场订阅以后重命名或删除 `美国 3`，需要同步修改本模块中的策略名称。

## 安装

在 Shadowrocket 的“配置 → 模块”中通过下面的 Raw URL 添加并启用模块：

```text
https://raw.githubusercontent.com/ethanfyx0423-del/shadowrocket-ai-routing/main/ai-pure-us-override.sgmodule
```

启用后可在“配置 → 测试规则”中分别测试 `claude.ai` 和 `anthropic.com`，结果应显示策略为 `美国 3`。

## 后续更新

模块地址保持不变。仓库中的模块文件更新后，在 Shadowrocket 中更新远程模块即可获取新版本，不需要重新修改订阅配置。

## 哔哩哔哩去广告（保留会员购）

该版本基于 [deezertidal/shadowrocket-rules 的 biliad.module](https://github.com/deezertidal/shadowrocket-rules/blob/main/modules/biliad.module)，移除了会隐藏会员购入口的“标签页处理”和“我的页面处理”，其余开屏、推荐流、动态、直播、番剧等处理保持不变。

```text
https://raw.githubusercontent.com/ethanfyx0423-del/shadowrocket-ai-routing/main/biliad-keep-mall.module
```

使用前请禁用或删除原版 `biliad.module`，不要同时启用两个版本。该模块包含 HTTPS 响应脚本，需要为当前配置正确安装并启用 Shadowrocket 的 HTTPS 解密证书。更新模块后请彻底关闭并重新打开哔哩哔哩；若会员购仍未出现，再清理哔哩哔哩缓存后重试。

## LinkedIn 香港节点组分流

该模块把 LinkedIn App、网页及相关静态资源固定路由到现有的 `🇭🇰 香港节点`策略组。它不会绑定单一节点，组内节点仍可按原配置自动测速和切换。

```text
https://raw.githubusercontent.com/ethanfyx0423-del/shadowrocket-ai-routing/main/linkedin-hk-routing.sgmodule
```

在 Shadowrocket 的“配置 → 模块”中通过上面的 Raw URL 添加并启用模块，然后彻底关闭并重新打开 LinkedIn。当前配置中必须存在名称完全一致的 `🇭🇰 香港节点`策略组。

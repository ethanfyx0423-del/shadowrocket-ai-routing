# Shadowrocket AI Routing

主配置把 Flower SS 与鹊桥作为两个独立节点源，在同一地区内共同自动测速；Claude、Anthropic 固定路由到 `[静态家宽]美国`，ChatGPT/OpenAI、Gemini 与其他 AI 使用 `🤖️ 人工智能`，优先选择 `[静态家宽]美国`，Flower 美国节点作为备用。AI 模块提供相同的规则覆盖，可与主配置配合使用。

## 双订阅主配置

文件：`shadowrocket-dual-subscriptions.conf`

- 普通境外流量默认使用香港地区组；
- 香港、日本、新加坡、台湾、美国等地区组会同时匹配两个订阅中的同地区节点；
- Claude 固定到 `[静态家宽]美国`，没有备用节点；
- 其他 AI 使用故障转移组，首选 `[静态家宽]美国`，备用为 Flower 美国高级1、高级3及标准1–8；已被识别为 SOCKS5 代理的高级2不参与；
- 配置不包含节点密码和订阅地址，也不设置会覆盖自定义内容的 `update-url`。

导入后，应继续保留并更新 Flower SS 与鹊桥两个订阅，但在“配置”页勾选本文件，不要把只含 `[Proxy]` 的订阅文件当作活动路由配置。

## 使用前提

Shadowrocket 中需要同时存在：

- 名称完全一致的节点 `[静态家宽]美国`，供 Claude/Anthropic 固定使用，并作为其他 AI 的首选节点；
- 名称完全一致的策略组 `🤖️ 人工智能`，供 Claude 之外的 AI 服务使用。

如果机场订阅以后重命名或删除 `[静态家宽]美国`，需要同步修改本模块中的策略名称。

## 安装

在 Shadowrocket 的“配置 → 模块”中通过下面的 Raw URL 添加并启用模块：

```text
https://raw.githubusercontent.com/ethanfyx0423-del/shadowrocket-ai-routing/main/ai-pure-us-override.sgmodule
```

启用后可在“配置 → 测试规则”中测试：

- `claude.ai` 和 `anthropic.com`，结果应显示策略为 `[静态家宽]美国`；
- `chatgpt.com` 和 `openai.com`，结果应显示策略为 `🤖️ 人工智能`；
- `gemini.google.com` 和 `generativelanguage.googleapis.com`，结果应显示策略为 `🤖️ 人工智能`。

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

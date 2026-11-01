# 红果短剧去广告 · Stash 覆写

拦截 **红果短剧**（含番茄系 App 共用的广告基础设施）的广告请求。纯 `REJECT` 域名规则：

- ✅ 无需 MitM 证书、无需脚本
- ✅ 不修改机场订阅，以「覆写」形式叠加在任何配置之上
- ✅ Stash iOS 3.7.0 真机实测：信息流 / 插播第三方广告消失

## 安装

Stash → 覆写 → `+` → **从 URL 安装**，粘贴：

```text
https://raw.githubusercontent.com/lzwsoldier/stash-hongguo-adblock/main/hongguo-adblock.stoverride
```

大陆网络直连 raw 失败时用镜像（内容相同）：

```text
https://cdn.jsdelivr.net/gh/lzwsoldier/stash-hongguo-adblock@main/hongguo-adblock.stoverride
https://gh-proxy.com/raw.githubusercontent.com/lzwsoldier/stash-hongguo-adblock/main/hongguo-adblock.stoverride
```

安装时选「**安装并启用**」，然后**强制退出红果短剧再重新打开**（清掉已缓存的广告素材）。

## 拦截范围

| 类别 | 域名 | 对应广告 |
|---|---|---|
| 穿山甲 / CSJ 广告 SDK | `api-access.pangolin-sdk-toutiao{,1,-b}.com`、`gromore.pangolin-sdk-toutiao.com`、`ether-pack.pangolin-sdk-toutiao.com` | 开屏广告、激励视频、GroMore 聚合 |
| 广告模板 / 渲染包 | `sf3/sf6-fe-tos.pglstatp-toutiao.com`、`cm.bilibili.com` | 广告素材加载 |
| 字节自家广告 API | `*.zijieapi.com` | 信息流广告请求（`ads*`）、广告配置（`tnc`）、风控（`mssdk`）、埋点（`mon/applog`） |
| 广告素材 CDN | `*.pglstatp-toutiao.com`、`*.pstatp.com`、`*.pangle.cn`、`*-ad-sign.byteimg.com` | 广告图片与静态资源 |
| 广告效果追踪 | `effect.snssdk.com`、`ichannel.snssdk.com`、`zlink.toutiao.com` | 曝光 / 点击归因 |

## 什么拦不掉（别白费劲）

- 首页「猜你喜欢」剧集推荐卡片、金币任务、VIP 会员推广 —— 红果**第一方业务**，与剧集内容走同一 API，域名拦截无法区分
- 「看广告领金币 / 权益」会**直接失效**（与普通广告共用 SDK，属预期行为）；需要领金币时在 Stash 覆写页临时停用即可

## 注意

- 仅供学习研究；绕过广告可能违反红果 / 番茄《用户协议》，请自行评估（含账号风险）
- 域名为 2026-11 真机连接观察所得，字节可能轮换域名；失效请提 issue 并附上 Stash 面板里的连接域名
- 与其他去广告覆写叠加时会有规则重复（无害，但没必要）

## 来源与致谢

- 穿山甲 SDK 域名列表修改自 [azel-ko/stash-adblock-rules](https://github.com/azel-ko/stash-adblock-rules)（Apache-2.0）
- `zijieapi.com` 等字节自家广告 API 来自实机连接观察 + 社区番茄小说去广告规则交叉验证

## License

Apache-2.0（见 [LICENSE](LICENSE) 与 [NOTICE](NOTICE)）

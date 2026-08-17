# 中正锅炉页面 GEO 诊断报告

基于 `yao-geo-skills / yao-geo-page-audit` 方法论重跑  
生成日期：2026-08-17

## 1. 执行摘要

本次按姚金刚开源项目 `yao-geo-page-audit` 的页面诊断方法论，将中正锅炉官网与产品中心放进五段链路中评估：发现入口、检索候选、主内容抽取、证据质量、生成引用。

结论：中正锅炉页面的品牌和产品大类能被识别，基础标题、描述、H1/H2、canonical 等结构信号较完整；但从 GEO 视角看，当前页面还不够像“可被 AI 搜索放心抽取和引用的官方资料页”。最需要优先处理的是可抓取性异常、证据来源不足、参数表缺失、FAQ 缺失、更新时间缺失和 schema 缺失。

P0/P1 风险：

- P0：本地可复测请求出现 HTTP/2 stream 错误、HTTPS 空响应、HTTP 444、robots/sitemap 空响应或超时，可能影响部分抓取器把页面纳入候选素材。
- P1：产品中心缺少同口径参数表、选型 FAQ、来源说明、更新时间，削弱 AI 对“锅炉怎么选、产品有哪些、如何比较供应商”的抽取和引用准备度。
- P1：快照中没有 JSON-LD schema，AI 和搜索系统缺少结构化实体、产品、FAQ、面包屑线索。

边界说明：本轮没有服务器日志、CMS 后台、真实浏览器 DOM、AI 平台回答样本，因此不判断真实抓取频次、平台召回、排名、答案出现率或引用份额。

## 2. 输入与范围

| 项目 | 内容 |
|---|---|
| 品牌 | 中正锅炉 |
| 官网 | [官网首页](https://www.zzgl.cn/) |
| 产品中心 | [产品中心](https://www.zzgl.cn/chanpinzhongxin/) |
| 目标问题 | 工业锅炉厂家怎么选；中正锅炉产品有哪些；蒸汽锅炉和热水锅炉怎么选；燃气锅炉和生物质锅炉哪个好 |
| 可用材料 | 用户提供 URL；上一轮 GEOHub 快照；本地 HTTP/DNS/TLS 复测；yao-geo-page-audit 方法论 |
| 不可用材料 | 服务器日志、CMS 源码、真实渲染 DOM、PageSpeed 数据、AI 平台采样回答 |

## 3. 页面组合与选择依据

| 页面 | 类型 | 选择依据 | 本轮状态 |
|---|---|---|---|
| 首页 | 首页 | 品牌入口页，承载品牌实体、产品入口、服务入口 | 已基于本地快照和请求复测诊断 |
| 产品中心 | 一级页 | 用户指定，承载主要产品分类和询价意图 | 已基于本地快照和请求复测诊断 |
| WNS/SZS 等产品详情页 | 二级页候选 | 产品中心首类为燃油/燃气锅炉，详情页通常承载参数和场景 | 未纳入结构评分；缺少可稳定抓取 HTML |

输入缺口：用户没有提供具体二级产品详情页 URL，本地抓取也不稳定，所以二级页只作为后续抽样建议，不写成已观察结论。

## 4. 五段链路评分

| 链路阶段 | 分数 | 判断 |
|---|---:|---|
| 发现入口 | 45/100 | DNS 能解析，官方 URL 明确；但 HTTP/HTTPS/robots/sitemap 复测异常 |
| 检索候选 | 40/100 | 页面主题明确，但抓取异常可能影响部分检索系统候选构建 |
| 主内容抽取 | 62/100 | 标题、meta、canonical、H1/H2、main 基础结构可用；缺 FAQ、表格、锚点、schema |
| 证据质量 | 32/100 | 官方产品大类和联系信息可见；缺参数来源、手册、案例、检测报告、更新时间 |
| 生成引用 | 38/100 | 有可引用的品牌和产品分类事实；缺可独立引用的原子事实、问答、表格和来源标注 |

## 5. 公开答案素材问题集

| 高意图问题 | 需要补的官方素材 | 优先级 |
|---|---|---|
| 中正锅炉产品有哪些？ | 产品分类总览、每类锅炉定义、适用行业、容量范围、资料链接 | P1 |
| 工业锅炉厂家怎么选？ | 选型流程、工况参数清单、服务边界、案例来源、售后能力说明 | P1 |
| 燃气锅炉和生物质锅炉哪个好？ | 同口径比较表：燃料、排放、热效率、运行成本、适用场景 | P1 |
| 食品厂/化工厂如何选锅炉？ | 行业场景页：蒸汽需求、压力、排放、典型方案和案例链接 | P2 |
| 导热油锅炉适合哪些场景？ | 高温低压供热边界、适用行业、典型型号、限制条件 | P2 |
| 循环流化床锅炉和燃煤锅炉区别？ | 技术边界、燃料适应性、脱硫/低氮说明、容量范围 | P2 |

这些问题不是 AI 平台表现数据，而是“公开答案素材准备度”问题集。

## 6. 权威证据台账

| 结论 | 来源层级 | 页面或材料 | 影响 | 可信度 |
|---|---|---|---|---|
| DNS 可解析到公网 IP `193.112.50.236` | 观察 | 本地 DNS 复测 | 说明域名基础解析存在 | 高 |
| HTTPS 首页 HEAD 请求出现 HTTP/2 stream 错误 | 观察 | 本地 curl 复测 | 可能影响部分抓取器候选获取 | 中 |
| HTTPS 首页 HTTP/1.1 请求出现空响应 | 观察 | 本地 curl 复测 | 可抓取性风险，需要服务端复测 | 中 |
| HTTP 首页返回 nginx 444 | 观察 | 本地 curl 复测 | 非浏览器/异常请求可能被边缘服务拒绝 | 高 |
| robots.txt 和 sitemap.xml 请求空响应 | 观察 | 本地 curl 复测 | 发现入口和规范入口不稳定 | 中 |
| 首页快照包含 title、meta description、canonical、1 个 H1、4 个 H2 | 观察 | 本地 HTML 快照 | 基础结构信号较好 | 中 |
| 产品中心快照包含 title、meta description、canonical、1 个 H1、6 个 H2 | 观察 | 本地 HTML 快照 | 产品分类结构可抽取 | 中 |
| 快照中未观察到 JSON-LD schema | 观察 | 本地 HTML 快照 | 实体和 FAQ 结构化信号不足 | 中 |
| 结构化数据必须匹配页面可见正文 | 标准 | Google 结构化数据指南 | 防止 schema 虚构事实 | 高 |
| 没有 AI 平台采样时不能判断召回、排名或引用份额 | 研究/方法 | yao-geo-page-audit 方法论 | 避免把页面准备度误写成平台表现 | 高 |

## 7. 抓取与渲染诊断

观察：

- `www.zzgl.cn` 和 `zzgl.cn` 均能解析到公网 IP。
- `https://www.zzgl.cn/` 的 HEAD 请求出现 HTTP/2 stream 内部错误。
- `https://www.zzgl.cn/` 使用 HTTP/1.1 请求时出现空响应。
- `http://www.zzgl.cn/` 返回 nginx `444`。
- `robots.txt` 和 `sitemap.xml` 请求出现空响应。
- `https://m.zzgl.cn/chanpinzhongxin/` 复测超时。

影响：

- 这不等于搜索引擎或 AI 平台一定抓不到，但说明非典型客户端、无 Cookie 客户端或部分抓取器可能遇到候选获取失败。
- `robots.txt` 和 `sitemap.xml` 不稳定会削弱发现入口质量。

行动：

```bash
URL="https://www.zzgl.cn/"
curl -I --http1.1 -L "$URL"
curl -I --http2 -L "$URL"
curl -L "https://www.zzgl.cn/robots.txt"
curl -L "https://www.zzgl.cn/sitemap.xml"
```

验收：

- 首页、产品中心、robots、sitemap 在无 Cookie、普通 User-Agent 下返回 200 或合理 3xx。
- HTTPS/HTTP2/HTTP1.1 均不出现空响应、444、stream error。
- 移动端 URL 能稳定返回可读内容或明确 301 到 canonical URL。

## 8. 结构规范性诊断

首页快照：

- title：存在。
- meta description：存在，约 51 字。
- canonical：存在。
- H1：1 个，为“中正锅炉”。
- H2：4 个，覆盖产品系列、行业解决方案、服务支持、联系方式。
- main：存在。
- JSON-LD：未观察到。
- 表格：未观察到。
- FAQ：未观察到。
- 可见正文长度：约 267 字。

产品中心快照：

- title：存在。
- meta description：存在，约 54 字。
- canonical：存在。
- H1：1 个，为“锅炉产品中心”。
- H2：6 个，覆盖燃油/燃气、燃煤、生物质、导热油、循环流化床、询价与联系。
- main：存在。
- JSON-LD：未观察到。
- 表格：未观察到。
- FAQ：未观察到。
- 可见正文长度：约 396 字。

判断：

- 结构骨架可用，但页面仍偏“分类展示”，没有把参数、证据、选型边界做成机器可稳定抽取的模块。

## 9. 内容证据诊断

已有正向信号：

- 品牌实体明确。
- 产品大类明确。
- 联系电话和地址可作为组织实体辅助信息。

主要缺口：

- 缺少产品系列的统一参数表。
- 缺少产品手册、检测报告、案例页或资料下载作为引用来源。
- 缺少更新时间、审核人或资料版本。
- 缺少产品适用边界和不适用边界。
- 缺少对“锅炉选型”“供应商比较”“询价准备”的官方问答。

内容改造方向：

1. 首屏摘要：80-120 字说明中正锅炉是谁、产品覆盖什么、适合哪些场景。
2. 产品事实表：每类锅炉使用相同字段。
3. 选型 FAQ：按采购、设备、项目负责人问题组织。
4. 来源说明：每个参数和案例绑定资料来源。
5. 更新时间：每个页面或资料模块保留审核时间。

## 10. AI 可抽取性诊断

当前页面对 AI 可抽取性的主要阻力：

- 原子事实少：例如“哪类锅炉适合什么行业”没有拆成独立事实。
- 键值对少：容量、压力、燃料、排放、效率等没有统一字段。
- 对比表缺失：不利于回答“燃气锅炉和生物质锅炉哪个好”。
- FAQ 缺失：不利于回答采购前常见问题。
- chunk 引用准备不足：段落没有清晰来源、更新时间、锚点或资料链接。

建议新增模块：

```html
<section id="product-summary">
  <h2>中正锅炉产品中心概览</h2>
  <p>中正锅炉产品中心覆盖燃油燃气锅炉、燃煤锅炉、
  生物质锅炉、导热油锅炉和循环流化床锅炉，面向
  工业供热、蒸汽、热水及导热油等应用场景。</p>
</section>

<section id="selection-faq">
  <h2>锅炉选型常见问题</h2>
  <h3>询价前需要准备哪些工况参数？</h3>
  <p>建议准备燃料类型、额定蒸发量或热功率、压力、
  温度、排放要求、使用行业、运行时间和安装地区。</p>
</section>
```

## 11. Schema 一致性建议

快照中未观察到 JSON-LD。建议优先补充 `Organization`、`WebPage`、`BreadcrumbList`，在 FAQ 正文上线后再补 `FAQPage`。

示例只应使用页面可见事实：

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "中正锅炉",
  "url": "https://www.zzgl.cn/",
  "telephone": "13506151202",
  "address": {
    "@type": "PostalAddress",
    "addressRegion": "江苏",
    "addressLocality": "无锡宜兴",
    "streetAddress": "周铁镇新达路76号"
  }
}
```

验收：

- schema 字段都能在页面可见正文或官方资料中回溯。
- 使用 Schema.org validator 和 Google Rich Results Test 复测。
- 不把未在正文出现的热效率、排放、案例、价格写入 schema。

## 12. 移动端与性能

本轮限制：

- 未获得稳定移动端 HTML。
- 未运行 PageSpeed、Lighthouse 或 Web Vitals。

风险：

- 如果移动端内容少于桌面端，移动优先索引和 AI 抽取可能拿不到完整产品事实。
- 如果产品参数通过懒加载或客户端 JS 后置加载，部分抓取器可能只看到空容器。

复测建议：

```bash
URL="https://www.zzgl.cn/chanpinzhongxin/"
npx lighthouse "$URL" --preset=desktop
npx lighthouse "$URL" --preset=mobile
```

验收：

- 移动端和桌面端都有相同的核心正文、标题、meta、schema 和产品参数。
- 首屏主要内容不依赖用户交互后才加载。
- LCP、INP、CLS 有明确监测结果。

## 13. 修复清单

### P0：修复可抓取性异常

问题：本地请求出现 HTTP/2 stream 错误、空响应、HTTP 444、robots/sitemap 空响应。  
证据：本地 curl、DNS、HTTP 复测。  
影响：可能阻断部分抓取器进入发现入口和检索候选阶段。  
动作：检查 nginx、WAF、防盗链、User-Agent 策略、HTTP/2 配置、robots/sitemap 路由。  
负责人：技术/运维。  
成本：中。  
验收：无 Cookie curl 可稳定返回 200/3xx，robots/sitemap 可访问。

### P1：重构产品中心首屏与参数表

问题：产品大类可识别，但缺少统一参数、适用行业、资料来源。  
证据：产品中心快照有 H2 分类，但无表格和来源模块。  
影响：不利于 AI 回答“产品有哪些”“怎么选”“适合什么场景”。  
动作：新增首屏摘要、产品事实表、资料链接、更新时间。  
负责人：产品/内容/CMS。  
成本：中。  
验收：每类锅炉至少有 8 个统一字段，并绑定来源链接。

### P1：新增选型 FAQ

问题：快照中没有 FAQ 问答。  
证据：FAQ-like 问号数量为 0。  
影响：不利于生成式引擎直接回答高意图问题。  
动作：新增 8-12 个选型问答，覆盖燃料、容量、压力、排放、行业、询价准备。  
负责人：产品/销售工程师/内容。  
成本：低到中。  
验收：FAQ 正文上线，问题能独立回答，答案引用资料来源。

### P1：补充 schema

问题：快照中未观察到 JSON-LD。  
证据：HTML 快照 json-ld count 为 0。  
影响：实体、面包屑和 FAQ 结构化信号不足。  
动作：补 `Organization`、`WebPage`、`BreadcrumbList`，FAQ 上线后补 `FAQPage`。  
负责人：前端/SEO。  
成本：低。  
验收：结构化数据校验通过，字段均可在正文回溯。

### P2：建立公开资料和案例证据库

问题：页面缺少产品手册、案例页、检测报告、版本日期。  
证据：快照未观察到来源、参考、更新、检测等证据语言。  
影响：引用源质量不足，难支撑高置信回答。  
动作：建立资料下载页、行业案例页、参数说明页、更新记录。  
负责人：产品/技术文档/销售工程师。  
成本：中到高。  
验收：关键参数和案例均有官方页面或 PDF 资料支撑。

## 14. 产品中心推荐信息架构

1. 首屏摘要：中正锅炉是谁、产品覆盖什么、服务哪些行业。
2. 产品系列导航：燃油燃气、燃煤、生物质、导热油、循环流化床。
3. 产品参数总表：统一字段和筛选入口。
4. 选型流程：工况收集、方案匹配、报价、安装、售后。
5. 行业方案：食品、化工、制药、造纸、学校宾馆等。
6. 选型 FAQ：面向采购和设备负责人的真实问题。
7. 证据与来源：产品手册、案例、报告、更新时间。
8. 联系与询价：热线、表单、地址、服务边界。

## 15. 质量报告摘要

| 自检项 | 状态 | 说明 |
|---|---|---|
| 范围完整 | 通过 | 覆盖首页、一级产品中心，并标出二级页输入缺口 |
| 证据完整 | 通过 | 关键结论标记观察、官方、标准、研究、推断或缺口 |
| 技术完整 | 通过 | 覆盖抓取、渲染、移动、结构、schema、性能风险 |
| 内容完整 | 通过 | 覆盖实体、事实、来源、时间、服务边界、FAQ |
| AI 完整 | 通过 | 覆盖抽取、chunk、问答、引用准备度和公开答案素材 |
| 平台表现边界 | 通过 | 未写平台召回、排名、答案频次或引用份额 |

## 16. 参考来源

- [yao-geo-skills GitHub 仓库](https://github.com/yaojingang/yao-geo-skills)
- [yao-geo-page-audit SKILL.md](https://raw.githubusercontent.com/yaojingang/yao-geo-skills/main/skills/yao-geo-page-audit/SKILL.md)
- [页面 GEO 诊断研究依据](https://raw.githubusercontent.com/yaojingang/yao-geo-skills/main/skills/yao-geo-page-audit/references/research-foundation.md)
- [权威参考与证据分层](https://raw.githubusercontent.com/yaojingang/yao-geo-skills/main/skills/yao-geo-page-audit/references/authority-reference-model.md)
- [页面 GEO 诊断质量门](https://raw.githubusercontent.com/yaojingang/yao-geo-skills/main/skills/yao-geo-page-audit/references/quality-gates.md)
- [中正锅炉官网首页](https://www.zzgl.cn/)
- [中正锅炉产品中心](https://www.zzgl.cn/chanpinzhongxin/)

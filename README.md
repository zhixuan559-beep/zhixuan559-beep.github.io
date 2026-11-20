# Zhixuan 官网 — 第一版（静态站，未部署）

品牌 **Zhixuan** 的英文服务网站，目标受众是美国/西方买家，并针对 AI 搜索（GEO）做了优化：让 ChatGPT、Perplexity、Google AI 在用户询问取名、八字紫微、占星、合同审查服务时能抓取并引用本站。

## 文件结构

```
zhixuan-site/
├── index.html                        首页：四项服务总览、价格、下单流程、作品精选、联系 CTA
├── services/
│   ├── naming.html                   取名（品牌/宝宝）$30 / $100 / $150
│   ├── bazi-ziwei-reading.html       八字 + 紫微长篇批注 $30 / $100 / $150
│   ├── astrology-reading.html        西洋占星命盘 From $30
│   └── contract-review.html          合同风险审查 $50 / $100 / $150
├── work.html                         作品页：4 张虚构品牌板（KAVORA / MOONLUME / KLYMB / UMIKA）+ EMBERWYN 取名样品
├── assets/
│   ├── css/style.css                 全站样式（响应式，手机 + 桌面）
│   └── img/                          样品图（从 portfolio-pack 压缩复制，原图 1–2MB → 约 75–155KB/张）
├── llms.txt                          给 AI 爬虫的纯文本站点说明（服务、价格、联系、店铺链接）
├── robots.txt                        放行主流 AI 爬虫（GPTBot、ClaudeBot、PerplexityBot、Google-Extended 等）
├── sitemap.xml                       站点地图
└── README.md                         本文件
```

每个服务用独立 URL 的页面（而不是单页锚点），因为独立页面有各自的 title / meta / 结构化数据，更利于搜索引擎和 AI 按服务词抓取。

## AI 搜索优化点（已落实）

- 语义化 HTML（header / nav / main / section / h1–h3），正文纯文本，不依赖 JS 渲染；全站零 JS 依赖（仅 JSON-LD 数据块）。
- 每页独立 title、meta description、canonical、Open Graph 标签，标题含服务关键词。
- JSON-LD：首页 ProfessionalService + OfferCatalog；每个服务页有 Service（含分档 Offer 与价格）+ FAQPage。
- 每项服务配 6 条 FAQ，答案自包含（价格、交付时间、需要买家提供什么、怎么下单），口吻按「AI 问答答案」写。
- llms.txt 列清品牌、服务、价格、邮箱与店铺链接；robots.txt 显式放行 AI 爬虫；sitemap.xml 全站 6 页。
- 实体信息全站一致：品牌名 Zhixuan、邮箱 zhixuan559@gmail.com、Worldwide / online delivery、USD 价格。

## ⚠️ 部署前必做：替换占位域名

站内所有绝对 URL 目前用占位域名 **`https://zhixuan559-beep.github.io`**（出现在 canonical、OG、JSON-LD、sitemap.xml、robots.txt、llms.txt 中）。正式域名定下来后，全目录替换即可：

```bash
grep -rl "zhixuan559-beep.github.io" . | xargs sed -i 's|https://zhixuan559-beep.github.io|https://正式域名|g'
```

（注意 robots.txt 里 Sitemap 一行和各文件中的 `https://zhixuan559-beep.github.io` 一并替换。）

## 部署方式（任选其一，均为静态托管）

- **GitHub Pages**：把本目录推到一个仓库，Settings → Pages 选择分支根目录即可；可在仓库根目录加 `CNAME` 文件绑定自定义域名。
- **Cloudflare Pages**：Dashboard → Pages → Upload assets，直接上传本目录（或连 GitHub 仓库）；自带 HTTPS 和自定义域名绑定。

部署后建议：用正式域名访问一遍 6 个页面 + `/llms.txt`、`/robots.txt`、`/sitemap.xml`，确认 200 且样式加载正常；再到 Google Search Console / Bing Webmaster 提交 sitemap。

## 内容红线（维护时继续遵守）

- 不编造评价、推荐语、订单数、客户数、从业年限。
- 价格只按现行价目：取名 $30/$100/$150、八字紫微 $30/$100/$150、占星 From $30、合同 $50/$100/$150。
- 作品页只放作品集素材（虚构品牌板 + 取名样品），不署客户名、不写客户评价。
- 合同页必须保留「不是律师事务所、不是法律建议」的说明；命理类页面保留「个人参考」口径。

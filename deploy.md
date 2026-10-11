# 作品页部署套件（Cloudflare Pages · 15 分钟上线）

> 周复盘决定：作品页直接选 **Cloudflare Pages**（不比较方案）。
> 本目录 = 完整静态站点：`index.html` + 4 份样张 PDF（`demo-01-hvac-v3.pdf` / `demo-02-dental.pdf` / `demo-03-ecommerce-support.pdf` / `demo-04-geo-monitor.pdf`）。

## Step 0 · 先替换 4 个占位符（2 分钟）

在 `index.html` 中查找并替换：

| 占位符 | 出现处 | 建议值 |
|---|---|---|
| `[Studio Name]` | 页头 / 标题 / 页脚 | `Jian · AI Studio`（或你的最终定名） |
| `[your@email]` | 头部 CTA 按钮 + 页脚（2 处） | 你常用的商务邮箱 |
| `[@yourhandle]` | 页脚 X 链接 | 你的 X 用户名 |
| `[微信号]` | 页脚 | 微信号（不留可整段删除） |

查找命令：`findstr /n "\[" index.html`

## Step 1 · 部署（三选一）

### 方案 A（推荐）· wrangler 一键部署（登录一次，之后一行命令）

```cmd
cd /d C:\Users\Administrator\opc\site
npx wrangler@latest pages deploy . --project-name=jian-ai-studio
```

- 首次运行会弹出浏览器要求登录 Cloudflare（账号：`jian1929@qq.com`）。
- 完成后返回形如 `https://jian-ai-studio.pages.dev` 的公网地址。
- 之后每次更新：同一条命令重跑即可（增量发布，秒级）。

### 方案 B · API Token 无人值守部署

1. Cloudflare Dashboard → My Profile → API Tokens → Create Token → 模板选 **Cloudflare Pages: Edit**；
2. 运行（Account ID 已知：`5f635a2c1f2e3595584ac2fdb54b2015`）：

```cmd
cd /d C:\Users\Administrator\opc\site
set CLOUDFLARE_API_TOKEN=<你的token>
set CLOUDFLARE_ACCOUNT_ID=5f635a2c1f2e3595584ac2fdb54b2015
npx wrangler@latest pages deploy . --project-name=jian-ai-studio
```

### 方案 C · 备选：挂到 jian1929.store（需在该服务器上操作）

把本目录整体拷到 jian1929.store 的静态目录（Lucky 反代已有），加一条路由即可。仅当方案 A/B 都不可用时用。

## Step 2 · 上线后 3 件事（3 分钟）

1. `offers\platform-copy.md` 里 2 处"[作品页链接]"替换为正式 URL；
2. `leads\leads.csv` 中"部署作品页"一行改 `已完成`，备注写上 URL；
3. 手机打开 URL 自检：4 个 PDF 链接可下载、页面无占位符残留。

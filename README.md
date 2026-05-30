# ClawBBA × OpenClaw — One-Key Access to 362+ AI Models

<p align="center">
  <strong>ClawBBA</strong> · Unified Platform API &nbsp;|&nbsp; <strong>OpenClaw</strong> · Personal AI Agent Runtime
</p>

<p align="center">
  <a href="https://www.clawbba.com">Website</a> ·
  <a href="https://www.clawbba.com/agent/api-keys">Get API Key</a> ·
  <a href="https://www.clawbba.com/downloads/clawbba-api-1.5.27.zip">Download Skill v1.5.27</a> ·
  <a href="https://clawhub.ai/clawbba-ux/clawbba-api">ClawHub</a> ·
  <a href="https://docs.openclaw.ai/">OpenClaw Docs</a>
</p>

<p align="center">
  🇺🇸 English · 🇨🇳 简体中文 · 🇯🇵 日本語 · 🇰🇷 한국어
</p>

<!-- Media: hosted on clawbba-ux/ClawBBA main branch -->
<p align="center">
  <a href="https://www.clawbba.com/agent/api-keys">
    <img src="https://raw.githubusercontent.com/clawbba-ux/ClawBBA/main/opencla_clawbba.png" alt="OpenClaw 一键接入 · ClawBBA × OpenClaw · 362+ 顶级大模型" width="480">
  </a>
</p>

<p align="center">
  <strong>OpenClaw 一键接入</strong> · 362+ models · GPT · Claude · Gemini · DeepSeek · Qwen<br/>
  <a href="https://www.clawbba.com/agent/api-keys"><strong>Get API Key → Install → Chat on WebChat / WeChat / Telegram</strong></a>
</p>

<p align="center">
  <video src="https://raw.githubusercontent.com/clawbba-ux/ClawBBA/refs/heads/main/wechat.mp4" controls width="480"></video>
  <br/>
  <sub>
    <a href="https://raw.githubusercontent.com/clawbba-ux/ClawBBA/refs/heads/main/wechat.mp4">▶ wechat.mp4</a>
    ·
    <a href="https://github.com/clawbba-ux/ClawBBA/blob/main/opencla_clawbba.png">opencla_clawbba.png</a>
  </sub>
</p>

---

## About

**ClawBBA** is a global AI model platform with an OpenAI-compatible API. **OpenClaw** is your local AI agent runtime (WebChat, tools, Gateway). Together they give you **one Platform API Key** to run **362+ frontier models** — GPT, Claude, Gemini, DeepSeek, Qwen, FLUX, Veo, and more — for **chat, image, and video**, from your own machine.

| | |
|---|---|
| **What you get** | Text chat · image generation · video generation · vision · async jobs |
| **Billing** | One ClawBBA account balance (same as the web Agent) |
| **Install** | 2 steps: create Key → one-line shell on your OpenClaw host |
| **Skill package** | [`clawbba-api-1.5.27.zip`](https://www.clawbba.com/downloads/clawbba-api-1.5.27.zip) |
| **Console** | [API Keys & OpenClaw guide](https://www.clawbba.com/agent/api-keys) |
| **Chat apps** | WebChat, WeChat, Telegram, WhatsApp, Discord, Slack, Feishu, QQ, and [20+ more OpenClaw channels](https://docs.openclaw.ai/channels) |
| **Demo video** | [wechat.mp4](https://raw.githubusercontent.com/clawbba-ux/ClawBBA/refs/heads/main/wechat.mp4) — WeChat ClawBot + ClawBBA |
| **Poster** | [opencla_clawbba.png](https://github.com/clawbba-ux/ClawBBA/blob/main/opencla_clawbba.png) |

> **Brand rule:** End users see **ClawBBA** only. The skill wires OpenClaw internally; you never need separate vendor API keys.

> **Prerequisite for all channels:** Complete [Quick Start](#quick-start-2-steps) (ClawBBA Key + `clawbba-api` install) **before** binding messengers. Every channel uses the same Gateway and **362+ models**.

---

## Quick Start (2 Steps)

### Step 1 — Create your Platform API Key

1. Sign in at [clawbba.com](https://www.clawbba.com)
2. Top up balance: [CDKey recharge](https://www.clawbba.com/product/CDKEY)
3. Open **[API Keys → OpenClaw 一键接入](https://www.clawbba.com/agent/api-keys)**
4. Click **Create API Key**, copy the full secret (`cbb_sk_live_…`) — **shown once only**

### Step 2 — One-line install on your OpenClaw machine

Requirements: **Node.js 18+**, **OpenClaw CLI**, `curl`, `unzip`.

```bash
export CLAWBBA_API_KEY='cbb_sk_live_YOUR_FULL_KEY'
curl -fsSL https://www.clawbba.com/downloads/install-clawbba-api.sh | bash
```

The script will:

- Download [`clawbba-api-1.5.27.zip`](https://www.clawbba.com/downloads/clawbba-api-1.5.27.zip)
- Install to `~/.openclaw/skills/clawbba-api`
- Validate your Key against `https://www.clawbba.com/api/v1`
- Merge **362+ models** into `openclaw.json` + `models.json`
- Apply runtime patches (WebChat live media, image/video delivery, recover, etc.)
- Restart OpenClaw Gateway (unless `SKIP_GATEWAY_RESTART=1`)

**Verify:**

```bash
openclaw config validate
openclaw models list | grep clawbba
node ~/.openclaw/skills/clawbba-api/scripts/verify-openclaw-runtime.mjs
```

Open a **new WebChat session**, then:

```
/model clawbba/google/gemini-2.5-flash-preview
```

---

## Install Package: `clawbba-api-1.5.27.zip`

| Item | Detail |
|------|--------|
| **Download** | https://www.clawbba.com/downloads/clawbba-api-1.5.27.zip |
| **Install script** | https://www.clawbba.com/downloads/install-clawbba-api.sh (default version **1.5.27**) |
| **Install path** | `~/.openclaw/skills/clawbba-api` (override: `OPENCLAW_SKILL_DIR`) |
| **License** | MIT-0 |

### Manual install (offline / air-gapped)

```bash
export CLAWBBA_API_KEY='cbb_sk_live_YOUR_FULL_KEY'
export OPENCLAW_SKILL_DIR="$HOME/.openclaw/skills/clawbba-api"
unzip clawbba-api-1.5.27.zip -d "$OPENCLAW_SKILL_DIR"
cd "$OPENCLAW_SKILL_DIR"
./scripts/verify-key.sh
./scripts/one-shot-setup.sh
bash scripts/ensure-openclaw-patches.sh --install
openclaw gateway restart
```

### Alternative: ClawHub / OpenClaw CLI

```bash
# ClawHub
npm i -g clawhub && clawhub install clawbba-api --no-input

# OpenClaw CLI
openclaw skills install clawbba-api

export CLAWBBA_API_KEY='cbb_sk_live_YOUR_FULL_KEY'
cd ~/.openclaw/skills/clawbba-api && ./scripts/one-shot-setup.sh
openclaw gateway restart
```

ClawHub: [clawbba-ux/clawbba-api](https://clawhub.ai/clawbba-ux/clawbba-api)

### What the package contains

```
clawbba-api/
├── SKILL.md                 # OpenClaw skill manifest (always-on agent rules)
├── scripts/
│   ├── install.sh           # Used by public install-clawbba-api.sh
│   ├── one-shot-setup.sh    # Writes openclaw.json + provider fixups
│   ├── patch-openclaw-media-delivery.mjs
│   ├── verify-openclaw-runtime.mjs
│   └── verify-openclaw-patch.mjs
└── references/              # Integration specs, error translation, model tables
```

---

## Usage

### Text chat (362+ LLMs)

```
/model clawbba/<platform-model-id>
```

Examples: `clawbba/anthropic/claude-sonnet-4`, `clawbba/deepseek/deepseek-chat`, `clawbba/qwen/qwen3-235b-a22b`

List models:

```bash
openclaw models list
/tool image_generate action=list    # image providers
/tool video_generate action=list    # video providers
```

### Image generation (WebChat)

Default (uses setup default model):

```
请使用 ClawBBA 生成图片能力，为我生成 9:16 竖图：赛博朋克城市夜景，霓虹灯与雨雾，电影感构图
```

With model:

```
请使用 ClawBBA 生成图片能力，模型 black-forest-labs/flux.2-pro，为我生成 16:9 横图：（your prompt）
```

After completion, the agent delivers **`MEDIA:/root/.openclaw/media/tool-image-generation/…`** in the assistant reply (local file on your OpenClaw machine).

### Video generation

```
请使用 ClawBBA 生成视频能力，模型 google/veo-3.1-fast，为我生成 16:9、8 秒视频：海浪拍打礁石，电影感航拍
```

**Recover** (completed job, no re-billing):

```
/tool video_generate action=recover jobId=<video_job_id> timeoutMs=600000
```

### API (direct HTTP)

Base URL: `https://www.clawbba.com/api/v1`

```bash
curl https://www.clawbba.com/api/v1/chat/completions \
  -H "Authorization: Bearer $CLAWBBA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"google/gemini-2.5-flash-preview","messages":[{"role":"user","content":"Hello"}]}'
```

Full endpoint list: see skill `references/api-endpoints.md` or the **接口文档** tab on the [API Keys page](https://www.clawbba.com/agent/api-keys).

---

## Chat from anywhere — IM channels

After **ClawBBA + clawbba-api** is installed, connect **any supported messenger** to the same OpenClaw Gateway. You chat on WhatsApp / WeChat / Telegram / … — the agent runs **362+ ClawBBA models** on your server.

```
Phone / Desktop IM app          OpenClaw Gateway (your server)          ClawBBA API
──────────────────────          ─────────────────────────────          ───────────
WeChat / Telegram / …    ──►    Agent + clawbba-api skill      ──►    362+ models
WebChat (browser)        ──►    image_generate / video_generate
```

Official channel list: [docs.openclaw.ai/channels](https://docs.openclaw.ai/channels)

### Supported messengers (OpenClaw)

| Category | Channels | Setup doc |
|----------|----------|-----------|
| **Built-in Web UI** | **WebChat** | Open Gateway URL in browser (best for image/video `MEDIA:` preview) |
| **China / 华语** | **WeChat** (微信), **Feishu** (飞书), **QQ** | [WeChat](https://docs.openclaw.ai/channels/wechat) · Feishu bundled plugin |
| **Global — fast setup** | **Telegram**, **Discord**, **Slack** | [Telegram](https://docs.openclaw.ai/channels/telegram) · [Discord](https://docs.openclaw.ai/channels/discord) · [Slack](https://docs.openclaw.ai/channels/slack) |
| **Global — mobile** | **WhatsApp**, **Signal**, **iMessage**, **LINE**, **Zalo** | [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) · [Channels index](https://docs.openclaw.ai/channels) |
| **Work / team** | **Microsoft Teams**, **Google Chat**, **Matrix**, **Mattermost** | [Channels index](https://docs.openclaw.ai/channels) |
| **More** | IRC, Nostr, Twitch, Synology Chat, Nextcloud Talk, Tlon, … | [openclaw/openclaw](https://github.com/openclaw/openclaw) |

Multiple channels can run **at the same time**; OpenClaw routes by chat session.

> **Tip:** `clawbba-api` **v1.5.12+** optimizes **WebChat** live image/video delivery (no refresh). Other channels deliver text natively; rich media behavior follows each channel’s OpenClaw plugin.

---

### WebChat (browser — recommended for media)

1. Install ClawBBA skill ([Quick Start](#quick-start-2-steps))
2. Start Gateway: `openclaw gateway` or `openclaw gateway restart`
3. Open the **WebChat / Control UI** URL shown by OpenClaw (local or your public Gateway)
4. New session → `/model clawbba/<model-id>` or send ClawBBA image/video prompts

---

### WeChat 微信 — ClawBot plugin (WebChat UI)

Tencent official plugin: [`@tencent-weixin/openclaw-weixin`](https://docs.openclaw.ai/channels/wechat)

#### A. Install from WebChat (easiest)

1. Complete **ClawBBA Key + clawbba-api** install first
2. Open **WebChat** → **我的** → **设置** → **插件**
3. Open **微信 ClawBot** → **详情**
4. **Copy install command** and run on the **Gateway host**:

```bash
npx -y @tencent-weixin/openclaw-weixin-cli@latest install
```

5. **Copy the bind URL** from the plugin page → open in browser → **scan QR with WeChat** on your phone → confirm login
6. `openclaw gateway restart`
7. Approve first DM if pairing is enabled:

```bash
openclaw pairing list openclaw-weixin
openclaw pairing approve openclaw-weixin <CODE>
```

8. Chat in **WeChat** — same ClawBBA models as WebChat (`/model clawbba/…` or natural language)

#### B. Install from terminal (same result)

```bash
npx -y @tencent-weixin/openclaw-weixin-cli@latest install
# or:
openclaw plugins install "@tencent-weixin/openclaw-weixin"
openclaw config set plugins.entries.openclaw-weixin.enabled true
openclaw channels login --channel openclaw-weixin   # QR scan
openclaw gateway restart
```

Docs: [OpenClaw WeChat channel](https://docs.openclaw.ai/channels/wechat)

#### Demo · 效果演示

<p align="center">
  <img src="https://raw.githubusercontent.com/clawbba-ux/ClawBBA/main/opencla_clawbba.png" alt="OpenClaw 一键接入 poster" width="320">
  &nbsp;
  <video src="https://raw.githubusercontent.com/clawbba-ux/ClawBBA/refs/heads/main/wechat.mp4" controls width="320"></video>
</p>

| Asset | Link |
|-------|------|
| **Video** | https://raw.githubusercontent.com/clawbba-ux/ClawBBA/refs/heads/main/wechat.mp4 |
| **Poster (view)** | https://github.com/clawbba-ux/ClawBBA/blob/main/opencla_clawbba.png |
| **Poster (raw)** | https://raw.githubusercontent.com/clawbba-ux/ClawBBA/main/opencla_clawbba.png |

Recording covers: create Key → install → WebChat plugin → WeChat QR bind → chat with ClawBBA models in WeChat.

---

### Telegram (fast global setup)

1. Create bot via [@BotFather](https://t.me/BotFather) → `/newbot` → save token
2. Add to `~/.openclaw/openclaw.json`:

```json5
{
  channels: {
    telegram: {
      enabled: true,
      botToken: "YOUR_BOT_TOKEN",
      dmPolicy: "pairing",
    },
  },
}
```

3. `openclaw gateway restart`
4. `openclaw pairing list telegram` → `openclaw pairing approve telegram <CODE>`

Doc: [docs.openclaw.ai/channels/telegram](https://docs.openclaw.ai/channels/telegram)

---

### WhatsApp

1. `openclaw channels login whatsapp` (QR pairing on Gateway host)
2. `openclaw gateway restart`

Doc: [docs.openclaw.ai/channels/whatsapp](https://docs.openclaw.ai/channels/whatsapp)

---

### Discord / Slack

1. Create bot app in Discord Developer Portal / Slack API
2. Paste bot token under `channels.discord` or `channels.slack` in config
3. `openclaw gateway restart` · configure `allowFrom` / pairing as needed

Docs: [Discord](https://docs.openclaw.ai/channels/discord) · [Slack](https://docs.openclaw.ai/channels/slack)

---

### Feishu 飞书 / Lark

Feishu/Lark bot via WebSocket (bundled OpenClaw plugin). Configure app credentials in OpenClaw channel settings, then restart Gateway.

Doc: [docs.openclaw.ai/channels](https://docs.openclaw.ai/channels) (Feishu section)

---

### QQ

Supported as an OpenClaw channel (see [OpenClaw channel list](https://github.com/openclaw/openclaw)). Install the channel plugin per OpenClaw docs, then bind and restart Gateway.

---

### First-time channel wizard

```bash
openclaw onboard          # interactive setup
openclaw channels status --probe
openclaw gateway restart
```

---

## Architecture

```
Your WebChat / Agent
       ↓
OpenClaw Gateway
  ├─ clawbba/<id>     → POST /api/v1/chat/completions   (text + vision)
  └─ image_generate / video_generate
         → models.providers.openrouter (baseUrl = clawbba.com)
         → ClawBBA Platform API
       ↓
Files saved locally: ~/.openclaw/media/
Delivered via MEDIA: lines in assistant reply
```

| Layer | Role |
|-------|------|
| **ClawBBA** | Auth, billing, 362+ model catalog, image/video APIs |
| **clawbba-api skill** | Platform Key, config merge, OpenClaw runtime patches |
| **OpenClaw** | Agent, tools, WebChat, Gateway, local media storage |

---

## Systemd (production Gateway)

```bash
sudo mkdir -p /etc/systemd/system/openclaw-gateway.service.d
sudo tee /etc/systemd/system/openclaw-gateway.service.d/clawbba.conf <<EOF
[Service]
Environment=CLAWBBA_API_KEY=cbb_sk_live_YOUR_FULL_KEY
Environment=OPENROUTER_API_KEY=cbb_sk_live_YOUR_FULL_KEY
EOF
sudo systemctl daemon-reload
sudo systemctl restart openclaw-gateway
```

---

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| `402` / insufficient balance | [Recharge CDKey](https://www.clawbba.com/product/CDKEY) |
| `403 Your request was blocked` in WebChat | Re-run install; check `models.json` has real Key (not `${CLAWBBA_API_KEY}` placeholder) |
| Only 1 model in OpenClaw | `./scripts/one-shot-setup.sh` then `openclaw gateway restart` |
| Image/video not visible until refresh | Upgrade to **≥ 1.5.12**; re-run `install-clawbba-api.sh` |
| `No image-generation provider registered for clawbba` | Use `image_generate` with platform id in user message; never `clawbba/` prefix on image tools |
| Video timeout | `action=recover jobId=… timeoutMs=600000` — do not regenerate |

Diagnostics:

```bash
export CLAWBBA_API_KEY='cbb_sk_live_…'
bash ~/.openclaw/skills/clawbba-api/scripts/ensure-openclaw-patches.sh --install
node ~/.openclaw/skills/clawbba-api/scripts/verify-openclaw-runtime.mjs
```

More: `references/error-translation.md` inside the skill package.

---

## Changelog (v1.5.27 highlights)

- User-facing model labels show **ClawBBA/vendor/model** (not internal provider names)
- WebChat live inject for image/video/recover (no browser refresh)
- `video_generate action=recover` + `action=tasks`
- Vision text models for chat-with-image upload
- Install verify script stability fixes

Full log: [packages/clawbba-api/README.md](../packages/clawbba-api/README.md) (monorepo) or `README.md` inside the zip.

---

---

# 简体中文

## 简介

**ClawBBA** 是全球 AI 模型平台，提供 OpenAI 兼容 API。**OpenClaw** 是本地 AI Agent 运行时。二者联合：**一个 Platform API Key**，在 OpenClaw 上使用 **362+ 顶级大模型**（GPT、Claude、Gemini、DeepSeek、Qwen、FLUX、Veo 等），支持**对话、生图、生视频**。

| 项目 | 说明 |
|------|------|
| 控制台 | [API 密钥 · OpenClaw 一键接入](https://www.clawbba.com/agent/api-keys) |
| 安装包 | [clawbba-api-1.5.27.zip](https://www.clawbba.com/downloads/clawbba-api-1.5.27.zip) |
| 计费 | 与网页 Agent 共用 ClawBBA 账户余额 |
| 聊天渠道 | WebChat、微信、Telegram、WhatsApp、Discord、Slack、飞书、QQ 等 [20+ 通道](https://docs.openclaw.ai/channels) |
| 演示视频 | [wechat.mp4](https://raw.githubusercontent.com/clawbba-ux/ClawBBA/refs/heads/main/wechat.mp4) |
| 介绍海报 | [opencla_clawbba.png](https://github.com/clawbba-ux/ClawBBA/blob/main/opencla_clawbba.png) |

## 两步接入

### ① 创建 API Key

1. 登录 [clawbba.com](https://www.clawbba.com)
2. 充值：[CDKey](https://www.clawbba.com/product/CDKEY)
3. 打开 [API 密钥](https://www.clawbba.com/agent/api-keys) → **创建 API Key**
4. 复制完整密钥（`cbb_sk_live_…`，**仅显示一次**）

### ② 一键安装

在 OpenClaw 机器终端执行：

```bash
export CLAWBBA_API_KEY='cbb_sk_live_你的完整密钥'
curl -fsSL https://www.clawbba.com/downloads/install-clawbba-api.sh | bash
```

安装完成后 **新开 WebChat 对话**。

## 使用示例

**文本对话：**

```
/model clawbba/google/gemini-2.5-flash-preview
```

**生图（默认模型）：**

```
请使用 ClawBBA 生成图片能力，为我生成 9:16 竖图：（画面描述）
```

**生图（指定模型）：**

```
请使用 ClawBBA 生成图片能力，模型 black-forest-labs/flux.2-pro，为我生成 16:9 横图：（画面描述）
```

**生视频：**

```
请使用 ClawBBA 生成视频能力，模型 google/veo-3.1-fast，为我生成 16:9、8 秒视频：（画面描述）
```

生图/生视频完成后，Agent 在回复中使用 **`MEDIA:本地路径`** 交付（文件保存在本机 `~/.openclaw/media/`）。

## 即时通讯 · 全渠道使用 362+ 模型

先完成 **ClawBBA Key + clawbba-api 安装**，再绑定任意 OpenClaw 支持的聊天软件。你在微信 / Telegram / WhatsApp 里发消息，Gateway 上的 Agent 调用 **同一套 ClawBBA 362+ 模型**。

| 类型 | 渠道 |
|------|------|
| 浏览器 | **WebChat**（生图/生视频预览体验最佳） |
| 华语 | **微信**、**飞书**、**QQ** |
| 国际常用 | **Telegram**、**WhatsApp**、**Discord**、**Slack**、**Signal**、**LINE** |
| 企业 | **Microsoft Teams**、**Google Chat**、**Matrix** 等 |

完整列表：[OpenClaw Channels](https://docs.openclaw.ai/channels)

### WebChat

安装 clawbba-api 后 → `openclaw gateway restart` → 浏览器打开 Gateway 的 WebChat 地址 → 新开会话即可。

### 微信 · ClawBot 插件（推荐华语用户）

1. 先完成 [API 密钥](https://www.clawbba.com/agent/api-keys) 一键安装  
2. 打开 **WebChat** → **我的** → **设置** → **插件**  
3. 进入 **微信 ClawBot** → **详情**  
4. **复制安装命令**，在 Gateway 所在机器执行：

```bash
npx -y @tencent-weixin/openclaw-weixin-cli@latest install
```

5. **复制绑定网址** → 浏览器打开 → **微信扫码**确认  
6. `openclaw gateway restart`  
7. 如需配对：`openclaw pairing approve openclaw-weixin <CODE>`

官方文档：[WeChat 通道](https://docs.openclaw.ai/channels/wechat)

**效果演示：**

<p align="center">
  <img src="https://raw.githubusercontent.com/clawbba-ux/ClawBBA/main/opencla_clawbba.png" alt="OpenClaw 一键接入" width="300">
  &nbsp;
  <video src="https://raw.githubusercontent.com/clawbba-ux/ClawBBA/refs/heads/main/wechat.mp4" controls width="300"></video>
</p>

- 演示视频：[wechat.mp4](https://raw.githubusercontent.com/clawbba-ux/ClawBBA/refs/heads/main/wechat.mp4)  
- 介绍海报：[opencla_clawbba.png](https://github.com/clawbba-ux/ClawBBA/blob/main/opencla_clawbba.png)

### Telegram（海外最快）

1. @BotFather 创建 Bot → 获取 token  
2. 写入 `openclaw.json` 的 `channels.telegram`  
3. `openclaw gateway restart` → `openclaw pairing approve telegram <CODE>`

### WhatsApp / Discord / Slack

按 [OpenClaw 官方频道文档](https://docs.openclaw.ai/channels) 配置 token 或 QR 登录后重启 Gateway。

## 安装包说明

| 文件 | 地址 |
|------|------|
| ZIP | https://www.clawbba.com/downloads/clawbba-api-1.5.27.zip |
| 安装脚本 | https://www.clawbba.com/downloads/install-clawbba-api.sh |
| 技能目录 | `~/.openclaw/skills/clawbba-api` |

离线安装：解压 zip → `verify-key.sh` → `one-shot-setup.sh` → `ensure-openclaw-patches.sh --install` → `openclaw gateway restart`

## 常见问题

- **余额不足**：充值 CDKey
- **WebChat 403**：重跑一键安装，确认 Key 已写入 `models.json`
- **生图后需刷新**：升级到 1.5.27 并重装 patch
- **视频超时 recover**：`video_generate action=recover jobId=… timeoutMs=600000`，勿重新 generate
- **微信绑不上**：确认 Gateway 本机已执行 `npx -y @tencent-weixin/openclaw-weixin-cli@latest install` 并 `gateway restart`；扫码后执行 `openclaw pairing approve openclaw-weixin <CODE>`
- **多渠道**：WebChat / 微信 / Telegram 等可同时在线，共用同一套 ClawBBA 362+ 模型

---

# 日本語

## ClawBBA × OpenClaw 概要

**ClawBBA** はグローバル AI モデルプラットフォーム、**OpenClaw** はローカル AI エージェント実行環境です。**Platform API Key 1 本**で **362 以上のモデル**（GPT、Claude、Gemini、DeepSeek、Qwen など）を **チャット・画像・動画** に利用できます。

## 2 ステップで接続

### ① API Key を作成

1. [clawbba.com](https://www.clawbba.com) にログイン
2. [CDKey](https://www.clawbba.com/product/CDKEY) でチャージ
3. [API Keys](https://www.clawbba.com/agent/api-keys) で Key を作成（`cbb_sk_live_…`）

### ② ワンラインインストール

```bash
export CLAWBBA_API_KEY='cbb_sk_live_YOUR_KEY'
curl -fsSL https://www.clawbba.com/downloads/install-clawbba-api.sh | bash
```

パッケージ: [clawbba-api-1.5.27.zip](https://www.clawbba.com/downloads/clawbba-api-1.5.27.zip)

## 使用例

```
/model clawbba/google/gemini-2.5-flash-preview
```

画像生成:

```
请使用 ClawBBA 生成图片能力，为我生成 9:16 竖图：（説明）
```

（WebChat では中国語テンプレートがそのまま使えます。API Keys ページにコピー用例あり。）

## IM · チャットアプリから利用

clawbba-api インストール後、OpenClaw が対応する **WebChat / WeChat / Telegram / WhatsApp** 等から同じ **362+ モデル** を利用できます。

**WeChat（微信）:** WebChat → 我的 → 设置 → 插件 → 微信 ClawBot → 详情 →  
`npx -y @tencent-weixin/openclaw-weixin-cli@latest install` → URL を開いて QR スキャン  
[公式ドキュメント](https://docs.openclaw.ai/channels/wechat)

**Telegram:** BotFather で token → `channels.telegram` 設定 → `openclaw gateway restart`

詳細: [OpenClaw Channels](https://docs.openclaw.ai/channels)

---

# 한국어

## ClawBBA × OpenClaw 소개

**ClawBBA**는 글로벌 AI 모델 플랫폼, **OpenClaw**는 로컬 AI 에이전트 런타임입니다. **Platform API Key 하나**로 **362개 이상의 모델**(GPT, Claude, Gemini, DeepSeek, Qwen 등)을 **채팅·이미지·비디오**에 사용할 수 있습니다.

## 2단계 연동

### ① API Key 생성

1. [clawbba.com](https://www.clawbba.com) 로그인
2. [CDKey](https://www.clawbba.com/product/CDKEY) 충전
3. [API Keys](https://www.clawbba.com/agent/api-keys)에서 Key 생성

### ② 원라인 설치

```bash
export CLAWBBA_API_KEY='cbb_sk_live_YOUR_KEY'
curl -fsSL https://www.clawbba.com/downloads/install-clawbba-api.sh | bash
```

패키지: [clawbba-api-1.5.27.zip](https://www.clawbba.com/downloads/clawbba-api-1.5.27.zip)

## IM · 메신저에서 사용

clawbba-api 설치 후 **WebChat / WeChat / Telegram / WhatsApp** 등 OpenClaw 지원 채널에서 **362+ 모델**을 동일하게 사용합니다.

**WeChat（微信）:** WebChat → 我的 → 设置 → 插件 → 微信 ClawBot →  
`npx -y @tencent-weixin/openclaw-weixin-cli@latest install` → URL 열고 QR 스캔  
[WeChat 채널 문서](https://docs.openclaw.ai/channels/wechat)

**Telegram:** @BotFather → token → `channels.telegram` → Gateway 재시작

전체 채널: [docs.openclaw.ai/channels](https://docs.openclaw.ai/channels)

---

## Repository structure (this repo)

| Path | Description |
|------|-------------|
| `clawbba-api/` or skill zip | OpenClaw skill — install, patch, references |
| `docs/` | Platform & integration documentation |
| Releases | Attach `clawbba-api-x.y.z.zip` or link to clawbba.com/downloads |

**Related repositories**

- Skill on ClawHub: [clawbba-ux/clawbba-api](https://clawhub.ai/clawbba-ux/clawbba-api)
- OpenClaw: [docs.openclaw.ai](https://docs.openclaw.ai/)

---

## License

MIT-0 — see [LICENSE](./LICENSE) in this repository (same as [clawbba-api](https://www.clawbba.com/downloads/clawbba-api-1.5.27.zip) skill package).

---

## Links

| Resource | URL |
|----------|-----|
| 🌐 Website | https://www.clawbba.com |
| 🔑 API Keys & OpenClaw guide | https://www.clawbba.com/agent/api-keys |
| 📦 Skill zip v1.5.27 | https://www.clawbba.com/downloads/clawbba-api-1.5.27.zip |
| 📜 Install script | https://www.clawbba.com/downloads/install-clawbba-api.sh |
| 🦞 ClawHub skill | https://clawhub.ai/clawbba-ux/clawbba-api |
| 📖 OpenClaw docs | https://docs.openclaw.ai |
| 🎬 WeChat demo video | https://raw.githubusercontent.com/clawbba-ux/ClawBBA/refs/heads/main/wechat.mp4 |
| 🖼 Intro poster | https://github.com/clawbba-ux/ClawBBA/blob/main/opencla_clawbba.png |
| 💳 Recharge | https://www.clawbba.com/product/CDKEY |

<p align="center">
  <strong>ClawBBA × OpenClaw</strong><br/>
  One Key · 362+ Models · WebChat · WeChat · Telegram · Every IM App
</p>

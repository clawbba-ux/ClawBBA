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

> **Brand rule:** End users see **ClawBBA** only. The skill wires OpenClaw internally; you never need separate vendor API keys.

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

MIT-0 — see [LICENSE](../packages/clawbba-api/LICENSE) in the skill package.

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
| 💳 Recharge | https://www.clawbba.com/product/CDKEY |

<p align="center">
  <strong>ClawBBA × OpenClaw</strong><br/>
  One Key · 362+ Models · Chat · Image · Video · Global Access
</p>

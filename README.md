# FastClaw - LazyCat App

[FastClaw](https://github.com/fastclaw-ai/fastclaw)（轻量级 AI Agent 运行时）的懒猫微服（LazyCat）打包。

## 模式

- **SQLite 存储**：使用应用默认 SQLite（`$FASTCLAW_HOME/fastclaw.db`），无 Postgres 依赖，单容器部署。
- **镜像模式（mirror）**：`birdxs/fastclaw` 镜像经 `docker.1ms.run` 加速器拉取，`require_digest_match: true` 校验镜像内容与上游一致。
- **自动跟随上游**：每日检查上游 semver tag（`channel: custom` + `sort: semver`），发现新版本自动更新版本号与镜像、构建 LPK、发布商店。
- **喵喵商店发布**：仅私有商店（MiaoMiao private store），不发布官方商店。

## 说明

- 上游官方镜像在 GHCR（`ghcr.io/fastclaw-ai/fastclaw`）但未公开（匿名拉取被拒），Docker Hub `birdxs/fastclaw` 为社区同步镜像，滞后上游（当前 v1.1.0 vs 上游 v1.4.0），跟随该镜像源。
- 首次打开应用进入 onboard 向导创建超管账号；已配置免密登录（捕获 onboard 凭据、登录页自动填充）。
- 官方商店已有同名应用（`cloud.lazycat.app.fastclaw`），本包使用 `community.lazycat.app.fastclaw`。

## 结构

| 文件 | 说明 |
| --- | --- |
| `package.yml` | 包元数据（`community.lazycat.app.fastclaw`） |
| `lzc-manifest.yml` | 服务、路由与免密注入配置 |
| `lzc-build.yml` | 构建配置 |
| `icon.png` | 图标（上游 logo） |
| `.github/lazycat-action.yml` | [lazycat-github-action](https://github.com/ca-x/lazycat-github-action) 配置 |
| `.github/workflows/lazycat.yml` | 构建 + 发布工作流 |

## 所需 Secrets

| Secret | 说明 |
| --- | --- |
| `APPSTORE_URL` / `APPSTORE_TOKEN` | 喵喵商店 API 地址与发布令牌 |
| `APP_ID` | 可选 |
| `PRIVATE_STORE_GROUP_CODES` | 可选，私有分组码 |

## 许可

Apache-2.0（上游 LICENSE）

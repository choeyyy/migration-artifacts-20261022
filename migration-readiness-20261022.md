# 迁移准备报告（2026-10-22）

## 1. TikTok 项目上传 GitLab（新分支 `upload-current-20261022`）

已将当前 TikTok 项目完整工作树（含 docs/openspec/specs/wiki 等需求文档）上传到 GitLab 新分支：

- `xiaoshuo/drama/drama-mini` -> `upload-current-20261022`
- `xiaoshuo/drama/drama-backend` -> `upload-current-20261022`
- `xiaoshuo/drama/drama-admin` -> `upload-current-20261022`

GitLab SSH：`ssh://git@47.119.33.240:222`，使用 key `~/.ssh/gitlab_tiktok_ed25519`（账号 cenhuiying）。

说明：上传时遵循各项目 `.gitignore`，未包含 `node_modules/`、`dist/`、日志与缓存等生成物；源码与需求/设计文档已包含。

## 2. Codex Session 源文件打包

已打包本机 Codex 所有 session 源文件（主/子 session）：

- 文件：`/Users/mac/Documents/codex-sessions-20261022.zip`
- 内容：`~/.codex/sessions/`、`~/.codex/archived_sessions/`、`session_index.jsonl`
- 数量：173 个 session 文件；压缩包约 178 MB。

## 3. 本机本周活跃检查（迁移风险清单）

### 3.1 活跃产物 / 正在运行的服务
- Unity Editor 进程运行中（监听 `*:39000`），项目：`/Users/mac/Desktop/work/doupai-web`、`doupai-client`。
- 本地后端服务集群运行中（端口 `54057-54070`）：app-service、identity、content、media、trade、entitlement、data 等。
- MySQL 运行中（`127.0.0.1:35319`）。
- ADB 服务运行中（`127.0.0.1:5037`），但当前无已连接设备。
- ClashX 代理运行中（`7890/9090`）。
- Java 进程运行中（端口 `53616/53617`）。
- OpenCode / Codex 进程运行中。

迁移前建议：停止 Unity、本地后端集群、MySQL，确认无未保存场景/未提交改动；导出数据库 dump。

### 3.2 个人信息 / 凭证（需随迁移安全转移）
- SSH：`~/.ssh/gitlab_tiktok_ed25519`、`~/.ssh/id_rsa`（已过期，GitLab 提示 expired）、`known_hosts`。
- Git 配置：`~/.gitconfig`（user.name=mac，email 为空）。
- Codex 认证：`~/.codex/auth.json`（ChatGPT 登录态，含 token）。
- 飞书凭证：`~/.codex/tiktok-runtime-private/feishu-admin.json`（app_id/app_secret 明文）。
- 本地私有环境/SQL：`work/*-private.env`、`*-private.sql`、`private-profile-fixture.sql` 等（含连接信息）。
- 浏览器/系统：Chrome profile（`~/Library/Application Support/Google/Chrome`）、Keychain（`~/Library/Keychains`）、应用偏好设置。

### 3.3 本周活跃文件 / 目录（高变化）
- `/Users/mac/Documents/Codex`（本周大量修改，核心工作区，含 xiaoshuo 项目与交付物）。
- `/Users/mac/Desktop/work`（doupai-web/client Unity 项目，本周有改动）。
- `/Users/mac/.codex`（sessions、skills、plugins、sqlite 状态库）。
- `/Users/mac/go/pkg`、`~/.vscode/extensions`（工具链）。
- `/Users/mac/Downloads`（含 `tiktok-upload-20261021/Ep1.mp4`）。

### 3.4 迁移建议
- 先停止所有本地服务并导出 MySQL 数据与 Unity 项目改动。
- 将 SSH key、Codex auth、飞书凭证、私有 env/sql 通过安全渠道迁移，勿提交到 Git。
- Codex sessions 已打包为 zip，可直接迁移。
- TikTok 项目已上传 GitLab 新分支，迁移后 clone 即可。

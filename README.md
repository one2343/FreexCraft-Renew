# FreeXCraft 自动续期
自动登录 freexcraft.com，每2小时续期服务器。
流程：登录 → 续期 → 获取服务器信息 → TG 通知

---

## Secrets 配置

| Secret | 格式 | 说明 | 必填 |
|--------|------|------|------|
| `FXC_ACCOUNT` | `email,password` | 登录账号 | ✅ |
| `TG_BOT` | `chat_id,bot_token` | Telegram 通知 | ⬜ |
| `GOST_PROXY` | `socks5://user:pass@host:port` | 代理 | ⬜ |
| `PRIVATE_REPO_TOKEN` | GitHub PAT | 访问私库权限 | ✅ |

---

## 公共配置

这些值已硬编码在脚本中，无需配置 Secret，但若网站更新可能需要同步修改。

| 变量 | 当前值 | 说明 |
|------|--------|------|
| `SUPABASE_URL` | `https://aeilbxxjgrnnqmtwnesh.supabase.co` | FreeXCraft 后端数据库地址（Supabase 项目实例） |
| `SUPABASE_ANON_KEY` | `eyJhbGci...` | Supabase 匿名访问密钥，用于登录鉴权请求，属于公开客户端凭证 |
| `SITE_URL` | `https://freexcraft.com` | 网站地址，用于构造续期请求的 `origin` / `referer` 头 |
| `SERVER_ID` | `f59428a5-...` | 需要续期的服务器 UUID，可在控制台 URL 中找到 |
| `SERVER_NAME` | `FreexCraft 🇳🇱` | 服务器展示名称，仅用于 TG 通知，硬编码无需动态获取 |
| `EXPIRE_TIME` | `03:59:59` | 续期后的有效时长，仅用于 TG 通知展示，与实际服务端一致 |

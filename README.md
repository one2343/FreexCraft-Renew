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

> ⚠️ `SUPABASE_ANON_KEY` 虽为公开凭证（前端 JS 中可见），但仍建议不要在公开 Repo 中暴露，可改为 Secret 注入。

### 如何获取 SERVER_ID

登录 freexcraft.com 后进入服务器控制台，浏览器地址栏 URL 格式为：
```
https://freexcraft.com/dashboard/server/f59428a5-ead9-4cd1-b34e-c67fb5a1396c
```

最后一段即为 `SERVER_ID`，复制替换脚本中的对应值即可。

### 如何获取 SUPABASE_URL / SUPABASE_ANON_KEY

这两个值来自 FreeXCraft 前端源码，无需注册 Supabase 账号，获取方式如下：

1. 打开 freexcraft.com，按 `F12` 进入开发者工具
2. 切换到 **Network** 标签，刷新页面
3. 筛选请求，找到任意发往 `supabase.co` 的请求
4. 在请求 **Headers** 中找到 `apikey` 字段，其值即为 `SUPABASE_ANON_KEY`
5. 该请求的域名部分（如 `https://aeilbxxjgrnnqmtwnesh.supabase.co`）即为 `SUPABASE_URL`

> 通常这两个值不会变动，仅在 FreeXCraft 迁移 Supabase 项目时才需要更新。

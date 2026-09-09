# dsxair-renew

NVIDIA DSX Air 仿真自动续期(GitHub Actions)。

每天定时把所有仿真(simulation)的 `expires_at` 往后推 24 小时(单次不超过 now+68h,API 上限为 72h),并通过 Telegram 通知结果。

## 原理
- `GET  https://api.dsx-air.nvidia.com/api/v3/simulations/` 列出所有仿真
- `PATCH /api/v3/simulations/{id}/` 修改 `expires_at`(= 到期自动删除时间)
- `expires_at=null` 的仿真视为永不过期,跳过

## Secrets
| Secret | 必填 | 说明 |
|---|---|---|
| `NGC_API_KEY` | 是 | NGC Personal API Key(生成时勾选 NVIDIA Air 服务),`***` 开头 |
| `TG_BOT_TOKEN` | 推荐 | Telegram Bot token,不配则跳过通知 |
| `TG_CHAT_ID` | 推荐 | 接收通知的 chat ID |

## 手动触发
Actions 页面 -> Run workflow。

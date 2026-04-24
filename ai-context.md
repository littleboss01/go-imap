## 2026-04-24 COMPRESS 升级时序修复

- 已在 `client/client.go` 新增导出方法 `UpgradeWithCommand`：
  - 先执行升级触发命令
  - 再 `WaitReady` 同步读协程
  - 最后包装并替换连接
- 已将 `client/cmd_noauth.go` 的 `StartTLS` 切换为调用 `UpgradeWithCommand`。
- 目标是给 `go-imap-compress` 提供和 `StartTLS` 同等安全的升级时序，避免 `COMPRESS DEFLATE` 切换竞态。

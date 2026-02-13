🔄 rclone-sync


使用 GitHub Actions + rclone 自动同步两个云存储（如 OneDrive、Google Drive、WebDAV 等）之间的文件。  

✨ 特性


🔒 敏感信息加密存储（rclone 配置通过 GitHub Secrets 注入）
🧪 支持 Dry Run 模式（手动触发时可预览操作，避免误删）
🛠️ 灵活配置源/目标路径（通过仓库 Variables 动态修改）
📊 详细日志输出（便于排查同步失败原因）

⚙️ 使用方法

准备 rclone 配置

在本地运行 rclone config，创建两个远程存储（例如 onedrive 和 googledrive），然后复制完整配置内容

设置 GitHub Secrets
进入你的仓库 → Settings → Secrets and variables → Actions

添加 Secret：
  RCLONE_CONF：粘贴上面的完整 rclone.conf 内容（不要 Base64 编码）

（可选）添加 Variables（用于自定义路径）：
  SOURCE_REMOTE：例如 onedrive:Photos
  DEST_REMOTE：例如 googledrive:Backup/Photos


若不设置 Variables，默认同步 onedrive: → googledrive:（根目录）。

启用工作流：


首次使用请手动触发一次 Dry Run 测试：
  进入 Actions → Rclone Sync → Run workflow
  勾选 “启用 Dry Run 模式”
  查看日志确认无误

📂 目录结构

.rclone-sync/

├── .github/

│   └── workflows/

│       └── rclone-sync.yml          # 核心自动化脚本

└── README.md                 # 本说明文件

⚠️ 注意事项

GitHub Actions 免费账户每月有 2000 分钟 运行时长，请合理安排同步频率。


首次同步建议开启 Dry Run，防止因路径错误导致数据覆盖或删除。


rclone 默认 单向同步（源 → 目标），目标端多余文件会被删除。如需保留，请改用 copy 命令。


确保 RCLONE_CONF 中的 token 有效（尤其是 OneDrive / Google Drive 的 refresh token）。

🤝 贡献与反馈

欢迎提交 Issue 或 PR！如果你觉得这个项目对你有帮助，不妨点个 ⭐ 支持一下 😊


⚠️ 免责声明


本项目（rclone-sync）按“原样”提供，作者不对其正确性、可靠性、安全性或适用性作任何明示或暗示的保证。


使用本项目前，请务必备份重要数据。


由于 rclone 默认采用单向同步（sync 模式），目标路径中不存在于源路径的文件将被永久删除，操作不可逆。


因配置错误、Token 失效、网络中断、云存储 API 变更或 GitHub Actions 运行异常等导致的数据丢失、同步失败或其他损失，作者概不负责。


请确保你已充分理解 rclone 官方文档 的行为逻辑，并在测试环境中验证后再用于生产场景。


使用即表示你已知悉风险，并自愿承担所有后果。

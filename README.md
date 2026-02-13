🔧 配置建议
✅ Secrets
RCLONE_CONF：你的完整 rclone.conf 内容
示例：
[onedrive]
type = onedrive
client_id = xxx
client_secret = yyy
token = {"access_token":"...","expiry":"..."}
[googledrive]
type = drive
client_id = aaa
client_secret = bbb
token = {"access_token":"..."}

✅ Variables（可选，用于灵活切换路径）
进入 Settings → Secrets and variables → Actions → Variables，添加：
SOURCE_REMOTE：例如 onedrive:Photos
DEST_REMOTE：例如 googledrive:Backup/Photos


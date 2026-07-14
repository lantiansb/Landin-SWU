# Landin-SWU

Landin 工具的公开静态更新床。客户端只通过匿名 HTTPS 读取版本清单和安装包；本仓库不保存访问令牌、API 密钥或其他运行时凭据。

## 目录契约

~~~text
db-tools/
└─ CVTPDAnalyser/
   ├─ VersionHistory.ini
   ├─ icon.ico
   └─ <version>/
      └─ cvtpd-analyser-<version>-setup.exe
~~~

正式更新根地址：

~~~text
https://raw.githubusercontent.com/lantiansb/Landin-SWU/main/db-tools
~~~

## 发布约束

1. `VersionHistory.ini` 的 `LatestVersion` 指向已存在的版本目录。
2. 安装包必须是普通 Git blob，严格小于 100 MiB；不使用 Git LFS 或 GitHub Release 跳转地址。
3. 清单中的 `ToolFile`、`Size` 和 `SHA256` 必须与安装包完全一致，不能保留 `@AUTO@`。
4. GitHub 提交应同时包含版本目录和清单，使 `main` 的切换保持原子性。若目标镜像无法原子更新，先发布安装包，最后更新清单。
5. 发布内容由 CVTPD Analyser 源仓库的 `build-docs-release.ps1` 生成；不要手工改写已生成的大小或哈希。

SHA-256 用于校验下载内容一致性，不替代发布者数字签名。

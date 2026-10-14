# Gajim 定制版 · GitHub Actions 云构建

本仓库只放两样东西，不放 Gajim 源码：

- `gajim-dynamic-server.patch`：动态服务器发现补丁
  （启动拉 txt 取域名、端口丢弃；程序内 63114；用户名模式；隐藏服务器设置）
- `.github/workflows/build-windows.yml`：云构建工作流

用法：

1. 在本仓库页面点 **Actions** → **Build Gajim Windows portable** → **Run workflow**。
2. 等构建完成（约 20–40 分钟），在同一页面底部下载 `gajim-portable`
   （内含 `Gajim-Portable.zip`，约 160–200MB）。
3. 解压后直接运行 `Gajim\bin\Gajim.exe` 即可，不安装、不写注册表、
   配置存在程序目录里（便携模式），整个文件夹拷到哪都能用。
4. 构建用 `windows-latest` + MSYS2，全程无人值守；构建脚本是 Gajim
   官方的 `win/build.sh`，未做任何修改（仅在 runner 里跳过安装包打包步骤）。
5. 保险：如果构建中途失败，工作流会把已生成的文件也上传为
   `gajim-built-files-rescue`（ZIP 或程序目录原样），不会让一小时构建白跑。

说明：

- 源码每次从上游 `gajim/gajim` 的固定提交 `b3a40f2` 拉取，补丁基于该提交制作，
  保证可复现；上游更新不影响本次构建。
- 仓库建议设为 Public（构建分钟数免费无限；Private 仓库 Windows 构建按 2 倍计费）。
- 补丁内容见 `gajim-dynamic-server.patch`，无任何密钥与私密信息。

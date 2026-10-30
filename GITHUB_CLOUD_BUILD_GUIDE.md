# GitHub 云端编译说明（手机操作版）

本项目已包含 GitHub Actions 工作流：上传源码到 GitHub 的 `main` 或 `master` 分支后会自动编译；也可以在 Actions 页面手动运行。编译产物是 **debug 签名 APK**，适合本机安装测试，不是正式发布签名包。

## 第一次设置

1. 登录 https://github.com/ ，创建一个新仓库。建议选择 **Private（私有）**，仓库名可填 `VideoSpeed-Douyin-40.4`。
2. 不要勾选自动添加 README、License 或 `.gitignore`，创建空仓库。
3. 在仓库首页选择 **Add file → Upload files**，把本 ZIP 解压后 `io.github.MarsGao.speed-master` 文件夹里面的全部文件和文件夹上传到仓库根目录。必须能直接看到 `app`、`gradle`、`gradlew`、`settings.gradle` 和 `.github`，不要把外层文件夹再套一层。
4. 在页面底部选择提交到 `main` 分支（Commit changes）。
5. 打开仓库的 **Actions** 页面，进入 **Build VideoSpeed APK**，等待运行完成。
6. 运行成功后，在该次运行页面底部的 **Artifacts** 区域下载 `VideoSpeed-1.2.13-Douyin-40.4-debug`，解压后得到 APK。

## 以后重新编译

修改源码并提交到 `main` 后会自动编译。也可以进入 **Actions → Build VideoSpeed APK → Run workflow** 手动编译。

## 重要说明

- 该工作流只负责云端编译，不会自动把 APK 安装到手机。
- 生成的是 debug APK。安装前如果手机已有同包名但使用不同签名的 VideoSpeed，Android 可能提示签名冲突；需要先卸载旧版模块，再安装新 APK。
- APK 能成功编译不代表抖音 40.4.0 的 Hook 已经实机验证。安装后仍需在 LSPosed 中启用模块、勾选抖音并重启抖音测试。
- 不要把签名密钥、密码、账号令牌或其他密钥文件上传到仓库。

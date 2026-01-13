# 下一步操作指南

## ✅ 已完成的修改

1. **创建了 `/lib` 目录结构**
   - 添加了 README.md 说明文档
   - 添加了 .gitkeep 文件以确保目录被 git 跟踪

2. **修改了 GitHub Actions 工作流** (`.github/workflows/ipa.yml`)
   - 支持选择 Swiftgram、Turrit、Telegram 三个变体
   - 从 `/lib` 目录注入自定义 dylib 文件
   - 支持自动获取或手动提供 IPA URL
   - 可选注入 SideloadFix.dylib 和 NSEFix.dylib
   - Swiftgram 变体支持注入 SwiftgramPro.dylib

3. **更新了 `.gitignore`**
   - 跟踪 `/lib` 目录中的 dylib 文件
   - 忽略构建产物

4. **更新了 `README.md`**
   - 添加了详细的使用说明
   - 支持的变体表格
   - 文件结构说明

## 📋 你需要做的事情

### 1. 添加 TGExtra (必需)

你已经添加了 `TGExtra-1.7.1.deb` ✅ - 工作流会自动从中提取 `.dylib` 文件！

```bash
# 验证文件已添加
ls -lh lib/TGExtra*.deb

# 或者如果你有 .dylib 文件，也可以直接添加
# cp /path/to/TGExtra.dylib lib/
```

### 2. 添加 SwiftgramPro (可选，用于 Swiftgram 变体)

你已经添加了 `SwiftgramPro-1.1-7.deb` ✅ - 工作流会自动从中提取 `.dylib` 文件！

```bash
# 验证文件已添加
ls -lh lib/SwiftgramPro*.deb

# 或者如果你有 .dylib 文件，也可以直接添加
# cp /path/to/SwiftgramPro.dylib lib/
```

### 3. (可选) 添加其他 dylib 文件

```bash
# 如果你想本地提供 SideloadFix 和 NSEFix (否则会自动下载)
cp /path/to/SideloadFix.dylib lib/
cp /path/to/NSEFix.dylib lib/
```

> **注意**: 工作流支持 `.dylib` 文件和 `.deb` 包。如果提供 `.deb` 文件，工作流会自动提取其中的 `.dylib` 文件。

### 3. 提交并推送更改

```bash
# 查看当前状态
git status

# 添加所有更改
git add .

# 提交更改
git commit -m "修改工作流以支持多变体 IPA 构建和自定义 dylib 注入"

# 推送到 GitHub
git push origin main
```

### 4. 运行 GitHub Actions 工作流

1. 访问你的 GitHub 仓库
2. 点击 **Actions** 标签
3. 选择 **"Build and Release IPA"** 工作流
4. 点击 **"Run workflow"** 按钮
5. 填写选项:
   - **telegram_variant**: 选择 `swiftgram`、`turrit` 或 `telegram`
   - **decrypted_ipa_url**: (可选) 提供解密 IPA 的直接 URL,或留空自动获取
   - **inject_sideload_fix**: 勾选以注入 SideloadFix.dylib
   - **inject_nse_fix**: 勾选以注入 NSEFix.dylib
6. 点击 **"Run workflow"** 开始构建

### 5. 下载构建的 IPA

1. 等待工作流完成 (通常 5-10 分钟)
2. 转到 **Releases** 页面
3. 下载文件:
   - `*.ipa` - 用于侧载 (AltStore, Sideloadly 等)
   - `*.tipa` - 用于 TrollStore 安装

## 📝 重要说明

### 关于 IPA 来源

工作流会尝试从以下 GitHub 仓库自动获取 IPA:
- **Swiftgram**: `Swiftgram/Swiftgram`
- **Turrit**: `Turrit-Telegram/Turrit`
- **Telegram**: `TelegramMessenger/Telegram-iOS`

**注意**: 这些官方仓库可能不包含解密的 IPA 文件。如果自动获取失败,你需要:
1. 从可信来源获取解密的 IPA
2. 在运行工作流时提供直接下载 URL

### 关于 dylib 文件

| 文件 | 是否必需 | 用途 | 来源 | 支持格式 |
|------|---------|------|------|---------|
| TGExtra | ✅ 必需 | 主要 tweak 功能 | 你需要提供 | .dylib 或 .deb |
| SwiftgramPro | ❌ 可选 | Swiftgram Pro 功能解锁 | 你需要提供 (仅 Swiftgram) | .dylib 或 .deb |
| SideloadFix.dylib | ❌ 可选 | 侧载修复 | 自动下载或本地提供 | .dylib |
| NSEFix.dylib | ❌ 可选 | 通知扩展修复 | 自动下载或本地提供 | .dylib |

> **注意**: 工作流会自动从 `.deb` 包中提取 `.dylib` 文件。

### 支持的变体

| 变体 | Bundle ID | SwiftgramPro 支持 |
|------|-----------|------------------|
| Swiftgram | `app.swiftgram.ios` | ✅ 是 |
| Turrit | `com.seastar.turrit` | ❌ 否 |
| Telegram | `ph.telegra.Telegraph` | ❌ 否 |

## 🔧 故障排除

### 问题: "TGExtra.dylib not found in lib directory"

**解决方案**: 你必须先添加 `TGExtra.dylib` 到 `/lib` 目录。

### 问题: 自动获取 IPA 失败

**解决方案**: 手动提供解密 IPA 的 URL:
1. 从可信来源获取解密的 IPA
2. 上传到文件托管服务或使用直接下载链接
3. 在运行工作流时粘贴 URL

### 问题: 构建的 IPA 无法安装

**可能原因**:
1. IPA 版本不兼容
2. 需要重新签名
3. dylib 架构不匹配

**解决方案**: 使用 AltStore 或 Sideloadly 重新签名 IPA。

## 📚 更多信息

查看以下文档了解更多详情:
- [README.md](file:///Users/jiaweiding/Documents/TGExtra/README.md) - 项目概述和使用说明
- [lib/README.md](file:///Users/jiaweiding/Documents/TGExtra/lib/README.md) - dylib 目录说明
- [walkthrough.md](file:///Users/jiaweiding/.gemini/antigravity/brain/d75c5174-6cfb-4068-a568-025faffc14a0/walkthrough.md) - 完整的修改演练

## ✨ 快速开始

你已经完成了第一步！现在只需要提交和推送：

```bash
# 1. 查看当前状态 (你已经添加了 .deb 文件)
git status

# 2. 提交更改
git add .
git commit -m "Add TGExtra and SwiftgramPro deb files, update workflow"
git push

# 3. 在 GitHub Actions 中运行 "Build and Release IPA" 工作流

# 4. 从 Releases 下载构建的 IPA
```

祝你使用愉快! 🎉

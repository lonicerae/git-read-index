[English](README.md)

# Git Index Reader - git-read-index

## 概述 (Overview)
`git-read-index` 是一个基于 Python 开发的实用工具，用于读取并解析 Git 索引文件（`.git/index`）。它可以详细展示 Git 仓库中暂存区（Staging Area）文件的具体信息，帮助开发者深入了解暂存内容，包括文件元数据、权限、SHA-1 校验和等。

## 特性 (Features)
* **原生解析**：直接解析 Git 索引文件，无需依赖外部 Git 命令行工具。
* **详尽信息**：展示暂存文件的详细属性，包括文件权限（mode）、大小及修改时间（mtime）。
* **完整性校验**：自动验证 SHA-1 校验和，确保索引文件的完整性。
* **扩展支持**：具备解析各种 Git 索引扩展字段（Extensions）的能力。
* **用户友好**：控制台输出经过色彩编码处理，易于阅读；具备 Git 仓库位置自动检测功能。

## 前置条件 (Prerequisites)
* Python 3.x
* 系统已安装并配置好 Git 环境
* 一个现有的 Git 仓库（该工具可以在任何有效的 Git 目录下运行）

## 安装 (Installation)

### 直接下载
从本项目仓库下载 `git-read-index` 脚本，并赋予执行权限：
```bash
chmod +x git-read-index
cp git-read-index /path/to/your/executables/
```

## 使用说明 (Usage)

### 基本用法
在任何 Git 仓库目录下运行以下命令即可：
```bash
./git-read-index
# 或者
python3 git-read-index
```

### 命令行选项
脚本会自动检测当前目录或其父目录中的 Git 仓库。对于标准操作，无需传递额外参数。

### 输出格式示例 (Output Format Example)
工具会以结构化且易于阅读的格式展示信息：

```text
============================================================
[ Git Index Header ]
  Magic Number  : 4D5F5347
  Version       : 2
  Entries Count : 15
============================================================
[ Staging Entries ]
------------------------------------------------------------
 [1] src/main.py
     └─ Mode (Permissions) : 100644
     └─ File Size          : 1024 bytes
     └─ Blob SHA-1         : a1b2c3d4e5f67890123456789012345678901234
     └─ Modified (mtime)   : 1634567890
------------------------------------------------------------
[ Extensions ]
  Found Extension: TREE (Size: 20 bytes)
  Found Extension: REUC (Size: 12 bytes)
============================================================
```

## 使用示例 (Examples)

**查看当前仓库索引：**
```bash
cd /path/to/your/git/repo
./git-read-index
```

**检查索引完整性：**
工具会自动验证 SHA-1 校验和，如果检测到文件损坏，将会发出警告：
```text
⚠️ WARNING: Index file SHA-1 checksum failed, file may be corrupted!
```

## 故障排除 (Troubleshooting)

| 问题 | 原因 | 解决方案 |
| :--- | :--- | :--- |
| `FATAL ERROR: Not in Git Repository` | 当前目录或父目录不是 Git 仓库。 | 请在有效的 Git 项目目录中运行脚本。 |
| `Permission denied` | 脚本缺少执行权限。 | 执行 `chmod +x git-read-index`。 |
| `SHA-1 checksum failed` | 索引文件可能已损坏或被篡改。 | 运行 `git status` 检查仓库完整性；必要时使用 `git reset`。 |

## 调试建议 (Debugging Tips)
* **验证 Git 安装情况**：
  ```bash
  git --version
  ```
* **检查 Git 仓库结构**：
  ```bash
  ls -la .git/
  ```
* **验证索引文件位置**：
  ```bash
  git rev-parse --git-dir
  ```

## 贡献 (Contributing)
欢迎提交 Pull Request！

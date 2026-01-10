# Python 编程新手指南 (macOS 版)

欢迎开启 Python 编程之旅！本指南专为 macOS 入门用户设计，旨在帮助你快速上手并建立正确的开发认知。

---

## 0. 核心概念速查 (Terminology)

在开始之前，我们需要理清几个核心术语：

| 概念 | 身份 | 作用 |
| :--- | :--- | :--- |
| **Python** | 编程语言 | 你编写的代码逻辑。目前通用版本为 Python 3。 |
| **Python3** | 解释器 | 在 Mac 上负责读取并执行 Python 代码的程序。 |
| **pip3** | 包管理器 | Python 的“应用商店”，用于下载和安装第三方的功能库。 |

---

## 1. 使用 Homebrew 安装

在 macOS 上，我们统一使用 **Homebrew** 安装 Python。这会为你安装一个**全局可用**的 Python 3 运行环境。

如果你尚未安装 Homebrew，请先阅读 [macOS 编程环境入门](./00_macOS_Programming_Base_Setup.md)。

**安装命令：**
```bash
brew install python
```
> **注意：** 该命令安装的是目前最新的 Python 3。安装后，系统会自动带上 `pip3`（包管理器）。

---

## 2. 验证、版本查看与升级

安装完成后，你需要确认它们是否已正确进入你的系统。

### 验证安装与版本查看
在终端输入以下命令：
```bash
python3 --version
pip3 --version
```

### 寻找安装位置
如果你想知道 Python 到底安装在磁盘的哪个角落，可以使用 `which` 指令：
```bash
which python3
which pip3
```
> **提示：** 对于 Homebrew 安装的工具，路径通常位于 `/opt/homebrew/bin/`。
> **提示：** 在 macOS 上，为了避免与系统自带的旧版工具冲突，请始终使用 `python3` 和 `pip3` 命令。

### 升级 Python
Homebrew 让升级变得非常简单。当你想要使用更新的版本时，只需执行：
```bash
brew update            # 更新 Homebrew 自身的清单
brew upgrade python    # 升级 Python 到最新版本
```

---

## 3. 运行简单的临时性脚本

如果你只是想测试一段代码逻辑，或者运行一个简单的自动化脚本（**不涉及任何第三方库**），可以直接使用全局 Python。

1. **创建一个文件**：例如 `hello.py`。
2. **编写代码**：
   ```python
   print("Hello, macOS Python!")
   ```
3. **在终端运行**：
   ```bash
   python3 hello.py
   ```

---

## 4. 项目级别参考进阶版指南

当你准备开始开发一个真正的应用，或者需要用到 `requests`、`pandas` 等第三方库时，直接在全局环境下操作会导致系统环境混乱。此时你需要进入**现代化项目管理模式**。

**进阶学习路线：**
- **如何管理多版本**（为什么 Homebrew 的 Python 不够用）
- **如何隔离不同的项目环境**（虚拟环境的底层原理）
- **如何高效管理项目依赖**（使用 `uv`）

请直接参考：[Python 现代化项目管理指南 (uv)](./Python_Modern_Project_Guide_uv.md)

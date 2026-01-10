# JavaScript 编程新手指南 (macOS 版)

欢迎开启 JavaScript 编程之旅！本指南专为 macOS 入门用户设计，旨在帮助你快速上手并建立正确的开发认知。

---

## 0. 核心概念速查 (Terminology)

在开始之前，我们需要理清几个核心术语：

| 概念 | 身份 | 作用 |
| :--- | :--- | :--- |
| **JavaScript** | 编程语言 | 你编写的代码逻辑。 |
| **Node.js** | 运行时/解释器 | 让 JavaScript 脱离浏览器，直接在你的 Mac 上运行的“引擎”。 |
| **npm** | 包管理器 | 类似于“应用商店”，用于下载和管理第三方的功能库。 |

---

## 1. 使用 Homebrew 安装

在 macOS 上，我们统一使用 **Homebrew** 安装 Node.js。这会为你安装一个**全局可用**的运行环境。

如果你尚未安装 Homebrew，请先阅读 [macOS 编程环境入门](./00_macOS_Programming_Base_Setup.md)。

**安装命令：**
```bash
brew install node
```
> **注意：** 该命令会同时安装 `node`（解释器）和 `npm`（包管理器）。

---

## 2. 验证、版本查看与升级

安装完成后，你需要确认它们是否已正确进入你的系统。

### 验证安装与版本查看
在终端输入以下命令，如果能看到版本号（如 `v20.x.x`），说明安装成功：
```bash
node -v
npm -v
```

### 寻找安装位置
如果你想知道 Node.js 到底安装在磁盘的哪个角落，可以使用 `which` 指令：
```bash
which node
which npm
```
> **提示：** 对于 Homebrew 安装的工具，路径通常位于 `/opt/homebrew/bin/`。

### 升级 Node.js
Homebrew 让升级变得非常简单。当你想要使用更新的版本时，只需执行：
```bash
brew update          # 更新 Homebrew 自身的清单
brew upgrade node    # 升级 Node.js 到最新版本
```

---

## 3. 运行简单的临时性脚本

如果你只是想测试一段代码逻辑，或者运行一个简单的自动化脚本（**不涉及任何第三方库**），可以直接使用全局 Node.js。

1. **创建一个文件**：例如 `hello.js`。
2. **编写代码**：
   ```javascript
   console.log("Hello, macOS JavaScript!");
   ```
3. **在终端运行**：
   ```bash
   node hello.js
   ```

---

## 4. 项目级别参考进阶版指南

当你准备开始编写一个真正的项目（例如需要用到 `axios` 或 `dayjs` 等第三方库）时，全局安装就力不从心了。此时你需要进入**现代化项目管理模式**。

**进阶学习路线：**
- **如何管理多版本**（使用 `fnm`）
- **如何隔离不同的项目环境**（Node.js 的项目级隔离机制）
- **如何高效管理项目依赖**（使用 `pnpm`）

请直接参考：[JavaScript 现代化项目管理指南 (pnpm & fnm)](./JS_Modern_Project_Guide_pnpm.md)

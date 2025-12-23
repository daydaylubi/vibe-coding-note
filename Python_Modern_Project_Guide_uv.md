# Python 现代化项目管理指南：全面拥抱 uv

在上一篇指南中，我们学习了通过 Homebrew 安装 Python 以及手动管理虚拟环境的基础知识。但在真实的开发世界中，随着项目增多，你会遇到更加棘手的问题。

本指南将带你进入 Python 业界目前最推崇的现代化管理方式 —— **使用 uv**。

---

## 1. 为什么 Homebrew 以后还不够？

Homebrew 安装的是“系统级”的 Python，它的版本是固定的（通常是最新稳定版）。

### 痛点：多版本并存
在实际开发中，你可能会遇到以下情况：
- **项目 A**：使用了较旧的深度学习库，必须运行在 **Python 3.10**。
- **项目 B**：想尝试最新的语法特性，需要 **Python 3.13**。
- **项目 C**：生产环境服务器固定在 **Python 3.11**，你必须在本地环境与其对齐。

如果只靠 Homebrew，你很难在这些版本间无缝切换，且容易把系统环境搞乱。

### 过去与现在
- **过去**：开发者通常使用 `pyenv` 管理 Python 版本，配合 `pipreqs` 或手动维护 `requirements.txt`。配置繁琐，速度较慢。
- **现在**：**uv** 出现后，它以极速（Rust 编写）统一了 Python 版本管理、包安装、虚拟环境创建和项目初始化。**它是目前 Python 开发者的首选“全能工具”。**

---

## 2. 安装 uv

在 macOS 上，我们依然利用 Homebrew 来安装 uv 这个工具本身：

```bash
brew install uv
```

---

## 3. 多版本 Python 管理

有了 uv，你不再需要去 Python 官网下载安装包，也不再需要手动管理路径。

### 安装特定版本
你可以直接让 uv 为你下载并管理多个 Python 版本：
```bash
uv python install 3.10 3.11 3.12
```

### 查看安装路径
uv 会将这些 Python 安装在它的私有目录下，不会污染你的系统路径。你可以通过以下命令查看：
```bash
uv python dir
```
> **提示**：你会发现它们通常被存放在 `~/.local/share/uv/python` 目录下。

### 锁定项目版本 (Pinning)
如果你希望某个项目始终使用特定版本（例如 3.11），在项目目录下运行：
```bash
uv python pin 3.11
```
这会创建一个 `.python-version` 文件，uv 及其它工具会自动识别并使用该版本。

---

## 4. 项目初始化：uv init

当你开始一个新项目时，告别手动创建文件夹。

```bash
uv init my-project
cd my-project
```

### 产生的核心文件
- **`pyproject.toml`**：项目的“灵魂”。它记录了项目的元数据（名称、版本、作者）以及项目所依赖的库。
- **`.python-version`**：记录了该项目锁定的 Python 版本。
- **`main.py`**：一个默认生成的示例文件。
- **`README.md`**：项目说明文档。

---

## 5. 虚拟环境：uv venv

虽然 uv 可以直接运行代码，但在项目内部创建虚拟环境依然是最佳实践。

```bash
uv venv
```
- **默认行为**：会在当前目录下生成 `.venv` 文件夹。
- **环境继承**：这个虚拟环境会自动使用你刚才“pin”住的那个 Python 版本。
- **本质**：它与 `python -m venv` 创建的环境在结构上是一样的。这意味着你可以继续使用传统的激活方式：
  ```bash
  source .venv/bin/activate
  ```
> **注意**：激活后，输入 `python` 或 `pip` 都会指向这个极速构建的虚拟环境。

---

## 6. 依赖管理：uv add vs pip install

这是 uv 最强大、最能体现“工业化规范”的地方。

### 规范的操作
使用 `uv add` 而不是 `pip install`：
```bash
uv add requests
```

### 核心区别
1.  **自动记录**：`uv add` 会自动将 `requests` 写入 `pyproject.toml` 的依赖列表中。
2.  **版本锁定 (Lockfile)**：uv 会生成或更新一个 `uv.lock` 文件。这个文件会精确记录你安装的每一个库及其依赖的具体版本号。
    - **为什么要 Lock？** 确保你的同事克隆代码后，安装的版本和你一模一样，杜绝“我电脑上明明能跑”的玄学问题。
3.  **极速**：你会发现安装过程几乎是瞬间完成的，因为它有极其高效的缓存机制。

---

## 7. 运行你的代码

现在你有两种方式运行代码：

### 方式 A：传统方式（需激活）
```bash
source .venv/bin/activate
python hello.py
```

### 方式 B：现代化方式（推荐）
```bash
uv run hello.py
```
**为什么推荐 `uv run`？**
- 它会自动检查你的虚拟环境是否是最新的。
- 如果你添加了新依赖但还没安装，`uv run` 会在运行前自动帮你同步（Sync）好。
- 它甚至可以免激活运行。

---

## 总结：uv 现代化开发流

1.  **安装 uv**：`brew install uv`。
2.  **创建项目**：`uv init my_project`。
3.  **锁定版本**：`uv python pin 3.12`。
4.  **添加依赖**：`uv add pandas`（自动更新 `pyproject.toml` 和 `uv.lock`）。
5.  **一键运行**：`uv run main.py`。

通过 uv，你不仅获得了极致的速度，更重要的是，你正站在 Python 工程化的最前沿。

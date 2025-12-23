# Python 编程新手指南 (macOS 版)

欢迎开启 Python 编程之旅！本指南专为 macOS 用户设计，旨在帮助你建立一个规范、高效且整洁的 Python 开发环境。

---

## 1. 环境搭建：使用 Homebrew 安装 Python 3

在 macOS 上，推荐使用 **Homebrew**（包管理器）来管理 Python。

### 核心机制：环境配置与路径

*   **Q: 安装 Homebrew 后，那个 `eval ...` 是什么意思？**
    *   **A:** 在安装 Homebrew 时，终端会提示你将 `eval "$(/opt/homebrew/bin/brew shellenv)"` 写入 `~/.zprofile`。
    *   **含义：** 这行代码的作用是在你每次打开终端时，“初始化” Homebrew 环境。它会自动设置环境变量，确保终端知道去哪里找 Homebrew 下载的软件。
*   **Q: Homebrew 把软件装在哪了？**
    *   **A:** 对于 Apple Silicon (M1/M2/M3) 的 Mac，Homebrew 的默认安装路径是：
        `/opt/homebrew/bin` 和 `/opt/homebrew/sbin`。
*   **Q: 会和系统自带的 Python3 冲突吗？**
    *   **A:** macOS（/usr/bin 下）虽然可能带有 Python3，但 **Homebrew 的路径在 `PATH` 变量中位次更靠前**。这意味着当你输入 `python3` 时，系统会优先匹配并运行 Homebrew 安装的版本，从而实现“无损覆盖”。

### 常见疑问

*   **Q: `python3` 和 `python` 有什么区别？**
    *   **A:** `python` 通常指已淘汰的 Python 2。**目前的工业规范是：始终使用 `python3`。**
*   **Q: `python3` 和 `pip3` 是什么关系？**
    *   **A:** `python3` 是解释器（运行代码），`pip3` 是包管理器（下载工具）。安装 `python3` 会自动带上 `pip3`。

### 安装习惯

**划重点：** 虽然 `brew install python` 也会安装 Python 3，但为了表达清晰并符合未来规范，**建议统一使用：**
```bash
brew install python3
```

---

## 2. 验证、版本查看与升级

### 验证安装
在终端输入：
```bash
python3 --version
```
确保输出的版本来自 Homebrew（通常版本号更新）。

### 升级 Python
与其混用，不如养成习惯：
```bash
brew update
brew upgrade python3
```

---

## 3. Python 虚拟环境 (Virtual Environment)

虚拟环境是 Python 开发的“洁癖准则”。

### 规范：我需要创建虚拟环境吗？
**是的。** 即便只是写一个“Hello World”以外的简单脚本，也请通过虚拟环境保持环境整洁。

### 核心原理

*   **Q: 激活环境（Source activate）到底在做什么？**
    *   **A: 激活的本质是修改 PATH。** 当你运行 `source venv/bin/activate` 时，它会临时把该项目下的 `venv/bin` 文件夹塞到系统搜索路径的最前面。
*   **Q: 激活后为什么直接用 `python` 就行了？**
    *   **A:** 正因为 `venv/bin` 优先级最高，里面已经存在一个名为 `python` 的软链接指向 Python3。所以激活后，你**不再需要**输入 `python3` 或 `pip3`，直接用 `python` 和 `pip` 即可。
*   **Q: 激活是永久的吗？**
    *   **A: 不是。** 激活操作**只对当前这一个终端窗口有效**。如果你多开了几个窗口，或者关闭后重新打开，都需要在对应的项目目录下重新执行 `source` 命令。

### 实战操作

1.  **进入项目并创建环境：**
    ```bash
    python3 -m venv venv(这个名字可以随便取，但是通常都是 venv)
    ```

2.  **激活环境：**
    ```bash
    source venv/bin/activate
    ```
    *看到 `(venv)` 标志了吗？这意味着现在 `python` 命令指向的就是这里。*

3.  **使用 `pip` 与 `requirements.txt`：**
    *   安装库：`pip install requests`
    *   **什么时候用 requirements？** 当你需要把代码交给别人，或在不同机器运行。
    *   生成清单：`pip freeze > requirements.txt`
    *   一键恢复：`pip install -r requirements.txt`

4.  **退出环境：**
    ```bash
    deactivate
    ```

---

## 总结你的新手开发流

1.  **打开终端，进入项目文件夹**。
2.  **创建并激活虚拟环境**（第一次：`python3 -m venv venv` ➜ 每次：`source venv/bin/activate`）。
3.  **在该环境下开发**（直接使用 `python` 和 `pip`）。
4.  **如需共享，记得生成 `requirements.txt`**。
5.  **关闭窗口即自动失效，再次开发需重新激活**。

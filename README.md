# 一个Python项目的模板

## 目录结构（示例）

```.
├── src                        # 代码文件夹
│   ├── ...
│   └── ...
│
├── docs                       # 文档文件夹
│   └── ...
│
├── .gitignore                 # Git忽略文件
├── .pre-commit-config.yaml    # pre-commit配置文件
├── .python-version            # Python版本文件
├── dev.py                     # 开发脚本，集成常用指令
├── pyproject.toml             # Python项目配置文件
├── README.md                  # 项目说明文件
└── uv.lock                    # Python依赖锁文件
```

## 获取项目

```bash
git clone https://github.com/your-username/your-project.git
```

## 环境配置

本项目使用 `uv` 管理，为确保项目的可复现性，请按照以下步骤配置环境：

### 1. 安装 `uv`

`Windows`

> 建议获取管理员权限后运行

```bash
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

`MacOS / Linux`

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

如果系统没有 curl，可以使用 wget：

```bash
wget -qO- https://astral.sh/uv/install.sh | sh
```

> 更多安装方式可以参考
> [uv 官方文档](https://docs.astral.sh/uv/getting-started/installation/) /
> [中文翻译版本](https://docs.astral.org.cn/uv/getting-started/installation/)。

### 2. 验证安装

完成上一步后，可能需要重启终端以使用新的环境变量配置。

无论使用何种方式安装，都需要确保可以直接使用 `uv` 命令。

```bash
uv --version
```

### 3. 安装python

> 下载 Python 可能较慢，`uv` 支持换源，但是国内镜像源暂时没有很好的兼容，
> 这一步可以尝试手动下载对应版本的 Python

```bash
uv python install
```

### 4. 创建虚拟环境

这有助于保持你的设备环境的整洁，并确保项目依赖的隔离。

> 一般来说，uv 会在需要的时候自动创建并使用一个虚拟环境，保险起见，这里显式创建一次。

```bash
uv venv
```

### 5. 安装项目依赖

> 这一步可以跳过，uv 会在运行项目时自动安装依赖，但提前安装可以节省后续的时间。

```bash
uv sync
```

### 6. 初始化项目

使用项目的开发脚本 [`dev.py`](./dev.py) 来执行一些初始化操作（有关
[`dev.py`](./dev.py) 的更多信息，请参见 [快速指令](#快速指令)）：

```bash
uv run dev.py init
```

## 快速指令

[`dev.py`](./dev.py) 是一个开发脚本，集成了开发需要用到的指令。

可以直接使用 `uv` 运行脚本，也可以使用激活了项目虚拟环境的 Python 运行：

```bash
uv run dev.py [OPTIONS] COMMAND [ARGS]...
# python dev.py [OPTIONS] COMMAND [ARGS]...
```

### 获取指令帮助

使用 `--help` 参数可以获取指令的帮助信息：

```bash
uv run dev.py --help
```

或者不带参数也可以显示帮助信息：

```bash
uv run dev.py
```

也可以在子命令后面加上 `--help` 来获取子命令的帮助信息：

```bash
uv run dev.py auto --help
```

### 初始化项目

```bash
uv run dev.py init
```

这会自动创建项目钩子

### 代码审查指令

```bash
uv run dev.py check
```

代码审查包含 3 个部分：

- 格式化代码：使用 `ruff` 的 `format` 命令来格式化代码。
- 分析代码质量：使用 `ruff` 的 `check` 命令来分析代码质量，并尝试修复可修复的问题。
- 静态类型检查：使用 `ty` 的 `check` 命令来进行静态类型检查。

> 注意：这一步如果不通过，会阻止进行 `git commit` 相关操作，请务必确保通过代码审查。

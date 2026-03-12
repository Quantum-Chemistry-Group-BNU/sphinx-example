# Sphinx + MyST 最小示例

## 1. Sphinx 的基本使用可以怎么讲

### 第一步：安装

一般先安装 Sphinx、主题和 Markdown 支持，例如：

```bash
pip install sphinx furo myst-parser
```

- `sphinx`：文档工具本体
- `furo`：一个常用主题，其他主题也可以例如 `sphinx-rtd-theme`
- `myst-parser`：让 Sphinx 支持 Markdown

若使用这个示例仓库里的环境，可以先进入：

```bash
conda activate sphinx
pip install sphinx furo myst-parser
```

### 第二步：初始化文档目录

在项目里新建文档：

```bash
sphinx-quickstart docs
```

它会生成一个 `docs/` 目录。常见结构里最重要的文件通常有：

- `conf.py`：配置文件
- `index.rst`：首页
- `_static/`：静态资源
- `_templates/`：模板

这个 example 采用的是 Sphinx 常见的 `source/` 结构，当前目录是：

```text
docs/
├── Makefile
├── build/
└── source/
    ├── conf.py
    ├── index.rst
    ├── markdown-guide.md
    └── rst-guide.rst
```

也就是说，在这个示例里：

- `docs/source/conf.py` 是配置文件
- `docs/source/index.rst` 是首页
- `docs/build/html/` 是生成后的网页目录

### 第三步：写文档内容

比如在这个项目的 `docs/source/index.rst` 里写目录：

```rst
Sphinx + MyST 最小示例
======================

这个示例展示了：

- 首页继续使用 ``reStructuredText``
- 子页面同时包含 ``Markdown`` 和 ``reStructuredText``
- ``myst-parser`` 让 Sphinx 能直接解析 ``.md`` 文件


.. toctree::
   :maxdepth: 2
   :caption: Contents

   markdown-guide
   rst-guide
```

如果更习惯 Markdown，也可以在配置好 `myst-parser` 之后直接写 `.md` 文件。

这个 example 就是混合写法：

- `docs/source/index.rst`：入口页
- `docs/source/markdown-guide.md`：Markdown / MyST 示例
- `docs/source/rst-guide.rst`：rst 示例

当前示例已经包含这些内容：

- rst 和 Markdown 混合放进同一个 `toctree`
- Markdown 页面中的 MyST 指令
- Markdown 和 rst 中的数学公式
- 公式编号与交叉引用
- Markdown 和 rst 之间的跳转

rst 基本语法可以参考：
[rst tutorial](https://rst-tutorial.readthedocs.io/zh/latest/base)

### 第四步：配置 `conf.py`

在这个项目里，配置文件路径是：

```text
docs/source/conf.py
```

当前 example 里实际使用的核心配置如下：

```python
project = "sphinx-example"
author = "zbwu"
extensions = ["myst_parser"]

source_suffix = {
    ".rst": "restructuredtext",
    ".md": "markdown",
}

myst_enable_extensions = [
    "amsmath",
    "colon_fence",
]

html_theme = "alabaster"
```

这里：

- `project` 和 `author`：项目信息
- `extensions = ["myst_parser"]`：让 Sphinx 支持 Markdown
- `source_suffix`：同时识别 `.rst` 和 `.md`
- `myst_enable_extensions`：打开 MyST 的数学和指令能力
- `html_theme`：设置 HTML 主题

这个 example 里还额外配置了 `mathjax3_config`，用于给 HTML 页面里的公式补充 `\braket{}` 宏。

### 第五步：本地生成网页

在这个项目根目录下，可以直接执行：

```bash
cd docs; make html
```

生成好的网页在：

```text
docs/build/html/
```

打开下面这个文件，查看本地效果：

```text
docs/build/html/index.html
```

## readsthedocs 使用

如果希望把文档发布到线上，通常使用[Read the Docs](https://readsthedocs.com/) 

可以分层5步
- GitHub 上放源码和文档源文件
- Read the Docs 自动拉取仓库
- 自动安装依赖
- 自动执行 Sphinx 构建
- 自动生成文档网站


在这个 example 里，需要额外准备两个文件：

- `docs/requirements.txt`
- `.readthedocs.yaml`

其中：

- `docs/requirements.txt`：声明文档构建依赖
- `.readthedocs.yaml`：告诉 Read the Docs 如何构建当前项目

当前项目中，`docs/requirements.txt` 可以写成：

```txt
sphinx
myst-parser
```

当前项目中，`.readthedocs.yaml` 可以写成：

```yaml
version: 2

build:
  os: ubuntu-24.04
  tools:
    python: "3.12"

sphinx:
  configuration: docs/source/conf.py

python:
  install:
    - requirements: docs/requirements.txt
```

这里要注意：

- `configuration: docs/source/conf.py` 必须对应当前仓库的实际目录
- 依赖文件写成 `docs/requirements.txt`，这样 Read the Docs 会自动安装后再构建

配置好之后，Read the Docs 就会自动生成 HTML 文档网站。

> 这个项目使用codex完成
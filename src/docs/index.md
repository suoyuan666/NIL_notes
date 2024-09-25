# 关于本网站

NIL wiki

本站目前仍在完善中

## 如何参与维护工作

仓库地址: https://github.com/suoyuan666/NIL_notes

在 GitHub 上 fork 该仓库，之后将你 fork 后产生的仓库 clone 到本地

我推荐使用虚拟环境，这样安装的库文件不会污染到整个系统中。Python 内置了一个虚拟环境的模块 [venv](https://docs.python.org/zh-cn/3/library/venv.html)，也有第三方的工具实现更彻底的虚拟，我印象中有一个可以允许虚拟环境指定 Python 版本的，但我没用过。

在你 clone 的目录下运行:

```bash
$ python -m venv .
$ source ./bin/activate
```

第二个命令是为了将当前的环境变成你初始化好的虚拟环境，[venv](https://docs.python.org/zh-cn/3/library/venv.html#how-venvs-work) 中列出了不同 shell 需要执行的命令。

该文档使用 [mkdocs](https://github.com/mkdocs/mkdocs) 生成，使用了 [mkdocs-material](https://github.com/squidfunk/mkdocs-material) 主题，所以需要使用 pip 安装相关的库

```bash
$ pip install mkdocs-material mkdocs
```

如果因为网络原因无法正常下载库文件，可以使用国内的 pypi 源，这样就是向国内的服务器访问了，会快很多。

给出以下的镜像源:

- [pypi | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/pypi/)
- [PyPI - USTC Mirror Help](https://mirrors.ustc.edu.cn/help/pypi.html)
- [PyPI — NJU Mirror Help](https://nju-mirror-help.njuer.org/pypi.html)

此外还有上交大，北京外国语等学校都提供了镜像源服务，不过不清楚是否提供了 pip 的镜像源，初次之外，阿里，腾讯等也提供了镜像源服务。

清华和南大的镜像源甚至提供了常见软件和 Linux 发行版，可以直接在镜像站中下载。我并不清楚中科大的镜像站是否也提供了这个服务。

该项目的基本结构:

```txt
.
├── bin
│   ├── activate
│   ├── activate.csh
│   ├── activate.fish
│   ├── Activate.ps1
│   ├── ghp-import
│   ├── markdown_py
│   ├── mkdocs
│   ├── mkdocs-get-deps
│   ├── normalizer
│   ├── pip
│   ├── pip3
│   ├── pip3.12
│   ├── pybabel
│   ├── pygmentize
│   ├── python -> /usr/lib/python-exec/python3.12/python
│   ├── python3 -> python
│   ├── python3.12 -> python
│   └── watchmedo
├── include
│   └── python3.12
├── lib
│   └── python3.12
│       └── site-packages
├── lib64 -> lib
├── pyvenv.cfg
├── README.md
└── src
    ├── docs
    │   ├── index.md
    │   ├── linux/
    │   ├── notes/
    │   ├── programming/
    │   └── tools/
    └── mkdocs.yml
```

_bin_, _lib_, _lib64_ 等就是 python 的 venv 自动生成的，_src_ 是你需要编写的部分

mkdocs 需要一个配置文件，这里的就是 _src/mkdocs.yml_，你可以在 _src_ 目录下执行 `mkdocs serve` 即可在你的浏览器中本地访问。

配置文件这里只说 `nav` 部分，其他的可以参考 [Configuration](https://www.mkdocs.org/user-guide/configuration/)

```yml
nav:
  - 开始:
    - index.md
  - 编程基础:
    - C/C++:
      - programming/lec00/lec00.md
  - Linux 相关:
    - linux/keep.md
  - 工具使用:
    - tools/keep.md
  - 笔记:
    - notes/keep.md
```

这里表示的就是文档的层级关系，你简单看一下网页就能知道这到底是什么写的了。你可以在 _src/docs_ 文件夹中找到对应的文件。

文档使用 Markdown 语言编写，如果不熟悉可参考 [Markdown](./misc/markdown/)
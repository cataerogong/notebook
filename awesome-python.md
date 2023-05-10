# Awesome Python

2023-05-10
----------

* `rich` [https://github.com/Textualize/rich]

  Rich 是一个 Python 库，可以为您在终端中提供富文本和精美格式。

  Rich 的 API 让在终端输出颜色和样式变得很简单。此外，Rich 还可以绘制漂亮的表格、进度条、markdown、语法高亮的源代码以及栈回溯信息（tracebacks）等——开箱即用。

  强大的命令行/终端界面 UI 库。

* `textual` [https://github.com/Textualize/textual]

  Textual is a Rapid Application Development framework for Python. Build sophisticated user interfaces with a simple Python API. Run your apps in the terminal and (coming soon) a web browser!

  基于 `rich` 库的命令行/终端界面应用开发框架。

2020-07-13
__________

* `fire` [https://github.com/google/python-fire]

  Python Fire is a library for automatically generating command line interfaces (CLIs) from absolutely any Python object.

  Google 开发的 Python CLI 库，能够自动为任意程序生成 CLI 界面。

  ``` Python
  import fire

  def hello(name="World"):
    return "Hello %s!" % name

  if __name__ == '__main__':
    fire.Fire(hello)
  ```

2020-07-11
__________

* `Pydantic` [https://github.com/samuelcolvin/pydantic]

  Data validation and settings management using Python type hinting.

  基于 Python 3.6+ 的 type hints.

* `Click` [https://github.com/pallets/click/] [https://click.palletsprojects.com/]

  `Click` is a Python package for creating beautiful command line interfaces in a composable way with as little code as necessary.

  快速方便的 CLI 命令行程序开发库。

* `FastAPI` [https://github.com/tiangolo/fastapi] [https://fastapi.tiangolo.com/]

  `FastAPI` is a modern, fast (high-performance), web framework for building APIs with Python 3.6+ based on standard Python type hints.

  快速方便的 Web API 框架，基于 Python 3.6+ 的 type hints。

* `Typer` [https://github.com/tiangolo/typer] [https://typer.tiangolo.com/]

  `Typer` is a library for building CLI applications that users will love using and developers will love creating. Based on Python 3.6+ type hints.

  快速方便的 CLI 命令行程序开发库，基于 Python 3.6+ 的 type hints。它的底层主要基于 `Click`，但比 `Click` 更方便。

  能根据 Python 代码:
    - 自动解析、验证命令行参数
    - 自动生成 help text
    - 支持多层命令结构 等

2019-09-02
__________

* `PySimpleGUI` [https://github.com/PySimpleGUI/PySimpleGUI]

  极简 GUI 框架，基于 Python 自带的 tkinter 图形界面库。（还有 PySimpleGUIQt, PySimpleGUIwx）

  如果开发简单 GUI 程序的话，很好用。无法或者很难实现一些高级界面效果。

  目前，开发者更新很活跃，可能变动较大。

* `docopt` [https://github.com/docopt/docopt]

  从 *使用说明* 中识别 *命令行参数定义* 并自动解析。

    ```
    """Greeting

    Usage:
    greeting.py (hello|aloha|bye) <name>...
    greeting.py (-h|--help)
    greeting.py --version

    Options:
    -h --help     Show this screen.
    --version     Show version.

    More help informations...
    """
    from docopt import docopt

    if __name__ == '__main__':
        arguments = docopt(__doc__, version='Greeting v1.0')
        if arguments['hello']:
            print('Hello, {}!'.format(' and '.join(arguments['<name>'])))
        elif arguments['aloha']:
            print('Aloha, {}!'.format(' and '.join(arguments['<name>'])))
        elif arguments['bye']:
            print('Bye-bye, {}!'.format(' and '.join(arguments['<name>'])))
    ```

* `dataset` [https://github.com/pudo/dataset]

  简单易用的数据库接口。自动创建表、增加列

    ```
    import dataset

    db = dataset.connect('sqlite:///:memory:')

    table = db['sometable']
    table.insert(dict(name='John Doe', age=37))
    table.insert(dict(name='Jane Doe', age=34, gender='female'))

    john = table.find_one(name='John Doe')
    ```

* `peewee` [https://github.com/coleifer/peewee]

  轻量级的数据库 ORM 模块。

* `SQLAlchemy` [https://github.com/sqlalchemy/sqlalchemy]

  强大的数据库 ORM 模块。

* `sh` [https://github.com/amoffat/sh]

  ( 只支持 linux,osx ) 比 subprocess 更好用的子进程模块。在 Python 里调用外部程序并处理返回结果。

    ```
    import sh
    sh.echo('hello world!')
    ```

* `python-patterns` [https://github.com/faif/python-patterns]

  python 实现各种 *设计模式* 的示例。

2019-08-27
__________

* `pipdeptree` [https://github.com/naiquevin/pipdeptree]

  显示 Python 包依赖树。

  PS: 这个就是对我的 `pkgtree` 项目造成极大打击的那个( T o T )，除了不能输出 `pip uninstall`，其他方面完全碾压。

2019-08-20
__________

* `requests` [https://github.com/psf/requests]

  Python HTTP Requests for Humans™ ✨🍰✨

* `requests-html` [https://github.com/psf/requests-html]

  Pythonic HTML Parsing for Humans™

* `interactive-coding-challenges` [https://github.com/donnemartin/interactive-coding-challenges]

  120+ interactive Python coding interview challenges (algorithms and data structures).
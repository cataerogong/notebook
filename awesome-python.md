# Awesome Python

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
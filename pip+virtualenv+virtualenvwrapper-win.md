# 使用 `pip` + `virtualenv` + `virtualenvwrapper-win` 管理 Python 项目的依赖项

## 安装

  ```
  python -m pip install -upgrade pip
  pip install virtualenv
  pip install virtualenv-win
  ```

## 创建虚拟环境

  * 设置虚拟环境根目录

    所有的虚拟环境都将创建在一个根目录下，设置环境变量 `WORKON_HOME=your\venv\root\folder`。

  * 创建虚拟环境
    ```
    mkvirtualenv <venv-name>
    ```
    会在 `WORKON_HOME` 目录下创建 `<venv-name>` 虚拟环境文件夹。

## 启动虚拟环境

  ```
  workon <venv-name>
  ```
  
  * 命令行提示符最前面会增加 `(<venv-name>)` 标识。
  * 如果关联了项目文件夹，会进入项目文件夹。
  * 不带参数的 `workon` 会列出 `WORKON_HOME` 下的所有虚拟环境。

## 安装 Python 包

  项目需要的 Python 包都安装在虚拟环境中。

  * 启动虚拟环境后，使用 `pip` 安装 Python 包
    ```
    pip install <package>
    ```

  * 手工维护 `depends.txt` 文件

    `depends.txt` 是记录项目的直接依赖信息的文件，没有固定格式，建议参考 `Pipfile`。
    ```
    [requires]
    python_version = "3.6"

    [packages]
    bottle = "*"
    bottle-sqlite = "*"

    [dev-packages]
    PyInstaller = "*"
    ```

  * 更新 requirements.txt 文件
    ```
    pip freeze > requirements.txt
    ```

  * 我写了一个小工具 `pkgtree`，可以展示 Python 包的依赖树状图，并且可以生成 Python 包及其依赖包的 `pip uninstall` 命令。
    ~~~
    > pkgtree
    # 输出
    autopep8 == 1.4.4
      pycodestyle == 2.5.0
    docutils == 0.15.2
    pip == 19.2.2
    pkgtree == 0.5
      setuptools == 40.8.0
    ~~~
    ~~~
    > pkgtree autopep8 -u -p
    # 输出
    pip uninstall --yes autopep8
    pip uninstall --yes pycodestyle
    ~~~

## 在项目中使用

  * 系统 Python 环境

    系统 Python 环境中尽量不要安装 Python 包。

  * 项目虚拟环境

    为每个项目建立对应的虚拟环境，在其中安装项目所需的 Python 包。

  * `depends.txt`

    维护一个 `depends.txt` 文件，记录项目的直接依赖包及 Python 环境信息。

  * `requirements.txt`

    维护 `requirements.txt` 文件，每次 Python 包有变动都要及时更新这个文件。最好在每次 release 之后都重新生成这个文件。

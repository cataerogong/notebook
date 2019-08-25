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

## 
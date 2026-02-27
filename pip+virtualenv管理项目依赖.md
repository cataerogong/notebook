# 使用 `pip` + `virtualenv` 管理 Python 项目的依赖项

## 安装

  * 主要工具：`pip`, `virtualenv`, `virtualenvwrapper-win`
  ```
  python -m pip install -upgrade pip
  pip install virtualenv
  pip install virtualenvwrapper-win
  ```

## 设置虚拟环境根目录

  设置环境变量 `WORKON_HOME=your\venv\root\folder`，所有的虚拟环境都将保存在这个目录下。

## 创建虚拟环境 (`virtualenv` + `virtualenvwrapper-win`)

  * 创建项目目录

  * 创建虚拟环境

    **在项目目录下**，执行以下命令创建虚拟环境，并关联项目目录
    ```
    mkvirtualenv -a . --no-download 虚拟环境名
    ```
    > 会在 `WORKON_HOME` 目录下创建 `虚拟环境名` 文件夹。

## 启动虚拟环境

  执行以下命令启动虚拟环境：
  ```
  workon 虚拟环境名
  ```

  > * 命令行提示符最前面会增加 `(虚拟环境名)` 标识。
  > * 如果关联了项目目录，会进入项目目录。
  > * 不带参数的 `workon` 会列出 `WORKON_HOME` 下的所有虚拟环境。

## 在虚拟环境中安装 Python 包

  * 启动虚拟环境后(`workon 虚拟环境名`)，使用 `pip` 安装 Python 包
    ```
    pip install <package>
    ```

  * 更新 `requirements.txt` 文件
    ```
    pip freeze > requirements.txt
    ```

## 建议

  * 系统 Python 环境

    系统 Python 环境中尽量不要安装 Python 包。

  * 项目虚拟环境

    为每个项目建立对应的虚拟环境，在其中安装项目所需的 Python 包。

  * `depends.txt`

    手工维护 `depends.txt` 文件，记录项目的 Python 环境信息及**直接**依赖包，格式建议如下：
    ```
    [requires]
    python_version = "3.12"

    [packages]
    pandas = "1.5.3"
    oracledb = "3.3.0"

    [dev-packages]
    PyInstaller = "*"
    ```

  * `requirements.txt`

    使用命令生成/更新 `requirements.txt` 文件。

    ```
    pip freeze > requirements.txt
    ```

    > * 这个文件记录了项目安装的所有 Python 包（包括直接安装和间接依赖安装），可以方便地恢复开发环境。
    > * 每次 Python 包有变动都要及时更新这个文件。
    > * 可以在项目每次 release 之后都重新生成这个文件，确保是最新的信息。

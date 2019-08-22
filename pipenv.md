# pipenv 笔记

基于 pipenv `version 2018.11.26`

* github: <https://github.com/pypa/pipenv/>
* docs: <https://docs.pipenv.org/>

## pipenv 是啥

* pipenv = pip + virtualenv
* 将安装的模块分为 *default* 和 *develop* 两类，仅开发时使用的模块 ( 比如测试模块 ) 安装在 *develop* 分类下，那么在生产部署时可以选择不安装这些 *develop* 模块

以下摘自 知乎 董伟明 [使用pipenv管理你的项目](<https://zhuanlan.zhihu.com/p/32913361>):

> Pipenv 是 Python 项目的依赖管理器。其实它不是什么先进的理念和技术，如果你熟悉 Node.js 的 npm/yarn 或 Ruby 的 bundler，那么就非常好理解了，它在思路上与这些工具类似。尽管pip可以安装Python包，但仍推荐使用Pipenv，因为它是一种更高级的工具，可简化依赖关系管理的常见使用情况。
>
> 主要特性包含：
>
> 1. 根据 Pipfile 自动寻找项目根目录。
> 2. 如果不存在，可以自动生成 Pipfile 和 Pipfile.lock。
> 3. 自动在项目目录的 .venv 目录创建虚拟环境。（当然这个目录地址通过设置WORKON_HOME改变）
> 4. 自动管理 Pipfile 新安装和删除的包。
> 5. 自动更新 pip。

## 安装 pipenv

`pip install pipenv`

## 指定虚拟环境文件夹位置

在创建虚拟环境之前，需要考虑 *虚拟环境文件夹* 的存放位置。

有 3 个位置，pipenv 运行时会通过环境变量来选择：

1. `PIPENV_VENV_IN_PROJECT=1`: (最高优先级)在项目目录内创建 `.venv` 文件夹
2. `WORKON_HOME=your/virtualenvs/path`: (次优先级)在指定目录内创建项目虚拟环境文件夹
3. (默认)在用户文件夹(C:\Users\username) 的 `.virtualenvs` 目录下创建项目的虚拟环境文件夹

**[ 注意 ]** 某些情况会导致 pipenv 找不到虚拟环境从而重新创建虚拟环境
1. pipenv 命令每次执行时都会判断环境变量，因此创建完虚拟环境后再改变环境变量会导致 pipenv 重新创建虚拟环境
2. 后两种模式下，所有项目的虚拟环境都是在同一个目录下的子文件夹，文件夹名由 pipenv 根据项目文件夹名自动生成，如果修改了项目文件夹名，会导致 pipenv 重新创建虚拟环境

**[ Tips ]** 可以在项目文件夹下用 `pipenv --venv` 命令显示对应虚拟环境的位置

## 创建虚拟环境

有多种创建虚拟环境的方式

* `pipenv --two|three`

  使用 python 2 或 3 创建一个 *初始虚拟环境* ( 只包含 python 环境和 pip、setuptools、wheel 模块 )

* `pipenv --python x[.y[.z]]`

  使用指定的 python 版本创建一个 *初始虚拟环境*，可以指定 1 到 3 位 python 版本号，如 `3`, `2.7`, `3.6.8`

* `pipenv install`

  + 如果项目根目录没下有 `Pipfile` 和 `Pipfile.lock` 文件，使用当前 python 版本创建一个 *初始虚拟环境*
    - 这里也可以添加 `--two|three` 和 `--python x[.y[.z]]` 参数指定 python 版本，等同于 `pipenv --two|three` 和 `pipenv --python x[.y[.z]]`

  + 如果项目根目录下有 `Pipfile` 和 `Pipfile.lock` 文件，根据这两个文件创建虚拟环境并安装相应的 python 模块
    - 这可以保证创建的虚拟环境与当初生成 `Pipfile`、`Pipfile.lock` 文件时的环境保持一致

## 安装 python 模块

`pipenv install <module-name>[version] [-d|--dev]`

* 类似于 `pip install`
* 会自动安装依赖模块
* 安装成功后会自动更新 `Pipfile` 和 `Pipfile.lock` 文件
* `[version]` 部分示例：
    ```
    pipenv install "requests>=1.4"   # will install a version equal or larger than 1.4.0
    pipenv install "requests<=2.13"  # will install a version equal or lower than 2.13.0
    pipenv install "requests>2.19"   # will install 2.19.1 but not 2.19.0
    ```
* `[-d|--dev]`: 将模块安装到 *develop* 分类下

## 卸载 python 模块

`pipenv uninstall <module-name>`

* 类似于 `pip uninstall`
* 卸载成功后会自动更新 `Pipfile` 和 `Pipfile.lock` 文件
* **[ 坑 ]** pipenv 不会自动卸载依赖模块，卸载后再运行 `pipenv clean` 可以卸载不再被依赖的模块

## 更新 python 模块

* `pipenv update <module-name>`

  更新指定模块

* `pipenv update`

  更新所有模块


#### To be continued...
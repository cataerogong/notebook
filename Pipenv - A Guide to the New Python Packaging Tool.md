    # Pipenv: A Guide to the New Python Packaging Tool
# Pipenv: 全新的 Python 包管理工具 使用指南

作者: [Alexander VanTol](https://realpython.com/pipenv-guide/#author)

原文: <https://realpython.com/pipenv-guide/>

目录

    * Problems that Pipenv Solves Pipenv 解决的问题
      + Dependency Management with requirements.txt 利用 requirements.txt 进行依赖项管理
      + Development of Projects with Different Dependencies 具有不同的依赖项的多项目开发
      + Dependency Resolution 依赖项解决方案
    Pipenv Introduction 
        Example Usage
        Pipenv’s Dependency Resolution Approach
        The Pipfile
        The Pipfile.lock
        Pipenv Extra Features
    Package Distribution
        Yes, I need to distribute my code as a package
        I don’t need to distribute my code as a package
    I already have a requirements.txt. How do I convert to a Pipfile?
    What’s next?
    Is Pipenv worth checking out?
    References, further reading, interesting discussions, and so forth

    Pipenv is a packaging tool for Python that solves some common problems associated with the typical workflow using pip, virtualenv, and the good old requirements.txt.

Pipenv 是一个 Python 的包管理工具，它解决了原本使用 `pip`、`virtualenv` 和 `requirements.txt` 的开发流程中的一些常见问题。

    In addition to addressing some common issues, it consolidates and simplifies the development process to a single command line tool.

除了解决一些常见问题，它还将（原本需要使用多种工具的）开发过程整合、化简到一个单一的命令行工具上。

    This guide will go over what problems Pipenv solves and how to manage your Python dependencies with Pipenv. Additionally, it will cover how Pipenv fits in with previous methods for package distribution.

这份指南将会详细介绍 Pipenv 解决的问题与如何用 Pipenv 管理你的 Python 依赖项。另外，还会介绍如何将 Pipenv 与以前的包分发方式相结合。

    ## Problems that Pipenv Solves
## Pipenv 解决的问题

    To understand the benefits of Pipenv, it’s important to walk through the current methods for packaging and dependency management in Python.

为了更好地了解 Pipenv 的优点，必须先看看当前 Python 中的打包和依赖项管理方式。

    Let’s start with a typical situation of handling third-party packages. We’ll then build our way towards deploying a complete Python application.

让我们从处理第三方包的典型情况开始，然后我们将部署一个完整的 Python 应用。

    ### Dependency Management with requirements.txt
### 利用 `requirements.txt` 进行依赖项管理

    Imagine you’re working on a Python project that uses a third-party package like flask. You’ll need to specify that requirement so that other developers and automated systems can run your application.

假设你正在参与开发的 Python 项目中使用了一个第三方包，例如 `flask`。为了让其他开发者和自动化系统能够运行你的这个应用，你需要特别指明这个要求。

    So you decide to include the flask dependency in a requirements.txt file:

于是你决定在 `requirements.txt` 文件中加入 `flask` 依赖项。

```
# Python Requirements
flask
```

    Great, everything works fine locally, and after hacking away on your app for a while, you decide to move it to production. Here’s where things get a little scary…

非常好，在本地一切都工作正常。然后你又对你的应用进行了一些改进，决定让它进入生产环境。从这儿开始，事情开始变得微妙起来……

    The above requirements.txt file doesn’t specify which version of flask to use. In this case, pip install -r requirements.txt will install the latest version by default. This is okay unless there are interface or behavior changes in the newest version that break our application.

上面的 `requirements.txt` 文件没有指明使用 `flask` 的哪个版本。这种情况下， `pip install -r requirements.txt` 会默认安装最新的版本。这一般没问题，除非最新版本中接口或处理逻辑改变了，从而使我们的应用崩溃。

    For the sake of this example, let’s say that a new version of flask got released. However, it isn’t backward compatible with the version you used during development.

为了这个例子，我们假设 `flask` 又发布了一个新版本。然而，它与你开发过程中使用的那个版本不兼容。

    Now, let’s say you deploy your application to production and do a pip install -r requirements.txt. Pip gets the latest, not-backward-compatible version of flask, and just like that, your application breaks… in production.

现在，我们假设你将你的应用部署到了生产环境，执行了 `pip install -r requirements.txt`。Pip 获取了最新的、不兼容的 `flask` 版本，就像上面说的，你的应用崩溃了……在生产环境里。

“But hey, it worked on my machine!”—I’ve been there myself, and it’s not a great feeling.

“嘿，但它在我的机器上工作正常！”——我也曾亲身经历过，这种滋味不好受。

At this point, you know that the version of flask you used during development worked fine. So, to fix things, you try to be a little more specific in your requirements.txt. You add a version specifier to the flask dependency. This is also called pinning a dependency:

到这里，你知道你开发时使用的那个 `flask` 版本工作正常。所以，为了解决问题，你试着在 `requirements.txt` 文件中增加一些更明确的信息。你在 `flask` 依赖项上增加了 *version specifier*。这也叫 *固定* 依赖项。

```
# Python Requirements
flask==0.12.1
```

    Pinning the flask dependency to a specific version ensures that a pip install -r requirements.txt sets up the exact version of flask you used during development. But does it really?

将 `flask` 依赖项固定在一个特定版本，就确保 `pip install -r requirements.txt` 安装的就是你开发时使用的那个 `flask` 版本。但真的是这样吗？

    Keep in mind that flask itself has dependencies as well (which pip installs automatically). However, flask itself doesn’t specify exact versions for its dependencies. For example, it allows any version of Werkzeug>=0.14.

别忘了，`flask` 本身也有依赖项（pip 会自动安装）。然而，`flask` 本身并没有指定它的依赖项的确切版本。例如，它允许 `Werkzeug>=0.14` 的任何版本。

    Again, for the sake of this example, let’s say a new version of Werkzeug got released, but it introduces a show-stopper bug to your application.

再一次，为了这个例子，我们假设 `Werkzeug` 发布了新版本，而这个版本为你的应用引入了一个停机缺陷。

    When you do pip install -r requirements.txt in production this time, you will get flask==0.12.1 since you’ve pinned that requirement. However, unfortunately, you’ll get the latest, buggy version of Werkzeug. Again, the product breaks in production.

这次，当你在生产环境中运行 `pip install -r requirements.txt`，由于你固定了要求，你会获得 `flask==0.12.1`。然而不幸的是，你也会获得最新的、有缺陷的 `Werkzeug` 版本。再一次，应用在生产环境中崩溃了。

    The real issue here is that the build isn’t deterministic. What I mean by that is that, given the same input (the requirements.txt file), pip doesn’t always produce the same environment. At the moment, you can’t easily replicate the exact environment you have on your development machine in production.

这里真正的问题是：**构建过程具有不确定性**。我的意思是，给定同样的输入（`requirements.txt` 文件），pip 不能总是产生同样的环境。目前，你无法轻松地将你开发机器上的环境完全复制到生产环境中。


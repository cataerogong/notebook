# Development with Git

## 分支管理

### 分支的划分

工程的分支主要分为 master、dev、hotfix、feature 四类。

* master：线上代码主分支，该代码和线上代码一致
* dev: 开发分支，包含即将上线的新功能，由各个新功能开发分支经测试后合入，属于分支测试后的产物
* feature: 功能开发分支，当有新开发任务时，开发需要从dev分支拉取 feature 分支，开发完毕经过分支测试后，可以进行 pull request 请求，申请将分支合入 dev 分支，该分支是开发过程中最常使用的分支
* hotfix: bug 修复分支，或紧急需求开发分支（一般不要在 hotfix 分支上进行新需求的开发）。该分支从 master 分支拉出，经开发测试完成之后，可以进行 pull requets，申请将分支合入 master

**[ 注意事项 ]**

* feature 只能从 dev 分支拉出，hotfix 分支只能从 master 拉出
* 在进行 pull/merge request 请求之前必须对当前的开发分支进行反合，即 dev 分支反合 feature 分支，master 分支反合 hotfix 分支
* dev 分支会在稳定之后合入 master 分支
* 不能将 master 分支与 feature 反合，dev 分支与 hotfix 反合
* 开发只能将代码提交至对应的开发分支，不能直接提交到 master 分支或 dev 分支

### 分支的提交注意事项

* 在拉取新分支之前一定要确保本地的 master 分支和 dev 分支代码是最新的（在拉分支之前进行 pull 操作）
* 分支的 pull 和 push 请用 git 命令或 16 版本及以上 IDEA 完成，不要使用 eclipse
* 本地代码提交时需要确保本地分支对应的远程分支代码最新，具体在进行提交操作之前请进行 pull 操作
* 代码提交时要进行相关注释，说明修改的代码内容；建议提高代码提交的频率，这样在出现问题时方便问题的定位与代码的回滚
* 代码提交时要在本地解决冲突，冲突解决完成，并且代码在本地可以编译通过之后才能提交代码
* 在 windows 下进行开发一定要注意 git 有关换行符的问题（ CRLF 与 LF 的问题），具体请在 git 中设置相关的配置（git config --global core.autocrlf true），并在开发工具中将默认的环境设置为 linux，避免提交的代码出现大量的冲突。如果出现这种情况的冲突，请不要提交代码到远程仓库，本地解决之后再提

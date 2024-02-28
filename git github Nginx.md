## 项目上传至github


---
## git常用操作

#### 提交

```bash
$ git add . #添加所有改动过的文件
    // 如果想忽略某个文件，需要新建一个.gitignore文件,写入想忽略的文件名称
$ git add <file> #添加指定的文件
$ git mv <old> <new> #文件重命名
$ git rm <file> #删除文件
$ git rm -cached <file> #停止跟踪文件但不删除
$ git commit -m <file> # 提交指定文件
$ git commit -m “commit message” #提交所有更新过的文件
$ git commit -amend # 修改最后一次提交
$ git commit -C HEAD -a -amend #增补提交（不会产生新的提交历史纪录）
```

#### 撤消操作

```bash
$ git reset -hard HEAD #撤消工作目录中所有未提交文件的修改内容  比如删除也可以撤销
$ git checkout HEAD <file1> <file2> #撤消指定的未提交文件的修改内容
$ git checkout HEAD. #撤消所有文件
$ git revert <commit> #撤消指定的提交
```

#### 分支

```bash
git branch
git branch -a

git branch 分支名   // 创建分支
git checkout 分支名
git checkout -b 分支名  // 如果不存在，创建分支

git branch -d 分支名    // 删除分支
-d  // 合并到master后删除
-D // 硬删

git merge 分支名

git revert HEAD     // 撤销前一次commit
git reset --hard    // 撤销所有本地修改

git branch -v 查找远程分支
git branch branch_name remote_name/branch  // 基于远程仓库创建新分支
git checkout -b branch_name remote_name/branch // 基于远程仓库创建新分支并且切换到新分支

git remote prune origin // 同步和清理本地的远程分支
```

## github

### 1. 本机生成ssh

```bash
ssh-keygen -t rsa -C "你在gitee/github/gitlab上注册帐号时填写的邮箱"
```

**注意！！不要填密码passport**
用户下会有.ssh文件  .pub的是公钥

### 2. github添加ssh

头像 →  settings → SSH and GPG keys → add一个

## nginx

#### 启动

C:\server\nginx-1.0.2>start nginx

或

C:\server\nginx-1.0.2>nginx.exe

注：建议使用第一种，第二种会使你的cmd窗口一直处于执行中，不能进行其他命令操作。

#### 关闭

C:\server\nginx-1.0.2>nginx.exe -s stop

或

C:\server\nginx-1.0.2>nginx.exe -s quit

注：stop是快速停止nginx，可能并不保存相关信息；quit是完整有序的停止nginx，并保存相关信息。

#### 重启

C:\server\nginx-1.0.2>nginx.exe -s reload

当配置信息修改，需要重新载入这些配置时使用此命令。

#### 查看版本

C:\server\nginx-1.0.2>nginx -v

## Nginx虚拟目录alias和root目录

<https://www.cnblogs.com/kevingrace/p/6187482.html>

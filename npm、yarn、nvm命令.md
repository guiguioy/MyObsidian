# npm

## 下载nodejs

1.  官网下载安装
    <https://nodejs.org/en/>
2.  命令行  node -v 查看版本
3.  升级最新版本 官网去下了安装

## 使用nvm管理多个版本的nodejs

下载地址
[nvm github](https://github.com/coreybutler/nvm-windows)

NVM 安装成功后会自动生成环境变量 NVM\_HOME 和 NVM\_SYMLINK<br>
NVM\_HOME ：NVM 安装路径<br>
NVM\_SYMLINK ： NodeJS 快捷方式路径

```sh
# 查看可安装的nodejs版本
nvm list available

# 使用 nvm install 版本号 命令，安装指定版本的 NodeJS，如：
nvm install 14.21.1

# 切换nodejs版本
nvm use 14.21.1

# 查看目前已安装的Nodejs版本
nvm list
```

## cnpm

# yarn

### 安装

1.

## npm和yarn命令对比

<https://www.jianshu.com/p/e7209ecc120d>

## 升级指定包

<https://blog.csdn.net/weixin_39825105/article/details/111608511>

## tyarn

### package-lock.json和package.json和yarn.lock

package.json中版本号详解\~和^和\*的区别

    ~ 会匹配最近的小版本依赖包，比如~1.2.3会匹配所有1.2.x版本，但是不包括1.3.0
    ^ 会匹配最新的大版本依赖包，比如^1.2.3会匹配所有1.x.x的包，包括1.3.0，但是不包括2.0.0
    这意味着安装最新版本的依赖包
    推荐使用~，只会修复版本的bug，比较稳定
    使用^ ，有的小版本更新后会引入新的问题导致项目不稳定，

### package.json、package-lock.json和yarn.lock

<https://blog.csdn.net/weixin_50736511/article/details/127574137>

### npm install 安装依赖包 --save、--save-dev、-S、-D的区别

<https://blog.csdn.net/aaqingying/article/details/101371352>

### npm install 安装某个指定的版本

<https://www.cnblogs.com/yetiezhu/p/12813532.html>

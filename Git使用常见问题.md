# Git 使用常见问题



## 1. Failed to connect to raw.githubusercontent.com port 443


**方法一（推荐）**
直接在命令行中输入

```
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```



**方法二**

- 修改Hosts文件，首先查询真实IP, 在https://www.ipaddress.com 查询raw.githubusercontent.com 的真实IP

- 然后修改Hosts文件, 在终端输入sudo vim /etc/hosts,在hosts文件中添加以下内容

```
199.232.68.133(刚刚查到的ip) raw.githubusercontent.com
```



## 2.Failed to connect to github.com port 443 after 17992 ms: Operation timed out

**方案一：删除代理**

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```



**方案二：注释掉host修改**

这种情况下我即开了ClashX，又在host中对github.com的ip进行了绑定。此时去掉hosts中的修改，仅仅保留ClashX即可



## 3.remote: Support for password authentication was removed on August 13, 2021

`原先的密码凭证从2021年8月13日`开始就不能用了，`必须使用个人访问令牌（personal access token）`，就是把你的`密码`替换成`token`！

- 登录自己的github账号，个人设置那里

![img](1.png)

- 选择开发者设置 Developer setting

![img](2.png)

- 选择个人访问令牌 Personal access tokens，然后选中生成令牌 Generate new token

![img](3.png)

- 设置token的有效期，访问权限等

```
选择要授予此令牌token的范围或权限。
要使用token从命令行访问仓库，请选择repo。
要使用token从命令行删除仓库，请选择delete_repo
其他根据需要进行勾选
```

![img](4.png)

- 最后生成令牌 Generate token

![img](/Users/apple/Documents/P14_VersionControlAndCodeReview/Git/Git_QA/5.png)

- 生成后的token如下：

![img](6.png)

注意：

记得把你的token保存下来，因为你再次刷新网页的时候，你已经没有办法看到它了，之后用自己生成的token登录，把上面生成的token粘贴到输入密码的位置，然后成功push代码！也可以 把token直接添加远程仓库链接中，这样就可以避免同一个仓库每次提交代码都要输入token了：

```
git remote set-url origin https://<your_token>@github.com/<USERNAME>/<REPO>.git

<your_token>：换成你自己得到的token
<USERNAME>：是你自己github的用户名
<REPO>：是你的仓库名称
```




例如：（全局设置某一个仓库的 token）以后每次提交都不需要账户和密码了

` git remote set-url origin https://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@github.com/github的用户名/仓库名称`

最后提交 直接输入： `git push`     

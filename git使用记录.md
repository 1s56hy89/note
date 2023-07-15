# git 使用语句

## 一般语句

1.初始化
>git init //-b main

2.新建仓库
>git remote add origin 仓库远程地址

3.更改仓库
>方法①
>git remote set-url origin 仓库远程地址
>方法②
>git remote rm origin
>git remote add origin 仓库远程地址

4.提交代码
>git add .
>git commit -m 提交原因

5.远程仓库同步
>git pull --rebase origin main

6.将本地代码推送
>git push origin main
>git push -u origin main

7.强制推送，覆盖远程仓库代码(不要轻易使用,新仓库可以随意)
>git push origin main --force

8.拉取代码
>git pull origin main

9.创建分支
>git checkout -b (main)

10.合并分支
>git merge main

## 同时使用github和gitee

1.新建仓库github
>git init
>git remote add origin ...

2.查看当前
>git remote
不出意外会输出
origin
远程仓库重命名
git remote rename origin github
可以再次查看，会输出
github origin  https://github.com/&lt;远程地址&gt; (fetch)
github origin  https://github.com/&lt;远程地址&gt; (push)
添加码云的地址
git remote add <u>gitee</u> &lt;远程地址&gt;
推送更改为
git push github main
git pull github main
git push gitee main
git pull gitee main
删除一个远程仓库地址
git remote remove gitee

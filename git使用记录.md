# git 使用语句

## 一般语句

1. 初始化
    >git init //-b main

2. 新建仓库
    >git remote add origin 仓库远程地址

3. 更改仓库
    >方法①
    >git remote set-url origin 仓库远程地址
    >方法②
    >git remote rm origin
    >git remote add origin 仓库远程地址

4. 提交代码
    >git add .
    >git commit -m 提交原因

5. 远程仓库同步
    >git pull --rebase origin main

6. 将本地代码推送
    >git push origin main
    >git push -u origin main

7. 强制推送，覆盖远程仓库代码(不要轻易使用,新仓库可以随意)
    >git push origin main --force

8. 拉取代码
    >git pull origin main

9. 创建分支
    >git checkout -b (main)

10. 合并分支
    >git merge main

## 同时使用github和gitee

### 配置github和gitee的公钥

1. 生成公钥

    ```c
    ssh-keygen -t rsa -C 'github邮箱号' -f ~/.ssh/id_rsa_github
    ssh-keygen -t rsa -C 'gitee邮箱号' -f ~/.ssh/id_rsa_gitee
    ```

2. 添加公钥到github和gitee

3. 配置config
    >进入.ssh文件，有则直接修改，无则重新创建

    ```c
    gitee
    Host gitee.com
    HostName gitee.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_gitee
    github
    Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_github
    ```

4. 测试链接

    ```c
    gitee
    ssh -T git@gitee.com
    github
    ssh -T git@github.com
    ```

### 使用git上传github和gitee

1. 新建仓库初始化

    ```c
    git init
    ```

2. 添加两条仓库地址

    ```c
    git add . //添加全部文件
    git commit -m "first commit" //添加上传注释
    git remote add github [github仓库地址_建议采用ssh地址]
    git remote add gitee [gitee仓库地址_建议采用ssh地址]
    ```

3. 推送更改为

    ```c
    git push github main
    git pull github main
    git push gitee main
    git pull gitee main
    ```

4. 删除一个远程仓库地址

    `git remote rm gitee`

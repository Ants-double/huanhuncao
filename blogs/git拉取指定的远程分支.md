# 直接拉取
```
 git clone -b ants git@github.com:Ants-double/CareerJava.git
 git clone -b 远程分支名  仓库地址

```

# 本地已经有相关的仓库代码
```
//查看远程分支
git branch -r
//创建本地分支并关联
git checkout -b 本地分支 origin/远程分支

//已有本地分支创建关联
git branch --set-upstream-to origin/远程分支名  本地分支名
//拉取
git pull

```




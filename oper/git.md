Git

git add -a 添加暂存 从红->绿

git commit -m 'test' 把添加暂存的新文件提交

git commit -am '' 把修改的文件提交

git status 查看状态

1
git clone + 远程地址 克隆 适合本地没有代码
2
git remote set-url origin https://new.url.to.your/repo.git 切换远程
git remote add origin + 远程仓库

git remote -v
git pull  拉取

git push -u origin 分支名 推送

git push origin master

分支 
git checkout -b 分支名 创建分支并切换到新分支
git checkout 分支名 切换分支 



### 撤销修改  

已修改但未暂存

git checkout【名】

已暂存但未提交

git reset【名】

已提交撤销提交

git revert 【hash】

git reset --hard 【想回到的哪一集hash】

显示所有log 

git reflog

补充最新提交内容

git commit -m '信息' --amend



### 问题

#### 1.出现 timeout

查看电脑网络的代理 查看端口

设置  git config --global http.proxy http://127.0.0.1:7890 ;git config --global https.proxy http://127.0.0.1:7890 即可


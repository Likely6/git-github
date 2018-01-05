###git常用命令
git config --list ^^查看配置列表
git config --global user.name 'username'  ^^配置用户名和邮箱
git config --global user.email 'youremail@qq.com'
git init  ^^初始化仓库（此时目录下会多出一个.git目录，是用来跟踪版管理本库的  用ls -ah来查看）
git add readme.txt  ^^添加文件到版本库的暂存区
git commit -m '添加readme.txt文件'  ^^将缓存区文件提交到当前分支
git status  ^^查看仓库状态
git diff readme.txt ^^查看具体修改情况
git log ^^显示提交日志（git log --pretty=oneline  可以一行显示免得显示太乱）
git reset --hard HEAD^  ^^回退到上一个版本（HEAD表示当前版本 HEAD^表示上一个版本 HEAD^^表示上上个版本以此类推  也可以HEAD~10表示回退多山版本）
git reset --hard b87431a   ^^指定版本号回退（不需要写全版本号）
git reflog  ^^查看你的每一条命令
git checkout -- readme.txt  ^^丢弃工作区readme.txt的修改 其实是用版本库里的最新版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”   
git reset HEAD readme.txt ^^移除暂存区的readme.txt文件(就是当你add后需要撤回时)
git rm test.txt ^^删除指定文件,删除文件后你有两个选择，1.确实要删除该文件（commit就直接从版本库删了） 2.删错了，要恢复（checkout可恢复）
git remote add origin git@............  ^^然后关联远程仓库
git pull origin master  ^^拉取远程master分支
git push -u origin master ^^推送当前分支到远程
git checkout -b dev ^^在当前分支创建并切换分支
git branch dev  ^^在当前分支创建dev分支
git checkout dev  ^^切换分支到dev
git branch  ^^查看分支 会列出所有分支 列表中带\*表示当前分支
git merge dev ^^合并指定分支到当前分支
git merge --on-ff -m '合并分支' dev ^^--on-ff为普通模式合并分支 删除分之后也有分支信息
git branch -d dev ^^删除dev分支
git branch -D dev  ^^强行删除dev分支   如果要丢弃一个没有被合并过的分支时
git log --graph ^^查看分支合并图 
git stash ^^将当前工作现场存储起来，等回复现场后继续工作
git stash list  ^^查看刚刚存储起来的工作现场
git stash apply ^^恢复现场
git stash drop ^^删除现场(删除后git stash list 查寻不到)
git stash pop ^^恢复且删除现场(删除后git stash list 查寻不到)

###创建秘钥（用于连接github仓库）与添加秘钥关联远程仓库
1.  cd ~/.ssh ^^查看是否已有秘钥
2.  ssh-keygen -t rsa -C 'youremail@163.com'  ^^创建秘钥一路回车（生成一个私钥一个公钥）
3.  登录github  settings -> SSH and GPG keys -> New SSH key ^^在github里添加ssh公钥 
4.  git remote add origin git@............  ^^然后关联远程仓库
5.  下一步是 如果远程仓库有内容 则先拉取后推送 没有则直接推送
6.git pull origin master  ^^拉取
7.git push -u origin master ^^推送

###用到的CMD命令
mkdir demo  ^^创建demo文件夹
cd demo ^^进入到该目录下的demo文件夹
pwd ^^显示当前目录所在位置
echo "hello world" > readme.txt ^^创建readme.txt文件并写入'hello world'
cat readme.txt  ^^查看文件内容
rm test.txt ^^删除指定文件

###小结：
1. 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除
2. 开发新功能时，通常会新建feature分支进行开发，然后合并，最后删除
3. 当你的小伙伴从远程库clone到本地时，默认情况下，你的小伙伴只能看到本地的master分支。现在，你的小伙伴要在dev分支上开发，就必须创建远程origin的dev分支到本地  git checkout -b dev origin/dev
4. 多人协作的工作模式通常是这样：
首先，可以试图用git push origin branch-name推送自己的修改；
如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
如果合并有冲突，则解决冲突，并在本地提交；
没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！
如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。
5. fork别人仓库后进行修改
在GitHub上，可以任意Fork开源仓库；
自己拥有Fork后的仓库的读写权限；
可以推送pull request给官方仓库来贡献代码

具体可学习廖雪峰老师的git教程：https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

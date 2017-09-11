# clone git project
   git clone git@gitlib28:chenxuelin/schedule.git
# check out svn project with same directory of git project
   svn co svn://192.168.1.66/namtso/branch/web_code/svntest schedule --username chenxl --password xuelin
# add ignore of svn,attention that has a enter after git and has dot in the end
   svn propset svn:ignore ".git
   .gitignore" .
   svn status 查看状态
# commit to svn 
  svn add *
  svn commit -m "result from git"  --username chenxl --password xuelin
# commit to git
   git add * 
   git commit -m "add .svn path to git res"
   git push
# add test file in git and check in to svn
   vi test.md
   git add test.md
   git commit -m 'add test.md'
   svn add test.md 
   svn commit -m 'check in file from git'  --username chenxl --password xuelin
   git commit -m 'delete test.md'
   git pull
   svn add * --force
   svn commit -m 'test add file' --username chenxl --password xuelin
   删除文件无法自动提交到svn中
   
# git-svn
   echo xuelin|git svn clone svn://192.168.1.66/namtso/branch/web_code/tp5-project -r29318:HEAD --username chenxl
   git branch
   git remote add origin git@gitlib28:chenxuelin/schedule.git
   git pull origin master ctrl+x提交
   git branch --set-upstream-to=origin/master
   强制刷新本地版本为远程仓库
   git fetch --all
   git reset --hard origin/master 
   # Append svn:ignore settings to the default Git exclude file:
   git svn show-ignore >> .git/info/exclude
   git svn dcommit
   
# from git commit to svn
   1、create new clone project
   git clone git@gitlib28:chenxuelin/schedule
   cd schedule
   2、create new svn clone project
   echo xuelin|git svn clone svn://192.168.1.66/namtso/branch/web_code/tp5 -r29318:HEAD --username chenxl
   cd tp5
   git remote add origin git@gitlib28:chenxuelin/schedule.git

# git version commit to svn
   http://blog.csdn.net/zhangskd/article/details/43452627
   1. git clone git@gitlib28:chenxuelin/schedule
   2. git svn init svn://192.168.1.66/namtso/branch/web_code/tp5 
   3. git svn fetch
   4. git show-ref svn | tail -n 1
       f7e97acecbb8098757d9dc451b3c76eb59c4da9d refs/remotes/origin/master
   5. git log --pretty=oneline master | tail -n 1 
       8041fab27f1ff38f980b9ea00fd335c50005af8c nf:  create svntest project
   6. echo "8041fab27f1ff38f980b9ea00fd335c50005af8c 5194b04324e1fa8bcec215ec053c5e707d2e4b83" >> .git/info/grafts
   试验失败
   
# another
   1、echo xuelin|git svn clone svn://192.168.1.66/namtso/branch/web_code/tp5 -r29318:HEAD --username chenxl
   2、git remote add origin git@gitlib28:chenxuelin/schedule.git
   3、git branch --set-upstream-to=origin/master master
   4、git pull origin 
   5、git svn dcommit
   6、git checkout -b newfeature
   7、git checkout master
   8、git merge newfeature
   9、git push origin
   10、git svn dcommit
   
 # schedule project
 
    1. install git-svn
       apt install git-svn
    2. clone svn project,that is empty project
       echo xuelin|git svn clone svn://192.168.1.66/namtso/branch/web_code/schedule -r29318:HEAD --username chenxl
    3. update from svn
       git svn rebase
    4. find all branch
       git branch -a
    5. add remote git repository
       git remote add origin git@gitlab28:chenxuelin/schedule.git    
    6. set master branch upstream
       git branch --set-upstream-to=origin/master master
    7. pull data from remote git
       git pull origin ==》ctrl+x
    8. submit to svn
       git svn dcommit
    9. develope in branch 
       git checkout -b "cxl"   
       git rm test.md
       git commit -m "made some change"
    10.return to master for push to remote of git&svn
       git checkout master
       git merge cxl
       git push origin master
       git svn dcommit
    11.add ignore from git to svn
       git svn show-ignore >> .git/info/exclude
       
# tp5 project
      
    1. clone svn project,that is empty project
       echo xuelin|git svn clone svn://192.168.1.66/namtso/branch/web_code/spi -r29318:HEAD --username chenxl
    2. cd spi
    3. add remote git repository
       git remote add origin git@gitlab28:websrc/spi.git
    4. make some change
    5. git add .
    6. git commit -m 'add ignore'
    7. submit to remote git
    		git push -u origin master
    8. submit to svn
       git svn dcommit

# spi project
    1. clone svn project spi-front  
    		echo xuelin|git svn clone svn://192.168.1.66/EmicallDev/ApplicationPlatform/sandbox/WebApplication/spi-front -r3000:HEAD --username chenxl 
    2. clone svn project spi-php
    		echo xuelin|git svn clone svn://192.168.1.66/EmicallDev/ApplicationPlatform/sandbox/WebApplication/spi-php -r3000:HEAD --username chenxl
    3. cd spi-php
    4. add remote git repository
       git remote add origin git@gitlab28:websrc/spi.git
    5. view remote info
       git remote -v
    6. pull data from remote git
    		git pull origin
    7. git branch -a
       * master
       		remotes/git-svn
       		remotes/origin/master
    8. merge origin/master to local branch master
    		git merge remotes/origin/master ==》ctrl+x
    9. add ignore from git to svn
       git svn show-ignore >> .git/info/exclude
    10.create branch of "bin" 
       git checkout -b "bin"

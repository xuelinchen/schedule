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

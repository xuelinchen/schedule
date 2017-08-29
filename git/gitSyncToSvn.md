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
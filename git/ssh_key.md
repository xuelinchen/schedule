# 配置两个key，一个给github，一个给本地gitlib

# cd ~/.ssh
# ssh-keygen -t rsa -C "303566@qq.com" -f ~/.ssh/github
# 在目录下有两个文件 github和github.pub，cat github.pub拷贝内容
# 登录github》》your profile》》ssh keys》》粘贴内容到sshkey

# ssh-keygen -t rsa -C "chenxuelin@emicnet.com" -f ~/.ssh/gitlib-cxl
# 在目录下有两个文件 gitlib-cxl和gitlib-cxl.pub，cat gitlib-cxl.pub拷贝内容
# 登录gitlib》》your profile》》ssh keys》》粘贴内容到sshkey

# 创建~/.ssh/config
   #303566-github
  host github
  user git
  hostname github.com
  port 22
  identityfile ~/.ssh/github
  #chenxuelin-gitlib28
  host gitlib28
  user git
  hostname 10.0.0.28
  port 22
  identityfile ~/.ssh/gitlib-cxl
  
# 测试
## root@1604developer:~/.ssh# ssh -T gitlib28
    Welcome to GitLab, chenxuelin!
## root@1604developer:~/.ssh# ssh -T github
    Hi xuelinchen! You've successfully authenticated, but GitHub does not provide shell access.
    
    
# 在github创建项目
   git clone git@github:xuelinchen/schedule.git
   # 增加remote仓库
   git remote add gitlib28 git@gitlib28:chenxuelin/schedule.git
   # 提交结果到远程仓库
   git push gitlib28
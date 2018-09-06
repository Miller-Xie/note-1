
centos  
git  
Gitbook  


1. 安装nodejs
```
yum install nodejs
```

2. 安装Gitbook
```
npm install gitbook-cli -g
gitbook -V
```
3. 安装git
```
sudo yum install git
```
4. 把github上项目clone下来
```
git remote add note git@github.com:#/note.git
ssh-keygen -t rsa -C "#@163.com"
cat /root/.ssh/id_rsa.pub
ssh -T git@github.com
```

5. gitbook init
6. book.json

7. gitbook serve --port 80

fuser -n tcp 4000
kill -9 17126

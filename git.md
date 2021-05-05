# Structure
Working Directory

// git add
untracked -> tracked

// git commit
로컬에 집어넣음

Local Repository

// git remote add origin
연결해서 pipeline을 만듦

// git push
서버에 올림
// git pull
 서버에서 받음

Remote Repository (Server)

## Git Config
### create remote repository in Github
git config --list
git config user.name
//git config --glbal user.name <github-name>
git config user.email
//git config --global user.email <email>

cat ~/.gitconfig

//grep = filtering
git config --list | grep "user.name"

## Make connection (Working Directory <--> Local Repository)
### create local repository
git init
.gitignore 파일 생성 // VS code에 .gitignore 새파일을 만들어도 됨.
서버에 올리지 않아도 되는 필요없는 파일은 .gitignore 파일에 직접 넣어도 됨
***
.vscode
b.txt
***
cmd에서는 echo git.md >> .gitignore

#### local repository에 파일 올리기
git add --all
git add <filename>, git add .

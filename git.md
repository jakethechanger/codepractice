# Structure
Working Directory

// git add -> Send to Staging Area
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

### local repository에 파일 올리기
git add --all
git add <filename>, git add .

### local repository에 파일 저장
git commit -am "message"
git commit -m "message"


## Make connection (Local Repo <--> Remote Repo)
git remote add origin <git-remote-url>

```
remote origin master v remote branch v origin master v branch
```

### 파일 올리기
git push -u origin master
//한번만 하면 됨
//push Up origin as master (To remote repo)

git push -fu origin master
//에러, 충돌 무시하고 push

```
Do the pull first before push
```


## Reset (돌아가기) v Merge (충돌시 병합하기)

### 상태 명령어
git log
git log --graph --oneline
git log --oneline


### git reset v git revert
git reset -- [hard | soft | mixed]
hard는 시계(모든것)를 되돌림. 그래서 되돌린 시점 이후에 생성되었던 변경, 소스가 지워짐.
*다른 사람의 소스도 지워짐

git revert
history쌓임, 소스 그대로

### git lens
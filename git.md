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
This is to use the git control in VS code

### Rollback
git reset 239ff16
```
* eef79e1 (HEAD -> master, origin/master, origin/HEAD) Update: git lens:comment
* 239ff16 Update: git lens
* 51532d0 Update: 6/5/2021 morning
* 1c2b9bc Update: test2
* c587f5d Update: new folder commit
* 9967703 Update: 3rd commit
* 9b37dec Create README.md
* 222563f Update: 2nd commit
* 66b5c57 Upload: first commit
```

리셋해도 로컬 디렉토리의 소스는 변화가 없다
git log에서 히스토리는 없어짐.
git commit, git push하면 reject. (로컬하고 리모트 소스가 다르기때문에)
File History에서 차이를 보고 똑같이 맞춰줘야 함.

똑같이 맞추고 git add, git commit, git push해도 reject 됨
git push origin +master

git push -fu origin master //에러, 충돌 무시하고 push와 같은 의미인듯.

#### git revert
git revert cf5f216
```
error: could not revert cf5f216... Update: Before adding git revert
hint: after resolving the conflicts, mark the corrected paths
hint: with 'git add <paths>' or 'git rm <paths>'
hint: and commit the result with 'git commit'
```
Conflict 발생 - 한개의 파일을 두방향에서 (보통 두사람, 여기서는 2리비젼에서 일어남)
//revert는 이전으로 돌아가기만 할뿐 그사이의 변경사항을 지우지 않기때문에 conflict 발생  

동일 파일이 여러방향에서 수정되어 서로 다르면 확인후 모든 변경사항을 받아들이거나 어느한쪽을 받아들이지 않으면 된다.

만약 양방향에서 수정이 일어났을경우 push에서 reject. git pull을 해서 conflict를 해결 (양방향 수정을 모두 승인하거나 상대방 수정사항을 무시하고 내것만 push할수도 있다.)


## Git Branch

git branch #로컬에 있는 브랜치 이름
git branch -r #서버에 있는 브랜치 이름
git branch -a #양쪽 브랜치 모두 보기
#### 브랜치 생성 및 변경전에 반드시 commit

git checkout <branch-name>

git branch <branch-name> #로컬에 브랜치 올리기
git push origin <branch-name> #서버에 브랜치 올리기

git branch -d <branch-name> #로컬에서 브랜치 삭제
git push --delete origin <branch-name>  #서버에서 브랜치 삭제
### Master로 Merge해주기
Branch에서 작업한 자료 (예를 들어 a.py)를 Master의 a.py에 입력해 주는과정

1. Maset로 Merge하기 (In Working directory)
git checkout master #master로 변경
git merge <branch-name>

그래서 br2에서 br1의 코드를 가져오려면
git checkout br2
git merge br1

### Diff
- git diff <branch-name>
- git diff <branch-name> <file-name>
- git checkout -p <branch-name> <file-name> #브랜치에 있는 변경사항을 내 브랜치로 패치해서 가져옴

*** git pull은 마스터의 소스만 온다.
그래서 Remote의 마스터 소스를 Local의 마스터로 받고 다시 브랜치로 patch해서 사용.

만약 서버의 특정 브랜치를 가져오고 싶으면... (t = target, origin(서버를 지칭)/<branch-name>)
git checkout -t origin/<branch-name>

특정 브랜치를 pull하고 싶다면
git pull origin <branch-name> v git push origin <branch-name>


#### 회사에서 br1으로 작업후 R의 br1으로 push, 집에서 br1을 받아올때
git pull하게 되면 안됨. 마스터를 받아오기때문
git pull origin br1도 안됨. 집에서는 br1의 소유와 존재를 모르기때문
그래서
git checkout -t origin/<branch-name>해야 로컬에도 브랜치 생성후 pull
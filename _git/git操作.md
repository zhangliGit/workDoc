### git仓库

**git仓库分为工作区，暂存区和版本库（本地仓库）**
**使用git add命令把工作区代码提交到暂存区，然后通过git commit把代码提交到本地分支仓库**

### 设置git免登陆

```js
git config --list 查配置
git config user.name 'zhangliGit'
git config user.email '22@qq.com'

```

### 创建分支

```js
git branch [branchName] // 创建新分支 指向当前分支

git checkout -b [branchName] // 创建新分支并切换到创建的分支
```

### 拉去远程分支（本地没有）

```js
git fetch origin branchName:branchName
```

### 切换分支

```js
git checkout [branchName]
```

### 删除本地分支

```js
git branch -D [branchName]
```

### 删除远程分支

```js
git push origin --delete [branchName]
```

### 删除远程分支文件

```js
git rm fileName

git commit -m 'xx'

git push origin master
```

### 删除文件为提交时找回

```js

git reset HEAD fileName // 从暂存区撤销

git checkout -- fileName

```

### 查看分支

```js
git branch // 查看本地分支

git branch -r //查看远程分支

git branch -a //查看所有分支
```

### 提交代码到暂存区stage

```js
git add . // 提交工作区所有变化的代码

git add fileName  // 提交工作区制定的文件
```

### 从暂存区撤销提交的文件

```js
git reset HEAD // 撤销所有add的文件

git reset HEAD fileName //撤销指定add的文件
```

### 提交代码到本地仓库

**commit往往是有重大改变的版本改变或某一块功能开发完毕之后的提交**

```js
git commit -m 'xxx' //提价所有代码的说明

git commit -m 'xxx' fileName // 提交单独文件的说明
```

### 撤销最近的一次提交

```js
git revert HEAD

git revert HEAD~1 // 撤销上一次提交

git revert id // 撤销id这次的提交
```

### 合并分支

**合并dev分支到master分支**

```js
> git checkout master // 首先切换到master分支

> git merge dev // 然后合并dev分支到master
```

### 比较工作区和暂存区的区别

```js
git diff --cached //比较暂存区和本都仓库
```

### 查看分析所有提价的版本信息

```js
git reflog

git log
```

### 会退到某个历史版本（分支回滚）

```js
git reset --hard 版本号
```



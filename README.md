# GitHub Practice

透過這個Repository練習Git及GitHub

## 分支

- master: 主要分支
- develop: 開發分支
- release: 發布分支
- feature: 功能分支
- issue: 問題分支
- hotfix: 修補分支

> 視實際情況可刪減分支, 但master是主要分支, 所以不可以刪除

## GitHub Flow

https://guides.github.com/introduction/flow/

## Fork

將Repository複製至自己的GitHub帳號下，此機制為GitHub的權限控管，避免影響主要程式

## Pull Request

透過Pull Request(PR)送出請求，請求原作者將異動合併至原Repository

## Lab

實際操作

### Start

執行Script檔案, 確認可以執行

```bash
$ ./commit.sh
2021-03-16
Hello World!!!
```

### Create develop branch

```bash
$ git checkout master
$ git reset --hard origin/master
$ git checkout -b develop
```

### Commit

修改commit.sh檔案內容, 在檔案的最後寫上 **echo "Your Name"**, 將Your Name改成自己的名字

```bash
$ vi commit.sh
```

檔案內容修改完如下所示

```txt
#!/bin/bash
echo `date +"%Y-%m-%d"`
echo "Hello World!!!"
###
### Write down your name.
###
echo "Your Name"
```

改完之後, 可以執行快捷鍵Shift + Z, 再按一次Z

```bash
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   commit.sh

no changes added to commit (use "git add" and/or "git commit -a")

$ git diff
diff --git a/commit.sh b/commit.sh
index 5b4eda8..a5b181a 100644
--- a/commit.sh
+++ b/commit.sh
@@ -4,4 +4,4 @@ echo "Hello World!!!"
 ###
 ### Write down your name.
 ###
-
+echo "Your Name"

$ git add commit.sh
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   commit.sh

$ git diff --staged
diff --git a/commit.sh b/commit.sh
index 5b4eda8..a5b181a 100644
--- a/commit.sh
+++ b/commit.sh
@@ -4,4 +4,4 @@ echo "Hello World!!!"
 ###
 ### Write down your name.
 ###
-
+echo "Your Name"

$ git commit -m "輸出名字"
[master .......] 輸出名字
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### Push to Remote Repository

將分支推送至遠端版控伺服器

```bash
$ git remote -v
origin  https://github.com/githubusername/githubpractice.git (fetch)
origin  https://github.com/githubusername/githubpractice.git (push)
# 請置換GitHub Url
$ git remote set-url origin <GitHub Url>
$ git push origin develop
```

> 遠端Repository連結可使用HTTPS或SSH
> HTTPS: 每次存取遠端Repository都需要輸入帳號密碼, 也可以在HTTPS網址上加上帳號, 並用「@」隔開原本的網址
> SSH: 需要先上傳SSH Public key至遠端版控伺服器, 後續存取遠端Repository均不需要帳號密碼


### Test

```bash
$ ./commit.sh
2021-03-16
Hello World!!!
Your Name
```

### Merge branch

```bash
$ git checkout master
$ git reset --hard origin/master
$ git merge origin/develop
```

### Conflict

發生衝突時, 需要判斷為何發生衝突, 處理方式有兩種
1. 處理合併分支的Commit, 使其衝突不會在合併時發生
2. 手動解決衝突, 修改成最後版本

```bash
$ git checkout master
$ git reset --hard origin/master
$ git merge origin/conflict
Auto-merging commit.sh
CONFLICT (content): Merge conflict in commit.sh
Automatic merge failed; fix conflicts and then commit the result.
```
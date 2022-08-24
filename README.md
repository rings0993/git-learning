# git-learning 這只是用於熟悉git操作創建的Repository

# Git Local

## Git 初始化配置
- 全局有效的初始化配置
``` CMD
git config --global user.name "vay.liu"
git config --global email "ringsliu0993@gmail.com"
```

- 顯示當前配置
```CMD
git config -l
```

- 初始化本地Repositories，若有全局配置有差異則以**本地**為準
``` CMD
git init
```

- 查看目前git 目錄下的文件
``` CMD
git ls-files -s
```
返回值為: 文件權限，blob對象, 0, 文件名，如:
![[Pasted image 20220824110834.png]]

## Git Status

- 查看目前狀態，會返回的有目前**所在分枝**及**文件狀態**
``` CMD
git status
```


## Git Add 
* 使用Git add時，git 會創建一個目錄，並使用文件內容建立一個`blob`文件和**哈希值**，需要注意的是檔案名稱並**不會**影響Hash值的生成
``` CMD
git add filename.file
```

- 哈希值本身包含的資訊為object類型(`blob`)、檔案內容長度及檔案內容

- 查看物件(`objects`)的**類型**，可以只填物件的**目錄加上一部分的Hash值**
``` CMD
git cat-file -t 239f21

//expect output: blob
```

- 查看物件(`objects`)的**內容**，可以只填物件的**目錄加上一部分的Hash值**
``` CMD
git cat-file -p 239f21
```


## Git Commit
- 利用 `-m` 設定 `commit message`
``` CMD
git commit -m "1st commit"

[master (root-commit) 267acd5] 1st commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 hello.txt
```

- 每次 `commit` 都會創建一個 `commit objects` 其中會包含一個 `tree objects`、`author` (作者，時間，時區)、`commiter` 及 `commit message`

- `tree objects` 內包含的是權限、objects、對應的Hash值及文件名稱，若有資料夾結構，本身也會是一個`tree objects`


## Git 文件狀態

### Git Restore
- `git restore --stage`，將Staged的Bash指向切換回先前狀態
- `git retore`，將Modified內的文件狀態切換回先前狀態

## Git log
檢視Commit 的歷史，
-  `-2` 代表只顯示最近2次的`commit`
- `--after-"2020-05-21"` 為只顯示2020/05/21之後的提交(包含)，也可以使用 `--before`(不包含)
- `shortlog`則可以依照作者去顯示`commit`次數與每次的`commit message`
- `--stage`額外顯示的修改內容，包含文件的新增與刪除
```CMD
git log -2
git log --after-"2020-05-21"
git shortlog
git log --stage
```

## Git reflog
檢視Commit 的歷史log，包含**已經刪除**的分支
```CMD
git reflog
```

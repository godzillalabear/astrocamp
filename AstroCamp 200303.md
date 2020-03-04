# AstroCamp 200303


* 問公司
	1. 公司有沒有在做測試
	2. 有沒有在做版本控制

`#QA 如何寫測試檔？會教嗎？會可是太多惹，學不完，只能工作中邊做邊學`

git指令有一百多個，但常用的只有二十幾個，且使用情境跟指令搭不起來，兩成的指令足以應付八成工作
有些人把git當FTP使用，但FTP沒有在做**版本控制（Version Control）**
	FTP ：大公司提供空間讓使用者上傳檔案，有點像現在的雲端？？ `#Q`

git只能認出純文字檔之間的差別，ppt, 或其他設計類檔案為二進位檔，檔案內涵圖片等複雜的東西，文字型態的檔案git比較能夠分別

What can git do?
- 備份
- 歷史紀錄及證據（知道哪條程式碼是誰寫的）

### 分散式的版本控制
* 版本： 每存一次檔就有一個版本
* 控制：隨時可以前進後退通往任何版本，把自己控制在某一版本上
* 分散式：使用者們可以不透過中央伺服器就修改刪除或新增檔案，每個手上都有一份資料
`#QA 會不會每個人都不一樣？沒關係，等到上傳到中央伺服器後，git會辨認版本的不同並標籤無法辨認的部分，告知使用者`


### 版本控制工具們
* CVS
* SVN

	^^集中式管理，伺服器壞掉就不能使用
---
* git (同時支援本地及遠端操作)

### git的爸爸 — Linus Torvalds
* linux kernel creator
* 兇巴巴，講話大聲，不善言詞，愛比中指
* 10 天創造git 
* #HW 找Linus Torvalds 專訪
* git出生15年囉

### git 和 GitHub 不能混為一談
* GitHub 為使用git伺服器的網頁介面
* gitlab 是GitHub對手
* gitlab 和 GitHub 都適用ruby寫的
* isrubydead.com
* java的商業炒做

### GUI for git
* SourceTree
* GitHub Desktop
* …

用終端機指令建立觀念，用圖形化介面查看版本


### 1. 設定基本資料
`git config —list` 查看設定
```
git config —global user.name "Yushan Cheng”
git config -global user.email "b10432020@gapps.ntust.edu.tw”
```
```
user.name=Yushan Cheng
user.email=b10432020@gapps.ntust.edu.tw
```
遇到（END）卡住時，或看到一半（:），**可以按q跳出** 
#Q 什麼情況用q什麼情況用ctrl+D
終端機顯示`:`表示後面還有資料
不用帳號密碼就可以用任何email設定發布者資料，廠商二包三包的時候都這樣河河
### 2. 初始化 git  init
`$ pwd`顯示目前位置
`$ cd ` 後面直接拖曳目錄資料夾就能夠自動填入位址，還不會打錯
在/tmp裡面做事，用完就會不見，適合做測試
`$ mkdir` make directory 建立資料夾
```
$ git init // 初始化資料夾
Initialized empty Git repository in /Users/godzillalabear/Documents/Astro_Camp/git practice/demo/.git/
$ git init //做一次就好囉不用兩次
Reinitialized existing Git repository in /Users/godzillalabear/Documents/Astro_Camp/git practice/demo/.git/
```
```
//資料夾裡面新產生這些檔案
$ ls -al //顯示隱藏的檔案
total 0
drwxr-xr-x   3 godzillalabear  staff   96  3  3 11:48 .
drwxr-xr-x   4 godzillalabear  staff  128  3  3 11:48 ..
drwxr-xr-x  10 godzillalabear  staff  320  3  3 11:48 .git
```
.git之下的資料夾會做版本控制，之上的資料夾如果也坐版控，那可能會出問題
檔案狀態改變都會在.git底下被執行

不要在上層資料夾做版本控制，每個專案分開個別做
`#QA 做錯了要怎麼復原？ $ rm -rf .git 版本控制的東西就會不見了`
`$ rm -rf []` 刪東西用 []寫位址 **請小心使用** rm remove
### 3. 完成一次存檔
**Working Directory工作目錄**  
**Staging Area暫存區域** 
 **Repository 儲存庫**
![](AstroCamp%20200303/%E6%88%AA%E5%9C%96%202020-03-03%20%E4%B8%8B%E5%8D%885.46.44.png)

* git add git commit 完成一次存檔
`$ git status` //查看現在檔案的狀態
```
$ touch index.html
$ git status //查看現在檔案的狀態
On branch master

No commits yet

Untracked files: //尚未被追蹤的檔案
  (use “git add <file>…” to include in what will be committed)

	index.html //←

nothing added to commit but untracked files present (use "git add" to track)
```
要存到暫存區或儲存庫，才會是被追蹤的狀態

`$ git add index.html `//把index.html從工作目錄轉移到暫存區
```
$ git add index.html //把index.html從工作目錄轉移到暫存區
$ git status
On branch master

No commits yet

Changes to be committed:
  (use “git rm —cached <file>…” to unstage)

	new file:   index.html
```
`git add .`//. 代表這裡。 .. 代表上一層
`git add —all`// 這兩個指令都可以把資料夾中所有檔案加進來

`git commit -m “...”`把檔案從暫存區存到儲存庫
```
$ git commit -m “just for testing” //把檔案放進儲存庫時要貼個小標籤說明檔案用途
[master (root-commit) 68e75a2] just for testing
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 index.html
$ git commit -m “just for testing” //暫存區沒有東西就沒有東西可以移到倉庫
On branch master
nothing to commit, working tree clean
```
 -m後面的訊息像是工作記錄，方便回覆版本時知道是哪一個版本
commit的訊息很重要，不要亂寫 ，可以這樣寫 -> “#23 bug fixed”
#Q issue system [事務跟蹤管理系統 - 維基百科，自由的百科全書](https://zh.wikipedia.org/wiki/%E4%BA%8B%E5%8A%A1%E8%B7%9F%E8%B8%AA%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9F)
`git help commit` 可以查看commit指令的詳細用法

把檔案從工作目錄 → 暫存區 -> 儲存庫，這樣的流程就是完成一次存檔

### 4. 改變檔案權限
```
ls -al
total 0
drwxr-xr-x   5 godzillalabear  staff  160  3  3 12:16 .
drwxr-xr-x   4 godzillalabear  staff  128  3  3 12:16 ..
drwxr-xr-x  13 godzillalabear  staff  416  3  3 12:16 .git
-rw-r--r--@  1 godzillalabear  staff    0  3  3 12:15 data.txt
-rw-r--r--@  1 godzillalabear  staff    0  3  3 12:00 index.html
```
#QA d代表目錄 git是個資料夾 前面的點代表被隱藏了
r read 可讀取 w write 可寫入 x excution 可執行
drwxr-xr-x -> 表示檔案的權限

| d | rwx | r-x | r-x |
|---|---|---|---|
|     | user   | group      |   others    |
	
`chmod 700 index.html`可以改變檔案權限
```
$ ls -al
total 0
drwxr-xr-x   5 godzillalabear  staff  160  3  3 12:16 .
drwxr-xr-x   4 godzillalabear  staff  128  3  3 12:16 ..
drwxr-xr-x  13 godzillalabear  staff  416  3  3 12:16 .git
-rw-r—-r-—@  1 godzillalabear  staff    0  3  3 12:15 data.txt
-rwx———-——@  1 godzillalabear  staff    0  3  3 12:00 index.html //變成私人檔案
```

ugo: user group others
`$ chmod g+x index.html `//增加 group 執行的權限
```
$ chmod g+x index.html //增加 group 執行的權限
Godzillalabearde-MacBook-Pro:demo godzillalabear$ ls -al
total 0
drwxr-xr-x   5 godzillalabear  staff  160  3  3 12:16 .
drwxr-xr-x   4 godzillalabear  staff  128  3  3 12:16 ..
drwxr-xr-x  13 godzillalabear  staff  416  3  3 12:16 .git
-rw-r—-r-—@  1 godzillalabear  staff    0  3  3 12:15 data.txt
-rwx——x--—@  1 godzillalabear  staff    0  3  3 12:00 index.html
```

`#QA staff ??wheel?? 代表使用者所在的組別，可以自己命名但是有慣例，wheel 通常表示有最高權限的使用組別`



為什麼要兩段式？就像計算機組織裡面會把暫存區跟儲存區分開，兩段式可以對存檔做更精細的控制
什麼時候需要Commit? 隨時都可以，你認為你需要存檔，就commit

`$ git log `//顯示工作記錄
```
$ git log //顯示工作記錄
commit e2ccdde3f946f03a3ed38b849f14a1e361794859 (HEAD -> master)
Author: Yushan Cheng <b10432020@gapps.ntust.edu.tw>
Date:   Tue Mar 3 12:16:30 2020 +0800

    just for testing

commit 68e75a2eb4aea1fa0b583ffd32c1ee15680b63d7
Author: Yushan Cheng <b10432020@gapps.ntust.edu.tw>
Date:   Tue Mar 3 12:09:09 2020 +0800

    just for testing

```
```
#QA  (HEAD -> master)
	master為內建的一個分支
	HEAD是指標，代表現在進度在哪裡（當前指標）
	(HEAD -> master) 現在正在這個分支上，代表現在進度在哪裡
```

### 5. 刪除檔案
`$ git status`可以查看現在版本的狀態，哪些被刪掉了哪些沒有
如果有修改過專案卻還沒commit，git status會提醒你可以怎麼做
```
$ rm data.txt //刪除檔案
Godzillalabearde-MacBook-Pro:demo godzillalabear$ git status
On branch master
Changes not staged for commit:
  (use “git add/rm <file>…” to update what will be committed)
	//確認刪除檔案
  (use “git checkout — <file>...” to discard changes in working directory)
	//取消刪除檔案（穢土轉生）

	deleted:    data.txt
	modified:   index.html

no changes added to commit (use “git add” and/or “git commit -a”)

```

### 6. 怪別人的時候
`stree .` 開啟圖形化介面
`git blame index.html` //看得出每一行什麼時候由誰完成的
```
r$ git blame index.html
abb4f438 (Eddie Kao 2017-08-02 16:49:49 +0800  1) <!DOCTYPE html>
abb4f438 (Eddie Kao 2017-08-02 16:49:49 +0800  2) <html>
abb4f438 (Eddie Kao 2017-08-02 16:49:49 +0800  3)   <head>
abb4f438 (Eddie Kao 2017-08-02 16:49:49 +0800  4)     <meta charset=“utf-8”>
abb4f438 (Eddie Kao 2017-08-02 16:49:49 +0800  5)     <title>首頁</title>
abb4f438 (Eddie Kao 2017-08-02 16:49:49 +0800  6)   </head>
abb4f438 (Eddie Kao 2017-08-02 16:49:49 +0800  7)   <body>
657fce78 (Eddie Kao 2017-08-02 16:53:43 +0800  8)     <div class="container">
657fce78 (Eddie Kao 2017-08-02 16:53:43 +0800  9)     </div>
abb4f438 (Eddie Kao 2017-08-02 16:49:49 +0800 10)   </body>
abb4f438 (Eddie Kao 2017-08-02 16:49:49 +0800 11) </html>
```
`$ git log -p index.html `\\檢視單一檔案的紀錄
```
$ git log -p index.html \\檢視單一檔案的紀錄
commit 657fce783a23e26721ec4f778b9e0e108253e92d
Author: Eddie Kao <eddie@5xruby.tw>
Date:   Wed Aug 2 16:53:43 2017 +0800

    add container

diff —git a/index.html b/index.html
index d1146e2..e90bdb3 100644
— a/index.html
+++ b/index.html
@@ -5,5 +5,7 @@
     <title>首頁</title>
   </head>
   <body>
+    <div class=“container”>
+    </div>
   </body>
 </html>

commit abb4f43814af7bcf47afa9b779aaba63599e562b
Author: Eddie Kao <eddie@5xruby.tw>
Date:   Wed Aug 2 16:49:49 2017 +0800

    update index page

diff —git a/index.html b/index.html
index e69de29..d1146e2 100644
— a/index.html
+++ b/index.html
@@ -0,0 +1,9 @@
+<!DOCTYPE html>
+<html>
+  <head>
+    <meta charset=“utf-8”>
+    <title>首頁</title>
+  </head>
+  <body>
+  </body>
+</html>

commit cef6e4017eb1a16a7bb3434f12d9008ff83a821a
Author: Eddie Kao <eddie@5xruby.tw>
Date:   Wed Aug 2 03:02:37 2017 +0800

    create index page

diff —git a/index.html b/index.html
new file mode 100644
index 0000000..e69de29

```

### 7. 分支 branch
* 什麼時候要用分支？怕做錯、做測試、我開心用就用
* 一開始有一個master分支
#QA 做完什麼事的時候要分支？
	當我們已經完成一個可以使用的網站，想要發展新功能時，我們會用分支分出去做新功能，等到新功能經過測試確認沒問題之後，才會合併會Master。Master通常表示沒有出錯的檔案
* 分支像個貼紙般的存在，commit本身才是重點，分支（貼紙）不是
* `$ git branch cat` 建立名叫cat的分支，不可新增已經存在的同名分支
 可以在同一個版本上貼好多張貼紙
貼紙檔案大小只有40bytes
```
$ git branch //顯示現有分支
  cat
* master //＊號代表現在HEAD所在
```
#HW 畫步驟圖
```
$ git checkout cat //把主控權交給cat
Switched to branch ‘cat’
$ git branch
* cat
  master
```

`git checkout` can switch branch or restore

#HW what is VIM
how to exit VIM

```
$ git add .
$ git commit -m “add branch cat 1”
On branch cat
nothing to commit, working tree clean
$ touch cat1.html
$ git add .
$ git commit -m “add branch cat 1”
[cat f4530a6] add branch cat 1
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 cat1.html
$ touch cat2.html
$ git add .
$ git commit -m “add branch cat 2”
[cat 0ec96fb] add branch cat 2
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 cat2.html

```
#HW graph
### 8. 
* 版本**控制**
```
$ ls -al
total 16
drwxr-xr-x   9 godzillalabear  staff  288  3  3 15:09 .
drwxr-xr-x@ 10 godzillalabear  staff  320  3  3 15:09 ..
drwxr-xr-x  18 godzillalabear  staff  576  3  3 15:09 .git
-rw-r—r—@  1 godzillalabear  staff    0  3  3 15:08 cat1.html
-rw-r—r—@  1 godzillalabear  staff    0  3  3 15:09 cat2.html
drwxr-xr-x   3 godzillalabear  staff   96  3  3 14:04 config
-rw-r—r—@  1 godzillalabear  staff    0  8 20  2017 hello.html
-rw-r—r—@  1 godzillalabear  staff  161  8 20  2017 index.html
-rw-r—r—@  1 godzillalabear  staff   11  8 20  2017 welcome.html
$  git checkout master
Switched to branch ‘master’
$ ls -al
total 16
drwxr-xr-x   7 godzillalabear  staff  224  3  3 15:19 .
drwxr-xr-x@ 10 godzillalabear  staff  320  3  3 15:19 ..
drwxr-xr-x  18 godzillalabear  staff  576  3  3 15:19 .git
drwxr-xr-x   3 godzillalabear  staff   96  3  3 14:04 config
-rw-r—r—@  1 godzillalabear  staff    0  8 20  2017 hello.html
-rw-r—r—@  1 godzillalabear  staff  161  8 20  2017 index.html
-rw-r—r—@  1 godzillalabear  staff   11  8 20  2017 welcome.html
$ git checkout cat
Switched to branch ‘cat’
$ ls -al
total 16
drwxr-xr-x   9 godzillalabear  staff  288  3  3 15:19 .
drwxr-xr-x@ 10 godzillalabear  staff  320  3  3 15:19 ..
drwxr-xr-x  18 godzillalabear  staff  576  3  3 15:19 .git
-rw-r—r—   1 godzillalabear  staff    0  3  3 15:19 cat1.html
-rw-r—r—   1 godzillalabear  staff    0  3  3 15:19 cat2.html
drwxr-xr-x   3 godzillalabear  staff   96  3  3 14:04 config
-rw-r--r--@  1 godzillalabear  staff    0  8 20  2017 hello.html
-rw-r--r--@  1 godzillalabear  staff  161  8 20  2017 index.html
-rw-r—r—@  1 godzillalabear  staff   11  8 20  2017 welcome.html
```

### 9. 分支合併
分身任務成功後，本體要收割成果
```
$ git merge cat  
	//merge 後面的是受詞，head 所帶領的分支是主詞
Updating e12d8ef..0ec96fb
Fast-forward //把貼紙往前快進
 cat1.html | 0
 cat2.html | 0
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 cat1.html
 create mode 100644 cat2.html
```
單線進行預設會快轉合併
#QA 那後退叫什麼呢？ reset
#HW 	交換貼紙 git merge -m...

#QA 工作目錄的檔案也會被commit嗎？不會 要先add才行

* no fast forward
`git merge cat —-no-ff`
就可以看出分岔了！！ 但沒必要

* 合併貓狗（Y型分支）
```
$ git checkout cat
Switched to branch ‘cat’
$ git merge dog -m “merge”
Merge made by the ‘recursive’ strategy.
 dog1.html | 0
 dog2.html | 0
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 dog1.html
 create mode 100644 dog2.html

```
![](AstroCamp%20200303/%E6%88%AA%E5%9C%96%202020-03-03%20%E4%B8%8B%E5%8D%883.55.50.png)
#HW 試做貓狗兩分支
`$ git branch -d cat`//刪除分支

### 10. 合併衝突
如果兩個分支同時改同一個檔案怎麼辦？
	git會幫你標記，合併失敗
```
$ git merge member
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html //合併失敗
Automatic merge failed; fix conflicts and then commit the result.

$ git status
On branch payment
You have unmerged paths.
  (fix conflicts and run “git commit”)
  (use “git merge —abort” to abort the merge)

Changes to be committed:

	new file:   member.html

Unmerged paths:
  (use “git add <file>…” to mark resolution)

	both modified:   index.html //兩個分支都修改了同個檔案
```
![](AstroCamp%20200303/%E6%88%AA%E5%9C%96%202020-03-03%20%E4%B8%8B%E5%8D%884.21.56.png)
git 會在index.html 檔案中用箭頭幫你標記出來，剩下就是人要處理的事
了
- - - -
### 11. rebase 
rebase 複製一份貼到新地方（剪接歷史）
看不出來誰先誰後
#HW rebase 的terminal歷程
末端枝節沒有人看管就會隱形

#QA 什麼時候該使用Y型合併，什麼時候該使用rebase？
* merge vs. rebase
rebase 看不出來誰先誰後
merge 想要保留歷史紀錄時使用

把head倒退時雖然會看不到commit紀錄，但檔案都會留著

### 12. 如何回復上一步
reset 在這裡表示become’變成’
checkout vs reset
	checkout 會移動HEAD
	reset 會移動 Master
	根據ppt的狀況，末端節點只要有人看管就不會消失，但當前指標指向C3，就只會看到C3以前發生的事

設c3, c4, c5為commit 節點
`$ git reset C3 --mixed` //把c4, c5新增的檔案放到工作目錄//預設值
`$ git reset C3 --soft`//把c4, c5新增的檔案放到暫存區
`$ git reset C3 --hard`//把c4, c5新增的檔案殺死
但commit 節點的名字臭臭長很難記，所以我們要幫他取代名詞（分支指標）(HEAD, cat, dog)
所以分支也可以用來做標籤貼紙用
也可以用＾代表倒退幾步
`$ git reset HEAD^ --mixed` 倒退一步
`$ git reset HEAD~5 --mixed` 倒退五步
^和～7都可以表示指標的相對位置，^為前一個，^^為前兩個，~加數字代表前幾個

> 在git的世界，沒有刪除commit這件事  

#QA rm /reset /資料夾的變化 /commit的變化






- - - -
HW
#HW 下課全部再做一次
#HW 看不見分支還是能貼的回去
- - - -
Reference:
1. https://www.tiobe.com/tiobe-index/
2. [常用命令指令](https://railsbook.tw/chapters/03-command-line-tools.html)
3. [事務跟蹤管理系統 - 維基百科，自由的百科全書](https://zh.wikipedia.org/wiki/%E4%BA%8B%E5%8A%A1%E8%B7%9F%E8%B8%AA%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9F)



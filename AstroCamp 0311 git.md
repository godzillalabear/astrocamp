# 0311 直播 git的世界觀

> 寶藏都藏在.git目錄

### 0. git中有4種物件
	* 檔案 blob
	* 目錄 tree
	* commit
	* tag		
### 1. git add index.html
不完全是改變檔案狀態
他會把index.html的內容物計算並壓縮後以blob的物件放到.git的資料夾
```
//git的計算方式
input =  “blob #{content.length}\0#{content}”

puts Digest::SHA1.hexdigest(input)		//SHA1是一個雜湊演算法
```
```
//我們可以這樣查看出計算內容
cat index.html		//在終端機顯示檔案內容
cat index.html | git hash-object —stdin				//計算出上面SHA1的結果
```


> git 不在乎檔案名稱，他只在乎檔案內容  

```
open .git			//開啟.git資料夾
```
![](https://i.imgur.com/XIM4Tii.png)

object資料夾會存每次commit的commit, blob與tree
![](https://i.imgur.com/MYkttsL.png)

前面兩個數字是資料夾名字，後面一長串是檔案名字
存在.git之中的objects資料夾
所以`git add index.html`，會增加一個34的資料夾裡面有名為d3d9....的blob（檔案）

git用檔案的內容物去運用，所以只建立一個空的資料夾，git沒辦法感受
沒有辦法git add 一個資料夾，資料夾裡面必須要有東西，即便是空的檔案

==#Q e6 與34以十六進位的數字？還是文字？==
看起來像是16進位的數字

### 2. git commit 進行第一次commit
![](https://i.imgur.com/ZKRjB7E.png)

會多一個bb的目錄

```
git cat-file bb7e082 -t	//查看物件型態
git cat-file bb7e082 -p	//查看物件內容
```

![](https://i.imgur.com/Bq57fu1.png)

這個commit物件bb7e底下會生出一個tree叫做eb12
tree 目錄
![](https://i.imgur.com/LQNGR3g.png)




```
//看看eb12的tree又有什麼呢？
git cat-file eb12 -p		
```
![](https://i.imgur.com/bV2jKjk.png)

eb12這個tree(目錄)指向 a618的tree以及34d3的blob

==#QA 為什麼檔案名字只打前面4個字呢？==\
只打一個字git沒辦法辨認
如果剛剛好有前4個字一樣的檔案，git會通知你，讓你選擇
![](https://i.imgur.com/JZTjbMV.png)


再去追a618這個tree
應該是代表config tree(目錄）

![](https://i.imgur.com/3Pws4mc.png)

這個樹狀結構是我們想像出來的，在git的世界是攤平的資料夾們，資料夾之間會一個一個指向彼此，所以我們可以想想資料夾之間的結構

### 3. 修改index內容之後...，git要如何知道呢？

git會把新的內容跟34d3裡面的內容去比較

![](https://i.imgur.com/cuXYHjy.png)

只要修改內容後，會計算出截然不同的結果

### 4. 進行第二次commit之後
![](https://i.imgur.com/hARiIWj.png)


d4a4為這次commit的名字
![](https://i.imgur.com/5mjJmHf.png)


這個commit比上一個多了一個parent 叫做bb7e，剛好就是我們上次的那一個commit
每一個commit都會指向上一個commit

看看tree 0261
![](https://i.imgur.com/HNtB9kc.png)

指向了我們修改過的0a68的檔案，以及原來儲存的資料夾a618
由於檔案只有修改過而沒有移動位置，所以這個tree指向的之前的資料夾位置

### 5. 創造一個新檔案 README.md 空的檔案
![](https://i.imgur.com/eRfUHoY.png)

原來就有一個空檔案叫做database.yml
新的空檔案即便檔名不同，他還是會計算出一樣的內容
如同第一次commit的空檔案database.yml
這樣add之後，他會修改之前的e69d檔案，而不會新增新的物件
e69e除了代表database.yml外，也代表 README
![](https://i.imgur.com/i9TgpnY.png)



### 6. 第三次commit後
![](https://i.imgur.com/segDJI1.png)

這個commit名叫ee39
他之中有一個tree叫做948c
一個parent d4a4 -> 就是第二次的commit

看看948c的tree有什麼？
![](https://i.imgur.com/AALgEa2.png)

這個tree中指向2個blob
其一是沒有修改的前一個版本的index.html -> 0a68
另一個是新增的readme檔案
最後指向了原來的目錄tree
![](https://i.imgur.com/QtdPaqA.png)


每次新增檔案（add），git會生出一個一個的檔案blob，每次commit後，git會生出commit檔案以及一些tree去指向檔案

![](https://i.imgur.com/GPYEZs3.png)



![](https://i.imgur.com/GTIQyzI.png)


這種圖形叫做
DAG = Directed Arrow Graph 有向無環圖

### 7. 在做分支切換到底會發生什麼事？
就好像在換整串葡萄
我們在git圖形化介面通常都只看得到粉紅色的commit節點，就像葡萄梗，而下面看不到的東西是葡萄們，每次在做分支切換，就像在換一串葡萄
![](https://i.imgur.com/6IhpVmu.png)



![](https://i.imgur.com/5jN0RtA.png)


每次commit都像一串葡萄，head一動就像抽出其中一串放到桌上一樣

git不是在做差異備份，而是工作記錄，你需要哪一份紀錄，他就會把其中一份抽出來給你


### 8. 和其他版控軟體做比較

![](https://i.imgur.com/KAcBVwX.png)


他牌版控軟體大多都只做差異備份，但git會把整個檔案做備份，雖然我們只修改一個字，但他會做成一個blob物件給我們
耗空間，效率速度好
git的爸爸認為效率大於一切，雖然浪費空間，但硬碟會隨著時間變便宜，時間卻會隨著時間變貴



```
//補充的終端機指令
ls -al | grep “apple”	//在檔案中只列出有apple的檔案
		        // ｜ 叫做pipe 把前面的結果丟到下一個程式去接管
```

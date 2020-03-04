# AstroCamp 2000304 Ruby for Rails
#AstroCamp


### Ruby is an interesting programming language
	* ruby 效能雖然不算好，但容易理解，寫得開心卻改不動
	* 黑魔法 -> 用就對了
	* 要想辦法維持自己的成就感
	* 都市傳說（很慢、要用mac）
### Ruby 特產 
	* 雙重定義  `x, y = y, x`
	* 允許修改常數（跟物件導向有關）
	* 只有nil 和false是假的，其他（-1, 0）都是真的
	* evil twins 邪惡分身
	* 用 `0..3` 取代`x >= 0 && x <= 3`
	* 方法中的小括號可以被“適當的”省略 `say_hello_to '孫悟空'`

### What is Ruby?
1. 泛用型程式語言，不限定用來開發網站
2. 腳本式程式語言
	* 程式語言可以用要不要編譯區分，不需編譯的程式語言叫做腳本式程式語言
	* 編譯會做最佳化
	* 效能比較慢，但開發流程較快
3. 物件導向程式語言，理論上在Ruby的世界所有東西都是物件
4. Rails是Ruby之中的一個套件
5. CRuby, JRuby, mRuby(for embedded system)

### What is Gem?
套件管理工具
```
$ gem install takami
$ gem uninstall takami
```
[RubyGems.org | Ruby 社群 Gem 套件管理平台](https://rubygems.org/?locale=zh-TW)
↑ 所有套件都在裡面
上架後的套件就不能下架了

### Hello

1. `$ ruby -e “puts ‘hello’”` 
2. 使用irb (interactive ruby)
3. 寫在某檔案裡
```
$ touch hello.rb //在hello.rb 中寫上程式碼
$ ruby hello.rb // hello.rb 可以不經編譯直接在終端機上執行
hi
hi
hi

```

副檔名不是重點，重點是檔案裡面的內容以及你用什麼工具解碼
```
$ cp hello.rb hello.php
$ ruby hello.php
hi
hi
hi

```

### REPL Read-Eval-Print-Loop
Read | Eval | Print | Loop
—|—|—|—
讀取 | 評估 | 印出 | 無窮迴圈

	* irb為一種 REPL的環境

### Comment
```
# this is a greeting message
puts “hi”
puts “hi”
puts “hi”

```
debug 要好好用
```
=begin
multiple line comment
not useful
=end
```

### Coding Style
	* 就像口音

	* 使用tab而非4個空格
	* snake_case 
	* ` puts 1 + 2`
	* 實務上少用puts在方法內作為回傳值，因為沒有回傳值

### 變數 Variable 
* 變數：幫某塊記憶體取名這樣才方便一直存取
* 變數使用前要先定義喔，但不用先宣告，也不用決定型態


種類 | 區域變數 | 全域變數 | 實體變數 | 類別變數
—|—|—|—|—
命名樣式 | username | $username |  @username | @@username
 | | 少用，易出錯| | | 

```
a = a + 1
a += 2 // a = a + 2
``` 
=代表指定

```
c = c || 10	#如果c有內容我就給你c，如果沒有就給你10
				#有點像預設值的概念
puts c	#output 10
c ||= 20
puts c	#output 10
```

* 變數的命名慣例
	* snake_case ✔︎
	* camelCase
	* 要取清楚有意義的命名

交換變數
```
temp = x
x = y
y = temp
```
```
#ruby 作弊法
x, y = y, x
```

how to switch two variables without a third one
	the general form is:
```
# A = A operation B
# B = A inverse-operation B
# A = A inverse-operation B 

x = x + y
y = x - y
x = x - y
```

### 常數 Constant
* 大寫字母開頭的就是常數 `BOOK = “username”` , `User = "Godzi”`
* 只定義過一次之後就再也不改
* 金鑰，系統密碼
* ruby 允許修改常數

常數vs變數？？ruby中的常數可以改變，所以在本質上來說ruby的常數與變數只有命名的差別而已

### 關鍵字與保留字 keyword and reserved word

#### 字串 String
`name = ‘godzi’`
`nickname = “lalabear”`
* 字串串接
```
name = “godzi”
age = 23
puts “hi, I am #{name}, and I am #{age} years old”
	#雙引號可以翻譯#{ }
puts ‘hi, I am #{name}’
	#單引號無法做字串串接/翻譯變數，但效率較快
```
* 引號被亂用？？
`puts’ hi, I\’m aaa’`
`\`代表跳脫，escape
`puts “he said, /“hi/””`
`puts %Q(hi, I am #{})` %Q -> 雙引號
`puts %q(hi, I am #{})` %q -> 單引號（不翻譯變數）

### 邏輯判斷與流程控制
* if -> 非黑即白 （布林型態 boolean 1/0）
* == 比較是否相同
* 在ruby只有兩個東西是假的 ->  false, nil = false
0, -1, [], {} -> 在ruby 之中也是真的

`nil  #不存在的存在`
```
tr = 1
tru = 1
true = 1 #true在ruby生成的時候已經被定義了，是保留字，為內建且不能改的變數 #true = true != 其他任何東西
```

* 等號 
```
a = 10
b = “10”

puts a == b		#印出 false
puts a === b		#印出 false
puts a = b		#印出 b
```


* puts print p
```
> puts “aaa”		#沒有回傳值， 有換行
aaa
 => nil 

> print “aaa”		#沒有回傳值，沒有換行
aaa => nil 

> p “aaa”			#有回傳值，有換行，還可以看出結構
“aaa”
 => “aaa” 
```
```
> 1 + 2
 => 3 		#這個3是irb幫忙印出來的 （回傳值）
> puts 1 + 2
3				#這個3是puts幫忙印出來的
 => nil 		#這個nil是irb幫忙印出來的 （回傳值）
> p 1 + 2
3				#這個3是p幫忙印出來的
 => 3 		#這個3是irb幫忙印出來的 （回傳值）

```

在ruby中每個輸字都是物件
`1 + 2` 實際上在程式中是 `1. +(2)`，把 `物件2` 呼叫 `+()` 這個方法和 `物件1` 結合

* evil twins 邪惡分身
if not == unless
if == unless not
unless 也有倒裝
`puts”hi” unless weather ==‘rain’`


* if else

* 三元運算子
只有二分的時候可以用
```
age = 19

if age >= 18
	status = “已成年”
else
	status = “未成年”
end
```
`status = (age> = 18)? ”已成年”：“未成年”` 

但有兩個條件時，也是可以啦，但很醜很醜很醜
```
age = 19
gender = 1

if age >= 18
	if gender == 1
		puts “male adult”
	else
		puts “female adult”
else
	puts “teenager”

result = (age >= 18)?(gender == 1) "male adult”:”female adult”:”teenager”
```

* if elsif else
```
weather = “rain”

if weather == “rain”
	puts “stay at home”
elsif weather == “sunny”
	puts “play out!”
else
	puts “sleep”
end
```

* case when
```
weather = “rain”

case weather
when “rain”
	puts “stay at home”
when “sunny”
	puts “play out!”
else
	puts “sleep”
end
```
the super power of case when
```
age = 10

case age
when 0..3
	puts “fetal”
when 4..10
	puts “child”
when 11..17
	puts “teenager”
else
	puts “adult”
end
```

NULL vs. nil
黑洞 vs. 存在
### begin rescue 例外處理
#QA rescue 後面要加方法?
rescue 後面會放這個方法的回傳值
```
def wrong 
	puts "you enter a wrong number"
end

def bmi_calculator(height, weight)
	begin
		weight / (height * height)
	rescue									#防呆機制
		wrong
	end
end

p bmi_calculator(0, 80)
```

### method 方法
* 賦予一段程式碼意義，讓人知道它的功能
* 讓人可以方便使用且重複使用一段程式碼
* 實務上少用puts在方法內作為回傳值，因為沒有回傳值
```
def greeting
	puts “hi”
	puts “hello”
	puts “:)”
end

greeting()
```
* 定義方法
```
def method_name(param1, param2)		#定義的時候叫參數
#…
end

method_name(argu1, argu2)			#要用的時候是引數
```
參數與引數 parameter and argument
* 方法中的小括號可以被“適當的”省略 `say_hello_to '孫悟空'`
* 回傳值
在ruby的方法中，預設最後一行的執行結果就是他的回傳值
回傳 -> 交回控制權
```
age = 18

def age 
	return 20
end

puts age			#ruby會’變數優先’而非方法
puts age()		#印出方法
```
```
def age 			#空方法
end				
					#回傳值為nil
```
```
def calc_perimeter(radius)
	return 2 * Math::PI *radius
end

puts calc_perimeter(5)
```
前三行先定義方法，第五行呼叫方法，就會暫時把控制權交給上面的方法，等方法執行完控制權才會回來第五行

```
def f2c(f)
	(f-32)*5.0/9		#只要除數被除數任一個是小數結果就為小數
end

puts f2c(140)
puts f2c (130)
```		


`ruby -w xx.rb` -w 會印出所有可能的warning message 


- - - -
Reference
1.  [Ruby Wizardry - X-Files](https://doc.lagout.org/programmation/Ruby/Ruby%20Wizardry_%20An%20Introduction%20to%20Programming%20for%20Kids%20%5BWeinstein%202014-12-18%5D.pdf) //full e book
2. [RubyGems.org | Ruby 社群 Gem 套件管理平台](https://rubygems.org/?locale=zh-TW)
3. [How one developer just broke Node, Babel and thousands of projects in 11 lines of JavaScript • The Register](https://www.theregister.co.uk/2016/03/23/npm_left_pad_chaos/)
4. [他一怒之下刪除11行程式碼 互聯網遭殃 - The News Lens 關鍵評論網](https://www.thenewslens.com/article/39189)
5. [c++ - Swapping two variable value without using third variable - Stack Overflow](https://stackoverflow.com/questions/1826159/swapping-two-variable-value-without-using-third-variable)
6. [B.C. & Lowy: 為什麼不能除以0？印度教授用白話文解釋給你聽](http://forgetfulbc.blogspot.com/2018/05/division.html)
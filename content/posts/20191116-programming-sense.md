+++
title = "Programming Sense (1)"
date = "2019-11-16T08:53:13+08:00"
url = "/posts/20191116-programming-sense"
description = ""
image = "https://images.unsplash.com/photo-1539392156992-268f1e62f111?ixlib=rb-1.2.1&auto=format&fit=crop&w=2689&q=80"
credit = "https://unsplash.com/photos/hHdKh1Gr9gY"
thumbnail = ""
comments = true
categories = ["程式設計"]
tags = ["programming sense", "小技巧", "coding style", "c", "可讀性"]
toc = true
draft = false
+++
<!-- https://drive.google.com/uc?export=view&id= -->
主要是我自己編寫邊學慢慢累積的，說真的也找不太到相關的資源，要搜尋也不知道下什麼關鍵字，問別人其實也很難在一時半刻裡解釋清楚，所以就拿來發一篇吧 OuO

<!--more-->

# 前言

期中加資格考的爆炸禮拜終於結束，其實比我想得還要容易，雖然我都很沒把握，因為我幾乎不狂寫考古題，而是以觀念取勝，有沒有取到就不確定了。

寫程式很簡單，拿來解決問題就有些難度，最難的是用優雅易懂且嚴謹的程式碼來解決問題，寫得好絕對遠遠好過寫得快。

關於這個主題，其實很早就打算寫了，只是一直擱置連架構都沒出來，直到最近有幫同學看一下程式碼，所以覺得這個觀念還是頗為重要，所以整理一下發個文，主要也希望可以幫助比較沒經驗的人，但也不限於此，我相信也會有畢業於資訊工程相關科系而沒有這些觀念。


當然在整個程式界我也不是老手，幾乎沒在開源貢獻，更沒參與過業界，所以很多的概念是我在大學時期慢慢累積起來的，主要來源就是一些開源的專案還有自身的經驗，不能說涵蓋得很全面，也不是說我這套最棒了大家看了之後一定要照這些規則，這篇從來就不是規則，而是我在寫了幾年程式後整理出來讓自己開發更為流暢的一些想法，希望大家能夠來互相討論給與意見。


架構會以不同的主題當作探討，雖然全部都是在講 programming sense，內容因為相當廣泛，切成不同文章又會讓某些部分零碎化，所以請善用標題跟右方的目錄來幫助閱讀。順序以 "工具"，"coding style"，"習慣養成"，"抽像化"，"寫程式的過程"，"除錯"。並主要以 C 語言當作講解範例。

雖然雜但是請記得一個中心思想：

> 用程式碼來溝通 (Communication Through Code)

# 工具

「工欲善其事，必先利其器」《論語·衛靈公》 善用工具真的頗為重要，使用得當可以大量減少重複性的動作，如果是寫一般的小程式的話我會建議可以玩看看 [VIM](https://en.wikipedia.org/wiki/Vim_(text_editor)) 設定可以參考[我的設定](https://github.com/aben20807/aben20807.vim)或直接問我，可以大量減少手部的負擔。大型一點的我會推薦 [VSCode](https://code.visualstudio.com/)，因為內容會偏多所以我就用一個副標題來說明了。

![google-vi... ](https://drive.google.com/open?id=1kYWGLrrnkeQaVo2OwbMZQddDu6iIn-do) [^7]

## VSCode

VSCode 其實不太像一般的 IDE，它更像一個單純的文字編輯器，只是有相當多好用的外掛功能，基本的包含了對各種語言的程式碼的關鍵字 highlight、檔案架構樹、搜尋取代功能、編碼轉換、coding style 自動重新排版。以下附上一些我目前服役中的外掛功能，使用方法就請各位自己前往查看了：

+ `alefragnani.bookmarks` [🔗](https://marketplace.visualstudio.com/items?itemName=alefragnani.Bookmarks)： 可以在想要標記的程式碼上加入書籤，這個在瀏覽大型專案需要跳來跳去 trace 程式碼下可以幫很大的忙，至少不用再記是第幾行了。
+ `coenraads.bracket-pair-colorizer` [🔗](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer)：連結對應的括號，這在括號一堆的語言 (C, C++, Java, Lisp) 相當有幫助，可以一眼就看出在哪個有效範圍 (scope)。
+ `streetsidesoftware.code-spell-checker` [🔗](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)：幫忙檢查英文拼字。
+ `tabnine.tabnine-vscode` [🔗](https://marketplace.visualstudio.com/items?itemName=TabNine.tabnine-vscode)：程式碼補全建議。
+ `gruntfuggly.todo-tree` [🔗](https://marketplace.visualstudio.com/items?itemName=Gruntfuggly.todo-tree)：收集註解中有 `TODO` 標籤的地方。
+ `donjayamanne.githistory` [🔗](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory)：Git 系列。
+ `eamodio.gitlens` [🔗](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)：Git 系列。
+ `zhuangtongfa.material-theme` [🔗](https://marketplace.visualstudio.com/items?itemName=zhuangtongfa.Material-theme)：耐看主題。
+ `vscode-icons-team.vscode-icons` [🔗](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons)：美美的檔案圖示。

![google-名稱拿去搜尋即可](https://drive.google.com/open?id=1YrpZ2ktFpMxR3Y7MZM0zBrt4DtRFNmga)

## Shell

很多指令都是可以幫助懶惰的人，目前我還沒有遇過我想要但是沒有的指令。

### 重新導向 (Redirection)

寫程式時會常使用重新導向 (Redirection) 的方式來減少標準輸入 (stdin) 的次數，用法也相當直觀，只需要先將測試輸入先打在一份文檔 (例如：input.txt) 中，再使用以下指令執行程式即可。

```bash
$ ./queue < input.txt
```

若要把標準輸出 (stdout) 存到另一份文件時呢，當然也是使用重新導向。這適合在輸出很多時或是需要搜尋結果時使用。

```bash
$ ./queue < input.txt > output.txt
```

# Coding Style

這是一個看似微小卻非常重要的細節，尤其是需要別人幫忙 review 甚至是合作時都需要事先講好共用的 coding style，一來格式統一閱讀時不需要轉換，二來可以避免因為工具自動調整造成不必要的程式改動紀錄。

看別人的程式碼時最怕遇到沒有縮排的...

這裡涵蓋的範圍包括了縮排、空格、括號、命名。

![google-pythonize ... 別亂學 XDD](https://drive.google.com/open?id=1srj3r8VaQ4_csG69Lr3vQD_ENvjEXmJH) [^8]

## Google Coding Style

若要偷懶，強烈建議就直接用最多人使用的就好，很多工具都有辦法幫忙重新排版程式碼，這裡展示如何用 VSCode 來設定 Google 使用的 coding style，規定的格式細節可參考 [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)。

![google-開啟設定](https://drive.google.com/open?id=1lCoOvNF61c1WaNoZ2MhO9QioANQS3HUS)
![google-搜尋 format style，將欄位改成 Google](https://drive.google.com/open?id=1RCaxBhfaLrVM84FoD3ekeu4AmtBhnxLJ)
![google-使用格式化可以用右鍵或是直接按對應的快捷鍵](https://drive.google.com/open?id=1rALSINyYBW1JuCiWsj1IVSLhiI_-_rXd)

# 習慣養成

> 傻瓜都可以寫出機器能讀懂的代碼，但只有專業程序員才能寫出人能讀懂的代碼。  
> --- 系統程序員成長計劃

## Coding Style Again

用工具是很方便沒錯，不過盡量還是養成習慣而不依賴工具，這裡介紹幾個比較常見的格式：

### 空行 (Blank)

把所有操作寫在同一個函式裡面通常不容易辦到，因此不免會有某些區塊在做相關的事，合理使用空行能夠讓讀者很容易就看出程式碼的這些區塊的用途。

### 縮排 (Indent)

我以前偏好 4 個空格，但是最近有往兩個空格移動的趨勢，另外 Google 也是以 2 個空格為主。然而 Linux kernel 是使用 tab，這裡其實只要跟合作的夥伴們講好統一使用一種即可，就不提有統計指出用 space 賺的錢比用 tab 的人多了 [^5]。

### If Statement

#### 加上空格們

```c
if(condition) {   // Bad
if (condition){   // Bad
if(condition){    // Doubly bad
if (condition) {  // Good
```

#### 加上大括號們

這裡我會比較嚴格規定自己，就算是只有一行也要加，這樣比較方便擴充，例如臨時要加上 `printf` 時就不用再加。
```c
if (condition) {
  foo;
} else {
  bar;
}
```

### Loop Statement

#### 加上空格們

注意 `;` 前不要後要。  
這裡用 `i++` 或 `++i` 其實基本上沒有效能差異 [^1]，編譯器會幫你最佳化，我更喜歡 `i++` 因為要改成 `i+=2` 之類的比較方便，另外也是有 `i-=-1` [^2] 這種邪教...

```c
for (int i = 0; i < some_number; i++) {
  printf("OuO\n");
}
```

### Pointer 變數宣告

`int*x;`、`int *x;`、`int* x`、`int * x` 都是可編譯的寫法，在 C 中 `int *x;` 更為常用。C++ 中反而是 `int* x;` [^3]。

### 命名 (Naming Convention)

#### 檔案名稱、變數 (Variable)、函式 (Function)

使用 [snake_case](https://en.wikipedia.org/wiki/Snake_case) 並取有上下文關係的名字，例如 `flag`、`count` 就沒有上下文，會不知道這個變數要用來存放什麼東西。  
e.g., `http_server_logs.h`、`table_name`  

Google 的函式也可用 UpperCamelCase，但我個人比較習慣 snake_case，另外函式須以動詞開頭以表明動作。  
e.g., `add_table_entry`

#### Struct, Class

使用 [UpperCamelCase](https://en.wikipedia.org/wiki/Camel_case)  
e.g., `UrlTableProperties`, `TableInfo`

#### 常數 (Constant)

使用全大寫並以 `_` 連接。  
e.g., `MAX_ROW_SIZE`

## 初始化 (Initialize)

寫 C 語言時要注意變數的初始化，以免結果跟自己所想的不一樣，這是因為在規格書中的定義中提到，只有全域變數或是靜態 (static) 變數會被初始化，其他未初始化的則不會有明確的初始值。 C99 §6.7.8.10 [^4]。在陣列的初始化若要全部定義為 `\0`，我們可以直接在宣告中使用 `{}` 即可，因為規格書中有規定若初始化的個數不足則會比照靜態變數 C99 §6.7.8.21 [^4]:  

```c
// 每個變數宣告時搭配初始化
int n = 0;
// 陣列初始化以下都可以
char que[26] = {'\0'};
char que[26] = {0};
char que[26] = {};
```

## 註解 (Comment)

請盡量使用英文來註解，因為英文比較不像中文那樣一詞多義，可以較明確的敘述，若執意要用中文就需要注意編碼，目前主流應該是使用 UTF8。內容部份可以多記錄一點上下文而不是僅僅該行程式碼做了什麼事，通常註解會拿來說明整個函式，會需要一行一行註解的情況比較少並會用高可讀性的程式馬來替代。我之前有找到一篇非常詳盡的指南 [^6] 可以參考看看 (雖然我也沒有仔細讀完就是了＠＠

寫法上注意空格即可。

```c
// OuO
/* OuO */
```

## 副:作用 (Side Effect)

副作用 ([Side Effect](https://en.wikibooks.org/wiki/C_Programming/Side_effects_and_sequence_points)) 聽起來好像很不妙，簡單來說就是會在函式內部修改到參數的情況。其實這在一般程式語言中頗為常見，沒有這項功能的話程式會變得相當難寫，例如 Functional language 寫起來就頗耗費腦力。

### 在函式宣告時點出副作用

但是在開發過程需要適時隔離變化，C 語言提供了 `const` 修飾字來標示該參數在函式中不會被修改。以下範例中的 `rear` 和 `orig`  不會被修改到內容，所以可以利用 `const` 來提醒函式呼叫者該參數不會被改動，反之 `front` 就有機會被改動。詳細的排列組合可以參考 [^9]。

```c
void deque(char *orig, int *front, int *rear) {
  if (*front == *rear) {
    printf("Empty");
  } else {
    printf("%c\n", orig[*front]);
    *front = *front + 1;
  }
}
```

```c
// rear, orig 皆是指向一個唯讀參數 (read-only parameter)
// 的唯讀指標 (read-only location)
// 若嘗試在函式中修改 `rear` 或 `*rear` 就會得到編譯錯誤
void deque(
    const char * const orig,
    int *front,
    const int * const rear) {
```

### 需要修改的才傳入其指標 (Pointer)

這裡要先宣導一個觀念就是 C 語言只有 Pass By Value，也就是只會複製傳入變數的數值，傳入指標也是一樣，我們只是傳入了指標這個數值，而透過這個指標的取值 (dereference) 可以改動對應的記憶體位置 C99 §6.5.2.2.4 [^4]。而因為 C 的函式回傳值只限一個，所以大部分會使用修改參數的方式來回傳數值，而真正的回傳值就用來表示函式是否正確執行，否則就回傳對應的錯誤碼。

上面那樣改起來好像太奇葩，更好的解決方式是要先思考，把將要在函式內部更動變數在傳入其指標，其餘的只須把數值傳進去即可。當然若是傳入陣列就還是需要指標就像 `orig`。

```c
// 因為最後一個參數不會變動而且只需要其數值
// 所以直接以常數傳入，當然函式內部就不需要取值了
void deque(
    char const * const orig,
    int *front,
    const int rear_value) {
  if (*front == rear_value) {
    printf("Empty");
  } else {
    printf("%c\n", orig[*front]);
    *front = *front + 1;
  }
}
```

## 多檔案

### 避免重複 include

專案擴張下，必然會用到多檔案，這時候就會拆成很多的 `.h`, `.c` 檔，`.h` 用來作為界面的溝通，這時候一定要使用 macro ([Include guard](https://en.wikipedia.org/wiki/Include_guard)) 防止重複 include。以下為檔名為 `file.h` 的內容範例：`FILE_H`, `_FILE_H`, `__FILE_H__` 都有人用，但一般以第一種為主即可。

```c
#ifndef FILE_H
#define FILE_H

/* ... Declarations etc here ... */

#endif /* FILE_H */
```

### 用 `static` 修飾內部函數

如果在多檔案下函數並不是要開放給其他檔案呼叫時，請加上 `static` 來保證只有當前檔案內部可以看到那個函數。

```c
static void my_local_function() {
  printf("OuO\n");
}
```

## 避免使用危險的函式們

C 語言給予使用者相當大的彈性但用起來需要知道自己在做什麼，否則會有許多安全性漏洞，有一些函式很容易造成誤用，連資深工程師也常用錯，因此蠻多專案直接把不安全的函式禁用，例如 Git [^12]，Intel 的 safestringlib 也有一個完整列表 [^13]。以下給出一些較常見的。

+ `gets()` [^10] C11 已經不支援，請改用 `fgets()`
+ `strcpy()` 沒有長度偵測。
+ `strncpy()` 有長度但是不會在結尾補上 `\0` [^11]。
+ `ato*()` 改用 `strto*()` 利於錯誤處理 C99 §7.20.1 [^4]。

## 其他習慣

+ 盡量不使用全域變數


[{{ 下一篇傳送門：Programming Sense (2) }}]({{< ref "/posts/20191118-programming-sense-2" >}})


[^1]: [Is there a performance difference between i++ and ++i in C?](https://stackoverflow.com/a/24887/6734174)
[^2]: [`i-=-1` is hipster, expressive and symmetric](https://twitter.com/DasSurma/status/1192736235447619584)
[^3]: [Is `int* p;` right or is `int *p;` right?](http://www.stroustrup.com/bs_faq2.html#whitespace)
[^4]: [C99 規格書 ISO/IEC 9899:TC3](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1256.pdf)
[^5]: [Developers Who Use Spaces Make More Money Than Those Who Use Tabs](https://stackoverflow.blog/2017/06/15/developers-use-spaces-make-money-use-tabs/)
[^6]: [Writing system software: code comments.](http://antirez.com/news/124)
[^7]: [Tim Pope: when people ask me to recommend a text editor](https://twitter.com/tpope/status/1172743697315835904)
[^8]: [A Python programmer attempting Java](https://www.reddit.com/r/ProgrammerHumor/comments/2wrxyt/a_python_programmer_attempting_java/)
[^9]: [What is the difference between const int*, const int * const, and int const *?](https://stackoverflow.com/a/1143272)
[^10]: [CWE-242: Use of Inherently Dangerous Function](https://cwe.mitre.org/data/definitions/242.html)
[^11]: [How can code that tries to prevent a buffer overflow end up causing one?](https://devblogs.microsoft.com/oldnewthing/?p=36773)
[^12]: [git/banned.h](https://github.com/git/git/blob/master/banned.h)
[^13]: [SDL List of Banned Functions](https://github.com/intel/safestringlib/wiki/SDL-List-of-Banned-Functions)

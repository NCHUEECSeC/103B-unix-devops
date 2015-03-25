title: Unix DevOp #1
author: PastLeo

%%%%%%%%%%%%%%%%%%%
% Use '%' to comment or directive (ex:css below)
%%%%%%%%%%%%%%%%%%%
%% You can add some custom style rules here...

%css



%end

%%%%%%%%%%%%%%%%%%%
%% occupation of scale=1:
%% x = 1200
%% y = 700
%% occupation of scale=2: [occupation of scale=1] * 2
%% x = 2400
%% y = 1400
%% occupation of scale=3: [occupation of scale=1] * 3
%% x = 3600
%% y = 2100
%% occupation of scale=4: [occupation of scale=1] * 4
%% ...
%% the location of one step (slide) is originated from the center!

%%%%%%%%%%%%%%%%%%%
%% Here we go...

%%%%%%%%%%%%%%%
!SLIDE x=0 y=0 scale=4

## Unix DevOps #1

#### Basic Operations

%%%%%%%%%%%%%%%
!SLIDE x=0 y=2000 rotate=180 scale=4

## 啥是 `DevOps`

#### [Check this out](http://zh.wikipedia.org/wiki/DevOps)

%%%%%%%%%%%%%%%
!SLIDE x=8400 y=2000 rotate=270 scale=10

### 本課期主要希望可以教會大家以下

 * Unix 基本操作
 * Linux 權限、使用者管理
 * 系統管理、軟體安裝
 * 架設 Web Server
 * 部署一個 Web service

```
希望能讓 Linux 的(雲端)伺服器成為各位的好朋友
```

%%%%%%%%%%%%%%%
!SLIDE x=3000 y=2000 z=-3000 rotate=300 scale=1

## 首先，來點基本操作

#### 打開終端機

%%%%%%%%%%%%%%%
!SLIDE x=14400 y=2000 rotate=270 scale=6

### 你可能會發現這是個 void

![terminal_1](http://i.imgur.com/MpkRc8l.png)

%%%%%%%%%%%%%%%
!SLIDE x=14400 y=2000 z=7000 rotate=270 scale=6

### 其實它的可能性比 GUI 多更多

![terminal_2](http://i.imgur.com/Bl0AleE.png)

%%%%%%%%%%%%%%%
!SLIDE center x=14400 y=2000 z=14000 rotate=270 rotate-z=90 scale=6

### 它也讓遠端操作變得比較省資源

![terminal_3](http://i.imgur.com/iiwctF2.png)

%%%%%%%%%%%%%%%
!SLIDE x=20700 y=-2000 scale=4

## One more thing ... before we start

#### 別忘了愛用 `Tab` 問問電腦有啥可用的指令


%%%%%%%%%%%%%%%
!SLIDE picture center x=20700 y=0 scale=4

### 檔案操作

![file_manager](http://i.imgur.com/B3FFDjY.png)

%%%%%%%%%%%%%%%
!SLIDE x=20100 y=-600 z=6000 scale=1

## `pwd # 取得現在的位置`

%%%%%%%%%%%%%%%
!SLIDE x=20100 y=-200 z=6000 scale=1

## `ls [-al] # 列出目前所在位置的檔案清單`

%%%%%%%%%%%%%%%
!SLIDE x=20100 y=200 z=6000 scale=1

## `cd <path> # 去別的目錄`

%%%%%%%%%%%%%%%
!SLIDE x=20100 y=600 z=6000 scale=1

## `mkdir [-p] <path> # 建立資料夾`

%%%%%%%%%%%%%%%
!SLIDE x=21300 y=-600 z=6000 scale=1

## `touch <path> # 建立 / 戳一下檔案`

%%%%%%%%%%%%%%%
!SLIDE x=21300 y=-200 z=6000 scale=1

## `mv <src> <des> # 移動 / 重新命名`

%%%%%%%%%%%%%%%
!SLIDE x=21300 y=200 z=6000 scale=1

## `cp [-Rv] <src> <des> # 複製`

%%%%%%%%%%%%%%%
!SLIDE x=21300 y=600 z=6000 scale=1

## `rm [-Rvf] <path> # 刪除`

%%%%%%%%%%%%%%%
!SLIDE x=20700 y=0 z=4000 scale=4

%%%%%%%%%%%%%%%
!SLIDE picture center x=20700 y=5000 scale=4

### 純文字檔操作

![notepad](http://i.imgur.com/WcNDCQc.png)

%%%%%%%%%%%%%%%
!SLIDE x=20100 y=4800 z=6000 scale=1

## `>> | > <path> # 把 stdout 輸入至檔案`

#### `echo 'hello everyone' >> hello`

%%%%%%%%%%%%%%%
!SLIDE x=20100 y=5200 z=6000 scale=1

## `cat <path> # 印出檔案內容`

%%%%%%%%%%%%%%%
!SLIDE x=21300 y=4800 z=6000 scale=1

## `less [+F] <path> # 觀看檔案內容`

%%%%%%%%%%%%%%%
!SLIDE x=21300 y=5200 z=6000 scale=1

## `vi | vim <path>`

#### `文字編輯器，神之編輯器`

#### [簡易操作說明](http://blog.vgod.tw/2009/12/08/vim-cheat-sheet-for-programmers/)

%%%%%%%%%%%%%%%
!SLIDE x=20700 y=5000 z=4000 scale=4

%%%%%%%%%%%%%%%
!SLIDE x=6300 y=-4000 rotate=20 scale=4

## 你剛剛呼叫的東西全部都是執行檔

#### 別忘了 `Tab` 是你的好朋友

%%%%%%%%%%%%%%%
!SLIDE x=7000 y=-5000 rotate=40 scale=3

## 這些執行檔到底在哪

```
which <exe_name>
```

%%%%%%%%%%%%%%%
!SLIDE x=7700 y=-6000 z=-100 rotate=60 scale=2

## 電腦找了那些地方?

```
echo $PATH
```

#### 記得 `Windows` 也是如此嗎

%%%%%%%%%%%%%%%
!SLIDE x=8400 y=-6500 rotate=90 scale=1

## 電腦，教我

```
man <name>
```

%%%%%%%%%%%%%%%
!SLIDE x=5000 y=-7000 scale=3

## 今天的指令先到這吧

#### 下次就要開始做系統管理了

#### 希望大家能準備好自己的 Linux 環境 (debian 為主)

#### [使出學生牌，取得雲端主機](https://gist.github.com/qas612820704/c72639928b732103a138)

#### 要不然就是用 Virtualbox 在自己的電腦上安裝...

%% The End
%%%%%%%%%%%%%%%

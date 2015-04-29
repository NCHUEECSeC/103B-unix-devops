title: Unix DevOp #3
author: PastLeo

%%%%%%%%%%%%%%%%%%%
% Use '%' to comment or directive (ex:css below)
%%%%%%%%%%%%%%%%%%%
%% You can add some custom style rules here...

%css

.bg-when-present.active {
    background: rgba(59, 65, 62, 0.85);
    border-radius: 10px;
}

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

## Unix DevOps #3

#### Service Deployment & Database

%%%%%%%%%%%%%%%
!SLIDE x=0 y=2500 scale=4

### 這堂課程我們將會

 * 認識 DBMS 資料庫
 * 安裝、設定資料庫 MySQL (MariaDB)
 * 介紹服務
 * 部署一個服務，以 Wordpress 為範例
 * 如果還有時間，希望能講到
 * 更多服務的的佈署，例如 Laravel 專案、Django 專案
 * Docker & Boot2docker

%%%%%%%%%%%%%%%
!SLIDE x=8400 y=2000 rotate=270 scale=10

### 開始囉，請確保你的環境已經準備好：

 * 雲端主機: DigitalOcean
 * VM: Vagrant + Virtualbox，[我寫的教學](https://gist.github.com/chgu82837/ab1255846b5335407105)
 * 821 的 Ubuntu 1404 環境，似乎可以裝 docker

> 如果純粹使用 Virtualbox 手動下載 ISO 的人，不妨看一下我寫的 Vagrant 教學喔

%%%%%%%%%%%%%%%
!SLIDE x=3000 y=2000 z=-3000 rotate=300 scale=1

## 首先，來認識一下 DBMS ，資料庫管理程式

%%%%%%%%%%%%%%%
!SLIDE x=14400 y=2000 rotate=270 scale=6

### 為何要用資料庫

 * 關於存檔的問題
     * 有寫過讀存檔的程式嗎？
     * 寫一個可存檔的遊戲，你如何存檔？存檔的內容怎麼排？
 * 資料庫管理程式 DBMS 可以讓我們
     * 直接使用程式語言的資料型態跟資料溝通
     * 有統一的增刪改查介面 (API)
         * 方便不同程式溝通
         * 可以用別人寫好的 GUI 操作或是除錯
     * 還有很多...

%%%%%%%%%%%%%%%
!SLIDE x=14400 y=2000 z=10000 rotate=270 rotate-x=180 scale=6

### 有哪些 DBMS

 * 用網路進行存取，同時功能比較完整，有使用者、存取控制等等功能：
     * MySQL
     * PostgreSQL
 * 用檔案作為資料庫，只是純粹使用 SQL 語言進行資料存取：
    * Sqlite

> 到現在其實我蠻推薦開發的時候使用 Sqlite 進行開發，因為測試資料比較容易攜帶而且簡單，正式上線再弄成 MySQL 變成方便管理

%%%%%%%%%%%%%%%
!SLIDE x=20700 y=-2000 scale=4

###  我們用 MySQL 作為範例，所以來安裝 MySQL 吧

```
apt-get update
apt-cache search mysql
apt-get install ...?
```

> 嘿，還記得套件管理程式嗎

%%%%%%%%%%%%%%%
!SLIDE x=20700 y=0 scale=4

### MySQL 的管理介面

 * Commandline: `mysql -u <username> -h localhost -p`
 * for Windows: [HediSQL](http://www.heidisql.com/)
 * for OSX: [Sequel Pro](http://www.sequelpro.com/)

%%%%%%%%%%%%%%%
!SLIDE x=20700 y=0 z=-4000 scale=4

### MySQL 資料庫的架構

```
Database > Table > Row > Column
           + ---- Schema ---- +
```

 * 通常一個 `Database` 對應一個應用程式
 * 通常一個 `Table` 對應一個 `Class`
 * 通常一個 `Row` 對應一個 `Object`
 * 通常一個 `Column` 對應一個 `Object 的屬性或是成員`
 * `Schema` 則是定義有哪些 `Table`, `Row`, `Column`

> 大部分資料庫的架構都是如此

%%%%%%%%%%%%%%%
!SLIDE x=20700 y=0 z=-8000 scale=4

### MySQL 幾個常用的指令

```
show databases; # 觀看所有資料庫
use <db_name>; # 選定一個資料庫
show tables; # 顯示一個資料庫的所有 Table
use mysql; select user,host,password from user; # 顯示所有使用者 (host 為允許登入的來源)
CREATE USER 'username'@'localhost' IDENTIFIED BY 'pw'; # 增加使用者
CREATE DATABASE <name>; # 建立資料庫
GRANT ALL ON <db_name|*>.* TO 'username'@'localhost' WITH GRANT OPTION; # 給予全部權限
exit # 離開
```

%%%%%%%%%%%%%%%
!SLIDE center x=20700 y=5000 scale=4

### 初始化，並設定 MySQL

 * 如果你的環境跟我一模一樣，那麼應該會在安裝的時候請你設定 root 密碼
 * `mysql_secure_installation` 把 root 的遠端登入取消
 * 接著我們來設定一個最高使用者來取代 root 這個登入
    * 作為管理的示範
    * 也幫自己建立一個神的腳色
    * DEMO，用 Commandline

%%%%%%%%%%%%%%%
!SLIDE bg-when-present x=20700 y=5000 z=4000 scale=4

## 這樣一來對 DBMS 應該有基本概念並且稍微會管理了

#### 接下來進入服務的介紹

%%%%%%%%%%%%%%%
!SLIDE x=6300 y=-4000 rotate=20 scale=4

## 關於這裡說的服務...

#### 提供服務等待別人隨時來使用

#### 所以就是一個監聽網路來訪且持續運作的應用程式

%%%%%%%%%%%%%%%
!SLIDE x=7000 y=-5000 rotate=40 scale=3

## 網路上有很多開源的這類應用程式

#### 例如 [Wordpress](https://tw.wordpress.org), [Joomla](http://joomla.org.tw), [Drupal](http://drupaltaiwan.org), [mediawiki](https://www.mediawiki.org/wiki/MediaWiki), [Gitlab](https://about.gitlab.com) 等

#### 或者自己寫的應用程式，例如學生會的一些專案

%%%%%%%%%%%%%%%
!SLIDE x=7700 y=-6000 z=-100 rotate=60 scale=2

## 接下來我們就是要來把這些應用程式架設成服務 (Deplpy)

%%%%%%%%%%%%%%%
!SLIDE x=8400 y=-6500 rotate=90 scale=1

### 架設服務的大概流程

 1. 閱讀作者的說明文件
 2. 安裝運作需要的軟體，把環境準備好 (Dependency)
 3. 取得應用程式本體，可能透過 git clone, wget 或者流覽器下載，啊如果需要編譯就來編一下
 4. 如果會需要用到資料庫，則
    1. 幫應用程式建立一個資料庫以及使用者
    2. 把 schema 建到資料庫裡，通常可以用 framework 的 migration 功能建立
 5. 依照說明文件設定其他東西，如果有需要
 6. 啟動服務，依照你的服務環境啟動的方式也不同

%%%%%%%%%%%%%%%
!SLIDE x=8400 y=-6500 z=-1000 rotate=90 scale=1

## DEMO 佈署 Wordpress

%%%%%%%%%%%%%%%
!SLIDE x=8400 y=-6500 z=-2000 rotate=90 scale=1

## 然後來 DEMO 架設一個由 Framework 建立的應用程式

#### 大家想要看哪個勒？

#### Laravel 專案 (based on PHP)：[三合一選舉系統](https://git@github.com:NCHUSG/app_election.git)

#### Django 專案 (based on Python)：[唯一學號取票系統](https://git@github.com:NCHUSG/eve_prVoting.git)

%%%%%%%%%%%%%%%
!SLIDE x=5000 y=-7000 scale=3

### 關於建立環境這件事...

 * 永遠不能期待不會出問題
 * 根據我的經驗，用 Linux 或是 OSX 建立環境問題都比較少
     * 因為有 apt-get, yum 或是 brew
     * 結論就是不要用 Windows 開發XDD
 * 可是我平常要打 LOL，必須使用 Windows 怎辦？

%%%%%%%%%%%%%%%
!SLIDE x=5000 y=-7000 z=-3000 scale=3

### 一個很潮的東西：Docker

 * 一個潮到出水的虛擬技術，只模擬作業系統而不模擬硬體
 * 缺點是，只能 Linux 虛擬 Linux
 * 那到底能幹麻
 * 對企業級使用來說，就算是 Linux 上也有很多相依的問題，他們用 docker 來做這個問題的解決
 * 那對我們小開發者呢？
 * 先講一下 docker 的優點

%%%%%%%%%%%%%%%
!SLIDE x=5000 y=-7000 z=-6000 scale=3

### Docker 是一個只虛擬作業系統，driver 以及硬體都直接使用原本的作業系統

 * 啟動虛擬機的速度跟執行一個程式一樣快，秒速完成
 * 環境可以用堆疊的，所以可以有兩個環境共用同一個基底環境
 * 環境之間完全切開，可以解決 Python2 跟 Python3 的問題
 * 最後使用起來消耗的容量遠小於 VM
 * 最重要的一點是他因為限制使用 Linux，所以原生支援使用 Shell script 自動部署，還可以直接從網路下載別人建立好的環境，這樣一來

%%%%%%%%%%%%%%%
!SLIDE bg-when-present x=4000 y=-8000 z=-4500 rotate-x=-90 scale=1

### 好吧，要怎麼開始使用 Docker 呢？ (Boot2docker)

 * 就算是 OSX 也不算是 Linux，所以需要一層 boot2docker 這個虛擬機 (using virtualbox)
 * 靠阿還不是需要虛擬機，而且還是在虛擬機裡頭開虛擬環境
 * 你錯了，這個虛擬機只有 23 MB，你沒看錯，這個虛擬機只包了 Linux 的核心和 docker
 * 這個虛擬機開機當然也快，等開好之後再透過 docker 建立任何 Linux 環境，這樣整個環境堆疊就顯得很合理好用了
 * DEMO 安裝 Boot2docker

%%%%%%%%%%%%%%%
!SLIDE x=4000 y=-10000 z=-4500 rotate-x=-90 scale=1

### 利用 Docker 最重要的特性：使用別人寫好 / 建立好的環境：

 * 使用 Dockerfile，[官方說明](https://docs.docker.com/reference/builder/)
 * 但是有些參數還是很麻煩，我有寫好一個方便大家建立環境的工具：dockeRun
 * DEMO dockeRun 安裝以及使用

> `dockeRun` 只是一個 shell script 來幫助我們，請各位大大有興趣一定要參考一下 docker 原生的文件

%%%%%%%%%%%%%%%
!SLIDE x=-3000 y=-7000 scale=4

### 講到這裡，我想我已經做到 devOps 的『引入門』的動作了

 * 希望大家能夠自發性的找尋目標來做練習，例如幫自己架設一個網誌之類的
 * 將來真的要面對環境或 Linux 管理的問題的時候，一些 Google 旁敲側擊絕對還是不可免的，我交給大家的只是我個人經驗的總結，希望大家能夠有個基本概念
 * 謝謝大家，Unix DevOps 課程到此結束

%% The End
%%%%%%%%%%%%%%%

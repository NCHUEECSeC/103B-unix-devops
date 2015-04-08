title: Unix DevOp #2
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

## Unix DevOps #2

#### Management & Software installation

%%%%%%%%%%%%%%%
!SLIDE x=0 y=2000 rotate=180 scale=4

## Linux 可以用來做啥？

%%%%%%%%%%%%%%%
!SLIDE x=8400 y=2000 rotate=270 scale=10

### 我先講我用來做啥

 * [我的個人網頁](http://pastleo.me)
 * 這個 Slide 放置的地方
 * Minecraft server XDD

```
想來玩的...可以找我加入，不過伺服器很弱，撐不了很多人ㄎ
```

%%%%%%%%%%%%%%%
!SLIDE x=3000 y=2000 z=-3000 rotate=300 scale=1

### 雲端伺服器還可以拿來幹麻

 * 架設XX網站
 * 自己的 mail server
 * 遊戲 backend server
 * SFTP 自架網路硬碟

```
總之就是一個不關機的電腦，提供隨時隨地可存取的服務
```

%%%%%%%%%%%%%%%
!SLIDE x=14400 y=2000 rotate=270 scale=6

### 首先取得你的 Linux 環境

 * 如果你有帶自己的電腦： VM 虛擬機 -- [Vagrant & Virtualbox](https://gist.github.com/chgu82837/ab1255846b5335407105)
 * 如果你 [DigitalOcean 學生方案](https://gist.github.com/qas612820704/c72639928b732103a138) OK，就用這個吧，之後的變動都可以直接應用進去
 * 以上都沒有的話...就用眼前的電腦吧

> 如果要跟我一樣，環境請選擇 Debian 7 (wheezy)  
> [debian75-x64 for vagrant](https://atlas.hashicorp.com/puphpet/boxes/debian75-x64)

%%%%%%%%%%%%%%%
!SLIDE x=14400 y=2000 z=7000 rotate=270 scale=6

## DEMO

#### 啟動一台 DigitalOcean

%%%%%%%%%%%%%%%
!SLIDE x=20700 y=-2000 scale=4

### SSH 連線

```
ssh <user_name>@<host>
```

製作通行證：  

```
ssh-keygen # 生產 ssh key
```

%%%%%%%%%%%%%%%
!SLIDE picture center x=20700 y=0 scale=4

## [使用者管理](http://linux.vbird.org/linux_basic/0410accountmanager.php)

%%%%%%%%%%%%%%%
!SLIDE bg-when-present x=20100 y=-300 z=6000 scale=1

## `su` / `sudo`

#### [變更身份 / 使用不同身份做 ...](http://linux.vbird.org/linux_basic/0410accountmanager.php#userswitch)

%%%%%%%%%%%%%%%
!SLIDE bg-when-present x=21300 y=0 z=6000 scale=1

## `useradd <user_name>`

#### [創造使用者](http://linux.vbird.org/linux_basic/0410accountmanager.php#useradd)

%%%%%%%%%%%%%%%
!SLIDE bg-when-present x=20100 y=300 z=6000 scale=1

## `usermod <option> <user_name>`

#### [更改使用者](http://linux.vbird.org/linux_basic/0410accountmanager.php#usermod)

%%%%%%%%%%%%%%%
!SLIDE x=20700 y=0 z=4000 scale=4

%%%%%%%%%%%%%%%
!SLIDE center x=20700 y=5000 scale=4

## [權限控制](http://linux.vbird.org/linux_basic/0210filepermission.php)

%%%%%%%%%%%%%%%
!SLIDE bg-when-present x=20100 y=4800 z=6000 scale=1

## `chown [-Rv] <user>[:<group>] <path>`

#### [更改擁有者](http://linux.vbird.org/linux_basic/0210filepermission.php#chown)

%%%%%%%%%%%%%%%
!SLIDE bg-when-present x=21300 y=5200 z=6000 scale=1

## `chmod [-Rv] <mod> <path>`

#### [修改權限模式](http://linux.vbird.org/linux_basic/0210filepermission.php#chmod)

%%%%%%%%%%%%%%%
!SLIDE x=20700 y=5000 z=4000 scale=4

%%%%%%%%%%%%%%%
!SLIDE x=6300 y=-4000 rotate=20 scale=4

## 系統狀態查詢

%%%%%%%%%%%%%%%
!SLIDE x=7000 y=-5000 rotate=40 scale=3

## [類似只能看的工作管理員](http://linux.vbird.org/linux_basic/0440processcontrol.php#process_1)

```
top
```

```
ps auxww | grep <program>
```

%%%%%%%%%%%%%%%
!SLIDE x=7700 y=-6000 z=-100 rotate=60 scale=2

## [網路狀態](http://linux.vbird.org/linux_server/0140networkcommand.php#ifconfig)

```
ifconfig
```

#### `Windows` 上叫做 `ipconfig`

%%%%%%%%%%%%%%%
!SLIDE x=8400 y=-6500 rotate=90 scale=1

## [目前電腦網路連線](http://linux.vbird.org/linux_server/0140networkcommand.php#netstat)

```
netstat -tenlp # 目前監聽網路的清單
```

#### 大部分 Linux 適用， Mac 上要用別的

%%%%%%%%%%%%%%%
!SLIDE x=5000 y=-7000 scale=3

## 套件管理程式

#### 自動從網路下載並安裝程式

#### 我決定要來好好講一下這個部分

%%%%%%%%%%%%%%%
!SLIDE x=5000 y=-7000 z=-3000 scale=3

### 套件管理程式的好處

 * 把安裝軟體的方式簡單化，就像在 App 商店安裝應用程式一般簡單
 * 輕鬆追蹤是否有更新，一鍵更新所有套件
 * 如果軟體間存在相依性，會自動把缺少的一併安裝

> 應用程式、環境安裝上的好幫手  
> 我目前基本上都以套件安裝取代手動(編譯)安裝

%%%%%%%%%%%%%%%
!SLIDE x=5000 y=-7000 z=-6000 scale=3

### 套件管理程式的大致使用方法

 1. 知道你要安裝的套件名稱，透過 `Google` 旁敲側擊是不錯的方法
 2. `<exe> install <package_name>`

`<exe>` 根據不同的套件管理程式而不同，以下將進行介紹

> 這個只是大致的使用方法！！要根據狀況自行應變啊  
> 這個只是大致的使用方法！！要根據狀況自行應變啊  
> 這個只是大致的使用方法！！要根據狀況自行應變啊  

%%%%%%%%%%%%%%%
!SLIDE bg-when-present x=4000 y=-8000 z=-4500 rotate-x=-90 scale=1

### 系統內建的軟體安裝套件管理程式

根據不同 Linux 作業系統會有不一樣的套件管理程式

 * Ubuntu / Debian 系列: `apt-get`
    * 任何操作之前都先 `apt-get update` 一下
    * 可以用 `apt-cache search <package>` 搜尋套件
    * `apt-get install <package>` 進行安裝
    * 另外有個 `aptitude` 的屌程式可用
 * CentOS / RedHat 系列: `yum`
    * `yum search <package>` 搜尋套件
    * `yum install <package>` 進行安裝

%%%%%%%%%%%%%%%
!SLIDE x=4000 y=-10000 z=-4500 rotate-x=-90 scale=1

## DEMO : 安裝 nginx

%%%%%%%%%%%%%%%
!SLIDE bg-when-present x=5000 y=-8000 z=-4500 rotate-x=-90 scale=1

### 軟體安裝的套件管理程式也可以由第三方提供

 * OSX: [homebrew](http://brew.sh)
    * 讚，好用
    * `brew install <package>`
 * Windows: [chocolately](https://chocolatey.org)
    * [舉例：用 chocolately 安裝 Putty](https://chocolatey.org/packages/putty)
    * [舉例：用 chocolately 安裝 Visual Studio 2013 !?](https://chocolatey.org/packages/VisualStudio2013Ultimate)
    * BUT 很容易出問題，Windows 哭哭

但是由於是第三方提供，作業系統一更新就很容易 GG

%%%%%%%%%%%%%%%
!SLIDE bg-when-present x=6000 y=-8000 z=-4500 rotate-x=-90 scale=1

### 特定程式語言的套件安裝

現在新潮的程式語言都有套件管理程式

 * Python: `pip`，通常伴隨 Python 一同安裝
 * Ruby: `gem`，通常伴隨 Ruby 一同安裝
 * NodeJs: `npm`，通常伴隨 NodeJS 一同安裝
 * PHP: `composer`，和以上三者比較不同，[來這取得](https://getcomposer.org)

%%%%%%%%%%%%%%%
!SLIDE x=6000 y=-10000 z=-4500 rotate-x=-90 scale=1

## DEMO : 安裝 Python + Django

%%%%%%%%%%%%%%%
!SLIDE x=5000 y=-10000 z=-4500 rotate-x=-90 scale=1

## 背景服務的控制

```
service [service_name] [status | start | stop]
# CentOS 7 改成 systemctl 了
```

%%%%%%%%%%%%%%%
!SLIDE x=5000 y=-12000 z=-4500 rotate-x=-90 scale=1

## DEMO 啟動 nginx

%%%%%%%%%%%%%%%
!SLIDE x=5000 y=-12000 scale=4

## 關於 Linux 的設定檔 `/etc/`

#### 用講的沒FU

#### DEMO 設定 Nginx 根目錄到自己的家目錄下

%%%%%%%%%%%%%%%
!SLIDE x=0 y=-7000 scale=4

## 這樣一來大家就會建立基礎環境了

#### 請各位把自己的個人網站架到一台 Linux 電腦上

#### [像是這樣](http://pastleo.me)

%%%%%%%%%%%%%%%
!SLIDE x=-3000 y=-7000 scale=4

### 下禮拜會說明進階的服務架設

基本上就是需要資料庫的 Service

 * DBMS: 以 MySQL 為例
 * [Wordpress](https://tw.wordpress.org/)
 * [Django](https://www.djangoproject.com/)
 * [Laravel](http://laravel.tw/)

%% The End
%%%%%%%%%%%%%%%

# Cloud9 on EC2 安裝筆記

先前在用 [Cloud9](https://c9.io/) 的編輯器玩 [Node.js](https://nodejs.org/en/) 時覺得很方便, 可以線上直接編輯, 運行, 但是免費使用時, 機器不會 always 保持開啟, 也只有一個 private 的 repository 可以用, 看一下計價 ![](https://s3-ap-northeast-1.amazonaws.com/daidoujiminecraft/Daidouji/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7+2016-10-02+%E4%B8%8A%E5%8D%8811.03.00.png) 實在是超級貴酸酸, 而 AWS 最便宜的一台機器 `t2.nano` 一個月算下來大約只要 5 鎂, 永遠在線, 無限 repository, 非常的划算, 加上 Cloud9 的 [Source](https://github.com/c9/core/) 有放在 github 上, 讓我們可以自己 DIY 一台, 下面將紀錄安裝的流程步驟, 以防未來連我自己都忘記.

## 首先要有一台開好的機器

起手隨便開

 * AMI - 這個時間點上, 我選的是 `Amazon Linux AMI 2016.09.0 (HVM), SSD Volume Type - ami-1a15c77b`
 * Instance Type - `t2.nano`, 便宜, 而且可以集能量, 酷炫又帥
 * Instance Details - 本身沒什麼要調整, 直接下一步
 * Add Storage - 調整需要的硬碟大小, 看個人需求
 * Tag Instance - 也是隨便, 可以叫鵝妹子嚶
 * Security Group - 要開的 port, 用預設的 22, 可以連上先
 
review 看還有沒有什麼要改的, 都 ok 就 launch. 等機器開好中 
![](https://s3-ap-northeast-1.amazonaws.com/daidoujiminecraft/Daidouji/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7+2016-10-02+%E4%B8%8A%E5%8D%8811.35.01.png)
開好後, 連入機器, 先設定 root 用戶, 可以參考 [第一次設定Root密碼](http://wuboshian.pixnet.net/blog/post/25311095-%5Blinux%5D-%E7%AC%AC%E4%B8%80%E6%AC%A1%E8%A8%AD%E5%AE%9Aroot%E5%AF%86%E7%A2%BC), 切成 su 之後這邊就告一個段落.

## 前置安裝

 * 更新當前機器既有套件 - `sudo yum update -y`
 * 安裝後面步驟需要的套件 - `sudo yum install git gcc-c++ glibc-static -y`
 * clone node - `git clone https://github.com/nodejs/node`
 * build node
  - `cd node`
  - `./configure`
  - `make` (輸入後需要等待一段很長的時間, 可以靠開更強的機器解決這個問題...後來開了 m3.medium 還是花很多時間)
  - `sudo make install`
  - `cd ..`
  
## Cloud9 安裝

 * clone Cloud9 - `git clone git://github.com/c9/core.git c9sdk`
 * install Cloud9
  - `cd c9sdk`
  - `./scripts/install-sdk.sh`
 * 安裝完畢之後, 會提示 `node server.js -p 8080 -a`, 運行後就可以 work 囉
 

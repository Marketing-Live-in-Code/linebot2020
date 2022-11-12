# 打造聊天機器人，商管人也看得懂的最詳細步驟【2020年最新更新版本】

> 相關文章：
> [幫助Python新手度過陣痛期的關鍵功能！整合開發環境 Spyder三大功能初學者必看！一個觀念，開啟Python 網路爬蟲成長之路！](https://medium.com/%E8%AA%A4%E9%97%96%E6%95%B8%E6%93%9A%E5%8F%A2%E6%9E%97%E7%9A%84%E5%95%86%E7%AE%A1%E4%BA%BAzino/%E5%B9%AB%E5%8A%A9python%E6%96%B0%E6%89%8B%E5%BA%A6%E9%81%8E%E9%99%A3%E7%97%9B%E6%9C%9F%E7%9A%84%E9%97%9C%E9%8D%B5%E5%8A%9F%E8%83%BD-%E6%95%B4%E5%90%88%E9%96%8B%E7%99%BC%E7%92%B0%E5%A2%83-spyder%E4%B8%89%E5%A4%A7%E5%8A%9F%E8%83%BD-619f43ea0e8f)

經過Line的大改版，Github被微軟收購後，整個Line預警機器人操作，明顯與之前不同。相信商管背景的您，對於系統的架構感到陌生，因此我們撰寫本篇文章，讓即刻想打造預警機器人的您，可以立馬上手。
![Line Bot機器人建置圖](https://i.imgur.com/53RpeU8.png)

## 平台創建
本文章共會用到三個平台，分別是Heroku、Line、Github。請依照以下步驟，帶領您一步步進行申請。

### Heroku
Heroku是支援多種程式語言的雲端平台服務。簡單來說，就是您租用了美國的某台電腦，並將機器人的程式碼傳到上面。我們大家都有電腦，為什麼還要特別租一台電腦呢？因為程式碼放在您自己的電腦，那您的電腦就要24小時不斷電，否則機器人服務會停止。且放在自己電腦，就要承擔所有資安、斷電、水災等風險。

您可能會擔心租金要多少。其實本專案並不用支付額外任何費用。Heroku有免付費版本，但有以下限制：
* 機器閒置30分鐘後會睡覺：剛使用機器人的時候，大約要等待10秒。
* 只能申請5個專案：最多五個，超過要付費。因此代表只能有5個機器人。
* 521Mb容量：免費租用電腦，容量當然不會太大，但對機器人非常夠用。

#### 創辦heroku帳號
[點我到heroku](https://www.heroku.com/)
密碼要求必須要英文大小寫、數字混合。接下來的範例，需要將程式碼部屬（傳送）到上面。
![](https://i.imgur.com/CzR5Bdf.png)

#### 創立一個新的APP專案
按下右上角「Creat new app」。
![Heroku官網畫面](https://i.imgur.com/vKXt5mV.png)

#### 創立專案
專案的名稱必須是世界上獨一無二，類似線上遊戲角色ID的概念。到這裡heroku平台就告一段落了。等等進行串接的時候會再回來。
![創立一個新的APP專案](https://i.imgur.com/6MdlpF2.png)

### Github
如果您走軟體業，不能不知道這個平台。Github是目前全世界最大的git平台，簡單來說，就是能將程式碼傳上去的平台，當然還支援版本控制、共同開發等。很多公司應徵工程師，都會看您在Github上的專案貢獻喔！

由於2018年微軟收購了Github平台，本來Github的私有功能（就是別人看不到您傳上去的程式碼）是要付費的，現在免費了，因此我們選擇用Github平台作為部屬的媒介。部屬過程會很繁瑣，但對於商管人來說，friendly的圖形化界面更重要。

#### 創立Github帳號
[點我到Github](https://github.com/)
因為資安意識的抬頭，帳號申請加入了很多機器人驗證的過程。
![創立Github帳號](https://i.imgur.com/LziW4Fi.png)

#### 創立Github專案
專案的名稱只要不要在帳號中有重複即可。非常重要的一點，必須要句選Privite，否則等等上傳的程式碼中，會有您機器人的「密碼」，如果別人知道這組密碼，那它就可以利用您的機器人，隨意散播訊息，甚至是不法用途。
![創立Github專案](https://i.imgur.com/4uEXxMP.png)

### Line
近年來Line經過多次的改革，將原本的Line developer跟分隔成原本的Line developer 與 Line manager（之後兩者都會用到）。商管人可能對於 Line manager會比較熟係，最有名就是Line @，但最近修改條約後，收費大幅度上升，相對我們今天的主軸，Line bot的價格便宜了很多。

> Line@收費
![資料來自Line@官方](https://i.imgur.com/xcAW6OS.png)
> Line bot
![資料來自Line Developer](https://i.imgur.com/s5nawFP.png)

#### 登入Line Developer
[點我到Line Developer](https://developers.line.biz/en/)
接下來到Line developer創建屬於自己的Linebot機器人專案，先登入自己的Line帳號後，就可以進入了。由於一般大家Line都是用手機自動登入，很多人早就忘記密碼是多少，因此還有提供QR code的登入方式，您可以多多利用。
![圖片來自Line Developer官方網站](https://i.imgur.com/ulADc2e.png)

#### 創立providers
providers的意思是提供者，可以把它當作專案的分類資料夾。通常會將私人使用的機器人，與公司的機器人分開。
![創建providers](https://i.imgur.com/E9iT4Sj.png)

#### 創立機器人專案
選擇「Create a new channel」後，在channel中選「Messaging API」。
![創建新的Messaging API](https://i.imgur.com/tPXD5bz.png)

輸入機器人的基本資料。其中要注意的是channel name的部分，也就是機器人的名稱。這個名稱雖然之後可以做修改，但改完後有7天不能更動，因此命名還是要決定好再輸入。
![機器人的各項設定](https://i.imgur.com/PBBxna4.png)

## 三大平台串聯
接下來就要將剛剛申請完成的Heroku、Line、Github。串接的過程三個平台會交叉切換，因此三個平台的畫面請隨時準備好。

### 下載Line bot程式碼
裡面有三個檔案，簡單與您介紹。
> 📌Procfile：
> Heroku所需要的文件，讓Heroku的主機知道要開啟機器人的主程式是哪一個。因此檔案app.py的名稱若有做修改，這裡面也必須一起修改。

> 📌app.py：
> 機器人的主程式，本文章會修改的程式碼都在這個檔案中。檔案內的方法handle_message(event)是主要編輯區塊，所有與使用者對答的邏輯都在這裡實作（程式碼41～44行）。

> 📌requirements.txt：
> 告訴Heroku要安裝哪一些套件。requirement的意思就是先決條件，要搭建這個機器人，需要用到的套件，就是他的先決條件。
![](https://i.imgur.com/KGYwn1g.png)

### 貼上Channel secret
我們剛剛申請好的機器人專案中，有一個「Channel secret」的選項，貼到您剛剛下載的app.py檔案中，第17行的位置。
![貼上Channel secret](https://i.imgur.com/wwkPAcu.png)

### 貼上Your user ID
找到「Your user ID」，並複製到app.py檔案中，第19行的位置。
![貼上Your user ID](https://i.imgur.com/XfcOSnG.png)

### 貼上Channel access token
切換上方的選項Messaging API，找到「Channel access token」並按下後方的Issue，即可得到token，並複製到app.py檔案中，第15行的位置。

> 請注意！若有心人士拿到這個token，他就可以操控您的機器人，因此請妥善保管。
![貼上Channel access token](https://i.imgur.com/VKBuHE4.png)

### 設定Webhook URL
一樣在選項Messaging API中，找到「Webhook settings」，將我們在Heroku中申請好的專案網址貼上，後方必須要加入「/callback」，否則會無法執行。
![設定Webhook URL](https://i.imgur.com/2ZTccoQ.png)

### 打開Webhook
這個步驟很簡單，送出剛剛的webhook後，將下方的use webhook打開即可（呈現綠色）。為何這麼簡單的動作，我還會獨立出一個步驟呢？因為時常會有朋友忘記把他打開，甚至有時候明明打開了，網頁重新整理，又被關閉了，因此這邊必須多次確認。
![打開Webhook](https://i.imgur.com/8nbzzj9.png)

### 細節設定
這部分不一定要設定。
![細節設定](https://i.imgur.com/0VCfBfT.png)

### 加入好友
您可以加入自己機器人的好友了，但機器人還沒有任何功能，所以密他並不會有任何回復喔（或者是罐頭回復）。
![加入好友](https://i.imgur.com/sy1njRL.png)

## 上傳程式碼到平台
完成這個步驟，您的機器人就活起來了！待會會將編寫好的程式碼，先上傳到Github中，再將Github與Heroku連接，進行部屬。

### 上傳程式碼到Github：
請切換到各位剛辦好的Github專案，點選「Upload files」，並將四個檔案都拉進去。
![上傳程式碼到Github](https://i.imgur.com/u5ZNHCU.png)

### Heroku與Github連接
請選擇Deployment method中的Github，以前機器人都是使用第一個heroku Git，他是使用終端機的方式。當初會這樣選擇是因為，當時github設置私有專案是要付費的，但現在變成免費的，那也會建議商管人用圖形化介面的Github就好，不要一直與終端機打交道。
![Heroku與Github連接](https://i.imgur.com/trnpZN1.png)

### 佈署機器人
拉到最下方，按下Deploy Branch即可佈署了。
![佈署機器人](https://i.imgur.com/vZlN05Z.png)

## 測試機器人
如果您的機器人有主動密你說：「你可以開始了」，那就代表「三大平台串接」的整個步驟沒有問題。這裡就可以發現，罐頭回復非常影響使用者體驗，因此建議回到「細節設定」的部分，將它關掉。
![測試機器人](https://i.imgur.com/TMExLab.png)

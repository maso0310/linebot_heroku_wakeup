
# 操作步驟：<br>

1.下載程式碼
~~~
git clone https://github.com/maso0310/linebot_heroku_wakeup.git
~~~
2.依照[此篇影片](https://youtu.be/cHKr211oTlQ)內容步驟中進行程式碼中LINEBOT、MongoDB設定<br><br>

3.將自己的herokuapp網址複製至下圖紅框中，完成指定的herokuapp喚醒設定<br>
![喚醒heroku的網址設定](https://i.imgur.com/OcVdGnz.jpg)
<br><br>

4.若要維持每天24小時運作，則需要進入heroku官網進行信用卡資料設定(從每月550小時額度新增為1000小時)，同一個帳號之下的APP使用的運作時間共同計算，可由信用卡設定下方觀看每月額度與已使用累積時間。
![heroku信用卡設定的位置](https://i.imgur.com/gMWiDL3.jpg)<br>
<br><br>

5.部署至herokuapp之後，可由自己的heroku根路徑('/')網址進入以下網頁<br>
![簡易說明頁面](https://i.imgur.com/Kyauumv.png)<br>

6.在herokuapp的more當中，可由viewlog看到每28分鐘進行一次喚醒的動作，代表完成設定<br>
![喚醒成功的log](https://i.imgur.com/NRneRZW.jpg)<br><br>

## 簡易的聊天機器人資料庫 Heroku / MongoDB / LINE BOT / HTML網頁<br><br>

### 讓herokuapp持續運作不休眠 / flask的route設定與templates網頁模板<br><br>
1.在app.py當中設定要放置html模板的路徑位置，template_folder='templates'
~~~
app = Flask(__name__,template_folder='templates')
~~~
2.新增兩個route，一個在根路徑("/")下，作為首頁範例，另一個則是在("/heroku_wake_up")
~~~
@app.route("/")
def index():
    return render_template("./index.html")

@app.route("/heroku_wake_up")
def heroku_wake_up():
    return "Hey!Wake Up!!"
~~~
3.建立templates資料夾，並新增第一個範例首頁index.html
~~~
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Maso的萬事屋LINEBOT範例</title>
</head>

<body>
    <h1>Maso的萬事屋LINEBOT範例，使用到以下套件</h1>
    <ul>
        <li>Flask: 一個使用Python編寫的輕量級Web應用框架。</li>
        <li>line-bot-sdk: 一個基於Python的SDK，可用於呼叫LINE BOT API。</li>
        <li>Pymongo: 串連No SQL資料庫型態的MongoDB所使用的python套件。</li>
        <li>Requests: 用於透過pyhon發出request的套件。</li>
        <li>BeautifulSoup4: 用於解析HTML文檔的套件。</li>
    </ul>
</body>

</html>
~~~
4.建立每28分鐘喚醒herokuapp的request函數，並以子執行緒方式啟動，使該任務在不影響主程式情況下持續運作
~~~
#======讓heroku不會睡著======
import threading 
import requests
def wake_up_heroku():
    while 1==1:
        url = '你的herokuapp網址' + 'heroku_wake_up'
        res = requests.get(url)
        if res.status_code==200:
            print('喚醒heroku成功')
        else:
            print('喚醒失敗')
        time.sleep(28*60)

threading.Thread(target=wake_up_heroku).start()
#======讓heroku不會睡著======
~~~
5.完成以Flask網頁框架製作的LINEBOT、HTML網頁模板、MongoDB資料庫與持續運作的herokuapp範例專案部署
<br><br>

====================================<br>
如果喜歡這個教學內容<br>
歡迎訂閱Youtube頻道<br>
[Maso的萬事屋](https://www.youtube.com/playlist?list=PLG4d6NSc7_l5-GjYiCdYa7H5Wsz0oQA7U)<br>
或加LINE私下交流 LINE ID: mastermaso<br>
![LOGO](https://yt3.ggpht.com/ytc/AKedOLR7I7tw_IxwJRgso1sT4paNu2s6_4hMw2goyDdrYQ=s88-c-k-c0x00ffffff-no-rj)<br>
====================================<br>

# 如何在Local端架設Swagger UI
### 一、安裝Docker ( 若已安裝可跳過 )

Mac
https://docs.docker.com/desktop/install/mac-install/

Windows
https://docs.docker.com/desktop/install/windows-install/

Ubuntu
```
$ sudo apt update
$ sudo apt install docker.io
```
<br>
二、下載映像檔並執行

下載 pull
$ sudo docker pull swaggerapi/swagger-ui

執行 run
```
$ sudo docker run -d -p 8886:8080 --name swagger swaggerapi/swagger-ui
```
參數說明
-d, detach, 在背景執行不然會卡住 terminal
-p, port binding, 把 docker內的8080 bind 到 目前機器上的 8886
--name, 命名為swagger, 比較好操作

打開網頁, 輸入 http://localhost:8886, 就能看到 swagger-ui 的頁面了！( 快速驗證完成 )

<br>
三、複製json檔案內容

點擊「 標題下方的json網頁連結 」, 會出現 json內容的網頁, 把內容複製下來存成「 data.json 」

使用編輯器開啟 data.json 把標題title那一欄位改成「 更改後的標題 哈哈 」

<br>
四、使用自己的json檔

在 data.json 的資料夾下 「 pwd 」會得到一個路徑位置 例如「 /aaaa/bbbb/cccc/data.json 」

把原本的container砍掉
```
$ docker stop swagger
$ docker container rm swagger
```
重新執行並指定自己的檔案路徑
```
$ docker run -d -p 8886:8080 -e SWAGGER_JSON=/mnt/data.json -v /aaaa/bbbb/cccc/:/mnt --name swagger swaggerapi/swagger-ui
```
<br>
五、看結果

瀏覽器輸入 https://localhost:8886

應該會看到 Swagger UI 的網頁 with 標題 「 更改後的標題 哈哈 」

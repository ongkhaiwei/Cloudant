---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2017-01-11 -->

# 建立簡單的 {{site.data.keyword.cloud_notm}} 應用程式以存取 {{site.data.keyword.cloudant_short_notm}} 資料庫：上傳應用程式

指導教學的這一節說明如何上傳 {{site.data.keyword.cloud}} 應用程式。
{:shortdesc}

<div id="uploading"></div>

## 連接至 {{site.data.keyword.cloud_notm}}

第一項作業是連接至 {{site.data.keyword.cloud_notm}}。

[{{site.data.keyword.cloud_notm}} 工具箱](create_bmxapp_appenv.html#toolkits)可協助您進行連線。

Cloud Foundry 需要知道用於進行 API 呼叫（例如，當您上傳應用程式時）的 URL。{{site.data.keyword.cloud_notm}} 工具箱使用 '`cf api`' 指令來管理 API 端點。[這裡提供了 ![外部鏈結圖示](../images/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/docs/cli/reference/cfcommands/index.html#cf_api){:new_window} '`cf api`' 指令的相關資訊。

使用下列指令，以告知 Cloud Foundry 要使用的 URL：

```sh
bluemix api https://api.ng.bluemix.net
```
{:pre}

預期結果類似下列輸出：

```
Invoking 'cf api https://api.ng.bluemix.net'...

Setting api endpoint to https://api.ng.bluemix.net...
OK

API endpoint:   https://api.ng.bluemix.net
API version:    2.54.0
Not logged in. Use 'bluemix login' to log in.
```
{:codeblock}

Cloud Foundry 現在知道將 API 呼叫傳送到哪裏，以便管理應用程式。

下一步是登入 {{site.data.keyword.cloud_notm}} 應用程式環境。您必須提供下列帳戶詳細資料：

-   您的使用者名稱（其指定為 '`-u`' 參數）。
-   您的組織名稱（其指定為 '`-o`' 參數）。
-   您的空間（其指定為 '`-s`' 參數）。

>   **附註**：當您透過 Web 瀏覽器登入時，
    {{site.data.keyword.cloud_notm}} 儀表板上會提供帳戶詳細資料，如下列範例所示：<br/>
    ![尋找 {{site.data.keyword.cloud_notm}} 帳戶詳細資料](images/img0035.png)

使用與下列範例類似的指令來登入 {{site.data.keyword.cloud_notm}} 應用程式環境。請注意，系統會要求您輸入您的帳戶密碼。

```sh
bluemix login -u Adrian.Warman@uk.ibm.com -o Adrian.Warman@uk.ibm.com -s dev
```
{:pre}

預期結果類似下列輸出：

```
Invoking 'cf login -u Adrian.Warman@uk.ibm.com -o Adrian.Warman@uk.ibm.com -s dev'...

API endpoint: https://api.ng.bluemix.net

Password> 
Authenticating...
OK

Targeted org Adrian.Warman@uk.ibm.com

Targeted space dev
                
API endpoint:   https://api.ng.bluemix.net (API version: 2.54.0)
User:           adrian.warman@uk.ibm.com
Org:            Adrian.Warman@uk.ibm.com
Space:          dev
```
{:codeblock}

## 上傳應用程式

{{site.data.keyword.cloudant_short_notm}} Foundry 工具箱現在知道如何連接至 {{site.data.keyword.cloud_notm}} 環境。

下一步是上傳應用程式本身。[資訊清單檔](create_bmxapp_appenv.html#manifest)中提供 {{site.data.keyword.cloud_notm}} 應用程式的詳細資料。

已如[這裡](create_bmxapp_createapp.html#essential-files)所述，更新了指導教學應用程式的資訊清單檔。

請使用與下列範例類似的指令來登入，以上傳 {{site.data.keyword.cloud_notm}} 應用程式。

```sh
cf push "Cloudant Python"
```
{:pre}

即會顯示一系列的結果訊息。

```
Using manifest file /..../BMXDemo/manifest.yml

Updating app {{site.data.keyword.cloudant_short_notm}} Python in org Adrian.Warman@uk.ibm.com / space dev as Adrian.Warman@uk.ibm.com...
OK
```
{:codeblock}

Cloud Foundry 工具箱已找到資訊清單檔，並且準備好使用您[稍早](#uploading)提供的連線及識別詳細資料來上傳應用程式。

```
Using route Cloudant-Python.mybluemix.net
Uploading Cloudant Python...
Uploading app files from: /..../BMXDemo
Uploading 1.5K, 3 files
Done uploading               
OK
Binding service {{site.data.keyword.cloudant_short_notm}} Service 2017 to app {{site.data.keyword.cloudant_short_notm}} Python in org Adrian.Warman@uk.ibm.com / space dev as Adrian.Warman@uk.ibm.com...
OK
```
{:codeblock}

已順利上傳應用程式，並與 {{site.data.keyword.cloudant_short_notm}} 資料庫實例進行連線。

```
Starting app {{site.data.keyword.cloudant_short_notm}} Python in org Adrian.Warman@uk.ibm.com / space dev as Adrian.Warman@uk.ibm.com...
-----> Downloaded app package (4.0K)
-----> Downloaded app buildpack cache (29M)
-------> Buildpack version 1.5.5
     $ pip install -r requirements.txt
DEPRECATION: --allow-all-external has been deprecated and will be removed in the future. Due to changes in the repository protocol, it no longer has any effect.
       Collecting cloudant==2.3.1 (from -r requirements.txt (line 1))
         Downloading cloudant-2.3.1-py2-none-any.whl (63kB)
       Collecting requests<3.0.0,>=2.7.0 (from cloudant==2.3.1->-r requirements.txt (line 1))
         Downloading requests-2.12.4-py2.py3-none-any.whl (576kB)
       Installing collected packages: requests, cloudant
       Successfully installed cloudant-2.3.1 requests-2.12.4
You are using pip version 8.1.1, however version 9.0.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
You are using pip version 8.1.1, however version 9.0.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
-----> Uploading droplet (30M)

0 of 1 instances running, 1 starting
1 of 1 instances running

App started


OK

App {{site.data.keyword.cloudant_short_notm}} Python was started using this command `python server.py`
```
{:codeblock}

應用程式會自動啟動。在啟動期間，會透過評估 [requirements.txt 檔案](create_bmxapp_appenv.html#requirements)的內容，進行檢查以確保符合所有需求。應用程式需要存取 {{site.data.keyword.cloudant_short_notm}} 程式庫，這是在建立應用程式時[指定](create_bmxapp_createapp.html#essential-files)。

在您上傳並啟動應用程式之後，會執行一些簡單的系統檢查，確認對於 {{site.data.keyword.cloud_notm}} 而言，應用程式正確地在執行中。

```
Showing health and status for app {{site.data.keyword.cloudant_short_notm}} Python in org Adrian.Warman@uk.ibm.com / space dev as Adrian.Warman@uk.ibm.com...
OK

requested state: started
instances: 1/1
usage: 128M x 1 instances
urls: Cloudant-Python.mybluemix.net
last uploaded: Thu Dec 22 15:58:18 UTC 2016
stack: cflinuxfs2
buildpack: python 1.5.5

     state     since                    cpu    memory          disk           details
#0   running   2016-12-22 03:59:21 PM   0.0%   49.9M of 128M   110.6M of 1G
```
{:codeblock}

## 測試範例應用程式

第一次建立「{{site.data.keyword.cloud_notm}} 應用程式」環境時，儀表板會在`路徑`直欄中包含應用程式的鏈結：<br/>
![顯示應用程式之儀表板的擷取畫面](images/img0017.png)

按一下鏈結會開啟瀏覽器視窗，以向在對應埠上接聽的應用程式要求一些資料。應用程式會傳回應用程式啟動時所產生日誌檔的內容，以作為回應：<br/>
![指導教學應用程式開始執行時所產生的日誌檔](images/img0030.png)

此日誌檔的內容十分有趣。會清楚地顯示開始及結束時間。在這中間，日誌記錄了擷取 {{site.data.keyword.cloudant_short_notm}} 的連線資訊時的所有詳細資料。連線的實際值並不重要。日誌顯示指導教學應用程式能夠找到、擷取並使用這些值，以在 {{site.data.keyword.cloudant_short_notm}} 資料庫中建立新文件。

### 確認資料庫詳細資料

請先開啟「{{site.data.keyword.cloudant_short_notm}} 儀表板」。在 {{site.data.keyword.cloudant_short_notm}} 服務頁面的`管理`標籤上，按一下`啟動`圖示：<br/>
![在 {{site.data.keyword.cloudant_short_notm}} 服務頁面上的「啟動」圖示](images/img0036.png)

若要尋找 {{site.data.keyword.cloudant_short_notm}} 服務頁面，請參閱[建立 {{site.data.keyword.cloudant_short_notm}} 實例指導教學](create_service.html#locating-your-service-credentials)中的詳細資料。
{: tip}

儀表板開啟時，您可以看到應用程式已建立 '`databasedemo`' 資料庫：<br/>
![顯示新資料庫的「{{site.data.keyword.cloudant_short_notm}} 儀表板」](images/img0031.png)

資料庫包含應用程式所建立的單一文件。若要驗證文件是否存在，請按一下儀表板內的資料庫名稱。即會出現資料庫的選項清單。當您選取`所有文件`標籤時，即會出現單一文件的詳細資料：<br/>
![新資料庫內的單一文件](images/img0032.png)

若要查看文件的內容，請按一下顯示為鉛筆影像的`編輯`圖示：<br/>
![文件的詳細資料](images/img0033.png)

文件的內容出現時，您可以查看指導教學應用程式已建立的每一個欄位。<br/>
![文件內的欄位](images/img0034.png)<br/>
特別值得一提的是，`rightNow` 欄位具有建立文件的日期和時間。此值對應於[應用程式日誌檔](#testing-the-sample-application)內已記錄的時間。

## 下一步

指導教學中的下一步是[操作及維護應用程式](create_bmxapp_maintain.html)，例如，當您啟動、停止及除錯應用程式時。

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

# {{site.data.keyword.cloudant_short_notm}} データベースにアクセスする単純な {{site.data.keyword.cloud_notm}} アプリケーションの作成: コード

チュートリアルのこのセクションでは、{{site.data.keyword.cloud}} アプリケーションのコードについて説明します。
{:shortdesc}

<div id="theApp"></div>

## アプリケーションの作成

以下のコンポーネントが揃ったため、アプリケーションの作成を開始できます。

-   [Python プログラミング言語](create_bmxapp_prereq.html#python)。
-   [{{site.data.keyword.cloudant_short_notm}} データベース・インスタンス](create_bmxapp_prereq.html#csi)。
-   [{{site.data.keyword.cloud_notm}} アプリケーション環境](create_bmxapp_appenv.html#creating)。
-   {{site.data.keyword.cloudant_short_notm}} データベース・インスタンスと
    {{site.data.keyword.cloud_notm}} アプリケーション環境間の[接続](create_bmxapp_appenv.html#connecting)。
-   Cloud Foundry ベースの {{site.data.keyword.cloud_notm}} アプリケーションを管理するための [ツールキット](create_bmxapp_appenv.html#toolkits)。
-   初期構成とコード・テンプレートのファイルを含む [「スターター」アプリケーション・パック](create_bmxapp_appenv.html#starter)。

>   **注**: このチュートリアルでは、_効率的な_ Python コードの作成は意図していません。
    仕組みを理解してアプリケーション作成時に参考にするための、単純で分かりやすい実際のコードを示すことを目的としています。
    また、考えられるすべてのチェックおよびエラー条件には対応していません。
    一部の手法を示すためにサンプルのチェックがいくつか組み込まれています。
    実際のアプリケーションでは、すべての警告およびエラー条件をチェックして処理してください。

### 重要なファイル

アプリケーションには、3 つの構成ファイルと 1 つのソース・ファイルが必要です。
これらはすべて、[「スターター」アプリケーション・パック](create_bmxapp_appenv.html#starter)にあります。
 
-   [「`Procfile`」](create_bmxapp_appenv.html#procfile)
-   [「`manifest.yml`」](create_bmxapp_appenv.html#manifest)
-   [「`requirements.txt`」](create_bmxapp_appenv.html#requirements)
-   アプリケーション・ソース・ファイル。チュートリアルのこのセクションで説明します。

構成ファイルを次のように変更します。

1.  「`Procfile`」ファイルを編集して、次のテキストを含めます。
```
    web: python server.py
    ```
    {:codeblock}

2.  「`manifest.yml`」ファイルを編集して、次のテキストを含めます。
```
    applications:
    - path: .
      memory: 128M
      instances: 1
      domain: <ドメイン>
      name: <アプリケーション名>
      host: <アプリケーション・ホスト>
      disk_quota: 1024M
      services:
      - <データベース・インスタンス>
    ```
    {:codeblock}
    >   **注**: 必ず、`「domain」`、`「name」`、`「host」`、および`「services」の値を変更してください。これらは、[{{site.data.keyword.cloud_notm}} アプリケーション環境](create_bmxapp_appenv.html#creating)と [{{site.data.keyword.cloudant_short_notm}} データベース・インスタンス](create_bmxapp_prereq.html#csi)の作成時に入力した値です。

3.  「`requirements.txt`」ファイルを編集して、次のテキストを含めます。
```
    cloudant==2.3.1
    ```
    {:codeblock}

### アプリケーション・コード

次のステップでは、アプリケーション・コードに取り組みます。
各セクションについて説明し、コードを示します。
アプリケーション・コードの[全プログラムの表示](#complete-listing)が、チュートリアルのこのセクションの最後にあります。

#### 始めに

Python アプリケーションには、いくつかの基本的コンポーネントが動作することが必要です。
それらは、次のようにしてインポートされます。

```python
# Make Python modules available.
import os
import json

# It is helpful to have access to tools
# for formatting date and time values.
from time import gmtime, strftime
```
{:codeblock}

このアプリケーションは、単純な Web サーバーとして動作し、1 つのページだけを表示します。
それは、{{site.data.keyword.cloudant_short_notm}} データベース・インスタンスへの接続とデータベース作成の結果が入ったログです。

アプリケーションには、Web ページを提供するためのコンポーネントが必要です。

```python
# Simplify access to basic Python web server tools.
try:
    from SimpleHTTPServer import SimpleHTTPRequestHandler as Handler
    from SocketServer import TCPServer as Server
except ImportError:
    from http.server import SimpleHTTPRequestHandler as Handler
    from http.server import HTTPServer as Server
```
{:codeblock}

>   **注**: このコード・セグメントは、[「スターター」アプリケーション・パック](create_bmxapp_appenv.html#starter)の一部として提供されます。

アプリケーションは、{{site.data.keyword.cloudant_short_notm}} データベース・インスタンスに接続するため、
{{site.data.keyword.cloudant_short_notm}} ライブラリー・コンポーネントをインポートする必要があります。

```python
# Enable the required Python libraries for working with {{site.data.keyword.cloudant_short_notm}}.
from cloudant.client import Cloudant
from cloudant.error import CloudantException
from cloudant.result import Result, ResultByKey
```
{:codeblock}

このアプリケーションでは、{{site.data.keyword.cloudant_short_notm}} データベース・インスタンス内にデータベースを作成します。
以下のようにして、データベースの名前が必要です。

```python
# This is the name of the database we intend to create.
databaseName = "databasedemo"
```
{:codeblock}

アプリケーションでは、{{site.data.keyword.cloudant_short_notm}} データベース・インスタンスに接続してデータベースを作成する際に、進行状況を記録します。
この記録は、ログ・ファイルの形式で、Python Web サーバーからアクセス可能なフォルダー内に保管されます。

フォルダー (このアプリケーションでは名前が「`static`」) を作成し、それにファイルを保管する準備をします。

```python
# Change current directory to avoid exposure of control files
try:
    os.mkdir('static')
except OSError:
    # The directory already exists,
    # no need to create it.
    pass
os.chdir('static')
```
{:codeblock}

次に、単純な HTML ファイルを作成します。
ファイルには、アプリケーションがデータベースを作成する際の、各アクティビティーのログが入ります。

```python
# Begin creating a very simple web page.
filename = "index.html"
target = open(filename, 'w')
target.truncate()
target.write("<html><head><title>{{site.data.keyword.cloudant_short_notm}} Python Demo</title></head><body><p>Log of Cloudant Python steps...</p><pre>")
```
{:codeblock}

ログの最初の部分は、現在日時の記録です。
この記録を利用して、データベースを新しく作成中であることを確認できます。

```python
# Put a clear indication of the current date and time at the top of the page.
target.write("====\n")
target.write(strftime("%Y-%m-%d %H:%M:%S", gmtime()))
target.write("\n====\n\n")
```
{:codeblock}

#### {{site.data.keyword.cloudant_short_notm}} データベース・インスタンスの処理

Python アプリケーションは、{{site.data.keyword.cloud_notm}} アプリケーション環境内で実行されます。
この環境は、接続されたサービスにアプリケーションがアクセスするために必要なすべての情報を提供します。
情報は、環境変数「`VCAP_SERVICES`」内で提供されます。
この変数は、アプリケーションがアクセスして、接続詳細の判別に使用できます。

最初のタスクでは、アプリケーションが {{site.data.keyword.cloud_notm}} アプリケーション環境内で
実行されていることを確認します。
以下のように、「`VCAP_SERVICES`」環境変数の存在をテストしてチェックします。

```python
# Check that we are running in an {{site.data.keyword.cloud_notm}} application environment.
if 'VCAP_SERVICES' in os.environ:
```
{:codeblock}

>   **注**: 次のコード・セクションは、環境変数が見つかった場合にのみ実行されます。
    Python で、以下のコードは、テストの本体であることを示すために、インデントされます。
    このチュートリアルでは、スペースを節約するために、コード・セグメントでインデントは省略されています。
    ただし、[全プログラムの表示](#complete-listing)では、インデントが正しく示されています。

変数が見つかったら、続行してその情報を使用します。
まず、変数内に保管された JSON データをロードして、
新しい「ログ・ファイル」にイベントを記録します。

```python
# Yes we are, so get the service information.
vcap_servicesData = json.loads(os.environ['VCAP_SERVICES'])
# Log the fact that we successfully found some service information.
target.write("Got vcap_servicesData\n")
```
{:codeblock}

次に、接続された {{site.data.keyword.cloudant_short_notm}} データベース・インスタンスに関する情報を探します。
同様に、「ログ・ファイル」にイベントを記録します。

```python
# Look for the {{site.data.keyword.cloudant_short_notm}} service instance.
cloudantNoSQLDBData = vcap_servicesData['cloudantNoSQLDB']
# Log the fact that we successfully found some {{site.data.keyword.cloudant_short_notm}} service information.
target.write("Got cloudantNoSQLDBData\n")
```
{:codeblock}

複数の {{site.data.keyword.cloud_notm}} サービスがアプリケーション環境に接続される場合があります。
各サービスの資格情報は、配列エレメントとしてリストされます。
このチュートリアルでは、
1 つだけの[サービス接続が作成されています](create_bmxapp_appenv.html#connecting)。
そのため、アプリケーションは最初のエレメント (エレメント「ゼロ」) にアクセスします。
各サービス・エレメントには、そのサービスの資格情報が含まれます。
それは、サービスのアクセスに必要な重要フィールドの名前で索引付けされたリストとして表されます。
フィールド名に関する詳細は、単純データベースの作成タスクに関する
[チュートリアル](create_database.html#pre-requisites)にあります。

```python
# Get a list containing the {{site.data.keyword.cloudant_short_notm}} connection information.
credentials = cloudantNoSQLDBData[0]
# Get the essential values for our application to talk to the service.
credentialsData = credentials['credentials']
# Log the fact that we successfully found the {{site.data.keyword.cloudant_short_notm}} values.
target.write("Got credentialsData\n\n")
```
{:codeblock}

次に、リストを調べて、重要な値を取得します。

```python
# Get the username ...
serviceUsername = credentialsData['username']
target.write("Got username: ")
target.write(serviceUsername)
target.write("\n")
# ... the password ...
servicePassword = credentialsData['password']
target.write("Got password: ")
target.write(servicePassword)
target.write("\n")
# ... and the URL of the service within {{site.data.keyword.cloud_notm}}.
serviceURL = credentialsData['url']
target.write("Got URL: ")
target.write(serviceURL)
target.write("\n")
```
{:codeblock}

{{site.data.keyword.cloudant_short_notm}} データベース・インスタンス内にデータベースを作成するために必要な詳細が、アプリケーションにすべて用意されました。
このタスクについては、単純データベースの作成に関する
[チュートリアル](create_database.html#creating-a-database-within-the-service-instance)に詳しい説明があります。

アプリケーションでは、以下のタスクを実行する必要があります。

1.  データベース・インスタンスへの接続を確立します。
2.  [前に](#getting-started)指定された名前でデータベースを作成します。
3.  現在の日時を含む JSON 文書を作成します。
4.  データベースに JSON 文書を保管します。
5.  文書が安全に保管されたことを確認します。
6.  データベース・インスタンスへの接続をクローズします。

これらのタスクのコードは、以下のとおりです。

```python
# We now have all the details we need to work with the {{site.data.keyword.cloudant_short_notm}} service instance.
# Connect to the service instance.
client = Cloudant(serviceUsername, servicePassword, url=serviceURL)
client.connect()
# Create a database within the instance.
myDatabaseDemo = client.create_database(databaseName)
if myDatabaseDemo.exists():
    target.write("'{0}' successfully created.\n".format(databaseName))
    # Create a very simple JSON document with the current date and time.
    jsonDocument = {
        "rightNow": strftime("%Y-%m-%d %H:%M:%S", gmtime())
    }
    # Store the JSON document in the database.
    newDocument = myDatabaseDemo.create_document(jsonDocument)
    if newDocument.exists():
        target.write("Document successfully created.\n")
# All done - disconnect from the service instance.
client.disconnect()
```
{:codeblock}

#### ログ・ファイルのクローズ

次のステップでは、ログ・ファイルを完成させて、
アプリケーション内の単純 Python Web サーバーを使用してそれを提供する準備をします。

```python
# Put another clear indication of the current date and time at the bottom of the page.
target.write("\n====\n")
target.write(strftime("%Y-%m-%d %H:%M:%S", gmtime()))
target.write("\n====\n")
# Finish creating the web page.
target.write("</pre></body></html>")
target.close()
```
{:codeblock}

#### ログ・ファイルの提供

最後のタスクでは、Python アプリケーション内の Web サーバーを開始します。
サーバーの目的は、要求に応じてログ・ファイルを戻すことだけです。
このログ・ファイルによって、Python アプリケーションが以下のタスクを正常に完了したことが確認されます。

1.  {{site.data.keyword.cloud_notm}} アプリケーション環境内で正常に実行されました。
2.  サービス接続の詳細を判別しました。
3.  {{site.data.keyword.cloudant_short_notm}} データベース・インスタンスに接続しました。
4.  データベースを作成しました。
5.  データベース内に文書を作成しました。
6.  要求時にイベントのログで応答しました。

Python Web サーバーを開始するコードは、
[「スターター」アプリケーション・パック](create_bmxapp_appenv.html#starter)の一部として含まれています。

```python
# Start up the simple Python web server application,
# so that it can 'serve' our newly created web page.
PORT = int(os.getenv('PORT', 8000))
httpd = Server(("", PORT), Handler)
try:
  print("Start serving at port %i" % PORT)
  httpd.serve_forever()
except KeyboardInterrupt:
  pass
httpd.server_close()
```
{:codeblock}

## 次のステップ

チュートリアルの次のステップでは、テスト目的で[アプリケーションをアップロードします](create_bmxapp_upload.html)。

## 全プログラムの表示

以下のコードは、{{site.data.keyword.cloud_notm}} 上の {{site.data.keyword.cloudant_short_notm}} サービス・インスタンスにアクセスする完全な Python プログラムです。

```python
# Make Python modules available.
import os
import json

# It is helpful to have access to tools
# for formatting date and time values.
from time import gmtime, strftime

# Simplify access to basic Python web server tools.
try:
    from SimpleHTTPServer import SimpleHTTPRequestHandler as Handler
    from SocketServer import TCPServer as Server
except ImportError:
    from http.server import SimpleHTTPRequestHandler as Handler
    from http.server import HTTPServer as Server

# Enable the required Python libraries for working with {{site.data.keyword.cloudant_short_notm}}.
from cloudant.client import Cloudant
from cloudant.error import CloudantException
from cloudant.result import Result, ResultByKey

# This is the name of the database we intend to create.
databaseName = "databasedemo"

# Change current directory to avoid exposure of control files
try:
    os.mkdir('static')
except OSError:
    # The directory already exists,
    # no need to create it.
    pass
os.chdir('static')

# Begin creating a very simple web page.
filename = "index.html"
target = open(filename, 'w')
target.truncate()
target.write("<html><head><title>Cloudant Python Demo</title></head><body><p>Log of {{site.data.keyword.cloudant_short_notm}} Python steps...</p><pre>")

# Put a clear indication of the current date and time at the top of the page.
target.write("====\n")
target.write(strftime("%Y-%m-%d %H:%M:%S", gmtime()))
target.write("\n====\n\n")

# Start working with the {{site.data.keyword.cloudant_short_notm}} service instance.

# Check that we are running in an {{site.data.keyword.cloud_notm}} application environment.
if 'VCAP_SERVICES' in os.environ:
    # Yes we are, so get the service information.
    vcap_servicesData = json.loads(os.environ['VCAP_SERVICES'])
    # Log the fact that we successfully found some service information.
    target.write("Got vcap_servicesData\n")
    # Look for the {{site.data.keyword.cloudant_short_notm}} service instance.
    cloudantNoSQLDBData = vcap_servicesData['cloudantNoSQLDB']
    # Log the fact that we successfully found some {{site.data.keyword.cloudant_short_notm}} service information.
    target.write("Got cloudantNoSQLDBData\n")
    # Get a list containing the {{site.data.keyword.cloudant_short_notm}} connection information.
    credentials = cloudantNoSQLDBData[0]
    # Get the essential values for our application to talk to the service.
    credentialsData = credentials['credentials']
    # Log the fact that we successfully found the {{site.data.keyword.cloudant_short_notm}} values.
    target.write("Got credentialsData\n\n")
    # Get the username ...
    serviceUsername = credentialsData['username']
    target.write("Got username: ")
    target.write(serviceUsername)
    target.write("\n")
    # ... the password ...
    servicePassword = credentialsData['password']
    target.write("Got password: ")
    target.write(servicePassword)
    target.write("\n")
    # ... and the URL of the service within {{site.data.keyword.cloud_notm}}.
    serviceURL = credentialsData['url']
    target.write("Got URL: ")
    target.write(serviceURL)
    target.write("\n")

    # We now have all the details we need to work with the {{site.data.keyword.cloudant_short_notm}} service instance.
    # Connect to the service instance.
    client = Cloudant(serviceUsername, servicePassword, url=serviceURL)
    client.connect()
    # Create a database within the instance.
    myDatabaseDemo = client.create_database(databaseName)
    if myDatabaseDemo.exists():
        target.write("'{0}' successfully created.\n".format(databaseName))
        # Create a very simple JSON document with the current date and time.
        jsonDocument = {
            "rightNow": strftime("%Y-%m-%d %H:%M:%S", gmtime())
        }
        # Store the JSON document in the database.
        newDocument = myDatabaseDemo.create_document(jsonDocument)
        if newDocument.exists():
            target.write("Document successfully created.\n")
    # All done - disconnect from the service instance.
    client.disconnect()

# Put another clear indication of the current date and time at the bottom of the page.
target.write("\n====\n")
target.write(strftime("%Y-%m-%d %H:%M:%S", gmtime()))
target.write("\n====\n")
# Finish creating the web page.
target.write("</pre></body></html>")
target.close()

# Start up the simple Python web server application,
# so that it can 'serve' our newly created web page.
PORT = int(os.getenv('PORT', 8000))
httpd = Server(("", PORT), Handler)
try:
  print("Start serving at port %i" % PORT)
  httpd.serve_forever()
except KeyboardInterrupt:
  pass
httpd.server_close()
```
{:codeblock}

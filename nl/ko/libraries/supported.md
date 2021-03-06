---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

<!-- Acrolinx: 2017-03-06 -->

# 지원되는 클라이언트 라이브러리

## Mobile

{{site.data.keyword.cloudantfull}} Sync 라이브러리는 모바일 디바이스에서 로컬 JSON 데이터를 저장하고, 인덱싱하고 조회하는 데 사용됩니다.
이는 여러 디바이스 간에 데이터를 동기화하는 경우에도 사용됩니다.
동기화는 사용자의 애플리케이션에 의해 제어됩니다.
또한
라이브러리는 로컬 디바이스 및 원격 데이터베이스 둘 다에서 충돌을 찾고
해결하는 헬퍼 메소드를 제공합니다.

두 가지 버전이 사용 가능합니다.

-   [{{site.data.keyword.cloudant_short_notm}} Sync - Android / JavaSE ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant/sync-android){:new_window}
-   [{{site.data.keyword.cloudant_short_notm}} Sync - iOS(CDTDatastore) ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant/CDTDatastore){:new_window}

{{site.data.keyword.cloudant_short_notm}} Sync에 대한 개요는 [여기 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://cloudant.com/product/cloudant-features/sync/){:new_window}에 있습니다.
{{site.data.keyword.cloudant_short_notm}} Sync 리소스에 대한 세부사항은 [여기 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://cloudant.com/cloudant-sync-resources/){:new_window}에 있습니다.

## Java

[java-cloudant ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant/java-cloudant){:new_window}는
Java용 공식 {{site.data.keyword.cloudantfull}} 라이브러리입니다.

라이브러리를 Maven 또는 Gradle 빌드에 종속 항목으로 추가하여 설치하는 방법에 대한 정보는
[여기 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant/java-cloudant#installation-and-usage){:new_window}에 있으며,
여기에는 해당 라이브러리를 사용하는 방법에 대한 세부사항 및 예가 함께 제공되어 있습니다.

### Java용 라이브러리 및 프레임워크

#### 지원되는 Java용 라이브러리

-   [java-cloudant ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant/java-cloudant){:new_window}

#### 지원되지 않는 Java용 라이브러리

-   [ektorp ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://helun.github.io/Ektorp/reference_documentation.html){:new_window}
-   [jcouchdb ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](http://code.google.com/p/jcouchdb/){:new_window}
-   [jrelax ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/isterin/jrelax){:new_window}
-   [LightCouch ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](http://www.lightcouch.org/){:new_window}
-   {{site.data.keyword.cloud}}용 [Java Cloudant Web Starter ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://ace.ng.bluemix.net/#/store/cloudOEPaneId=store&appTemplateGuid=CloudantJavaBPTemplate&fromCatalog=true){:new_window} 표준 유형

### Java용 예제 및 튜토리얼

-   [HTTP 및 JSON 라이브러리를 사용한 작성, 읽기, 업데이트 및 삭제 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant/haengematte/tree/master/java){:new_window}
-   [ektorp 라이브러리를 사용한 작성, 읽기, 업데이트 및 삭제 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant/haengematte/tree/master/java/CrudWithEktorp){:new_window}
-   [Java와 {{site.data.keyword.cloud}}의 {{site.data.keyword.cloudant_short_notm}}를 사용한 앱 빌드 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://cloudant.com/blog/building-apps-using-java-with-cloudant-on-ibm-bluemix/){:new_window}
-   [Liberty, {{site.data.keyword.cloudant_short_notm}} 및 싱글 사인온을 사용한 게임 앱 빌드 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/developerworks/cloud/library/cl-multiservicegame-app/index.html?ca=drs-){:new_window} {{site.data.keyword.cloud_notm}} 예제
-   [Watson 및 {{site.data.keyword.cloudant_short_notm}}를 사용하여 {{site.data.keyword.cloud_notm}}에 Java EE 앱 빌드 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/bluemix/2014/10/17/building-java-ee-app-ibm-bluemix-using-watson-cloudant/){:new_window} {{site.data.keyword.cloud_notm}} 예제와 [YouTube 동영상 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://www.youtube.com/watch?feature=youtu.be&v=9AFMY6m0LIU&app=desktop){:new_window}


## Node.js

[nodejs-cloudant ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant/nodejs-cloudant){:new_window}는
Node.js용 공식 {{site.data.keyword.cloudant_short_notm}} 라이브러리입니다.
npm을 사용하여 이를 설치할 수 있습니다.

```sh
npm install cloudant
```
{:codeblock}

### node.js용 라이브러리 및 프레임워크

#### 지원되는 node.js용 라이브러리

-   [nodejs-cloudant ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant/nodejs-cloudant){:new_window}([npm ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://www.npmjs.org/package/cloudant){:new_window})

#### 지원되지 않는 node.js용 라이브러리 및 프레임워크

-   브라우저에서도 작동하는 [sag-js ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/sbisbee/sag-js){:new_window}.
    세부사항은 [saggingcouch ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/sbisbee/saggingcouch.com){:new_window}를 참조하십시오.
-   [nano ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/dscape/nano){:new_window}는 최소한의 구현입니다.
-   [restler ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/danwrong/restler){:new_window}는 성능이 가장 좋지만 핵심 기능만을 포함하고 있습니다.
-   [cradle ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/flatiron/cradle){:new_window}은
    성능 저하를 감수하더라도 사용 용이성을 높여야 하는 경우에도 사용할 수 있는 상위 레벨 클라이언트입니다.
-   [cane_passport ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ddemichele/cane_passport){:new_window} - 부트스트랩을 사용하는 {{site.data.keyword.cloudant_short_notm}} Angular Node Express
-   [express-cloudant ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant-labs/express-cloudant){:new_window} - PouchDB 및 Grunt 또한 사용하는, Node.js Express 프레임워크의 템플리트
-   [Node.js {{site.data.keyword.cloudant_short_notm}} DB Web Starter ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://ace.ng.bluemix.net/#/store/cloudOEPaneId=store&appTemplateGuid=nodejscloudantbp&fromCatalog=true){:new_window} - {{site.data.keyword.cloud_notm}}의 표준 유형
-   [Mobile Cloud ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://ace.ng.bluemix.net/#/store/cloudOEPaneId=store&appTemplateGuid=mobileBackendStarter&fromCatalog=true){:new_window} - {{site.data.keyword.cloud_notm}}의 표준 유형(Node.js, 보안, 푸시 및 모바일 데이터/{{site.data.keyword.cloudant_short_notm}})

### node.js용 예제 및 튜토리얼

-   [작성, 읽기, 업데이트 및 삭제 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant/haengematte/tree/master/nodejs){:new_window}
-   [Cloudant-Uploader ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/garbados/Cloudant-Uploader){:new_window} - `.csv` 파일을 {{site.data.keyword.cloudant_short_notm}}에 업로드하는 유틸리티입니다.
-   [couchimport ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/glynnbird/couchimport){:new_window} - `.csv` 또는 `.tsv` 파일을 CouchDB 또는 {{site.data.keyword.cloudant_short_notm}}로 가져오는 유틸리티입니다.
-   [{{site.data.keyword.cloud_notm}} 및 Node.js 시작하기 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](http://thoughtsoncloud.com/2014/07/getting-started-ibm-bluemix-node-js/){:new_window}
-   [{{site.data.keyword.cloud_notm}}, {{site.data.keyword.cloudant_short_notm}} 및 Node.js의 클라우드 모임 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://gigadom.wordpress.com/2014/08/15/a-cloud-medley-with-ibm-bluemix-cloudant-db-and-node-js/){:new_window}
-   [{{site.data.keyword.cloud_notm}}의 {{site.data.keyword.cloudant_short_notm}}를 사용한 간단한 단어 게임 앱 빌드 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/developerworks/cloud/library/cl-guesstheword-app/index.html?ca=drs-){:new_window} - Node.js를 사용합니다. 
-   [실시간 SMS 투표 앱 빌드 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html){:new_window} - Node.js, Twilio 및 {{site.data.keyword.cloudant_short_notm}}를 사용하는, 여섯 부분으로 구성된 튜토리얼입니다.
-   [다중 계층 Windows Azure 웹 애플리케이션 빌드 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://www.ampower.me/article/CouchDB/Tutorial-Building-a-Multi-Tier-Windows-Azure-Web-application-use-Cloudants-Couchdb-as-a-Service-node-94-409665?eqs=Z2NWNlltTmlUWStWcHdEWENWc3UxdmowREpiMjlGUVpKajJOZGJpSlVkemlPS2oxa0YxZE5BPT0=){:new_window} - {{site.data.keyword.cloudant_short_notm}}, Node.js, CORS 및 Grunt를 사용합니다.
-   [직접 해보기: {{site.data.keyword.cloud_notm}}, {{site.data.keyword.cloudant_short_notm}} 및 Raspberry Pi를 사용한 원격 감시 앱 빌드 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/developerworks/library/ba-remoteservpi-app/index.html){:new_window}

## Python

Python을 사용하여 {{site.data.keyword.cloudant_short_notm}} 관련 작업을 수행하는 데 지원되는 라이브러리는
[여기 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant/python-cloudant){:new_window}에 있습니다.

>   **참고:** {{site.data.keyword.cloudant_short_notm}}에 액세스하는 Python 애플리케이션에는 컴포넌트 종속성이 있습니다. 이러한 종속성은 `requirements.txt` 파일에 지정되어야 합니다. 자세한 정보는 [여기 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://pip.readthedocs.io/en/1.1/requirements.html){:new_window}를 참조하십시오.

현재 라이브러리 릴리스는 [여기 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://pypi.python.org/pypi/cloudant/){:new_window}에서 다운로드하십시오.
[python.org ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://www.python.org/about/){:new_window}에서 Python 언어에 대한 자세한 정보를 알아보십시오. 

## Swift

{{site.data.keyword.cloudant_short_notm}} 관련 작업을 수행하는 데 필요한 지원되는 라이브러리가 있습니다.
이 라이브러리의 이름은 SwiftCloudant이며 `cocoapods`를 사용하여 설치됩니다.

podfile 항목은 다음과 같습니다.

```sh
pod 'SwiftCloudant'
```
{:codeblock}

설치 세부사항과 {{site.data.keyword.cloudant_short_notm}}에서 원격 JSON 데이터를 저장하고, 인덱싱하고 조회하는 방법을 포함한, SwiftCloudant에 대한 자세한 정보는
[여기 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudant/swift-cloudant){:new_window}를 참조하십시오.

라이브러리는 초기 릴리스 버전입니다.
따라서 현재 전체 {{site.data.keyword.cloudant_short_notm}} API 범위를 포함하지는 않습니다. 

>   **참고**: SwiftCloudant는 iOS에서 지원되지 않으며 Objective-C로부터 호출할 수 없습니다.

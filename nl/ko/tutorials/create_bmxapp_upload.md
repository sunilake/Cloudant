---

copyright:
  years: 2017
lastupdated: "2017-01-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2017-01-11 -->

# Cloudant 데이터베이스에 액세스하기 위한 간단한 Bluemix 애플리케이션 작성: 애플리케이션 업로드

이 튜토리얼 섹션에서는 {{site.data.keyword.Bluemix}} 애플리케이션을 업로드하는 방법을 설명합니다.
{:shortdesc}

<div id="uploading"></div>

## Bluemix에 연결

첫 번째 태스크는 {{site.data.keyword.Bluemix_notm}}에 연결하는 것입니다. 

[{{site.data.keyword.Bluemix_notm}} 툴킷](create_bmxapp_appenv.html#toolkits)은 연결하는 데 도움을 줍니다. 

Cloud Foundry는 애플리케이션을 업로드할 때와 같은 경우에서 API 호출에 사용할 URL을 알고 있어야 합니다.
{{site.data.keyword.Bluemix_notm}} 툴킷은 '`cf api`' 명령을 사용하여 API 엔드포인트를 관리합니다.
'`cf api`' 명령에 대한 자세한 정보는 [여기 ![외부 링크 아이콘](../images/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/docs/cli/reference/cfcommands/index.html#cf_api){:new_window}에 있습니다. 

다음 명령을 사용하여 Cloud Foundry에 사용할 URL을 전달하십시오. 

```sh
bluemix api https://api.ng.bluemix.net
```
{:pre}

다음 출력과 유사한 결과가 표시됩니다. 

```
Invoking 'cf api https://api.ng.bluemix.net'...

Setting api endpoint to https://api.ng.bluemix.net...
OK

API endpoint:   https://api.ng.bluemix.net
API version:    2.54.0
Not logged in. Use 'bluemix login' to log in.
```
{:codeblock}

이제 Cloud Foundry에서 애플리케이션 관리를 위한 API 호출을 전송할 위치를 파악했습니다. 

다음 단계는 {{site.data.keyword.Bluemix_notm}} 애플리케이션 환경에 로그인하는 것입니다. 사용자는 다음 계정 세부사항을 제공해야 합니다. 

-   '`-u`' 매개변수로 지정되는 사용자 이름
-   '`-o`' 매개변수로 지정되는 조직 이름
-   '`-s`' 매개변수로 지정되는 영역 이름

>   **참고**: 계정 세부사항은 {{site.data.keyword.Bluemix_notm}} 대시보드에 있으며,
    이는 웹 브라우저를 통해 로그인한 경우 다음 예에 표시된 것과 같습니다. <br/>
    ![{{site.data.keyword.Bluemix_notm}} 계정 세부사항 찾기](images/img0035.png)

다음 예와 유사한 명령을 사용하여 {{site.data.keyword.Bluemix_notm}} 애플리케이션 환경에 로그인하십시오. 사용자는 계정 비밀번호를 입력하라는 요구를 받습니다. 

```sh
bluemix login -u Adrian.Warman@uk.ibm.com -o Adrian.Warman@uk.ibm.com -s dev
```
{:pre}

다음 출력과 유사한 결과가 표시됩니다. 

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

## 애플리케이션 업로드

이제 Cloudant Foundry 툴킷은 {{site.data.keyword.Bluemix_notm}} 환경에 연결하는 방법을 알고 있습니다. 

다음 단계는 애플리케이션 자체를 업로드하는 것입니다. {{site.data.keyword.Bluemix_notm}} 애플리케이션의 세부사항은 [Manifest 파일](create_bmxapp_appenv.html#manifest)에서 제공됩니다. 

튜토리얼 애플리케이션의 Manifest 파일은 [여기](create_bmxapp_createapp.html#essential-files)에 설명되어 있는 바와 같이 업데이트되었습니다. 

다음 예와 유사한 명령을 사용하여, {{site.data.keyword.Bluemix_notm}} 애플리케이션을 업로드하기 위해 로그인하십시오. 

```sh
cf push "Cloudant Python"
```
{:pre}

일련의 결과 메시지가 표시됩니다. 

```
Using manifest file /..../BMXDemo/manifest.yml

Updating app Cloudant Python in org Adrian.Warman@uk.ibm.com / space dev as Adrian.Warman@uk.ibm.com...
OK
```
{:codeblock}

Cloud Foundry 툴킷이 Manifest 파일을 찾고, [이전](#uploading)에 제공된 연결 및 식별 세부사항을 사용하여 애플리케이션 업로드를 준비합니다. 

```
Using route Cloudant-Python.mybluemix.net
Uploading Cloudant Python...
Uploading app files from: /..../BMXDemo
Uploading 1.5K, 3 files
Done uploading               
OK
Binding service Cloudant Service 2017 to app Cloudant Python in org Adrian.Warman@uk.ibm.com / space dev as Adrian.Warman@uk.ibm.com...
OK
```
{:codeblock}

애플리케이션이 업로드되며 {{site.data.keyword.cloudant_short_notm}} 데이터베이스 인스턴스에 연결됩니다. 

```
Starting app Cloudant Python in org Adrian.Warman@uk.ibm.com / space dev as Adrian.Warman@uk.ibm.com...
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

App Cloudant Python was started using this command `python server.py`
```
{:codeblock}

애플리케이션이 자동으로 시작됩니다. 시작의 일부로서,
[requirements.txt 파일](create_bmxapp_appenv.html#requirements)의
컨텐츠를 평가하여 모든 요구사항을 만족하는지 확인하는 검사가 수행됩니다.
애플리케이션은 작성 시에 [지정](create_bmxapp_createapp.html#essential-files)된
{{site.data.keyword.cloudant_short_notm}} 라이브러리에 대한 액세스를 필요로 합니다. 

애플리케이션을 업로드한 후 시작하고 나면 {{site.data.keyword.Bluemix_notm}}의 관점에서
애플리케이션이 올바르게 실행되고 있는지 확인하기 위한 몇 가지 간단한 검사가 실행됩니다. 

```
Showing health and status for app Cloudant Python in org Adrian.Warman@uk.ibm.com / space dev as Adrian.Warman@uk.ibm.com...
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

## 샘플 애플리케이션 테스트

{{site.data.keyword.Bluemix_notm}} 애플리케이션 환경이 처음으로 작성될 때, 대시보드에는 애플리케이션의 `Route` 열에 대한 링크가 포함되었습니다. <br/>
![애플리케이션의 대시보드를 보여주는 스크린샷](images/img0017.png)

이 링크를 클릭하면 해당 포트를 청취하고 있는 애플리케이션으로부터 몇 가지 데이터를 요구하는 브라우저 창이 열립니다.
애플리케이션은 시작 시에 생성된 로그 파일의 컨텐츠를 리턴하여 응답합니다. <br/>
![튜토리얼 애플리케이션 실행 시작 시에 생성된 로그 파일](images/img0030.png)

이 로그 파일의 컨텐츠는 흥미롭습니다. 시작 및 종료 시간이 분명히 표시되어 있습니다.
그 사이의 로그에는 {{site.data.keyword.cloudant_short_notm}}의 연결 정보 검색에 대한
각 세부사항이 기록되어 있습니다. 연결의 실제 값은 중요하지 않습니다.
이 로그는 튜토리얼 애플리케이션이 {{site.data.keyword.cloudant_short_notm}} 데이터베이스에
새 문서를 작성하기 위해 이러한 값을 찾고, 검색하고, 사용할 수 있었음을 보여줍니다. 

### 데이터베이스 세부사항 확인

{{site.data.keyword.cloudant_short_notm}} 대시보드를 열어 시작하십시오.
{{site.data.keyword.cloudant_short_notm}} 서비스 페이지의 `Manage` 탭에 있는
`Launch` 아이콘을 클릭하십시오. <br/>
![{{site.data.keyword.cloudant_short_notm}} 서비스 페이지의 Launch 아이콘](images/img0036.png)

> **참고**: {{site.data.keyword.cloudant_short_notm}} 서비스 페이지를 찾으려면
  ['{{site.data.keyword.cloudant_short_notm}} 인스턴스 작성' 튜토리얼](create_service.html#locating-your-service-credentials)에 있는 세부사항을 참조하십시오. 

대시보드가 열리면 '`databasedemo`' 데이터베이스를 작성한 애플리케이션을 볼 수 있습니다. <br/>
![새 데이터베이스를 표시하고 있는 {{site.data.keyword.cloudant_short_notm}} 대시보드](images/img0031.png)

이 데이터베이스에는 애플리케이션이 작성한 하나의 문서가 포함되어 있습니다.
문서의 유무를 확인하려면 대시보드 내의 데이터베이스 이름을 클릭하십시오.
데이터베이스에 대한 옵션 목록이 표시됩니다. `All documents` 탭을
선택하면 하나의 문서에 대한 세부사항이 표시됩니다. <br/>
![새 데이터베이스에 있는 하나의 문서](images/img0032.png)

이 문서의 컨텐츠를 보려면 연필의 이미지로 표시된 `Edit` 아이콘을 클릭하십시오. <br/>
![문서의 세부사항](images/img0033.png)

문서의 컨텐츠가 표시되면 튜토리얼 애플리케이션에 의해 작성된 각 필드를 볼 수 있습니다. <br/>
![문서 내의 필드](images/img0034.png)<br/>
특히, `rightNow` 필드에는 문서가 작성된 날짜 및 시간이 있습니다.
이 값은 [애플리케이션 로그 파일](#testing-the-sample-application)에
기록된 시간에 해당합니다. 

## 다음 단계

튜토리얼의 다음 단계는 애플리케이션을 시작하거나, 중지하거나, 디버그하는 것과 같은
[애플리케이션 운영 및 유지보수](create_bmxapp_maintain.html)입니다. 

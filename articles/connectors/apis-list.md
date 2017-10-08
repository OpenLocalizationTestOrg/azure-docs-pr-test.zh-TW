---
title: "Azure 邏輯應用程式的 aaaConnectors |Microsoft 文件"
description: "從所有 hello 可用的 Microsoft 管理連接器 toobuild 選擇和建立邏輯應用程式"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f1f1fd50-b7f9-4d13-824a-39678619aa7a
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: mandia; ladocs
ms.openlocfilehash: d681d13d642e6e1512d1f8ab0e1078a194b5da83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connectors-list"></a>連接器清單
> [!TIP]
> hello [A 到 Z 的完整清單](#az)（在本主題） 會列出所有您可以使用邏輯應用程式中的 hello 可用連接器。 [連接器詳細資料](/connectors/)列出的任何觸發程序和動作中 hello swagger 定義，也會列出每個連接器的任何限制。

連接器是建立邏輯應用程式時不可或缺的部分。 使用這些連接器，可以真正展開內部和雲端應用程式 toodo 不同的項目與您建立、 資料和您已經有的資料。 hello 連接器可提供下列分類的 hello: 

* **標準連接器**︰當您使用邏輯應用程式時自動取得和納入。 例如：服務匯流排、Power BI、Oracle Database、OneDrive 等等。

* **整合帳戶連接器**︰當您購買整合帳戶時取得。 使用這些連接器，您可以轉換和驗證 XML、透過 AS2 / X12 / EDIFACT 處理企業對企業訊息，以及進行一般檔案的編碼和解碼。 如果您使用 BizTalk Server 時，這些連接器通常會以適合 tooexpand BizTalk 流程至 Azure。  

    BizTalk Server 也有[Logic Apps 配接器](https://msdn.microsoft.com/library/mt787163.aspx)包含從邏輯應用程式中，接收和傳送 tooa 邏輯應用程式。

* **企業連接器**︰包含 MQ 和 SAP。 需要支付額外費用。 

[邏輯應用程式定價](https://azure.microsoft.com/pricing/details/logic-apps/)和[定價模型](../logic-apps/logic-apps-pricing.md)hello 成本上提供更多詳細資料。 

## <a name="popular-connectors"></a>熱門的連接器
有數千個應用程式和數百萬次執行作業使用這些連接器，成功處理資料和資訊。 hello 下表列出最常用的 hello 和與使用者某些 [我的最愛]:

| |  |  |  |
| --- | --- | --- | --- |
| [![API 圖示][AzureBlobStorageicon]<br/>**Azure Blob<br/>儲存體**][AzureBlobStoragedoc] | 如果您想要 tooautomate 任何工作與您的儲存體帳戶，然後您應該查看此連接器。 支援 CRUD (建立、讀取、更新、刪除) 作業。 | [![API 圖示][Azure-Functionsicon]<br/>**Azure Functions**][azure-functionsdoc] | 建立可執行 C# 或 node.js 之自訂程式碼片段的函式，然後在邏輯應用程式中使用這些函式。  |
| [![API 圖示][Dynamics-365icon]<br/>**Dynamics 365<br/>CRM Online**][Dynamics-365doc] | 其中一個 hello 大部分要求的連接器。 它有觸發程序和動作 toohelp 將與潛在客戶和多個工作流程自動化。 | [![API 圖示][Event-Hubs-icon]<br/>**事件中樞**][event-hubs-doc] | 在事件中樞上取用和發佈事件。 比方說，您可以從您使用事件中心的邏輯應用程式取得輸出，並再傳送嗨輸出 tooa 即時分析提供者。 |
| [![API 圖示][FTPicon]<br/>**FTP**][FTPdoc] | 如果您的 FTP 伺服器從存取 hello 網際網路，則您可以將自動化工作流程 toowork 檔案和資料夾。 <br/><br/>SFTP 也會提供與 hello SFTP 連接器的。 | [![API 圖示][HTTPicon]<br/>**HTTP**][httpdoc] | 透過 HTTP 與任何端點使用邏輯應用程式 toocommunicate。 |
| [![API 圖示][Office-365-Outlookicon]<br/>**Office 365<br/>Outlook**][office365-outlookdoc] | 許多觸發程序，並更多動作 toouse Office 365 電子郵件和工作流程內的事件。 <br/><br/>此連接器包含*核准電子郵件*動作 tooapprove 休假要求的經費支出報表，和等等。 <br/><br/>Office 365 使用者皆可與 hello Office 365 使用者連接器。| [![API 圖示][HTTP-Requesticon]<br/>**要求 / 回應**][HTTP-Requestdoc] | 此連接器會提供 HTTPS URL。 當 hello 邏輯應用程式收到要求 toothis URL 時，會啟動 hello 邏輯應用程式。 |
| [![API 圖示][Salesforceicon]<br/>**Salesforce**][salesforcedoc] | 輕鬆地使用您 Salesforce 帳戶 tooget 存取 tooobjects，例如潛在客戶，以及其他更多登入。 |  [![API 圖示][Service-Busicon]<br/>**服務匯流排**][Service-Busdoc] | hello 邏輯應用程式內的熱門連接器，其中包括觸發程序和動作 toodo 非同步傳訊和佇列、 訂閱和主題與發佈/訂閱。 |
|  [![API 圖示][SharePointicon]<br/>**SharePoint<br/>Online**][SharePointdoc] | 如果您使用 SharePoint 執行任何動作，並且受惠於自動化作業，我們建議看看此連接器。 可以搭配內部部署 SharePoint 和 SharePoint Online 使用 | [![API 圖示][SQL-Servericon]<br/>**SQL Server**][SQL-Serverdoc] | Hello 的其中一個最常使用連接器，它可以連接 tooan 在內部部署 SQL Server 及 Azure SQL Database。 | 
| [![API 圖示][Twittericon]<br/>**Twitter**][Twitterdoc] | 使用 Twitter 帳戶輕鬆登入，然後在新推文發佈時啟動工作流程。 然後，儲存這些推文 tooa SQL 資料庫或 SharePoint 清單。 | | | 

## <a name="integration-account-connectors"></a>整合帳戶連接器 

hello 企業整合組件 (EIP) 包含已知 toohello BizTalk Server 社群的接點。 當您購買[整合帳戶](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)，您也可以取得下列連接器的 hello: 

|  |  |  |  |
| --- | --- | --- | --- |
| [![API 圖示][as2icon]<br/>**AS2</br> 解碼**][as2decode] | [![API 圖示][as2icon]<br/>**AS2</br> 編碼**][as2encode] | [![API 圖示][x12icon]<br/>**EDIFACT</br> 解碼**][EDIFACTdecode] | [![API 圖示][x12icon]<br/>**EDIFACT</br> 編碼**][EDIFACTencode] |
[![API 圖示][flatfileicon]<br/>**一般檔案</br> 編碼**][flatfiledoc] | [![API 圖示][flatfiledecodeicon]<br/>**一般檔案</br> 解碼**][flatfiledecodedoc] | [![API 圖示][integrationaccounticon]<br/>**整合<br/>帳戶**][integrationaccountdoc] | [![API 圖示][xmltransformicon]<br/>**轉換<br/>XML**][xmltransformdoc] |
| [![API 圖示][x12icon]<br/>**X12</br> 解碼**][x12decode] | [![API 圖示][x12icon]<br/>**X12</br> 編碼**][x12encode] | [![API 圖示][xmlvalidateicon]<br/>**XML <br/>驗證**][xmlvalidatedoc] | |

## <a name="enterprise-connectors"></a>企業連接器

在您的 logic apps tooyour 企業應用程式連接。

|  |  |
| --- | --- |
|[![API 圖示][MQicon]<br/>**MQ**][mqdoc]|[![API 圖示][SAPicon]<br/>**SAP**][sapconnector]|


## <a name="az"></a>A-Z 完整清單

[連接器詳細資料](/connectors/)列出任何觸發程序和動作中 hello swagger 定義，也會列出每個連接器的任何限制。

| | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [**1**](#1) | [**A**](#a) | [**B**](#b) | [**C**](#c) | [**D**](#d) | [**E**](#e) | [**F**](#f) | [**G**](#g) | [**H**](#h) | [**I**](#i) | [**J**](#j) | [**L**](#l) | [**M**](#m) |
| [**N**](#n) | [**O**](#o) | [**P**](#p) | [**R**](#r) | [**S**](#s) | [**T**](#t) | [**U**](#u) | [**V**](#v) | [**W**](#w) | [**X**](#x) | [**Y**](#y) | [**Z**](#z) | | 

| | |
|---|---|
|<a name="1"></a>10to8 Appointment Scheduling<br/><br/><a name="a"></a>Act!<br/>Adobe Creative Cloud<br/>appFigures<br/>[AS2][as2doc]<br/>Asana<br/>Azure Active Directory (AD)<br/>Azure API 管理<br/>Azure App Service<br/>Azure 應用程式<br/>Azure 自動化<br/>[Azure Blob 儲存體][azureblobstoragedoc]<br/>Azure Data Lake<br/>Azure DocumentDB (Cosmos DB)<br/>[Azure Functions][azure-functionsdoc]<br/>[Azure Logic Apps][nested-logic-appdoc]<br/>AzureML<br/>Azure 佇列<br/>Azure Resource Manager<br/>[Azure SQL Database][sql-serverdoc]<br/><br/><a name="b"></a>Basecamp 2<br/>Basecamp 3<br/>批次<br/>Benchmark Email<br/>Bing 搜尋<br/>Bitbucket<br/>Bitly<br/>BizTalk Server<br/>Blogger<br/>Box<br/>Buffer<br/><br/><a name="c"></a>Calendly<br/>Campfire<br/>Capsule CRM<br/>Chatter<br/>Cognito Forms<br/>辨識服務電腦視覺 API<br/>辨識服務臉部 API<br/>辨識服務 LUIS<br/>辨識服務文字分析<br/>Common Data Service<br/>內容轉換<br/>Control-Terminate<br/>[自訂 API / Web 應用程式][api/web-appdoc]<br/><br/><a name="d"></a>Data Operations<br/>[DB2][db2doc]<br/>Disqus<br/>DocuSign<br/>Do Until<br/>Dropbox<br/>[Dynamics 365 CRM Online][Dynamics-365doc]<br/>Dynamics 365 for Financials<br/>Dynamics 365 for Operations<br/>Dynamics NAV<br/><br/><a name="e"></a>Easy Redmine<br/>EDIFACT<br/>[事件中樞][event-hubs-doc]<br/>Eventbrite<br/><br/><a name="f"></a>Facebook<br/>[檔案系統][filesystemdoc]<br/>[一般檔案][flatfiledoc]<br/>FreshBooks<br/>Freshdesk!<br/>FreshService<br/>[FTP][ftpdoc]<br/><br/><a name="g"></a>GitHub<br/>Gmail<br/>Google 行事曆<br/>Google 聯絡人<br/>Google 雲端硬碟<br/>Google 試算表<br/>Google 工作表<br/>GoToMeeting<br/>GoToTraining<br/>GoToWebinar<br/><br/><a name="h"></a>Harvest<br/>HelloSign<br/>HipChat<br/>[HTTP][httpdoc]<br/>[HTTP + Swagger][http-swaggerdoc]<br/>[HTTP Webhook][webhookdoc]<br/><br/><a name="i"></a>[Informix][informixdoc]<br/>Infusionsoft<br/>Inoreader<br/>Insightly<br/>Instagram<br/>Instapaper<br/>整合帳戶<br/>Intercom | <a name="j"></a>JotForm<br/>JIRA<br/><br/><a name="l"></a>LeanKit<br/>LiveChat<br/><br/><a name="m"></a>MailChimp<br/>Mandrill<br/>中型<br/>Microsoft Forms<br/>Microsoft Teams<br/>Microsoft Translator<br/>[MQ][mqdoc]<br/>MSN 天氣<br/>Muhimbi PDF<br/>MySQL<br/><br/><a name="n"></a>Nexmo<br/><br/><a name="o"></a>[Office 365 Outlook][office365-outlookdoc]<br/>Office 365 使用者<br/>Office 365 影片<br/>OneDrive<br/>OneDrive for Business<br/>OneNote (Business)<br/>[Oracle Database][oracle-db-doc]<br/>Outlook Customer Manager<br/>Outlook 工作<br/>Outlook.com<br/><br/><a name="p"></a>PagerDuty<br/>Parserr<br/>Paylocity<br/>Pinterest<br/>Pipedrive<br/>Pivotal Tracker<br/>Planner<br/>PostgreSQL<br/>Power BI<br/>Project Online<br/><br/><a name="r"></a>Redmine<br/>[要求 / 回應][http-requestdoc]<br/>RSS<br/><br/><a name="s"></a>[Salesforce][salesforcedoc]<br/>[SAP 應用程式伺服器][sapconnector]<br/>[SAP 訊息伺服器][sapconnector]<br/>[排程][recurrencedoc]<br/>Scope<br/>SendGrid<br/>傳送訊息 toobatch<br/>[服務匯流排][service-busdoc]<br/>SFTP<br/>[SharePoint Online][sharepointdoc]<br/>[SharePoint Server][sharepointserver]<br/>Slack<br/>Smartsheet<br/>SMTP<br/>SparkPost<br/>[SQL Server][sql-serverdoc]<br/>等量磁碟區<br/>SurveyMonkey<br/>切換大小寫<br/><br/><a name="t"></a>Teamwork 專案<br/>Teradata<br/>Todoist<br/>Toodledo<br/>[轉換 XML][xmltransformdoc]<br/>Trello<br/>Twilio<br/>[Twitter][twitterdoc]<br/>Typeform<br/><br/><a name="u"></a>UserVoice<br/><br/><a name="v"></a>變數<br/>Vimeo<br/>Visual Studio Team Services<br/><br/><a name="w"></a>WebMerge<br/>WordPress<br/>Wunderlist<br/><br/><a name="x"></a>[X12][x12doc]<br/>[XML 驗證][xmlvalidatedoc]<br/><br/><a name="y"></a>Yammer<br/>YouTube<br/><br/><a name="z"></a>Zendesk |

> [!TIP]
> tooget 之前註冊 Azure 帳戶，使用 Azure 邏輯應用程式啟動太移[再試一次 Logic Apps](https://tryappservice.azure.com/?appservice=logic)。 您可以立即建立短期的入門邏輯應用程式。 不需要信用卡；沒有承諾。

## <a name="connectors-as-triggers-and-actions"></a>連接器做為觸發程序和動作

**觸發程序**可啟動或執行邏輯應用程式的執行個體。 有些連接器會提供觸發程序，以在發生特定事件時通知您的應用程式。 比方說，hello FTP 連接器有 hello`OnUpdatedFile`更新檔案時，啟動應用程式邏輯的觸發程序。 

邏輯應用程式包括下列類型的觸發程序的 hello:  

* *輪詢觸發程序*： 這些觸發程序輪詢您在指定的頻率 toocheck 新資料的服務。 

    新的資料可用時，邏輯應用程式的新執行個體以執行 hello 資料做為輸入。 

* *推入觸發程序*： 這些觸發程序會接聽端點上的資料或事件 toohappen，然後觸發程序邏輯應用程式的新執行個體。

* 週期性觸發程序︰此觸發程序會依照指定的排程具現化邏輯應用程式的執行個體。

連接器也會提供您可使用於工作流程中的**動作**。 比方說，邏輯應用程式可以查閱資料，稍後在邏輯應用程式中使用此資料。 更具體來說，您可以從 SQL 資料庫中，查閱客戶資料，，然後使用這個客戶資料 toobuild 您的工作流程。 

> [!TIP]
> [連接器概觀](connectors-overview.md)提供有關觸發程序和動作的詳細資訊。 


## <a name="message-manipulation-actions"></a>訊息操作動作

邏輯應用程式包含內建動作，可變更或操作承載資料。 內建的 hello**資料作業**connector 包含 hello 下列動作： 

| | |
|---|---|
| **撰寫** | 建置或更新版本中，產生值或物件 toouse 或當您建置您的工作流程。 例如，您可以撰寫多個步驟，從值的 JSON 物件或計算常數 tooreference 稍後在邏輯應用程式中執行。 |
| **建立 CSV 資料表**<br/>**建立 HTML 資料表** | 將陣列結果集變成 CSV 或 HTML 資料表。 比方說，加入 hello CRM 「 清單記錄 」 動作，並加入資料錄加入目前的篩選。 然後，作為一個 HTML 資料表，以電子郵件傳送 hello 結果。 |
| **篩選陣列** (查詢) | 篩選您感興趣的結果集 toohello 項目。 例如，搜尋與所有推文`#Azure`，然後 [篩選] hello 會傳回推文 tooonly 傳回的結果`Tweeted_by_followers > 50`。 |
| **Join** | 由某個分隔符號聯結陣列。 比方說，hello 偵測的主要片語作業會傳回陣列的主要片語。 您可以用 `,` 或類似符號加以「聯結」。 因此，您會取得 `"Some, Phrase"`，而不是 `["Some", "Phrase"]`。 |
| **剖析 JSON** | 剖析時，存取從 hello 設計工具中的 JSON 物件的值。 例如，如果您的 Azure 函式會傳回 JSON 承載，然後您可以剖析它 tooaccess hello JSON 屬性，稍後在另一個步驟。 hello 動作也會驗證該 hello JSON 相符項目 hello 指定結構描述在執行階段。 | 
| **選取** | 選取陣列的某些屬性，以便進一步處理。 如果您從 SQL 執行「列出記錄」，而它傳回 15 個資料行，則只要選取幾個資料行以便進一步處理。 hello 輸出是陣列，其中只包含您選取的 hello 屬性。 |

## <a name="custom-connectors-and-azure-certification"></a>自訂連接器和 Azure 憑證 

應用程式開發介面，執行自訂程式碼，或無法使用與連接器 toocall，您可以擴充 hello 邏輯應用程式平台所[建立 REST 式 API 應用程式與自訂連接器](../logic-apps/logic-apps-create-api-app.md)。 

如果您想 toomake 您自訂 API 的應用程式公開和可用 toouse 在 Azure 中，然後送出提名 toohello [Microsoft Azure 認證計劃](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/)。

## <a name="get-help"></a>取得說明

tooask 問題、 回答問題和其他 Azure 邏輯應用程式使用者執行，請參閱移 toohello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。

toohelp 改善 Azure 邏輯應用程式和連接器、 票選或送出意見在 hello [Logic Apps 使用者意見反應網站](http://aka.ms/logicapps-wish)。

我們是否遺漏連接器主題，或任何您認為重要的詳細資訊？ 如果 [是]，然後新增 tooour 現有主題，藉此協助我們，或自行撰寫。 我們的文件是開放原始碼並存放於 GitHub。 從我們的 [GitHub 存放庫](https://github.com/Microsoft/azure-docs)著手。 

## <a name="next-steps"></a>後續步驟
* [建立第一個邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)
* [建立邏輯應用程式的自訂 API](../logic-apps/logic-apps-create-api-app.md)
* [監視邏輯應用程式](../logic-apps/logic-apps-monitor-your-logic-apps.md)

<!--Connectors Documentation-->

[api/web-appdoc]: ../logic-apps/logic-apps-custom-hosted-api.md "整合邏輯應用程式與 App Service API Apps"
[azureblobstoragedoc]: ./connectors-create-api-azureblobstorage.md "使用 Azure Blob 儲存體連接器管理 Blob 容器中的檔案"
[azure-functionsdoc]: ../logic-apps/logic-apps-azure-functions.md "整合邏輯應用程式與 Azure Functions"
[db2doc]: ./connectors-create-api-db2.md "連接 tooIBM DB2 hello 雲端或內部部署中。更新資料列、取得資料表等等"
[Dynamics-365doc]: ./connectors-create-api-crmonline.md "連線 tooDynamics CRM Online，讓您可以使用 CRM Online 資料"
[event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "連接 tooAzure 事件中心。在邏輯應用程式與事件中樞之間接收和傳送事件"
[filesystemdoc]: ../logic-apps/logic-apps-using-file-connector.md "連接 tooan 在內部部署檔案系統"
[ftpdoc]: ./connectors-create-api-ftp.md "連接 tooan FTP / FTPS 伺服器的 FTP 工作，例如上傳時，取得、 刪除檔案及其他"
[httpdoc]: ./connectors-native-http.md "進行 HTTP 呼叫與 hello HTTP 連接器"
[http-requestdoc]: ./connectors-native-reqres.md "將 HTTP 要求和回應 tooyour 邏輯應用程式的動作"
[http-swaggerdoc]: ./connectors-native-http-swagger.md "使用 HTTP + Swagger 連接器進行 HTTP 呼叫"
[informixdoc]: ./connectors-create-api-informix.md "連接 tooInformix hello 雲端或內部部署中。讀取資料列、 清單 hello 資料表及多個"
[nested-logic-appdoc]: ../logic-apps/logic-apps-http-endpoint.md "整合邏輯應用程式與巢狀工作流程"
[office365-outlookdoc]: ./connectors-create-api-office365-outlook.md "Tooyour Office 365 帳戶連接。傳送和接收電子郵件、管理行事曆和連絡人等等"
[oracle-db-doc]: ./connectors-create-api-oracledatabase.md "Tooan Oracle 資料庫 tooadd、 插入、 刪除資料列和多個連接"
[mqdoc]: ./connectors-create-api-mq.md "連接 tooMQ 內部部署或 Azure，以及傳送和接收訊息"
[recurrencedoc]:  ./connectors-native-recurrence.md "觸發邏輯應用程式的重複執行動作"
[salesforcedoc]: ./connectors-create-api-salesforce.md "Tooyour Salesforce 帳戶連接。管理帳戶、潛在客戶、機會等等"
[sapconnector]: ../logic-apps/logic-apps-using-sap-connector.md "Tooan 在內部部署 SAP 系統連接"
[service-busdoc]: ./connectors-create-api-servicebus.md "從「服務匯流排佇列和主題」傳送訊息，並接收來自「服務匯流排佇列和訂用帳戶」的訊息"
[sharepointdoc]: ./connectors-create-api-sharepointonline.md "連接 tooSharePoint 線上。管理文件、列出項目等等"
[sharepointserver]: ./connectors-create-api-sharepointserver.md "連接 tooSharePoint 內部部署伺服器上。管理文件、列出項目等等"
[sql-serverdoc]: ./connectors-create-api-sqlazure.md "TooAzure SQL Database 或 SQL server 連接。建立、更新、取得和刪除 SQL Database 資料表中的項目。"
[twitterdoc]: ./connectors-create-api-twitter.md "連接 tooTwitter。取得時間軸、張貼推文等等"
[webhookdoc]: ./connectors-native-webhook.md "新增 Webhook 動作和觸發程序 tooyour 邏輯應用程式"

[as2doc]: ../logic-apps/logic-apps-enterprise-integration-as2.md "深入了解企業整合 AS2。"
[x12doc]: ../logic-apps/logic-apps-enterprise-integration-x12.md "深入了解企業整合 X12"
[flatfiledoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "深入了解企業整合一般檔案。"
[flatfiledecodedoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "深入了解企業整合一般檔案。"
[xmlvalidatedoc]: ../logic-apps/logic-apps-enterprise-integration-xml-validation.md "深入了解企業整合 XML 驗證。"
[xmltransformdoc]: ../logic-apps/logic-apps-enterprise-integration-transform.md "深入了解企業整合轉換。"
[as2decode]: ../logic-apps/logic-apps-enterprise-integration-as2-decode.md "深入了解企業整合 AS2 解碼"
[as2encode]:../logic-apps/logic-apps-enterprise-integration-as2-encode.md "深入了解企業整合 AS2 編碼"
[X12decode]: ../logic-apps/logic-apps-enterprise-integration-X12-decode.md "深入了解企業整合 X12 解碼"
[X12encode]: ../logic-apps/logic-apps-enterprise-integration-X12-encode.md "深入了解企業整合 X12 編碼"
[EDIFACTdecode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-decode.md "深入了解企業整合 EDIFACT 解碼"
[EDIFACTencode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-encode.md "深入了解企業整合 EDIFACT 編碼"
[integrationaccountdoc]: ../logic-apps/logic-apps-enterprise-integration-metadata.md "查閱整合帳戶中的結構描述、對應、合作夥伴和其他資訊"


[boxDoc]: ./connectors-create-api-box.md "連接 tooBox。上傳、取得、刪除、列出您的檔案等等"
[delaydoc]: ./connectors-native-delay.md "執行延遲的動作"
[dropboxdoc]: ./connectors-create-api-dropbox.md "連接 tooDropbox。上傳、取得、刪除、列出您的檔案等等"
[facebookdoc]: ./connectors-create-api-facebook.md "連接 tooFacebook。Post tooa 時間表、 取得和多個網頁摘要，"
[githubdoc]: ./connectors-create-api-github.md "連接 tooGitHub 和追蹤問題"
[google-drivedoc]: ./connectors-create-api-googledrive.md "連接 tooGoogleDrive，因此您可以使用您的資料"
[google-sheetsdoc]: ./connectors-create-api-googlesheet.md "連接 tooGoogle 工作表，以便可以修改您的工作表"
[google-tasksdoc]: ./connectors-create-api-googletasks.md "連接 tooGoogle 」 工作，因此您可以管理您的工作"
[google-calendardoc]: ./connectors-create-api-googlecalendar.md "連接 tooGoogle 行事曆和可以管理行事曆。"
[http-responsedoc]: ./connectors-native-reqres.md "將 HTTP 要求和回應 tooyour 邏輯應用程式的動作"
[instagramdoc]: ./connectors-create-api-instagram.md "連接 tooInstagram。觸發事件或對其採取行動"
[mailchimpdoc]: ./connectors-create-api-mailchimp.md "Tooyour MailChimp 帳戶連接。管理及自動處理郵件"
[mandrilldoc]: ./connectors-create-api-mandrill.md "連接通訊 tooMandrill"
[microsoft-translatordoc]: ./connectors-create-api-microsofttranslator.md "連接 tooMicrosoft 轉譯器。翻譯文字、偵測語言等等" 
[office365-usersdoc]: ./connectors-create-api-office365-users.md 
[office365-videodoc]: ./connectors-create-api-office365-video.md "取得影片資訊、影片清單和頻道，以及 Office 365 影片的播放 URL"
[onedrivedoc]: ./connectors-create-api-onedrive.md "連接 tooyour Microsoft 的個人 OneDrive。上傳、刪除、列出檔案等等"
[onedrive-for-businessdoc]: ./connectors-create-api-onedriveforbusiness.md "連接 tooyour 商務 Microsoft OneDrive。上傳、刪除、列出您的檔案等等"
[outlook.comdoc]: ./connectors-create-api-outlook.md "連接 tooyour Outlook 信箱。管理電子郵件、行事曆、連絡人等等"
[project-onlinedoc]: ./connectors-create-api-projectonline.md "連接 tooMicrosoft Project Online。管理專案、工作、資源等等"
[querydoc]: ./connectors-native-query.md "選取和篩選 hello 查詢動作的陣列"
[rssdoc]: ./connectors-create-api-rss.md "發佈和擷取摘要項目，觸發作業，當新項目是已發行的 tooan RSS 摘要。"
[sendgriddoc]: ./connectors-create-api-sendgrid.md "連接 tooSendGrid。傳送電子郵件及管理收件者清單"
[sftpdoc]: ./connectors-create-api-sftp.md "Tooyour SFTP 帳戶連接。上傳、取得、刪除檔案等等"
[slackdoc]: ./connectors-create-api-slack.md "連接 tooSlack 並且公佈訊息 tooSlack 通道"
[smtpdoc]: ./connectors-create-api-smtp.md "Tooa SMTP 伺服器連線及傳送電子郵件與附件"
[sparkpostdoc]: ./connectors-create-api-sparkpost.md "連接通訊 tooSparkPost"
[trellodoc]: ./connectors-create-api-trello.md "連接 tooTrello。管理您的專案並組織任何項目與任何人"
[twiliodoc]: ./connectors-create-api-twilio.md "連接 tooTwilio。傳送和取得訊息、取得可用的號碼、管理撥入的電話號碼等等"
[wunderlistdoc]: ./connectors-create-api-wunderlist.md "連接 tooWunderlist。管理您的工作和待辦事項清單、讓您的生活保持同步等等"
[yammerdoc]: ./connectors-create-api-yammer.md "連接 tooYammer。張貼訊息、取得新訊息等等"
[youtubedoc]: ./connectors-create-api-youtube.md "連接 tooYouTube。管理您的影片和頻道"


<!--Icon references-->
[appFiguresicon]: ./media/apis-list/appfigures.png
[Asanaicon]: ./media/apis-list/asana.png
[Azure-Automation-icon]: ./media/apis-list/azure-automation.png
[AzureBlobStorageicon]: ./media/apis-list/azureblob.png
[Azure-Data-Lake-icon]: ./media/apis-list/azure-data-lake.png
[Azure-DocumentDBicon]: ./media/apis-list/azure-documentdb.png
[Azure-MLicon]: ./media/apis-list/azureml.png
[Azure-Resource-Manager-icon]: ./media/apis-list/azure-resource-manager.png
[Azure-Queues-icon]: ./media/apis-list/azure-queues.png
[Basecamp-3icon]: ./media/apis-list/basecamp.png
[Bitbucket-icon]: ./media/apis-list/bitbucket.png
[Bitlyicon]: ./media/apis-list/bitly.png
[BizTalk-Servericon]: ./media/apis-list/biztalk.png
[Bloggericon]: ./media/apis-list/blogger.png
[Boxicon]: ./media/apis-list/box.png
[Campfireicon]: ./media/apis-list/campfire.png
[Cognitive-Services-Text-Analyticsicon]: ./media/apis-list/cognitiveservicestextanalytics.png
[DB2icon]: ./media/apis-list/db2.png
[Dropboxicon]: ./media/apis-list/dropbox.png
[Dynamics-365icon]: ./media/apis-list/dynamicscrmonline.png
[Dynamics-365-for-Financialsicon]: ./media/apis-list/madeira.png
[Dynamics-365-for-Operationsicon]: ./media/apis-list/dynamicsax.png
[Easy-Redmineicon]: ./media/apis-list/easyredmine.png
[Event-Hubs-icon]: ./media/apis-list/eventhubs.png
[Facebookicon]: ./media/apis-list/facebook.png
[FTPicon]: ./media/apis-list/ftp.png
[GitHubicon]: ./media/apis-list/github.png
[Google-Calendaricon]: ./media/apis-list/googlecalendar.png
[Google-Driveicon]: ./media/apis-list/googledrive.png
[Google-Sheetsicon]: ./media/apis-list/googlesheet.png
[Google-Tasksicon]: ./media/apis-list/googletasks.png
[HideKeyicon]: ./media/apis-list/hidekey.png
[HipChaticon]: ./media/apis-list/hipchat.png
[Informixicon]: ./media/apis-list/informix.png
[Insightlyicon]: ./media/apis-list/insightly.png
[Instagramicon]: ./media/apis-list/instagram.png
[Instapapericon]: ./media/apis-list/instapaper.png
[JIRAicon]: ./media/apis-list/jira.png
[MailChimpicon]: ./media/apis-list/mailchimp.png
[Mandrillicon]: ./media/apis-list/mandrill.png
[Microsoft-Translatoricon]: ./media/apis-list/microsofttranslator.png
[MQicon]: ./media/apis-list/mq.png
[Office-365-Outlookicon]: ./media/apis-list/office365.png
[Office-365-Usersicon]: ./media/apis-list/office365users.png
[Office-365-Videoicon]: ./media/apis-list/office365video.png
[OneDriveicon]: ./media/apis-list/onedrive.png
[OneDrive-for-Businessicon]: ./media/apis-list/onedriveforbusiness.png
[Oracle-DB-icon]: ./media/apis-list/oracle-db.png
[Outlook.comicon]: ./media/apis-list/outlook.png
[PagerDutyicon]: ./media/apis-list/pagerduty.png
[Pinteresticon]: ./media/apis-list/pinterest.png
[Project-Onlineicon]: ./media/apis-list/projectonline.png
[Redmineicon]: ./media/apis-list/redmine.png
[RSSicon]: ./media/apis-list/rss.png
[Common-Data-Serviceicon]: ./media/apis-list/runtimeservice.png
[Salesforceicon]: ./media/apis-list/salesforce.png
[SAPicon]: ./media/apis-list/sap.png
[SendGridicon]: ./media/apis-list/sendgrid.png
[Service-Busicon]: ./media/apis-list/servicebus.png
[SFTPicon]: ./media/apis-list/sftp.png
[SharePointicon]: ./media/apis-list/sharepointonline.png
[Slackicon]: ./media/apis-list/slack.png
[Smartsheeticon]: ./media/apis-list/smartsheet.png
[SMTPicon]: ./media/apis-list/smtp.png
[SparkPosticon]: ./media/apis-list/sparkpost.png
[SQL-Servericon]: ./media/apis-list/sql.png
[Todoisticon]: ./media/apis-list/todoist.png
[Trelloicon]: ./media/apis-list/trello.png
[Twilioicon]: ./media/apis-list/twilio.png
[Twittericon]: ./media/apis-list/twitter.png
[Vimeoicon]: ./media/apis-list/vimeo.png
[Visual-Studio-Team-Servicesicon]: ./media/apis-list/visualstudioteamservices.png
[WordPressicon]: ./media/apis-list/wordpress.png
[Wunderlisticon]: ./media/apis-list/wunderlist.png
[Yammericon]: ./media/apis-list/yammer.png
[YouTubeicon]: ./media/apis-list/youtube.png

<!-- Primitive Icons -->
[API/Web-Appicon]: ./media/apis-list/api.png
[Azure-Functionsicon]: ./media/apis-list/function.png
[Delayicon]: ./media/apis-list/delay.png
[FileSystemIcon]: ./media/apis-list/filesystem.png
[HTTPicon]: ./media/apis-list/http.png
[HTTP-Requesticon]: ./media/apis-list/request.png
[HTTP-Responseicon]: ./media/apis-list/response.png
[HTTP-Swaggericon]: ./media/apis-list/http_swagger.png
[Nested-Logic-Appicon]: ./media/apis-list/workflow.png
[Recurrenceicon]: ./media/apis-list/recurrence.png
[Queryicon]: ./media/apis-list/query.png
[Webhookicon]: ./media/apis-list/webhook.png

<!-- EIP Icons -->
[as2icon]: ./media/apis-list/as2.png
[x12icon]: ./media/apis-list/x12new.png
[flatfileicon]: ./media/apis-list/flatfileencoding.png
[flatfiledecodeicon]: ./media/apis-list/flatfiledecoding.png
[xmlvalidateicon]: ./media/apis-list/xmlvalidation.png
[xmltransformicon]: ./media/apis-list/xsltransform.png
[integrationaccounticon]: ./media/apis-list/integrationaccount.png

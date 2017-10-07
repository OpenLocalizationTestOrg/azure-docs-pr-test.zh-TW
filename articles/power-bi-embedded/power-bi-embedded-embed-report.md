---
title: "報表中 Azure Power BI Embedded aaaEmbed |Microsoft 文件"
description: "深入了解如何 tooembed 到您的應用程式是在 Power BI Embedded 的報表。"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a>將報告內嵌在 Power BI Embedded

深入了解如何 tooembed 到您的應用程式是在 Power BI Embedded 的報表。

我們將探討如何 tooactually 將報表內嵌到您的應用程式。 本文假設您在工作區集合的某個工作區內已存有報告。 如果您尚未完成該步驟，請參閱[開始使用 Power BI Embedded](power-bi-embedded-get-started.md)。

您可以使用 hello.NET (C#) 或 Node.js SDK，以及 JavaScript、 tooeasily 建置使用 Power BI Embedded 應用程式。 

## <a name="using-hello-access-keys-toouse-rest-apis"></a>使用 hello 存取金鑰 toouse REST Api

在順序 toocall hello REST API，您可以傳遞 hello 存取金鑰，您可以取得 hello Azure 入口網站指定的工作區集合。 如需詳細資訊，請參閱[開始使用 Power BI Embedded](power-bi-embedded-get-started.md)。

## <a name="get-a-report-id"></a>取得報告識別碼

每個存取權杖都會以報告為基礎。 您必須指定您想 tooembed hello 報表的報表 id tooget hello。 這可以根據呼叫 toohello[取得報表](https://msdn.microsoft.com/library/azure/mt711510.aspx)REST API。 這會傳回識別碼和 hello 內嵌 url 的 hello 報表。 這可以使用 Power BI.NET SDK hello 或直接呼叫 hello REST API。

### <a name="using-hello-power-bi-net-sdk"></a>使用 Power BI.NET SDK hello

當使用 hello.NET SDK，您必須 toocreate hello 存取金鑰，您會收到 hello Azure 入口網站為基礎的權杖認證。 這需要您安裝 hello [Power BI API NuGet 套件](https://www.nuget.org/profiles/powerbi)。

**NuGet 套件安裝**

```
Install-Package Microsoft.PowerBI.Api
```

**C# 程式碼**

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a>呼叫 hello REST API 直接

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a>建立存取權杖

Power BI Embedded 使用內嵌權杖，這是 HMAC 簽署的 JSON Web 權杖。 hello 權杖會簽署與 hello 便捷鍵，從 Azure Power BI Embedded 的工作區集合。 內嵌語彙基元，根據預設，會讀取使用的 tooprovide 只能存取 tooa 報表 tooembed 到應用程式。 內嵌權杖會針對特定報告來核發，而且應該與內嵌 URL 相關聯。

使用 toosign/加密 hello 語彙基元 hello 便捷鍵時，應該 hello 伺服器上建立存取權杖。 如需詳細資訊 toocreate 存取權杖，請參閱[驗證和授權使用 Power BI Embedded](power-bi-embedded-app-token-flow.md)。 您也可以檢閱 hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)方法。 這會看起來像用於 Power BI 中的 hello.NET SDK 的範例如下。

您將使用您先前擷取的 hello 報表識別碼。 Hello 內嵌在建立權杖，您將使用 hello 存取金鑰 toogenerate hello 權杖從 hello javascript 觀點來看，您可以使用。 hello *PowerBIToken 類別*需要您安裝 hello [Power BI 核心 NuGut 封裝](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)。

**NuGet 套件安裝**

```
Install-Package Microsoft.PowerBI.Core
```

**C# 程式碼**

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a>新增權限範圍 tooembed 權杖

當使用內嵌語彙基元時，您可能想 hello 資源存取權給予 toorestrict 使用量。 為此，您可以產生具有範圍權限的權杖。 如需詳細資訊，請參閱[範圍](power-bi-embedded-app-token-flow.md#scopes)

## <a name="embed-using-javascript"></a>使用 JavaScript 進行內嵌

您擁有 hello 存取權杖和 hello 報表識別碼之後，我們可以將內嵌 hello 報表使用 JavaScript。 這需要您安裝 hello nuget [Power BI JavaScript 封裝](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)。 hello embedUrl 只是 https://embedded.powerbi.com/appTokenReportEmbed。

> [!NOTE]
> 您可以使用 hello [JavaScript 報表內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)tootest 功能。 同時也會提供可用的 hello 不同作業的程式碼範例。

**NuGet 套件安裝**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**JavaScript 程式碼**

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-hello-size-of-embedded-elements"></a>設定內嵌元素 hello 大小

hello 報表將自動內嵌根據 hello 其容器的大小。 只要內嵌 hello toooverride hello 預設大小加入 CSS 類別屬性或內嵌樣式的寬度和高度。

## <a name="see-also"></a>另請參閱

[開始使用範例](power-bi-embedded-get-started-sample.md)  
[在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[JavaScript 內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI JavaScript 套件](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
[Power BI API NuGet 套件](https://www.nuget.org/profiles/powerbi)
[Power BI 核心 NuGut 套件](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[PowerBI-CSharp Git 存放庫](https://github.com/Microsoft/PowerBI-CSharp)  
[PowerBI-Node Git存放庫](https://github.com/Microsoft/PowerBI-Node)  
有其他疑問？ [再試一次 hello Power BI 社群](http://community.powerbi.com/)

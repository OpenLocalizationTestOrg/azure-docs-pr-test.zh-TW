---
title: "從 Azure Power BI Embedded 中的資料集的新報表 aaaCreate |Microsoft 文件"
description: "您現在可以在自己的應用程式中從資料集建立 Power BI Embedded 報告。"
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>在 Power BI Embedded 中從資料集建立新的報告

您現在可以在自己的應用程式中從資料集建立 Power BI Embedded 報告。 

hello 驗證方法是類似的報表 toothat 內嵌。 它根據特定 tooa 資料集的存取語彙基元。 用於 PowerBI.com 的權杖是由 Azure Active Directory (AAD) 核發，Power BI Embedded 權杖則是由您自己的服務核發。

建立內嵌報表，hello 簽發的權杖時特定資料集。 語彙基元應該是相關以 hello 內嵌 URL 上 hello 相同項目 tooensure 每個具有唯一的語彙基元。 若要 toocreate 內嵌報表， *Dataset.Read 和 Workspace.Report.Create*範圍必須提供 hello 存取權杖中。

## <a name="create-access-token-needed-toocreate-new-report"></a>建立存取權杖需要的 toocreate 新報表

Power BI Embedded 使用內嵌權杖，這是 HMAC 簽署的 JSON Web 權杖。 hello 權杖會簽署與 hello 便捷鍵，從 Azure Power BI Embedded 的工作區集合。 內嵌語彙基元，根據預設，會讀取使用的 tooprovide 只能存取 tooa 報表 tooembed 到應用程式。 內嵌權杖會針對特定報告來核發，而且應該與內嵌 URL 相關聯。

使用 toosign/加密 hello 語彙基元 hello 便捷鍵時，應該 hello 伺服器上建立存取權杖。 如需詳細資訊 toocreate 存取權杖，請參閱[驗證和授權使用 Power BI Embedded](power-bi-embedded-app-token-flow.md)。 您也可以檢閱 hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)方法。 這會看起來像用於 Power BI 中的 hello.NET SDK 的範例如下。

在此範例中，我們有我們我們想 toocreat hello 新報表的資料集識別碼。 我們還需要 tooadd hello 範圍*Dataset.Read 和 Workspace.Report.Create*。

hello *PowerBIToken 類別*需要您安裝 hello [Power BI 核心 NuGut 封裝](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)。

**NuGet 套件安裝**

```
Install-Package Microsoft.PowerBI.Core
```

**C# 程式碼**

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a>建立新的空白報告

順序 toocreate 新的報表，在建立 hello 應提供組態。 這應該包含 hello 存取權杖、 hello embedURL 和 hello datasetID 我們想要針對 toocreate hello 報表。 這需要您安裝 hello nuget [Power BI JavaScript 封裝](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)。 hello embedUrl 只是 https://embedded.powerbi.com/appTokenReportEmbed。

> [!NOTE]
> 您可以使用 hello [JavaScript 報表內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)tootest 功能。 同時也會提供可用的 hello 不同作業的程式碼範例。

**NuGet 套件安裝**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**JavaScript 程式碼**

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

呼叫*powerbi.createReport()*將空白的畫布中編輯模式出現在 hello *div*項目。

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>儲存新報告

hello 報表會實際之前不會建立呼叫 hello**存**作業。 這可從 [檔案] 功能表或從 JavaScript 來進行。

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> 在呼叫**另存新檔**後，才會建立新報告。 儲存之後，hello 畫布仍將顯示 hello 資料集編輯模式和不 hello 報告中。 就像任何其他報表一樣，您將需要 tooreload hello 新報表。

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a>載入 hello 新報表

在訂單 toointeract 與 hello 新報表中，您需要 tooembed 它 hello 一樣 hello 應用程式內嵌一般報表、 意義、 新的權杖必須發出特別為 hello 新報表，然後呼叫 hello 內嵌方法。

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a>自動儲存和載入新的報表，使用 「 儲存 」 事件的 hello

Tooautomate hello 程序中的 另存新檔 」 和 「 儲存 」 事件的 hello 然後載入 hello 新的報表，您可以進行使用。 Hello 儲存作業完成，且它會傳回 Json 物件，包含 hello 新 reportId、 報表名稱、 hello 舊 reportId （如果有的話），如果 hello 作業另存新檔或儲存時，會引發這個事件。

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

您可以接聽 hello 「 儲存 」 事件、 使用 hello 新 reportId、 建立 hello 新權杖並與其內嵌 hello 新報表，tooAutomate hello 程序。

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a>另請參閱

[開始使用範例](power-bi-embedded-get-started-sample.md)  
[儲存報告](power-bi-embedded-save-reports.md)  
[內嵌報告](power-bi-embedded-embed-report.md)  
[在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript 內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI 核心 NuGut 套件](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Power BI JavaScript 套件](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
有其他疑問？ [再試一次 hello Power BI 社群](http://community.powerbi.com/)

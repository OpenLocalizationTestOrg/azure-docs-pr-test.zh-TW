---
title: "在 Azure Power BI Embedded 中儲存報告 | Microsoft Docs"
description: "了解如何在 Power BI Embedded 內儲存報告。 這需要適當權限才能順利運作。"
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
ms.openlocfilehash: ad895004cc2972f2ded81566186325a16d401151
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="save-reports-in-power-bi-embedded"></a>在 Power BI Embedded 中儲存報告

了解如何在 Power BI Embedded 內儲存報告。 這需要適當權限才能順利運作。

在 Power BI Embedded 內，您可以編輯現有報告並予以儲存。 您也可以建立新的報告，並另存為新報告來建立報告。

若要儲存報告，您必須先為特定報告建立具有正確範圍的權杖︰

* 若要啟用儲存，就必須有 Report.ReadWrite 範圍
* 若要啟用另存新檔，就必須有 Report.Read 和 Workspace.Report.Copy 範圍
* 若要啟用儲存和另存新檔，就必須有 Report.ReadWrite 和 Workspace.Report.Copy

若要在 [檔案] 功能表中分別啟用正確的 [儲存]/[另存新檔] 按鈕，您必須在內嵌報告時於內嵌組態中提供正確的權限︰

* models.Permissions.ReadWrite
* models.Permissions.Copy
* models.Permissions.All

> [!NOTE]
> 存取權杖也需要適當的範圍。 如需詳細資訊，請參閱[範圍](power-bi-embedded-app-token-flow.md#scopes)。

## <a name="embed-report-in-edit-mode"></a>內嵌編輯模式的報告

假設您想要在應用程式中內嵌編輯模式的報告，若要這麼做，只需在內嵌組態中傳遞正確的屬性並呼叫 powerbi.embed() 即可。 您必須提供權限和 viewMode，才能在編輯模式中看到 [儲存] 和 [另存新檔] 按鈕。 如需詳細資訊，請參閱[內嵌組態詳細資料](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details)。

例如，在 JavaScript 中：

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used to describe the what and how to embed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference to the embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed the report and display it within the div container.
    var report = powerbi.embed(reportContainer, config);
```

現在報告會以編輯模式內嵌在應用程式中。

## <a name="save-report"></a>儲存報告

使用正確的權杖和權限內嵌編輯模式的報告之後，即可從 [檔案] 功能表或從 JavaScript 儲存報告︰

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>另存新檔

```
// Get a reference to the embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> 在另存新檔後才會建立新報告。 在儲存後，畫布仍會顯示編輯模式的舊報告，而非新報告。 您必須內嵌已建立的新報告。 這會需要新的存取權杖，因為權杖是針對個別報告來建立的。

然後，您必須在另存新檔之後載入新的報告。 這與內嵌任何報告時類似。

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="see-also"></a>另請參閱

[開始使用範例](power-bi-embedded-get-started-sample.md)  
[內嵌報告](power-bi-embedded-embed-report.md)  
[從資料集建立新的報告](power-bi-embedded-create-report-from-dataset.md)  
[在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript 內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
有其他疑問？ [試用 Power BI 社群](http://community.powerbi.com/)


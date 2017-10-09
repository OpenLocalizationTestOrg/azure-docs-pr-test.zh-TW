---
title: "在 Azure Power BI Embedded aaaSave 報表 |Microsoft 文件"
description: "了解如何內嵌 Power BI 中的 toosave 報表。 已成功，這需要 toowork 順序中的適當權限。"
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
ms.openlocfilehash: 984537ce1ce1afc787d6c6c9f61ae8d6226d1171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="save-reports-in-power-bi-embedded"></a>在 Power BI Embedded 中儲存報告

了解如何內嵌 Power BI 中的 toosave 報表。 已成功，這需要 toowork 順序中的適當權限。

在 Power BI Embedded 內，您可以編輯現有報告並予以儲存。 您也可以建立新的報表，並儲存為新的報表 toocreate 其中一個。

順序 toosave 報告在您第一次需要 toocreate 語彙基元 hello 與 hello 權限範圍的特定報表：

* 儲存 Report.ReadWrite 範圍 tooenable 是必要項
* 做為儲存 tooenable，Report.Read 和 Workspace.Report.Copy 範圍所需
* tooenable 儲存，而且儲存，Report.ReadWrite 和 Workspace.Report.Copy requierd

分別儲存/儲存右的順序 tooenable hello 中以在 [檔案] 功能表按鈕需要 tooprovide hello 以滑鼠右鍵 hello 內嵌組態中的權限時您內嵌 hello 報表：

* models.Permissions.ReadWrite
* models.Permissions.Copy
* models.Permissions.All

> [!NOTE]
> 您的存取權杖也需要 hello 適當的範圍。 如需詳細資訊，請參閱[範圍](power-bi-embedded-app-token-flow.md#scopes)。

## <a name="embed-report-in-edit-mode"></a>內嵌編輯模式的報告

讓我們假設您的應用程式內想 tooEmbed 處於編輯模式的報表，toodo 只要傳入內嵌組態中的 hello 權限內容，並呼叫 powerbi.embed()。 您將需要 toosupply 權限和順序 toosee hello 儲存，並將儲存在 viewMode，以在編輯模式中的按鈕。 如需詳細資訊，請參閱[內嵌組態詳細資料](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details)。

例如，在 JavaScript 中：

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
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

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

現在報告會以編輯模式內嵌在應用程式中。

## <a name="save-report"></a>儲存報告

Embbeding hello 報表中的編輯權限語彙基元 hello 和權限模式之後您就可以從 hello 檔案 功能表或從 javascript 儲存 hello 報表：

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>另存新檔

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
> 在另存新檔後才會建立新報告。 Hello 儲存之後，hello 畫布仍然編輯模式和不 hello 新報表中顯示 hello 舊的報表。 您將需要 tooembed hello 新報表所建立。 這會需要新的存取權杖，因為權杖是針對個別報告來建立的。

然後，您將需要 tooload hello 新報表之後*存*。 這是類似 tooembedding 任何報表。

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

## <a name="see-also"></a>另請參閱

[開始使用範例](power-bi-embedded-get-started-sample.md)  
[內嵌報告](power-bi-embedded-embed-report.md)  
[從資料集建立新的報告](power-bi-embedded-create-report-from-dataset.md)  
[在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript 內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
有其他疑問？ [再試一次 hello Power BI 社群](http://community.powerbi.com/)


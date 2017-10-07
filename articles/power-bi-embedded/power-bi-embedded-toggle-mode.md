---
title: "檢視和編輯模式中 Azure Power BI Embedded 報表之間 aaaToggle |Microsoft 文件"
description: "深入了解如何內嵌 Power BI 中報表的檢視和編輯模式之間 tootoggle。"
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
ms.openlocfilehash: c9e3da5f9ae74d221af650adebde7c9d83b38a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a>為 Power BI Embedded 中的報告切換檢視和編輯模式

深入了解如何內嵌 Power BI 中報表的檢視和編輯模式之間 tootoggle。

## <a name="creating-an-access-token"></a>建立存取權杖

您將需要 toocreate hello 能力 tooboth 檢視和編輯報表，可讓您存取權杖。 tooedit 儲存報告，您將需要 hello **Report.ReadWrite**語彙基元的權限。 如需詳細資訊，請參閱[在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)。

> [!NOTE]
> 這將允許您 tooedit 並儲存變更 tooan 現有的報表。 如果您也想要支援的 hello 函式**存**，您將需要 toosupply 額外的權限。 如需詳細資訊，請參閱[範圍](power-bi-embedded-app-token-flow.md#scopes)。

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a>內嵌組態

您將需要 toosupply 權限和順序 toosee hello 儲存在編輯模式中的按鈕中的 viewMode。 如需詳細資訊，請參閱[內嵌組態詳細資料](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details)。

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
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
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

這會指出基礎檢視模式中的 tooembed hello 報表**viewMode**設定得**模型。ViewMode.View**。

## <a name="view-mode"></a>檢視模式

如果您是在編輯模式，您可以使用下列 JavaScript tooswitch 進入檢視模式的 hello。

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a>編輯模式

如果您在檢視模式，您可以使用下列 JavaScript tooswitch 進入編輯模式的 hello。

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a>另請參閱

[開始使用範例](power-bi-embedded-get-started-sample.md)  
[內嵌報告](power-bi-embedded-embed-report.md)  
[在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[JavaScript 內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[PowerBI-CSharp Git 存放庫](https://github.com/Microsoft/PowerBI-CSharp)  
[PowerBI-Node Git存放庫](https://github.com/Microsoft/PowerBI-Node)  
有其他疑問？ [再試一次 hello Power BI 社群](http://community.powerbi.com/)

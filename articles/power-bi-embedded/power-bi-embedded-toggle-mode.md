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
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a><span data-ttu-id="68285-103">為 Power BI Embedded 中的報告切換檢視和編輯模式</span><span class="sxs-lookup"><span data-stu-id="68285-103">Toggle between view and edit mode for reports in Power BI Embedded</span></span>

<span data-ttu-id="68285-104">深入了解如何內嵌 Power BI 中報表的檢視和編輯模式之間 tootoggle。</span><span class="sxs-lookup"><span data-stu-id="68285-104">Learn how tootoggle between view and edit mode for your reports within Power BI Embedded.</span></span>

## <a name="creating-an-access-token"></a><span data-ttu-id="68285-105">建立存取權杖</span><span class="sxs-lookup"><span data-stu-id="68285-105">Creating an access token</span></span>

<span data-ttu-id="68285-106">您將需要 toocreate hello 能力 tooboth 檢視和編輯報表，可讓您存取權杖。</span><span class="sxs-lookup"><span data-stu-id="68285-106">You will need toocreate an access token that gives you hello ability tooboth view and edit a report.</span></span> <span data-ttu-id="68285-107">tooedit 儲存報告，您將需要 hello **Report.ReadWrite**語彙基元的權限。</span><span class="sxs-lookup"><span data-stu-id="68285-107">tooedit and save a report, you will need hello **Report.ReadWrite** token permission.</span></span> <span data-ttu-id="68285-108">如需詳細資訊，請參閱[在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)。</span><span class="sxs-lookup"><span data-stu-id="68285-108">For more information, see [Authenticating and authorizing in Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

> [!NOTE]
> <span data-ttu-id="68285-109">這將允許您 tooedit 並儲存變更 tooan 現有的報表。</span><span class="sxs-lookup"><span data-stu-id="68285-109">This will allow you tooedit and save changes tooan existing report.</span></span> <span data-ttu-id="68285-110">如果您也想要支援的 hello 函式**存**，您將需要 toosupply 額外的權限。</span><span class="sxs-lookup"><span data-stu-id="68285-110">If you would also like hello function of supporting **Save As**, you will need toosupply additional permissions.</span></span> <span data-ttu-id="68285-111">如需詳細資訊，請參閱[範圍](power-bi-embedded-app-token-flow.md#scopes)。</span><span class="sxs-lookup"><span data-stu-id="68285-111">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a><span data-ttu-id="68285-112">內嵌組態</span><span class="sxs-lookup"><span data-stu-id="68285-112">Embed configuration</span></span>

<span data-ttu-id="68285-113">您將需要 toosupply 權限和順序 toosee hello 儲存在編輯模式中的按鈕中的 viewMode。</span><span class="sxs-lookup"><span data-stu-id="68285-113">You will need toosupply permissions and a viewMode in order toosee hello save button when in edit mode.</span></span> <span data-ttu-id="68285-114">如需詳細資訊，請參閱[內嵌組態詳細資料](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details)。</span><span class="sxs-lookup"><span data-stu-id="68285-114">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="68285-115">例如，在 JavaScript 中：</span><span class="sxs-lookup"><span data-stu-id="68285-115">For example in JavaScript:</span></span>

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

<span data-ttu-id="68285-116">這會指出基礎檢視模式中的 tooembed hello 報表**viewMode**設定得**模型。ViewMode.View**。</span><span class="sxs-lookup"><span data-stu-id="68285-116">This will indicate tooembed hello report in view mode based on **viewMode** being set too**models.ViewMode.View**.</span></span>

## <a name="view-mode"></a><span data-ttu-id="68285-117">檢視模式</span><span class="sxs-lookup"><span data-stu-id="68285-117">View mode</span></span>

<span data-ttu-id="68285-118">如果您是在編輯模式，您可以使用下列 JavaScript tooswitch 進入檢視模式的 hello。</span><span class="sxs-lookup"><span data-stu-id="68285-118">You can use hello following JavaScript tooswitch into view mode, if you are in edit mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a><span data-ttu-id="68285-119">編輯模式</span><span class="sxs-lookup"><span data-stu-id="68285-119">Edit mode</span></span>

<span data-ttu-id="68285-120">如果您在檢視模式，您可以使用下列 JavaScript tooswitch 進入編輯模式的 hello。</span><span class="sxs-lookup"><span data-stu-id="68285-120">You can use hello following JavaScript tooswitch into edit mode, if you are in view mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a><span data-ttu-id="68285-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="68285-121">See also</span></span>

[<span data-ttu-id="68285-122">開始使用範例</span><span class="sxs-lookup"><span data-stu-id="68285-122">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="68285-123">內嵌報告</span><span class="sxs-lookup"><span data-stu-id="68285-123">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="68285-124">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="68285-124">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="68285-125">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="68285-125">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="68285-126">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="68285-126">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="68285-127">PowerBI-CSharp Git 存放庫</span><span class="sxs-lookup"><span data-stu-id="68285-127">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="68285-128">PowerBI-Node Git存放庫</span><span class="sxs-lookup"><span data-stu-id="68285-128">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="68285-129">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="68285-129">More questions?</span></span> [<span data-ttu-id="68285-130">再試一次 hello Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="68285-130">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

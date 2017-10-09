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
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="beb54-104">在 Power BI Embedded 中儲存報告</span><span class="sxs-lookup"><span data-stu-id="beb54-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="beb54-105">了解如何內嵌 Power BI 中的 toosave 報表。</span><span class="sxs-lookup"><span data-stu-id="beb54-105">Learn how toosave reports within Power BI embedded.</span></span> <span data-ttu-id="beb54-106">已成功，這需要 toowork 順序中的適當權限。</span><span class="sxs-lookup"><span data-stu-id="beb54-106">This requires proper permissions in order toowork successfully.</span></span>

<span data-ttu-id="beb54-107">在 Power BI Embedded 內，您可以編輯現有報告並予以儲存。</span><span class="sxs-lookup"><span data-stu-id="beb54-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="beb54-108">您也可以建立新的報表，並儲存為新的報表 toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="beb54-108">You can also create a new report and save as a new report toocreate one.</span></span>

<span data-ttu-id="beb54-109">順序 toosave 報告在您第一次需要 toocreate 語彙基元 hello 與 hello 權限範圍的特定報表：</span><span class="sxs-lookup"><span data-stu-id="beb54-109">In order toosave a report you first need toocreate a token for hello specific report with hello right scopes:</span></span>

* <span data-ttu-id="beb54-110">儲存 Report.ReadWrite 範圍 tooenable 是必要項</span><span class="sxs-lookup"><span data-stu-id="beb54-110">tooenable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="beb54-111">做為儲存 tooenable，Report.Read 和 Workspace.Report.Copy 範圍所需</span><span class="sxs-lookup"><span data-stu-id="beb54-111">tooenable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="beb54-112">tooenable 儲存，而且儲存，Report.ReadWrite 和 Workspace.Report.Copy requierd</span><span class="sxs-lookup"><span data-stu-id="beb54-112">tooenable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="beb54-113">分別儲存/儲存右的順序 tooenable hello 中以在 [檔案] 功能表按鈕需要 tooprovide hello 以滑鼠右鍵 hello 內嵌組態中的權限時您內嵌 hello 報表：</span><span class="sxs-lookup"><span data-stu-id="beb54-113">Respectively in order tooenable hello right save/save as buttons in file menu you need tooprovide hello right permission in hello Embed configuration when you Embed hello report:</span></span>

* <span data-ttu-id="beb54-114">models.Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="beb54-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="beb54-115">models.Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="beb54-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="beb54-116">models.Permissions.All</span><span class="sxs-lookup"><span data-stu-id="beb54-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="beb54-117">您的存取權杖也需要 hello 適當的範圍。</span><span class="sxs-lookup"><span data-stu-id="beb54-117">Your access token also needs hello appropriate scopes.</span></span> <span data-ttu-id="beb54-118">如需詳細資訊，請參閱[範圍](power-bi-embedded-app-token-flow.md#scopes)。</span><span class="sxs-lookup"><span data-stu-id="beb54-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="beb54-119">內嵌編輯模式的報告</span><span class="sxs-lookup"><span data-stu-id="beb54-119">Embed report in edit mode</span></span>

<span data-ttu-id="beb54-120">讓我們假設您的應用程式內想 tooEmbed 處於編輯模式的報表，toodo 只要傳入內嵌組態中的 hello 權限內容，並呼叫 powerbi.embed()。</span><span class="sxs-lookup"><span data-stu-id="beb54-120">Let's say you want tooEmbed a report in edit mode inside your app, toodo so just pass hello right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="beb54-121">您將需要 toosupply 權限和順序 toosee hello 儲存，並將儲存在 viewMode，以在編輯模式中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="beb54-121">You will need toosupply permissions and a viewMode in order toosee hello save and save as buttons when in edit mode.</span></span> <span data-ttu-id="beb54-122">如需詳細資訊，請參閱[內嵌組態詳細資料](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details)。</span><span class="sxs-lookup"><span data-stu-id="beb54-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="beb54-123">例如，在 JavaScript 中：</span><span class="sxs-lookup"><span data-stu-id="beb54-123">For example in JavaScript:</span></span>

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

<span data-ttu-id="beb54-124">現在報告會以編輯模式內嵌在應用程式中。</span><span class="sxs-lookup"><span data-stu-id="beb54-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="beb54-125">儲存報告</span><span class="sxs-lookup"><span data-stu-id="beb54-125">Save report</span></span>

<span data-ttu-id="beb54-126">Embbeding hello 報表中的編輯權限語彙基元 hello 和權限模式之後您就可以從 hello 檔案 功能表或從 javascript 儲存 hello 報表：</span><span class="sxs-lookup"><span data-stu-id="beb54-126">After Embbeding hello report in edit mode with hello right token and permissions you can save hello report from hello file menu or from javascript:</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="beb54-127">另存新檔</span><span class="sxs-lookup"><span data-stu-id="beb54-127">Save as</span></span>

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
> <span data-ttu-id="beb54-128">在另存新檔後才會建立新報告。</span><span class="sxs-lookup"><span data-stu-id="beb54-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="beb54-129">Hello 儲存之後，hello 畫布仍然編輯模式和不 hello 新報表中顯示 hello 舊的報表。</span><span class="sxs-lookup"><span data-stu-id="beb54-129">After hello save, hello canvas is still showing hello old report in edit mode and not hello new report.</span></span> <span data-ttu-id="beb54-130">您將需要 tooembed hello 新報表所建立。</span><span class="sxs-lookup"><span data-stu-id="beb54-130">You will need tooembed hello new report that was created.</span></span> <span data-ttu-id="beb54-131">這會需要新的存取權杖，因為權杖是針對個別報告來建立的。</span><span class="sxs-lookup"><span data-stu-id="beb54-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="beb54-132">然後，您將需要 tooload hello 新報表之後*存*。</span><span class="sxs-lookup"><span data-stu-id="beb54-132">You will then need tooload hello new report after a *save as*.</span></span> <span data-ttu-id="beb54-133">這是類似 tooembedding 任何報表。</span><span class="sxs-lookup"><span data-stu-id="beb54-133">This is similar tooembedding any report.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="beb54-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="beb54-134">See also</span></span>

[<span data-ttu-id="beb54-135">開始使用範例</span><span class="sxs-lookup"><span data-stu-id="beb54-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="beb54-136">內嵌報告</span><span class="sxs-lookup"><span data-stu-id="beb54-136">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="beb54-137">從資料集建立新的報告</span><span class="sxs-lookup"><span data-stu-id="beb54-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="beb54-138">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="beb54-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="beb54-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="beb54-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="beb54-140">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="beb54-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="beb54-141">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="beb54-141">More questions?</span></span> [<span data-ttu-id="beb54-142">再試一次 hello Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="beb54-142">Try hello Power BI Community</span></span>](http://community.powerbi.com/)


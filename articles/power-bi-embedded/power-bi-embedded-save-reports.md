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
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="d6888-104">在 Power BI Embedded 中儲存報告</span><span class="sxs-lookup"><span data-stu-id="d6888-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="d6888-105">了解如何在 Power BI Embedded 內儲存報告。</span><span class="sxs-lookup"><span data-stu-id="d6888-105">Learn how to save reports within Power BI embedded.</span></span> <span data-ttu-id="d6888-106">這需要適當權限才能順利運作。</span><span class="sxs-lookup"><span data-stu-id="d6888-106">This requires proper permissions in order to work successfully.</span></span>

<span data-ttu-id="d6888-107">在 Power BI Embedded 內，您可以編輯現有報告並予以儲存。</span><span class="sxs-lookup"><span data-stu-id="d6888-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="d6888-108">您也可以建立新的報告，並另存為新報告來建立報告。</span><span class="sxs-lookup"><span data-stu-id="d6888-108">You can also create a new report and save as a new report to create one.</span></span>

<span data-ttu-id="d6888-109">若要儲存報告，您必須先為特定報告建立具有正確範圍的權杖︰</span><span class="sxs-lookup"><span data-stu-id="d6888-109">In order to save a report you first need to create a token for the specific report with the right scopes:</span></span>

* <span data-ttu-id="d6888-110">若要啟用儲存，就必須有 Report.ReadWrite 範圍</span><span class="sxs-lookup"><span data-stu-id="d6888-110">To enable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="d6888-111">若要啟用另存新檔，就必須有 Report.Read 和 Workspace.Report.Copy 範圍</span><span class="sxs-lookup"><span data-stu-id="d6888-111">To enable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="d6888-112">若要啟用儲存和另存新檔，就必須有 Report.ReadWrite 和 Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="d6888-112">To enable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="d6888-113">若要在 [檔案] 功能表中分別啟用正確的 [儲存]/[另存新檔] 按鈕，您必須在內嵌報告時於內嵌組態中提供正確的權限︰</span><span class="sxs-lookup"><span data-stu-id="d6888-113">Respectively in order to enable the right save/save as buttons in file menu you need to provide the right permission in the Embed configuration when you Embed the report:</span></span>

* <span data-ttu-id="d6888-114">models.Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="d6888-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="d6888-115">models.Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="d6888-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="d6888-116">models.Permissions.All</span><span class="sxs-lookup"><span data-stu-id="d6888-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="d6888-117">存取權杖也需要適當的範圍。</span><span class="sxs-lookup"><span data-stu-id="d6888-117">Your access token also needs the appropriate scopes.</span></span> <span data-ttu-id="d6888-118">如需詳細資訊，請參閱[範圍](power-bi-embedded-app-token-flow.md#scopes)。</span><span class="sxs-lookup"><span data-stu-id="d6888-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="d6888-119">內嵌編輯模式的報告</span><span class="sxs-lookup"><span data-stu-id="d6888-119">Embed report in edit mode</span></span>

<span data-ttu-id="d6888-120">假設您想要在應用程式中內嵌編輯模式的報告，若要這麼做，只需在內嵌組態中傳遞正確的屬性並呼叫 powerbi.embed() 即可。</span><span class="sxs-lookup"><span data-stu-id="d6888-120">Let's say you want to Embed a report in edit mode inside your app, to do so just pass the right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="d6888-121">您必須提供權限和 viewMode，才能在編輯模式中看到 [儲存] 和 [另存新檔] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d6888-121">You will need to supply permissions and a viewMode in order to see the save and save as buttons when in edit mode.</span></span> <span data-ttu-id="d6888-122">如需詳細資訊，請參閱[內嵌組態詳細資料](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details)。</span><span class="sxs-lookup"><span data-stu-id="d6888-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="d6888-123">例如，在 JavaScript 中：</span><span class="sxs-lookup"><span data-stu-id="d6888-123">For example in JavaScript:</span></span>

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

<span data-ttu-id="d6888-124">現在報告會以編輯模式內嵌在應用程式中。</span><span class="sxs-lookup"><span data-stu-id="d6888-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="d6888-125">儲存報告</span><span class="sxs-lookup"><span data-stu-id="d6888-125">Save report</span></span>

<span data-ttu-id="d6888-126">使用正確的權杖和權限內嵌編輯模式的報告之後，即可從 [檔案] 功能表或從 JavaScript 儲存報告︰</span><span class="sxs-lookup"><span data-stu-id="d6888-126">After Embbeding the report in edit mode with the right token and permissions you can save the report from the file menu or from javascript:</span></span>

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="d6888-127">另存新檔</span><span class="sxs-lookup"><span data-stu-id="d6888-127">Save as</span></span>

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
> <span data-ttu-id="d6888-128">在另存新檔後才會建立新報告。</span><span class="sxs-lookup"><span data-stu-id="d6888-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="d6888-129">在儲存後，畫布仍會顯示編輯模式的舊報告，而非新報告。</span><span class="sxs-lookup"><span data-stu-id="d6888-129">After the save, the canvas is still showing the old report in edit mode and not the new report.</span></span> <span data-ttu-id="d6888-130">您必須內嵌已建立的新報告。</span><span class="sxs-lookup"><span data-stu-id="d6888-130">You will need to embed the new report that was created.</span></span> <span data-ttu-id="d6888-131">這會需要新的存取權杖，因為權杖是針對個別報告來建立的。</span><span class="sxs-lookup"><span data-stu-id="d6888-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="d6888-132">然後，您必須在另存新檔之後載入新的報告。</span><span class="sxs-lookup"><span data-stu-id="d6888-132">You will then need to load the new report after a *save as*.</span></span> <span data-ttu-id="d6888-133">這與內嵌任何報告時類似。</span><span class="sxs-lookup"><span data-stu-id="d6888-133">This is similar to embedding any report.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="d6888-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d6888-134">See also</span></span>

[<span data-ttu-id="d6888-135">開始使用範例</span><span class="sxs-lookup"><span data-stu-id="d6888-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="d6888-136">內嵌報告</span><span class="sxs-lookup"><span data-stu-id="d6888-136">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="d6888-137">從資料集建立新的報告</span><span class="sxs-lookup"><span data-stu-id="d6888-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="d6888-138">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="d6888-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="d6888-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="d6888-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="d6888-140">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="d6888-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="d6888-141">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="d6888-141">More questions?</span></span> [<span data-ttu-id="d6888-142">試用 Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="d6888-142">Try the Power BI Community</span></span>](http://community.powerbi.com/)


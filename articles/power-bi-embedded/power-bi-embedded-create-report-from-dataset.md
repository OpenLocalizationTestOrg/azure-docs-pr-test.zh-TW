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
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="b51cf-103">在 Power BI Embedded 中從資料集建立新的報告</span><span class="sxs-lookup"><span data-stu-id="b51cf-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="b51cf-104">您現在可以在自己的應用程式中從資料集建立 Power BI Embedded 報告。</span><span class="sxs-lookup"><span data-stu-id="b51cf-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="b51cf-105">hello 驗證方法是類似的報表 toothat 內嵌。</span><span class="sxs-lookup"><span data-stu-id="b51cf-105">hello authentication method is similar toothat of report embed.</span></span> <span data-ttu-id="b51cf-106">它根據特定 tooa 資料集的存取語彙基元。</span><span class="sxs-lookup"><span data-stu-id="b51cf-106">It is based on access tokens that are specific tooa dataset.</span></span> <span data-ttu-id="b51cf-107">用於 PowerBI.com 的權杖是由 Azure Active Directory (AAD) 核發，Power BI Embedded 權杖則是由您自己的服務核發。</span><span class="sxs-lookup"><span data-stu-id="b51cf-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="b51cf-108">建立內嵌報表，hello 簽發的權杖時特定資料集。</span><span class="sxs-lookup"><span data-stu-id="b51cf-108">When createing an Embedded report, hello tokens issued are for a specific dataset.</span></span> <span data-ttu-id="b51cf-109">語彙基元應該是相關以 hello 內嵌 URL 上 hello 相同項目 tooensure 每個具有唯一的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="b51cf-109">Tokens should be associated with hello embed URL on hello same element tooensure each has a unique token.</span></span> <span data-ttu-id="b51cf-110">若要 toocreate 內嵌報表， *Dataset.Read 和 Workspace.Report.Create*範圍必須提供 hello 存取權杖中。</span><span class="sxs-lookup"><span data-stu-id="b51cf-110">In order toocreate an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in hello access token.</span></span>

## <a name="create-access-token-needed-toocreate-new-report"></a><span data-ttu-id="b51cf-111">建立存取權杖需要的 toocreate 新報表</span><span class="sxs-lookup"><span data-stu-id="b51cf-111">Create access token needed toocreate new report</span></span>

<span data-ttu-id="b51cf-112">Power BI Embedded 使用內嵌權杖，這是 HMAC 簽署的 JSON Web 權杖。</span><span class="sxs-lookup"><span data-stu-id="b51cf-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="b51cf-113">hello 權杖會簽署與 hello 便捷鍵，從 Azure Power BI Embedded 的工作區集合。</span><span class="sxs-lookup"><span data-stu-id="b51cf-113">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="b51cf-114">內嵌語彙基元，根據預設，會讀取使用的 tooprovide 只能存取 tooa 報表 tooembed 到應用程式。</span><span class="sxs-lookup"><span data-stu-id="b51cf-114">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="b51cf-115">內嵌權杖會針對特定報告來核發，而且應該與內嵌 URL 相關聯。</span><span class="sxs-lookup"><span data-stu-id="b51cf-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="b51cf-116">使用 toosign/加密 hello 語彙基元 hello 便捷鍵時，應該 hello 伺服器上建立存取權杖。</span><span class="sxs-lookup"><span data-stu-id="b51cf-116">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="b51cf-117">如需詳細資訊 toocreate 存取權杖，請參閱[驗證和授權使用 Power BI Embedded](power-bi-embedded-app-token-flow.md)。</span><span class="sxs-lookup"><span data-stu-id="b51cf-117">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="b51cf-118">您也可以檢閱 hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)方法。</span><span class="sxs-lookup"><span data-stu-id="b51cf-118">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="b51cf-119">這會看起來像用於 Power BI 中的 hello.NET SDK 的範例如下。</span><span class="sxs-lookup"><span data-stu-id="b51cf-119">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="b51cf-120">在此範例中，我們有我們我們想 toocreat hello 新報表的資料集識別碼。</span><span class="sxs-lookup"><span data-stu-id="b51cf-120">In this example, we have our dataset id that we want toocreat hello new report on.</span></span> <span data-ttu-id="b51cf-121">我們還需要 tooadd hello 範圍*Dataset.Read 和 Workspace.Report.Create*。</span><span class="sxs-lookup"><span data-stu-id="b51cf-121">We also need tooadd hello scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="b51cf-122">hello *PowerBIToken 類別*需要您安裝 hello [Power BI 核心 NuGut 封裝](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)。</span><span class="sxs-lookup"><span data-stu-id="b51cf-122">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="b51cf-123">**NuGet 套件安裝**</span><span class="sxs-lookup"><span data-stu-id="b51cf-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="b51cf-124">**C# 程式碼**</span><span class="sxs-lookup"><span data-stu-id="b51cf-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="b51cf-125">建立新的空白報告</span><span class="sxs-lookup"><span data-stu-id="b51cf-125">Create a new blank report</span></span>

<span data-ttu-id="b51cf-126">順序 toocreate 新的報表，在建立 hello 應提供組態。</span><span class="sxs-lookup"><span data-stu-id="b51cf-126">In order toocreate a new report, hello create configuration should be provided.</span></span> <span data-ttu-id="b51cf-127">這應該包含 hello 存取權杖、 hello embedURL 和 hello datasetID 我們想要針對 toocreate hello 報表。</span><span class="sxs-lookup"><span data-stu-id="b51cf-127">This should include hello access token, hello embedURL and hello datasetID that we want toocreate hello report against.</span></span> <span data-ttu-id="b51cf-128">這需要您安裝 hello nuget [Power BI JavaScript 封裝](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)。</span><span class="sxs-lookup"><span data-stu-id="b51cf-128">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="b51cf-129">hello embedUrl 只是 https://embedded.powerbi.com/appTokenReportEmbed。</span><span class="sxs-lookup"><span data-stu-id="b51cf-129">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="b51cf-130">您可以使用 hello [JavaScript 報表內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)tootest 功能。</span><span class="sxs-lookup"><span data-stu-id="b51cf-130">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="b51cf-131">同時也會提供可用的 hello 不同作業的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="b51cf-131">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="b51cf-132">**NuGet 套件安裝**</span><span class="sxs-lookup"><span data-stu-id="b51cf-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="b51cf-133">**JavaScript 程式碼**</span><span class="sxs-lookup"><span data-stu-id="b51cf-133">**JavaScript code**</span></span>

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

<span data-ttu-id="b51cf-134">呼叫*powerbi.createReport()*將空白的畫布中編輯模式出現在 hello *div*項目。</span><span class="sxs-lookup"><span data-stu-id="b51cf-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within hello *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="b51cf-135">儲存新報告</span><span class="sxs-lookup"><span data-stu-id="b51cf-135">Save new reports</span></span>

<span data-ttu-id="b51cf-136">hello 報表會實際之前不會建立呼叫 hello**存**作業。</span><span class="sxs-lookup"><span data-stu-id="b51cf-136">hello report will not actually be created until you call hello **save as** operation.</span></span> <span data-ttu-id="b51cf-137">這可從 [檔案] 功能表或從 JavaScript 來進行。</span><span class="sxs-lookup"><span data-stu-id="b51cf-137">This can be done from file menu or from JavaScript.</span></span>

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
> <span data-ttu-id="b51cf-138">在呼叫**另存新檔**後，才會建立新報告。</span><span class="sxs-lookup"><span data-stu-id="b51cf-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="b51cf-139">儲存之後，hello 畫布仍將顯示 hello 資料集編輯模式和不 hello 報告中。</span><span class="sxs-lookup"><span data-stu-id="b51cf-139">After you save, hello canvas will still show hello dataset in edit mode and not hello report.</span></span> <span data-ttu-id="b51cf-140">就像任何其他報表一樣，您將需要 tooreload hello 新報表。</span><span class="sxs-lookup"><span data-stu-id="b51cf-140">You will need tooreload hello new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a><span data-ttu-id="b51cf-141">載入 hello 新報表</span><span class="sxs-lookup"><span data-stu-id="b51cf-141">Load hello new report</span></span>

<span data-ttu-id="b51cf-142">在訂單 toointeract 與 hello 新報表中，您需要 tooembed 它 hello 一樣 hello 應用程式內嵌一般報表、 意義、 新的權杖必須發出特別為 hello 新報表，然後呼叫 hello 內嵌方法。</span><span class="sxs-lookup"><span data-stu-id="b51cf-142">In order toointeract with hello new report you need tooembed it in hello same way hello application embeds a regular report, meaning, a new token must be issued specifically for hello new report and then call hello embed method.</span></span>

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a><span data-ttu-id="b51cf-143">自動儲存和載入新的報表，使用 「 儲存 」 事件的 hello</span><span class="sxs-lookup"><span data-stu-id="b51cf-143">Automate save and load of a new report using hello "saved" event</span></span>

<span data-ttu-id="b51cf-144">Tooautomate hello 程序中的 另存新檔 」 和 「 儲存 」 事件的 hello 然後載入 hello 新的報表，您可以進行使用。</span><span class="sxs-lookup"><span data-stu-id="b51cf-144">In order tooautomate hello process of "save as" and then loading hello new report you can make use of hello "saved" Event.</span></span> <span data-ttu-id="b51cf-145">Hello 儲存作業完成，且它會傳回 Json 物件，包含 hello 新 reportId、 報表名稱、 hello 舊 reportId （如果有的話），如果 hello 作業另存新檔或儲存時，會引發這個事件。</span><span class="sxs-lookup"><span data-stu-id="b51cf-145">This event is fired when hello save operation is complete and it returns a Json object containing hello new reportId, report name, hello old reportId(if there was one) and if hello operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="b51cf-146">您可以接聽 hello 「 儲存 」 事件、 使用 hello 新 reportId、 建立 hello 新權杖並與其內嵌 hello 新報表，tooAutomate hello 程序。</span><span class="sxs-lookup"><span data-stu-id="b51cf-146">tooAutomate hello process you can listen on hello "saved" event, take hello new reportId, create hello new token and embed hello new report with it.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="b51cf-147">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b51cf-147">See also</span></span>

[<span data-ttu-id="b51cf-148">開始使用範例</span><span class="sxs-lookup"><span data-stu-id="b51cf-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="b51cf-149">儲存報告</span><span class="sxs-lookup"><span data-stu-id="b51cf-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="b51cf-150">內嵌報告</span><span class="sxs-lookup"><span data-stu-id="b51cf-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="b51cf-151">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="b51cf-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="b51cf-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="b51cf-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="b51cf-153">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="b51cf-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="b51cf-154">Power BI 核心 NuGut 套件</span><span class="sxs-lookup"><span data-stu-id="b51cf-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="b51cf-155">Power BI JavaScript 套件</span><span class="sxs-lookup"><span data-stu-id="b51cf-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="b51cf-156">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="b51cf-156">More questions?</span></span> [<span data-ttu-id="b51cf-157">再試一次 hello Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="b51cf-157">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

---
title: "在 Azure Power BI Embedded 中從資料集建立新的報告 | Microsoft Docs"
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
ms.openlocfilehash: 457f53aa76059dbb2faed6b264102f1f59b9918a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="a80a2-103">在 Power BI Embedded 中從資料集建立新的報告</span><span class="sxs-lookup"><span data-stu-id="a80a2-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="a80a2-104">您現在可以在自己的應用程式中從資料集建立 Power BI Embedded 報告。</span><span class="sxs-lookup"><span data-stu-id="a80a2-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="a80a2-105">其驗證方法類似內嵌報告所用的方法，</span><span class="sxs-lookup"><span data-stu-id="a80a2-105">The authentication method is similar to that of report embed.</span></span> <span data-ttu-id="a80a2-106">會以資料集特有的存取權杖為基礎。</span><span class="sxs-lookup"><span data-stu-id="a80a2-106">It is based on access tokens that are specific to a dataset.</span></span> <span data-ttu-id="a80a2-107">用於 PowerBI.com 的權杖是由 Azure Active Directory (AAD) 核發，Power BI Embedded 權杖則是由您自己的服務核發。</span><span class="sxs-lookup"><span data-stu-id="a80a2-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="a80a2-108">在建立 Embedded 報告時，權杖會針對特定資料集來核發。</span><span class="sxs-lookup"><span data-stu-id="a80a2-108">When createing an Embedded report, the tokens issued are for a specific dataset.</span></span> <span data-ttu-id="a80a2-109">權杖應該與相同元素上的內嵌 URL 相關聯，以確保每個項目都有獨一無二的權杖。</span><span class="sxs-lookup"><span data-stu-id="a80a2-109">Tokens should be associated with the embed URL on the same element to ensure each has a unique token.</span></span> <span data-ttu-id="a80a2-110">若要建立 Embedded 報告，則必須在存取權杖中提供 Dataset.Read 和 Workspace.Report.Create 範圍。</span><span class="sxs-lookup"><span data-stu-id="a80a2-110">In order to create an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in the access token.</span></span>

## <a name="create-access-token-needed-to-create-new-report"></a><span data-ttu-id="a80a2-111">建立所需的存取權杖來建立新的報告</span><span class="sxs-lookup"><span data-stu-id="a80a2-111">Create access token needed to create new report</span></span>

<span data-ttu-id="a80a2-112">Power BI Embedded 使用內嵌權杖，這是 HMAC 簽署的 JSON Web 權杖。</span><span class="sxs-lookup"><span data-stu-id="a80a2-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="a80a2-113">權杖會使用來自 Azure Power BI Embedded 工作區集合的存取金鑰進行簽署。</span><span class="sxs-lookup"><span data-stu-id="a80a2-113">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="a80a2-114">內嵌權杖依預設可用來提供要內嵌至應用程式之報告的唯讀存取權。</span><span class="sxs-lookup"><span data-stu-id="a80a2-114">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="a80a2-115">內嵌權杖會針對特定報告來核發，而且應該與內嵌 URL 相關聯。</span><span class="sxs-lookup"><span data-stu-id="a80a2-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="a80a2-116">存取權杖應該建立在伺服器上，因為會使用存取金鑰來簽署/加密權杖。</span><span class="sxs-lookup"><span data-stu-id="a80a2-116">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="a80a2-117">如需如何建立存取權杖的相關資訊，請參閱[使用 Power BI Embedded 驗證和授權](power-bi-embedded-app-token-flow.md)。</span><span class="sxs-lookup"><span data-stu-id="a80a2-117">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="a80a2-118">您也可以檢閱 [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) 方法。</span><span class="sxs-lookup"><span data-stu-id="a80a2-118">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="a80a2-119">以下是使用 .NET SDK for Power BI 時此方法所呈現樣貌的範例。</span><span class="sxs-lookup"><span data-stu-id="a80a2-119">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="a80a2-120">在此範例中，我們有想要用來建立新報告的資料集識別碼。</span><span class="sxs-lookup"><span data-stu-id="a80a2-120">In this example, we have our dataset id that we want to creat the new report on.</span></span> <span data-ttu-id="a80a2-121">我們也需要新增 Dataset.Read 和 Workspace.Report.Create 的範圍。</span><span class="sxs-lookup"><span data-stu-id="a80a2-121">We also need to add the scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="a80a2-122">要使用 PowerBIToken 類別，您必須安裝 [Power BI 核心 NuGut 套件](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)。</span><span class="sxs-lookup"><span data-stu-id="a80a2-122">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="a80a2-123">**NuGet 套件安裝**</span><span class="sxs-lookup"><span data-stu-id="a80a2-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="a80a2-124">**C# 程式碼**</span><span class="sxs-lookup"><span data-stu-id="a80a2-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="a80a2-125">建立新的空白報告</span><span class="sxs-lookup"><span data-stu-id="a80a2-125">Create a new blank report</span></span>

<span data-ttu-id="a80a2-126">若要建立新報告，請提供建立組態。</span><span class="sxs-lookup"><span data-stu-id="a80a2-126">In order to create a new report, the create configuration should be provided.</span></span> <span data-ttu-id="a80a2-127">這應該包括存取權杖、embedURL 和我們想要用來建立報告的 datasetID。</span><span class="sxs-lookup"><span data-stu-id="a80a2-127">This should include the access token, the embedURL and the datasetID that we want to create the report against.</span></span> <span data-ttu-id="a80a2-128">這需要您安裝 NuGet [Power BI JavaScript 套件](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)。</span><span class="sxs-lookup"><span data-stu-id="a80a2-128">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="a80a2-129">embedUrl 會是 https://embedded.powerbi.com/appTokenReportEmbed。</span><span class="sxs-lookup"><span data-stu-id="a80a2-129">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="a80a2-130">您可以使用 [JavaScript 報告內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)來測試功能。</span><span class="sxs-lookup"><span data-stu-id="a80a2-130">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="a80a2-131">它也會提供可用之不同作業的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="a80a2-131">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="a80a2-132">**NuGet 套件安裝**</span><span class="sxs-lookup"><span data-stu-id="a80a2-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="a80a2-133">**JavaScript 程式碼**</span><span class="sxs-lookup"><span data-stu-id="a80a2-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="a80a2-134">呼叫 powerbi.createReport() 會讓編輯模式的空白畫布出現在 div 元素內。</span><span class="sxs-lookup"><span data-stu-id="a80a2-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within the *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="a80a2-135">儲存新報告</span><span class="sxs-lookup"><span data-stu-id="a80a2-135">Save new reports</span></span>

<span data-ttu-id="a80a2-136">在您呼叫**另存新檔**作業後，才會實際建立報告。</span><span class="sxs-lookup"><span data-stu-id="a80a2-136">The report will not actually be created until you call the **save as** operation.</span></span> <span data-ttu-id="a80a2-137">這可從 [檔案] 功能表或從 JavaScript 來進行。</span><span class="sxs-lookup"><span data-stu-id="a80a2-137">This can be done from file menu or from JavaScript.</span></span>

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
> <span data-ttu-id="a80a2-138">在呼叫**另存新檔**後，才會建立新報告。</span><span class="sxs-lookup"><span data-stu-id="a80a2-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="a80a2-139">儲存之後，畫布仍會顯示編輯模式的資料集，而非報告。</span><span class="sxs-lookup"><span data-stu-id="a80a2-139">After you save, the canvas will still show the dataset in edit mode and not the report.</span></span> <span data-ttu-id="a80a2-140">您必須像處理任何其他報告一樣，重新載入新的報告。</span><span class="sxs-lookup"><span data-stu-id="a80a2-140">You will need to reload the new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a><span data-ttu-id="a80a2-141">載入新報告</span><span class="sxs-lookup"><span data-stu-id="a80a2-141">Load the new report</span></span>

<span data-ttu-id="a80a2-142">若要與新報告互動，您必須利用和應用程式內嵌一般報告相同的方式，將新報告內嵌，也就是說，必須特別為新報告核發新權杖，然後呼叫內嵌方法。</span><span class="sxs-lookup"><span data-stu-id="a80a2-142">In order to interact with the new report you need to embed it in the same way the application embeds a regular report, meaning, a new token must be issued specifically for the new report and then call the embed method.</span></span>

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

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a><span data-ttu-id="a80a2-143">使用「已儲存」的事件自動儲存和載入新報告</span><span class="sxs-lookup"><span data-stu-id="a80a2-143">Automate save and load of a new report using the "saved" event</span></span>

<span data-ttu-id="a80a2-144">若要自動進行「另存新檔」的程序，然後載入新報告，您可以利用「已儲存」的事件。</span><span class="sxs-lookup"><span data-stu-id="a80a2-144">In order to automate the process of "save as" and then loading the new report you can make use of the "saved" Event.</span></span> <span data-ttu-id="a80a2-145">這個事件的引發條件為：儲存作業完成，並傳回包含新 reportId、報告名稱、舊 reportId (如果有的話) 的 Json 物件，而且如果該作業是另存新檔或儲存時。</span><span class="sxs-lookup"><span data-stu-id="a80a2-145">This event is fired when the save operation is complete and it returns a Json object containing the new reportId, report name, the old reportId(if there was one) and if the operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="a80a2-146">若要自動進行程序，您可以接聽「已儲存」的事件、取得新 reportId、建立新權杖，然後將新報告內嵌在其中。</span><span class="sxs-lookup"><span data-stu-id="a80a2-146">To Automate the process you can listen on the "saved" event, take the new reportId, create the new token and embed the new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints to Log window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that the application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide the wanted scopes*/);
        
        
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

## <a name="see-also"></a><span data-ttu-id="a80a2-147">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a80a2-147">See also</span></span>

[<span data-ttu-id="a80a2-148">開始使用範例</span><span class="sxs-lookup"><span data-stu-id="a80a2-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="a80a2-149">儲存報告</span><span class="sxs-lookup"><span data-stu-id="a80a2-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="a80a2-150">內嵌報告</span><span class="sxs-lookup"><span data-stu-id="a80a2-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="a80a2-151">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="a80a2-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="a80a2-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="a80a2-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="a80a2-153">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="a80a2-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="a80a2-154">Power BI 核心 NuGut 套件</span><span class="sxs-lookup"><span data-stu-id="a80a2-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="a80a2-155">Power BI JavaScript 套件</span><span class="sxs-lookup"><span data-stu-id="a80a2-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="a80a2-156">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="a80a2-156">More questions?</span></span> [<span data-ttu-id="a80a2-157">試用 Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="a80a2-157">Try the Power BI Community</span></span>](http://community.powerbi.com/)
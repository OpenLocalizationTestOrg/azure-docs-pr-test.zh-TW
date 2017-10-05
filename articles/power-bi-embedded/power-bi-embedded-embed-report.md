---
title: "將報告內嵌在 Azure Power BI Embedded | Microsoft Docs"
description: "了解如何將 Power BI Embedded 中的報告內嵌到您的應用程式。"
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
ms.openlocfilehash: 3d865af2418c9c557c861a379766a125d75cebf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="1f2f3-103">將報告內嵌在 Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="1f2f3-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="1f2f3-104">了解如何將 Power BI Embedded 中的報告內嵌到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-104">Learn how to embed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="1f2f3-105">我們將探討如何將報告實際內嵌到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-105">We will look at how to actually embed a report into your application.</span></span> <span data-ttu-id="1f2f3-106">本文假設您在工作區集合的某個工作區內已存有報告。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="1f2f3-107">如果您尚未完成該步驟，請參閱[開始使用 Power BI Embedded](power-bi-embedded-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="1f2f3-108">您可以使用 .NET (C#) 或 Node.js SDK 以及 JavaScript 來輕鬆建置含有 Power BI Embedded 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-108">You can use the .NET (C#) or Node.js SDK, along with JavaScript, to easily build your application with Power BI Embedded.</span></span> 

## <a name="using-the-access-keys-to-use-rest-apis"></a><span data-ttu-id="1f2f3-109">使用存取金鑰來使用 REST API</span><span class="sxs-lookup"><span data-stu-id="1f2f3-109">Using the access keys to use REST APIs</span></span>

<span data-ttu-id="1f2f3-110">若要呼叫 REST API，您可以傳遞給定工作區集合的存取金鑰 (可從 Azure 入口網站取得)。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-110">In order to call the REST API, you can pass the access key which you can get from the Azure portal for a given workspace collection.</span></span> <span data-ttu-id="1f2f3-111">如需詳細資訊，請參閱[開始使用 Power BI Embedded](power-bi-embedded-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="1f2f3-112">取得報告識別碼</span><span class="sxs-lookup"><span data-stu-id="1f2f3-112">Get a report id</span></span>

<span data-ttu-id="1f2f3-113">每個存取權杖都會以報告為基礎。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-113">Every access token is based on a report.</span></span> <span data-ttu-id="1f2f3-114">您必須針對想要內嵌的報告取得給定的報告識別碼。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-114">You will need to get the given report id for the report that you want to embed.</span></span> <span data-ttu-id="1f2f3-115">這可以根據[取得報告](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API 的呼叫來完成。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-115">This can be done based on calls to the [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="1f2f3-116">這會傳回報告識別碼和內嵌 URL。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-116">This will return the report id and the embed url.</span></span> <span data-ttu-id="1f2f3-117">這可以使用 Power BI .NET SDK 或直接呼叫 REST API 來完成。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-117">This can be done using the Power BI .NET SDK or calling the REST API directly.</span></span>

### <a name="using-the-power-bi-net-sdk"></a><span data-ttu-id="1f2f3-118">使用 Power BI .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1f2f3-118">Using the Power BI .NET SDK</span></span>

<span data-ttu-id="1f2f3-119">在使用 .NET SDK 時，您必須建立以取自 Azure 入口網站的存取金鑰為基礎的權杖認證。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-119">When using the .NET SDK, you will need to create a token credential which is based on the access key you get from the Azure portal.</span></span> <span data-ttu-id="1f2f3-120">這需要您安裝 [Power BI API NuGet 套件](https://www.nuget.org/profiles/powerbi)。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-120">This requires that you install the [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="1f2f3-121">**NuGet 套件安裝**</span><span class="sxs-lookup"><span data-stu-id="1f2f3-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="1f2f3-122">**C# 程式碼**</span><span class="sxs-lookup"><span data-stu-id="1f2f3-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select the report that you want to work with from the collection of reports.
```

### <a name="calling-the-rest-api-directly"></a><span data-ttu-id="1f2f3-123">直接呼叫 REST API</span><span class="sxs-lookup"><span data-stu-id="1f2f3-123">Calling the REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response to get the report you want to work with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="1f2f3-124">建立存取權杖</span><span class="sxs-lookup"><span data-stu-id="1f2f3-124">Create an access token</span></span>

<span data-ttu-id="1f2f3-125">Power BI Embedded 使用內嵌權杖，這是 HMAC 簽署的 JSON Web 權杖。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="1f2f3-126">權杖會使用來自 Azure Power BI Embedded 工作區集合的存取金鑰進行簽署。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-126">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="1f2f3-127">內嵌權杖依預設可用來提供要內嵌至應用程式之報告的唯讀存取權。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-127">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="1f2f3-128">內嵌權杖會針對特定報告來核發，而且應該與內嵌 URL 相關聯。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="1f2f3-129">存取權杖應該建立在伺服器上，因為會使用存取金鑰來簽署/加密權杖。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-129">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="1f2f3-130">如需如何建立存取權杖的相關資訊，請參閱[使用 Power BI Embedded 驗證和授權](power-bi-embedded-app-token-flow.md)。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-130">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="1f2f3-131">您也可以檢閱 [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) 方法。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-131">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="1f2f3-132">以下是使用 .NET SDK for Power BI 時此方法所呈現樣貌的範例。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-132">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="1f2f3-133">您會使用先前擷取到的報告識別碼。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-133">You will use the report id that you retrieved earlier.</span></span> <span data-ttu-id="1f2f3-134">建立了內嵌權杖後，您接著會使用存取金鑰來產生可從 JavaScript 觀點來使用的權杖。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-134">Once the embed token is created, you will then use the access key to generate the token which you can use from the javascript perspective.</span></span> <span data-ttu-id="1f2f3-135">要使用 PowerBIToken 類別，您必須安裝 [Power BI 核心 NuGut 套件](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-135">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="1f2f3-136">**NuGet 套件安裝**</span><span class="sxs-lookup"><span data-stu-id="1f2f3-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="1f2f3-137">**C# 程式碼**</span><span class="sxs-lookup"><span data-stu-id="1f2f3-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-to-embed-tokens"></a><span data-ttu-id="1f2f3-138">在內嵌權杖新增權限範圍</span><span class="sxs-lookup"><span data-stu-id="1f2f3-138">Adding permission scopes to embed tokens</span></span>

<span data-ttu-id="1f2f3-139">在使用內嵌權杖時，您可能會想限制您授與了存取權之資源的使用量。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-139">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="1f2f3-140">為此，您可以產生具有範圍權限的權杖。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="1f2f3-141">如需詳細資訊，請參閱[範圍](power-bi-embedded-app-token-flow.md#scopes)</span><span class="sxs-lookup"><span data-stu-id="1f2f3-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="1f2f3-142">使用 JavaScript 進行內嵌</span><span class="sxs-lookup"><span data-stu-id="1f2f3-142">Embed using JavaScript</span></span>

<span data-ttu-id="1f2f3-143">擁有存取權杖和報告識別碼後，我們可以使用 JavaScript 來內嵌報告。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-143">After you have the access token and the report id, we can embed the report using JavaScript.</span></span> <span data-ttu-id="1f2f3-144">這需要您安裝 NuGet [Power BI JavaScript 套件](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-144">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="1f2f3-145">embedUrl 會是 https://embedded.powerbi.com/appTokenReportEmbed。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-145">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="1f2f3-146">您可以使用 [JavaScript 報告內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)來測試功能。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-146">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="1f2f3-147">它也會提供可用之不同作業的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-147">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="1f2f3-148">**NuGet 套件安裝**</span><span class="sxs-lookup"><span data-stu-id="1f2f3-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="1f2f3-149">**JavaScript 程式碼**</span><span class="sxs-lookup"><span data-stu-id="1f2f3-149">**JavaScript code**</span></span>

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

### <a name="set-the-size-of-embedded-elements"></a><span data-ttu-id="1f2f3-150">設定內嵌元素大小</span><span class="sxs-lookup"><span data-stu-id="1f2f3-150">Set the size of embedded elements</span></span>

<span data-ttu-id="1f2f3-151">報告會根據其容器的大小自動內嵌。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-151">The report will automatically be embedded based on the size of its container.</span></span> <span data-ttu-id="1f2f3-152">若要覆寫預設的內嵌大小，只需新增 CSS 類別屬性或寬度和高度的內嵌樣式即可。</span><span class="sxs-lookup"><span data-stu-id="1f2f3-152">To override the default size of the embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="1f2f3-153">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1f2f3-153">See also</span></span>

[<span data-ttu-id="1f2f3-154">開始使用範例</span><span class="sxs-lookup"><span data-stu-id="1f2f3-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="1f2f3-155">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="1f2f3-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="1f2f3-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="1f2f3-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="1f2f3-157">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="1f2f3-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="1f2f3-158">Power BI JavaScript 套件</span><span class="sxs-lookup"><span data-stu-id="1f2f3-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="1f2f3-159">[Power BI API NuGet 套件](https://www.nuget.org/profiles/powerbi)
[Power BI 核心 NuGut 套件](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="1f2f3-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="1f2f3-160">PowerBI-CSharp Git 存放庫</span><span class="sxs-lookup"><span data-stu-id="1f2f3-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="1f2f3-161">PowerBI-Node Git存放庫</span><span class="sxs-lookup"><span data-stu-id="1f2f3-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="1f2f3-162">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="1f2f3-162">More questions?</span></span> [<span data-ttu-id="1f2f3-163">試用 Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="1f2f3-163">Try the Power BI Community</span></span>](http://community.powerbi.com/)

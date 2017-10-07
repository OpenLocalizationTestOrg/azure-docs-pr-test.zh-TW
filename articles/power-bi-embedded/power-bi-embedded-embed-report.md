---
title: "報表中 Azure Power BI Embedded aaaEmbed |Microsoft 文件"
description: "深入了解如何 tooembed 到您的應用程式是在 Power BI Embedded 的報表。"
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
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="ec541-103">將報告內嵌在 Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="ec541-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="ec541-104">深入了解如何 tooembed 到您的應用程式是在 Power BI Embedded 的報表。</span><span class="sxs-lookup"><span data-stu-id="ec541-104">Learn how tooembed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="ec541-105">我們將探討如何 tooactually 將報表內嵌到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec541-105">We will look at how tooactually embed a report into your application.</span></span> <span data-ttu-id="ec541-106">本文假設您在工作區集合的某個工作區內已存有報告。</span><span class="sxs-lookup"><span data-stu-id="ec541-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="ec541-107">如果您尚未完成該步驟，請參閱[開始使用 Power BI Embedded](power-bi-embedded-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ec541-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="ec541-108">您可以使用 hello.NET (C#) 或 Node.js SDK，以及 JavaScript、 tooeasily 建置使用 Power BI Embedded 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec541-108">You can use hello .NET (C#) or Node.js SDK, along with JavaScript, tooeasily build your application with Power BI Embedded.</span></span> 

## <a name="using-hello-access-keys-toouse-rest-apis"></a><span data-ttu-id="ec541-109">使用 hello 存取金鑰 toouse REST Api</span><span class="sxs-lookup"><span data-stu-id="ec541-109">Using hello access keys toouse REST APIs</span></span>

<span data-ttu-id="ec541-110">在順序 toocall hello REST API，您可以傳遞 hello 存取金鑰，您可以取得 hello Azure 入口網站指定的工作區集合。</span><span class="sxs-lookup"><span data-stu-id="ec541-110">In order toocall hello REST API, you can pass hello access key which you can get from hello Azure portal for a given workspace collection.</span></span> <span data-ttu-id="ec541-111">如需詳細資訊，請參閱[開始使用 Power BI Embedded](power-bi-embedded-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ec541-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="ec541-112">取得報告識別碼</span><span class="sxs-lookup"><span data-stu-id="ec541-112">Get a report id</span></span>

<span data-ttu-id="ec541-113">每個存取權杖都會以報告為基礎。</span><span class="sxs-lookup"><span data-stu-id="ec541-113">Every access token is based on a report.</span></span> <span data-ttu-id="ec541-114">您必須指定您想 tooembed hello 報表的報表 id tooget hello。</span><span class="sxs-lookup"><span data-stu-id="ec541-114">You will need tooget hello given report id for hello report that you want tooembed.</span></span> <span data-ttu-id="ec541-115">這可以根據呼叫 toohello[取得報表](https://msdn.microsoft.com/library/azure/mt711510.aspx)REST API。</span><span class="sxs-lookup"><span data-stu-id="ec541-115">This can be done based on calls toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="ec541-116">這會傳回識別碼和 hello 內嵌 url 的 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="ec541-116">This will return hello report id and hello embed url.</span></span> <span data-ttu-id="ec541-117">這可以使用 Power BI.NET SDK hello 或直接呼叫 hello REST API。</span><span class="sxs-lookup"><span data-stu-id="ec541-117">This can be done using hello Power BI .NET SDK or calling hello REST API directly.</span></span>

### <a name="using-hello-power-bi-net-sdk"></a><span data-ttu-id="ec541-118">使用 Power BI.NET SDK hello</span><span class="sxs-lookup"><span data-stu-id="ec541-118">Using hello Power BI .NET SDK</span></span>

<span data-ttu-id="ec541-119">當使用 hello.NET SDK，您必須 toocreate hello 存取金鑰，您會收到 hello Azure 入口網站為基礎的權杖認證。</span><span class="sxs-lookup"><span data-stu-id="ec541-119">When using hello .NET SDK, you will need toocreate a token credential which is based on hello access key you get from hello Azure portal.</span></span> <span data-ttu-id="ec541-120">這需要您安裝 hello [Power BI API NuGet 套件](https://www.nuget.org/profiles/powerbi)。</span><span class="sxs-lookup"><span data-stu-id="ec541-120">This requires that you install hello [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="ec541-121">**NuGet 套件安裝**</span><span class="sxs-lookup"><span data-stu-id="ec541-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="ec541-122">**C# 程式碼**</span><span class="sxs-lookup"><span data-stu-id="ec541-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a><span data-ttu-id="ec541-123">呼叫 hello REST API 直接</span><span class="sxs-lookup"><span data-stu-id="ec541-123">Calling hello REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="ec541-124">建立存取權杖</span><span class="sxs-lookup"><span data-stu-id="ec541-124">Create an access token</span></span>

<span data-ttu-id="ec541-125">Power BI Embedded 使用內嵌權杖，這是 HMAC 簽署的 JSON Web 權杖。</span><span class="sxs-lookup"><span data-stu-id="ec541-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="ec541-126">hello 權杖會簽署與 hello 便捷鍵，從 Azure Power BI Embedded 的工作區集合。</span><span class="sxs-lookup"><span data-stu-id="ec541-126">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="ec541-127">內嵌語彙基元，根據預設，會讀取使用的 tooprovide 只能存取 tooa 報表 tooembed 到應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec541-127">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="ec541-128">內嵌權杖會針對特定報告來核發，而且應該與內嵌 URL 相關聯。</span><span class="sxs-lookup"><span data-stu-id="ec541-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="ec541-129">使用 toosign/加密 hello 語彙基元 hello 便捷鍵時，應該 hello 伺服器上建立存取權杖。</span><span class="sxs-lookup"><span data-stu-id="ec541-129">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="ec541-130">如需詳細資訊 toocreate 存取權杖，請參閱[驗證和授權使用 Power BI Embedded](power-bi-embedded-app-token-flow.md)。</span><span class="sxs-lookup"><span data-stu-id="ec541-130">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="ec541-131">您也可以檢閱 hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)方法。</span><span class="sxs-lookup"><span data-stu-id="ec541-131">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="ec541-132">這會看起來像用於 Power BI 中的 hello.NET SDK 的範例如下。</span><span class="sxs-lookup"><span data-stu-id="ec541-132">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="ec541-133">您將使用您先前擷取的 hello 報表識別碼。</span><span class="sxs-lookup"><span data-stu-id="ec541-133">You will use hello report id that you retrieved earlier.</span></span> <span data-ttu-id="ec541-134">Hello 內嵌在建立權杖，您將使用 hello 存取金鑰 toogenerate hello 權杖從 hello javascript 觀點來看，您可以使用。</span><span class="sxs-lookup"><span data-stu-id="ec541-134">Once hello embed token is created, you will then use hello access key toogenerate hello token which you can use from hello javascript perspective.</span></span> <span data-ttu-id="ec541-135">hello *PowerBIToken 類別*需要您安裝 hello [Power BI 核心 NuGut 封裝](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)。</span><span class="sxs-lookup"><span data-stu-id="ec541-135">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="ec541-136">**NuGet 套件安裝**</span><span class="sxs-lookup"><span data-stu-id="ec541-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="ec541-137">**C# 程式碼**</span><span class="sxs-lookup"><span data-stu-id="ec541-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a><span data-ttu-id="ec541-138">新增權限範圍 tooembed 權杖</span><span class="sxs-lookup"><span data-stu-id="ec541-138">Adding permission scopes tooembed tokens</span></span>

<span data-ttu-id="ec541-139">當使用內嵌語彙基元時，您可能想 hello 資源存取權給予 toorestrict 使用量。</span><span class="sxs-lookup"><span data-stu-id="ec541-139">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="ec541-140">為此，您可以產生具有範圍權限的權杖。</span><span class="sxs-lookup"><span data-stu-id="ec541-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="ec541-141">如需詳細資訊，請參閱[範圍](power-bi-embedded-app-token-flow.md#scopes)</span><span class="sxs-lookup"><span data-stu-id="ec541-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="ec541-142">使用 JavaScript 進行內嵌</span><span class="sxs-lookup"><span data-stu-id="ec541-142">Embed using JavaScript</span></span>

<span data-ttu-id="ec541-143">您擁有 hello 存取權杖和 hello 報表識別碼之後，我們可以將內嵌 hello 報表使用 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="ec541-143">After you have hello access token and hello report id, we can embed hello report using JavaScript.</span></span> <span data-ttu-id="ec541-144">這需要您安裝 hello nuget [Power BI JavaScript 封裝](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)。</span><span class="sxs-lookup"><span data-stu-id="ec541-144">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="ec541-145">hello embedUrl 只是 https://embedded.powerbi.com/appTokenReportEmbed。</span><span class="sxs-lookup"><span data-stu-id="ec541-145">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="ec541-146">您可以使用 hello [JavaScript 報表內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)tootest 功能。</span><span class="sxs-lookup"><span data-stu-id="ec541-146">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="ec541-147">同時也會提供可用的 hello 不同作業的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ec541-147">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="ec541-148">**NuGet 套件安裝**</span><span class="sxs-lookup"><span data-stu-id="ec541-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="ec541-149">**JavaScript 程式碼**</span><span class="sxs-lookup"><span data-stu-id="ec541-149">**JavaScript code**</span></span>

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

### <a name="set-hello-size-of-embedded-elements"></a><span data-ttu-id="ec541-150">設定內嵌元素 hello 大小</span><span class="sxs-lookup"><span data-stu-id="ec541-150">Set hello size of embedded elements</span></span>

<span data-ttu-id="ec541-151">hello 報表將自動內嵌根據 hello 其容器的大小。</span><span class="sxs-lookup"><span data-stu-id="ec541-151">hello report will automatically be embedded based on hello size of its container.</span></span> <span data-ttu-id="ec541-152">只要內嵌 hello toooverride hello 預設大小加入 CSS 類別屬性或內嵌樣式的寬度和高度。</span><span class="sxs-lookup"><span data-stu-id="ec541-152">toooverride hello default size of hello embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="ec541-153">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ec541-153">See also</span></span>

[<span data-ttu-id="ec541-154">開始使用範例</span><span class="sxs-lookup"><span data-stu-id="ec541-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="ec541-155">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="ec541-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="ec541-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="ec541-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="ec541-157">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="ec541-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="ec541-158">Power BI JavaScript 套件</span><span class="sxs-lookup"><span data-stu-id="ec541-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="ec541-159">[Power BI API NuGet 套件](https://www.nuget.org/profiles/powerbi)
[Power BI 核心 NuGut 套件](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="ec541-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="ec541-160">PowerBI-CSharp Git 存放庫</span><span class="sxs-lookup"><span data-stu-id="ec541-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="ec541-161">PowerBI-Node Git存放庫</span><span class="sxs-lookup"><span data-stu-id="ec541-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="ec541-162">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="ec541-162">More questions?</span></span> [<span data-ttu-id="ec541-163">再試一次 hello Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="ec541-163">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

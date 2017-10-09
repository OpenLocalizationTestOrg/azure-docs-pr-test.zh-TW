---
title: "aaaAuthenticating 並向 Power BI Embedded 授權"
description: "使用 Power BI Embedded 驗證和授權"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="4064a-103">使用 Power BI Embedded 驗證和授權</span><span class="sxs-lookup"><span data-stu-id="4064a-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="4064a-104">hello 內嵌 Power BI 服務會使用**金鑰**和**應用程式權杖**進行驗證和授權，而不要使用明確的使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="4064a-104">hello Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="4064a-105">在此模型中，您的應用程式會管理使用者的驗證與授權。</span><span class="sxs-lookup"><span data-stu-id="4064a-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="4064a-106">必要時，您的應用程式會建立，並傳送 hello 應用程式權杖，告訴我們服務 toorender hello 要求的報表。</span><span class="sxs-lookup"><span data-stu-id="4064a-106">When necessary, your app creates and sends hello App Tokens that tells our service toorender hello requested report.</span></span> <span data-ttu-id="4064a-107">這項設計並不需要您的應用程式 toouse Azure Active Directory 進行使用者驗證和授權，雖然您仍然可以。</span><span class="sxs-lookup"><span data-stu-id="4064a-107">This design doesn't require your app toouse Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-tooauthenticate"></a><span data-ttu-id="4064a-108">兩種方式 tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="4064a-108">Two ways tooauthenticate</span></span>

<span data-ttu-id="4064a-109">**金鑰** - 您可以針對所有 Power BI Embedded REST API 呼叫使用金鑰。</span><span class="sxs-lookup"><span data-stu-id="4064a-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="4064a-110">hello 金鑰可以在 hello **Azure 入口網站**按一下**所有設定**然後**存取金鑰**。</span><span class="sxs-lookup"><span data-stu-id="4064a-110">hello keys can be found in hello **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="4064a-111">一律將您的金鑰視為密碼。</span><span class="sxs-lookup"><span data-stu-id="4064a-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="4064a-112">這些有特定的工作區集合呼叫任何 REST API 的權限 toomake。</span><span class="sxs-lookup"><span data-stu-id="4064a-112">These keys have permissions toomake any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="4064a-113">toouse 在 REST 呼叫的索引鍵新增下列授權標頭的 hello:</span><span class="sxs-lookup"><span data-stu-id="4064a-113">toouse a key on a REST call, add hello following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="4064a-114">**應用程式權杖** - 應用程式權杖用於所有內嵌的要求。</span><span class="sxs-lookup"><span data-stu-id="4064a-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="4064a-115">它們是設計的 toobe 執行用戶端，所以限制 tooa 單一報表和它的最佳作法 tooset 到期時間。</span><span class="sxs-lookup"><span data-stu-id="4064a-115">They’re designed toobe run client-side, so they're restricted tooa single report and it’s best practice tooset an expiration time.</span></span>

<span data-ttu-id="4064a-116">應用程式權杖是 JWT (JSON Web 權杖)，由您的其中一個金鑰簽署。</span><span class="sxs-lookup"><span data-stu-id="4064a-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="4064a-117">您的應用程式的權杖可以包含下列宣告 hello:</span><span class="sxs-lookup"><span data-stu-id="4064a-117">Your app token can contain hello following claims:</span></span>

| <span data-ttu-id="4064a-118">宣告</span><span class="sxs-lookup"><span data-stu-id="4064a-118">Claim</span></span> | <span data-ttu-id="4064a-119">說明</span><span class="sxs-lookup"><span data-stu-id="4064a-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4064a-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="4064a-120">**ver**</span></span> |<span data-ttu-id="4064a-121">hello hello 應用程式權杖版本。</span><span class="sxs-lookup"><span data-stu-id="4064a-121">hello version of hello app token.</span></span> <span data-ttu-id="4064a-122">0.2.0 是 hello 目前版本。</span><span class="sxs-lookup"><span data-stu-id="4064a-122">0.2.0 is hello current version.</span></span> |
| <span data-ttu-id="4064a-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="4064a-123">**aud**</span></span> |<span data-ttu-id="4064a-124">hello 預期收件者的 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="4064a-124">hello intended recipient of hello token.</span></span> <span data-ttu-id="4064a-125">對於 Power BI Embedded，使用：“https://analysis.windows.net/powerbi/api”。</span><span class="sxs-lookup"><span data-stu-id="4064a-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="4064a-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="4064a-126">**iss**</span></span> |<span data-ttu-id="4064a-127">字串，表示權杖 hello hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4064a-127">A string indicating hello application which issued hello token.</span></span> |
| <span data-ttu-id="4064a-128">**type**</span><span class="sxs-lookup"><span data-stu-id="4064a-128">**type**</span></span> |<span data-ttu-id="4064a-129">正在建立的應用程式語彙基元 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="4064a-129">hello type of app token which is being created.</span></span> <span data-ttu-id="4064a-130">目前僅支援 hello 類型是**內嵌**。</span><span class="sxs-lookup"><span data-stu-id="4064a-130">Current hello only supported type is **embed**.</span></span> |
| <span data-ttu-id="4064a-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="4064a-131">**wcn**</span></span> |<span data-ttu-id="4064a-132">工作區集合名稱 hello 語彙基元所發出。</span><span class="sxs-lookup"><span data-stu-id="4064a-132">Workspace collection name hello token is being issued for.</span></span> |
| <span data-ttu-id="4064a-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="4064a-133">**wid**</span></span> |<span data-ttu-id="4064a-134">工作區識別碼 hello 語彙基元所發出。</span><span class="sxs-lookup"><span data-stu-id="4064a-134">Workspace ID hello token is being issued for.</span></span> |
| <span data-ttu-id="4064a-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="4064a-135">**rid**</span></span> |<span data-ttu-id="4064a-136">報表識別碼 hello 語彙基元所發出。</span><span class="sxs-lookup"><span data-stu-id="4064a-136">Report ID hello token is being issued for.</span></span> |
| <span data-ttu-id="4064a-137">**username** (選擇性)</span><span class="sxs-lookup"><span data-stu-id="4064a-137">**username** (optional)</span></span> |<span data-ttu-id="4064a-138">這是字串，可協助您識別 hello 使用者套用 RLS 規則時使用 rls。</span><span class="sxs-lookup"><span data-stu-id="4064a-138">Used with RLS, this is a string that can help identify hello user when applying RLS rules.</span></span> |
| <span data-ttu-id="4064a-139">**角色** (選擇性)</span><span class="sxs-lookup"><span data-stu-id="4064a-139">**roles** (optional)</span></span> |<span data-ttu-id="4064a-140">字串，包含 hello 角色 tooselect 套用資料列層級安全性規則時。</span><span class="sxs-lookup"><span data-stu-id="4064a-140">A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="4064a-141">如果傳遞多個角色，應該將它們傳遞為字串陣列。</span><span class="sxs-lookup"><span data-stu-id="4064a-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="4064a-142">**scp** (選擇性)</span><span class="sxs-lookup"><span data-stu-id="4064a-142">**scp** (optional)</span></span> |<span data-ttu-id="4064a-143">字串，包含 hello 權限範圍。</span><span class="sxs-lookup"><span data-stu-id="4064a-143">A string containing hello permissions scopes.</span></span> <span data-ttu-id="4064a-144">如果傳遞多個角色，應該將它們傳遞為字串陣列。</span><span class="sxs-lookup"><span data-stu-id="4064a-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="4064a-145">**exp** (選擇性)</span><span class="sxs-lookup"><span data-stu-id="4064a-145">**exp** (optional)</span></span> |<span data-ttu-id="4064a-146">指出 hello 時間中的 hello token 會過期。</span><span class="sxs-lookup"><span data-stu-id="4064a-146">Indicates hello time in which hello token will expire.</span></span> <span data-ttu-id="4064a-147">這些項目應該傳遞為 Unix 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="4064a-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="4064a-148">**nbf** (選擇性)</span><span class="sxs-lookup"><span data-stu-id="4064a-148">**nbf** (optional)</span></span> |<span data-ttu-id="4064a-149">指出在哪些 hello 語彙基元開始生效時的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="4064a-149">Indicates hello time in which hello token starts being valid.</span></span> <span data-ttu-id="4064a-150">這些項目應該傳遞為 Unix 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="4064a-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="4064a-151">範例應用程式權杖看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="4064a-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="4064a-152">解碼時，看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="4064a-152">When decoded, it will look something like this:</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

<span data-ttu-id="4064a-153">有方法可以在 hello 簡化建立 apptokens 的 Sdk 中使用。</span><span class="sxs-lookup"><span data-stu-id="4064a-153">There are methods available within hello SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="4064a-154">例如，適用於.NET 您可以查看 hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken)類別和 hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)方法。</span><span class="sxs-lookup"><span data-stu-id="4064a-154">For example, for .NET you can look at hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="4064a-155">Hello.NET SDK，您可以使用參照太[範圍](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes)。</span><span class="sxs-lookup"><span data-stu-id="4064a-155">For hello .NET SDK, you can refer too[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="4064a-156">範圍</span><span class="sxs-lookup"><span data-stu-id="4064a-156">Scopes</span></span>

<span data-ttu-id="4064a-157">當使用內嵌語彙基元時，您可能想 hello 資源存取權給予 toorestrict 使用量。</span><span class="sxs-lookup"><span data-stu-id="4064a-157">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="4064a-158">為此，您可以產生具有範圍權限的權杖。</span><span class="sxs-lookup"><span data-stu-id="4064a-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="4064a-159">hello 如下的 Power BI Embedded hello 可用的領域。</span><span class="sxs-lookup"><span data-stu-id="4064a-159">hello following are hello available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="4064a-160">Scope</span><span class="sxs-lookup"><span data-stu-id="4064a-160">Scope</span></span>|<span data-ttu-id="4064a-161">說明</span><span class="sxs-lookup"><span data-stu-id="4064a-161">Description</span></span>|
|---|---|
|<span data-ttu-id="4064a-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="4064a-162">Dataset.Read</span></span>|<span data-ttu-id="4064a-163">提供的權限 tooread hello 指定資料集。</span><span class="sxs-lookup"><span data-stu-id="4064a-163">Provides permission tooread hello specified dataset.</span></span>|
|<span data-ttu-id="4064a-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="4064a-164">Dataset.Write</span></span>|<span data-ttu-id="4064a-165">提供指定的權限 toowrite toohello 資料集。</span><span class="sxs-lookup"><span data-stu-id="4064a-165">Provides permission toowrite toohello specified dataset.</span></span>|
|<span data-ttu-id="4064a-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="4064a-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="4064a-167">提供的權限 tooread 」 和 「 寫入 toohello 指定資料集。</span><span class="sxs-lookup"><span data-stu-id="4064a-167">Provides permission tooread and write toohello specificed dataset.</span></span>|
|<span data-ttu-id="4064a-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="4064a-168">Report.Read</span></span>|<span data-ttu-id="4064a-169">提供的權限 tooview hello 指定報表。</span><span class="sxs-lookup"><span data-stu-id="4064a-169">Provides permission tooview hello specified report.</span></span>|
|<span data-ttu-id="4064a-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="4064a-170">Report.ReadWrite</span></span>|<span data-ttu-id="4064a-171">提供的權限 tooview 和編輯 hello 指定的報表。</span><span class="sxs-lookup"><span data-stu-id="4064a-171">Provides permission tooview and edit hello specified report.</span></span>|
|<span data-ttu-id="4064a-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="4064a-172">Workspace.Report.Create</span></span>|<span data-ttu-id="4064a-173">提供的權限 toocreate 內 hello 指定新的報表 工作區。</span><span class="sxs-lookup"><span data-stu-id="4064a-173">Provides permission toocreate a new report within hello specified workspace.</span></span>|
|<span data-ttu-id="4064a-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="4064a-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="4064a-175">提供的權限 tooclone 內 hello 指定現有的報表 工作區。</span><span class="sxs-lookup"><span data-stu-id="4064a-175">Provides permission tooclone an existing report within hello specified workspace.</span></span>|

<span data-ttu-id="4064a-176">您可以使用類似 hello 下列 hello 範圍之間的空格提供多個領域。</span><span class="sxs-lookup"><span data-stu-id="4064a-176">You can supply multiple scopes by using a space between hello scopes like hello following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="4064a-177">**必要宣告 - 範圍**</span><span class="sxs-lookup"><span data-stu-id="4064a-177">**Required claims - scopes**</span></span>

<span data-ttu-id="4064a-178">scp: {scopesClaim} scopesClaim 可以是字串或字串陣列，您會看到 hello 允許權限 tooworkspace 資源 （報表、 資料集）</span><span class="sxs-lookup"><span data-stu-id="4064a-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting hello allowed permissions tooworkspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="4064a-179">已解碼的權杖中，與範圍定義，看起來類似 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="4064a-179">A decoded token, with scopes defined, would look similar toohello following.</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a><span data-ttu-id="4064a-180">作業和範圍</span><span class="sxs-lookup"><span data-stu-id="4064a-180">Operations and scopes</span></span>

|<span data-ttu-id="4064a-181">作業</span><span class="sxs-lookup"><span data-stu-id="4064a-181">Operation</span></span>|<span data-ttu-id="4064a-182">目標資源</span><span class="sxs-lookup"><span data-stu-id="4064a-182">Target resource</span></span>|<span data-ttu-id="4064a-183">權杖權限</span><span class="sxs-lookup"><span data-stu-id="4064a-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="4064a-184">根據資料集建立新的報告 (在記憶體內部)。</span><span class="sxs-lookup"><span data-stu-id="4064a-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="4064a-185">Dataset</span><span class="sxs-lookup"><span data-stu-id="4064a-185">Dataset</span></span>|<span data-ttu-id="4064a-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="4064a-186">Dataset.Read</span></span>|
|<span data-ttu-id="4064a-187">建立新的報表資料集為基礎的 （記憶體），並儲存 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="4064a-187">Create (in-memory) a new report based on a dataset and save hello report.</span></span>|<span data-ttu-id="4064a-188">Dataset</span><span class="sxs-lookup"><span data-stu-id="4064a-188">Dataset</span></span>|<span data-ttu-id="4064a-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="4064a-189">* Dataset.Read</span></span><br><span data-ttu-id="4064a-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="4064a-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="4064a-191">檢視和瀏覽/編輯現有報告 (在記憶體內部)。</span><span class="sxs-lookup"><span data-stu-id="4064a-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="4064a-192">Report.Read 暗指 Dataset.Read。</span><span class="sxs-lookup"><span data-stu-id="4064a-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="4064a-193">這不會允許權限 toosave 編輯。</span><span class="sxs-lookup"><span data-stu-id="4064a-193">This will not allow permissions toosave edits.</span></span>|<span data-ttu-id="4064a-194">報告</span><span class="sxs-lookup"><span data-stu-id="4064a-194">Report</span></span>|<span data-ttu-id="4064a-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="4064a-195">Report.Read</span></span>|
|<span data-ttu-id="4064a-196">編輯並儲存現有報告。</span><span class="sxs-lookup"><span data-stu-id="4064a-196">Edit and save an existing report.</span></span>|<span data-ttu-id="4064a-197">報告</span><span class="sxs-lookup"><span data-stu-id="4064a-197">Report</span></span>|<span data-ttu-id="4064a-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="4064a-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="4064a-199">儲存報告複本 (另存新檔)。</span><span class="sxs-lookup"><span data-stu-id="4064a-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="4064a-200">報告</span><span class="sxs-lookup"><span data-stu-id="4064a-200">Report</span></span>|<span data-ttu-id="4064a-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="4064a-201">* Report.Read</span></span><br><span data-ttu-id="4064a-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="4064a-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-hello-flow-works"></a><span data-ttu-id="4064a-203">以下是 hello 流程的運作方式</span><span class="sxs-lookup"><span data-stu-id="4064a-203">Here's how hello flow works</span></span>
1. <span data-ttu-id="4064a-204">複製 hello API 金鑰 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4064a-204">Copy hello API keys tooyour application.</span></span> <span data-ttu-id="4064a-205">您可以在取得 hello 金鑰**Azure 入口網站**。</span><span class="sxs-lookup"><span data-stu-id="4064a-205">You can get hello keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="4064a-206">權杖判斷提示宣告，並有到期時間。</span><span class="sxs-lookup"><span data-stu-id="4064a-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="4064a-207">以 API 存取金鑰簽署權杖。</span><span class="sxs-lookup"><span data-stu-id="4064a-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="4064a-208">使用者要求報表時 tooview。</span><span class="sxs-lookup"><span data-stu-id="4064a-208">User requests tooview a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="4064a-209">以 API 存取金鑰驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="4064a-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="4064a-210">Power BI Embedded 傳送報表 toouser。</span><span class="sxs-lookup"><span data-stu-id="4064a-210">Power BI Embedded sends a report toouser.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="4064a-211">之後**Power BI Embedded**報表 toohello 使用者，會傳送 hello 使用者可以檢視在自訂應用程式中的 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="4064a-211">After **Power BI Embedded** sends a report toohello user, hello user can view hello report in your custom app.</span></span> <span data-ttu-id="4064a-212">例如，如果您匯入 hello[分析銷售資料 PBIX 範例](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix)，hello 範例 web 應用程式會看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="4064a-212">For example, if you imported hello [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="4064a-213">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4064a-213">See Also</span></span>

[<span data-ttu-id="4064a-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="4064a-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="4064a-215">開始使用 Microsoft Power BI Embedded 範例</span><span class="sxs-lookup"><span data-stu-id="4064a-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="4064a-216">Microsoft Power BI Embedded 常見案例</span><span class="sxs-lookup"><span data-stu-id="4064a-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="4064a-217">開始使用 Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="4064a-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="4064a-218">PowerBI-CSharp Git 存放庫</span><span class="sxs-lookup"><span data-stu-id="4064a-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="4064a-219">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="4064a-219">More questions?</span></span> [<span data-ttu-id="4064a-220">再試一次 hello Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="4064a-220">Try hello Power BI Community</span></span>](http://community.powerbi.com/)


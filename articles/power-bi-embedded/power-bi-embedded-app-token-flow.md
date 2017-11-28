---
title: "使用 Power BI Embedded 驗證和授權"
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
ms.openlocfilehash: 93027f0f5467e0b21c47bbcbc84c67cdd50b26b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="04900-103">使用 Power BI Embedded 驗證和授權</span><span class="sxs-lookup"><span data-stu-id="04900-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="04900-104">Power BI Embedded 服務是使用**金鑰**和**應用程式權杖**進行驗證和授權，而不是使用明確的使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="04900-104">The Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="04900-105">在此模型中，您的應用程式會管理使用者的驗證與授權。</span><span class="sxs-lookup"><span data-stu-id="04900-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="04900-106">然後，您的應用程式可以在必要時建立及傳送應用程式權杖，以告知我們的服務轉譯要求的報告。</span><span class="sxs-lookup"><span data-stu-id="04900-106">When necessary, your app creates and sends the App Tokens that tells our service to render the requested report.</span></span> <span data-ttu-id="04900-107">雖然您仍然可以使用 Azure Active Directory 來進行使用者驗證與授權，但這項設計不需要您的應用程式這樣做。</span><span class="sxs-lookup"><span data-stu-id="04900-107">This design doesn't require your app to use Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-to-authenticate"></a><span data-ttu-id="04900-108">兩種驗證方式</span><span class="sxs-lookup"><span data-stu-id="04900-108">Two ways to authenticate</span></span>

<span data-ttu-id="04900-109">**金鑰** - 您可以針對所有 Power BI Embedded REST API 呼叫使用金鑰。</span><span class="sxs-lookup"><span data-stu-id="04900-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="04900-110">金鑰可以在 **Azure 入口網站** 中找到，方法是按一下[所有設定]，然後按一下 [存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="04900-110">The keys can be found in the **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="04900-111">一律將您的金鑰視為密碼。</span><span class="sxs-lookup"><span data-stu-id="04900-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="04900-112">這些金鑰具有在特定工作區集合上呼叫任何 REST API 的權限。</span><span class="sxs-lookup"><span data-stu-id="04900-112">These keys have permissions to make any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="04900-113">若要在 REST 呼叫上使用金鑰，請新增下列授權標頭︰</span><span class="sxs-lookup"><span data-stu-id="04900-113">To use a key on a REST call, add the following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="04900-114">**應用程式權杖** - 應用程式權杖用於所有內嵌的要求。</span><span class="sxs-lookup"><span data-stu-id="04900-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="04900-115">它們設計為在用戶端執行，因此限制為單一報告，且最佳做法是設定到期時間。</span><span class="sxs-lookup"><span data-stu-id="04900-115">They’re designed to be run client-side, so they're restricted to a single report and it’s best practice to set an expiration time.</span></span>

<span data-ttu-id="04900-116">應用程式權杖是 JWT (JSON Web 權杖)，由您的其中一個金鑰簽署。</span><span class="sxs-lookup"><span data-stu-id="04900-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="04900-117">您的應用程式權杖可包含下列宣告：</span><span class="sxs-lookup"><span data-stu-id="04900-117">Your app token can contain the following claims:</span></span>

| <span data-ttu-id="04900-118">宣告</span><span class="sxs-lookup"><span data-stu-id="04900-118">Claim</span></span> | <span data-ttu-id="04900-119">說明</span><span class="sxs-lookup"><span data-stu-id="04900-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04900-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="04900-120">**ver**</span></span> |<span data-ttu-id="04900-121">應用程式權杖的版本。</span><span class="sxs-lookup"><span data-stu-id="04900-121">The version of the app token.</span></span> <span data-ttu-id="04900-122">目前版本為 0.2.0。</span><span class="sxs-lookup"><span data-stu-id="04900-122">0.2.0 is the current version.</span></span> |
| <span data-ttu-id="04900-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="04900-123">**aud**</span></span> |<span data-ttu-id="04900-124">權杖的預定接收者。</span><span class="sxs-lookup"><span data-stu-id="04900-124">The intended recipient of the token.</span></span> <span data-ttu-id="04900-125">對於 Power BI Embedded，使用：“https://analysis.windows.net/powerbi/api”。</span><span class="sxs-lookup"><span data-stu-id="04900-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="04900-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="04900-126">**iss**</span></span> |<span data-ttu-id="04900-127">字串，表示已發出權杖的應用程式。</span><span class="sxs-lookup"><span data-stu-id="04900-127">A string indicating the application which issued the token.</span></span> |
| <span data-ttu-id="04900-128">**type**</span><span class="sxs-lookup"><span data-stu-id="04900-128">**type**</span></span> |<span data-ttu-id="04900-129">正在建立的應用程式權杖類型。</span><span class="sxs-lookup"><span data-stu-id="04900-129">The type of app token which is being created.</span></span> <span data-ttu-id="04900-130">目前唯一支援的類型為 **內嵌**。</span><span class="sxs-lookup"><span data-stu-id="04900-130">Current the only supported type is **embed**.</span></span> |
| <span data-ttu-id="04900-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="04900-131">**wcn**</span></span> |<span data-ttu-id="04900-132">為其發出權杖的工作區集合名稱。</span><span class="sxs-lookup"><span data-stu-id="04900-132">Workspace collection name the token is being issued for.</span></span> |
| <span data-ttu-id="04900-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="04900-133">**wid**</span></span> |<span data-ttu-id="04900-134">為其發出權杖的工作區識別碼。</span><span class="sxs-lookup"><span data-stu-id="04900-134">Workspace ID the token is being issued for.</span></span> |
| <span data-ttu-id="04900-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="04900-135">**rid**</span></span> |<span data-ttu-id="04900-136">為其發出權杖的報告識別碼。</span><span class="sxs-lookup"><span data-stu-id="04900-136">Report ID the token is being issued for.</span></span> |
| <span data-ttu-id="04900-137">**username** (選擇性)</span><span class="sxs-lookup"><span data-stu-id="04900-137">**username** (optional)</span></span> |<span data-ttu-id="04900-138">與 RLS 搭配使用，這是字串，可以在套用 RLS 規則時協助識別使用者。</span><span class="sxs-lookup"><span data-stu-id="04900-138">Used with RLS, this is a string that can help identify the user when applying RLS rules.</span></span> |
| <span data-ttu-id="04900-139">**角色** (選擇性)</span><span class="sxs-lookup"><span data-stu-id="04900-139">**roles** (optional)</span></span> |<span data-ttu-id="04900-140">字串，包含套用資料列層級安全性規則時要選取的角色。</span><span class="sxs-lookup"><span data-stu-id="04900-140">A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="04900-141">如果傳遞多個角色，應該將它們傳遞為字串陣列。</span><span class="sxs-lookup"><span data-stu-id="04900-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="04900-142">**scp** (選擇性)</span><span class="sxs-lookup"><span data-stu-id="04900-142">**scp** (optional)</span></span> |<span data-ttu-id="04900-143">字串，包含權限範圍。</span><span class="sxs-lookup"><span data-stu-id="04900-143">A string containing the permissions scopes.</span></span> <span data-ttu-id="04900-144">如果傳遞多個角色，應該將它們傳遞為字串陣列。</span><span class="sxs-lookup"><span data-stu-id="04900-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="04900-145">**exp** (選擇性)</span><span class="sxs-lookup"><span data-stu-id="04900-145">**exp** (optional)</span></span> |<span data-ttu-id="04900-146">指出權杖到期的時間。</span><span class="sxs-lookup"><span data-stu-id="04900-146">Indicates the time in which the token will expire.</span></span> <span data-ttu-id="04900-147">這些項目應該傳遞為 Unix 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="04900-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="04900-148">**nbf** (選擇性)</span><span class="sxs-lookup"><span data-stu-id="04900-148">**nbf** (optional)</span></span> |<span data-ttu-id="04900-149">指出權杖開始生效的時間。</span><span class="sxs-lookup"><span data-stu-id="04900-149">Indicates the time in which the token starts being valid.</span></span> <span data-ttu-id="04900-150">這些項目應該傳遞為 Unix 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="04900-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="04900-151">範例應用程式權杖看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="04900-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="04900-152">解碼時，看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="04900-152">When decoded, it will look something like this:</span></span>

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

<span data-ttu-id="04900-153">SDK 中有方法可簡化 apptokens 的建立。</span><span class="sxs-lookup"><span data-stu-id="04900-153">There are methods available within the SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="04900-154">例如，對於 .NET，您可以看看 [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) 類別和 [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) 方法。</span><span class="sxs-lookup"><span data-stu-id="04900-154">For example, for .NET you can look at the [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="04900-155">對於 .NET SDK，您可以參考[範圍](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes)。</span><span class="sxs-lookup"><span data-stu-id="04900-155">For the .NET SDK, you can refer to [Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="04900-156">範圍</span><span class="sxs-lookup"><span data-stu-id="04900-156">Scopes</span></span>

<span data-ttu-id="04900-157">在使用內嵌權杖時，您可能會想限制您授與了存取權之資源的使用量。</span><span class="sxs-lookup"><span data-stu-id="04900-157">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="04900-158">為此，您可以產生具有範圍權限的權杖。</span><span class="sxs-lookup"><span data-stu-id="04900-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="04900-159">以下是 Power BI Embedded 的可用範圍。</span><span class="sxs-lookup"><span data-stu-id="04900-159">The following are the available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="04900-160">Scope</span><span class="sxs-lookup"><span data-stu-id="04900-160">Scope</span></span>|<span data-ttu-id="04900-161">說明</span><span class="sxs-lookup"><span data-stu-id="04900-161">Description</span></span>|
|---|---|
|<span data-ttu-id="04900-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="04900-162">Dataset.Read</span></span>|<span data-ttu-id="04900-163">提供讀取指定資料集的權限。</span><span class="sxs-lookup"><span data-stu-id="04900-163">Provides permission to read the specified dataset.</span></span>|
|<span data-ttu-id="04900-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="04900-164">Dataset.Write</span></span>|<span data-ttu-id="04900-165">提供寫入指定資料集的權限。</span><span class="sxs-lookup"><span data-stu-id="04900-165">Provides permission to write to the specified dataset.</span></span>|
|<span data-ttu-id="04900-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="04900-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="04900-167">提供讀取和寫入指定資料集的權限。</span><span class="sxs-lookup"><span data-stu-id="04900-167">Provides permission to read and write to the specificed dataset.</span></span>|
|<span data-ttu-id="04900-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="04900-168">Report.Read</span></span>|<span data-ttu-id="04900-169">提供檢視指定報告的權限。</span><span class="sxs-lookup"><span data-stu-id="04900-169">Provides permission to view the specified report.</span></span>|
|<span data-ttu-id="04900-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="04900-170">Report.ReadWrite</span></span>|<span data-ttu-id="04900-171">提供檢視和編輯指定報告的權限。</span><span class="sxs-lookup"><span data-stu-id="04900-171">Provides permission to view and edit the specified report.</span></span>|
|<span data-ttu-id="04900-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="04900-172">Workspace.Report.Create</span></span>|<span data-ttu-id="04900-173">提供在指定工作區內建立新報告的權限。</span><span class="sxs-lookup"><span data-stu-id="04900-173">Provides permission to create a new report within the specified workspace.</span></span>|
|<span data-ttu-id="04900-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="04900-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="04900-175">提供在指定工作區內複製現有報告的權限。</span><span class="sxs-lookup"><span data-stu-id="04900-175">Provides permission to clone an existing report within the specified workspace.</span></span>|

<span data-ttu-id="04900-176">您可以如下所示，在範圍之間使用空格來提供多個範圍。</span><span class="sxs-lookup"><span data-stu-id="04900-176">You can supply multiple scopes by using a space between the scopes like the following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="04900-177">**必要宣告 - 範圍**</span><span class="sxs-lookup"><span data-stu-id="04900-177">**Required claims - scopes**</span></span>

<span data-ttu-id="04900-178">scp: {scopesClaim} scopesClaim 可以是字串或字串陣列，會記錄工作區資源 (報告、資料集等) 的允許權限</span><span class="sxs-lookup"><span data-stu-id="04900-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting the allowed permissions to workspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="04900-179">已定義範圍的解碼權杖看起來像下面這樣。</span><span class="sxs-lookup"><span data-stu-id="04900-179">A decoded token, with scopes defined, would look similar to the following.</span></span>

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

### <a name="operations-and-scopes"></a><span data-ttu-id="04900-180">作業和範圍</span><span class="sxs-lookup"><span data-stu-id="04900-180">Operations and scopes</span></span>

|<span data-ttu-id="04900-181">作業</span><span class="sxs-lookup"><span data-stu-id="04900-181">Operation</span></span>|<span data-ttu-id="04900-182">目標資源</span><span class="sxs-lookup"><span data-stu-id="04900-182">Target resource</span></span>|<span data-ttu-id="04900-183">權杖權限</span><span class="sxs-lookup"><span data-stu-id="04900-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="04900-184">根據資料集建立新的報告 (在記憶體內部)。</span><span class="sxs-lookup"><span data-stu-id="04900-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="04900-185">Dataset</span><span class="sxs-lookup"><span data-stu-id="04900-185">Dataset</span></span>|<span data-ttu-id="04900-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="04900-186">Dataset.Read</span></span>|
|<span data-ttu-id="04900-187">根據資料集建立新的報告並儲存報告 (在記憶體內部)。</span><span class="sxs-lookup"><span data-stu-id="04900-187">Create (in-memory) a new report based on a dataset and save the report.</span></span>|<span data-ttu-id="04900-188">Dataset</span><span class="sxs-lookup"><span data-stu-id="04900-188">Dataset</span></span>|<span data-ttu-id="04900-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="04900-189">* Dataset.Read</span></span><br><span data-ttu-id="04900-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="04900-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="04900-191">檢視和瀏覽/編輯現有報告 (在記憶體內部)。</span><span class="sxs-lookup"><span data-stu-id="04900-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="04900-192">Report.Read 暗指 Dataset.Read。</span><span class="sxs-lookup"><span data-stu-id="04900-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="04900-193">這不會允許儲存編輯內容的權限。</span><span class="sxs-lookup"><span data-stu-id="04900-193">This will not allow permissions to save edits.</span></span>|<span data-ttu-id="04900-194">報告</span><span class="sxs-lookup"><span data-stu-id="04900-194">Report</span></span>|<span data-ttu-id="04900-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="04900-195">Report.Read</span></span>|
|<span data-ttu-id="04900-196">編輯並儲存現有報告。</span><span class="sxs-lookup"><span data-stu-id="04900-196">Edit and save an existing report.</span></span>|<span data-ttu-id="04900-197">報告</span><span class="sxs-lookup"><span data-stu-id="04900-197">Report</span></span>|<span data-ttu-id="04900-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="04900-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="04900-199">儲存報告複本 (另存新檔)。</span><span class="sxs-lookup"><span data-stu-id="04900-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="04900-200">報告</span><span class="sxs-lookup"><span data-stu-id="04900-200">Report</span></span>|<span data-ttu-id="04900-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="04900-201">* Report.Read</span></span><br><span data-ttu-id="04900-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="04900-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-the-flow-works"></a><span data-ttu-id="04900-203">以下是流程的運作方式</span><span class="sxs-lookup"><span data-stu-id="04900-203">Here's how the flow works</span></span>
1. <span data-ttu-id="04900-204">將 API 金鑰複製到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="04900-204">Copy the API keys to your application.</span></span> <span data-ttu-id="04900-205">您可以在 **Azure 入口網站**取得金鑰。</span><span class="sxs-lookup"><span data-stu-id="04900-205">You can get the keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="04900-206">權杖判斷提示宣告，並有到期時間。</span><span class="sxs-lookup"><span data-stu-id="04900-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="04900-207">以 API 存取金鑰簽署權杖。</span><span class="sxs-lookup"><span data-stu-id="04900-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="04900-208">使用者要求檢視報告。</span><span class="sxs-lookup"><span data-stu-id="04900-208">User requests to view a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="04900-209">以 API 存取金鑰驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="04900-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="04900-210">Power BI Embedded 將報表傳送給使用者。</span><span class="sxs-lookup"><span data-stu-id="04900-210">Power BI Embedded sends a report to user.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="04900-211">當 **Power BI Embedded** 將報表傳送給使用者之後，使用者就可以在您自訂的應用程式中檢視報表。</span><span class="sxs-lookup"><span data-stu-id="04900-211">After **Power BI Embedded** sends a report to the user, the user can view the report in your custom app.</span></span> <span data-ttu-id="04900-212">例如，如果您匯入了 [分析銷售資料 PBIX 範例](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix)，範例 Web 應用程式看起來就會像這樣︰</span><span class="sxs-lookup"><span data-stu-id="04900-212">For example, if you imported the [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="04900-213">另請參閱</span><span class="sxs-lookup"><span data-stu-id="04900-213">See Also</span></span>

[<span data-ttu-id="04900-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="04900-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="04900-215">開始使用 Microsoft Power BI Embedded 範例</span><span class="sxs-lookup"><span data-stu-id="04900-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="04900-216">Microsoft Power BI Embedded 常見案例</span><span class="sxs-lookup"><span data-stu-id="04900-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="04900-217">開始使用 Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="04900-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="04900-218">PowerBI-CSharp Git 存放庫</span><span class="sxs-lookup"><span data-stu-id="04900-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="04900-219">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="04900-219">More questions?</span></span> [<span data-ttu-id="04900-220">試用 Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="04900-220">Try the Power BI Community</span></span>](http://community.powerbi.com/)


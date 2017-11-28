---
title: "Azure Active Directory B2C：使用方式報告 API 範例和定義 | Microsoft Docs"
description: "取得關於 Azure AD B2C 租用戶使用者、驗證及多重要素驗證之報告的相關指南和範例"
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: f01f0d1d12464e38f892f1fdd5c7408a3b4cd1aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a><span data-ttu-id="3cf11-103">存取 Azure AD B2C 中透過 hello reporting API 的使用方式報表</span><span class="sxs-lookup"><span data-stu-id="3cf11-103">Accessing usage reports in Azure AD B2C via hello reporting API</span></span>

<span data-ttu-id="3cf11-104">Azure Active Directory B2C (Azure AD B2C) 會根據使用者登入和 Azure Multi-Factor Authentication 提供驗證。</span><span class="sxs-lookup"><span data-stu-id="3cf11-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="3cf11-105">驗證可跨識別提供者提供給應用程式系列的使用者。</span><span class="sxs-lookup"><span data-stu-id="3cf11-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="3cf11-106">當您知道 hello 登錄 hello 租用戶，他們使用 tooregister，以及驗證的 hello 數目的 hello 提供者中，依類型的使用者數目時，您可以回答問題，例如：</span><span class="sxs-lookup"><span data-stu-id="3cf11-106">When you know hello number of users registered in hello tenant, hello providers they used tooregister, and hello number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="3cf11-107">從每一種身分識別提供者 （例如，Microsoft 或 LinkedIn 帳戶） 的使用者人數中註冊了 hello 最後 10 天？</span><span class="sxs-lookup"><span data-stu-id="3cf11-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in hello last 10 days?</span></span>
* <span data-ttu-id="3cf11-108">使用 Multi-factor Authentication 的驗證次數已順利完成在 hello 上個月？</span><span class="sxs-lookup"><span data-stu-id="3cf11-108">How many authentications using Multi-Factor Authentication have completed successfully in hello last month?</span></span>
* <span data-ttu-id="3cf11-109">這個月已完成幾次登入式驗證？</span><span class="sxs-lookup"><span data-stu-id="3cf11-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="3cf11-110">依每一天計算？</span><span class="sxs-lookup"><span data-stu-id="3cf11-110">Per day?</span></span> <span data-ttu-id="3cf11-111">依每一應用程式計算？</span><span class="sxs-lookup"><span data-stu-id="3cf11-111">Per application?</span></span>
* <span data-ttu-id="3cf11-112">如何評估 hello 預期每月成本的我的 Azure AD B2C 租用戶活動？</span><span class="sxs-lookup"><span data-stu-id="3cf11-112">How can I estimate hello expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="3cf11-113">本文著重於報表繫結 toobilling 活動為基礎的使用者、 計費登-中為基礎的驗證及多因素驗證的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="3cf11-113">This article focuses on reports tied toobilling activity, which is based on hello number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3cf11-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="3cf11-114">Prerequisites</span></span>
<span data-ttu-id="3cf11-115">您開始之前，您必須在 toocomplete hello 步驟[必要條件 tooaccess hello Azure AD 報告 Api](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/)。</span><span class="sxs-lookup"><span data-stu-id="3cf11-115">Before you get started, you need toocomplete hello steps in [Prerequisites tooaccess hello Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="3cf11-116">建立應用程式、 取得它的密碼和它存取的授與權限 tooyour Azure AD B2C 租用戶的報表。</span><span class="sxs-lookup"><span data-stu-id="3cf11-116">Create an application, obtain a secret for it, and grant it access rights tooyour Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="3cf11-117">這裡也提供了 Bash 指令碼和 Python 指令碼的範例。</span><span class="sxs-lookup"><span data-stu-id="3cf11-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="3cf11-118">PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="3cf11-118">PowerShell script</span></span>
<span data-ttu-id="3cf11-119">此指令碼示範使用 hello hello 建立四個使用方式報告`TimeStamp`參數與 hello`ApplicationId`篩選器。</span><span class="sxs-lookup"><span data-stu-id="3cf11-119">This script demonstrates hello creation of four usage reports by using hello `TimeStamp` parameter and hello `ApplicationId` filter.</span></span>

```powershell
# This script will require hello Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from hello tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for hello report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for hello " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="3cf11-120">使用報告定義</span><span class="sxs-lookup"><span data-stu-id="3cf11-120">Usage report definitions</span></span>
* <span data-ttu-id="3cf11-121">**tenantUserCount**: hello hello 租用戶身分識別提供者，每日在 hello 的型別中的使用者數目的過去 30 天。</span><span class="sxs-lookup"><span data-stu-id="3cf11-121">**tenantUserCount**: hello number of users in hello tenant by type of identity provider, per day in hello last 30 days.</span></span> <span data-ttu-id="3cf11-122">(選擇性地`TimeStamp`篩選工具提供的使用者計數指定的日期 toohello 從目前的日期)。</span><span class="sxs-lookup"><span data-stu-id="3cf11-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date toohello current date).</span></span> <span data-ttu-id="3cf11-123">hello 報表會提供：</span><span class="sxs-lookup"><span data-stu-id="3cf11-123">hello report provides:</span></span>
  * <span data-ttu-id="3cf11-124">**TotalUserCount**: hello 的所有使用者物件數目。</span><span class="sxs-lookup"><span data-stu-id="3cf11-124">**TotalUserCount**: hello number of all user objects.</span></span>
  * <span data-ttu-id="3cf11-125">**OtherUserCount**: hello Azure Active Directory 使用者 （而非 Azure AD B2C 使用者） 的數目。</span><span class="sxs-lookup"><span data-stu-id="3cf11-125">**OtherUserCount**: hello number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="3cf11-126">**LocalUserCount**: hello 與認證的本機 toohello Azure AD B2C 租用戶建立 Azure AD B2C 使用者帳戶數目。</span><span class="sxs-lookup"><span data-stu-id="3cf11-126">**LocalUserCount**: hello number of Azure AD B2C user accounts created with credentials local toohello Azure AD B2C tenant.</span></span>

* <span data-ttu-id="3cf11-127">**AlternateIdUserCount**: hello 人數 Azure AD B2C 向外部身分識別提供者 (例如 Facebook、 Microsoft 帳戶或另一個 Azure Active Directory 租用戶，也稱為 tooas `OrgId`)。</span><span class="sxs-lookup"><span data-stu-id="3cf11-127">**AlternateIdUserCount**: hello number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred tooas an `OrgId`).</span></span>

* <span data-ttu-id="3cf11-128">**b2cAuthenticationCountSummary**: hello 的計費驗證透過 hello 過去 30 天的日期和類型的驗證流程的每日數字的摘要。</span><span class="sxs-lookup"><span data-stu-id="3cf11-128">**b2cAuthenticationCountSummary**: Summary of hello daily number of billable authentications over hello last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="3cf11-129">**b2cAuthenticationCount**: hello 一段時間內驗證次數。</span><span class="sxs-lookup"><span data-stu-id="3cf11-129">**b2cAuthenticationCount**: hello number of authentications within a time period.</span></span> <span data-ttu-id="3cf11-130">hello 預設值為 hello 過去 30 天。</span><span class="sxs-lookup"><span data-stu-id="3cf11-130">hello default is hello last 30 days.</span></span>  <span data-ttu-id="3cf11-131">(選擇性： hello 開頭和結尾`TimeStamp`參數定義特定時間週期。) hello 輸出包含`StartTimeStamp`（最早日期的此租用戶的活動） 和`EndTimeStamp`（最新的更新）。</span><span class="sxs-lookup"><span data-stu-id="3cf11-131">(Optional: hello beginning and ending `TimeStamp` parameters define a specific time period.) hello output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="3cf11-132">**b2cMfaRequestCountSummary**: hello 每日數的日期和類型 （SMS 或語音） 的多因素驗證的摘要。</span><span class="sxs-lookup"><span data-stu-id="3cf11-132">**b2cMfaRequestCountSummary**: Summary of hello daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="3cf11-133">限制</span><span class="sxs-lookup"><span data-stu-id="3cf11-133">Limitations</span></span>
<span data-ttu-id="3cf11-134">使用者計數的資料重新整理每隔 24 too48 小時。</span><span class="sxs-lookup"><span data-stu-id="3cf11-134">User count data is refreshed every 24 too48 hours.</span></span> <span data-ttu-id="3cf11-135">驗證則是每天更新數次。</span><span class="sxs-lookup"><span data-stu-id="3cf11-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="3cf11-136">當使用 hello`ApplicationId`篩選，空白報表回應呇窆蒻孻 tooone 的下列條件：</span><span class="sxs-lookup"><span data-stu-id="3cf11-136">When using hello `ApplicationId` filter, an empty report response can be due tooone of following conditions:</span></span>
  * <span data-ttu-id="3cf11-137">hello 應用程式識別碼不存在於 hello 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="3cf11-137">hello application ID does not exist in hello tenant.</span></span> <span data-ttu-id="3cf11-138">請確定它是正確的。</span><span class="sxs-lookup"><span data-stu-id="3cf11-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="3cf11-139">hello 應用程式識別碼不存在，但在 hello 報告週期中找不到任何資料。</span><span class="sxs-lookup"><span data-stu-id="3cf11-139">hello application ID exists, but no data was found in hello reporting period.</span></span> <span data-ttu-id="3cf11-140">請檢閱您的日期/時間參數。</span><span class="sxs-lookup"><span data-stu-id="3cf11-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3cf11-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3cf11-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="3cf11-142">評估 Azure AD 的每月帳單</span><span class="sxs-lookup"><span data-stu-id="3cf11-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="3cf11-143">當結合[hello 最新 Azure AD B2C 定價可用](https://azure.microsoft.com/pricing/details/active-directory-b2c/)，可以每日、 估計每週和每月 Azure 耗用量。</span><span class="sxs-lookup"><span data-stu-id="3cf11-143">When combined with [hello most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="3cf11-144">當您規劃的租用戶行為變更可能會影響整體成本時，評估特別實用。</span><span class="sxs-lookup"><span data-stu-id="3cf11-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="3cf11-145">您可以在[連結的 Azure 訂用帳戶](active-directory-b2c-how-to-enable-billing.md)中檢閱實際成本。</span><span class="sxs-lookup"><span data-stu-id="3cf11-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="3cf11-146">其他輸出格式的選項</span><span class="sxs-lookup"><span data-stu-id="3cf11-146">Options for other output formats</span></span>
<span data-ttu-id="3cf11-147">hello 下列程式碼顯示傳送輸出 tooJSON、 name 值清單和 XML 的範例：</span><span class="sxs-lookup"><span data-stu-id="3cf11-147">hello following code shows examples of sending output tooJSON, a name value list, and XML:</span></span>
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```

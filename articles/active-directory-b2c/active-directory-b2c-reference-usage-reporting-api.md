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
ms.openlocfilehash: 52180b760046d273c5a75720df0a73532d0343ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-the-reporting-api"></a><span data-ttu-id="8833f-103">透過報告 API 存取 Azure AD B2C 中的使用報告</span><span class="sxs-lookup"><span data-stu-id="8833f-103">Accessing usage reports in Azure AD B2C via the reporting API</span></span>

<span data-ttu-id="8833f-104">Azure Active Directory B2C (Azure AD B2C) 會根據使用者登入和 Azure Multi-Factor Authentication 提供驗證。</span><span class="sxs-lookup"><span data-stu-id="8833f-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="8833f-105">驗證可跨識別提供者提供給應用程式系列的使用者。</span><span class="sxs-lookup"><span data-stu-id="8833f-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="8833f-106">當您知道已在租用戶中註冊的使用者數目、使用者用來註冊的提供者，以及不同類型的驗證次數時，就能以如下方式回答問題：</span><span class="sxs-lookup"><span data-stu-id="8833f-106">When you know the number of users registered in the tenant, the providers they used to register, and the number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="8833f-107">過去 10 天內各類型識別提供者 (例如，Microsoft 或 LinkedIn 帳戶) 註冊的使用者數目？</span><span class="sxs-lookup"><span data-stu-id="8833f-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in the last 10 days?</span></span>
* <span data-ttu-id="8833f-108">上個月使用 Multi-Factor Authentication 成功完成多少次驗證？</span><span class="sxs-lookup"><span data-stu-id="8833f-108">How many authentications using Multi-Factor Authentication have completed successfully in the last month?</span></span>
* <span data-ttu-id="8833f-109">這個月已完成幾次登入式驗證？</span><span class="sxs-lookup"><span data-stu-id="8833f-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="8833f-110">依每一天計算？</span><span class="sxs-lookup"><span data-stu-id="8833f-110">Per day?</span></span> <span data-ttu-id="8833f-111">依每一應用程式計算？</span><span class="sxs-lookup"><span data-stu-id="8833f-111">Per application?</span></span>
* <span data-ttu-id="8833f-112">如何評估我的 Azure AD B2C 租用戶活動的每月預期成本？</span><span class="sxs-lookup"><span data-stu-id="8833f-112">How can I estimate the expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="8833f-113">本文章著重於與計費活動有關的報告，而計費活動是以使用者數目、可計費的登入式驗證及多重要素驗證為根據。</span><span class="sxs-lookup"><span data-stu-id="8833f-113">This article focuses on reports tied to billing activity, which is based on the number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8833f-114">先決條件</span><span class="sxs-lookup"><span data-stu-id="8833f-114">Prerequisites</span></span>
<span data-ttu-id="8833f-115">開始之前，您必須先完成[存取 Azure AD 報告 API 的必要條件](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="8833f-115">Before you get started, you need to complete the steps in [Prerequisites to access the Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="8833f-116">建立應用程式、取得密碼，並授與對您的 Azure AD B2C 租用戶報告的存取權限。</span><span class="sxs-lookup"><span data-stu-id="8833f-116">Create an application, obtain a secret for it, and grant it access rights to your Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="8833f-117">這裡也提供了 Bash 指令碼和 Python 指令碼的範例。</span><span class="sxs-lookup"><span data-stu-id="8833f-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="8833f-118">PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="8833f-118">PowerShell script</span></span>
<span data-ttu-id="8833f-119">此指令碼示範如何使用 `TimeStamp` 參數和 `ApplicationId` 篩選器來建立四份使用報告。</span><span class="sxs-lookup"><span data-stu-id="8833f-119">This script demonstrates the creation of four usage reports by using the `TimeStamp` parameter and the `ApplicationId` filter.</span></span>

```powershell
# This script will require the Web Application and permissions setup in Azure Active Directory

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

    Write-host Data from the tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for the report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for the " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="8833f-120">使用報告定義</span><span class="sxs-lookup"><span data-stu-id="8833f-120">Usage report definitions</span></span>
* <span data-ttu-id="8833f-121">**tenantUserCount**：過去 30 天，租用戶中每一天各類型識別提供者的使用者數目。</span><span class="sxs-lookup"><span data-stu-id="8833f-121">**tenantUserCount**: The number of users in the tenant by type of identity provider, per day in the last 30 days.</span></span> <span data-ttu-id="8833f-122">(`TimeStamp` 篩選器可選擇性提供從指定日期至目前日期的使用者計數)。</span><span class="sxs-lookup"><span data-stu-id="8833f-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date to the current date).</span></span> <span data-ttu-id="8833f-123">此報告提供：</span><span class="sxs-lookup"><span data-stu-id="8833f-123">The report provides:</span></span>
  * <span data-ttu-id="8833f-124">**TotalUserCount**：所有使用者物件的數目。</span><span class="sxs-lookup"><span data-stu-id="8833f-124">**TotalUserCount**: The number of all user objects.</span></span>
  * <span data-ttu-id="8833f-125">**OtherUserCount**：Azure Active Directory 使用者 (而非 Azure AD B2C 使用者) 的數目。</span><span class="sxs-lookup"><span data-stu-id="8833f-125">**OtherUserCount**: The number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="8833f-126">**LocalUserCount**：Azure AD B2C 使用者帳戶的數目 (這些帳戶是以 Azure AD B2C 租用戶本機的認證所建立)。</span><span class="sxs-lookup"><span data-stu-id="8833f-126">**LocalUserCount**: The number of Azure AD B2C user accounts created with credentials local to the Azure AD B2C tenant.</span></span>

* <span data-ttu-id="8833f-127">**AlternateIdUserCount**：已向外部識別提供者 (例如 Facebook、Microsoft 帳戶或另一個 Azure Active Directory 租用戶，亦稱為 `OrgId`) 註冊的 Azure AD B2C 使用者數目。</span><span class="sxs-lookup"><span data-stu-id="8833f-127">**AlternateIdUserCount**: The number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred to as an `OrgId`).</span></span>

* <span data-ttu-id="8833f-128">**b2cAuthenticationCountSummary**：過去 30 天，每天及各類型驗證流程的每日可計費驗證次數摘要。</span><span class="sxs-lookup"><span data-stu-id="8833f-128">**b2cAuthenticationCountSummary**: Summary of the daily number of billable authentications over the last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="8833f-129">**b2cAuthenticationCount**：某段時間週期內的驗證次數。</span><span class="sxs-lookup"><span data-stu-id="8833f-129">**b2cAuthenticationCount**: The number of authentications within a time period.</span></span> <span data-ttu-id="8833f-130">預設值為過去 30 天。</span><span class="sxs-lookup"><span data-stu-id="8833f-130">The default is the last 30 days.</span></span>  <span data-ttu-id="8833f-131">(選擇性：開頭和結尾的 `TimeStamp` 參數會定義特定的期間)。輸出包括 `StartTimeStamp` (此租用戶的最早活動日期) 和 `EndTimeStamp` (最新的更新)。</span><span class="sxs-lookup"><span data-stu-id="8833f-131">(Optional: The beginning and ending `TimeStamp` parameters define a specific time period.) The output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="8833f-132">**b2cMfaRequestCountSummary**：依日期及類型 (SMS 或語音) 區分的每日多重要素驗證次數摘要。</span><span class="sxs-lookup"><span data-stu-id="8833f-132">**b2cMfaRequestCountSummary**: Summary of the daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="8833f-133">限制</span><span class="sxs-lookup"><span data-stu-id="8833f-133">Limitations</span></span>
<span data-ttu-id="8833f-134">使用者計數的資料每隔 24 到 48 小時會重新整理。</span><span class="sxs-lookup"><span data-stu-id="8833f-134">User count data is refreshed every 24 to 48 hours.</span></span> <span data-ttu-id="8833f-135">驗證則是每天更新數次。</span><span class="sxs-lookup"><span data-stu-id="8833f-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="8833f-136">使用 `ApplicationId` 篩選器時，空白報告回應是因為發生下列其中一種情況：</span><span class="sxs-lookup"><span data-stu-id="8833f-136">When using the `ApplicationId` filter, an empty report response can be due to one of following conditions:</span></span>
  * <span data-ttu-id="8833f-137">應用程式識別碼不存在於租用戶中。</span><span class="sxs-lookup"><span data-stu-id="8833f-137">The application ID does not exist in the tenant.</span></span> <span data-ttu-id="8833f-138">請確定它是正確的。</span><span class="sxs-lookup"><span data-stu-id="8833f-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="8833f-139">應用程式識別碼存在，但報告期間內找不到任何資料。</span><span class="sxs-lookup"><span data-stu-id="8833f-139">The application ID exists, but no data was found in the reporting period.</span></span> <span data-ttu-id="8833f-140">請檢閱您的日期/時間參數。</span><span class="sxs-lookup"><span data-stu-id="8833f-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8833f-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8833f-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="8833f-142">評估 Azure AD 的每月帳單</span><span class="sxs-lookup"><span data-stu-id="8833f-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="8833f-143">搭配[最新 Azure AD B2C 價格](https://azure.microsoft.com/pricing/details/active-directory-b2c/)，您可以評估每日、每週、每月的 Azure 耗用量。</span><span class="sxs-lookup"><span data-stu-id="8833f-143">When combined with [the most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="8833f-144">當您規劃的租用戶行為變更可能會影響整體成本時，評估特別實用。</span><span class="sxs-lookup"><span data-stu-id="8833f-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="8833f-145">您可以在[連結的 Azure 訂用帳戶](active-directory-b2c-how-to-enable-billing.md)中檢閱實際成本。</span><span class="sxs-lookup"><span data-stu-id="8833f-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="8833f-146">其他輸出格式的選項</span><span class="sxs-lookup"><span data-stu-id="8833f-146">Options for other output formats</span></span>
<span data-ttu-id="8833f-147">下列程式碼示範將輸出傳送至 JSON、名稱值清單及 XML 的範例：</span><span class="sxs-lookup"><span data-stu-id="8833f-147">The following code shows examples of sending output to JSON, a name value list, and XML:</span></span>
```powershell
# to output to JSON use following line in the PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# to output the content to a name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# to output the content in XML use the following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```

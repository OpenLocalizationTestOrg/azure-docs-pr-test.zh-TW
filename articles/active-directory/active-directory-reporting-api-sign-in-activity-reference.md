---
title: "aaaAzure Active Directory 登入活動報表 API 參考 |Microsoft 文件"
description: "Hello Azure Active Directory 登入活動報表應用程式開發介面參考"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="ebe44-103">Azure Active Directory 登入活動報告 API 參考</span><span class="sxs-lookup"><span data-stu-id="ebe44-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="ebe44-104">本主題是有關 hello Azure Active Directory 的主題集合的一部分報告應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="ebe44-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="ebe44-105">Azure AD 報告 api 還可讓您的 API tooaccess 登入活動報表資料使用程式碼或相關的工具。</span><span class="sxs-lookup"><span data-stu-id="ebe44-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="ebe44-106">本主題的 hello 範圍是 tooprovide hello 的相關參考資訊**登入活動報表 API**。</span><span class="sxs-lookup"><span data-stu-id="ebe44-106">hello scope of this topic is tooprovide you with reference information about hello **sign-in activity report API**.</span></span>

<span data-ttu-id="ebe44-107">請參閱：</span><span class="sxs-lookup"><span data-stu-id="ebe44-107">See:</span></span>

* <span data-ttu-id="ebe44-108">[登入活動](active-directory-reporting-azure-portal.md#activity-reports) 以取得詳細概念資訊</span><span class="sxs-lookup"><span data-stu-id="ebe44-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="ebe44-109">[開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)的 hello reporting API 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ebe44-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="who-can-access-hello-api-data"></a><span data-ttu-id="ebe44-110">誰可以存取 hello API 資料？</span><span class="sxs-lookup"><span data-stu-id="ebe44-110">Who can access hello API data?</span></span>
* <span data-ttu-id="ebe44-111">使用者和 hello 安全性系統管理員或安全性 Reader 角色中的服務主體</span><span class="sxs-lookup"><span data-stu-id="ebe44-111">Users and Service Principals in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="ebe44-112">全域管理員</span><span class="sxs-lookup"><span data-stu-id="ebe44-112">Global Admins</span></span>
* <span data-ttu-id="ebe44-113">任何已授權 tooaccess hello API 的應用程式 （只會根據全域系統管理員權限，應用程式授權可以是安裝程式）</span><span class="sxs-lookup"><span data-stu-id="ebe44-113">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="ebe44-114">對於應用程式 tooaccess 安全性應用程式開發介面登入事件，例如使用下列 PowerShell tooadd hello 應用程式服務主體到 hello 安全性讀取者角色的 hello tooconfigure 存取</span><span class="sxs-lookup"><span data-stu-id="ebe44-114">tooconfigure access for an application tooaccess security APIs such as signin events, use hello following PowerShell tooadd hello applications Service Principal into hello Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="ebe44-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="ebe44-115">Prerequisites</span></span>
<span data-ttu-id="ebe44-116">tooaccess hello 報告應用程式開發介面，您必須透過此報告：</span><span class="sxs-lookup"><span data-stu-id="ebe44-116">tooaccess this report through hello reporting API, you must have:</span></span>

* <span data-ttu-id="ebe44-117">[Azure Active Directory Premium P1 或 P2 版本](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="ebe44-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="ebe44-118">已完成的 hello[必要條件 tooaccess hello Azure AD 報告 API](active-directory-reporting-api-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="ebe44-118">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="ebe44-119">存取 hello API</span><span class="sxs-lookup"><span data-stu-id="ebe44-119">Accessing hello API</span></span>
<span data-ttu-id="ebe44-120">您可以存取此應用程式開發介面透過 hello[圖表總管](https://graphexplorer2.cloudapp.net)或以程式設計方式使用，例如 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ebe44-120">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="ebe44-121">PowerShell toocorrectly 解譯 hello AAD Graph REST 呼叫中使用的 OData 篩選器語法的您必須使用 hello 倒單引號 (也稱為： 抑音符號) 字元太 「 逸出"hello $ 字元。</span><span class="sxs-lookup"><span data-stu-id="ebe44-121">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="ebe44-122">hello 倒單引號字元做為[PowerShell 的逸出字元](https://technet.microsoft.com/library/hh847755.aspx)，讓 PowerShell toodo hello $ 字元，常值解譯，同時避免混淆做為 PowerShell 變數的名稱 (亦即： $filter)。</span><span class="sxs-lookup"><span data-stu-id="ebe44-122">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="ebe44-123">本主題的 hello 重點是在 hello 圖表總管。</span><span class="sxs-lookup"><span data-stu-id="ebe44-123">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="ebe44-124">如需 PowerShell 範例，請參閱此 [PowerShell 指令碼](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script)。</span><span class="sxs-lookup"><span data-stu-id="ebe44-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="ebe44-125">API 端點</span><span class="sxs-lookup"><span data-stu-id="ebe44-125">API Endpoint</span></span>
<span data-ttu-id="ebe44-126">您可以存取此應用程式開發介面，使用下列基底 URI 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ebe44-126">You can access this API using hello following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="ebe44-127">Toohello 磁碟區的資料，因為這個 API 已傳回記錄的 1 百萬個的限制。</span><span class="sxs-lookup"><span data-stu-id="ebe44-127">Due toohello volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="ebe44-128">這個呼叫會傳回批次中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="ebe44-128">This call returns hello data in batches.</span></span> <span data-ttu-id="ebe44-129">每個批次的上限為 1000 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="ebe44-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="ebe44-130">tooget hello 下一個批次的記錄，以使用 hello 下一步 連結。</span><span class="sxs-lookup"><span data-stu-id="ebe44-130">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="ebe44-131">取得 hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) hello 第一組傳回的記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="ebe44-131">Get hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from hello first set of returned records.</span></span> <span data-ttu-id="ebe44-132">hello 跳過權杖會在 hello hello 結果集的結尾。</span><span class="sxs-lookup"><span data-stu-id="ebe44-132">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="ebe44-133">支援的篩選器</span><span class="sxs-lookup"><span data-stu-id="ebe44-133">Supported filters</span></span>
<span data-ttu-id="ebe44-134">您可以縮小 hello 應用程式開發介面所傳回的記錄數目的篩選器的形式呼叫。</span><span class="sxs-lookup"><span data-stu-id="ebe44-134">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="ebe44-135">登入應用程式開發介面支援的相關的資料，下列篩選器的 hello:</span><span class="sxs-lookup"><span data-stu-id="ebe44-135">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="ebe44-136">**$top =\<傳回的記錄 toobe 數目\>** -toolimit hello 數傳回的記錄。</span><span class="sxs-lookup"><span data-stu-id="ebe44-136">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="ebe44-137">這是一項昂貴的作業。</span><span class="sxs-lookup"><span data-stu-id="ebe44-137">This is an expensive operation.</span></span> <span data-ttu-id="ebe44-138">如果您想要 tooreturn 數以千計的物件，則不應使用此篩選條件。</span><span class="sxs-lookup"><span data-stu-id="ebe44-138">You should not use this filter if you want tooreturn thousands of objects.</span></span>  
* <span data-ttu-id="ebe44-139">**$filter =\<您篩選陳述式\>** -toospecify，hello 為基礎，支援的篩選欄位，您有興趣的資料錄的 hello 類型</span><span class="sxs-lookup"><span data-stu-id="ebe44-139">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="ebe44-140">支援的篩選欄位和運算子</span><span class="sxs-lookup"><span data-stu-id="ebe44-140">Supported filter fields and operators</span></span>
<span data-ttu-id="ebe44-141">您有興趣的資料錄 toospecify hello 類型，您可以建置可包含一或多種 hello 下列篩選欄位的篩選陳述式：</span><span class="sxs-lookup"><span data-stu-id="ebe44-141">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="ebe44-142">[signinDateTime](#signindatetime) - 定義日期或日期範圍</span><span class="sxs-lookup"><span data-stu-id="ebe44-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="ebe44-143">[userId](#userid) -定義特定的使用者基礎 hello 使用者的識別碼。</span><span class="sxs-lookup"><span data-stu-id="ebe44-143">[userId](#userid) - defines a specific user based hello user's ID.</span></span>
* <span data-ttu-id="ebe44-144">[userPrincipalName](#userprincipalname) -定義特定的使用者基礎 hello 使用者的使用者主體名稱 (UPN)</span><span class="sxs-lookup"><span data-stu-id="ebe44-144">[userPrincipalName](#userprincipalname) - defines a specific user based hello user's user principal name (UPN)</span></span>
* <span data-ttu-id="ebe44-145">[appId](#appid) -定義特定的應用程式基礎 hello 應用程式的識別碼</span><span class="sxs-lookup"><span data-stu-id="ebe44-145">[appId](#appid) - defines a specific app based hello app's ID</span></span>
* <span data-ttu-id="ebe44-146">[appDisplayName](#appdisplayname) -定義特定的應用程式基礎 hello 應用程式的顯示名稱</span><span class="sxs-lookup"><span data-stu-id="ebe44-146">[appDisplayName](#appdisplayname) - defines a specific app based hello app's display name</span></span>
* <span data-ttu-id="ebe44-147">[loginStatus](#loginStatus) -定義 hello hello 登入狀態 (成功 / 失敗)</span><span class="sxs-lookup"><span data-stu-id="ebe44-147">[loginStatus](#loginStatus) - defines hello status of hello logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="ebe44-148">使用圖表總管，當您 hello 需要 toouse hello 正確每個字母的案例是篩選欄位。</span><span class="sxs-lookup"><span data-stu-id="ebe44-148">When using Graph Explorer, you hello need toouse hello correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="ebe44-149">toonarrow hello hello 傳回的資料範圍下，您可以建立 hello 支援篩選和篩選欄位的組合。</span><span class="sxs-lookup"><span data-stu-id="ebe44-149">toonarrow down hello scope of hello returned data, you can build combinations of hello supported filters and filter fields.</span></span> <span data-ttu-id="ebe44-150">例如，hello 下列陳述式會傳回 hello 年 7 月 6 日完成 2016 年 7 月 1 日到 2016年之間的前 10 筆記錄：</span><span class="sxs-lookup"><span data-stu-id="ebe44-150">For example, hello following statement returns hello top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="ebe44-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="ebe44-151">signinDateTime</span></span>
<span data-ttu-id="ebe44-152">**支援的運算子**：eq、ge、le、gt、lt</span><span class="sxs-lookup"><span data-stu-id="ebe44-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="ebe44-153">**範例**：</span><span class="sxs-lookup"><span data-stu-id="ebe44-153">**Example**:</span></span>

<span data-ttu-id="ebe44-154">使用特定日期</span><span class="sxs-lookup"><span data-stu-id="ebe44-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="ebe44-155">使用日期範圍</span><span class="sxs-lookup"><span data-stu-id="ebe44-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="ebe44-156">**注意**：</span><span class="sxs-lookup"><span data-stu-id="ebe44-156">**Notes**:</span></span>

<span data-ttu-id="ebe44-157">hello datetime 參數應該是以 hello UTC 格式</span><span class="sxs-lookup"><span data-stu-id="ebe44-157">hello datetime parameter should be in hello UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="ebe44-158">userId</span><span class="sxs-lookup"><span data-stu-id="ebe44-158">userId</span></span>
<span data-ttu-id="ebe44-159">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="ebe44-159">**Supported operators**: eq</span></span>

<span data-ttu-id="ebe44-160">**範例**：</span><span class="sxs-lookup"><span data-stu-id="ebe44-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="ebe44-161">**注意**：</span><span class="sxs-lookup"><span data-stu-id="ebe44-161">**Notes**:</span></span>

<span data-ttu-id="ebe44-162">使用者識別碼 hello 值是字串值</span><span class="sxs-lookup"><span data-stu-id="ebe44-162">hello value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="ebe44-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="ebe44-163">userPrincipalName</span></span>
<span data-ttu-id="ebe44-164">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="ebe44-164">**Supported operators**: eq</span></span>

<span data-ttu-id="ebe44-165">**範例**：</span><span class="sxs-lookup"><span data-stu-id="ebe44-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="ebe44-166">**注意**：</span><span class="sxs-lookup"><span data-stu-id="ebe44-166">**Notes**:</span></span>

<span data-ttu-id="ebe44-167">userPrincipalName hello 值是字串值</span><span class="sxs-lookup"><span data-stu-id="ebe44-167">hello value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="ebe44-168">appId</span><span class="sxs-lookup"><span data-stu-id="ebe44-168">appId</span></span>
<span data-ttu-id="ebe44-169">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="ebe44-169">**Supported operators**: eq</span></span>

<span data-ttu-id="ebe44-170">**範例**：</span><span class="sxs-lookup"><span data-stu-id="ebe44-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="ebe44-171">**注意**：</span><span class="sxs-lookup"><span data-stu-id="ebe44-171">**Notes**:</span></span>

<span data-ttu-id="ebe44-172">hello appId 值是字串值</span><span class="sxs-lookup"><span data-stu-id="ebe44-172">hello value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="ebe44-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="ebe44-173">appDisplayName</span></span>
<span data-ttu-id="ebe44-174">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="ebe44-174">**Supported operators**: eq</span></span>

<span data-ttu-id="ebe44-175">**範例**：</span><span class="sxs-lookup"><span data-stu-id="ebe44-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="ebe44-176">**注意**：</span><span class="sxs-lookup"><span data-stu-id="ebe44-176">**Notes**:</span></span>

<span data-ttu-id="ebe44-177">appDisplayName hello 值是字串值</span><span class="sxs-lookup"><span data-stu-id="ebe44-177">hello value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="ebe44-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="ebe44-178">loginStatus</span></span>
<span data-ttu-id="ebe44-179">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="ebe44-179">**Supported operators**: eq</span></span>

<span data-ttu-id="ebe44-180">**範例**：</span><span class="sxs-lookup"><span data-stu-id="ebe44-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="ebe44-181">**注意**：</span><span class="sxs-lookup"><span data-stu-id="ebe44-181">**Notes**:</span></span>

<span data-ttu-id="ebe44-182">有兩個選項的 hello loginStatus: 0-成功，1-失敗</span><span class="sxs-lookup"><span data-stu-id="ebe44-182">There are two options for hello loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="ebe44-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ebe44-183">Next steps</span></span>
* <span data-ttu-id="ebe44-184">您想 toosee 範例已篩選的登入活動？</span><span class="sxs-lookup"><span data-stu-id="ebe44-184">Do you want toosee examples for filtered sign-in activities?</span></span> <span data-ttu-id="ebe44-185">簽出 hello [Azure Active Directory 登入活動報表 API 範例](active-directory-reporting-api-sign-in-activity-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="ebe44-185">Check out hello [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="ebe44-186">您想深入了解 hello Azure AD 報告 API tooknow 嗎？</span><span class="sxs-lookup"><span data-stu-id="ebe44-186">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="ebe44-187">請參閱[開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ebe44-187">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>


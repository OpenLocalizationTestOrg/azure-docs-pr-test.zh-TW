---
title: "aaaAzure Active Directory 稽核 API 參考 |Microsoft 文件"
description: "Tooget 以 hello Azure Active Directory 稽核應用程式開發介面的啟動方式"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="8d108-103">Azure Active Directory 稽核 API 參考</span><span class="sxs-lookup"><span data-stu-id="8d108-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="8d108-104">本主題是有關 hello Azure Active Directory 的主題集合的一部分報告應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="8d108-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="8d108-105">Azure AD 報告 api 還可讓您的 API tooaccess 稽核資料使用程式碼或相關的工具。</span><span class="sxs-lookup"><span data-stu-id="8d108-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="8d108-106">本主題的 hello 範圍是 tooprovide hello 的相關參考資訊**稽核 API**。</span><span class="sxs-lookup"><span data-stu-id="8d108-106">hello scope of this topic is tooprovide you with reference information about hello **audit API**.</span></span>

<span data-ttu-id="8d108-107">請參閱：</span><span class="sxs-lookup"><span data-stu-id="8d108-107">See:</span></span>

* <span data-ttu-id="8d108-108">[稽核記錄](active-directory-reporting-azure-portal.md#activity-reports)以取得詳細概念資訊</span><span class="sxs-lookup"><span data-stu-id="8d108-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="8d108-109">[開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)的 hello reporting API 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8d108-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


<span data-ttu-id="8d108-110">關於：</span><span class="sxs-lookup"><span data-stu-id="8d108-110">For:</span></span>

- <span data-ttu-id="8d108-111">閱讀常見問題集，請參閱我們的[常見問題集](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="8d108-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="8d108-112">問題，請[提出支援票證](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="8d108-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-hello-data"></a><span data-ttu-id="8d108-113">誰可以存取 hello 資料？</span><span class="sxs-lookup"><span data-stu-id="8d108-113">Who can access hello data?</span></span>
* <span data-ttu-id="8d108-114">Hello 安全性系統管理員或安全性 Reader 角色中的使用者</span><span class="sxs-lookup"><span data-stu-id="8d108-114">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="8d108-115">全域管理員</span><span class="sxs-lookup"><span data-stu-id="8d108-115">Global Admins</span></span>
* <span data-ttu-id="8d108-116">任何已授權 tooaccess hello API 的應用程式 （只會根據全域系統管理員權限，應用程式授權可以是安裝程式）</span><span class="sxs-lookup"><span data-stu-id="8d108-116">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d108-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="8d108-117">Prerequisites</span></span>
<span data-ttu-id="8d108-118">透過此報告的順序 tooaccess 中 hello Reporting API，您必須具有：</span><span class="sxs-lookup"><span data-stu-id="8d108-118">In order tooaccess this report through hello Reporting API, you must have:</span></span>

* <span data-ttu-id="8d108-119">[Azure Active Directory Free 或更好的版本](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="8d108-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="8d108-120">已完成的 hello[必要條件 tooaccess hello Azure AD 報告 API](active-directory-reporting-api-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="8d108-120">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="8d108-121">存取 hello API</span><span class="sxs-lookup"><span data-stu-id="8d108-121">Accessing hello API</span></span>
<span data-ttu-id="8d108-122">您可以存取此應用程式開發介面透過 hello[圖表總管](https://graphexplorer2.cloudapp.net)或以程式設計方式使用，例如 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="8d108-122">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="8d108-123">PowerShell toocorrectly 解譯 hello AAD Graph REST 呼叫中使用的 OData 篩選器語法的您必須使用 hello 倒單引號 (也稱為： 抑音符號) 字元太 「 逸出"hello $ 字元。</span><span class="sxs-lookup"><span data-stu-id="8d108-123">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="8d108-124">hello 倒單引號字元做為[PowerShell 的逸出字元](https://technet.microsoft.com/library/hh847755.aspx)，讓 PowerShell toodo hello $ 字元，常值解譯，同時避免混淆做為 PowerShell 變數的名稱 (亦即： $filter)。</span><span class="sxs-lookup"><span data-stu-id="8d108-124">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="8d108-125">本主題的 hello 重點是在 hello 圖表總管。</span><span class="sxs-lookup"><span data-stu-id="8d108-125">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="8d108-126">如需 PowerShell 範例，請參閱此 [PowerShell 指令碼](active-directory-reporting-api-audit-samples.md#powershell-script)。</span><span class="sxs-lookup"><span data-stu-id="8d108-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="8d108-127">API 端點</span><span class="sxs-lookup"><span data-stu-id="8d108-127">API Endpoint</span></span>
<span data-ttu-id="8d108-128">您可以存取此應用程式開發介面，使用下列 URI 的 hello:</span><span class="sxs-lookup"><span data-stu-id="8d108-128">You can access this API using hello following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="8d108-129">Hello hello Azure AD 稽核 API （使用 OData 分頁） 傳回的記錄數目沒有限制。</span><span class="sxs-lookup"><span data-stu-id="8d108-129">There is no limit on hello number of records returned by hello Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="8d108-130">如需報告資料的保留限制，請參閱 [報告保留原則](active-directory-reporting-retention.md)。</span><span class="sxs-lookup"><span data-stu-id="8d108-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="8d108-131">這個呼叫會傳回批次中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="8d108-131">This call returns hello data in batches.</span></span> <span data-ttu-id="8d108-132">每個批次的上限為 1000 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="8d108-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="8d108-133">tooget hello 下一個批次的記錄，以使用 hello 下一步 連結。</span><span class="sxs-lookup"><span data-stu-id="8d108-133">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="8d108-134">收到 hello 第一組傳回的記錄中的 hello skiptoken 資訊。</span><span class="sxs-lookup"><span data-stu-id="8d108-134">Get hello skiptoken information from hello first set of returned records.</span></span> <span data-ttu-id="8d108-135">hello 跳過權杖會在 hello hello 結果集的結尾。</span><span class="sxs-lookup"><span data-stu-id="8d108-135">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="8d108-136">支援的篩選器</span><span class="sxs-lookup"><span data-stu-id="8d108-136">Supported filters</span></span>
<span data-ttu-id="8d108-137">您可以縮小 hello 應用程式開發介面所傳回的記錄數目的篩選器的形式呼叫。</span><span class="sxs-lookup"><span data-stu-id="8d108-137">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="8d108-138">登入應用程式開發介面支援的相關的資料，下列篩選器的 hello:</span><span class="sxs-lookup"><span data-stu-id="8d108-138">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="8d108-139">**$top =\<傳回的記錄 toobe 數目\>** -toolimit hello 數傳回的記錄。</span><span class="sxs-lookup"><span data-stu-id="8d108-139">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="8d108-140">這是一項昂貴的作業。</span><span class="sxs-lookup"><span data-stu-id="8d108-140">This is an expensive operation.</span></span> <span data-ttu-id="8d108-141">如果您想要 tooreturn 數以千計的物件，則不應使用此篩選條件。</span><span class="sxs-lookup"><span data-stu-id="8d108-141">You should not use this filter if you want tooreturn thousands of objects.</span></span>     
* <span data-ttu-id="8d108-142">**$filter =\<您篩選陳述式\>** -toospecify，hello 為基礎，支援的篩選欄位，您有興趣的資料錄的 hello 類型</span><span class="sxs-lookup"><span data-stu-id="8d108-142">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="8d108-143">支援的篩選欄位和運算子</span><span class="sxs-lookup"><span data-stu-id="8d108-143">Supported filter fields and operators</span></span>
<span data-ttu-id="8d108-144">您有興趣的資料錄 toospecify hello 類型，您可以建置可包含一或多種 hello 下列篩選欄位的篩選陳述式：</span><span class="sxs-lookup"><span data-stu-id="8d108-144">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="8d108-145">[activityDate](#activitydate) - 定義日期或日期範圍</span><span class="sxs-lookup"><span data-stu-id="8d108-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="8d108-146">[類別](#category)-定義您想要 toofilter hello 分類。</span><span class="sxs-lookup"><span data-stu-id="8d108-146">[category](#category) - defines hello category you want toofilter on.</span></span>
* <span data-ttu-id="8d108-147">[activityStatus](#activitystatus) -定義 hello 活動狀態</span><span class="sxs-lookup"><span data-stu-id="8d108-147">[activityStatus](#activitystatus) - defines hello status of an activity</span></span>
* <span data-ttu-id="8d108-148">[activityType](#activitytype) -定義 hello 活動類型</span><span class="sxs-lookup"><span data-stu-id="8d108-148">[activityType](#activitytype)  - defines hello type of an activity</span></span>
* <span data-ttu-id="8d108-149">[活動](#activity)-hello 活動定義為字串</span><span class="sxs-lookup"><span data-stu-id="8d108-149">[activity](#activity) - defines hello activity as string</span></span>  
* <span data-ttu-id="8d108-150">[動作項目/名稱](#actorname)-hello 演員姓名形式定義 hello 動作項目</span><span class="sxs-lookup"><span data-stu-id="8d108-150">[actor/name](#actorname) -   defines hello actor in form of hello actor's name</span></span>
* <span data-ttu-id="8d108-151">[動作項目/objectid](#actorobjectid) -hello 的執行者識別碼形式定義 hello 動作項目</span><span class="sxs-lookup"><span data-stu-id="8d108-151">[actor/objectid](#actorobjectid) - defines hello actor in form of hello actor's ID</span></span>   
* <span data-ttu-id="8d108-152">[動作項目/upn](#actorupn) -hello 執行者的使用者主要名稱 (UPN) 形式定義 hello 動作項目</span><span class="sxs-lookup"><span data-stu-id="8d108-152">[actor/upn](#actorupn)  - defines hello actor in form of hello actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="8d108-153">[目標/名稱](#targetname)-hello 演員姓名形式定義 hello 目標</span><span class="sxs-lookup"><span data-stu-id="8d108-153">[target/name](#targetname)  - defines hello target in form of hello actor's name</span></span>
* <span data-ttu-id="8d108-154">[目標/objectid](#targetobjectid) -hello 目標識別碼形式定義 hello 目標</span><span class="sxs-lookup"><span data-stu-id="8d108-154">[target/objectid](#targetobjectid) - defines hello target in form of hello target's ID</span></span>  
* <span data-ttu-id="8d108-155">[目標/upn](#targetupn) -hello 執行者的使用者主要名稱 (UPN) 形式定義 hello 動作項目</span><span class="sxs-lookup"><span data-stu-id="8d108-155">[target/upn](#targetupn) - defines hello actor in form of hello actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="8d108-156">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="8d108-156">activityDate</span></span>
<span data-ttu-id="8d108-157">**支援的運算子**：eq、ge、le、gt、lt</span><span class="sxs-lookup"><span data-stu-id="8d108-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="8d108-158">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d108-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="8d108-159">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8d108-159">**Notes**:</span></span>

<span data-ttu-id="8d108-160">datetime 應採用 UTC 格式</span><span class="sxs-lookup"><span data-stu-id="8d108-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="8d108-161">category</span><span class="sxs-lookup"><span data-stu-id="8d108-161">category</span></span>

<span data-ttu-id="8d108-162">**支援的值**：</span><span class="sxs-lookup"><span data-stu-id="8d108-162">**Supported values**:</span></span>

| <span data-ttu-id="8d108-163">類別</span><span class="sxs-lookup"><span data-stu-id="8d108-163">Category</span></span>                         | <span data-ttu-id="8d108-164">值</span><span class="sxs-lookup"><span data-stu-id="8d108-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="8d108-165">核心目錄</span><span class="sxs-lookup"><span data-stu-id="8d108-165">Core Directory</span></span>                   | <span data-ttu-id="8d108-166">目錄</span><span class="sxs-lookup"><span data-stu-id="8d108-166">Directory</span></span> |
| <span data-ttu-id="8d108-167">自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="8d108-167">Self-service Password Management</span></span> | <span data-ttu-id="8d108-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="8d108-168">SSPR</span></span>      |
| <span data-ttu-id="8d108-169">自助式群組管理</span><span class="sxs-lookup"><span data-stu-id="8d108-169">Self-service Group Management</span></span>    | <span data-ttu-id="8d108-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="8d108-170">SSGM</span></span>      |
| <span data-ttu-id="8d108-171">帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="8d108-171">Account Provisioning</span></span>             | <span data-ttu-id="8d108-172">Sync</span><span class="sxs-lookup"><span data-stu-id="8d108-172">Sync</span></span>      |
| <span data-ttu-id="8d108-173">自動密碼變換</span><span class="sxs-lookup"><span data-stu-id="8d108-173">Automated Password Rollover</span></span>      | <span data-ttu-id="8d108-174">自動密碼變換</span><span class="sxs-lookup"><span data-stu-id="8d108-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="8d108-175">身分識別保護</span><span class="sxs-lookup"><span data-stu-id="8d108-175">Identity Protection</span></span>              | <span data-ttu-id="8d108-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="8d108-176">IdentityProtection</span></span> |
| <span data-ttu-id="8d108-177">受邀的使用者</span><span class="sxs-lookup"><span data-stu-id="8d108-177">Invited Users</span></span>                    | <span data-ttu-id="8d108-178">受邀的使用者</span><span class="sxs-lookup"><span data-stu-id="8d108-178">Invited Users</span></span> |
| <span data-ttu-id="8d108-179">MIM 服務</span><span class="sxs-lookup"><span data-stu-id="8d108-179">MIM Service</span></span>                      | <span data-ttu-id="8d108-180">MIM 服務</span><span class="sxs-lookup"><span data-stu-id="8d108-180">MIM Service</span></span> |



<span data-ttu-id="8d108-181">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="8d108-181">**Supported operators**: eq</span></span>

<span data-ttu-id="8d108-182">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d108-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="8d108-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="8d108-183">activityStatus</span></span>

<span data-ttu-id="8d108-184">**支援的值**：</span><span class="sxs-lookup"><span data-stu-id="8d108-184">**Supported values**:</span></span>

| <span data-ttu-id="8d108-185">活動狀態</span><span class="sxs-lookup"><span data-stu-id="8d108-185">Activity Status</span></span> | <span data-ttu-id="8d108-186">值</span><span class="sxs-lookup"><span data-stu-id="8d108-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="8d108-187">成功</span><span class="sxs-lookup"><span data-stu-id="8d108-187">Success</span></span>         | <span data-ttu-id="8d108-188">0</span><span class="sxs-lookup"><span data-stu-id="8d108-188">0</span></span>     |
| <span data-ttu-id="8d108-189">失敗</span><span class="sxs-lookup"><span data-stu-id="8d108-189">Failure</span></span>         | <span data-ttu-id="8d108-190">- 1</span><span class="sxs-lookup"><span data-stu-id="8d108-190">- 1</span></span>   |

<span data-ttu-id="8d108-191">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="8d108-191">**Supported operators**: eq</span></span>

<span data-ttu-id="8d108-192">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d108-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="8d108-193">activityType</span><span class="sxs-lookup"><span data-stu-id="8d108-193">activityType</span></span>
<span data-ttu-id="8d108-194">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="8d108-194">**Supported operators**: eq</span></span>

<span data-ttu-id="8d108-195">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d108-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="8d108-196">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8d108-196">**Notes**:</span></span>

<span data-ttu-id="8d108-197">區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8d108-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="8d108-198">activity</span><span class="sxs-lookup"><span data-stu-id="8d108-198">activity</span></span>
<span data-ttu-id="8d108-199">**支援的運算子**：eq、contains、startsWith</span><span class="sxs-lookup"><span data-stu-id="8d108-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="8d108-200">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d108-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="8d108-201">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8d108-201">**Notes**:</span></span>

<span data-ttu-id="8d108-202">區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8d108-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="8d108-203">actor/name</span><span class="sxs-lookup"><span data-stu-id="8d108-203">actor/name</span></span>
<span data-ttu-id="8d108-204">**支援的運算子**：eq、contains、startsWith</span><span class="sxs-lookup"><span data-stu-id="8d108-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="8d108-205">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d108-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="8d108-206">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8d108-206">**Notes**:</span></span>

<span data-ttu-id="8d108-207">不區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8d108-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="8d108-208">actor/objectid</span><span class="sxs-lookup"><span data-stu-id="8d108-208">actor/objectId</span></span>
<span data-ttu-id="8d108-209">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="8d108-209">**Supported operators**: eq</span></span>

<span data-ttu-id="8d108-210">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d108-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="8d108-211">target/name</span><span class="sxs-lookup"><span data-stu-id="8d108-211">target/name</span></span>
<span data-ttu-id="8d108-212">**支援的運算子**：eq、contains、startsWith</span><span class="sxs-lookup"><span data-stu-id="8d108-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="8d108-213">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d108-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="8d108-214">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8d108-214">**Notes**:</span></span>

<span data-ttu-id="8d108-215">不區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8d108-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="8d108-216">target/upn</span><span class="sxs-lookup"><span data-stu-id="8d108-216">target/upn</span></span>
<span data-ttu-id="8d108-217">**支援的運算子**：eq、startsWith</span><span class="sxs-lookup"><span data-stu-id="8d108-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="8d108-218">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d108-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="8d108-219">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8d108-219">**Notes**:</span></span>

* <span data-ttu-id="8d108-220">不區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8d108-220">Case-insensitive</span></span>
* <span data-ttu-id="8d108-221">查詢 Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity 時，需要 tooadd hello 完整的命名空間</span><span class="sxs-lookup"><span data-stu-id="8d108-221">You need tooadd hello full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="8d108-222">target/objectid</span><span class="sxs-lookup"><span data-stu-id="8d108-222">target/objectId</span></span>
<span data-ttu-id="8d108-223">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="8d108-223">**Supported operators**: eq</span></span>

<span data-ttu-id="8d108-224">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d108-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="8d108-225">actor/upn</span><span class="sxs-lookup"><span data-stu-id="8d108-225">actor/upn</span></span>
<span data-ttu-id="8d108-226">**支援的運算子**：eq、startsWith</span><span class="sxs-lookup"><span data-stu-id="8d108-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="8d108-227">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d108-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="8d108-228">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8d108-228">**Notes**:</span></span>

* <span data-ttu-id="8d108-229">不區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8d108-229">Case-insensitive</span></span> 
* <span data-ttu-id="8d108-230">查詢 Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity 時，需要 tooadd hello 完整的命名空間</span><span class="sxs-lookup"><span data-stu-id="8d108-230">You need tooadd hello full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="8d108-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8d108-231">Next Steps</span></span>
* <span data-ttu-id="8d108-232">您想 toosee 範例篩選的系統活動？</span><span class="sxs-lookup"><span data-stu-id="8d108-232">Do you want toosee examples for filtered system activities?</span></span> <span data-ttu-id="8d108-233">簽出 hello [Azure Active Directory 稽核 API 範例](active-directory-reporting-api-audit-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="8d108-233">Check out hello [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="8d108-234">您想深入了解 hello Azure AD 報告 API tooknow 嗎？</span><span class="sxs-lookup"><span data-stu-id="8d108-234">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="8d108-235">請參閱[開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="8d108-235">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>


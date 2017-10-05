---
title: "Azure Active Directory 稽核 API 參考 | Microsoft Docs"
description: "如何開始使用 Azure Active Directory 稽核 API"
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
ms.openlocfilehash: 573e940c5390e7b990d889681eb37b73c5b253d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="8b29f-103">Azure Active Directory 稽核 API 參考</span><span class="sxs-lookup"><span data-stu-id="8b29f-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="8b29f-104">本主題是 Azure Active Directory 報告 API 相關主題集合的一部分。</span><span class="sxs-lookup"><span data-stu-id="8b29f-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="8b29f-105">Azure AD 報告提供的 API 可讓您使用程式碼或相關工具來存取稽核資料。</span><span class="sxs-lookup"><span data-stu-id="8b29f-105">Azure AD reporting provides you with an API that enables you to access audit data using code or related tools.</span></span>
<span data-ttu-id="8b29f-106">本主題的範疇是為您提供有關 **稽核 API**的參考資訊。</span><span class="sxs-lookup"><span data-stu-id="8b29f-106">The scope of this topic is to provide you with reference information about the **audit API**.</span></span>

<span data-ttu-id="8b29f-107">請參閱：</span><span class="sxs-lookup"><span data-stu-id="8b29f-107">See:</span></span>

* <span data-ttu-id="8b29f-108">[稽核記錄](active-directory-reporting-azure-portal.md#activity-reports)以取得詳細概念資訊</span><span class="sxs-lookup"><span data-stu-id="8b29f-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="8b29f-109">[開始使用 Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md) 以取得報告 API 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8b29f-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


<span data-ttu-id="8b29f-110">關於：</span><span class="sxs-lookup"><span data-stu-id="8b29f-110">For:</span></span>

- <span data-ttu-id="8b29f-111">閱讀常見問題集，請參閱我們的[常見問題集](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="8b29f-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="8b29f-112">問題，請[提出支援票證](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="8b29f-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-the-data"></a><span data-ttu-id="8b29f-113">誰可以存取資料？</span><span class="sxs-lookup"><span data-stu-id="8b29f-113">Who can access the data?</span></span>
* <span data-ttu-id="8b29f-114">具有安全性系統管理員或安全性讀取器角色的使用者</span><span class="sxs-lookup"><span data-stu-id="8b29f-114">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="8b29f-115">全域管理員</span><span class="sxs-lookup"><span data-stu-id="8b29f-115">Global Admins</span></span>
* <span data-ttu-id="8b29f-116">任何獲得授權存取 API 的應用程式 (只可以根據全域管理員的權限來設定應用程式授權)</span><span class="sxs-lookup"><span data-stu-id="8b29f-116">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b29f-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="8b29f-117">Prerequisites</span></span>
<span data-ttu-id="8b29f-118">若要透過報告 API 來存取此報告，您必須具有︰</span><span class="sxs-lookup"><span data-stu-id="8b29f-118">In order to access this report through the Reporting API, you must have:</span></span>

* <span data-ttu-id="8b29f-119">[Azure Active Directory Free 或更好的版本](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="8b29f-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="8b29f-120">了解 [存取 Azure AD 報告 API 的必要條件](active-directory-reporting-api-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="8b29f-120">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="8b29f-121">存取 API</span><span class="sxs-lookup"><span data-stu-id="8b29f-121">Accessing the API</span></span>
<span data-ttu-id="8b29f-122">您可以透過 [Graph 總管](https://graphexplorer2.cloudapp.net) 或以程式設計方式使用 PowerShell 來存取此 API。</span><span class="sxs-lookup"><span data-stu-id="8b29f-122">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="8b29f-123">為了讓 PowerShell 正確地解譯 AAD Graph REST 呼叫中使用的 OData 篩選語法，您必須使用倒單引號 (也稱為︰抑音符號) 字元來「逸出」$ 字元。</span><span class="sxs-lookup"><span data-stu-id="8b29f-123">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="8b29f-124">倒單引號字元可做為 [PowerShell 的逸出字元](https://technet.microsoft.com/library/hh847755.aspx)，讓 PowerShell 進行 $ 字元的常值解譯，並且避免將它與 PowerShell 變數名稱 (例如︰$filter) 搞混。</span><span class="sxs-lookup"><span data-stu-id="8b29f-124">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="8b29f-125">本主題的重點在於 Graph 總管。</span><span class="sxs-lookup"><span data-stu-id="8b29f-125">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="8b29f-126">如需 PowerShell 範例，請參閱此 [PowerShell 指令碼](active-directory-reporting-api-audit-samples.md#powershell-script)。</span><span class="sxs-lookup"><span data-stu-id="8b29f-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="8b29f-127">API 端點</span><span class="sxs-lookup"><span data-stu-id="8b29f-127">API Endpoint</span></span>
<span data-ttu-id="8b29f-128">您可以使用下列 URI 來存取此 API︰</span><span class="sxs-lookup"><span data-stu-id="8b29f-128">You can access this API using the following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="8b29f-129">Azure AD 稽核 API (使用 OData 分頁) 傳回的記錄筆數沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="8b29f-129">There is no limit on the number of records returned by the Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="8b29f-130">如需報告資料的保留限制，請參閱 [報告保留原則](active-directory-reporting-retention.md)。</span><span class="sxs-lookup"><span data-stu-id="8b29f-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="8b29f-131">此呼叫會分批傳回資料。</span><span class="sxs-lookup"><span data-stu-id="8b29f-131">This call returns the data in batches.</span></span> <span data-ttu-id="8b29f-132">每個批次的上限為 1000 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="8b29f-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="8b29f-133">若要取得下一批記錄，請使用 [下一個] 連結。</span><span class="sxs-lookup"><span data-stu-id="8b29f-133">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="8b29f-134">從第一組傳回的資料取得 skiptoken 資訊。</span><span class="sxs-lookup"><span data-stu-id="8b29f-134">Get the skiptoken information from the first set of returned records.</span></span> <span data-ttu-id="8b29f-135">略過 Token 位於結果集的結尾。</span><span class="sxs-lookup"><span data-stu-id="8b29f-135">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="8b29f-136">支援的篩選器</span><span class="sxs-lookup"><span data-stu-id="8b29f-136">Supported filters</span></span>
<span data-ttu-id="8b29f-137">您可以篩選形式縮小 API 呼叫所傳回的記錄筆數。</span><span class="sxs-lookup"><span data-stu-id="8b29f-137">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="8b29f-138">對於登入 API 相關資料，支援下列篩選︰</span><span class="sxs-lookup"><span data-stu-id="8b29f-138">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="8b29f-139">**$top=\<傳回的記錄筆數\>** - 限制傳回的記錄筆數。</span><span class="sxs-lookup"><span data-stu-id="8b29f-139">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="8b29f-140">這是一項昂貴的作業。</span><span class="sxs-lookup"><span data-stu-id="8b29f-140">This is an expensive operation.</span></span> <span data-ttu-id="8b29f-141">如果您想要傳回數千個物件，則不應該使用此篩選器。</span><span class="sxs-lookup"><span data-stu-id="8b29f-141">You should not use this filter if you want to return thousands of objects.</span></span>     
* <span data-ttu-id="8b29f-142">**$filter=\<您的篩選陳述式\>** - 根據支援的篩選欄位，指定您關心的記錄類型</span><span class="sxs-lookup"><span data-stu-id="8b29f-142">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="8b29f-143">支援的篩選欄位和運算子</span><span class="sxs-lookup"><span data-stu-id="8b29f-143">Supported filter fields and operators</span></span>
<span data-ttu-id="8b29f-144">若要指定您關心的記錄類型，您可以建立一個篩選陳述式，該陳述式可包含下列其中一個篩選欄位或其組合︰</span><span class="sxs-lookup"><span data-stu-id="8b29f-144">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="8b29f-145">[activityDate](#activitydate) - 定義日期或日期範圍</span><span class="sxs-lookup"><span data-stu-id="8b29f-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="8b29f-146">[category](#category) - 定義您想要篩選的類別。</span><span class="sxs-lookup"><span data-stu-id="8b29f-146">[category](#category) - defines the category you want to filter on.</span></span>
* <span data-ttu-id="8b29f-147">[activityStatus](#activitystatus) - 定義活動狀態</span><span class="sxs-lookup"><span data-stu-id="8b29f-147">[activityStatus](#activitystatus) - defines the status of an activity</span></span>
* <span data-ttu-id="8b29f-148">[activityType](#activitytype) - 定義活動類型</span><span class="sxs-lookup"><span data-stu-id="8b29f-148">[activityType](#activitytype)  - defines the type of an activity</span></span>
* <span data-ttu-id="8b29f-149">[activity](#activity) - 將活動定義為字串</span><span class="sxs-lookup"><span data-stu-id="8b29f-149">[activity](#activity) - defines the activity as string</span></span>  
* <span data-ttu-id="8b29f-150">[actor/name](#actorname) - 以動作項目的名稱形式定義動作項目</span><span class="sxs-lookup"><span data-stu-id="8b29f-150">[actor/name](#actorname) -   defines the actor in form of the actor's name</span></span>
* <span data-ttu-id="8b29f-151">[actor/objectid](#actorobjectid) - 以動作項目的識別碼形式定義動作項目</span><span class="sxs-lookup"><span data-stu-id="8b29f-151">[actor/objectid](#actorobjectid) - defines the actor in form of the actor's ID</span></span>   
* <span data-ttu-id="8b29f-152">[actor/upn](#actorupn) - 以動作項目的使用者主體名稱 (UPN) 形式定義動作項目</span><span class="sxs-lookup"><span data-stu-id="8b29f-152">[actor/upn](#actorupn)  - defines the actor in form of the actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="8b29f-153">[target/name](#targetname) - 以動作項目的名稱形式定義目標</span><span class="sxs-lookup"><span data-stu-id="8b29f-153">[target/name](#targetname)  - defines the target in form of the actor's name</span></span>
* <span data-ttu-id="8b29f-154">[target/objectid](#targetobjectid) - 以目標的識別碼形式定義目標</span><span class="sxs-lookup"><span data-stu-id="8b29f-154">[target/objectid](#targetobjectid) - defines the target in form of the target's ID</span></span>  
* <span data-ttu-id="8b29f-155">[target/upn](#targetupn) - 以動作項目的使用者主體名稱 (UPN) 形式定義動作項目</span><span class="sxs-lookup"><span data-stu-id="8b29f-155">[target/upn](#targetupn) - defines the actor in form of the actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="8b29f-156">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="8b29f-156">activityDate</span></span>
<span data-ttu-id="8b29f-157">**支援的運算子**：eq、ge、le、gt、lt</span><span class="sxs-lookup"><span data-stu-id="8b29f-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="8b29f-158">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="8b29f-159">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-159">**Notes**:</span></span>

<span data-ttu-id="8b29f-160">datetime 應採用 UTC 格式</span><span class="sxs-lookup"><span data-stu-id="8b29f-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="8b29f-161">category</span><span class="sxs-lookup"><span data-stu-id="8b29f-161">category</span></span>

<span data-ttu-id="8b29f-162">**支援的值**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-162">**Supported values**:</span></span>

| <span data-ttu-id="8b29f-163">類別</span><span class="sxs-lookup"><span data-stu-id="8b29f-163">Category</span></span>                         | <span data-ttu-id="8b29f-164">值</span><span class="sxs-lookup"><span data-stu-id="8b29f-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="8b29f-165">核心目錄</span><span class="sxs-lookup"><span data-stu-id="8b29f-165">Core Directory</span></span>                   | <span data-ttu-id="8b29f-166">目錄</span><span class="sxs-lookup"><span data-stu-id="8b29f-166">Directory</span></span> |
| <span data-ttu-id="8b29f-167">自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="8b29f-167">Self-service Password Management</span></span> | <span data-ttu-id="8b29f-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="8b29f-168">SSPR</span></span>      |
| <span data-ttu-id="8b29f-169">自助式群組管理</span><span class="sxs-lookup"><span data-stu-id="8b29f-169">Self-service Group Management</span></span>    | <span data-ttu-id="8b29f-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="8b29f-170">SSGM</span></span>      |
| <span data-ttu-id="8b29f-171">帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="8b29f-171">Account Provisioning</span></span>             | <span data-ttu-id="8b29f-172">Sync</span><span class="sxs-lookup"><span data-stu-id="8b29f-172">Sync</span></span>      |
| <span data-ttu-id="8b29f-173">自動密碼變換</span><span class="sxs-lookup"><span data-stu-id="8b29f-173">Automated Password Rollover</span></span>      | <span data-ttu-id="8b29f-174">自動密碼變換</span><span class="sxs-lookup"><span data-stu-id="8b29f-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="8b29f-175">身分識別保護</span><span class="sxs-lookup"><span data-stu-id="8b29f-175">Identity Protection</span></span>              | <span data-ttu-id="8b29f-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="8b29f-176">IdentityProtection</span></span> |
| <span data-ttu-id="8b29f-177">受邀的使用者</span><span class="sxs-lookup"><span data-stu-id="8b29f-177">Invited Users</span></span>                    | <span data-ttu-id="8b29f-178">受邀的使用者</span><span class="sxs-lookup"><span data-stu-id="8b29f-178">Invited Users</span></span> |
| <span data-ttu-id="8b29f-179">MIM 服務</span><span class="sxs-lookup"><span data-stu-id="8b29f-179">MIM Service</span></span>                      | <span data-ttu-id="8b29f-180">MIM 服務</span><span class="sxs-lookup"><span data-stu-id="8b29f-180">MIM Service</span></span> |



<span data-ttu-id="8b29f-181">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="8b29f-181">**Supported operators**: eq</span></span>

<span data-ttu-id="8b29f-182">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="8b29f-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="8b29f-183">activityStatus</span></span>

<span data-ttu-id="8b29f-184">**支援的值**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-184">**Supported values**:</span></span>

| <span data-ttu-id="8b29f-185">活動狀態</span><span class="sxs-lookup"><span data-stu-id="8b29f-185">Activity Status</span></span> | <span data-ttu-id="8b29f-186">值</span><span class="sxs-lookup"><span data-stu-id="8b29f-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="8b29f-187">成功</span><span class="sxs-lookup"><span data-stu-id="8b29f-187">Success</span></span>         | <span data-ttu-id="8b29f-188">0</span><span class="sxs-lookup"><span data-stu-id="8b29f-188">0</span></span>     |
| <span data-ttu-id="8b29f-189">失敗</span><span class="sxs-lookup"><span data-stu-id="8b29f-189">Failure</span></span>         | <span data-ttu-id="8b29f-190">- 1</span><span class="sxs-lookup"><span data-stu-id="8b29f-190">- 1</span></span>   |

<span data-ttu-id="8b29f-191">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="8b29f-191">**Supported operators**: eq</span></span>

<span data-ttu-id="8b29f-192">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="8b29f-193">activityType</span><span class="sxs-lookup"><span data-stu-id="8b29f-193">activityType</span></span>
<span data-ttu-id="8b29f-194">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="8b29f-194">**Supported operators**: eq</span></span>

<span data-ttu-id="8b29f-195">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="8b29f-196">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-196">**Notes**:</span></span>

<span data-ttu-id="8b29f-197">區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8b29f-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="8b29f-198">activity</span><span class="sxs-lookup"><span data-stu-id="8b29f-198">activity</span></span>
<span data-ttu-id="8b29f-199">**支援的運算子**：eq、contains、startsWith</span><span class="sxs-lookup"><span data-stu-id="8b29f-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="8b29f-200">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="8b29f-201">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-201">**Notes**:</span></span>

<span data-ttu-id="8b29f-202">區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8b29f-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="8b29f-203">actor/name</span><span class="sxs-lookup"><span data-stu-id="8b29f-203">actor/name</span></span>
<span data-ttu-id="8b29f-204">**支援的運算子**：eq、contains、startsWith</span><span class="sxs-lookup"><span data-stu-id="8b29f-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="8b29f-205">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="8b29f-206">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-206">**Notes**:</span></span>

<span data-ttu-id="8b29f-207">不區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8b29f-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="8b29f-208">actor/objectid</span><span class="sxs-lookup"><span data-stu-id="8b29f-208">actor/objectId</span></span>
<span data-ttu-id="8b29f-209">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="8b29f-209">**Supported operators**: eq</span></span>

<span data-ttu-id="8b29f-210">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="8b29f-211">target/name</span><span class="sxs-lookup"><span data-stu-id="8b29f-211">target/name</span></span>
<span data-ttu-id="8b29f-212">**支援的運算子**：eq、contains、startsWith</span><span class="sxs-lookup"><span data-stu-id="8b29f-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="8b29f-213">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="8b29f-214">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-214">**Notes**:</span></span>

<span data-ttu-id="8b29f-215">不區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8b29f-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="8b29f-216">target/upn</span><span class="sxs-lookup"><span data-stu-id="8b29f-216">target/upn</span></span>
<span data-ttu-id="8b29f-217">**支援的運算子**：eq、startsWith</span><span class="sxs-lookup"><span data-stu-id="8b29f-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="8b29f-218">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="8b29f-219">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-219">**Notes**:</span></span>

* <span data-ttu-id="8b29f-220">不區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8b29f-220">Case-insensitive</span></span>
* <span data-ttu-id="8b29f-221">您需要時在查詢 Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity 時新增完整的命名空間</span><span class="sxs-lookup"><span data-stu-id="8b29f-221">You need to add the full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="8b29f-222">target/objectid</span><span class="sxs-lookup"><span data-stu-id="8b29f-222">target/objectId</span></span>
<span data-ttu-id="8b29f-223">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="8b29f-223">**Supported operators**: eq</span></span>

<span data-ttu-id="8b29f-224">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="8b29f-225">actor/upn</span><span class="sxs-lookup"><span data-stu-id="8b29f-225">actor/upn</span></span>
<span data-ttu-id="8b29f-226">**支援的運算子**：eq、startsWith</span><span class="sxs-lookup"><span data-stu-id="8b29f-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="8b29f-227">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="8b29f-228">**注意**：</span><span class="sxs-lookup"><span data-stu-id="8b29f-228">**Notes**:</span></span>

* <span data-ttu-id="8b29f-229">不區分大小寫</span><span class="sxs-lookup"><span data-stu-id="8b29f-229">Case-insensitive</span></span> 
* <span data-ttu-id="8b29f-230">您需要時在查詢 Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity 時新增完整的命名空間</span><span class="sxs-lookup"><span data-stu-id="8b29f-230">You need to add the full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="8b29f-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b29f-231">Next Steps</span></span>
* <span data-ttu-id="8b29f-232">您想要查看篩選過的系統活動範例嗎？</span><span class="sxs-lookup"><span data-stu-id="8b29f-232">Do you want to see examples for filtered system activities?</span></span> <span data-ttu-id="8b29f-233">請查看 [Azure Active Directory 稽核 API 範例](active-directory-reporting-api-audit-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="8b29f-233">Check out the [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="8b29f-234">您想要深入了解 Azure AD 報告 API 嗎？</span><span class="sxs-lookup"><span data-stu-id="8b29f-234">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="8b29f-235">請參閱 [開始使用 Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="8b29f-235">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>


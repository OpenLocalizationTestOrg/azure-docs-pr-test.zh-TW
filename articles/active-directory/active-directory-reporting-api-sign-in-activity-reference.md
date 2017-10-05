---
title: "Azure Active Directory 登入活動報告 API 參考 | Microsoft Docs"
description: "Azure Active Directory 登入活動報告 API 的參考"
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
ms.openlocfilehash: d83f1a899ba38dab2c1c1661adede87db6f88c20
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="e0711-103">Azure Active Directory 登入活動報告 API 參考</span><span class="sxs-lookup"><span data-stu-id="e0711-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="e0711-104">本主題是 Azure Active Directory 報告 API 相關主題集合的一部分。</span><span class="sxs-lookup"><span data-stu-id="e0711-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="e0711-105">Azure AD 報告提供的 API 可讓您使用程式碼或相關工具來存取登入活動報告資料。</span><span class="sxs-lookup"><span data-stu-id="e0711-105">Azure AD reporting provides you with an API that enables you to access sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="e0711-106">本主題的範疇是為您提供有關 **登入活動報告 API**的參考資訊。</span><span class="sxs-lookup"><span data-stu-id="e0711-106">The scope of this topic is to provide you with reference information about the **sign-in activity report API**.</span></span>

<span data-ttu-id="e0711-107">請參閱：</span><span class="sxs-lookup"><span data-stu-id="e0711-107">See:</span></span>

* <span data-ttu-id="e0711-108">[登入活動](active-directory-reporting-azure-portal.md#activity-reports) 以取得詳細概念資訊</span><span class="sxs-lookup"><span data-stu-id="e0711-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="e0711-109">[開始使用 Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md) 以取得報告 API 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e0711-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="who-can-access-the-api-data"></a><span data-ttu-id="e0711-110">誰可以存取 API 資料？</span><span class="sxs-lookup"><span data-stu-id="e0711-110">Who can access the API data?</span></span>
* <span data-ttu-id="e0711-111">具有安全性系統管理員或安全性讀取者角色的使用者和服務主體</span><span class="sxs-lookup"><span data-stu-id="e0711-111">Users and Service Principals in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="e0711-112">全域管理員</span><span class="sxs-lookup"><span data-stu-id="e0711-112">Global Admins</span></span>
* <span data-ttu-id="e0711-113">任何獲得授權存取 API 的應用程式 (只可以根據全域管理員的權限來設定應用程式授權)</span><span class="sxs-lookup"><span data-stu-id="e0711-113">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="e0711-114">若要設定應用程式存取權以存取安全性 API (例如登入事件)，請使用下列 PowerShell 將應用程式服務主體新增至安全性讀取者角色</span><span class="sxs-lookup"><span data-stu-id="e0711-114">To configure access for an application to access security APIs such as signin events, use the following PowerShell to add the applications Service Principal into the Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="e0711-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="e0711-115">Prerequisites</span></span>
<span data-ttu-id="e0711-116">若要透過報告 API 來存取此報告，您必須具有︰</span><span class="sxs-lookup"><span data-stu-id="e0711-116">To access this report through the reporting API, you must have:</span></span>

* <span data-ttu-id="e0711-117">[Azure Active Directory Premium P1 或 P2 版本](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="e0711-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="e0711-118">了解 [存取 Azure AD 報告 API 的必要條件](active-directory-reporting-api-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="e0711-118">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="e0711-119">存取 API</span><span class="sxs-lookup"><span data-stu-id="e0711-119">Accessing the API</span></span>
<span data-ttu-id="e0711-120">您可以透過 [Graph 總管](https://graphexplorer2.cloudapp.net) 或以程式設計方式使用 PowerShell 來存取此 API。</span><span class="sxs-lookup"><span data-stu-id="e0711-120">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="e0711-121">為了讓 PowerShell 正確地解譯 AAD Graph REST 呼叫中使用的 OData 篩選語法，您必須使用倒單引號 (也稱為︰抑音符號) 字元來「逸出」$ 字元。</span><span class="sxs-lookup"><span data-stu-id="e0711-121">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="e0711-122">倒單引號字元可做為 [PowerShell 的逸出字元](https://technet.microsoft.com/library/hh847755.aspx)，讓 PowerShell 進行 $ 字元的常值解譯，並且避免將它與 PowerShell 變數名稱 (例如︰$filter) 搞混。</span><span class="sxs-lookup"><span data-stu-id="e0711-122">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="e0711-123">本主題的重點在於 Graph 總管。</span><span class="sxs-lookup"><span data-stu-id="e0711-123">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="e0711-124">如需 PowerShell 範例，請參閱此 [PowerShell 指令碼](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script)。</span><span class="sxs-lookup"><span data-stu-id="e0711-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="e0711-125">API 端點</span><span class="sxs-lookup"><span data-stu-id="e0711-125">API Endpoint</span></span>
<span data-ttu-id="e0711-126">您可以使用下列基底 URI 來存取此 API︰</span><span class="sxs-lookup"><span data-stu-id="e0711-126">You can access this API using the following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="e0711-127">由於資料量的緣故，此 API 有一百萬筆傳回記錄的限制。</span><span class="sxs-lookup"><span data-stu-id="e0711-127">Due to the volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="e0711-128">此呼叫會分批傳回資料。</span><span class="sxs-lookup"><span data-stu-id="e0711-128">This call returns the data in batches.</span></span> <span data-ttu-id="e0711-129">每個批次的上限為 1000 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="e0711-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="e0711-130">若要取得下一批記錄，請使用 [下一個] 連結。</span><span class="sxs-lookup"><span data-stu-id="e0711-130">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="e0711-131">從第一組傳回的資料取得 [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) 資訊。</span><span class="sxs-lookup"><span data-stu-id="e0711-131">Get the [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from the first set of returned records.</span></span> <span data-ttu-id="e0711-132">略過 Token 位於結果集的結尾。</span><span class="sxs-lookup"><span data-stu-id="e0711-132">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="e0711-133">支援的篩選器</span><span class="sxs-lookup"><span data-stu-id="e0711-133">Supported filters</span></span>
<span data-ttu-id="e0711-134">您可以篩選形式縮小 API 呼叫所傳回的記錄筆數。</span><span class="sxs-lookup"><span data-stu-id="e0711-134">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="e0711-135">對於登入 API 相關資料，支援下列篩選︰</span><span class="sxs-lookup"><span data-stu-id="e0711-135">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="e0711-136">**$top=\<傳回的記錄筆數\>** - 限制傳回的記錄筆數。</span><span class="sxs-lookup"><span data-stu-id="e0711-136">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="e0711-137">這是一項昂貴的作業。</span><span class="sxs-lookup"><span data-stu-id="e0711-137">This is an expensive operation.</span></span> <span data-ttu-id="e0711-138">如果您想要傳回數千個物件，則不應該使用此篩選器。</span><span class="sxs-lookup"><span data-stu-id="e0711-138">You should not use this filter if you want to return thousands of objects.</span></span>  
* <span data-ttu-id="e0711-139">**$filter=\<您的篩選陳述式\>** - 根據支援的篩選欄位，指定您關心的記錄類型</span><span class="sxs-lookup"><span data-stu-id="e0711-139">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="e0711-140">支援的篩選欄位和運算子</span><span class="sxs-lookup"><span data-stu-id="e0711-140">Supported filter fields and operators</span></span>
<span data-ttu-id="e0711-141">若要指定您關心的記錄類型，您可以建立一個篩選陳述式，該陳述式可包含下列其中一個篩選欄位或其組合︰</span><span class="sxs-lookup"><span data-stu-id="e0711-141">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="e0711-142">[signinDateTime](#signindatetime) - 定義日期或日期範圍</span><span class="sxs-lookup"><span data-stu-id="e0711-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="e0711-143">[userId](#userid) - 根據使用者的識別碼定義特定使用者。</span><span class="sxs-lookup"><span data-stu-id="e0711-143">[userId](#userid) - defines a specific user based the user's ID.</span></span>
* <span data-ttu-id="e0711-144">[userPrincipalName](#userprincipalname) - 根據使用者的使用者主體名稱 (UPN) 定義特定使用者</span><span class="sxs-lookup"><span data-stu-id="e0711-144">[userPrincipalName](#userprincipalname) - defines a specific user based the user's user principal name (UPN)</span></span>
* <span data-ttu-id="e0711-145">[appId](#appid) - 根據應用程式的識別碼定義特定應用程式</span><span class="sxs-lookup"><span data-stu-id="e0711-145">[appId](#appid) - defines a specific app based the app's ID</span></span>
* <span data-ttu-id="e0711-146">[appDisplayName](#appdisplayname) - 根據應用程式的顯示名稱定義特定應用程式</span><span class="sxs-lookup"><span data-stu-id="e0711-146">[appDisplayName](#appdisplayname) - defines a specific app based the app's display name</span></span>
* <span data-ttu-id="e0711-147">[loginStatus](#loginStatus) - 定義登入狀態 (成功 / 失敗)</span><span class="sxs-lookup"><span data-stu-id="e0711-147">[loginStatus](#loginStatus) - defines the status of the logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="e0711-148">使用 Graph 總管時，您需要針對篩選欄位中的字母使用正確的大小寫。</span><span class="sxs-lookup"><span data-stu-id="e0711-148">When using Graph Explorer, you the need to use the correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="e0711-149">若要縮小傳回的資料範圍，您可以建立支援的篩選和篩選欄位組合。</span><span class="sxs-lookup"><span data-stu-id="e0711-149">To narrow down the scope of the returned data, you can build combinations of the supported filters and filter fields.</span></span> <span data-ttu-id="e0711-150">例如，下列陳述式會傳回 2016 年 7 月 1 日與2016 年 7 月 6 日之間的前 10 筆記錄︰</span><span class="sxs-lookup"><span data-stu-id="e0711-150">For example, the following statement returns the top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="e0711-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="e0711-151">signinDateTime</span></span>
<span data-ttu-id="e0711-152">**支援的運算子**：eq、ge、le、gt、lt</span><span class="sxs-lookup"><span data-stu-id="e0711-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="e0711-153">**範例**：</span><span class="sxs-lookup"><span data-stu-id="e0711-153">**Example**:</span></span>

<span data-ttu-id="e0711-154">使用特定日期</span><span class="sxs-lookup"><span data-stu-id="e0711-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="e0711-155">使用日期範圍</span><span class="sxs-lookup"><span data-stu-id="e0711-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="e0711-156">**注意**：</span><span class="sxs-lookup"><span data-stu-id="e0711-156">**Notes**:</span></span>

<span data-ttu-id="e0711-157">datetime 參數應採用 UTC 格式</span><span class="sxs-lookup"><span data-stu-id="e0711-157">The datetime parameter should be in the UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="e0711-158">userId</span><span class="sxs-lookup"><span data-stu-id="e0711-158">userId</span></span>
<span data-ttu-id="e0711-159">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="e0711-159">**Supported operators**: eq</span></span>

<span data-ttu-id="e0711-160">**範例**：</span><span class="sxs-lookup"><span data-stu-id="e0711-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="e0711-161">**注意**：</span><span class="sxs-lookup"><span data-stu-id="e0711-161">**Notes**:</span></span>

<span data-ttu-id="e0711-162">userId 的值是字串值</span><span class="sxs-lookup"><span data-stu-id="e0711-162">The value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="e0711-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="e0711-163">userPrincipalName</span></span>
<span data-ttu-id="e0711-164">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="e0711-164">**Supported operators**: eq</span></span>

<span data-ttu-id="e0711-165">**範例**：</span><span class="sxs-lookup"><span data-stu-id="e0711-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="e0711-166">**注意**：</span><span class="sxs-lookup"><span data-stu-id="e0711-166">**Notes**:</span></span>

<span data-ttu-id="e0711-167">userPrincipalName 的值是字串值</span><span class="sxs-lookup"><span data-stu-id="e0711-167">The value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="e0711-168">appId</span><span class="sxs-lookup"><span data-stu-id="e0711-168">appId</span></span>
<span data-ttu-id="e0711-169">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="e0711-169">**Supported operators**: eq</span></span>

<span data-ttu-id="e0711-170">**範例**：</span><span class="sxs-lookup"><span data-stu-id="e0711-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="e0711-171">**注意**：</span><span class="sxs-lookup"><span data-stu-id="e0711-171">**Notes**:</span></span>

<span data-ttu-id="e0711-172">appId 的值是字串值</span><span class="sxs-lookup"><span data-stu-id="e0711-172">The value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="e0711-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="e0711-173">appDisplayName</span></span>
<span data-ttu-id="e0711-174">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="e0711-174">**Supported operators**: eq</span></span>

<span data-ttu-id="e0711-175">**範例**：</span><span class="sxs-lookup"><span data-stu-id="e0711-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="e0711-176">**注意**：</span><span class="sxs-lookup"><span data-stu-id="e0711-176">**Notes**:</span></span>

<span data-ttu-id="e0711-177">appDisplayName 的值是字串值</span><span class="sxs-lookup"><span data-stu-id="e0711-177">The value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="e0711-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="e0711-178">loginStatus</span></span>
<span data-ttu-id="e0711-179">**支援的運算子**：eq</span><span class="sxs-lookup"><span data-stu-id="e0711-179">**Supported operators**: eq</span></span>

<span data-ttu-id="e0711-180">**範例**：</span><span class="sxs-lookup"><span data-stu-id="e0711-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="e0711-181">**注意**：</span><span class="sxs-lookup"><span data-stu-id="e0711-181">**Notes**:</span></span>

<span data-ttu-id="e0711-182">loginStatus 有兩個選項：0 - 成功、1 - 失敗</span><span class="sxs-lookup"><span data-stu-id="e0711-182">There are two options for the loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="e0711-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0711-183">Next steps</span></span>
* <span data-ttu-id="e0711-184">您想要查看篩選過的登入活動範例嗎？</span><span class="sxs-lookup"><span data-stu-id="e0711-184">Do you want to see examples for filtered sign-in activities?</span></span> <span data-ttu-id="e0711-185">請查看 [Azure Active Directory 登入活動報告 API 範例](active-directory-reporting-api-sign-in-activity-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="e0711-185">Check out the [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="e0711-186">您想要深入了解 Azure AD 報告 API 嗎？</span><span class="sxs-lookup"><span data-stu-id="e0711-186">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="e0711-187">請參閱 [開始使用 Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e0711-187">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>


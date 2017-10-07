---
title: "群組為基礎的 Azure AD 授權的範例 aaaPowerShell |Microsoft 文件"
description: "Azure Active Directory 群組型授權的 PowerShell 案例"
services: active-directory
keywords: "Azure AD 授權"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.openlocfilehash: 31eeab0a34c35e80849a4cd11f5447a30b7c04be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-examples-for-group-based-licensing-in-azure-ad"></a><span data-ttu-id="1aa0f-104">Azure AD 群組型授權的 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="1aa0f-104">PowerShell examples for group-based licensing in Azure AD</span></span>

<span data-ttu-id="1aa0f-105">完整功能，以群組為基礎的授權是透過 hello [Azure 入口網站](https://portal.azure.com)，而且目前 PowerShell 支援有限。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-105">Full functionality for group-based licensing is available through hello [Azure portal](https://portal.azure.com), and currently PowerShell support is limited.</span></span> <span data-ttu-id="1aa0f-106">不過，有一些有用的工作，可以使用現有的 hello 執行[MSOnline PowerShell cmdlet](https://docs.microsoft.com/powershell/msonline/v1/azureactivedirectory)。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-106">However, there are some useful tasks that can be performed using hello existing [MSOnline PowerShell cmdlets](https://docs.microsoft.com/powershell/msonline/v1/azureactivedirectory).</span></span> <span data-ttu-id="1aa0f-107">本文件會提供可行功能的範例。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-107">This document provides examples of what is possible.</span></span>

> [!NOTE]
> <span data-ttu-id="1aa0f-108">在開始執行 cmdlet 之前，請確定您 tooyour 租用戶先連線，藉由執行 hello `Connect-MsolService` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-108">Before you begin running cmdlets, make sure you connect tooyour tenant first, by running hello `Connect-MsolService` cmdlet.</span></span>

## <a name="view-product-licenses-assigned-tooa-group"></a><span data-ttu-id="1aa0f-109">檢視產品的授權指派 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="1aa0f-109">View product licenses assigned tooa group</span></span>
<span data-ttu-id="1aa0f-110">[Get-msolgroup](/powershell/module/msonline/get-msolgroup?view=azureadps-1.0)指令程式可以使用的 tooretrieve hello 群組物件並檢查 hello*授權*屬性： 它會列出目前已指派 toohello 群組的所有產品授權。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-110">The [Get-MsolGroup](/powershell/module/msonline/get-msolgroup?view=azureadps-1.0) cmdlet can be used tooretrieve hello group object and check hello *Licenses* property: it lists all product licenses currently assigned toohello group.</span></span>
```
(Get-MsolGroup -ObjectId 99c4216a-56de-42c4-a4ac-e411cd8c7c41).Licenses
| Select SkuPartNumber
```
<span data-ttu-id="1aa0f-111">輸出：</span><span class="sxs-lookup"><span data-stu-id="1aa0f-111">Output:</span></span>
```
SkuPartNumber
-------------
ENTERPRISEPREMIUM
EMSPREMIUM
```

> [!NOTE]
> <span data-ttu-id="1aa0f-112">hello 資料是有限的 tooproduct (SKU) 資訊。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-112">hello data is limited tooproduct (SKU) information.</span></span> <span data-ttu-id="1aa0f-113">不可能 toolist hello 服務計劃在 hello 授權中停用。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-113">It is not possible toolist hello service plans disabled in hello license.</span></span>

## <a name="get-all-groups-with-licenses"></a><span data-ttu-id="1aa0f-114">取得具有授權的所有群組</span><span class="sxs-lookup"><span data-stu-id="1aa0f-114">Get all groups with licenses</span></span>

<span data-ttu-id="1aa0f-115">您可以找到任何授權指派，請執行下列命令的 hello 的所有群組：</span><span class="sxs-lookup"><span data-stu-id="1aa0f-115">You can find all groups with any license assigned by running hello following command:</span></span>
```
Get-MsolGroup | Where {$_.Licenses}
```
<span data-ttu-id="1aa0f-116">您可以顯示更多有關已指派之產品的詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="1aa0f-116">More details can be displayed about what products are assigned:</span></span>
```
Get-MsolGroup | Where {$_.Licenses} | Select `
    ObjectId, `
    DisplayName, `
    @{Name="Licenses";Expression={$_.Licenses | Select -ExpandProperty SkuPartNumber}}
```

<span data-ttu-id="1aa0f-117">輸出：</span><span class="sxs-lookup"><span data-stu-id="1aa0f-117">Output:</span></span>
```
ObjectId                             DisplayName              Licenses
--------                             -----------              --------
7023a314-6148-4d7b-b33f-6c775572879a EMS E5 – Licensed users  EMSPREMIUM
cf41f428-3b45-490b-b69f-a349c8a4c38e PowerBi - Licensed users POWER\_BI\_STANDARD
962f7189-59d9-4a29-983f-556ae56f19a5 O365 E3 - Licensed users ENTERPRISEPACK
c2652d63-9161-439b-b74e-fcd8228a7074 EMSandOffice             {ENTERPRISEPREMIUM,EMSPREMIUM}
```

## <a name="get-statistics-for-groups-with-licenses"></a><span data-ttu-id="1aa0f-118">取得具有授權之群組的統計資料</span><span class="sxs-lookup"><span data-stu-id="1aa0f-118">Get statistics for groups with licenses</span></span>
<span data-ttu-id="1aa0f-119">您可以針對具有授權的群組提出基本統計資料報告。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-119">You can report basic statistics for groups with licenses.</span></span> <span data-ttu-id="1aa0f-120">在 hello 面範例中，我們會列出 hello 總使用者計數，hello 計數具有已指派的 hello 群組和使用者的授權，無法指派 hello 群組 hello 計數授權的使用者。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-120">In hello example below we list hello total user count, hello count of users with licenses already assigned by hello group, and hello count of users for whom licenses could not be assigned by hello group.</span></span>

```
#get all groups with licenses
Get-MsolGroup -All | Where {$_.Licenses}  | Foreach {
    $groupId = $_.ObjectId;
    $groupName = $_.DisplayName;
    $groupLicenses = $_.Licenses | Select -ExpandProperty SkuPartNumber
    $totalCount = 0;
    $licenseAssignedCount = 0;
    $licenseErrorCount = 0;

    Get-MsolGroupMember -All -GroupObjectId $groupId |
    #get full info about each user in hello group
    Get-MsolUser -ObjectId {$_.ObjectId} |
    Foreach {
        $user = $_;
        $totalCount++

        #check if any licenses are assigned via this group
        if($user.Licenses | ? {$_.GroupsAssigningLicense -ieq $groupId })
        {
            $licenseAssignedCount++
        }
        #check if user has any licenses that failed toobe assigned from this group
        if ($user.IndirectLicenseErrors | ? {$_.ReferencedObjectId -ieq $groupId })
        {
            $licenseErrorCount++
        }     
    }

    #aggregate results for this group
    New-Object Object |
                    Add-Member -NotePropertyName GroupName -NotePropertyValue $groupName -PassThru |
                    Add-Member -NotePropertyName GroupId -NotePropertyValue $groupId -PassThru |
                    Add-Member -NotePropertyName GroupLicenses -NotePropertyValue $groupLicenses -PassThru |
                    Add-Member -NotePropertyName TotalUserCount -NotePropertyValue $totalCount -PassThru |
                    Add-Member -NotePropertyName LicensedUserCount -NotePropertyValue $licenseAssignedCount -PassThru |
                    Add-Member -NotePropertyName LicenseErrorCount -NotePropertyValue $licenseErrorCount -PassThru

    } | Format-Table
```


<span data-ttu-id="1aa0f-121">輸出：</span><span class="sxs-lookup"><span data-stu-id="1aa0f-121">Output:</span></span>
```
GroupName         GroupId                              GroupLicenses       TotalUserCount LicensedUserCount LicenseErrorCount
---------         -------                              -------------       -------------- ----------------- -----------------
Dynamics Licen... 9160c903-9f91-4597-8f79-22b6c47eafbf AAD_PREMIUM_P2                   0                 0                 0
O365 E5 - base... 055dcca3-fb75-4398-a1b8-f8c6f4c24e65 ENTERPRISEPREMIUM                2                 2                 0
O365 E5 - extr... 6b14a1fe-c3a9-4786-9ee4-3a2bb54dcb8e ENTERPRISEPREMIUM                3                 3                 0
EMS E5 - all s... 7023a314-6148-4d7b-b33f-6c775572879a EMSPREMIUM                       2                 2                 0
PowerBi - Lice... cf41f428-3b45-490b-b69f-a349c8a4c38e POWER_BI_STANDARD                2                 2                 0
O365 E3 - all ... 962f7189-59d9-4a29-983f-556ae56f19a5 ENTERPRISEPACK                   2                 2                 0
O365 E5 - EXO     102fb8f4-bbe7-462b-83ff-2145e7cdd6ed ENTERPRISEPREMIUM                1                 1                 0
Access tooOffi... 11151866-5419-4d93-9141-0603bbf78b42 STANDARDPACK                     4                 3                 1
```

## <a name="get-all-groups-with-license-errors"></a><span data-ttu-id="1aa0f-122">取得具有授權錯誤的所有群組</span><span class="sxs-lookup"><span data-stu-id="1aa0f-122">Get all groups with license errors</span></span>
<span data-ttu-id="1aa0f-123">包含某些使用者的授權，無法指派 toofind 群組：</span><span class="sxs-lookup"><span data-stu-id="1aa0f-123">toofind groups that contain some users for whom licenses could not be assigned:</span></span>
```
Get-MsolGroup -HasLicenseErrorsOnly $true
```
<span data-ttu-id="1aa0f-124">輸出：</span><span class="sxs-lookup"><span data-stu-id="1aa0f-124">Output:</span></span>
```
ObjectId                             DisplayName             GroupType Description
--------                             -----------             --------- -----------
11151866-5419-4d93-9141-0603bbf78b42 Access tooOffice 365 E1 Security  Users who should have E1 licenses
```
## <a name="get-all-users-with-license-errors-in-a-group"></a><span data-ttu-id="1aa0f-125">取得群組中具有授權錯誤的所有使用者</span><span class="sxs-lookup"><span data-stu-id="1aa0f-125">Get all users with license errors in a group</span></span>

<span data-ttu-id="1aa0f-126">若群組中包含某些授權相關錯誤，您現在可以列出這些錯誤所影響到的使用者。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-126">Given a group that contains some license related errors, you can now list all users affected by those errors.</span></span> <span data-ttu-id="1aa0f-127">Jser 也可能有來自其他群組的錯誤。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-127">A jser can have errors from other groups, too.</span></span> <span data-ttu-id="1aa0f-128">不過，在此範例中我們藉由檢查限制結果只有 tooerrors 相關 toohello 群組**ReferencedObjectId**每個屬性**IndirectLicenseError** hello 使用者上的項目。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-128">However, in this example we limit results only tooerrors relevant toohello group in question by checking the **ReferencedObjectId** property of each **IndirectLicenseError** entry on hello user.</span></span>

```
#a sample group with errors
$groupId = '11151866-5419-4d93-9141-0603bbf78b42'

#get all user members of hello group
Get-MsolGroupMember -All -GroupObjectId $groupId |
    #get full information about user objects
    Get-MsolUser -ObjectId {$_.ObjectId} |
    #filter out users without license errors and users with licenense errors from other groups
    Where {$_.IndirectLicenseErrors -and $_.IndirectLicenseErrors.ReferencedObjectId -eq $groupId} |
    #display id, name and error detail. Note: we are filtering out license errors from other groups
    Select ObjectId, `
           DisplayName, `
           @{Name="LicenseError";Expression={$_.IndirectLicenseErrors | Where {$_.ReferencedObjectId -eq $groupId} | Select -ExpandProperty Error}}
```

<span data-ttu-id="1aa0f-129">輸出：</span><span class="sxs-lookup"><span data-stu-id="1aa0f-129">Output:</span></span>
```
ObjectId                             DisplayName      License Error
--------                             -----------      ------------
6d325baf-22b7-46fa-a2fc-a2500613ca15 Catherine Gibson MutuallyExclusiveViolation
```
## <a name="get-all-users-with-license-errors-in-hello-entire-tenant"></a><span data-ttu-id="1aa0f-130">取得與授權錯誤 hello 整個租用戶中的所有使用者</span><span class="sxs-lookup"><span data-stu-id="1aa0f-130">Get all users with license errors in hello entire tenant</span></span>

<span data-ttu-id="1aa0f-131">toolist 可以用於所有使用者都有一個或多個群組，下列指令碼的 hello 從授權錯誤。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-131">toolist all users who have license errors from one or more groups, hello following script can be used.</span></span> <span data-ttu-id="1aa0f-132">此指令碼會列出一個資料列每個使用者，每個可讓您授權錯誤 tooclearly 識別 hello 來源的每個錯誤。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-132">This script will list one row per user, per license error which allows you tooclearly identify hello source of each error.</span></span>

> [!NOTE]
> <span data-ttu-id="1aa0f-133">此指令碼會列舉 hello 租用戶，但這不是最適合大型的租用戶中的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-133">This script will enumerate all users in hello tenant, which might not be optimal for large tenants.</span></span>

```
Get-MsolUser -All | Where {$_.IndirectLicenseErrors } | % {   
    $user = $_;
    $user.IndirectLicenseErrors | % {
            New-Object Object |
                Add-Member -NotePropertyName UserName -NotePropertyValue $user.DisplayName -PassThru |
                Add-Member -NotePropertyName UserId -NotePropertyValue $user.ObjectId -PassThru |
                Add-Member -NotePropertyName GroupId -NotePropertyValue $_.ReferencedObjectId -PassThru |
                Add-Member -NotePropertyName LicenseError -NotePropertyValue $_.Error -PassThru
        }
    }  
```

<span data-ttu-id="1aa0f-134">輸出：</span><span class="sxs-lookup"><span data-stu-id="1aa0f-134">Output:</span></span>

```
UserName         UserId                               GroupId                              LicenseError
--------         ------                               -------                              ------------
Anna Bergman     0d0fd16d-872d-4e87-b0fb-83c610db12bc 7946137d-b00d-4336-975e-b1b81b0666d0 MutuallyExclusiveViolation
Catherine Gibson 6d325baf-22b7-46fa-a2fc-a2500613ca15 f2503e79-0edc-4253-8bed-3e158366466b CountViolation
Catherine Gibson 6d325baf-22b7-46fa-a2fc-a2500613ca15 11151866-5419-4d93-9141-0603bbf78b42 MutuallyExclusiveViolation
Drew Fogarty     f2af28fc-db0b-4909-873d-ddd2ab1fd58c 1ebd5028-6092-41d0-9668-129a3c471332 MutuallyExclusiveViolation
```

<span data-ttu-id="1aa0f-135">以下是另一個版本只會搜尋包含授權錯誤群組的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-135">Here is another version of hello script that searches only through groups that contain license errors.</span></span> <span data-ttu-id="1aa0f-136">它可能是多個最佳化希望 toohave 案例發生問題的幾個群組。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-136">It may be more optimized for scenarios where you expect toohave few groups with problems.</span></span>

```
Get-MsolUser -All | Where {$_.IndirectLicenseErrors } | % {   
    $user = $_;
    $user.IndirectLicenseErrors | % {
            New-Object Object |
                Add-Member -NotePropertyName UserName -NotePropertyValue $user.DisplayName -PassThru |
                Add-Member -NotePropertyName UserId -NotePropertyValue $user.ObjectId -PassThru |
                Add-Member -NotePropertyName GroupId -NotePropertyValue $_.ReferencedObjectId -PassThru |
                Add-Member -NotePropertyName LicenseError -NotePropertyValue $_.Error -PassThru
        }
    }
```

## <a name="check-if-user-license-is-assigned-directly-or-inherited-from-a-group"></a><span data-ttu-id="1aa0f-137">檢查使用者的授權是透過直接指派還是群組繼承而得到</span><span class="sxs-lookup"><span data-stu-id="1aa0f-137">Check if user license is assigned directly or inherited from a group</span></span>

<span data-ttu-id="1aa0f-138">對使用者物件很可能 toocheck 如果特定產品的授權指派的群組，或直接指派。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-138">For a user object it is possible toocheck if a particular product license is assigned from a group or if it is assigned directly.</span></span>

<span data-ttu-id="1aa0f-139">下列的 hello 兩個範例函式可以在個別的使用者上使用指派 tooanalyze hello 類型：</span><span class="sxs-lookup"><span data-stu-id="1aa0f-139">hello two sample functions below can be used tooanalyze hello type of assignment on an individual user:</span></span>
```
#Returns TRUE if hello user has hello license assigned directly
function UserHasLicenseAssignedDirectly
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)

    foreach($license in $user.Licenses)
    {
        #we look for hello specific license SKU in all licenses assigned toohello user
        if ($license.AccountSkuId -ieq $skuId)
        {
            #GroupsAssigningLicense contains a collection of IDs of objects assigning hello license
            #This could be a group object or a user object (contrary toowhat hello name suggests)
            #If hello collection is empty, this means hello license is assigned directly - this is hello case for users who have never been licensed via groups in hello past
            if ($license.GroupsAssigningLicense.Count -eq 0)
            {
                return $true
            }

            #If hello collection contains hello ID of hello user object, this means hello license is assigned directly
            #Note: hello license may also be assigned through one or more groups in addition toobeing assigned directly
            foreach ($assignmentSource in $license.GroupsAssigningLicense)
            {
                if ($assignmentSource -ieq $user.ObjectId)
                {
                    return $true
                }
            }
            return $false
        }
    }
    return $false
}
#Returns TRUE if hello user is inheriting hello license from a group
function UserHasLicenseAssignedFromGroup
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)

    foreach($license in $user.Licenses)
    {
        #we look for hello specific license SKU in all licenses assigned toohello user
        if ($license.AccountSkuId -ieq $skuId)
        {
            #GroupsAssigningLicense contains a collection of IDs of objects assigning hello license
            #This could be a group object or a user object (contrary toowhat hello name suggests)
            foreach ($assignmentSource in $license.GroupsAssigningLicense)
            {
                #If hello collection contains at least one ID not matching hello user ID this means that hello license is inherited from a group.
                #Note: hello license may also be assigned directly in addition toobeing inherited
                if ($assignmentSource -ine $user.ObjectId)
                {
                    return $true
                }
            }
            return $false
        }
    }
    return $false
}
```

<span data-ttu-id="1aa0f-140">此指令碼會執行這些函式的每一個使用者在 hello 租用戶使用 hello SKU 識別碼做為輸入-在此範例中我們有興趣 hello 授權*Enterprise Mobility + Security*，我們的租用戶中表示識別碼*contoso:EMS*:</span><span class="sxs-lookup"><span data-stu-id="1aa0f-140">This script executes those functions on each user in hello tenant, using hello SKU ID as input - in this example we are interested in hello license for *Enterprise Mobility + Security*, which in our tenant is represented with ID *contoso:EMS*:</span></span>
```
#hello license SKU we are interested in. use Msol-GetAccountSku toosee a list of all identifiers in your tenant
$skuId = "contoso:EMS"

#find all users that have hello SKU license assigned
Get-MsolUser -All | where {$_.isLicensed -eq $true -and $_.Licenses.AccountSKUID -eq $skuId} | select `
    ObjectId, `
    @{Name="SkuId";Expression={$skuId}}, `
    @{Name="AssignedDirectly";Expression={(UserHasLicenseAssignedDirectly $_ $skuId)}}, `
    @{Name="AssignedFromGroup";Expression={(UserHasLicenseAssignedFromGroup $_ $skuId)}}
```

<span data-ttu-id="1aa0f-141">輸出：</span><span class="sxs-lookup"><span data-stu-id="1aa0f-141">Output:</span></span>
```
ObjectId                             SkuId       AssignedDirectly AssignedFromGroup
--------                             -----       ---------------- -----------------
157870f6-e050-4b3c-ad5e-0f0a377c8f4d contoso:EMS             True             False
1f3174e2-ee9d-49e9-b917-e8d84650f895 contoso:EMS            False              True
240622ac-b9b8-4d50-94e2-dad19a3bf4b5 contoso:EMS             True              True
```

## <a name="remove-direct-licenses-for-users-with-group-licenses"></a><span data-ttu-id="1aa0f-142">移除具有群組授權之使用者的直接授權</span><span class="sxs-lookup"><span data-stu-id="1aa0f-142">Remove direct licenses for users with group licenses</span></span>
<span data-ttu-id="1aa0f-143">此指令碼的 hello 用途是 tooremove 不需要直接授權已繼承群組; 中的 hello 相同授權的使用者例如，做為一部分[轉換 toogroup 授權](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-group-migration-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-143">hello purpose of this script is tooremove unnecessary direct licenses from users who already inherit hello same license from a group; for example, as part of a [transitioning toogroup-based licensing](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-group-migration-azure-portal).</span></span>
> [!NOTE]
> <span data-ttu-id="1aa0f-144">請務必 toofirst 驗證該 hello 直接授權 toobe 移除不要啟用比 hello 繼承授權的服務功能。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-144">It is important toofirst validate that hello direct licenses toobe removed do not enable more service functionality than hello inherited licenses.</span></span> <span data-ttu-id="1aa0f-145">否則，請移除 hello 直接授權可能會停用存取 tooservices 和使用者的資料。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-145">Otherwise, removing hello direct license may disable access tooservices and data for users.</span></span> <span data-ttu-id="1aa0f-146">目前不是透過 PowerShell 哪些服務透過直接繼承的授權與啟用的可能 toocheck。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-146">Currently it is not possible toocheck via PowerShell which services are enabled via inherited licenses vs direct.</span></span> <span data-ttu-id="1aa0f-147">我們將 hello 指令碼中指定 hello 最低層級的服務，因此我們會知道會正在繼承自群組，這樣的情況，我們會檢查。</span><span class="sxs-lookup"><span data-stu-id="1aa0f-147">In hello script we will specify hello minimum level of services we know are being inherited from groups and we will check against that.</span></span>

```
#BEGIN: Helper functions used by hello script

#Returns TRUE if hello user has hello license assigned directly
function UserHasLicenseAssignedDirectly
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)

    $license = GetUserLicense $user $skuId

    if ($license -ne $null)
    {
        #GroupsAssigningLicense contains a collection of IDs of objects assigning hello license
        #This could be a group object or a user object (contrary toowhat hello name suggests)
        #If hello collection is empty, this means hello license is assigned directly - this is hello case for users who have never been licensed via groups in hello past
        if ($license.GroupsAssigningLicense.Count -eq 0)
        {
            return $true
        }

        #If hello collection contains hello ID of hello user object, this means hello license is assigned directly
        #Note: hello license may also be assigned through one or more groups in addition toobeing assigned directly
        foreach ($assignmentSource in $license.GroupsAssigningLicense)
        {
            if ($assignmentSource -ieq $user.ObjectId)
            {
                return $true
            }
        }
        return $false
    }
    return $false
}
#Returns TRUE if hello user is inheriting hello license from a specific group
function UserHasLicenseAssignedFromThisGroup
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId, [Guid]$groupId)

    $license = GetUserLicense $user $skuId

    if ($license -ne $null)
    {
        #GroupsAssigningLicense contains a collection of IDs of objects assigning hello license
        #This could be a group object or a user object (contrary toowhat hello name suggests)
        foreach ($assignmentSource in $license.GroupsAssigningLicense)
        {
            #If hello collection contains at least one ID not matching hello user ID this means that hello license is inherited from a group.
            #Note: hello license may also be assigned directly in addition toobeing inherited
            if ($assignmentSource -ieq $groupId)
            {
                return $true
            }
        }
        return $false
    }
    return $false
}

#Returns hello license object corresponding toohello skuId. Returns NULL if not found
function GetUserLicense
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId, [Guid]$groupId)
    #we look for hello specific license SKU in all licenses assigned toohello user
    foreach($license in $user.Licenses)
    {
        if ($license.AccountSkuId -ieq $skuId)
        {
            return $license
        }
    }
    return $null
}

#produces a list of disabled service plan names for a set of plans we want tooleave enabled
function GetDisabledPlansForSKU
{
    Param([string]$skuId, [string[]]$enabledPlans)

    $allPlans = Get-MsolAccountSku | where {$_.AccountSkuId -ieq $skuId} | Select -ExpandProperty ServiceStatus | Where {$_.ProvisioningStatus -ieq "PendingActivation"} | Select -ExpandProperty ServicePlan | Select -ExpandProperty ServiceName
    $disabledPlans = $allPlans | Where {$enabledPlans -inotcontains $_}

    return $disabledPlans
}

function GetUnexpectedEnabledPlansForUser
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId, [string[]]$expectedDisabledPlans)

    $license = GetUserLicense $user $skuId

    $extraPlans = @();

    if($license -ne $null)
    {
        $userDisabledPlans = $license.ServiceStatus | where {$_.ProvisioningStatus -ieq "Disabled"} | Select -ExpandProperty ServicePlan | Select -ExpandProperty ServiceName

        $extraPlans = $expectedDisabledPlans | where {$userDisabledPlans -notcontains $_}
    }
    return $extraPlans
}
#END: helper functions

#BEGIN: executing hello script
#hello group toobe processed
$groupId = "48ca647b-7e4d-41e5-aa66-40cab1e19101"

#license toobe removed - Office 365 E3
$skuId = "contoso:ENTERPRISEPACK"

#minimum set of service plans we know are inherited from groups - we want toomake sure that there aren't any users who have more services enabled
#which could mean that they may lose access after we remove direct licenses
$servicePlansFromGroups = ("EXCHANGE_S_ENTERPRISE", "SHAREPOINTENTERPRISE", "OFFICESUBSCRIPTION")

$expectedDisabledPlans = GetDisabledPlansForSKU $skuId $servicePlansFromGroups

#process all members in hello group
Get-MsolGroupMember -All -GroupObjectId $groupId |
    #get full info about each user in hello group
    Get-MsolUser -ObjectId {$_.ObjectId} |
    Foreach {
        $user = $_;
        $operationResult = "";

        #check if Direct license exists on hello user
        if (UserHasLicenseAssignedDirectly $user $skuId)
        {
            #check if hello license is assigned from this group, as expected
            if (UserHasLicenseAssignedFromThisGroup $user $skuId $groupId)
            {
                #check if there are any extra plans we didn't expect - we are being extra careful not tooremove unexpected services
                $extraPlans = GetUnexpectedEnabledPlansForUser $user $skuId $expectedDisabledPlans
                if ($extraPlans.Count -gt 0)
                {
                    $operationResult = "User has extra plans that may be lost - license removal was skipped. Extra plans: $extraPlans"
                }
                else
                {
                    #remove hello direct license from user
                    Set-MsolUserLicense -ObjectId $user.ObjectId -RemoveLicenses $skuId
                    $operationResult = "Removed direct license from user."   
                }

            }
            else
            {
                $operationResult = "User does not inherit this license from this group. License removal was skipped."
            }
        }
        else
        {
            $operationResult = "User has no direct license tooremove. Skipping."
        }

        #format output
        New-Object Object |
                    Add-Member -NotePropertyName UserId -NotePropertyValue $user.ObjectId -PassThru |
                    Add-Member -NotePropertyName OperationResult -NotePropertyValue $operationResult -PassThru
    } | Format-Table
#END: executing hello script
```

<span data-ttu-id="1aa0f-148">輸出：</span><span class="sxs-lookup"><span data-stu-id="1aa0f-148">Output:</span></span>
```
UserId                               OperationResult                                                                                
------                               ---------------                                                                                
7c7f860f-700a-462a-826c-f50633931362 Removed direct license from user.                                                              
0ddacdd5-0364-477d-9e4b-07eb6cdbc8ea User has extra plans that may be lost - license removal was skipped. Extra plans: SHAREPOINTWAC
aadbe4da-c4b5-4d84-800a-9400f31d7371 User has no direct license tooremove. Skipping.                                                
```

## <a name="next-steps"></a><span data-ttu-id="1aa0f-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1aa0f-149">Next steps</span></span>

<span data-ttu-id="1aa0f-150">toolearn hello 功能有關的詳細資訊設定的授權管理透過群組，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="1aa0f-150">toolearn more about hello feature set for license management through groups, see hello following:</span></span>

* [<span data-ttu-id="1aa0f-151">什麼是 Azure Active Directory 中以群組為基礎的授權？</span><span class="sxs-lookup"><span data-stu-id="1aa0f-151">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="1aa0f-152">Azure Active Directory 中指派的授權 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="1aa0f-152">Assigning licenses tooa group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="1aa0f-153">識別及解決 Azure Active Directory 中群組的授權問題</span><span class="sxs-lookup"><span data-stu-id="1aa0f-153">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="1aa0f-154">如何 toomigrate 個別授權 toogroup 型授權 Azure Active Directory 中的使用者</span><span class="sxs-lookup"><span data-stu-id="1aa0f-154">How toomigrate individual licensed users toogroup-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="1aa0f-155">Azure Active Directory 群組型授權其他案例 (英文)</span><span class="sxs-lookup"><span data-stu-id="1aa0f-155">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)

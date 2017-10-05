---
title: "Azure AD 群組型授權的 PowerShell 範例 | Microsoft Docs"
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
ms.openlocfilehash: b561dd29faff63d4898f351b2c9a39d359b89539
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="powershell-examples-for-group-based-licensing-in-azure-ad"></a><span data-ttu-id="3d3e6-104">Azure AD 群組型授權的 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="3d3e6-104">PowerShell examples for group-based licensing in Azure AD</span></span>

<span data-ttu-id="3d3e6-105">透過 [Azure 入口網站](https://portal.azure.com)即可使用群組型授權的完整功能，在這方面 PowerShell 目前只能提供有限的支援。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-105">Full functionality for group-based licensing is available through the [Azure portal](https://portal.azure.com), and currently PowerShell support is limited.</span></span> <span data-ttu-id="3d3e6-106">不過，還是有一些工作可以使用現有的 [MSOnline PowerShell Cmdlet](https://docs.microsoft.com/powershell/msonline/v1/azureactivedirectory) 來執行。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-106">However, there are some useful tasks that can be performed using the existing [MSOnline PowerShell cmdlets](https://docs.microsoft.com/powershell/msonline/v1/azureactivedirectory).</span></span> <span data-ttu-id="3d3e6-107">本文件會提供可行功能的範例。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-107">This document provides examples of what is possible.</span></span>

> [!NOTE]
> <span data-ttu-id="3d3e6-108">在開始執行這些 Cmdlet 之前，請先確定您已藉由執行 `Connect-MsolService` Cmdlet 來連線到租用戶。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-108">Before you begin running cmdlets, make sure you connect to your tenant first, by running the `Connect-MsolService` cmdlet.</span></span>

## <a name="view-product-licenses-assigned-to-a-group"></a><span data-ttu-id="3d3e6-109">檢視指派給群組的產品授權</span><span class="sxs-lookup"><span data-stu-id="3d3e6-109">View product licenses assigned to a group</span></span>
<span data-ttu-id="3d3e6-110">[Get-MsolGroup](/powershell/module/msonline/get-msolgroup?view=azureadps-1.0) Cmdlet 可用來擷取群組物件並檢查「授權」屬性︰它會列出目前指派給群組的所有產品授權。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-110">The [Get-MsolGroup](/powershell/module/msonline/get-msolgroup?view=azureadps-1.0) cmdlet can be used to retrieve the group object and check the *Licenses* property: it lists all product licenses currently assigned to the group.</span></span>
```
(Get-MsolGroup -ObjectId 99c4216a-56de-42c4-a4ac-e411cd8c7c41).Licenses
| Select SkuPartNumber
```
<span data-ttu-id="3d3e6-111">輸出：</span><span class="sxs-lookup"><span data-stu-id="3d3e6-111">Output:</span></span>
```
SkuPartNumber
-------------
ENTERPRISEPREMIUM
EMSPREMIUM
```

> [!NOTE]
> <span data-ttu-id="3d3e6-112">此資料只會列出產品 (SKU) 資訊。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-112">The data is limited to product (SKU) information.</span></span> <span data-ttu-id="3d3e6-113">您無法列出授權中已停用的服務方案。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-113">It is not possible to list the service plans disabled in the license.</span></span>

## <a name="get-all-groups-with-licenses"></a><span data-ttu-id="3d3e6-114">取得具有授權的所有群組</span><span class="sxs-lookup"><span data-stu-id="3d3e6-114">Get all groups with licenses</span></span>

<span data-ttu-id="3d3e6-115">您可以執行下列命令來尋找所有已獲得授權的群組︰</span><span class="sxs-lookup"><span data-stu-id="3d3e6-115">You can find all groups with any license assigned by running the following command:</span></span>
```
Get-MsolGroup | Where {$_.Licenses}
```
<span data-ttu-id="3d3e6-116">您可以顯示更多有關已指派之產品的詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="3d3e6-116">More details can be displayed about what products are assigned:</span></span>
```
Get-MsolGroup | Where {$_.Licenses} | Select `
    ObjectId, `
    DisplayName, `
    @{Name="Licenses";Expression={$_.Licenses | Select -ExpandProperty SkuPartNumber}}
```

<span data-ttu-id="3d3e6-117">輸出：</span><span class="sxs-lookup"><span data-stu-id="3d3e6-117">Output:</span></span>
```
ObjectId                             DisplayName              Licenses
--------                             -----------              --------
7023a314-6148-4d7b-b33f-6c775572879a EMS E5 – Licensed users  EMSPREMIUM
cf41f428-3b45-490b-b69f-a349c8a4c38e PowerBi - Licensed users POWER\_BI\_STANDARD
962f7189-59d9-4a29-983f-556ae56f19a5 O365 E3 - Licensed users ENTERPRISEPACK
c2652d63-9161-439b-b74e-fcd8228a7074 EMSandOffice             {ENTERPRISEPREMIUM,EMSPREMIUM}
```

## <a name="get-statistics-for-groups-with-licenses"></a><span data-ttu-id="3d3e6-118">取得具有授權之群組的統計資料</span><span class="sxs-lookup"><span data-stu-id="3d3e6-118">Get statistics for groups with licenses</span></span>
<span data-ttu-id="3d3e6-119">您可以針對具有授權的群組提出基本統計資料報告。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-119">You can report basic statistics for groups with licenses.</span></span> <span data-ttu-id="3d3e6-120">下列範例列出了使用者總人數、群組已對其指派授權的使用者人數，以及群組無法對其指派授權的使用者人數。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-120">In the example below we list the total user count, the count of users with licenses already assigned by the group, and the count of users for whom licenses could not be assigned by the group.</span></span>

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
    #get full info about each user in the group
    Get-MsolUser -ObjectId {$_.ObjectId} |
    Foreach {
        $user = $_;
        $totalCount++

        #check if any licenses are assigned via this group
        if($user.Licenses | ? {$_.GroupsAssigningLicense -ieq $groupId })
        {
            $licenseAssignedCount++
        }
        #check if user has any licenses that failed to be assigned from this group
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


<span data-ttu-id="3d3e6-121">輸出：</span><span class="sxs-lookup"><span data-stu-id="3d3e6-121">Output:</span></span>
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
Access to Offi... 11151866-5419-4d93-9141-0603bbf78b42 STANDARDPACK                     4                 3                 1
```

## <a name="get-all-groups-with-license-errors"></a><span data-ttu-id="3d3e6-122">取得具有授權錯誤的所有群組</span><span class="sxs-lookup"><span data-stu-id="3d3e6-122">Get all groups with license errors</span></span>
<span data-ttu-id="3d3e6-123">若要尋找其所包含的使用者無法獲得授權指派的群組︰</span><span class="sxs-lookup"><span data-stu-id="3d3e6-123">To find groups that contain some users for whom licenses could not be assigned:</span></span>
```
Get-MsolGroup -HasLicenseErrorsOnly $true
```
<span data-ttu-id="3d3e6-124">輸出：</span><span class="sxs-lookup"><span data-stu-id="3d3e6-124">Output:</span></span>
```
ObjectId                             DisplayName             GroupType Description
--------                             -----------             --------- -----------
11151866-5419-4d93-9141-0603bbf78b42 Access to Office 365 E1 Security  Users who should have E1 licenses
```
## <a name="get-all-users-with-license-errors-in-a-group"></a><span data-ttu-id="3d3e6-125">取得群組中具有授權錯誤的所有使用者</span><span class="sxs-lookup"><span data-stu-id="3d3e6-125">Get all users with license errors in a group</span></span>

<span data-ttu-id="3d3e6-126">若群組中包含某些授權相關錯誤，您現在可以列出這些錯誤所影響到的使用者。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-126">Given a group that contains some license related errors, you can now list all users affected by those errors.</span></span> <span data-ttu-id="3d3e6-127">Jser 也可能有來自其他群組的錯誤。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-127">A jser can have errors from other groups, too.</span></span> <span data-ttu-id="3d3e6-128">不過，此範例所列出的結果僅限於與有問題之群組有關的錯誤，其方法是對使用者每個 **IndirectLicenseError** 項目的 **ReferencedObjectId** 屬性進行檢查。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-128">However, in this example we limit results only to errors relevant to the group in question by checking the **ReferencedObjectId** property of each **IndirectLicenseError** entry on the user.</span></span>

```
#a sample group with errors
$groupId = '11151866-5419-4d93-9141-0603bbf78b42'

#get all user members of the group
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

<span data-ttu-id="3d3e6-129">輸出：</span><span class="sxs-lookup"><span data-stu-id="3d3e6-129">Output:</span></span>
```
ObjectId                             DisplayName      License Error
--------                             -----------      ------------
6d325baf-22b7-46fa-a2fc-a2500613ca15 Catherine Gibson MutuallyExclusiveViolation
```
## <a name="get-all-users-with-license-errors-in-the-entire-tenant"></a><span data-ttu-id="3d3e6-130">取得整個租用戶中具有授權錯誤的所有使用者</span><span class="sxs-lookup"><span data-stu-id="3d3e6-130">Get all users with license errors in the entire tenant</span></span>

<span data-ttu-id="3d3e6-131">若要列出具有一或多個群組之授權錯誤的所有使用者，您可以使用下列指令碼。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-131">To list all users who have license errors from one or more groups, the following script can be used.</span></span> <span data-ttu-id="3d3e6-132">此指令碼會將每位使用者的每個授權錯誤各列在一個資料列中，以方便您清楚識別每個錯誤的來源。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-132">This script will list one row per user, per license error which allows you to clearly identify the source of each error.</span></span>

> [!NOTE]
> <span data-ttu-id="3d3e6-133">此指令碼會列舉租用戶中的所有使用者，因此可能不適合大型租用戶使用。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-133">This script will enumerate all users in the tenant, which might not be optimal for large tenants.</span></span>

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

<span data-ttu-id="3d3e6-134">輸出：</span><span class="sxs-lookup"><span data-stu-id="3d3e6-134">Output:</span></span>

```
UserName         UserId                               GroupId                              LicenseError
--------         ------                               -------                              ------------
Anna Bergman     0d0fd16d-872d-4e87-b0fb-83c610db12bc 7946137d-b00d-4336-975e-b1b81b0666d0 MutuallyExclusiveViolation
Catherine Gibson 6d325baf-22b7-46fa-a2fc-a2500613ca15 f2503e79-0edc-4253-8bed-3e158366466b CountViolation
Catherine Gibson 6d325baf-22b7-46fa-a2fc-a2500613ca15 11151866-5419-4d93-9141-0603bbf78b42 MutuallyExclusiveViolation
Drew Fogarty     f2af28fc-db0b-4909-873d-ddd2ab1fd58c 1ebd5028-6092-41d0-9668-129a3c471332 MutuallyExclusiveViolation
```

<span data-ttu-id="3d3e6-135">以下是另一個版本的指令碼，它只會針對包含授權錯誤的群組進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-135">Here is another version of the script that searches only through groups that contain license errors.</span></span> <span data-ttu-id="3d3e6-136">這個指令碼可能更適合用於預期不會有多少群組有問題的情況。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-136">It may be more optimized for scenarios where you expect to have few groups with problems.</span></span>

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

## <a name="check-if-user-license-is-assigned-directly-or-inherited-from-a-group"></a><span data-ttu-id="3d3e6-137">檢查使用者的授權是透過直接指派還是群組繼承而得到</span><span class="sxs-lookup"><span data-stu-id="3d3e6-137">Check if user license is assigned directly or inherited from a group</span></span>

<span data-ttu-id="3d3e6-138">對於使用者物件，您可以檢查特定產品授權是群組所指派還是直接指派的。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-138">For a user object it is possible to check if a particular product license is assigned from a group or if it is assigned directly.</span></span>

<span data-ttu-id="3d3e6-139">下列兩個函式範例可用來分析個別使用者的指派類型︰</span><span class="sxs-lookup"><span data-stu-id="3d3e6-139">The two sample functions below can be used to analyze the type of assignment on an individual user:</span></span>
```
#Returns TRUE if the user has the license assigned directly
function UserHasLicenseAssignedDirectly
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)

    foreach($license in $user.Licenses)
    {
        #we look for the specific license SKU in all licenses assigned to the user
        if ($license.AccountSkuId -ieq $skuId)
        {
            #GroupsAssigningLicense contains a collection of IDs of objects assigning the license
            #This could be a group object or a user object (contrary to what the name suggests)
            #If the collection is empty, this means the license is assigned directly - this is the case for users who have never been licensed via groups in the past
            if ($license.GroupsAssigningLicense.Count -eq 0)
            {
                return $true
            }

            #If the collection contains the ID of the user object, this means the license is assigned directly
            #Note: the license may also be assigned through one or more groups in addition to being assigned directly
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
#Returns TRUE if the user is inheriting the license from a group
function UserHasLicenseAssignedFromGroup
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)

    foreach($license in $user.Licenses)
    {
        #we look for the specific license SKU in all licenses assigned to the user
        if ($license.AccountSkuId -ieq $skuId)
        {
            #GroupsAssigningLicense contains a collection of IDs of objects assigning the license
            #This could be a group object or a user object (contrary to what the name suggests)
            foreach ($assignmentSource in $license.GroupsAssigningLicense)
            {
                #If the collection contains at least one ID not matching the user ID this means that the license is inherited from a group.
                #Note: the license may also be assigned directly in addition to being inherited
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

<span data-ttu-id="3d3e6-140">此指令碼會對租用戶中的每位使用者執行這些函式，使用 SKU 識別碼作為輸入 - 在此範例中我們感興趣的是 Enterprise Mobility + Security 的授權，它在我們的租用戶中是以識別碼 contoso:EMS 表示：</span><span class="sxs-lookup"><span data-stu-id="3d3e6-140">This script executes those functions on each user in the tenant, using the SKU ID as input - in this example we are interested in the license for *Enterprise Mobility + Security*, which in our tenant is represented with ID *contoso:EMS*:</span></span>
```
#the license SKU we are interested in. use Msol-GetAccountSku to see a list of all identifiers in your tenant
$skuId = "contoso:EMS"

#find all users that have the SKU license assigned
Get-MsolUser -All | where {$_.isLicensed -eq $true -and $_.Licenses.AccountSKUID -eq $skuId} | select `
    ObjectId, `
    @{Name="SkuId";Expression={$skuId}}, `
    @{Name="AssignedDirectly";Expression={(UserHasLicenseAssignedDirectly $_ $skuId)}}, `
    @{Name="AssignedFromGroup";Expression={(UserHasLicenseAssignedFromGroup $_ $skuId)}}
```

<span data-ttu-id="3d3e6-141">輸出：</span><span class="sxs-lookup"><span data-stu-id="3d3e6-141">Output:</span></span>
```
ObjectId                             SkuId       AssignedDirectly AssignedFromGroup
--------                             -----       ---------------- -----------------
157870f6-e050-4b3c-ad5e-0f0a377c8f4d contoso:EMS             True             False
1f3174e2-ee9d-49e9-b917-e8d84650f895 contoso:EMS            False              True
240622ac-b9b8-4d50-94e2-dad19a3bf4b5 contoso:EMS             True              True
```

## <a name="remove-direct-licenses-for-users-with-group-licenses"></a><span data-ttu-id="3d3e6-142">移除具有群組授權之使用者的直接授權</span><span class="sxs-lookup"><span data-stu-id="3d3e6-142">Remove direct licenses for users with group licenses</span></span>
<span data-ttu-id="3d3e6-143">此指令碼的目的，是要為已從群組繼承了相同授權的使用者，移除不必要的直接授權；例如，在[轉換為群組型授權](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-group-migration-azure-portal)的過程中進行此操作。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-143">The purpose of this script is to remove unnecessary direct licenses from users who already inherit the same license from a group; for example, as part of a [transitioning to group-based licensing](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-group-migration-azure-portal).</span></span>
> [!NOTE]
> <span data-ttu-id="3d3e6-144">請務必先驗證，要移除的直接授權所啟用的服務功能，沒有比繼承的授權所啟用的功能多。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-144">It is important to first validate that the direct licenses to be removed do not enable more service functionality than the inherited licenses.</span></span> <span data-ttu-id="3d3e6-145">否則，移除直接授權可能會停用使用者對服務和資料的存取權。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-145">Otherwise, removing the direct license may disable access to services and data for users.</span></span> <span data-ttu-id="3d3e6-146">目前無法透過 PowerShell 來檢查哪些服務是透過繼承授權來啟用，哪些則是透過直接授權來啟用。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-146">Currently it is not possible to check via PowerShell which services are enabled via inherited licenses vs direct.</span></span> <span data-ttu-id="3d3e6-147">在指令碼中，我們會指定已知從群組所繼承而來的最低層級服務，然後就此進行檢查。</span><span class="sxs-lookup"><span data-stu-id="3d3e6-147">In the script we will specify the minimum level of services we know are being inherited from groups and we will check against that.</span></span>

```
#BEGIN: Helper functions used by the script

#Returns TRUE if the user has the license assigned directly
function UserHasLicenseAssignedDirectly
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)

    $license = GetUserLicense $user $skuId

    if ($license -ne $null)
    {
        #GroupsAssigningLicense contains a collection of IDs of objects assigning the license
        #This could be a group object or a user object (contrary to what the name suggests)
        #If the collection is empty, this means the license is assigned directly - this is the case for users who have never been licensed via groups in the past
        if ($license.GroupsAssigningLicense.Count -eq 0)
        {
            return $true
        }

        #If the collection contains the ID of the user object, this means the license is assigned directly
        #Note: the license may also be assigned through one or more groups in addition to being assigned directly
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
#Returns TRUE if the user is inheriting the license from a specific group
function UserHasLicenseAssignedFromThisGroup
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId, [Guid]$groupId)

    $license = GetUserLicense $user $skuId

    if ($license -ne $null)
    {
        #GroupsAssigningLicense contains a collection of IDs of objects assigning the license
        #This could be a group object or a user object (contrary to what the name suggests)
        foreach ($assignmentSource in $license.GroupsAssigningLicense)
        {
            #If the collection contains at least one ID not matching the user ID this means that the license is inherited from a group.
            #Note: the license may also be assigned directly in addition to being inherited
            if ($assignmentSource -ieq $groupId)
            {
                return $true
            }
        }
        return $false
    }
    return $false
}

#Returns the license object corresponding to the skuId. Returns NULL if not found
function GetUserLicense
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId, [Guid]$groupId)
    #we look for the specific license SKU in all licenses assigned to the user
    foreach($license in $user.Licenses)
    {
        if ($license.AccountSkuId -ieq $skuId)
        {
            return $license
        }
    }
    return $null
}

#produces a list of disabled service plan names for a set of plans we want to leave enabled
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

#BEGIN: executing the script
#the group to be processed
$groupId = "48ca647b-7e4d-41e5-aa66-40cab1e19101"

#license to be removed - Office 365 E3
$skuId = "contoso:ENTERPRISEPACK"

#minimum set of service plans we know are inherited from groups - we want to make sure that there aren't any users who have more services enabled
#which could mean that they may lose access after we remove direct licenses
$servicePlansFromGroups = ("EXCHANGE_S_ENTERPRISE", "SHAREPOINTENTERPRISE", "OFFICESUBSCRIPTION")

$expectedDisabledPlans = GetDisabledPlansForSKU $skuId $servicePlansFromGroups

#process all members in the group
Get-MsolGroupMember -All -GroupObjectId $groupId |
    #get full info about each user in the group
    Get-MsolUser -ObjectId {$_.ObjectId} |
    Foreach {
        $user = $_;
        $operationResult = "";

        #check if Direct license exists on the user
        if (UserHasLicenseAssignedDirectly $user $skuId)
        {
            #check if the license is assigned from this group, as expected
            if (UserHasLicenseAssignedFromThisGroup $user $skuId $groupId)
            {
                #check if there are any extra plans we didn't expect - we are being extra careful not to remove unexpected services
                $extraPlans = GetUnexpectedEnabledPlansForUser $user $skuId $expectedDisabledPlans
                if ($extraPlans.Count -gt 0)
                {
                    $operationResult = "User has extra plans that may be lost - license removal was skipped. Extra plans: $extraPlans"
                }
                else
                {
                    #remove the direct license from user
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
            $operationResult = "User has no direct license to remove. Skipping."
        }

        #format output
        New-Object Object |
                    Add-Member -NotePropertyName UserId -NotePropertyValue $user.ObjectId -PassThru |
                    Add-Member -NotePropertyName OperationResult -NotePropertyValue $operationResult -PassThru
    } | Format-Table
#END: executing the script
```

<span data-ttu-id="3d3e6-148">輸出：</span><span class="sxs-lookup"><span data-stu-id="3d3e6-148">Output:</span></span>
```
UserId                               OperationResult                                                                                
------                               ---------------                                                                                
7c7f860f-700a-462a-826c-f50633931362 Removed direct license from user.                                                              
0ddacdd5-0364-477d-9e4b-07eb6cdbc8ea User has extra plans that may be lost - license removal was skipped. Extra plans: SHAREPOINTWAC
aadbe4da-c4b5-4d84-800a-9400f31d7371 User has no direct license to remove. Skipping.                                                
```

## <a name="next-steps"></a><span data-ttu-id="3d3e6-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d3e6-149">Next steps</span></span>

<span data-ttu-id="3d3e6-150">若要深入了解透過群組管理授權的功能集，請參閱下列各項：</span><span class="sxs-lookup"><span data-stu-id="3d3e6-150">To learn more about the feature set for license management through groups, see the following:</span></span>

* [<span data-ttu-id="3d3e6-151">什麼是 Azure Active Directory 中以群組為基礎的授權？</span><span class="sxs-lookup"><span data-stu-id="3d3e6-151">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="3d3e6-152">將授權指派給 Azure Active Directory 中的群組</span><span class="sxs-lookup"><span data-stu-id="3d3e6-152">Assigning licenses to a group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="3d3e6-153">識別及解決 Azure Active Directory 中群組的授權問題</span><span class="sxs-lookup"><span data-stu-id="3d3e6-153">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="3d3e6-154">如何將個別的已授權使用者移轉成 Azure Active Directory 中的群組型授權 (英文)</span><span class="sxs-lookup"><span data-stu-id="3d3e6-154">How to migrate individual licensed users to group-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="3d3e6-155">Azure Active Directory 群組型授權其他案例 (英文)</span><span class="sxs-lookup"><span data-stu-id="3d3e6-155">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)

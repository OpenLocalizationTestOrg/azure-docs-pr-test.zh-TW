---
title: "在 Azure Active Directory 中管理群組的 PowerShell 範例 | Microsoft Docs"
description: "此頁面會提供 PowerShell 範例以協助您管理 Azure Active Directory 中的群組"
keywords: "Azure AD, Azure Active Directory, PowerShell, 群組, 群組管理"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7a5023dc-2727-4c25-8254-b531fc3244ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: a81820bc778c26f6e8051e2817ebd2b9c24b697a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="a3b4b-104">適用於群組管理的 Azure Active Directory 第 2 版 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="a3b4b-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a3b4b-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a3b4b-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="a3b4b-106">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="a3b4b-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="a3b4b-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3b4b-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="a3b4b-108">本文包含的範例，會說明如何使用 PowerShell 管理 Azure Active Directory (Azure AD) 中的群組。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-108">This article contains examples of how to use PowerShell to manage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="a3b4b-109">其中也會說明如何使用 Azure AD PowerShell 模組來完成設定。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-109">It also tells you how to get set up with the Azure AD PowerShell module.</span></span> <span data-ttu-id="a3b4b-110">首先，您必須 [下載 Azure AD PowerShell 模組](https://www.powershellgallery.com/packages/AzureAD/)。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-110">First, you must [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-the-azure-ad-powershell-module"></a><span data-ttu-id="a3b4b-111">安裝 Azure AD PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="a3b4b-111">Installing the Azure AD PowerShell module</span></span>
<span data-ttu-id="a3b4b-112">若要安裝 AzureAD PowerShell 模組，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-112">To install the Azure AD PowerShell module, use the following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="a3b4b-113">若要確認已安裝此模組，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-113">To verify that the module was installed, use the following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="a3b4b-114">現在您可以開始在模組中使用 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-114">Now you can start using the cmdlets in the module.</span></span> <span data-ttu-id="a3b4b-115">如需有關 Azure AD 模組中各式 Cmdlet 的完整描述，請參閱 [Azure Active Directory PowerShell 第 2 版](/powershell/azure/install-adv2?view=azureadps-2.0)的線上參考文件。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-115">For a full description of the cmdlets in the Azure AD module, please refer to the online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-to-the-directory"></a><span data-ttu-id="a3b4b-116">連線到目錄</span><span class="sxs-lookup"><span data-stu-id="a3b4b-116">Connecting to the directory</span></span>
<span data-ttu-id="a3b4b-117">使用 Azure AD PowerShell Cmdlet 開始管理群組之前，您必須先將 PowerShell 工作階段連線至想要管理的目錄。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session to the directory you want to manage.</span></span> <span data-ttu-id="a3b4b-118">使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="a3b4b-118">Use the following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="a3b4b-119">Cmdlet 會提示您輸入需要用來存取目錄的認證。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-119">The cmdlet prompts you for the credentials you want to use to access your directory.</span></span> <span data-ttu-id="a3b4b-120">在此範例中，我們會使用 karen@drumkit.onmicrosoft.com 存取示範目錄。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-120">In this example, we are using karen@drumkit.onmicrosoft.com to access the demonstration directory.</span></span> <span data-ttu-id="a3b4b-121">Cmdlet 將會傳回確認，表示工作階段已成功連線到目錄︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-121">The cmdlet returns a confirmation to show the session was connected successfully to your directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="a3b4b-122">現在您可以開始使用 AzureAD Cmdlet 來管理您目錄中的群組。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-122">Now you can start using the AzureAD cmdlets to manage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="a3b4b-123">擷取群組</span><span class="sxs-lookup"><span data-stu-id="a3b4b-123">Retrieving groups</span></span>
<span data-ttu-id="a3b4b-124">若要從目錄中擷取現有的群組，您可以使用 Get-AzureADGroups Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-124">To retrieve existing groups from your directory you can use the Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="a3b4b-125">若要擷取目錄中的所有群組，請在使用 Cmdlet 時不要使用參數：</span><span class="sxs-lookup"><span data-stu-id="a3b4b-125">To retrieve all groups in the directory, use the cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="a3b4b-126">Cmdlet 將會傳回所連線目錄中的所有群組。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-126">The cmdlet returns all groups in the connected directory.</span></span>

<span data-ttu-id="a3b4b-127">您可以使用 -objectID 參數來擷取您指定其群組 objectID 的特定群組：</span><span class="sxs-lookup"><span data-stu-id="a3b4b-127">You can use the -objectID parameter to retrieve a specific group for which you specify the group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="a3b4b-128">現在，Cmdlet 將傳回 objectID 與您所輸入之參數值相符的群組︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-128">The cmdlet now returns the group whose objectID matches the value of the parameter you entered:</span></span>

    DeletionTimeStamp            :
    ObjectId                     : e29bae11-4ac0-450c-bc37-6dae8f3da61b
    ObjectType                   : Group
    Description                  :
    DirSyncEnabled               :
    DisplayName                  : Pacific NW Support
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 9bb4139b-60a1-434a-8c0d-7c1f8eee2df9
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

<span data-ttu-id="a3b4b-129">您可以使用 -filter 參數搜尋特定群組。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-129">You can search for a specific group using the -filter parameter.</span></span> <span data-ttu-id="a3b4b-130">此參數採用 ODATA 篩選子句，並傳回和篩選條件相符的所有群組，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-130">This parameter takes an ODATA filter clause and returns all groups that match the filter, as in the following example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

> [!NOTE] 
> <span data-ttu-id="a3b4b-131">AzureAD PowerShell Cmdlet 實作 OData 查詢標準。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-131">The AzureAD PowerShell cmdlets implement the OData query standard.</span></span> <span data-ttu-id="a3b4b-132">如需詳細資訊，請參閱[使用 OData 端點的 OData 系統查詢選項](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter)中的 **$filter**。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-132">For more information, see **$filter** in [OData system query options using the OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="a3b4b-133">建立群組</span><span class="sxs-lookup"><span data-stu-id="a3b4b-133">Creating groups</span></span>
<span data-ttu-id="a3b4b-134">若要在目錄中建立新群組，請使用 New-AzureADGroup Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-134">To create a new group in your directory, use the New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="a3b4b-135">這個 Cmdlet 會建立名為 “Marketing" 的新安全性群組︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="a3b4b-136">更新群組</span><span class="sxs-lookup"><span data-stu-id="a3b4b-136">Updating groups</span></span>
<span data-ttu-id="a3b4b-137">若要更新現有的群組，請使用 Set-AzureADGroup Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-137">To update an existing group, use the Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="a3b4b-138">在這個範例中，我們要變更 “Intune Administrators” 群組的 DisplayName 屬性。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-138">In this example, we’re changing the DisplayName property of the group “Intune Administrators.”</span></span> <span data-ttu-id="a3b4b-139">首先，我們使用 Get-AzureADGroup Cmdlet 找到該群組，然後使用 DisplayName 屬性進行篩選︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-139">First, we’re finding the group using the Get-AzureADGroup cmdlet and filter using the DisplayName attribute:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

<span data-ttu-id="a3b4b-140">接下來，我們要將 Description 屬性變更為新值 “Intune Device Administrators”︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-140">Next, we’re changing the Description property to the new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="a3b4b-141">現在如果我們再次尋找該群組，就會看到 Description 屬性已經更新，以反映新的值︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-141">Now if we find the group again, we see the Description property is updated to reflect the new value:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Device Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

## <a name="deleting-groups"></a><span data-ttu-id="a3b4b-142">刪除群組</span><span class="sxs-lookup"><span data-stu-id="a3b4b-142">Deleting groups</span></span>
<span data-ttu-id="a3b4b-143">若要從目錄中刪除群組，請使用 Remove-AzureADGroup Cmdlet，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-143">To delete groups from your directory, use the Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="a3b4b-144">管理群組成員</span><span class="sxs-lookup"><span data-stu-id="a3b4b-144">Managing members of groups</span></span>
<span data-ttu-id="a3b4b-145">如果您需要將新成員新增至群組，請使用Add-AzureADGroupMember Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-145">If you need to add new members to a group, use the Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="a3b4b-146">此命令會將成員新增至上述範例中所使用的 Intune Administrators 群組︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-146">This command adds a member to the Intune Administrators group we used in the previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="a3b4b-147">我們想要新增成員的群組，其 ObjectID 就是 -ObjectId 參數，而我們想要新增為群組成員的使用者，其 ObjectID 為 -RefObjectId。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-147">The -ObjectId parameter is the ObjectID of the group to which we want to add a member, and the -RefObjectId is the ObjectID of the user we want to add as a member to the group.</span></span>

<span data-ttu-id="a3b4b-148">若要取得群組的現有成員，請使用 Get-AzureADGroupMember Cmdlet，如此範例所示︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-148">To get the existing members of a group, use the Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="a3b4b-149">若要移除先前加入群組的成員，請使用Remove-AzureADGroupMember Cmdlet，如此處所示︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-149">To remove the member we previously added to the group, use the Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="a3b4b-150">若要驗證使用者的群組成員資格，請使用 Select-AzureADGroupIdsUserIsMemberOf Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-150">To verify the group membership(s) of a user, use the Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="a3b4b-151">這個 Cmdlet 會將要檢查群組成員資格的使用者，其 ObjectId 以及一份要檢查成員資格的群組清單做為參數。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-151">This cmdlet takes as its parameters the ObjectId of the user for which to check the group memberships, and a list of groups for which to check the memberships.</span></span> <span data-ttu-id="a3b4b-152">務必要以 “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck” 複雜變數類型的形式提供群組清單，因此我們必須先使用該類型建立一個變數：</span><span class="sxs-lookup"><span data-stu-id="a3b4b-152">The list of groups must be provided in the form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="a3b4b-153">接下來，我們提供 groupIds 的值，以簽入此複雜變數的 "GroupIds" 屬性︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-153">Next, we provide values for the groupIds to check in the attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="a3b4b-154">現在，如果我們想要檢查 ObjectID 為 72cd4bbd-2594-40a2-935c-016f3cfeeeea 的使用者，是否具有 $g 中任何群組的群組成員資格，我們應該使用︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-154">Now, if we want to check the group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against the groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="a3b4b-155">傳回的值就是成員中有這位使用者的群組清單。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-155">The value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="a3b4b-156">您也可以使用 Select-AzureADGroupIdsContactIsMemberOf、Select-AzureADGroupIdsGroupIsMemberOf 或 Select-AzureADGroupIdsServicePrincipalIsMemberOf，在檢查特定群組清單中的連絡人、群組或服務主體成員資格時，採用這個方法</span><span class="sxs-lookup"><span data-stu-id="a3b4b-156">You can also apply this method to check Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="a3b4b-157">管理群組擁有者</span><span class="sxs-lookup"><span data-stu-id="a3b4b-157">Managing owners of groups</span></span>
<span data-ttu-id="a3b4b-158">若要將擁有者新增到群組，請使用 Add-AzureADGroupOwner Cmdlet︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-158">To add owners to a group, use the Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="a3b4b-159">我們想要加入擁有者的群組，其 ObjectID 就是 -ObjectId 參數，而我們想要新增為群組擁有者的使用者，其 ObjectID 為 -RefObjectId。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-159">The -ObjectId parameter is the ObjectID of the group to which we want to add an owner, and the -RefObjectId is the ObjectID of the user we want to add as an owner of the group.</span></span>

<span data-ttu-id="a3b4b-160">若要擷取群組的擁有者，請使用 Get AzureADGroupOwner Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="a3b4b-160">To retrieve the owners of a group, use the Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="a3b4b-161">Cmdlet 會傳回所指定群組的擁有者清單︰</span><span class="sxs-lookup"><span data-stu-id="a3b4b-161">The cmdlet returns the list of owners for the specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="a3b4b-162">如果您需要從群組中移除擁有者，請使用 Remove-AzureADGroupOwner Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="a3b4b-162">If you want to remove an owner from a group, use the Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="a3b4b-163">保留的別名</span><span class="sxs-lookup"><span data-stu-id="a3b4b-163">Reserved aliases</span></span> 
<span data-ttu-id="a3b4b-164">當群組建立時，某些端點允許終端使用者指定 mailNickname 或別名，以作為群組電子郵件地址的一部分。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-164">When a group is created, certain endpoints allow the end user to specify a mailNickname or alias to be used as part of the email address of the group.</span></span> <span data-ttu-id="a3b4b-165">以下的電子郵件別名具有高度權限，只有 Azure AD 全域管理員才能建立使用這些別名的群組。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-165">Groups with the following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="a3b4b-166">abuse</span><span class="sxs-lookup"><span data-stu-id="a3b4b-166">abuse</span></span> 
* <span data-ttu-id="a3b4b-167">admin</span><span class="sxs-lookup"><span data-stu-id="a3b4b-167">admin</span></span> 
* <span data-ttu-id="a3b4b-168">administrator</span><span class="sxs-lookup"><span data-stu-id="a3b4b-168">administrator</span></span> 
* <span data-ttu-id="a3b4b-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="a3b4b-169">hostmaster</span></span> 
* <span data-ttu-id="a3b4b-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="a3b4b-170">majordomo</span></span> 
* <span data-ttu-id="a3b4b-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="a3b4b-171">postmaster</span></span> 
* <span data-ttu-id="a3b4b-172">root</span><span class="sxs-lookup"><span data-stu-id="a3b4b-172">root</span></span> 
* <span data-ttu-id="a3b4b-173">secure</span><span class="sxs-lookup"><span data-stu-id="a3b4b-173">secure</span></span> 
* <span data-ttu-id="a3b4b-174">security</span><span class="sxs-lookup"><span data-stu-id="a3b4b-174">security</span></span> 
* <span data-ttu-id="a3b4b-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="a3b4b-175">ssl-admin</span></span> 
* <span data-ttu-id="a3b4b-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="a3b4b-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a3b4b-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a3b4b-177">Next steps</span></span>
<span data-ttu-id="a3b4b-178">您可以在 [Azure Active Directory Cmdlet](/powershell/azure/install-adv2?view=azureadps-2.0)中找到更多 Azure Active Directory PowerShell 文件。</span><span class="sxs-lookup"><span data-stu-id="a3b4b-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="a3b4b-179">使用 Azure Active Directory 群組來管理資源的存取權</span><span class="sxs-lookup"><span data-stu-id="a3b4b-179">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="a3b4b-180">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3b4b-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

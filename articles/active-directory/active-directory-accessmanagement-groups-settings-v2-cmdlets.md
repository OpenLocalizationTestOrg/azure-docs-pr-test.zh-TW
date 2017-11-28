---
title: "管理 Azure Active Directory 中的群組的範例 aaaPowerShell |Microsoft 文件"
description: "本頁面提供的 PowerShell 範例 toohelp 您管理 Azure Active Directory 中的群組"
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
ms.openlocfilehash: ba049babc436e99a290f20899b3a87bcfa811d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="b406a-104">適用於群組管理的 Azure Active Directory 第 2 版 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="b406a-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b406a-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b406a-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="b406a-106">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="b406a-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="b406a-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b406a-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="b406a-108">本文章包含的範例 toouse PowerShell toomanage 您 Azure Active Directory (Azure AD) 中的群組。</span><span class="sxs-lookup"><span data-stu-id="b406a-108">This article contains examples of how toouse PowerShell toomanage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="b406a-109">它也會告訴您如何 tooget 設定與 hello Azure AD PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="b406a-109">It also tells you how tooget set up with hello Azure AD PowerShell module.</span></span> <span data-ttu-id="b406a-110">首先，您必須[下載 hello Azure AD PowerShell 模組](https://www.powershellgallery.com/packages/AzureAD/)。</span><span class="sxs-lookup"><span data-stu-id="b406a-110">First, you must [download hello Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-hello-azure-ad-powershell-module"></a><span data-ttu-id="b406a-111">正在安裝 hello Azure AD PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="b406a-111">Installing hello Azure AD PowerShell module</span></span>
<span data-ttu-id="b406a-112">tooinstall hello Azure AD PowerShell 模組，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b406a-112">tooinstall hello Azure AD PowerShell module, use hello following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="b406a-113">hello 模組的 tooverify 已安裝，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b406a-113">tooverify that hello module was installed, use hello following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="b406a-114">現在您可以開始使用 hello 模組中的 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b406a-114">Now you can start using hello cmdlets in hello module.</span></span> <span data-ttu-id="b406a-115">Hello Azure AD 模組中的 hello cmdlet 的完整說明，請參閱 toohello 線上參考文件[Azure Active Directory PowerShell 版本 2](/powershell/azure/install-adv2?view=azureadps-2.0)。</span><span class="sxs-lookup"><span data-stu-id="b406a-115">For a full description of hello cmdlets in hello Azure AD module, please refer toohello online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-toohello-directory"></a><span data-ttu-id="b406a-116">連接 toohello 目錄</span><span class="sxs-lookup"><span data-stu-id="b406a-116">Connecting toohello directory</span></span>
<span data-ttu-id="b406a-117">您可以開始管理群組使用 Azure AD PowerShell cmdlet 之前，您必須連接您想 toomanage 的 PowerShell 工作階段 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="b406a-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session toohello directory you want toomanage.</span></span> <span data-ttu-id="b406a-118">使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b406a-118">Use hello following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="b406a-119">hello cmdlet 會提示您如 hello 認證新增您想 toouse tooaccess 您的目錄。</span><span class="sxs-lookup"><span data-stu-id="b406a-119">hello cmdlet prompts you for hello credentials you want toouse tooaccess your directory.</span></span> <span data-ttu-id="b406a-120">在此範例中，我們會使用karen@drumkit.onmicrosoft.comtooaccess hello 示範目錄。</span><span class="sxs-lookup"><span data-stu-id="b406a-120">In this example, we are using karen@drumkit.onmicrosoft.com tooaccess hello demonstration directory.</span></span> <span data-ttu-id="b406a-121">hello cmdlet 會傳回已成功連接確認 tooshow hello 工作階段 tooyour 目錄：</span><span class="sxs-lookup"><span data-stu-id="b406a-121">hello cmdlet returns a confirmation tooshow hello session was connected successfully tooyour directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="b406a-122">現在您可以開始使用您的目錄中的 hello azure Ad cmdlet toomanage 群組。</span><span class="sxs-lookup"><span data-stu-id="b406a-122">Now you can start using hello AzureAD cmdlets toomanage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="b406a-123">擷取群組</span><span class="sxs-lookup"><span data-stu-id="b406a-123">Retrieving groups</span></span>
<span data-ttu-id="b406a-124">您可以使用您目錄 tooretrieve 現有群組 hello Get AzureADGroups cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b406a-124">tooretrieve existing groups from your directory you can use hello Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="b406a-125">所有 tooretrieve 都群組在 hello 目錄中，使用不含參數的 hello 指令程式：</span><span class="sxs-lookup"><span data-stu-id="b406a-125">tooretrieve all groups in hello directory, use hello cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="b406a-126">hello cmdlet 會傳回 hello 連接的目錄中的所有群組。</span><span class="sxs-lookup"><span data-stu-id="b406a-126">hello cmdlet returns all groups in hello connected directory.</span></span>

<span data-ttu-id="b406a-127">您可以使用 hello-objectID 參數 tooretrieve 特定群組，您可以為其指定 hello 群組的 objectID:</span><span class="sxs-lookup"><span data-stu-id="b406a-127">You can use hello -objectID parameter tooretrieve a specific group for which you specify hello group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="b406a-128">hello cmdlet 現在會傳回其 objectID 符合您輸入的 hello 參數 hello 值 hello 群組：</span><span class="sxs-lookup"><span data-stu-id="b406a-128">hello cmdlet now returns hello group whose objectID matches hello value of hello parameter you entered:</span></span>

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

<span data-ttu-id="b406a-129">您可以搜尋特定群組使用 hello-filter 參數。</span><span class="sxs-lookup"><span data-stu-id="b406a-129">You can search for a specific group using hello -filter parameter.</span></span> <span data-ttu-id="b406a-130">此參數採用的 ODATA 篩選器子句，並傳回所有的群組符合 hello 篩選條件，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b406a-130">This parameter takes an ODATA filter clause and returns all groups that match hello filter, as in hello following example:</span></span>

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
> <span data-ttu-id="b406a-131">hello azure Ad PowerShell cmdlet 實作 hello 標準 OData 查詢。</span><span class="sxs-lookup"><span data-stu-id="b406a-131">hello AzureAD PowerShell cmdlets implement hello OData query standard.</span></span> <span data-ttu-id="b406a-132">如需詳細資訊，請參閱**$filter**中[OData 系統查詢選項使用 hello OData 端點](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter)。</span><span class="sxs-lookup"><span data-stu-id="b406a-132">For more information, see **$filter** in [OData system query options using hello OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="b406a-133">建立群組</span><span class="sxs-lookup"><span data-stu-id="b406a-133">Creating groups</span></span>
<span data-ttu-id="b406a-134">toocreate 中您目錄中，使用 hello 新增 AzureADGroup 指令程式的新群組。</span><span class="sxs-lookup"><span data-stu-id="b406a-134">toocreate a new group in your directory, use hello New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="b406a-135">這個 Cmdlet 會建立名為 “Marketing" 的新安全性群組︰</span><span class="sxs-lookup"><span data-stu-id="b406a-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="b406a-136">更新群組</span><span class="sxs-lookup"><span data-stu-id="b406a-136">Updating groups</span></span>
<span data-ttu-id="b406a-137">tooupdate 現有的群組，使用 hello 組 AzureADGroup 指令程式。</span><span class="sxs-lookup"><span data-stu-id="b406a-137">tooupdate an existing group, use hello Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="b406a-138">在此範例中，我們要變更 hello DisplayName 屬性的 hello 群組 「 Intune 系統管理員。 」</span><span class="sxs-lookup"><span data-stu-id="b406a-138">In this example, we’re changing hello DisplayName property of hello group “Intune Administrators.”</span></span> <span data-ttu-id="b406a-139">首先，我們發現 hello 群組 hello Get AzureADGroup cmdlet，並使用 hello DisplayName 屬性篩選中使用：</span><span class="sxs-lookup"><span data-stu-id="b406a-139">First, we’re finding hello group using hello Get-AzureADGroup cmdlet and filter using hello DisplayName attribute:</span></span>

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

<span data-ttu-id="b406a-140">接下來，我們要變更 hello 描述屬性 toohello 新值 「 Intune 裝置系統管理員 」:</span><span class="sxs-lookup"><span data-stu-id="b406a-140">Next, we’re changing hello Description property toohello new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="b406a-141">現在如果我們仍會尋找 hello 群組，我們會看到 hello Description 屬性更新的 tooreflect 是 hello 新值：</span><span class="sxs-lookup"><span data-stu-id="b406a-141">Now if we find hello group again, we see hello Description property is updated tooreflect hello new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="b406a-142">刪除群組</span><span class="sxs-lookup"><span data-stu-id="b406a-142">Deleting groups</span></span>
<span data-ttu-id="b406a-143">從您的目錄，toodelete 群組，如下所示使用 hello 移除 AzureADGroup cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b406a-143">toodelete groups from your directory, use hello Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="b406a-144">管理群組成員</span><span class="sxs-lookup"><span data-stu-id="b406a-144">Managing members of groups</span></span>
<span data-ttu-id="b406a-145">如果您需要 tooadd 新成員 tooa 群組，請使用 hello 新增 AzureADGroupMember cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b406a-145">If you need tooadd new members tooa group, use hello Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="b406a-146">此命令會新增 hello 前一個範例中我們使用的是成員 toohello Intune 系統管理員群組：</span><span class="sxs-lookup"><span data-stu-id="b406a-146">This command adds a member toohello Intune Administrators group we used in hello previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="b406a-147">hello-ObjectId 參數為 hello ObjectID 的 hello 群組 toowhich 我們想 tooadd 成員，而且 hello-RefObjectId hello ObjectID 我們想要的 hello 使用者 tooadd 做為成員 toohello 群組。</span><span class="sxs-lookup"><span data-stu-id="b406a-147">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd a member, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as a member toohello group.</span></span>

<span data-ttu-id="b406a-148">tooget hello 現有群組的成員，使用 hello Get AzureADGroupMember 指令程式，如此範例所示：</span><span class="sxs-lookup"><span data-stu-id="b406a-148">tooget hello existing members of a group, use hello Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="b406a-149">tooremove hello 成員我們先前加入 toohello 群組中，使用 hello 移除 AzureADGroupMember 指令程式，如此處所示：</span><span class="sxs-lookup"><span data-stu-id="b406a-149">tooremove hello member we previously added toohello group, use hello Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="b406a-150">tooverify hello 群組成員資格的使用者，使用 hello 選取 AzureADGroupIdsUserIsMemberOf 指令程式。</span><span class="sxs-lookup"><span data-stu-id="b406a-150">tooverify hello group membership(s) of a user, use hello Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="b406a-151">此 cmdlet 會將當做它的參數 hello hello 哪些 toocheck hello 群組成員資格使用者的 ObjectId 和哪些 toocheck hello 成員資格的群組清單。</span><span class="sxs-lookup"><span data-stu-id="b406a-151">This cmdlet takes as its parameters hello ObjectId of hello user for which toocheck hello group memberships, and a list of groups for which toocheck hello memberships.</span></span> <span data-ttu-id="b406a-152">群組 hello 清單必須是提供的複雜類型之變數的"Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck"hello 形式，因此我們必須先建立一個變數與這個類型：</span><span class="sxs-lookup"><span data-stu-id="b406a-152">hello list of groups must be provided in hello form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="b406a-153">接下來，我們提供 hello groupIds toocheck hello 屬性 」 GroupIds 」 這個複雜變數的值：</span><span class="sxs-lookup"><span data-stu-id="b406a-153">Next, we provide values for hello groupIds toocheck in hello attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="b406a-154">現在，如果我們想 toocheck hello 群組成員資格，ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea 針對 $g 中的 hello 群組的使用者，我們應該使用：</span><span class="sxs-lookup"><span data-stu-id="b406a-154">Now, if we want toocheck hello group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against hello groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="b406a-155">傳回的 hello 值是一份這位使用者為成員的群組。</span><span class="sxs-lookup"><span data-stu-id="b406a-155">hello value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="b406a-156">您也可以套用這個方法 toocheck 連絡人、 群組或服務主體在指定的清單，使用選取 AzureADGroupIdsContactIsMemberOf，選取 AzureADGroupIdsGroupIsMemberOf 群組的成員資格或選取 AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="b406a-156">You can also apply this method toocheck Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="b406a-157">管理群組擁有者</span><span class="sxs-lookup"><span data-stu-id="b406a-157">Managing owners of groups</span></span>
<span data-ttu-id="b406a-158">tooadd owners tooa 群組、 使用 hello 新增 AzureADGroupOwner 指令程式：</span><span class="sxs-lookup"><span data-stu-id="b406a-158">tooadd owners tooa group, use hello Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="b406a-159">hello-ObjectId 參數為 hello ObjectID 的 hello 群組 toowhich 我們想 tooadd 擁有者，而且 hello-RefObjectId hello ObjectID 的 hello 使用者想 tooadd 以 hello 群組的擁有者。</span><span class="sxs-lookup"><span data-stu-id="b406a-159">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd an owner, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as an owner of hello group.</span></span>

<span data-ttu-id="b406a-160">tooretrieve hello 的擁有者的群組，使用 hello Get AzureADGroupOwner cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b406a-160">tooretrieve hello owners of a group, use hello Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="b406a-161">hello cmdlet 會傳回 hello hello 指定群組的擁有者清單：</span><span class="sxs-lookup"><span data-stu-id="b406a-161">hello cmdlet returns hello list of owners for hello specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="b406a-162">如果您想 tooremove 從群組的擁有者，請使用 hello 移除 AzureADGroupOwner cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b406a-162">If you want tooremove an owner from a group, use hello Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="b406a-163">保留的別名</span><span class="sxs-lookup"><span data-stu-id="b406a-163">Reserved aliases</span></span> 
<span data-ttu-id="b406a-164">建立群組時，特定端點允許 hello 終端使用者 toospecify mailNickname 或別名 toobe hello 電子郵件地址 hello 群組的一部分。</span><span class="sxs-lookup"><span data-stu-id="b406a-164">When a group is created, certain endpoints allow hello end user toospecify a mailNickname or alias toobe used as part of hello email address of hello group.</span></span> <span data-ttu-id="b406a-165">Azure AD 全域管理員可以只建立群組以 hello 遵循高特殊權限的電子郵件別名。</span><span class="sxs-lookup"><span data-stu-id="b406a-165">Groups with hello following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="b406a-166">abuse</span><span class="sxs-lookup"><span data-stu-id="b406a-166">abuse</span></span> 
* <span data-ttu-id="b406a-167">admin</span><span class="sxs-lookup"><span data-stu-id="b406a-167">admin</span></span> 
* <span data-ttu-id="b406a-168">administrator</span><span class="sxs-lookup"><span data-stu-id="b406a-168">administrator</span></span> 
* <span data-ttu-id="b406a-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="b406a-169">hostmaster</span></span> 
* <span data-ttu-id="b406a-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="b406a-170">majordomo</span></span> 
* <span data-ttu-id="b406a-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="b406a-171">postmaster</span></span> 
* <span data-ttu-id="b406a-172">root</span><span class="sxs-lookup"><span data-stu-id="b406a-172">root</span></span> 
* <span data-ttu-id="b406a-173">secure</span><span class="sxs-lookup"><span data-stu-id="b406a-173">secure</span></span> 
* <span data-ttu-id="b406a-174">security</span><span class="sxs-lookup"><span data-stu-id="b406a-174">security</span></span> 
* <span data-ttu-id="b406a-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="b406a-175">ssl-admin</span></span> 
* <span data-ttu-id="b406a-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="b406a-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b406a-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b406a-177">Next steps</span></span>
<span data-ttu-id="b406a-178">您可以在 [Azure Active Directory Cmdlet](/powershell/azure/install-adv2?view=azureadps-2.0)中找到更多 Azure Active Directory PowerShell 文件。</span><span class="sxs-lookup"><span data-stu-id="b406a-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="b406a-179">使用 Azure Active Directory 群組來管理存取 tooresources</span><span class="sxs-lookup"><span data-stu-id="b406a-179">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="b406a-180">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b406a-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

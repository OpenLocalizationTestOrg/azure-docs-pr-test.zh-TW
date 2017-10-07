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
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a>適用於群組管理的 Azure Active Directory 第 2 版 Cmdlet
> [!div class="op_single_selector"]
> * [Azure 入口網站](active-directory-groups-create-azure-portal.md)
> * [Azure 傳統入口網站](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

本文章包含的範例 toouse PowerShell toomanage 您 Azure Active Directory (Azure AD) 中的群組。  它也會告訴您如何 tooget 設定與 hello Azure AD PowerShell 模組。 首先，您必須[下載 hello Azure AD PowerShell 模組](https://www.powershellgallery.com/packages/AzureAD/)。

## <a name="installing-hello-azure-ad-powershell-module"></a>正在安裝 hello Azure AD PowerShell 模組
tooinstall hello Azure AD PowerShell 模組，使用下列命令的 hello:

    PS C:\Windows\system32> install-module azuread

hello 模組的 tooverify 已安裝，請使用下列命令的 hello:

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

現在您可以開始使用 hello 模組中的 hello cmdlet。 Hello Azure AD 模組中的 hello cmdlet 的完整說明，請參閱 toohello 線上參考文件[Azure Active Directory PowerShell 版本 2](/powershell/azure/install-adv2?view=azureadps-2.0)。

## <a name="connecting-toohello-directory"></a>連接 toohello 目錄
您可以開始管理群組使用 Azure AD PowerShell cmdlet 之前，您必須連接您想 toomanage 的 PowerShell 工作階段 toohello 目錄。 使用下列命令的 hello:

    PS C:\Windows\system32> Connect-AzureAD

hello cmdlet 會提示您如 hello 認證新增您想 toouse tooaccess 您的目錄。 在此範例中，我們會使用karen@drumkit.onmicrosoft.comtooaccess hello 示範目錄。 hello cmdlet 會傳回已成功連接確認 tooshow hello 工作階段 tooyour 目錄：

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

現在您可以開始使用您的目錄中的 hello azure Ad cmdlet toomanage 群組。

## <a name="retrieving-groups"></a>擷取群組
您可以使用您目錄 tooretrieve 現有群組 hello Get AzureADGroups cmdlet。 所有 tooretrieve 都群組在 hello 目錄中，使用不含參數的 hello 指令程式：

    PS C:\Windows\system32> get-azureadgroup

hello cmdlet 會傳回 hello 連接的目錄中的所有群組。

您可以使用 hello-objectID 參數 tooretrieve 特定群組，您可以為其指定 hello 群組的 objectID:

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

hello cmdlet 現在會傳回其 objectID 符合您輸入的 hello 參數 hello 值 hello 群組：

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

您可以搜尋特定群組使用 hello-filter 參數。 此參數採用的 ODATA 篩選器子句，並傳回所有的群組符合 hello 篩選條件，如 hello 下列範例所示：

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
> hello azure Ad PowerShell cmdlet 實作 hello 標準 OData 查詢。 如需詳細資訊，請參閱**$filter**中[OData 系統查詢選項使用 hello OData 端點](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter)。

## <a name="creating-groups"></a>建立群組
toocreate 中您目錄中，使用 hello 新增 AzureADGroup 指令程式的新群組。 這個 Cmdlet 會建立名為 “Marketing" 的新安全性群組︰

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a>更新群組
tooupdate 現有的群組，使用 hello 組 AzureADGroup 指令程式。 在此範例中，我們要變更 hello DisplayName 屬性的 hello 群組 「 Intune 系統管理員。 」 首先，我們發現 hello 群組 hello Get AzureADGroup cmdlet，並使用 hello DisplayName 屬性篩選中使用：

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

接下來，我們要變更 hello 描述屬性 toohello 新值 「 Intune 裝置系統管理員 」:

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

現在如果我們仍會尋找 hello 群組，我們會看到 hello Description 屬性更新的 tooreflect 是 hello 新值：

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

## <a name="deleting-groups"></a>刪除群組
從您的目錄，toodelete 群組，如下所示使用 hello 移除 AzureADGroup cmdlet:

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a>管理群組成員
如果您需要 tooadd 新成員 tooa 群組，請使用 hello 新增 AzureADGroupMember cmdlet。 此命令會新增 hello 前一個範例中我們使用的是成員 toohello Intune 系統管理員群組：

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

hello-ObjectId 參數為 hello ObjectID 的 hello 群組 toowhich 我們想 tooadd 成員，而且 hello-RefObjectId hello ObjectID 我們想要的 hello 使用者 tooadd 做為成員 toohello 群組。

tooget hello 現有群組的成員，使用 hello Get AzureADGroupMember 指令程式，如此範例所示：

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

tooremove hello 成員我們先前加入 toohello 群組中，使用 hello 移除 AzureADGroupMember 指令程式，如此處所示：

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

tooverify hello 群組成員資格的使用者，使用 hello 選取 AzureADGroupIdsUserIsMemberOf 指令程式。 此 cmdlet 會將當做它的參數 hello hello 哪些 toocheck hello 群組成員資格使用者的 ObjectId 和哪些 toocheck hello 成員資格的群組清單。 群組 hello 清單必須是提供的複雜類型之變數的"Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck"hello 形式，因此我們必須先建立一個變數與這個類型：

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

接下來，我們提供 hello groupIds toocheck hello 屬性 」 GroupIds 」 這個複雜變數的值：

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

現在，如果我們想 toocheck hello 群組成員資格，ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea 針對 $g 中的 hello 群組的使用者，我們應該使用：

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


傳回的 hello 值是一份這位使用者為成員的群組。 您也可以套用這個方法 toocheck 連絡人、 群組或服務主體在指定的清單，使用選取 AzureADGroupIdsContactIsMemberOf，選取 AzureADGroupIdsGroupIsMemberOf 群組的成員資格或選取 AzureADGroupIdsServicePrincipalIsMemberOf

## <a name="managing-owners-of-groups"></a>管理群組擁有者
tooadd owners tooa 群組、 使用 hello 新增 AzureADGroupOwner 指令程式：

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

hello-ObjectId 參數為 hello ObjectID 的 hello 群組 toowhich 我們想 tooadd 擁有者，而且 hello-RefObjectId hello ObjectID 的 hello 使用者想 tooadd 以 hello 群組的擁有者。

tooretrieve hello 的擁有者的群組，使用 hello Get AzureADGroupOwner cmdlet:

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

hello cmdlet 會傳回 hello hello 指定群組的擁有者清單：

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

如果您想 tooremove 從群組的擁有者，請使用 hello 移除 AzureADGroupOwner cmdlet:

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a>保留的別名 
建立群組時，特定端點允許 hello 終端使用者 toospecify mailNickname 或別名 toobe hello 電子郵件地址 hello 群組的一部分。 Azure AD 全域管理員可以只建立群組以 hello 遵循高特殊權限的電子郵件別名。 
  
* abuse 
* admin 
* administrator 
* hostmaster 
* majordomo 
* postmaster 
* root 
* secure 
* security 
* ssl-admin 
* webmaster 

## <a name="next-steps"></a>後續步驟
您可以在 [Azure Active Directory Cmdlet](/powershell/azure/install-adv2?view=azureadps-2.0)中找到更多 Azure Active Directory PowerShell 文件。

* [使用 Azure Active Directory 群組來管理存取 tooresources](active-directory-manage-groups.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

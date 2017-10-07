---
title: "Azure Active Directory 中的 aaaRestore 已刪除的 Office 365 群組 |Microsoft 文件"
description: "Toorestore 已刪除的群組、 檢視可還原的已群組和 permamnently 刪除 Azure Active Directory 中的群組"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a>在 Azure Active Directory 中還原已刪除的 Office 365 群組

當您刪除 hello Azure Active Directory (Azure AD) 中的 Office 365 群組時，hello 刪除群組為保留，但看不到 30 天內從 hello 刪除日期。 這是可以還原 hello 群組和其內容，如有需要。 此功能會受到限制專門 tooOffice 365 Azure AD 中的群組。 無法針對安全性群組和發佈群組使用。

> [!NOTE] 
> 請勿使用`Remove-MsolGroup`因為永遠會清除 hello 群組。 一律使用`Remove-AzureADMSGroup`toodelete O365 群組。 

hello 權限所需 toorestore 群組可以是 hello 下列任何一項：

角色  | 權限 
--------- | ---------
公司系統管理員、合作夥伴第 2 層支援，以及 InTune 服務管理員 | 可以還原任何已刪除的 Office 365 群組 
使用者帳戶管理員和合作夥伴第 1 層支援 | 可以還原任何已刪除的 Office 365 群組，除了那些指派 toohello 公司系統管理員角色 
User | 可以還原他們所擁有的任何已刪除的 Office 365 群組 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a>檢視 hello 刪除可用的 toorestore Office 365 群組
hello 下列指令程式可以使用的 tooview hello 刪除群組 tooverify hello 其中一個，或您感興趣的一不尚未永久清除。 這些 cmdlet 屬於 hello [Azure AD PowerShell 模組](https://www.powershellgallery.com/packages/AzureAD/)。 可以找到此模組的詳細資訊，在 hello [Azure Active Directory PowerShell 版本 2](/powershell/azure/install-adv2?view=azureadps-2.0)發行項。

1.  執行下列 cmdlet toodisplay 刪除所有 Office 365 租用戶中的群組仍然可以使用 toorestore hello。
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  或者，如果您知道某特定群組的 hello objectID （而且您可以從步驟 1 中的 hello cmdlet 取得），執行下列 cmdlet tooverify 的 hello 特定的已刪除的群組的 hello 不尚未已永久清除。
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a>如何 toorestore 已刪除的 Office 365 群組
一旦您確認該 hello 群組是 toorestore 仍然可以使用時，請使用其中一個步驟的 hello 還原 hello 刪除群組。 如果 hello 群組包含文件、 預存程序的網站或其他持續性的物件，它最多可能需要 too24 小時 toofully 還原為群組和其內容。

1.  執行 hello 下列 cmdlet toorestore hello 群組和其內容。
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

或者，hello 下列 cmdlet 可以執行 toopermanently 移除 hello 刪除群組。
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a>如何知道此動作已完成？
您已成功還原將 Office 365 群組執行 hello tooverify `Get-AzureADGroup –ObjectId <objectId>` hello 群組 cmdlet toodisplay 資訊。 Hello 還原之後完成的要求：
- hello 群組會出現在交換上的 hello 左瀏覽列
- hello 計劃 hello 群組會出現在規劃
- 任何 Sharepoint 網站及其所有內容都將可供使用
- 您可以從任何 hello 交換端點和支援 Office 365 群組的其他 Office 365 工作負載存取 hello 群組


## <a name="next-steps"></a>後續步驟
這些文章提供有關 Azure Active Directory 群組的其他資訊。

* [查看現有的群組](active-directory-groups-view-azure-portal.md)
* [管理群組的設定](active-directory-groups-settings-azure-portal.md)
* [管理群組的成員](active-directory-groups-members-azure-portal.md)
* [管理群組的成員資格](active-directory-groups-membership-azure-portal.md)
* [管理群組中使用者的動態規則](active-directory-groups-dynamic-membership-azure-portal.md)

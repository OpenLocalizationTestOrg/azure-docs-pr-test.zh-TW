---
title: "aaaPreview Office 365 群組在 Azure Active Directory 中的到期日 |Microsoft 文件"
description: "在 Azure Active Directory （預覽） tooset for Office 365 的到期組成群組的方式"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a>設定 Office 365 群組到期日 (預覽)

您現在可以藉由設定到期日，對您選取任何 Office 365 群組管理 Office 365 群組 hello 生命週期。 這些群組的擁有者一旦設定此期限，已要求 toorenew 其群組，如果它們仍然需要 hello 群組。 未續訂的任何 Office 365 群組將會予以刪除。 可以還原已刪除的任何 Office 365 群組的 30 天內，hello 群組擁有者或 hello 系統管理員。  


> [!NOTE]
> 您可以僅針對 Office 365 群組設定到期日。
>
> 設定已指派 Azure AD Premium 授權之 O365 群組所需要的到期日
>   - hello 系統管理員設定 hello hello 租用戶的到期設定
>   - 選取此設定的 hello 群組的所有成員

## <a name="set-office-365-groups-expiration"></a>設定 Office 365 群組到期日

1. 開啟 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)與 Azure AD 租用戶中的全域系統管理員帳戶。

2. 開啟 Azure AD，選取 [使用者和群組]。

3. 選取**群組設定**，然後選取 **到期**tooopen hello 逾期設定。
  
  ![[到期] 刀鋒視窗](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. 在 hello**到期**刀鋒視窗中，您可以：

  * 設定以天為單位的 hello 群組存留時間。 您可以選取其中一個 hello 預設值或自訂的值 （應為 31 天或更多）。 
  * 指定的群組有沒有擁有者時，傳送 hello 更新與到期通知電子郵件地址。 
  * 選取到期的 Office 365 群組。 您可以啟用到期日**所有**Office 365 群組中，您可以從 hello Office 365 群組中選取，或者您選取**無**停用所有群組的到期日。
  * 當您完成時，選取 [儲存] 會儲存您的設定。

如需 toodownload 並安裝 hello Microsoft PowerShell 模組 tooconfigure 到期日，Office 365 群組透過 PowerShell 的指示，請參閱[Azure Active Directory V2 PowerShell 模組-公開預覽版本 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137)。

Toohello Office 365 群組擁有者 30 天，15 天和 tooexpiration hello 群組的 1 日之前，會傳送電子郵件通知，例如這一個。

![到期電子郵件通知](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

然後可以選取 hello 群組擁有者**更新群組**toorenew hello Office 365 群組，或者也可以選取**移 toogroup** toosee hello 成員以及其他詳細資料 hello 群組。

當群組到期時，hello 群組將刪除 hello 到期日期後一天。 這種電子郵件通知會傳送告知 hello 到期和後續刪除其 Office 365 群組 toohello Office 365 群組擁有者。

![群組刪除電子郵件通知](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

可選取還原 hello 群組**還原群組**或 Azure Active Directory 中還原已刪除的 Office 365 群組] 中所述使用 PowerShell cmdlet (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal)。
    
如果您要還原的 hello 群組包含文件、 SharePoint 網站或其他持續性的物件，它可能會佔用 too24 小時 toofully 還原 hello 群組和其內容。

> [!NOTE]
> * 當部署 hello 到期日設定，可能會有超過 hello 到期視窗部分群組。 這些群組不會被立即刪除，但設定 too30 到期之前的天數。 hello 第一個更新通知電子郵件會在一天之內送出。 例如，群組 A 已建立 400 天前，並設定 hello 到期間隔 too180 天。 當您套用到期日設定時，群組 A 會有 30 天之後會被刪除，, 除非 hello 擁有者更新它。
> * 當刪除並還原動態群組時，它被視為新的群組並重新填入相應 toohello 規則。 此程序可能佔用 too24 小時。

## <a name="next-steps"></a>後續步驟
這些文章提供有關 Azure AD 群組的其他資訊。

* [查看現有的群組](active-directory-groups-view-azure-portal.md)
* [管理群組的設定](active-directory-groups-settings-azure-portal.md)
* [管理群組的成員](active-directory-groups-members-azure-portal.md)
* [管理群組的成員資格](active-directory-groups-membership-azure-portal.md)
* [管理群組中使用者的動態規則](active-directory-groups-dynamic-membership-azure-portal.md)

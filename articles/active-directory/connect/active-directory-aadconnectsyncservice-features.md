---
title: "aaaAzure AD Connect 同步服務功能和組態 |Microsoft 文件"
description: "描述 Azure AD Connect 同步處理服務的服務端功能。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a>Azure AD Connect 同步處理服務功能
Azure AD connect 的 hello 同步處理功能具有兩個元件：

* hello 內部元件，名為**Azure AD Connect 同步處理**，也稱為**同步處理引擎**。
* 也就位於 Azure AD 中的 hello 服務**Azure AD Connect 同步處理服務**

本主題說明 hello 下列功能如何的 hello **Azure AD Connect 同步處理服務**工作並設定它們使用 Windows PowerShell。

這些設定是由 hello [Azure Active Directory 的 Windows PowerShell 模組](http://aka.ms/aadposh)。 從 Azure AD Connect 個別進行下載和安裝。 在本主題中的 hello cmdlet 已導入 hello [2016 年 3 月發行 （建置 9031.1）](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1)。 如果您不需要在本主題中的 hello cmdlet，或它們不會產生的 hello 相同結果，則請確定您執行 hello 最新版本。

在執行的 Azure AD 目錄中的 toosee hello 組態`Get-MsolDirSyncFeatures`。  
![Get-MsolDirSyncFeatures 結果](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)

其中許多設定只能由 Azure AD Connect 進行變更。

hello 設定下列設定可以是`Set-MsolDirSyncFeature`:

| DirSyncFeature | 註解 |
| --- | --- |
| [EnableSoftMatchOnUpn](#userprincipalname-soft-match) |允許物件 toojoin 上的 userPrincipalName 加法 tooprimary SMTP 位址。 |
| [SynchronizeUpnForManagedUsers](#synchronize-userprincipalname-updates) |Hello 同步處理引擎 tooupdate hello userPrincipalName 屬性可讓受管理/授權 （非同盟） 的使用者。 |

啟用功能後，即無法將其停用。

> [!NOTE]
> 從 2016 年 8 月 24 日 hello 功能*重複屬性復原*預設會啟用新的 azure AD 目錄。 這項功能也會在此日期前建立的目錄上推出和啟用。 當您的目錄是 tooget 有關啟用這項功能，您會收到電子郵件通知。
> 
> 

hello 下列設定由 Azure AD Connect 設定，而且無法修改由`Set-MsolDirSyncFeature`:

| DirSyncFeature | 註解 |
| --- | --- |
| DeviceWriteback |[Azure AD Connect：啟用裝置回寫](active-directory-aadconnect-feature-device-writeback.md) |
| DirectoryExtensions |[Azure AD Connect 同步處理：目錄擴充](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency](#duplicate-attribute-resiliency) |可讓它是另一個物件，而非在匯出期間失敗 hello 整個物件的複本時，隔離屬性 toobe。 |
| PasswordSync |[使用 Azure AD Connect 同步處理實作密碼同步處理](active-directory-aadconnectsync-implement-password-synchronization.md) |
| UnifiedGroupWriteback |[預覽：群組回寫](active-directory-aadconnect-feature-preview.md#group-writeback) |
| UserWriteback |目前不支援。 |

## <a name="duplicate-attribute-resiliency"></a>重複屬性恢復功能
而非發生失敗 tooprovision 物件具有重複的 Upn/proxyAddresses，hello 重複的屬性 「 隔離 」，而且會指派暫時的值。 Hello 衝突解決時，暫時的 hello UPN 的自動變更 toohello 適當的值。 如需詳細資訊，請參閱 [身分識別同步處理和重複屬性恢復功能](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)。

## <a name="userprincipalname-soft-match"></a>UserPrincipalName 大致比對
啟用這項功能時，軟體相符項目中已啟用的 UPN 加法 toohello[主要 SMTP 位址](https://support.microsoft.com/kb/2641663)，永遠啟用。 軟相符項目是使用的 toomatch 現有的雲端使用者與內部部署使用者的 Azure AD 中。

如果您需要 toomatch 內部 AD 帳戶與 hello 雲端中建立的現有帳戶，而且您不能使用 Exchange Online，則此功能十分有用。 在此案例中，您通常不需要原因 tooset hello SMTP 屬性 hello 雲端中。

在新建立的 Azure AD 目錄中，預設會開啟這項功能。 您可以執行下列項目，查看是否已啟用此功能︰  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

如果您的 Azure AD 目錄未啟用這項功能，您可以執行下列項目加以啟用︰  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a>同步處理 userPrincipalName 更新
在過去，使用從內部部署的 hello 同步服務更新 toohello UserPrincipalName 屬性已被封鎖，除非這些條件都成立：

* hello 使用者被管理 （非同盟）。
* hello 使用者尚未指派授權。

如需詳細資訊，請參閱[Office 365、 Azure 或 Intune 中的名稱不相符的使用者 hello 在內部部署 UPN 或替代登入識別碼](https://support.microsoft.com/kb/2523192)。

啟用這項功能可讓 hello 同步處理引擎 tooupdate hello userPrincipalName，變更在內部部署，且您使用密碼同步處理時。如果您使用同盟，則不支援這項功能。

在新建立的 Azure AD 目錄中，預設會開啟這項功能。 您可以執行下列項目，查看是否已啟用此功能︰  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

如果您的 Azure AD 目錄未啟用這項功能，您可以執行下列項目加以啟用︰  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

啟用這項功能之後，現有的 userPrincipalName 值會保持不變。 下次 hello userPrincipalName 屬性在內部變更，對使用者的 hello 一般差異同步處理會更新 hello UPN。  

## <a name="see-also"></a>另請參閱
* [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。


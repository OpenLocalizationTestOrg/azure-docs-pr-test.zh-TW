---
title: "Azure AD Connect 同步：防止意外刪除 |Microsoft Docs"
description: "本主題描述 hello 防止被意外刪除 （防止意外刪除） 功能，在 Azure AD Connect。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 159597f8354806fcaea1430e0ff84956338592a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a>Azure AD Connect 同步處理：防止意外刪除
本主題描述 hello 防止被意外刪除 （防止意外刪除） 功能，在 Azure AD Connect。

時安裝 Azure AD Connect，防止被意外刪除預設會啟用並設定的 toonot 中允許超過 500 個刪除匯出。 這項功能是設計的 tooprotect 您從意外組態變更，並變更會影響許多使用者和其他物件的 tooyour 在內部部署目錄。

## <a name="what-is-prevent-accidental-deletes"></a>防止意外刪除是什麼
會看到多項刪除的常見案例包括：

* 變更太[篩選](active-directory-aadconnectsync-configure-filtering.md)其中整個[OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering)或[網域](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering)會變成未選取。
* OU 中的所有物件遭到刪除。
* OU 已重新命名，以便在它的所有物件都會都視為 toobe 同步處理的範圍。

可以使用 PowerShell 變更 hello 預設值為 500 個物件使用`Enable-ADSyncExportDeletionThreshold`。 您應該設定組織的此值 toofit hello 大小。 因為 hello 同步處理排程器執行每隔 30 分鐘，hello 值會是 hello 30 分鐘內出現的刪除數目。

如果有太多的接移刪除 toobe 會匯出 tooAzure AD，則 hello 匯出會停止，您會收到一封電子郵件，像這樣：

![防止意外刪除電子郵件](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> *Hello (技術連絡人)。（時間） 在 hello 身分識別同步處理服務偵測到刪除的 hello 數目超過 hello 刪除設定的臨界值 （組織名稱）。本次執行身分識別同步處理時，共傳送 (數目) 個物件進行刪除。這在達到或超過設定的 hello 刪除臨界值 （數字） 物件。我們需要您 tooprovide 確認刪除動作應該是之前，我們將繼續處理。請 hello 防止意外刪除，如需此電子郵件訊息中所列的 hello 錯誤詳細資訊，參閱。*
>
> 

您也可以查看 hello 狀態`stopped-deletion-threshold-exceeded`當您查看 hello**同步處理服務管理員**hello 匯出設定檔的 UI。
![防止意外刪除 Sync Service Manager UI](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)

如果這是非預期的結果，請進行調查，並採取修正動作。 toosee 哪些物件是關於 toobe 刪除，請勿 hello 遵循：

1. 啟動**同步處理服務**從 hello 開始] 功能表。
2. 跳過**連接器**。
3. 選取 hello 連接器類型**Azure Active Directory**。
4. 在下**動作**toohello 的權限，選取**搜尋連接器空間**。
5. 在 hello 下快顯**範圍**，選取**中斷連線後**hello 過去中挑選一次。 按一下 [搜尋] 。 此頁面提供有關 toobe 刪除所有物件的檢視。 按一下每個項目，您可以取得 hello 物件的其他資訊。 您也可以按一下**資料行設定**tooadd 其他屬性 toobe 在 hello 方格中顯示。

![搜尋連接器空間](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

如果需要針對所有 hello 刪除，然後 hello 遵循：

1. tooretrieve hello 目前刪除閾值，執行 hello PowerShell cmdlet `Get-ADSyncExportDeletionThreshold`。 提供 Azure AD 全域系統管理員帳戶與密碼。 hello 預設值為 500。
2. tootemporarily 停用此保護，並讓這些刪除瀏覽，請執行 hello PowerShell cmdlet: `Disable-ADSyncExportDeletionThreshold`。 提供 Azure AD 全域系統管理員帳戶與密碼。
   ![認證](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)
3. 以 hello Azure 仍然選取 Active Directory 連接器，選取 [hello 動作**執行**選取**匯出**。
4. toore 啟用 hello 保護執行 hello PowerShell cmdlet: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`。 取代您注意到擷取 hello 目前刪除閾值時的 hello 值為 500。 提供 Azure AD 全域系統管理員帳戶與密碼。

## <a name="next-steps"></a>後續步驟
**概觀主題**

* [Azure AD Connect 同步處理：了解及自訂同步處理](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

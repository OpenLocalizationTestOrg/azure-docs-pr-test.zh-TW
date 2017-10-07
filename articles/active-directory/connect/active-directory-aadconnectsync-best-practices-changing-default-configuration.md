---
title: "Azure AD Connect 同步： 變更 hello 預設組態 |Microsoft 文件"
description: "提供變更 hello 的 Azure AD Connect 同步處理的預設組態的最佳作法。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: aa05e935edd02c49c3c3fdc198b854f50327847c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-hello-default-configuration"></a>Azure AD Connect 同步： 變更 hello 預設組態的最佳做法
本主題的 hello 目的是 toodescribe 支援和不支援變更 tooAzure AD Connect 同步處理。

建立 Azure AD connect 的 hello 組態適用於 「 現狀 」 同步處理內部部署 Active Directory 與 Azure AD 的大多數環境。 不過，在某些情況下，它是必要的 tooapply 需要某些變更 tooa 組態 toosatisfy 特定或需求。

## <a name="changes-toohello-service-account"></a>變更 toohello 服務帳戶
Azure AD Connect 同步 hello 安裝精靈所建立的服務帳戶下執行。 此服務帳戶會保留 hello 加密金鑰 toohello 資料庫同步處理所使用。它使用 127 個字元長的密碼建立和設定 toonot hello 密碼到期。

* 它是**不支援**hello 服務帳戶的 toochange 或重設的 hello 密碼。 這樣會終結 hello 加密金鑰並且 hello 服務不能 tooaccess hello 資料庫，且不能 toostart。

## <a name="changes-toohello-scheduler"></a>變更 toohello 排程器
開頭為從組建 1.1 的 hello 版本 (年 2 月 2016)，您可以設定 hello[排程器](active-directory-aadconnectsync-feature-scheduler.md)toohave 不同的同步處理循環比 hello 預設 30 分鐘的時間。

## <a name="changes-toosynchronization-rules"></a>變更 tooSynchronization 規則
hello 安裝精靈提供了應該 toowork hello 最常見案例的組態。 萬一您需要 toomake 變更 toohello 組態，您必須遵循這些規則 toostill 具有支援的組態。

* 您可以[變更屬性流程](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes)如果 hello 預設直接屬性流程不是適用於您的組織。
* 如果您想太[流動屬性](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute)並移除任何現有的屬性值在 Azure AD 中，則您在此案例需要 toocreate 規則。
* [停用不必要的同步處理規則](#disable-an-unwanted-sync-rule) 而非加以刪除。 升級期間會重新建立已刪除的規則。
* 太[變更鶈蜪規則](#change-an-out-of-box-rule)，您應該複製一份 hello 原始規則並停用 hello 鶈蜪規則。 hello 同步處理規則編輯器會提示，並協助您。
* 匯出自訂同步處理規則使用 hello 同步處理規則編輯器。 hello 編輯器會提供您一個 PowerShell 指令碼，您可以使用 tooeasily 重新建立它們的災害復原案例中。

> [!WARNING]
> hello 現成的同步處理規則有憑證指紋。 如果 toothese 規則進行變更，不再符合 hello 指紋。 當您嘗試 tooapply Azure AD Connect 的新版本時，可能會在未來的 hello 發生問題。 在本文中，只提供變更 hello 方式描述。

### <a name="disable-an-unwanted-sync-rule"></a>停用不必要的同步處理規則
請勿刪除現成可用的同步處理規則。 升級期間會重新建立此規則。

在某些情況下，hello 安裝精靈所產生的組態，您的拓撲無法作用。 例如，如果您有帳戶資源樹系拓撲，但您有擴充的 hello 結構描述與 hello Exchange 結構描述的 hello 帳戶樹系中，規則適用於 Exchange 會建立 hello 帳戶樹系和 hello 資源樹系。 在此情況下，您需要適用於 Exchange toodisable hello 的同步處理規則。

![已停用同步處理規則](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

在上述的 hello 圖片，hello 安裝精靈已找到 hello 帳戶樹系中的舊的 Exchange 2003 結構描述。 Fabrikam 的環境中導入 hello 資源樹系之前，已加入此結構描述延伸模組。 tooensure 同步 hello 舊 Exchange 實作沒有屬性，應停用 hello 同步處理規則，如所示。

### <a name="change-an-out-of-box-rule"></a>變更現成可用的規則
hello 唯一的時候，您應該變更預設的規則時，您需要 toochange hello 聯結規則。 如果您需要 toochange 屬性流程，則您應該建立同步處理規則的優先順序高於 hello 鶈蜪規則。 只有您幾乎需要 tooclone 規則是 hello hello**中 from AD-User Join**。 您可以使用具有較高優先順序的規則來覆寫所有其他規則。

如果您需要 toomake 變更 tooan 鶈蜪規則，然後應該複製一份 hello 鶈蜪規則並停用 hello 原始規則。 然後請 hello 變更 toohello 複製的規則。 hello 同步處理規則編輯器會協助您進行這些步驟。 當您開啟現成可用的規則時，即會顯示此對話方塊：  
![對現成可用的規則發出警告](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

選取**是**toocreate hello 規則的複本。 然後開啟 hello 複製的規則。  
![複製的規則](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)

在此複製的規則，進行任何必要的變更 tooscope、 聯結和轉換。

## <a name="next-steps"></a>後續步驟
**概觀主題**

* [Azure AD Connect 同步處理：了解及自訂同步處理](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

---
title: "在 Azure Active Directory 群組 aaaResolve 授權問題 |Microsoft 文件"
description: "如何 tooidentify 並解決授權指派問題時您正在使用 Azure Active Directory 群組授權"
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
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ec9c74214a9e246f21fcf767b0bbd586ae702445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>識別及解決 Azure Active Directory 中群組的授權指派問題

群組為基礎授權 Azure Active Directory (Azure AD) 中引進使用者授權的錯誤狀態中的 hello 的概念。 在本文中，我們會說明為什麼使用者可能會結束此狀態中的 hello 原因。

當您將授權指派直接 tooindividual 使用者，而不需使用以群組為基礎的授權時，hello 分派作業可能會失敗。 例如，當您執行 hello PowerShell cmdlet`Set-MsolUserLicense`使用者，hello cmdlet 可以失敗的數目不相關的 toobusiness 邏輯的原因。 例如，可能會有授權或無法同時指派 hello 相同的兩個服務方案之間的衝突數目不足時間。 hello 報告的問題時立即回 tooyou。

當您使用以群組為基礎授權、 hello 可能會發生相同錯誤，但它們會在 hello 背景 hello Azure AD 服務會指派授權時。 基於這個理由，hello 錯誤無法立即被溝通的 tooyou。 相反地，它們是記錄在 hello 使用者物件上且然後經由 hello 系統管理網站回報。 請注意，hello 原始意圖 toolicense hello 使用者不會遺失，它會記錄在未來進行調查並解決錯誤狀態。

## <a name="how-toofind-license-assignment-errors"></a>如何 toofind 授權指派錯誤

1. 在特定群組中的錯誤狀態中，開啟 hello 刀鋒視窗中的 hello 群組 toofind 使用者。 [授權] 底下會有一份通知，顯示是否有任何使用者處於錯誤狀態。

![群組，錯誤通知](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. 按一下 hello 通知 tooopen 的所有受影響的使用者清單。 您可以個別按一下每個使用者 toosee 更多詳細資訊。

![群組，處於錯誤狀態的使用者清單](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. toofind 所有群組包含至少一個錯誤，在 hello **Azure Active Directory**刀鋒視窗選取**授權**然後**概觀**。 某些群組需要您注意時，會顯示資訊方塊。

![概觀，處於錯誤狀態的群組相關資訊](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. 按一下 hello 方塊 toosee 錯誤的所有群組的清單。 您可以按一下每個群組以取得詳細資訊。

![概觀，具有錯誤的群組清單](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


以下是每個潛在的問題和 hello 方式 tooresolve 描述它。

## <a name="not-enough-licenses"></a>沒有足夠的授權

**問題：**沒有足夠的可用授權的其中一個指定 hello 群組中的 hello 產品。 您需要 tooeither 購買更多授權 hello 的產品，或釋放未使用授權其他使用者或群組。

toosee 多少授權可用，請移過**Azure Active Directory** > **授權** > **所有產品**。

toosee 哪些使用者和群組會使用授權，按一下 [產品]。 在 [已授權的使用者] 底下，您會看到其授權已直接指派或透過一或多個群組指派的所有使用者。 在 [已授權的群組] 底下，您會看到已被指派該產品的所有群組。

**PowerShell：**PowerShell Cmdlet 會將此錯誤報告為 _CountViolation_。

## <a name="conflicting-service-plans"></a>衝突的服務方案

**問題：** hello 產品 hello 群組中所指定的其中一個包含已指派的 toohello 使用者透過不同的產品的另一個服務計劃與衝突的服務方案。 它們不能指派 toohello 的方式設定某些服務的方案相同的其他相關的服務方案的使用者。

請考慮下列範例中的 hello。 使用者有 Office 365 企業版授權**E1**直接指派給所有啟用的 hello 計劃。 新增 hello 使用者具有 Office 365 企業版的 hello tooa 群組**E3**產品指派 tooit。 本產品包含具有 hello 計劃包含在 E1、 hello 群組授權指派將失敗 hello 」 衝突服務計劃 」 錯誤，因此不能重疊的服務方案。 在此範例中，為 hello 衝突的服務方案：

-   SharePoint Online (方案 2) 與 SharePoint Online (方案 1) 衝突。
-   Exchange Online (方案 2) 與 Exchange Online (方案 1) 衝突。

toosolve 這項衝突，您需要 toodisable hello E1 上授權的直接指派的 toohello 使用者的兩個方案。 或者，您需要 toomodify hello 整個群組的授權指派，並停用 hello E3 授權中的 hello 計劃。 或者，您可能決定 tooremove hello E1 授權 hello 使用者如果備援 hello hello E3 授權內容中。

hello 決定如何 tooresolve 衝突產品授權一律屬於 toohello 系統管理員。 Azure AD 不會自動解決授權衝突。

**PowerShell：**PowerShell Cmdlet 會將此錯誤報告為 _MutuallyExclusiveViolation_。

## <a name="other-products-depend-on-this-license"></a>其他產品相依於此授權

**問題：** hello 產品 hello 群組中所指定的其中一個包含您必須啟用另一個服務計劃，另一個產品，函式中的服務方案。 Azure AD 嘗試 tooremove hello 基礎服務計劃時，就會發生此錯誤。 比方說，這種情形 hello 使用者正在從 hello 群組中移除。

toosolve 這個問題，您將需要 toomake 確定 toousers 透過其他方法，或 hello 相依服務已停用這些使用者仍指派該 hello 需要計劃。 執行這個動作之後, 可以正確 hello 群組授權移除這些使用者。

**PowerShell：**PowerShell Cmdlet 會將此錯誤報告為 _DependencyViolation_。

## <a name="usage-location-isnt-allowed"></a>不允許使用位置

**問題：**由於當地法律和法規，無法在所有位置使用某些 Microsoft 服務。 您可以指派授權 tooa 使用者之前，您必須為 hello 使用者 toospecify hello 「 使用量位置 」 屬性。 您可以在 hello**使用者** > **設定檔** > **設定**hello Azure 入口網站中的一節。

當 Azure AD 會嘗試 tooassign 群組授權 tooa 使用者的使用位置不受支援時，它將會失敗，而且這個 hello 使用者的錯誤記錄。

toosolve 這個問題，請從支援的位置，從 hello 授權群組移除使用者。 或者，如果 hello 目前使用量位置值不代表 hello 實際使用者的位置，您可以進行修改以便 hello 授權正確指派下一個階段 （如果支援 hello 新位置）。

**PowerShell：**PowerShell Cmdlet 會將此錯誤報告為 _ProhibitedInUsageLocationViolation_。

> [!NOTE]
> 當 Azure AD 會指派給群組授權時，指定使用位置沒有任何使用者都會繼承 hello hello 目錄位置。 我們建議系統管理員設定 hello 正確使用方式位置值上的使用者才能使用以群組為基礎的授權 toocomply 用戶所在地法律與規定。

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>當群組中有一個以上的產品授權時，會發生什麼事？

您可以指派多個產品授權 tooa 群組。 例如，您可以指派 Office 365 企業版 E3 與企業行動力 + 安全性 tooa 群組 tooeasily 啟用使用者的所有內含的服務。

Azure AD 會嘗試 tooassign hello 群組 tooeach 使用者中指定的所有授權。 如果 Azure AD 無法指定其中一個 hello 產品因為商務邏輯的問題 （例如，如果沒有足夠的授權，或與其他服務，在 hello 使用者上啟用衝突），它將不會指派 hello hello 群組中的其他授權其中一個。

您將會失敗，無法 tooget 指派的使用者可以 toosee hello 而且檢查哪些產品有已受此影響。

## <a name="license-assignment-fails-silently-for-a-user-due-tooduplicate-proxy-addresses-in-exchange-online"></a>由於 tooduplicate proxy 位址，在 Exchange Online 中的使用者以無訊息模式失敗授權指派

如果您使用 Exchange Online，您的租用戶中有些使用者可能設定不正確 hello 與相同的 proxy 位址值。 當以群組為基礎的授權伺服器嘗試 tooassign 授權 toosuch 使用者時，它將會失敗並不會記錄錯誤 (不同於在 hello 上面所述的其他錯誤情況)-這是在 hello 預覽版本，這項功能的限制，我們 tooaddress前面*一般可用性*。

> [!TIP]
> 如果您發現某些使用者未收到授權，且未對這些使用者記錄錯誤，請先檢查他們是否有重複的 Proxy 位址。
> 執行下列 PowerShell 指令程式針對 Exchange Online 的 hello 可以達成此目的：
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [這篇文章](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online)包含這個問題，請在包含資訊的更多詳細[如何使用遠端 PowerShell 線上 tooconnect tooExchange](https://technet.microsoft.com/library/jj984289.aspx)。

Proxy 位址的問題已解決的 hello 受影響的使用者之後，請確定 tooforce 授權處理 hello 群組 toomake 確定授權現在重新套用。

## <a name="how-do-you-force-license-processing-in-a-group-tooresolve-errors"></a>您要如何強制執行群組 tooresolve 錯誤處理授權？

取決於哪些步驟已取得 tooresolve 錯誤，可能需要 toomanually 觸發程序處理的群組 tooupdate hello 使用者狀態。

比方說，如果您釋放一些授權的移除使用者的直接授權指派，您必須 tootrigger 處理先前失敗 toofully 授權使用者的所有成員的群組。 toodo，尋找 hello 群組刀鋒視窗中，開啟**授權**，並選取 hello**重新處理**hello 工具列中的按鈕。

## <a name="next-steps"></a>後續步驟

toolearn 有關的授權管理群組，透過其他案例的詳細資訊，請參閱 hello 下列資訊：

* [Azure Active Directory 中指派的授權 tooa 群組](active-directory-licensing-group-assignment-azure-portal.md)
* [什麼是 Azure Active Directory 中以群組為基礎的授權？](active-directory-licensing-whatis-azure-portal.md)
* [如何 toomigrate 個別授權 toogroup 型授權 Azure Active Directory 中的使用者](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory 群組型授權其他案例 (英文)](active-directory-licensing-group-advanced.md)

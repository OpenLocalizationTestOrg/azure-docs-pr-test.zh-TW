---
title: "在 Azure Active Directory 群組個別的授權的使用者 tooa aaaHow toomigrate |Microsoft 文件"
description: "從個別使用者 tooswitch 授權 toogroup 授權使用 Azure Active Directory"
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
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a>Tooadd 如何授權 Azure Active Directory 中的授權使用者 tooa 群組

透過 「 直接指派 」; hello 組織中可能有現有的授權部署 toousers也就使用 PowerShell 指令碼或其他工具 tooassign 個別使用者授權。 如果您想要 toostart 您組織中使用以群組為基礎的授權 toomanage 授權，您必須移轉計劃 tooseamlessly 取代現有的解決方案以群組為基礎的授權。

請注意 hello 最重要事情 tookeep 是您應該避免在移轉 toogroup 為基礎的授權會導致使用者暫時遺失其目前指派的授權的情況。 移除授權可能會導致任何程序應該避免使用者存取 tooservices 和其資料會遺失 tooremove hello 風險。

## <a name="recommended-migration-process"></a>建議的移轉程序

1. 您有現有的自動化 (例如，PowerShell) 管理使用者的授權指派及移除。 保留它的執行原樣。

2. 建立新的授權群組 （或決定哪些現有群組 toouse），並確定所有必要的使用者會新增為成員。

3. 將所需的 hello 授權指派 toothose 群組;您的目標應該是 tooreflect hello 相同授權狀態您現有的自動化 (例如 PowerShell) 會套用 toothose 使用者。

4. 請確認使用權已經套用的 tooall 這些群組中的使用者。 作法是藉由檢查針對每個群組的 hello 處理狀態，以及檢查稽核記錄檔。

  - 您可以特別檢查個別使用者，方法是查看他們的授權詳細資料。 您會看到相同的授權指派給 「 直接 」 和 「 繼承 」 有 hello 的群組。

  - 您可以執行 PowerShell 指令碼太[確認授權如何指派 toousers](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses)。

  - 當 hello 相同產品的授權指派 toohello 使用者同時以直接或透過群組時，hello 使用者會耗用一個授權。 因此沒有額外的授權是必要的 tooperform 移轉。

5. 確認沒有授權指派失敗，方法是檢查每個群組中是否有使用者處於錯誤狀態。 如需詳細資訊，請參閱[識別及解決群組的授權問題](active-directory-licensing-group-problem-resolution-azure-portal.md)。

6. 請考慮移除 hello 原始直接設定;您可能會想 toodo 逐漸增加，在 「 波浪"toomonitor hello 先在使用者的子集上的結果。

  您可能會離開 hello 原始直接指派的使用者，但當 hello 使用者讓它們仍然保留其授權的群組 hello 原始授權，可能不想要。

## <a name="an-example"></a>範例

我們的組織有 1,000 位使用者。 所有使用者都需要 Enterprise Mobility + Security (EMS) 授權。 200 位使用者在 hello 財務部門中，但需要 Office 365 Enterprise E3 授權。 我們有內部部署執行中的 PowerShell 指令碼，在使用者就職和離職時新增及移除授權。 我們想要讓 Azure ad 授權會自動管理群組基礎授權的 tooreplace hello 指令碼。

以下是何種 hello 移轉程序可能看起來：

1. 使用 hello Azure 入口網站指派 hello EMS 授權 toohello**所有使用者**群組在 Azure AD 中。 指派 hello E3 授權 toohello**財務部門**包含 hello 所需的所有使用者的群組。

2. 對於每個群組，確認針對所有使用者已完成授權指派。 移 toohello 刀鋒視窗中的每個群組中，選取**授權**，並檢查 hello 處理狀態上方的 hello hello**授權**刀鋒視窗。

  - 尋找 「 最新的授權變更已套用的 tooall 使用者 」 tooconfirm 處理已完成。

  - 在最上層尋找任何使用者的授權可能尚未成功指派的相關通知。 我們對於某些使用者是否已用盡授權？ 某些使用者是否有衝突的授權 SKU，使其無法繼承群組授權？

3. 特別檢查有直接的 hello 和套用的群組授權某些使用者 tooverify。 移 toohello 刀鋒視窗中的使用者，則選取**授權**，以及檢查 hello 狀態的授權。

  - 這是預期的 hello 使用者狀態移轉期間：

      ![預期的使用者狀態](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  這可確認該 hello 使用者具有直接和繼承的授權。 我們看到同時指派 **EMS** 和 **E3**。

  - 選取 hello 啟用服務的相關的每個授權 tooshow 詳細資料。 如果直接 hello 和群組的授權啟用完全 hello hello 使用者相同的服務方案，這可能會使用的 toocheck。

      ![檢查服務方案](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. 在確認直接和群組授權是對等的之後，您可以開始從使用者移除直接授權。 您可以測試這種情況 hello 入口網站中的個別使用者移除它們，然後再執行自動化指令碼 toohave 大量加以移除。 以下是 hello 的範例與 hello 直接授權的同一個使用者透過 hello 入口網站來移除。 請注意 hello 授權狀態維持不變，但是我們不會再看見直接設定。

  ![直接授權已移除](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a>後續步驟

toolearn 深入了解其他透過群組，讀取授權管理案例

* [Azure Active Directory 中指派的授權 tooa 群組](active-directory-licensing-group-assignment-azure-portal.md)
* [什麼是 Azure Active Directory 中以群組為基礎的授權？](active-directory-licensing-whatis-azure-portal.md)
* [識別及解決 Azure Active Directory 中群組的授權問題](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Azure Active Directory 群組型授權其他案例](active-directory-licensing-group-advanced.md)

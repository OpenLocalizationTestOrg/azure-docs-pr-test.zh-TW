---
title: "Azure AD Connect︰當您已經有 Azure AD 時 | Microsoft Docs"
description: "本主題描述如何 toouse 連接時您有現有的 Azure AD 租用戶。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f7b166e9e85c1f03330e8e0074d4afa4036738c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-when-you-have-an-existent-tenant"></a>Azure AD Connect︰當您有存在的租用戶
大部分的 hello 主題 toouse Azure AD Connect 如何假設您開始使用新的 Azure AD 租用戶，並確認沒有任何使用者或有其他物件。 但如果您已經啟動的 Azure AD 租用戶中，填入使用者和其他物件，而想 toouse 連接，則本主題是供您。

## <a name="hello-basics"></a>hello 基本概念
Azure AD 中的物件可能是受控制 hello 雲端 (Azure AD) 或內部部署中。 針對一個單一物件，您無法管理內部部署的某些屬性和 Azure AD 中的一些其他屬性。 每個物件都有旗標，表示受到 hello 物件。

您可以管理有些使用者在內部部署及其他 hello 雲端中。 混合著會計工作者和銷售工作者的組織是此組態的常見案例。 hello 會計工作者已在內部 AD 帳戶，但 hello 銷售背景工作，請他們有 Azure AD 的帳戶。 您可在內部部署管理部分使用者，並在 Azure AD 管理其他使用者。

如果您啟動 toomanage 使用者在 Azure AD 也會在內部部署 AD，稍後想 toouse 連接，則您需要 tooconsider 一些其他考量。

## <a name="sync-with-existing-users-in-azure-ad"></a>在 Azure AD 中與現有的使用者同步處理
當您安裝 Azure AD Connect，您啟動同步處理時 hello （在 Azure AD) 中的 Azure AD 同步處理服務不在每個新的物件上執行檢查然後再次嘗試 toofind 現有的物件 toomatch。 有三種屬性用於此處理程序︰**userPrincipalName**、**proxyAddresses** 和 **sourceAnchor**/**immutableID**。 比對 **userPrincipalName** 和 **proxyAddresses** 稱為**大致比對**。 比對 **sourceAnchor** 稱為**精確比對**。 Hello **proxyAddresses**屬性只與 hello 值**SMTP:**的 hello 主要電子郵件地址，用於評估 hello。

hello 相符項目只會評估來自連接的新物件。 如果您變更現有的物件，而它會比對任何這些屬性，則您會看到錯誤。

如果 Azure AD 會尋找的物件是 hello 屬性值 hello 相同物件即將從連接，它已存在於在 Azure AD 中則 hello Azure AD 中的物件接手連接。 hello 先前雲端管理的物件標示為在內部部署管理。 所有屬性值在內部部署的 Azure AD 中 AD 會使用覆寫 hello 內部值。 當屬性擁有 hello 例外狀況**NULL**值在內部部署。 在此情況下，hello 值儲存在 Azure AD 還會保留，但是仍然只能變更它在內部部署 toosomething 其他。

> [!WARNING]
> Azure AD 中的所有屬性會成為 toobe hello 內部值來覆寫，請確定您有良好的資料在內部。 例如，如果您只在 Office 365 中管理電子郵件地址，且不會在內部部署 AD DS 中保持更新，則您會遺失不存在於 AD DS 之 Azure AD/Office 365 中的任何值。

> [!IMPORTANT]
> 如果您使用密碼同步處理，一律會使用快速設定，則在 Azure AD 中的 hello 密碼會以內部部署中的 hello 密碼覆寫 AD。 如果您的使用者是使用的 toomanage 不同的密碼，則您需要 tooinform 它們他們應該使用 hello 在內部部署密碼，當您安裝連接。

必須在您規劃考量 hello 上一節和警告。 如果您不會反映在 Azure AD 中所做的許多變更內部部署 AD DS 中，則您需要 tooplan 同步您的物件，使用 Azure AD Connect 之前 toopopulate AD DS 以 hello 更新值的方式。

如果您符合軟體對您物件，然後 hello **sourceAnchor**會在 Azure AD 中加入 toohello 物件，所以稍後可以使用固定的相符項目。

### <a name="hard-match-vs-soft-match"></a>精確比對與大致比對
對於 Connect 的全新安裝，精確比對與大致比對之間並無實際差別。 hello 差異是在災害復原情況下。 如果遺失您的伺服器與 Azure AD Connect，您可以重新安裝新的執行個體而不會遺失任何資料。 初始安裝期間傳送 tooConnect sourceAnchor 的物件。 hello 相符項目可以再來評估 hello 用戶端 (Azure AD Connect)，也就是許多較快，但這麼做 hello 相同 Azure AD 中。 精確比對會由 Connect 和 Azure AD 評估。 大致比對只會由 Azure AD 評估。

### <a name="other-objects-than-users"></a>使用者以外的其他物件
使用者通常會有 userPrincipalName 和 proxyAddresses，如此可輕鬆 hello 相符項目。 但是其他物件 (例如安全性群組) 沒有這些。 在此情況下，您可以只比對上使用 hello sourceAnchor 的硬碟相符項。 hello sourceAnchor 一律為 Base64 轉換的 hello **objectGUID**內部，所以您必須更新 hello 值，當您需要兩個物件 toomatch 的 Azure AD 中。 hello sourceAnchor/immutableID 只能使用 PowerShell，而不是透過 hello 入口網站更新。

## <a name="create-a-new-on-premises-active-directory-from-data-in-azure-ad"></a>從 Azure AD 中的資料建立新的內部部署 Active Directory
有些客戶開始使用僅限雲端的解決方案與 Azure AD，且他們沒有內部部署 AD。 稍後要 tooconsume 在內部部署資源和想 toobuild 內部 AD 為基礎的 Azure AD 資料。 Azure AD Connect 無法針對此案例協助您。 不會建立使用者內部部署和它並沒有任何能力 tooset hello 密碼在內部部署 toohello 相同，如 Azure AD 所示。

如果 hello 的唯一理由為何您計劃 tooadd 內部部署 AD toosupport Lob （特定業務應用程式），則也許您應該考慮 toouse [Azure AD 網域服務](../../active-directory-domain-services/index.md)改為。

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

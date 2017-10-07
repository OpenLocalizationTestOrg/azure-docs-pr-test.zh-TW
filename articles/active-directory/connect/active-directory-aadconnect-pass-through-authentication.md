---
title: "Azure AD Connect：傳遞驗證 | Microsoft Docs"
description: "這篇文章說明 Azure Active Directory (Azure AD) 傳遞驗證，以及它如何向內部部署 Active Directory 驗證使用者的密碼以允許 Azure AD 登入。"
services: active-directory
keywords: "什麼是 Azure AD Connect 傳遞驗證、安裝 Active Directory，以及 Azure AD、SSO、單一登入的必要元件"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 56cfb2c4f4afc7d46c926a392ae6ec01e96224d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a>使用 Azure Active Directory 傳遞驗證來進行使用者登入

## <a name="what-is-azure-active-directory-pass-through-authentication"></a>什麼是 Azure Active Directory 傳遞驗證？

Azure Active Directory (Azure AD) 通過驗證可讓使用者 toosign tooboth 內部和雲端型應用程式使用 hello 相同密碼。 這項功能提供您的使用者更好的體驗-一個較少的密碼 tooremember，並減少 IT 技術服務人員成本，因為使用者比較不可能 tooforget 如何 toosign 中的。 當使用者使用 Azure AD 登入時，此功能會向您的內部部署 Active Directory 直接驗證使用者的密碼。

這項功能是替代太[Azure AD 密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)，這樣會提供 hello 雲端驗證 tooorganizations 相同的優點。 不過，某些組織中的安全性與相容性原則不允許這些組織 toosend 使用者的密碼，即使在雜湊的形式中，其內部的界限之外。 Hello 解決方案這類組織通過驗證。

![Azure AD 傳遞驗證](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

您可以結合通過驗證的 hello[無接縫單一登入](active-directory-aadconnect-sso.md)功能。 如此一來，當您的使用者存取您公司網路內部其公司電腦上的應用程式時，它們不需要在其密碼 toosign 中的 tootype。

>[!IMPORTANT]
>Azure AD 傳遞驗證目前為預覽功能。

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a>使用 Azure AD 傳遞驗證的主要好處

- 良好的使用者體驗
  - 使用者使用 hello 同時在內部部署和雲端型應用程式的相同密碼 toosign。
  - 使用者耗費較少的時間與對話 toohello IT 技術服務人員解決密碼相關的問題。
  - 使用者可以完成[自助密碼管理](../active-directory-passwords-overview.md)hello 雲端中的工作。
- *輕鬆 toodeploy （& s) 管理*
  - 不必再進行複雜的內部部署或網路設定。
  - 需要只輕量型的代理程式 toobe 安裝在內部部署。
  - 沒有任何額外的管理負荷。 hello 代理程式會自動收到改進和 bug 修正。
- *安全*
  - 以任何形式的 hello 雲端中永遠不會儲存在內部部署密碼。
  - hello 代理程式只會從您的網路內的傳出連接。 因此，在周邊網路中，也稱為 DMZ 沒有需求 tooinstall hello 代理程式。
  - 與 [Azure AD 條件式存取原則](../active-directory-conditional-access-azure-portal.md) (包括 Multi-Factor Authentication (MFA)) 緊密配合，並[篩除暴力密碼破解攻擊](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)，藉此保護您的使用者帳戶。
- *高可用性*
  - 其他代理程式可以安裝在多個內部部署伺服器 tooprovide 高可用性的登入要求。

## <a name="feature-highlights"></a>功能要點

- 可讓使用者登入到使用[新式驗證](https://aka.ms/modernauthga)的所有 Web 瀏覽器型應用程式和 Microsoft Office 用戶端應用程式。
- 登入使用者名稱可以是任一個 hello 內部預設使用者名稱 (`userPrincipalName`) 或在 Azure AD Connect 中設定的另一個屬性 (又稱為`Alternate ID`)。
- hello 功能可以順暢地與[條件式存取](../active-directory-conditional-access.md)功能，例如 Multi-factor Authentication (MFA) toohelp 保護您的使用者。
- 如果 AD 樹系之間有樹系信任且名稱尾碼路由已正確設定，就支援多樹系環境。
- 這是可用的功能，而且不需要任何付費的版本的 Azure AD toouse 它。
- 您可以透過 [Azure AD Connect](active-directory-aadconnect.md) 啟用它。
- 它會使用輕量型在內部部署代理程式會接聽並回應 toopassword 驗證要求。
- 安裝多個代理程式就能提供高可用性的登入要求。
- 它[保護](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)暴力密碼破解針對您在內部部署帳戶強制執行密碼破解攻擊 hello 雲端中的。

## <a name="next-steps"></a>後續步驟

- [**快速入門**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - 開始使用 Azure AD 傳遞驗證。
- [**目前的限制**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 此功能目前為預覽狀態。 了解支援的情節和不支援的情節。
- [**技術性深入探討**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 了解這項功能的運作方式。
- [**常見問題集**](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 常見問題的答案。
- [**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -了解如何 tooresolve 常見問題與 hello 功能。
- [**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。

---
title: "Azure AD Connect：傳遞驗證 - 運作方式 | Microsoft Docs"
description: "本文描述 Azure Active Directory 傳遞驗證運作方式。"
services: active-directory
keywords: "Azure AD Connect 傳遞驗證, 安裝 Active Directory, Azure AD 的必要元件, SSO, 單一登入"
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
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a>Azure Active Directory 傳遞驗證：技術深入探討

>[!IMPORTANT]
>Azure AD 傳遞驗證目前為預覽功能。 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a>Azure Active Directory 傳遞驗證運作方式

在使用者嘗試 toosign 到 Azure Active directory (Azure AD)，保護應用程式，而且如果 hello 租用戶，啟用傳遞驗證 hello 時就會發生下列步驟：

1. hello 的使用者嘗試 tooaccess 應用程式 (例如 hello Outlook Web 應用程式-https://outlook.office365.com/owa/)。
2. Hello 使用者沒有已登入，hello 使用者登入頁面重新導向的 toohello Azure AD。
3. hello 使用者 hello Azure AD 登入頁面中輸入使用者名稱和密碼，然後按一下 hello 「 登入 」 按鈕。
4. 收到 hello 登入要求的 azure AD 會將 hello 使用者名稱和密碼 （加密使用公開金鑰） 放在佇列上。
5. 在內部部署的傳遞驗證代理程式可讓輸出呼叫 toohello 佇列，並擷取 hello 使用者名稱和加密的密碼。
6. hello 代理程式會使用其私密金鑰的 hello 密碼解密。
7. hello 代理程式接著會驗證 hello 使用者名稱和密碼，對使用標準 Windows Api （類似的機制 toowhat 由 Active Directory Federation Services） 的 Active Directory。 hello 使用者名稱可以是任一個 hello 內部預設使用者名稱 (通常`userPrincipalName`) 或在 Azure AD Connect 中設定的另一個屬性 (又稱為`Alternate ID`)。
8. hello 在內部部署 Active Directory 網域控制站 (DC) 然後評估 hello 要求並傳回 hello 適當的回應 (成功、 失敗，密碼過期或鎖定使用者) toohello 代理程式。
9. hello 代理程式，接著，會傳回此回應後 tooAzure AD。
10. Azure AD 評估 hello 回應及回應視 toohello 使用者-例如，它立即 hello 使用者登入或要求的多重要素驗證 (MFA)。
11. Hello 使用者登入成功時，hello 使用者能 tooaccess hello 應用程式。

hello 下列圖表說明所有 hello 元件和 hello 所需的步驟。

![傳遞驗證](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a>後續步驟
- [**目前的限制**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 此功能目前為預覽狀態。 了解支援的情節和不支援的情節。
- [**快速入門**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - 開始使用 Azure AD 傳遞驗證。
- [**常見問題集**](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 常見問題的答案。
- [**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -了解如何 tooresolve 常見問題與 hello 功能。
- [**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。

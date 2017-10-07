---
title: "Azure AD Connect：無縫單一登入 - 運作方式 | Microsoft Docs"
description: "本文說明 hello Azure Active Directory 無接縫單一登入功能的運作方式。"
services: active-directory
keywords: "何謂 Azure AD Connect、安裝 Active Directory、Azure AD、SSO、單一登入的必要元件"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a>Azure Active Directory 無縫單一登入：技術性深入探討

這篇文章提供您的技術詳細資料進入 hello Azure Active Directory 無接縫單一登入 (無縫式 SSO) 功能的運作方式。

>[!IMPORTANT]
>hello 無縫式 SSO 的功能目前為預覽狀態。

## <a name="how-does-seamless-sso-work"></a>順暢 SSO 如何運作？

本節提供的兩個部分 tooit:
1. hello hello 無縫式 SSO 功能的安裝程式。
2. 單一使用者登入交易如何與無縫 SSO 搭配運作。

### <a name="how-does-set-up-work"></a>設定如何運作？

無縫 SSO 是使用 Azure AD Connect 所啟用，如[這裏](active-directory-aadconnect-sso-quick-start.md)所示。 同時也可讓 hello 功能，就會發生 hello 下列步驟：
- 名為 `AZUREADSSOACCT` 的電腦帳戶 (代表 Azure AD) 是在您的內部部署 Active Directory (AD) 中建立。
- Azure AD 與安全地共用 hello 電腦帳戶的 Kerberos 解密金鑰。
- 此外，兩個 Kerberos 服務主要名稱 (Spn) 會建立 toorepresent Azure AD 登入期間所使用的兩個 Url。

>[!NOTE]
> 在每個 AD 樹系中建立 hello 電腦帳戶和 hello Kerberos Spn tooAzure AD 同步處理 （使用 Azure AD Connect），而且您想在其使用者的無縫式 SSO。 移動 hello`AZUREADSSOACCT`電腦帳戶 tooan 組織單位 (OU) 中其他電腦帳戶的管理中的預存的 tooensure hello 相同的方式並不會刪除。

>[!IMPORTANT]
>我們強烈建議您使用您[變換 hello Kerberos 解密金鑰](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account)的 hello`AZUREADSSOACCT`至少每隔 30 天內的電腦帳戶。

### <a name="how-does-sign-in-with-seamless-sso-work"></a>使用無縫 SSO 登入的運作方式？

Hello 安裝完成之後，無縫式 SSO 的運作方式相同方式與任何其他登入使用整合式 Windows 驗證 (IWA) 的 hello。 hello 流程如下所示：

1. hello 的使用者嘗試 tooaccess 應用程式 (例如 hello Outlook Web 應用程式-https://outlook.office365.com/owa/) 從公司網路內，已加入網域的公司裝置。
2. Hello 使用者沒有已登入，hello 使用者登入頁面重新導向的 toohello Azure AD。

  >[!NOTE]
  >如果 hello Azure AD 登入要求中包含`domain_hint`識別您租用戶-例如 (contoso.onmicrosoft.com） 或`login_hint`(hello 使用者-例如，用來識別user@contoso.onmicrosoft.com或user@contoso.com) 參數，則步驟 2 則會略過。

3. hello hello Azure AD 登入頁面使用者名稱中的使用者類型。
4. Azure AD 挑戰 hello 瀏覽器，透過 401 未授權回應，tooprovide hello 背景中使用 JavaScript，Kerberos 票證。
5. hello 瀏覽器中，依次要求票證從 Active Directory hello`AZUREADSSOACCT`電腦帳戶 （這表示 Azure AD）。
6. Active Directory 找出 hello 電腦帳戶，並傳回 hello 電腦帳戶的密碼以加密的 Kerberos 票證 toohello 瀏覽器。
7. hello 瀏覽器會轉送它從 Active Directory tooAzure AD 取得 hello Kerberos 票證 (上一個 hello [Azure AD Url 先前加入 toohello 瀏覽器的內部網路區域設定](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature))。
8. Azure AD 解密 hello Kerberos 票證，其中包括 hello 使用者登入 hello 公司裝置 hello 身分識別，先前使用 hello 共用金鑰。
9. 評估後，Azure AD 傳回的語彙基元後 toohello 應用程式或詢問 hello 使用者 tooperform 其他概念證明，例如 Multi-factor Authentication。
10. Hello 使用者登入成功時，hello 使用者能 tooaccess hello 應用程式。

hello 下列圖表說明所有 hello 元件和 hello 所需的步驟。

![順暢單一登入](./media/active-directory-aadconnect-sso/sso2.png)

無縫式 SSO 是隨機的這表示如果失敗，hello 登入體驗會回復 tooits 一般行為-也就是，hello 使用者需要 tooenter 中的其密碼 toosign。

## <a name="next-steps"></a>後續步驟

- [**快速入門**](active-directory-aadconnect-sso-quick-start.md) - 開始使用 Azure AD 無縫 SSO。
- [**常見問題集**](active-directory-aadconnect-sso-faq.md) -toofrequently 常見問題的答案。
- [**疑難排解**](active-directory-aadconnect-troubleshoot-sso.md) -了解如何 tooresolve 常見問題與 hello 功能。
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。

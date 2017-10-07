---
title: "在 Azure AD 中的特殊權限存取 aaaSecuring |Microsoft 文件"
description: "說明 hello 之主題的方法來保護跨 Azure、 Azure Active Directory 和 Microsoft Online Services 的特殊的存取權限。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a>保護 Azure AD 中的特殊權限存取
安全性權限存取很重要的第一個步驟 toohelp 保護現代的組織中的企業資產。 特殊權限帳戶是可管理 IT 系統的帳戶。 這些帳戶 toogain 存取 tooan 組織的資料和系統是攻擊者為目標。 toosecure 特殊權限存取，您應該隔離 hello 帳戶並從的 hello 風險的系統暴露 tooa 惡意使用者。

更多使用者開始透過雲端服務的 tooget 特殊權限存取。 這包括 Office365 的全域系統管理員、Azure 訂用帳戶系統管理員和有 VM 或 SaaS 應用程式系統管理存取權限的使用者。

Microsoft 建議您遵循 [Securing Privileged Access (保護特殊權限存取)](https://technet.microsoft.com/library/mt631194.aspx)的這份藍圖。

這些原則是否適用使用 Azure Active Directory、Office 365 或其他 Microsoft 服務和應用程式的客戶，取決於使用者帳戶是由 Active Directory 管理驗證，或在 Azure Active Directory 中管理驗證。 hello 下列各節提供詳細資訊在 Azure AD 功能 toosupport 保護特殊權限的存取。

## <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication
系統管理員驗證 tooincrease hello 安全性，您應該需要雙步驟驗證，才能授與權限。 兩步驟驗證是確認您是誰的方法需要 hello 使用不只是使用者名稱和密碼。 它提供安全性 toouser 登入和交易的第二層。

Azure Multi-factor Authentication (MFA) 是 Microsoft 的兩步驟驗證解決方案，可協助保護存取 toodata 和應用程式同時滿足簡單登入程序的使用者需求。 透過一系列簡單的驗證選項提供增強式驗證，選項包括：

- 電話通話
- 文字訊息
- 行動應用程式通知
- 行動應用程式驗證碼
- 協力廠商 OATH 權杖

Azure Multi-factor Authentication 的運作方式的概觀，請參閱下列視訊 hello:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

如需詳細資訊，請參閱 [MFA for Office 365 和 MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/)。

## <a name="time-bound-privileges"></a>時間界限權限
某些組織可能會發現它們有太多擁有高權限角色的使用者。 使用者可能已加入 toohello 角色特定的活動，例如 toosign 註冊服務，但沒有常之後使用這些權限。

權限 toolower hello 曝光時間並增加您掌握用法，限制使用者 tooonly 採用其權限 「 及時 」 (JIT)，在需要 tooperform 工作時。 Azure Active Directory 與 Microsoft Online Services 可以使用 [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM)。

![PIM 儀表板][2]

## <a name="attack-detection"></a>攻擊偵測
[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) 提供整合的檢視，綜觀會影響組織身分識別的風險事件和潛在弱點。 根據風險事件，Identity Protection 會計算每位使用者的使用者風險層級，讓您 tooconfigure 風險為基礎的原則保護 tooautomatically hello 您組織的身分識別。 這些原則，以及其他 Azure Active Directory 和 EMS，所提供的條件式存取控制項可以自動封鎖 hello 使用者，或提供建議，包括密碼重設以及強制多因素驗證。

![Azure AD Identity Protection][3]

## <a name="conditional-access"></a>條件式存取
條件式存取控制與 Azure Active Directory 檢查 hello 時允許存取 tooan 應用程式之前驗證使用者，您所選擇的特定條件。 一旦符合這些條件，hello 使用者已驗證，而且允許存取 toohello 應用程式。

![使用 MFA 設定條件式存取規則][4]

## <a name="related-articles"></a>相關文章
* 啟用 [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* 啟用 [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)
* 啟用 [Azure AD Identity Protection](../active-directory-identityprotection.md)
* 啟用[條件式存取控制](../active-directory-conditional-access.md)

如需有關如何建置完整的安全性藍圖的詳細資訊，請參閱 hello < 客戶責任和藍圖 > 一節 hello[企業架構設計人員的 Microsoft Cloud Security](http://aka.ms/securecustomer)文件。 如需參與 Microsoft 服務 tooassist 與任何這些主題的詳細資訊，請連絡您的 Microsoft 代表或瀏覽我們[顧慮解決方案頁面](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)。

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png

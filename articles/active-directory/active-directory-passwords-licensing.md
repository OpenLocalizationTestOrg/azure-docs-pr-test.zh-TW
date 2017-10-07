---
title: "授權︰Azure AD SSPR | Microsoft Docs"
description: "Azure AD 自助式密碼重設授權需求"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a>Azure AD 自助式密碼重設的授權需求

Azure AD 密碼重設 toofunction，讓您**必須至少一個組織中指派的授權**。 我們不會強制執行每個使用者授權 hello 密碼重設的經驗。 toomaintain 符合您的 Microsoft 授權合約，您必須使用 premium 功能 tooassign 授權 tooany 使用者。

* **僅限雲端使用者** - Office 365 (O365) 任何付費的 SKU，或 Azure AD Basic
* **雲端**及/或**內部部署使用者** - Azure AD Premium P1 或 P2、Enterprise Mobility + Security (EMS) 或 Secure Productive Enterprise (SPE)

## <a name="licenses-required-for-password-writeback"></a>密碼回寫所需的授權

toouse 密碼回寫，您必須有一個 hello 遵循您的租用戶中指派的授權。

* Azure AD Premium P1
* Azure AD Premium P2
* Enterprise Mobility + Security E3
* Enterprise Mobility + Security E5
* Secure Productive Enterprise E3
* Secure Productive Enterprise E5

> [!NOTE]
> 獨立 Office 365 授權計劃**不支援密碼回寫**和需要 hello 前的此功能 toowork 計劃的其中一個。

Hello 遵循頁面上可以找到額外的授權資訊，包括成本

* [Azure Active Directory 價格網站](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a>啟用以群組或使用者為基礎的授權

Azure AD 現在支援群組為基礎授權允許系統管理員 tooassign 授權大量 tooa 使用者群組，而不是將指派一次。 [指派、驗證授權及解決其問題](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

並非所有位置都可使用某些 Microsoft 服務。 Tooa 使用者可以指派授權之前，hello 系統管理員必須 hello 使用者指定 hello 「 使用量位置 」 屬性。 指派的授權，才可以在 使用者 > 設定檔 > hello Azure 入口網站中的設定一節。 **當使用群組授權指派，請指定使用位置沒有任何使用者都會繼承 hello hello 目錄位置。**

## <a name="next-steps"></a>後續步驟

hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊

* [**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理 
* [**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理
* [**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱
* [**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。
* [**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能
* [**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式
* [**常見問題集**](active-directory-passwords-faq.md) - 如何？ 原因為何？ 何事？ 何地？ 何人？ 何時？ -回答您總是想 tooask tooquestions
* [**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR


---
title: "使用 Azure AD 的 aaaSharing 帳戶 |Microsoft 文件"
description: "描述 Azure Active Directory 如何讓組織 toosecurely 共用帳戶在內部部署應用程式和取用者雲端服務。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 9f98bfa97a6c9ba1566d3f921c1b676d5f3c2a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sharing-accounts-with-azure-ad"></a>使用 Azure AD 共用帳戶
## <a name="overview"></a>概觀
有時候組織需要多人 toouse 單一使用者名稱和密碼。 這通常發生在兩個情況下：

* 每個使用者必須使用唯一的登入和密碼存取應用程式時 (無論是內部部署的應用程式或取用者雲端服務，例如公司的社交媒體帳戶)。
* 建立多個使用者環境時。 您可能需要一個單一的本機帳戶，具有更高的權限，而且可以是使用的 toodo 核心安裝、 管理和復原活動 （例如 hello 本機 「 全域系統管理員 」 帳戶在 Salesforce 中的 Office 365 或 hello 根帳戶）。

傳統上，這些帳戶會共用由散發 hello 認證 （使用者名稱/密碼） toohello 恰當的人員或將其儲存在多個信任的代理程式可以存取它們的共用位置。

hello 傳統共用模型有幾個缺點：

* 啟用存取 toonew 應用程式，需要在需要存取的 toodistribute 認證 tooeveryone。
* 每個共用的應用程式可能需要它自己組唯一的共用的認證，需要使用者 tooremember 多組認證。 當使用者擁有 tooremember 許多的認證時，hello 風險會增加他們將採用 toorisky 作法。 (例如寫下密碼。)
* 您無法分辨誰存取 tooan 應用程式。
* 您不知道誰 *存取* 了應用程式。
* 當您需要 tooremove 存取 tooan 應用程式時，您擁有 tooupdate hello 認證，並且將它們重新發佈 tooeveryone 需要存取 toothat 應用程式。

## <a name="azure-active-directory-account-sharing"></a>Azure Active Directory 帳戶共用
Azure AD 提供的新方法可消除這些缺點 toousing 共用帳戶。

hello Azure AD 系統管理員所設定的使用者可以存取使用 hello 存取面板，然後選擇 單一登入該應用程式最適合的 hello 類型的應用程式。 其中一種類型，*密碼型單一登入*，可讓 Azure AD 做為類型的"broker"hello 登入程序期間，應用程式。

使用者使用他們的組織帳戶登入一次。 這是 hello 他們經常使用 tooaccess，其桌上型電腦或電子郵件的相同帳戶。 他們只能探索和存取指派給他們的那些應用程式。 使用共用帳戶，這份應用程式清單可以包含任何數目的共用認證。 hello 終端使用者不需要 tooremember 或寫下 hello 各種可能使用的帳戶。

共用帳戶不只增加監督的方便性和改善可用性，也可增強安全性。 具有權限 toouse hello 認證的使用者看 hello 共用的密碼，但而取得的權限 toouse hello 密碼當做驗證協調的流程的一部分。 此外，某些密碼 SSO 應用程式中，您擁有 hello 選項 toohave Azure AD 定期變換 （更新） hello 密碼使用大型、 複雜密碼，增加 hello 帳戶安全性。 hello 系統管理員可以輕鬆地授與或撤銷存取 tooan 應用程式，也知道誰有存取 toohello 帳戶，以及誰在存取它在過去的 hello。

Azure AD 支援的共用帳戶適用於任何Enterprise Mobility Suite (EMS)、進階或基本型的授權使用者，含括所有類型的密碼單一登入應用程式。 您可以共用任何數千種預先整合的應用程式在 hello 應用程式庫中的帳戶，並可以加入自己的密碼驗證的應用程式與[自訂 SSO 應用程式](active-directory-sso-integrate-saas-apps.md)。

啟用帳戶共用的 Azure AD 功能包括：

* [密碼單一登入](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* 密碼單一登入代理程式
* [群組指派](active-directory-accessmanagement-self-service-group-management.md)
* 自訂密碼應用程式
* [應用程式使用量儀表板/報告](active-directory-passwords-get-insights.md)
* 使用者存取入口網站
* [應用程式 proxy](active-directory-application-proxy-get-started.md)
* [Active Directory 市集](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a>共用帳戶
Azure AD toouse tooshare 帳戶您必須：

* 新增應用程式[應用程式庫](https://azure.microsoft.com/marketplace/active-directory/)或[自訂應用程式](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)
* 設定密碼單一登入 (SSO) 的 hello 應用程式
* 使用[群組為基礎的指派](active-directory-accessmanagement-group-saasapps.md)和選取 hello 選項 tooenter 共用的認證
* 選擇性： 在某些應用程式，例如 Facebook、 Twitter 或 LinkedIn，您可以啟用 hello 選項[Azure AD 自動密碼變換](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)

您也可以讓您共用的帳戶更安全的多重要素驗證 (MFA) (深入了解[保護應用程式與 Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md))，您可以將委派 hello 能力 toomanage 擁有存取 toohello 應用程式使用[Azure AD 自助式](active-directory-accessmanagement-self-service-group-management.md)群組管理。

## <a name="related-articles"></a>相關文章
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [使用條件式存取來保護應用程式](active-directory-conditional-access.md)
* [自助式群組管理/SSAA](active-directory-accessmanagement-self-service-group-management.md)


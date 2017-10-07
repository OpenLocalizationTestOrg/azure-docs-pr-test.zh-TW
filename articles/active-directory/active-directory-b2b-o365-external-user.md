---
title: "aaaOffice 365 外部共用和 Azure Active Directory B2B 共同作業 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業的宣告對應參考資料"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a>Office 365 外部共用與 Azure Active Directory B2B 共同作業

在 Office 365 （OneDrive，SharePoint Online、 統一群組等） 和 Azure Active Directory (Azure AD) B2B 共同作業技術上來說是共用的外部 hello 相同的動作。 所有外部共用 （除了 OneDrive/SharePoint Online)，包括客體中的 Office 365 群組，已使用共用的 hello Azure AD B2B 共同作業邀請應用程式開發介面。

OneDrive/SharePoint Online 有個別的邀請管理員。 OneDrive/SharePoint Online 中的外部共用支援會在 Azure AD 開發其支援之前開始。 經過一段時間，OneDrive/SharePoint Online 的外部共用具有累加的數種功能，並使用 hello 產品的使用者數以百萬計的內建共用模式。 不過，OneDrive/SharePoint Online 外部共用的運作方式與 Azure AD B2B 共同作業的運作方式有些微差異：

- 之後使用者擁有兌換邀請其 OneDrive/SharePoint Online 將使用者 toohello 目錄。 因此前兌換，, 您沒有看到 Azure AD 入口網站中的 hello 使用者。 如果另一個站台同時邀請 hello 中的使用者，就會產生新的邀請。 不過，當您使用 Azure AD B2B 共同作業時，使用者會立即新增於邀請上，因而顯示在每個地方。

- 在 OneDrive/SharePoint Online 中的 hello 兌換體驗看起來 hello Azure AD B2B 共同作業經驗與不同的。 使用者贖回邀請之後，hello 體驗看起來一樣。

- 您可以從 OneDrive/SharePoint Online 共用對話方塊挑選 Azure AD B2B 共同作業邀請的使用者。 在 OneDrive/SharePoint 邀請的使用者兌換其邀請之後，也會出現在 Azure AD 中。

- 外部 toomanage 中 OneDrive/SharePoint Online 與 Azure AD B2B 共同作業的共用設定 hello OneDrive/SharePoint Online 外部共用設定太**只允許與外部使用者已經共用 hello 目錄中**。 使用者可以前往 tooexternally 共用站台，並且加入從外部共同作業者 hello 系統管理員挑選。 hello 系統管理員可以新增 hello 透過 hello B2B 共同作業邀請應用程式開發介面的外部共同作業者。

![hello OneDrive/SharePoint Online 外部共用設定](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 共同作業使用者屬性](active-directory-b2b-user-properties.md)
* [新增 B2B 共同作業使用者 tooa 角色](active-directory-b2b-add-guest-to-role.md)
* [委派 B2B 共同作業邀請](active-directory-b2b-delegate-invitations.md)
* [動態群組與 B2B 共同作業](active-directory-b2b-dynamic-groups.md)
* [B2B 共同作業程式碼與 PowerShell 範例](active-directory-b2b-code-samples.md)
* [設定適用於 B2B 共同作業的 SaaS 應用程式](active-directory-b2b-configure-saas-apps.md)
* [B2B 共同作業使用者權杖](active-directory-b2b-user-token.md)
* [B2B 共同作業使用者宣告對應](active-directory-b2b-claims-mapping.md)
* [B2B 共同作業目前的限制](active-directory-b2b-current-limitations.md)

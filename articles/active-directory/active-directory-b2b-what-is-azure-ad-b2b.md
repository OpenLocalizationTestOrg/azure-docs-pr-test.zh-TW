---
title: "aaaWhat 是 Azure Active Directory B2B 共同作業？ | Microsoft Docs"
description: "Azure Active Directory B2B 共同作業，讓商務夥伴 tooselectively 存取您公司應用程式，支援跨公司關聯性。"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: 359989b66f3d012c306e8748a607662fffacb919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a>什麼是 Azure AD B2B 共同作業？

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

Azure AD 企業對企業 (B2B) 共同作業功能啟用安全地使用 Azure AD toowork 使用者從任何其他組織，小型或大型的任何組織。 這些組織可以有或沒有 Azure AD，或甚至可以有或沒有 IT 組織。 

使用 Azure AD 的組織可以提供存取 tootheir 夥伴 toodocuments、 資源和應用程式，同時維護自己的公司資料的完整控制權。 開發人員可以使用 hello Azure AD 企業對企業應用程式開發介面 toowrite 應用程式，將兩個組織在一起更安全的方式。 此外，也是很方便使用者 toonavigate。

我們的客戶 97%有告訴我們 Azure AD B2B 共同作業是非常重要的 toothem。

![圓形圖](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

截至 2017 年 4 月初為止，我們有大約三百萬個使用者已經使用 Azure AD B2B 共同作業功能。 而有超過 23% 有 10 個使用者以上的 Azure AD 組織已經從這些功能獲益。

## <a name="hello-key-benefits-of-azure-ad-b2b-collaboration-tooyour-organization"></a>hello 的 Azure AD B2B 共同作業 tooyour 組織的主要優點

### <a name="work-with-any-user-from-any-partner"></a>可與來自任何合作夥伴的任何使用者共同作業

* 合作夥伴可使用他們自己的認證

* 不需要夥伴 toouse Azure AD

* 不需要外部目錄或複雜的設定

### <a name="simple-and-secure-collaboration"></a>簡單且安全的共同作業

* 提供存取 tooany 公司應用程式或資料，同時套用複雜，Azure AD 供電的授權原則

* 方便使用者

* 企業級的應用程式與資料安全性

### <a name="no-management-overhead"></a>沒有任何額外的管理負荷

* 不需要進行任何外部帳戶或密碼管理

* 不需要進行任何同步處理或手動帳戶生命週期管理

* 沒有任何額外的外部系統管理負荷

## <a name="you-can-easily-add-b2b-collaboration-users-tooyour-organization"></a>您可以輕鬆加入 B2B 共同作業的使用者 tooyour 組織

系統管理員可以新增 hello B2B 共同作業 (guest) 使用者[Azure 入口網站](https://portal.azure.com)。

![新增來賓使用者](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-toobring-their-own-identity"></a>啟用共同作業者 toobring 自己的識別身分

B2B 共同作業者可以使用自己選擇的身分識別來登入。 如果 hello 使用者沒有 Microsoft 帳戶或 Azure AD 帳戶，會建立一個，順暢地在優惠兌換的 hello 階段。

![登入身分識別選項](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-tooapplication-and-group-owners"></a>委派 tooapplication 和群組的擁有者 
應用程式和群組擁有者可以將 B2B 使用者直接 tooany 應用程式，您有興趣，無論或不是 Microsoft 應用程式。 系統管理員可以將委派權限 tooadd B2B 使用者 toonon 系統管理員。 非系統管理員可以使用 hello [Azure AD 應用程式存取面板](https://myapps.microsoft.com)tooadd B2B 共同作業的使用者 tooapplications 或群組。

![存取面板](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![新增成員](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a>授權原則可保護您的公司內容

可以強制執行條件式存取原則，例如多重要素驗證：
- Hello 租用戶層級
- Hello 應用程式層級
- 針對特定使用者 tooprotect 公司應用程式和資料

![新增成員](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-tooeasily-build-applications-tooonboard"></a>使用我們的 Api 和範例程式碼 tooeasily 建置應用程式 tooonboard
將帶您外部中的夥伴上的方式自訂的 tooyour 組織的需求。

使用 hello [B2B 共同作業邀請 Api](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)，您可以自訂您的入門訓練體驗，包括建立自助式註冊入口網站。 我們[在 Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web) 提供自助式入口網站的範例程式碼。

![註冊入口網站](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

Azure AD B2B 共同作業，您可以使用取得的 Azure AD tooprotect hello 全電力夥伴關係以使用者尋找容易、 淺顯易懂的方式。 因此請繼續進行，聯結 hello 千分位的組織，已經使用 Azure AD B2B 其外部共同作業 ！

## <a name="next-steps"></a>後續步驟

* 系統管理員體驗位於 hello [Azure 入口網站](https://portal.azure.com)。

* 資訊工作者經驗也可用在 hello[存取面板](https://myapps.microsoft.com)。

* 並如往常，請連接 hello 產品小組的任何意見反應、 討論及透過建議我們[Microsoft 技術社群](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b)。

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？](active-directory-b2b-admin-add-users.md)
* [資訊工作者如何新增 B2B 共同作業使用者？](active-directory-b2b-iw-add-users.md)
* [hello hello B2B 共同作業邀請電子郵件項目](active-directory-b2b-invitation-email.md)
* [B2B 共同作業邀請兌換](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 共同作業授權](active-directory-b2b-licensing.md)
* [針對 Azure Active Directory B2B 共同作業問題進行疑難排解](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 共同作業常見問題 (FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B 共同作業 API 和自訂](active-directory-b2b-api.md)
* [適用於 B2B 共同作業使用者的多重要素驗證](active-directory-b2b-mfa-instructions.md)
* [在沒有邀請的情況下新增 B2B 共同作業使用者](active-directory-b2b-add-user-without-invite.md)
* [B2B 共同作業使用者稽核和報告](active-directory-b2b-auditing-and-reporting.md)
* [Azure Active Directory 中應用程式管理的文章索引](active-directory-apps-index.md)

---
title: "Azure Active Directory B2B 共同作業的 aaaSelf 服務註冊入口網站 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業支援跨公司關聯性，方式是讓商務夥伴 tooselectively 存取公司的應用程式"
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
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a>Azure AD B2B 共同作業註冊的自助入口網站

客戶可以進行許多事情 hello 內建功能的公開會透過我們的 IT 系統管理員[Azure 入口網站](https://portal.azure.com)以及我們[應用程式存取面板](https://myapps.microsoft.com)終端使用者。 但是您也注意，企業需要 toocustomize hello 登入工作流程的 B2B 使用者 toofit 其組織的需求。 透過[我們的 API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)，企業就可以達成這個目的。

在與客戶討論過後，我們發現，企業有一項明顯的常見需求。 hello 邀請組織可能不知道事先人員 hello 個別外部共同作業者需要存取 tootheir 資源的人員。 使用者從夥伴公司太註冊本身與一組原則邀請組織控制項的 hello，他們會希望的方式。 透過我們的 API 就能實現此案例，因此我們在 GitHub 上發佈了專門針對此需求的專案：[GitHub 專案範例](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web)。

我們的 Github 專案會示範如何組織可以使用我們的 Api 和以原則為基礎的自助註冊功能提供信任的夥伴，以判斷它們可存取的 hello 應用程式的規則。 在需要時，安全地儲存，而不需要邀請組織 toomanually 將產品上架的 hello 合作夥伴使用者可以取得存取 tooresources 它們。 您可以輕鬆部署到您選擇的 Azure 訂用帳戶的 hello 專案。

## <a name="as-is-code"></a>現狀程式碼

請記住，這段程式碼可做為範例 toodemonstrate 使用方式的 hello Azure Active Directory B2B 邀請應用程式開發介面。 您應該讓開發小組或合作夥伴對此程式碼進行自訂，於檢閱過後再部署到生產案例。

## <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：
* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？](active-directory-b2b-admin-add-users.md)
* [資訊工作者如何新增 B2B 共同作業使用者？](active-directory-b2b-iw-add-users.md)
* [hello hello B2B 共同作業邀請電子郵件項目](active-directory-b2b-invitation-email.md)
* [B2B 共同作業邀請兌換](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 共同作業授權](active-directory-b2b-licensing.md)
* [針對 Azure Active Directory B2B 共同作業問題進行疑難排解](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 共同作業常見問題 (FAQ)](active-directory-b2b-faq.md)
* [適用於 B2B 共同作業使用者的多重要素驗證](active-directory-b2b-mfa-instructions.md)
* [在沒有邀請的情況下新增 B2B 共同作業使用者](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory 中應用程式管理的文章索引](active-directory-apps-index.md)
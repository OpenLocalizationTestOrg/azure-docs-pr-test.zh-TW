---
title: "aaaAdd B2B 共同作業的使用者 tooAzure Active Directory 沒有邀請函 |Microsoft 文件"
description: "您可以讓不含兌換邀請中 Azure Active Directory B2B 共同作業新增其他 Azure AD 的來賓使用者 tooyour guest 使用者。"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a>在沒有邀請的情況下新增 B2B 共同作業來賓使用者

您可以允許使用者，例如 hello 夥伴 tooyour 組織，而不需要兌換邀請 toobe 夥伴代表 tooadd 使用者。 您必須執行的是您所使用的 hello 夥伴組織的 hello 目錄中的列舉權限授與該使用者 

授與這些權限的時機︰

1. Hello 主機組織 (例如，WoodGrove) 中的使用者邀請 hello 夥伴組織中的一位使用者 (例如， Sam@litware.com) 為來賓。
2. hello hello 主機組織中的系統管理員設定原則，允許 Sam tooidentify 和從 hello 夥伴組織 (Litware) 新增其他使用者。
3. 現在 Sam 可以加入其他使用者從 Litware toohello WoodGrove 目錄、 群組或應用程式而不需要兌換邀請 toobe。 如果 Sam Litware 在 hello 適當列舉權限，它會自動發生。

### <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？](active-directory-b2b-admin-add-users.md)
* [資訊工作者如何新增 B2B 共同作業使用者？](active-directory-b2b-iw-add-users.md)
* [hello hello B2B 共同作業邀請電子郵件項目](active-directory-b2b-invitation-email.md)
* [B2B 共同作業邀請兌換](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 共同作業授權](active-directory-b2b-licensing.md)
* [針對 Azure Active Directory B2B 共同作業問題進行疑難排解](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 共同作業常見問題 (FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B 共同作業 API 和自訂](active-directory-b2b-api.md)
* [適用於 B2B 共同作業使用者的多重要素驗證](active-directory-b2b-mfa-instructions.md)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
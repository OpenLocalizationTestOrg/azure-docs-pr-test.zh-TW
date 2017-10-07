---
title: "Azure Active Directory B2B 共同作業的 aaaDelegate 邀請 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業的使用者屬性可進行設定"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a>委派 Azure Active Directory B2B 共同作業邀請

Azure Active Directory (Azure AD) 企業對企業 (B2B) 共同作業，您沒有 toobe 全域管理員 toosend 邀請。 相反地，您可以使用原則，以及委派邀請 toousers 其角色，可讓它們 toosend 邀請。 重要新方式 toodelegate 來賓使用者邀請是透過 hello 來賓邀請者角色。

## <a name="guest-inviter-role"></a>來賓邀請者角色
我們可以指派 hello 使用者 tooGuest 邀請者角色 toosend 邀請。 您不需要 hello 全域管理員角色 toosend 邀請 toobe 的成員。 根據預設，一般使用者也可以叫用 hello 邀請 API 全域系統管理員停用一般使用者的邀請。 使用者也可以叫用 hello API 使用 hello Azure 入口網站或 PowerShell。

以下是範例顯示如何 toouse PowerShell tooadd 使用者 toohello 來賓邀請者角色：

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a>控制誰可以邀請

![控制如何 tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

Azure AD B2B 共同作業，租用戶系統管理員可以設定下列邀請原則 hello:

- 關閉邀請
- 只有系統管理員和 hello 來賓邀請者角色中的使用者可以邀請
- 系統管理員、 hello 來賓邀請者角色和成員可以邀請
- 所有使用者 (包括來賓) 都可以邀請

根據預設，租用戶設定太 #4。 (所有使用者 (包括來賓) 都可以邀請 B2B 使用者。)

## <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 共同作業使用者屬性](active-directory-b2b-user-properties.md)
* [新增 B2B 共同作業使用者 tooa 角色](active-directory-b2b-add-guest-to-role.md)
* [動態群組與 B2B 共同作業](active-directory-b2b-dynamic-groups.md)
* [B2B 共同作業程式碼與 PowerShell 範例](active-directory-b2b-code-samples.md)
* [設定適用於 B2B 共同作業的 SaaS 應用程式](active-directory-b2b-configure-saas-apps.md)
* [B2B 共同作業使用者權杖](active-directory-b2b-user-token.md)
* [B2B 共同作業使用者宣告對應](active-directory-b2b-claims-mapping.md)
* [Office 365 外部共用](active-directory-b2b-o365-external-user.md)
* [B2B 共同作業目前的限制](active-directory-b2b-current-limitations.md)

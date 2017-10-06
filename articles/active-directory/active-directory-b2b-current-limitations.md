---
title: "Azure Active Directory B2B 共同作業 aaaLimitations |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業目前的限制"
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
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a>Azure AD B2B 共同作業的限制
這篇文章中所述的主旨 toohello 限制的目前 azure Active Directory (Azure AD) B2B 共同作業。

## <a name="possible-double-multi-factor-authentication"></a>可能的雙重多重要素驗證
與 Azure AD B2B，您可以強制執行多重要素驗證在 hello 資源組織 (hello 邀請組織)。 這種方法的 hello 原因的詳細[B2B 共同作業的使用者的條件式存取](active-directory-b2b-mfa-instructions.md)。 如果夥伴已設定，並強制執行多重要素驗證，使用者可能已經使用 tooperform hello 驗證一次其主要組織，然後在您一次。

## <a name="instant-on"></a>即時
在 hello B2B 共同作業的流量，我們會加入使用者 toohello 目錄，並動態更新期間兌換邀請、 應用程式指派和等等。 hello 更新寫入通常發生在一個目錄執行個體和必須在所有執行個體之間進行複寫。 在所有執行個體都更新後，複寫作業便已完成。 有時當 hello 物件寫入或更新中有一個執行個體和 hello 呼叫 tooretrieve 這個物件是 tooanother 執行個體，複寫延遲可能會發生。 如果發生這種情況，請重新整理或 toohelp 重試一次。 如果您要撰寫的應用程式，但有一些使用我們的應用程式開發介面，然後重試輪詢是防禦的好作法 tooalleviate 此問題。

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
* [Office 365 外部共用](active-directory-b2b-o365-external-user.md)

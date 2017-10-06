---
title: "aaaDynamic 群組和 Azure Active Directory B2B 共同作業 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業可搭配 Azure AD 動態群組使用"
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>動態群組與 Azure Active Directory B2B 共同作業

## <a name="what-are-dynamic-groups"></a>什麼是動態群組？
Azure Active directory (Azure AD) 的動態組態的安全性群組成員資格位於[hello Azure 入口網站](https://portal.azure.com)。 系統管理員可以設定 Azure Active Directory 中建立的 toopopulate 群組根據使用者屬性 （例如 userType、 部門或國家/地區） 的規則。 成員可以從其屬性為基礎的安全性群組移除 tooor 會自動新增。 這些群組可提供存取 tooapplications 或雲端資源 （SharePoint 網站、 文件），並 tooassign 授權 toomembers。 若要深入了解動態群組，請參閱 [Azure Active Directory 中的專用群組](active-directory-accessmanagement-dedicated-groups.md)。

hello 適當[Azure AD Premium P1 或 P2 授權](https://azure.microsoft.com/pricing/details/active-directory/)是必要的 toocreate 和使用動態群組。 進一步了解本文 hello[建立 Azure Active Directory 中的屬性為基礎的動態群組成員資格規則](active-directory-groups-dynamic-membership-azure-portal.md)。

## <a name="what-are-hello-built-in-dynamic-groups"></a>Hello 內建的動態群組有哪些？
hello**所有使用者**動態群組可讓租用戶系統管理員 」 toocreate 按一下群組，包含具有單一 hello 租用戶中的所有使用者。 根據預設，hello**所有使用者**群組包含所有使用者在 hello 目錄中，包括成員和來賓。
在 [hello 新 Azure Active Directory 系統管理員入口網站中，您可以選擇 tooenable hello**所有使用者**群組 hello 群組設定] 檢視中。

![內建群組](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a>強化 hello 所有使用者的動態群組
根據預設，hello**所有使用者**群組包含您 B2B 共同作業 (guest) 使用者，以及。 您可以進一步保護您**所有使用者**使用規則 tooremove 來賓使用者群組。 hello 如下圖所示 hello**所有使用者**修改 tooexclude guests 群組。

![啟用所有使用者群組](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

您可能也會很有用 toocreate 新的動態群組，其中包含只 guest 使用者，讓您可以套用原則 （例如 Azure AD 條件式存取原則） toothem。
這種群組可能如下所示：

![排除來賓使用者](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 共同作業使用者屬性](active-directory-b2b-user-properties.md)
* [新增 B2B 共同作業使用者 tooa 角色](active-directory-b2b-add-guest-to-role.md)
* [委派 B2B 共同作業邀請](active-directory-b2b-delegate-invitations.md)
* [B2B 共同作業程式碼與 PowerShell 範例](active-directory-b2b-code-samples.md)
* [設定適用於 B2B 共同作業的 SaaS 應用程式](active-directory-b2b-configure-saas-apps.md)
* [B2B 共同作業使用者權杖](active-directory-b2b-user-token.md)
* [B2B 共同作業使用者宣告對應](active-directory-b2b-claims-mapping.md)
* [Office 365 外部共用](active-directory-b2b-o365-external-user.md)
* [B2B 共同作業目前的限制](active-directory-b2b-current-limitations.md)

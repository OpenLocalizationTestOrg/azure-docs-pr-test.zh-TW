---
title: "在 Azure Active Directory aaaDedicated 群組 |Microsoft 文件"
description: "在 Azure Active Directory 中如何建立專用群組與其運作方式的概觀。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Azure Active Directory 中的專用群組
在 Azure Active Directory (Azure AD) 中，hello 專用的群組功能，自動建立，並於其中填入預先定義的 Azure AD 群組的成員資格。 專用群組的成員無法加入或移除使用 hello Azure 傳統入口網站中，Windows PowerShell cmdlet，或以程式設計的方式。

> [!NOTE]
> 專用群組需要 Azure AD Premium 授權已指派給 
>
> * 負責管理群組中的 hello 規則 hello 系統管理員
> * 所有使用者都由 hello 選取都規則 toobe hello 群組的成員
>
>

**tooenable 專用群組**

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後開啟您的組織目錄。
2. 選取 hello**群組**索引標籤，然後再開啟 hello 想 tooedit 的群組。
3. 選取 hello**設定**索引標籤，然後再設定**啟用專用群組**太**是**。

一旦啟用專用群組切換的 hello 設定得**是**，您可以進一步啟用 hello 目錄 tooautomatically 建立 hello 所有使用者專用的群組設定 hello**啟用"All Users"群組**切換太**是**。 您接著還可以編輯此專用群組 hello 名稱輸入在 hello**顯示名稱為"All Users"群組**欄位。

hello 所有使用者群組可用 tooassign hello 相同使用者權限 tooall hello 目錄中的。 例如，您可以授與所有使用者在您的目錄存取 tooa SaaS 應用程式中指派 hello 所有使用者專用的群組 toothis 應用程式的存取。

hello 專用的所有使用者群組包含所有使用者，在 hello 目錄中，包括來賓與外部使用者。 如果您需要一組排除外部使用者，則您可以完成這項作業所建立的群組，並以屬性為基礎動態規則，例如 hello 下列：

                (user.userPrincipalName -notContains "#EXT#@")

排除所有客體為群組，請使用例如 hello 下列規則：

                (user.userType -ne "Guest")

有關如何 toolearn toocreate*進階*規則 （可以包含多個比較的規則） 的動態群組成員資格，請參閱[使用屬性 toocreate 進階規則](active-directory-accessmanagement-groups-with-advanced-rules.md)。

### <a name="next-steps"></a>後續步驟
這些文章提供有關 Azure Active Directory 的其他資訊。

* [使用 Azure Active Directory 群組來管理存取 tooresources](active-directory-manage-groups.md)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [什麼是 Azure Active Directory？](active-directory-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

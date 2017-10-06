---
title: "使用 Azure AD 的 aaaManaging 存取 tooapps |Microsoft 文件"
description: "描述 Azure Active Directory 如何讓組織 toospecify hello 應用程式 toowhich 每個使用者擁有存取權。"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: b0829f18-9e57-4107-925d-5f0457d81671
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: b9461b7a1cc8913cd8fb4a4ce0778afe03274935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-access-tooapps"></a>管理存取 tooapps
持續存取管理、 使用方式評估和報告繼續 toobe 一項挑戰，應用程式已整合至您的組織身分識別系統之後。 在許多情況下，IT 系統管理員或技術服務人員有 tootake 持續以主動管理存取 tooyour 應用程式。 有時候，指派是由一般或分區 IT 小組執行。 Hello 分派決策，通常就是預定的 toobe 委派的 toohello 商業決策人員，其 IT 會先取得核准 hello 分派。  其他組織投資於與現有的自動化身分識別與存取管理系統的整合，像是角色型存取控制 (RBAC) 或屬性型存取控制 (ABAC)。 Hello 整合和規則的開發通常 toobe 特製化且昂貴。 監視或報告任一管理方式是自己單獨、昂貴且複雜的投資。

## <a name="how-does-azure-active-directory-help"></a>Azure Active Directory 有何助益？
 設定應用程式，讓組織 tooeasily 的 azure AD 支援廣泛的存取權管理達到透過委派，包括範圍自動且屬性為基礎的指派 （ABAC 或 RBAC 的情況下） 中的 hello 正確的存取權原則系統管理員管理。 使用 Azure AD 可以輕易地達成複雜的原則，結合多個單一應用程式的管理模型，並可以具有應用程式之間的偶數重複使用管理規則 hello 相同對象。

* [加入新的或現有的應用程式](active-directory-sso-integrate-saas-apps.md)

 Azure AD 的應用程式指派著重於兩種主要的指派模式：

* **個別指派**目錄全域系統管理員權限的 IT 系統管理員可以選取個別的使用者帳戶並授與他們存取 toohello 應用程式。
* **群組為基礎的指派 （付費僅限 Azure AD）**目錄全域系統管理員權限的 IT 系統管理員可以指派群組 toohello 應用程式。 特定使用者存取權是由決定它們是否 hello 群組的成員 hello 次他們嘗試 tooaccess hello 應用程式。 換句話說，系統管理員可以有效地建立指出 「 hello 分派群組任何目前成員沒有存取 toohello 應用程式 」 的指派規則。 使用這個指派選項，系統管理員可以受益於 Azure AD 群組管理選項，包括 [屬性型動態群組](active-directory-accessmanagement-manage-groups.md)、外部系統群組 (例如：內部部署 Active Directory 或工作日)、系統管理員管理或自助管理的群組。 單一群組可輕鬆地指派 toomultiple 應用程式，確保指派親和性的應用程式可以共用指派規則，減少 hello 整體管理複雜性。 請注意，成員資格不支援以群組為基礎的指派 tooapplications 此時該巢狀的群組。

系統管理員可以使用這些兩種指派模式，達成任何需要的指派管理方法。

Azure ad 的使用量和指派 reporting 完全整合，啟用系統管理員 tooeasily 報表上指派狀態、 指派錯誤，以及甚至的使用方式。

## <a name="complex-application-assignment-with-azure-ad"></a>Azure AD 的複雜應用程式指派
考慮 Salesforce 之類的應用程式。 在許多組織中，主要是由 hello 行銷和銷售組織使用 Salesforce。 通常，hello 行銷團隊的成員有高特殊權限存取 tooSalesforce hello 銷售團隊的成員具有有限的存取時。 在許多情況下，資訊工作者的廣泛母體擴展有限制存取 toohello 應用程式。 例外狀況 toothese 規則讓事情更複雜。 它通常是 hello 人員必須 hello 行銷或銷售領導小組 toogrant 使用者存取權，或變更其角色，獨立於這些一般規則。

利用 Azure AD，可以預先設定 Salesforce 之類的應用程式使用單一登入 (SSO) 和自動化佈建。 Hello 應用程式設定之後，系統管理員可以使用 hello 單次性動作 toocreate，並指派 hello 適當的群組。 在此範例中，系統管理員可以執行下列指派 hello:

* [動態群組](active-directory-accessmanagement-manage-groups.md)可以是定義的 tooautomatically 代表 hello 行銷和銷售團隊使用的屬性，例如部門或角色的所有成員：
  
  * 在 Salesforce 中的 toohello"marketing"角色會指派行銷群組的所有成員
  * 所有成員的銷售都小組群組進行指派 toohello 在 Salesforce 中的 「 銷售 」 角色。 進一步精簡可以使用多個代表區域銷售團隊，指派 toodifferent Salesforce 角色的群組。
* tooenable hello 例外狀況機制，無法建立自助的群組，每個角色。 比方說，您可以建立 hello"Salesforce 行銷例外狀況 」 群組為自助群組。 hello 群組只能指派 toohello Salesforce 行銷角色，並且 hello 行銷領導小組可以擁有者。 Hello 行銷領導小組的成員可以加入或移除使用者、 設定聯結原則，或甚至核准或拒絕個別的使用者要求 toojoin。 這是透過不需要經過擁有者或成員特殊訓練的資訊工作者適當的體驗來支援。

在此情況下，所有指派的使用者會自動佈建的 tooSalesforce，因為它們是加入的 toodifferent 其角色指派會更新在 Salesforce 中的群組。 使用者會無法 toodiscover 及存取 Salesforce，透過 hello Microsoft 應用程式存取面板，Office web 用戶端，或甚至是藉由瀏覽 tootheir 組織 Salesforce 登入頁面。 系統管理員將能 tooeasily 檢視使用量和指派的狀態使用 Azure AD 報告 api。

系統管理員可以運用[Azure AD 條件式存取](active-directory-conditional-access.md)tooset 針對特定角色的存取原則。 這些原則可以包括是否允許存取企業環境的 hello 和甚至 Multi-factor Authentication 或裝置需求 tooachieve 存取在各種情況下之外。

## <a name="how-can-i-get-started"></a>如何開始使用？
首先，如果您還未使用 Azure AD，而且您是 IT 系統管理員：

* [試試看！](https://azure.microsoft.com/trial/get-started-active-directory/)  - 您可以立即註冊免費的 30 天試用版，並使用此連結在 5 分鐘內部署第一個雲端解決方案

啟用帳戶共用的 Azure AD 功能包括：

* [群組指派](active-directory-accessmanagement-self-service-group-management.md)
* 新增應用程式 tooAzure AD
* 開始使用指派
* 應用程式指派常見問題集
* [應用程式使用方式儀表板/報告](active-directory-passwords-get-insights.md)

## <a name="where-can-i-learn-more"></a>哪裡可以深入了解？
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [使用條件式存取來保護應用程式](active-directory-conditional-access.md)
* [自助式群組管理/SSAA](active-directory-accessmanagement-self-service-group-management.md)


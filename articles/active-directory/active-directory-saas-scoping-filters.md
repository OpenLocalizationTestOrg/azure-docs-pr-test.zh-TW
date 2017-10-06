---
title: "使用範圍設定篩選 aaaProvisioning 應用程式 |Microsoft 文件"
description: "了解如何 toouse 範圍設定篩選 tooprevent 支援自動的使用者佈建實際佈建如果物件不符合您的業務需求的應用程式中的物件。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>含範圍篩選器的屬性型應用程式佈建
本節 hello 目標是的 tooexplain 如何 toouse 範圍設定篩選 toodefine 屬性為基礎的規則，以決定哪些使用者佈建 toohello 應用程式。

## <a name="clauses-and-scope-groups"></a>子句和範圍群組
![範圍篩選器][1] 

範圍篩選器由一或多個**範圍群組**所定義，其中每個範圍群組都包含一或多個**子句**。 toosee hello 子句為特定範圍群組，請展開它，依序按一下 hello 箭號 toohello 左邊的 hello 群組名稱。

A**子句**決定哪些使用者可以 toopass 透過 hello 範圍設定篩選，藉由評估每個使用者的屬性。 比方說，您可能必須一個子句要求使用者的 'state' 屬性等於紐約，因此只有紐約使用者所佈建到 hello 應用程式。

![範圍群組名稱][2] 

每個**範圍群組**一開始就有一個強制**子句**hello 上方螢幕擷取畫面所示。 這個子句只是指出該 hello 使用者之前，必須先指派 toohello 應用程式範圍篩選器評估。 您無法刪除或修改這個子句。

您可以按下 hello 適當按鈕，來加入新子句或新的範圍群組。 您可以編輯範圍群組的 [範圍群組名稱]  屬性，以便為每個範圍群組提供一個名稱。

## <a name="how-scoping-filters-are-evaluated"></a>範圍篩選器的評估方式
在佈建，我們測試範圍的篩選器 toodetermine 針對每個指派的使用者，如果該使用者需要存取 toohello 應用程式。 您可以將每個子句視為必須傳入 hello 使用者 tooavoid 被篩除的順序的測試。 

如果您有多個定義的範圍群組，每位使用者必須通過至少其中一個 tooaccess hello 應用程式。 在每個範圍群組，不過，hello 使用者必須通過每個子句 toopass 該特定範圍群組。 

換句話說，您可以將範圍群組視為集合在一起，或您可以將 hello 子句視為 AND 集合在一起。 例如，請考慮 hello 範圍設定篩選的下方：

![範圍群組名稱][3]  

根據 toothis 範圍設定篩選，使用者必須滿足 hello 下列準則，toobe 佈建：

1. 它們必須被指派 toohello 應用程式。
2. 它們必須在 hello 工程部門工作
3. 他們必須在舊金山或加拿大工作。

## <a name="related-articles"></a>相關文章
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [自動化使用者佈建和取消佈建 tooSaaS 應用程式](active-directory-saas-app-provisioning.md)
* [自訂使用者佈建的屬性對應](active-directory-saas-customizing-attribute-mappings.md)
* [撰寫屬性對應的運算式](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [帳戶佈建通知](active-directory-saas-account-provisioning-notifications.md)
* [使用 SCIM tooenable 自動佈建的 Azure Active Directory tooapplications 來自使用者和群組](active-directory-scim-provisioning.md)
* [如何教學課程清單 tooIntegrate SaaS 應用程式](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png

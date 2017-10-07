---
title: "Azure AD 屬性對應 aaaCustomizing |Microsoft 文件"
description: "了解 Azure Active Directory 中的 SaaS 應用程式的哪些屬性對應如何修改它們 tooaddress 業務需要。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a>在 Azure Active Directory 中自訂 SaaS 應用程式的使用者佈建屬性對應
Microsoft Azure AD 提供使用者佈建 toothird 合作對象 saas De terceros como Salesforce，Google Apps y otros 的支援。 如果您已將使用者佈建的協力廠商 SaaS 應用程式已啟用，hello Azure 管理入口網站控制它的屬性值，在表單的設定，稱為 「 屬性對應 」。

在 Azure AD 使用者物件和每個 SaaS app 的使用者物件之間，有一組預先設定的屬性對應。 有些 app 則管理其他類型的物件，例如群組或連絡人。 <br> 
 您可以自訂 hello 根據 tooyour 商務需求的預設屬性對應。 這表示您可以變更或刪除現有的屬性對應，或建立新的屬性對應。

在 hello Azure AD 入口網站中，您可以存取這項功能，依序按一下**對應**底下設定**佈建**在 hello**管理**區段**企業應用程式**。


![Salesforce][5] 

按一下**對應**組態中，開啟相關的 hello**屬性對應**刀鋒視窗。  
有 asignaciones de atributos que son necesarias para SaaS 應用程式 toofunction 正確。 必要的屬性，如 hello**刪除**則無法使用功能。


![Salesforce][6]  

在 hello 上述範例中，您可以看到該 hello **Username**在 Salesforce 中的受管理物件的屬性填入 hello **userPrincipalName**的 hello 值連結的 Azure Active Directory 物件。

您可以按一下對應來自訂現有的 [屬性對應]。 這會開啟 hello**編輯屬性**刀鋒視窗。

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a>了解屬性對應類型
有了屬性對應，您就可以控制屬性在協力廠商 SaaS 應用程式中填入的方式。 支援四種不同的對應類型：

* **直接**– hello 目標屬性在 Azure AD 時填入 hello hello 連結物件的屬性值。
* **常數**– hello 目標屬性會填入您所指定的特定字串。
* **運算式**-根據 hello 的類似指令碼運算式的結果填入 hello 目標屬性。 
  如需詳細資訊，請參閱[在 Azure Active Directory 中撰寫屬性對應的運算式](active-directory-saas-writing-expressions-for-attribute-mappings.md)。
* **無**-hello 目標屬性會保留不變。 不過，如果 hello 目標 destino está vacío，它會填入 hello 您指定的預設值。

在加法 toothese 四個基本屬性對應類型中，自訂屬性對應還支援選擇性 hello 概念**預設**值指派。 hello 預設 la asignación del valor 目標屬性會填入值，如果沒有 ningún valor en Azure AD ni hello 目標物件上。 此空白 tooleave hello 最常見的組態。


## <a name="understanding-attribute-mapping-properties"></a>了解屬性對應屬性

在 hello 前一個區段中，您已經導入了的 toohello 屬性對應類型屬性。
在加法 toothis 屬性中，屬性對應並也支援下列屬性的 hello:

- **來源屬性**-hello 使用者屬性從 hello 來源系統 (例如： Azure Active Directory)。
- **目標屬性**– hello 目標系統中的 hello 使用者屬性 (例如： ServiceNow)。
- **符合使用此屬性的物件**– 是否應使用此對應 toouniquely 識別 hello 來源和目標系統之間的使用者。 這通常設定在 hello userPrincipalName，或在 Azure AD 中，通常是 mail 屬性對應 tooa 目標應用程式中的使用者名稱欄位。
- **比對優先順序** – 您可以設定多個比對屬性。 有多個，會評估 hello 這個欄位所定義的順序。 只要找到相符項目，便不會評估進一步比對屬性。
- **套用此對應**
    - **一律** – 將此對應套用於使用者建立和更新動作
    - **僅限建立期間** - 僅將此對應套用於使用者建立動作


## <a name="what-you-should-know"></a>您應該知道的事情

Microsoft Azure AD 提供有效率的同步處理程序實作。 在初始化環境中，同步處理期間只會處理需要更新的物件。 更新屬性對應上的同步處理循環的 hello 效能有影響。 更新 toohello 屬性對應組態需要重新評估所有受管理的物件 toobe。 它是建議最佳作法 tookeep hello 數目最少的連續變更 tooyour 屬性對應。

## <a name="next-steps"></a>後續步驟

* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [自動化使用者佈建/取消佈建 tooSaaS 應用程式](active-directory-saas-app-provisioning.md)
* [撰寫屬性對應的運算式](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [適用於使用者佈建的範圍篩選器](active-directory-saas-scoping-filters.md)
* [使用 SCIM tooenable 自動佈建的 Azure Active Directory tooapplications 來自使用者和群組](active-directory-scim-provisioning.md)
* [帳戶佈建通知](active-directory-saas-account-provisioning-notifications.md)
* [如何教學課程清單 tooIntegrate SaaS 應用程式](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png


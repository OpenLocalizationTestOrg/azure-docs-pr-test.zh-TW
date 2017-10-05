---
title: "在 Azure AD 中自動化 SaaS 應用程式使用者佈建 | Microsoft Docs"
description: "簡介如何使用 Azure AD 自動佈建、解除佈建，以及跨多個協力廠商 SaaS 應用程式持續更新使用者帳戶。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 58c5fa2d-bb33-4fba-8742-4441adf2cb62
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: curtand
ms.openlocfilehash: 7cb780117d64d67449146b9757f8162e23e65d1e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-to-saas-applications-with-azure-active-directory"></a>自動化使用 Azure Active Directory 對於 SaaS 應用程式的使用者佈建和取消佈建
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>SaaS 應用程式的自動化使用者佈建是什麼？
Azure Active Directory (Azure AD) 可讓您自動化在雲端 ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) 應用程式中建立、維護和移除使用者身分識別，例如 Dropbox、Salesforce、ServiceNow 等等。

**以下是這項功能可讓您執行的一些範例：**

* 當人員加入您的小組時，在正確的 SaaS 應用程式中為新的人員自動建立新帳戶。
* 當人員離開小組時，自動從 SaaS 應用程式停用帳戶。
* 確保您的 SaaS 應用程式中的身分識別，根據目錄中的變更保持最新狀態。
* 將支援的非使用者物件，例如群組，佈建至 SaaS 應用程式。

**自動化使用者佈建也包含下列功能：**

* 比對 Azure AD 和 SaaS 應用程式之間現有身分識別的能力。
* 自訂選項，協助 Azure AD 符合您目前使用之 SaaS 應用程式的目前組態。
* 佈建錯誤的選用電子郵件警示。
* 報告和活動記錄檔，協助監視與疑難排解。

## <a name="why-use-automated-provisioning"></a>為何要使用自動化佈建？
一些使用這項功能的常見動機包括：

* 為了避免成本、效率不彰，以及與手動佈建程序相關聯的人為錯誤。
* 為了在使用者離開組織時，立即從主要 SaaS 應用程式移除使用者的身分識別以保護您的組織。
* 為了輕鬆將大量使用者數目匯入特定 SaaS 應用程式。
* 為了享受讓佈建方案以您針對 Azure AD 單一登入定義的相同應用程式存取原則執行的便利性。

## <a name="frequently-asked-questions"></a>常見問題集
**Azure AD 將目錄變更寫入至 SaaS 應用程式的頻率為何？**

Azure AD 每隔五到十分鐘就會檢查變更。 如果 SaaS 應用程式傳回數個錯誤 (例如無效的系統管理認證)，則 Azure AD 會逐漸降低其頻率，最多每日一次直到修正錯誤為止。

**佈建我的使用者需要多久時間？**

累加變更幾乎是立即發生，但是如果您嘗試佈建大部分的目錄，則取決於您擁有的使用者和群組數目。 小型目錄只需要幾分鐘的時間，中型目錄可能需要數分鐘，而非常大型的目錄可能需要數小時。

**我要如何追蹤目前佈建作業的進度？**

您可以檢閱目錄的 [報告] 區段底下的 [帳戶佈建報告]。 另一個選項是造訪您的佈建目標之 SaaS 應用程式的 [儀表板] 索引標籤，並且查看頁面底部附近的 [整合狀態] 區段底下。

**如何得知使用者無法正確佈建？**

在佈建組態精靈的結尾，有一個選項可以訂閱佈建失敗的電子郵件通知。 您也可以檢查佈建錯誤報告，以查看哪些使用者無法佈建及其原因。

**Azure AD 是否可以將變更從 SaaS 應用程式寫回至目錄？**

對於大多數 SaaS 應用程式，佈建僅限輸出，這表示使用者會從目錄寫入應用程式，而變更無法從應用程式寫回至目錄。 但是，針對 [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx)，佈建僅限輸入，這表示使用者會從 Workday 匯入目錄，同樣地，目錄中的變更無法寫回至 Workday。

**我要如何提交意見反應給工程小組？**

請透過 [Azure Active Directory 意見反應論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)與我們連絡。

## <a name="how-does-automated-provisioning-work"></a>自動化佈建如何運作？
Azure AD 會藉由連接到每個應用程式廠商所提供的佈建端點，將使用者佈建至 SaaS 應用程式。 這些端點可以讓 Azure AD 以程式設計方式建立、更新和移除使用者。 以下是 Azure AD 進行自動化佈建的不同步驟的簡短概觀。

1. 當您第一次對應用程式啟用佈建時，會執行下列動作：
   * Azure AD 會嘗試比對 SaaS 應用程式中任何現有使用者與其在目錄中的對應身分識別。 若有使用者符合時，就「不會」  自動啟用單一登入。 為了讓使用者能存取應用程式，必須在 Azure AD 中直接或透過群組成員資格，明確將他們指派至應用程式。
   * 如果您已經指定哪些使用者應指派給應用程式，且 Azure AD 無法找到這些使用者的現有帳戶，則 Azure AD 會在應用程式中為其佈建新帳戶。
2. 一旦完成上述的初始同步處理之後，Azure AD 會每隔 10 分鐘檢查下列變更：
   * 如果新使用者已指派至應用程式 (直接或透過群組成員資格)，則系統會為他們在 SaaS 應用程式中佈建新的帳戶。
   * 如果已移除使用者的存取權，則其帳戶在 SaaS 應用程式中會標示為停用 (使用者永遠不會完全刪除，以保護您在錯誤設定時不會遺失資料)。
   * 如果使用者最近指派至應用程式，而且他們已經在 SaaS 應用程式中有帳戶，則該帳戶會標示為已啟用，如果相較於目錄是過時的，則可能會更新某些使用者屬性。
   * 如果使用者的資訊 (例如電話號碼、辦公室位置等等) 在目錄中已變更，則該資訊也會在 SaaS 應用程式中更新。

如需有關如何在 Azure AD 和 SaaS 應用程式之間對應屬性的詳細資訊，請參閱 [自訂屬性對應](active-directory-saas-customizing-attribute-mappings.md)上的文章。

## <a name="list-of-apps-that-support-automated-user-provisioning"></a>支援自動化使用者佈建的應用程式清單
Azure AD 應用程式資源庫中的所有「精選」應用程式都支援自動化使用者佈建。 [精選應用程式的清單可以在此檢視̂。](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

為了讓應用程式支援自動化使用者佈建，它必須先提供必要的端點，讓外部程式自動化建立、維護及移除使用者。 因此，並非所有 SaaS 應用程式都與此功能相容。 針對支援此功能的應用程式，Azure AD 工程小組則是能夠建置與這些應用程式的佈建連接器，這項工作是以目前和潛在客戶的需求來排定優先順序。

若要連絡 Azure AD 工程小組以要求對於其他應用程式的佈建支援，請透過 [Azure Active Directory 意見反應論壇](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning)提交訊息。

## <a name="related-articles"></a>相關文章
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [自訂使用者佈建的屬性對應](active-directory-saas-customizing-attribute-mappings.md)
* [撰寫屬性對應的運算式](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [適用於使用者佈建的範圍篩選器](active-directory-saas-scoping-filters.md)
* [使用 SCIM 以啟用從 Azure Active Directory 到應用程式的使用者和群組自動佈建](active-directory-scim-provisioning.md)
* [帳戶佈建通知](active-directory-saas-account-provisioning-notifications.md)
* [如何整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)


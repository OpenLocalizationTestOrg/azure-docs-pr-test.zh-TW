---
title: "aaaAutomated SaaS 應用程式使用者佈建 Azure AD 中 |Microsoft 文件"
description: "您可以使用 Azure AD tooautomatically 佈建、 簡介 toohow 解除佈建，並持續更新多個協力廠商 SaaS 應用程式的使用者帳戶。"
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
ms.openlocfilehash: a1f3ecdd513e2b603f8ad9901e9f551b3b982b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-toosaas-applications-with-azure-active-directory"></a>自動化使用者佈建和解除佈建 tooSaaS 應用程式與 Azure Active Directory
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>SaaS 應用程式的自動化使用者佈建是什麼？
Azure Active Directory (Azure AD) 可讓您 tooautomate hello 建立、 維護和移除的雲端中的使用者身分 ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) 應用程式，例如 Dropbox、 Salesforce、 ServiceNow、 等等。

**以下是一些範例項目這項功能可讓您 toodo 的：**

* 在自動建立新帳戶 hello 右 SaaS 應用程式為新的人在加入您的小組。
* 人員勢必會離開 hello 小組時，自動停用從 SaaS 應用程式的帳戶。
* 確保您的 SaaS 應用程式中的 hello 身分識別都保持向上 toodate 根據 hello 目錄中的變更。
* 非使用者物件，例如群組，支援這些 tooSaaS 應用程式佈建。

**自動的使用者佈建也會包含下列功能的 hello:**

* hello 能力 toomatch 現有之間的身分識別 Azure AD 與 SaaS 應用程式。
* Azure AD 的自訂選項 toohelp 容納 hello hello SaaS 應用程式目前正在使用您的組織目前的設定。
* 佈建錯誤的選用電子郵件警示。
* 報告和活動記錄檔 toohelp 監視和疑難排解。

## <a name="why-use-automated-provisioning"></a>為何要使用自動化佈建？
一些使用這項功能的常見動機包括：

* tooavoid hello 成本、 無效率，以及手動佈建程序相關聯的人為錯誤。
* toosecure 立即移除使用者的身分識別，從您的組織金鑰 SaaS 應用程式時離開 hello 組織。
* tooeasily 匯入大量使用者數目特定 SaaS 應用程式。
* tooenjoy hello 方便起見，讓您佈建的方案從 hello 執行您的 Azure AD 單一登入所定義的相同應用程式存取原則。

## <a name="frequently-asked-questions"></a>常見問題集
**Azure AD 頻率撰寫目錄變更 toohello SaaS 應用程式？**

Azure AD 會每五鐘顯示 tooten 檢查有變更。 如果 hello SaaS 應用程式傳回的幾個錯誤 （例如在 hello 大小寫不正確的系統管理員認證），Azure AD 將會逐漸減緩其每日 hello 錯誤修正之前的頻率 tooup tooonce。

**時間會花費 tooprovision 我的使用者？**

累加變更，就可能發生幾乎立即嘗試 tooprovision 但大部分的目錄，則依賴 hello 使用者和群組的數目。 小型目錄只需要幾分鐘的時間，中型目錄可能需要數分鐘，而非常大型的目錄可能需要數小時。

**如何追蹤 hello hello 的目前佈建作業進度？**

您可以檢閱 hello 報表區段的目錄下的 hello 帳戶佈建報表。 另一個選項是 toovisit hello SaaS 應用程式，您要佈建，hello 儀表板索引標籤，然後查看底下 hello hello hello 頁面底部附近的 「 Integration 狀態 」 一節。

**我怎麼知道的使用者是否無法佈建正確 tooget？**

結尾 hello hello 有佈建組態精靈是進行佈建失敗選項 toosubscribe tooemail 通知。 您也可以查看哪些使用者無法佈建 toobe hello 佈建錯誤報表 toosee 和原因。

**Azure AD 可以從 hello SaaS 應用程式後 toohello 目錄寫入變更嗎？**

針對大部分的 SaaS 應用程式，佈建是僅輸出，這表示使用者會從 hello 目錄 toohello 應用程式、 寫入和 hello 應用程式的變更無法寫回 toohello 目錄。 如[Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx)，不過，佈建僅限輸入，這表示，使用者會匯入至 hello 目錄從 Workday，而且同樣地，hello 目錄中的變更執行未取得寫回至 Workday。

**如何可提交意見反應 toohello 工程小組？**

請與我們連絡透過 hello [Azure Active Directory 意見反應論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)。

## <a name="how-does-automated-provisioning-work"></a>自動化佈建如何運作？
Azure AD 佈建使用者 tooSaaS 應用程式，藉由連接提供每個應用程式廠商 tooprovisioning 端點。 這些端點可讓 Azure AD tooprogrammatically 建立、 更新及移除使用者。 以下是不同的步驟，Azure AD 會佈建 tooautomate hello 的簡短概觀。

1. 當您啟用佈建應用程式的 hello 第一次時，請執行下列動作的 hello:
   * Azure AD 將會嘗試 toomatch hello SaaS 應用程式中的 hello 目錄中其對應身分識別任何現有使用者。 若有使用者符合時，就「不會」  自動啟用單一登入。 為了讓使用者 toohave 存取 toohello 應用程式，則必須明確地指派 toohello 應用程式在 Azure AD 中直接或透過群組成員資格。
   * 如果您已經指定哪些使用者應該指派 toohello 應用程式，且 Azure AD 失敗 toofind 現有的帳戶，這些使用者，Azure AD 將會在佈建新帳戶，hello 應用程式。
2. 一旦完成 hello 初始同步處理之後上面所述，Azure AD 會檢查每隔 10 分鐘 hello 下列變更：
   * 如果新的使用者已指派給 toohello 應用程式 （直接或透過群組成員資格），然後將其佈建 hello SaaS 應用程式中的新帳戶。
   * 如果已移除使用者的存取權，則 hello SaaS 應用程式中的帳戶將會標示為停用 （絕對不會完全刪除使用者，這會防止您的設定不正確的 hello 事件中的資料遺失）。
   * 如果使用者最近指派 toohello 應用程式，且他們已經有帳戶 hello SaaS 應用程式中帳戶將會標示為已啟用，以及在有過期的時間比較的 toohello 目錄，可能會更新某些使用者屬性。
   * 如果 hello 目錄中已經變更使用者的資訊 （例如電話、 辦公室位置等等），則該資訊都會也更新 hello SaaS 應用程式中。

如需有關 Azure AD 之間如何對應屬性及 SaaS 應用程式，請參閱 hello 文件[自訂屬性對應](active-directory-saas-customizing-attribute-mappings.md)。

## <a name="list-of-apps-that-support-automated-user-provisioning"></a>支援自動化使用者佈建的應用程式清單
所有 hello Azure AD 應用程式庫中的 hello 「 精選 」 應用程式都支援自動的使用者佈建。 [hello 份精選應用程式可以在此檢視。](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

為了讓應用程式 toosupport 自動化使用者佈建，它必須先提供 hello 允許外部程式 tooautomate hello 建立、 維護和移除使用者的必要端點。 因此，並非所有 SaaS 應用程式都與此功能相容。 針對支援此應用程式，hello Azure AD 的工程小組將則無法 toobuild 佈建的連接器 toothose 應用程式，而且這項工作已設定優先權，由 hello 的目前和潛在客戶的需求。

toocontact hello Azure AD 的工程小組 toorequest 佈建其他的應用程式的支援，請送出 hello 訊息[Azure Active Directory 意見反應論壇](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning)。

## <a name="related-articles"></a>相關文章
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [自訂使用者佈建的屬性對應](active-directory-saas-customizing-attribute-mappings.md)
* [撰寫屬性對應的運算式](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [適用於使用者佈建的範圍篩選器](active-directory-saas-scoping-filters.md)
* [使用 SCIM tooenable 自動佈建的 Azure Active Directory tooapplications 來自使用者和群組](active-directory-scim-provisioning.md)
* [帳戶佈建通知](active-directory-saas-account-provisioning-notifications.md)
* [如何教學課程清單 tooIntegrate SaaS 應用程式](active-directory-saas-tutorial-list.md)


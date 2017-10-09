---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 ZenDesk | Microsoft Docs"
description: "了解如何 tooconfigure Azure Active Directory tooautomatically 佈建和取消佈建使用者帳戶 tooZenDesk。"
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a>教學課程︰設定自動使用者佈建的 ZenDesk


本教學課程的 hello 目標是 tooshow hello 需要 tooperform ZenDesk 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooZenDesk 中的步驟。 

## <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

*   Azure Active Directory 租用戶
*   ZenDesk 租用戶與 hello[企業計劃](https://www.zendesk.com/product/pricing/)或進一步啟用 
*   ZenDesk 中具有系統管理員權限的使用者帳戶 

> [!NOTE]
> hello Azure AD 佈建整合依賴 hello [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api)，也就是可用 tooZenDesk 小組 hello 基本計劃或更高。

## <a name="assigning-users-toozendesk"></a>指派使用者 tooZenDesk

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。 

之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour ZenDesk 的應用程式中的群組。 一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour ZenDesk 應用程式：

[指派使用者或群組的 tooan 企業應用程式](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a>指派使用者 tooZenDesk 的重要秘訣

*   建議在單一 tooZenDesk tootest hello 佈建組態指派給 Azure AD 使用者。 其他使用者及/或群組可能會稍後再指派。

*   指派使用者 tooZenDesk 時，您必須選取其中一個 hello**使用者**角色或另一個有效應用程式特定的角色 （如果有的話） 在 hello 分派 對話方塊中。 hello**預設存取**角色不適用於佈建，以及這些使用者會略過。

> [!NOTE]
> 做為新增的功能，佈建服務的 hello 讀取 Zendesk 中, 定義的任何自訂角色，並匯入至 Azure AD 在 hello 選取角色 對話方塊中加以選取。 啟用佈建服務的 hello 和一個同步處理循環完成之後，這些角色會顯示在 hello Azure 入口網站。

## <a name="configuring-user-provisioning-toozendesk"></a>設定使用者佈建 tooZenDesk 

本節會引導您完成連接您的 Azure AD tooZenDesk 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用 Azure AD 中的使用者和群組指派為基礎的 ZenDesk 中指派的使用者帳戶。

> [!TIP] 
> 您也可以選擇 tooenabled SAML 型單一登入 zendesk，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a>設定 Azure AD 中佈建 tooZenDesk 自動使用者帳戶


1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。

2. 如果您已經設定 ZenDesk 的單一登入，搜尋您的 ZenDesk 使用 hello 搜尋欄位中的執行個體。 否則，請選取**新增**並搜尋**ZenDesk** hello 應用程式庫中。 從 hello 搜尋結果中，選取 ZenDesk，並將它新增 tooyour 的應用程式的清單。

3. 選取您的 ZenDesk，執行個體，然後選取 hello**佈建** 索引標籤。

4. 設定 hello**佈建模式**太**自動**。

    ![ZenDesk 佈建](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. 在 hello**系統管理員認證**區段中，輸入的 hello**管理員使用者名稱 & tokenkey 網域**產生由您的 ZenDesk 帳戶 (您可以在您的帳戶下找到 hello 語彙基元：**系統管理員**  >  **API** > **設定**)。 

    ![ZenDesk 佈建](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. 在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 的 tooyour ZenDesk 的應用程式可以連接。 如果 hello 連線失敗，請確定您的 ZenDesk 帳戶具有系統管理員權限，並再試一次步驟 5。

7. 輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，以及檢查 hello 核取方塊 傳送電子郵件通知發生失敗時。 」

8. 按一下 [儲存] 。 

9. 在 hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooZenDesk**。

10. 在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooZenDesk 同步。 hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 中的使用者帳戶 ZenDesk 進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

11. tooenable hello Azure AD 佈建服務 zendesk，變更 hello**佈建狀態**太**上**在 hello**設定**區段

12. 按一下 [儲存] 。 

這項作業會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooZenDesk 在 hello 使用者和群組 > 一節。 hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。 您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述 hello 佈建服務所執行的所有動作。

如需有關 tooread hello Azure AD 佈建的記錄方式的詳細資訊，請參閱[報告使用者自動帳戶佈建](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。


## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-enterprise-apps-manage-provisioning.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>後續步驟

* [瞭解如何 tooreview 記錄並取得上佈建活動報表](active-directory-saas-provisioning-reporting.md)

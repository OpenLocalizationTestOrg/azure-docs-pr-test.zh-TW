---
title: "教學課程：Azure Active Directory 與 Salesforce 沙箱整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Salesforce 沙箱之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 06ff50050845383a602b0edd6fca953ddd37cebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a>教學課程︰設定自動使用者佈建的 Salesforce 沙箱

本教學課程的 hello 目標是 tooshow hello 您需要在 Salesforce 沙箱和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooSalesforce 沙箱 tooperform 的步驟。

## <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

*   Azure Active Directory 租用戶。
*   您必須擁有 Salesforce Sandbox for Work 或 Salesforce Sandbox for Education 的有效租用戶。 您可以使用免費試用帳戶來使用任何服務。
*   具有小組系統管理員權限的 Salesforce 沙箱使用者帳戶。

## <a name="assigning-users-toosalesforce-sandbox"></a>指派使用者 tooSalesforce 沙箱

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。

之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooyour Salesforce 沙箱應用程式。 一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Salesforce 沙箱應用程式：

[指派使用者或群組的 tooan 企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce-sandbox"></a>指派使用者 tooSalesforce 沙箱的重要秘訣

* 建議在單一 tooSalesforce 沙箱 tootest hello 佈建組態指派給 Azure AD 使用者。 其他使用者及/或群組可能會稍後再指派。

* 指派使用者 tooSalesforce 沙箱時，您必須選取有效的使用者角色。 hello 「 預設的存取 」 角色不適用於佈建。

> [!NOTE]
> 此應用程式會從 Salesforce 沙箱的佈建程序，將使用者指派時，哪個 hello 客戶可能會想 tooselect hello 一部分匯入自訂的角色。

## <a name="enable-automated-user-provisioning"></a>啟用自動使用者佈建

本節引導您連接您 Azure AD tooSalesforce 沙箱的使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用指派的使用者帳戶，在 Salesforce 沙箱根據使用者和群組Azure AD 中的指派。

>[!Tip]
>您也可以選擇 tooenabled SAML 型單一登入 Salesforce 沙箱，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure 自動帳戶佈建使用者：

hello 本節目標在於 toooutline 如何 tooenable 使用者佈建的 Active Directory 使用者帳戶 tooSalesforce 沙箱。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。

2. 如果您已經設定進行單一登入 Salesforce 沙箱，搜尋您的 Salesforce 沙箱使用 hello 搜尋欄位中的執行個體。 否則，請選取**新增**並搜尋**Salesforce 沙箱**hello 應用程式庫中。 從 hello 搜尋結果中，選取 Salesforce 沙箱，並將它加入 tooyour 的應用程式的清單。

3. 選取您的 Salesforce 沙箱的執行個體，然後選取 hello**佈建** 索引標籤。

4. 設定 hello**佈建模式**太**自動**。 
    ![佈建](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)

5. 在 hello**系統管理員認證**區段中，提供下列組態設定的 hello:
   
    a. 在 hello**系統管理員使用者名稱**文字方塊中，輸入的 Salesforce 帳戶名稱已 hello**系統管理員**在 Salesforce.com 被指派的設定檔。
   
    b. 在 hello**系統管理員密碼**文字方塊中，此帳戶類型 hello 密碼。

6. tooget Salesforce 沙箱安全性權杖中，開啟新索引標籤，並登入 hello 相同 Salesforce 沙箱管理員帳戶。 Hello 右上角的 hello 頁面上，按一下您的名稱，然後**我的設定**。

     ![啟用自動使用者佈建](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "啟用自動使用者佈建")
7. 在 hello 左側瀏覽窗格中，按一下 **個人**tooexpand hello 相關的區段，然後按一下**重設我的安全性 Token**。
  
    ![啟用自動使用者佈建](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "啟用自動使用者佈建")
8. 在 [hello**重設我的安全性 Token**頁面上，按一下 hello**重設安全性 Token** ] 按鈕。

    ![啟用自動使用者佈建](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "啟用自動使用者佈建")
9. 請檢查與此系統管理員帳戶相關聯 hello 電子郵件收件匣。 從包含 hello 新的安全性權杖的 Salesforce Sandbox.com 尋找電子郵件。
10. 複製 hello 語彙基元，請移 tooyour Azure AD 視窗中，並將它貼到 hello**通訊端語彙基元**欄位。

11. 在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 可連接 tooyour Salesforce 沙箱應用程式。

12. 在 hello**通知電子郵件**欄位中，輸入 hello 電子郵件地址的個人或群組應該收到佈建錯誤通知，並選取 hello 核取方塊。

13. 按一下 [儲存]。  
    
14.  在 hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooSalesforce 沙箱。**

15. 在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooSalesforce 沙箱同步。 hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在 Salesforce 沙箱進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

16. tooenable hello Azure AD 佈建服務的 Salesforce 沙箱，變更 hello**佈建狀態**太**上**hello 設定 區段中

17. 按一下 [儲存]。


啟動 hello 初始同步處理的任何使用者和/或群組指派 tooSalesforce hello 使用者和群組 > 一節中的沙箱。 hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。 您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Salesforce 沙箱應用程式上的執行的所有動作。

您現在可以建立測試帳戶了。 等候總 tooverify hello 帳戶已經過同步處理 toosalesforce too20 分鐘。

## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定單一登入](active-directory-saas-salesforcesandbox-tutorial.md)
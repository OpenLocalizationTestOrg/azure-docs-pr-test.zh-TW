---
title: "教學課程：Azure Active Directory 與 Salesforce 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Salesforce 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a>教學課程︰設定自動使用者佈建的 Salesforce

本教學課程 hello 目標是在 Salesforce 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooSalesforce 的 tooshow hello 步驟需要的 tooperform。

## <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

*   Azure Active Directory 租用戶。
*   您必須擁有 Salesforce for Work 或 Salesforce for Education 的有效租用戶。 您可以使用免費試用帳戶來使用任何服務。
*   具有小組系統管理員權限的 Salesforce 使用者帳戶。

## <a name="assigning-users-toosalesforce"></a>指派使用者 tooSalesforce

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。

之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour Salesforce 應用程式中的群組。 一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Salesforce 應用程式：

[指派使用者或群組的 tooan 企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a>指派使用者 tooSalesforce 的重要秘訣

*   建議在單一 tooSalesforce tootest hello 佈建組態指派給 Azure AD 使用者。 其他使用者及/或群組可能會稍後再指派。

*  指派使用者 tooSalesforce 時，您必須選取有效的使用者角色。 hello 「 預設的存取 」 角色不適用於佈建

    > [!NOTE]
    > 此應用程式匯入來自 Salesforce 的佈建程序，將使用者指派時，哪個 hello 客戶可能會想 tooselect hello 一部分的自訂角色

## <a name="enable-automated-user-provisioning"></a>啟用自動使用者佈建

本節會引導您完成連接您的 Azure AD tooSalesforce 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用 Azure AD 中的使用者和群組指派為基礎的 Salesforce 中指派的使用者帳戶.

>[!Tip]
>您也可以選擇 tooenabled SAML 型單一登入 salesforce，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure 自動帳戶佈建使用者：

hello 本節目標在於 toooutline 如何 tooenable 使用者佈建的 Active Directory 使用者帳戶 tooSalesforce。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。

2. 如果您已經設定 Salesforce 的單一登入，搜尋您的 Salesforce 使用 hello 搜尋欄位中的執行個體。 否則，請選取**新增**並搜尋**Salesforce** hello 應用程式庫中。 從 hello 搜尋結果中，選取 Salesforce，並將它新增 tooyour 的應用程式的清單。

3. 選取您的 Salesforce 執行個體，然後選取 hello**佈建** 索引標籤。

4. 設定 hello**佈建模式**太**自動**。 
![佈建](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)

5. 在 hello**系統管理員認證**區段中，提供下列組態設定的 hello:
   
    a. 在 hello**系統管理員使用者名稱**文字方塊中，輸入 Salesforce 帳戶名稱已 hello**系統管理員**在 Salesforce.com 被指派的設定檔。
   
    b. 在 hello**系統管理員密碼**文字方塊中，此帳戶類型 hello 密碼。

6. tooget Salesforce 安全性權杖中，開啟新索引標籤，並登入 hello 相同 Salesforce 管理員帳戶。 Hello 右上角的 hello 頁面上，按一下您的名稱，然後**我的設定**。

     ![啟用自動使用者佈建](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "啟用自動使用者佈建")
7. 在 hello 左側瀏覽窗格中，按一下 **個人**tooexpand hello 相關的區段，然後按一下**重設我的安全性 Token**。
  
    ![啟用自動使用者佈建](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "啟用自動使用者佈建")
8. 在 [hello**重設我的安全性 Token**頁面上，按一下**重設安全性 Token** ] 按鈕。

    ![啟用自動使用者佈建](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "啟用自動使用者佈建")
9. 請檢查與此系統管理員帳戶相關聯 hello 電子郵件收件匣。 從包含 hello 新的安全性權杖的 Salesforce.com 尋找電子郵件。
10. 複製 hello 語彙基元，請移 tooyour Azure AD 視窗中，並將它貼到 hello**通訊端語彙基元**欄位。

11. 在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 的 tooyour Salesforce 應用程式可以連接。

12. 在 hello**通知電子郵件**欄位中，輸入 hello 電子郵件地址的個人或群組應該收到佈建錯誤通知，並選取 hello 核取方塊下方。

13. 按一下 [儲存]。  
    
14.  在 hello 對應區段中，選取**tooSalesforce 同步處理 Azure Active Directory 使用者。**

15. 在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooSalesforce 同步。 請注意，hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在 Salesforce 中進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

16. tooenable hello Azure AD 佈建服務針對 Salesforce，變更 hello**佈建狀態**太**上**hello 設定 區段中

17. 按一下 [儲存]。

這樣會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooSalesforce 在 hello 使用者和群組 > 一節。 請注意 hello 初始同步處理所花費的時間 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。 您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述 hello 佈建您的 Salesforce 應用程式上的服務所執行的所有動作。

您現在可以建立測試帳戶了。 等候總 tooverify hello 帳戶已經過同步處理 tooSalesforce too20 分鐘。

## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定單一登入](active-directory-saas-salesforce-tutorial.md)
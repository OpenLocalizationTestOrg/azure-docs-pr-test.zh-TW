---
title: "教學課程：Azure Active Directory 與 Jive 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Jive 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a>教學課程：設定 Jive 來佈建使用者

本教學課程的 hello 目標是 tooshow hello 您需要在 Jive 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooJive tooperform 的步驟。

## <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

*   Azure Active Directory 租用戶。
*   啟用 Jive 單一登入的訂用帳戶。
*   Jive 中具有小組管理員權限的使用者帳戶。

## <a name="assigning-users-toojive"></a>指派使用者 tooJive

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。

之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooyour Jive 的應用程式。 一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Jive 應用程式：

[指派使用者或群組的 tooan 企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a>指派使用者 tooJive 的重要秘訣

*   建議在單一 Azure AD 使用者被指派 tooJive tootest hello 佈建的組態。 其他使用者及/或群組可能會稍後再指派。

*   指派使用者 tooJive 時，您必須選取有效的使用者角色。 hello 「 預設的存取 」 角色不適用於佈建。

## <a name="enable-user-provisioning"></a>啟用使用者佈建

本節會引導您完成連接您的 Azure AD tooJive 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用 Azure AD 中的使用者和群組指派為基礎的 Jive 中指派的使用者帳戶。

> [!TIP]
> 您也可以選擇 SAML 型單一登入 jive，遵循所提供的 hello 指示 tooenabled [Azure 入口網站](https://portal.azure.com)。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure 使用者帳戶佈建：

hello 本節目標在於 toooutline 如何 tooenable 使用者佈建的 Active Directory 使用者帳戶 tooJive。
此程序的一部分，您就需要的 tooprovide 需要向 Jive.com toorequest 的使用者安全性 token。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。

2. 如果您已經設定進行單一登入 Jive，搜尋您的 Jive 使用 hello 搜尋欄位中的執行個體。 否則，請選取**新增**並搜尋**Jive** hello 應用程式庫中。 從 hello 搜尋結果中，選取 Jive，並將它新增 tooyour 的應用程式的清單。

3. 選取您的 Jive，執行個體，然後選取 hello**佈建** 索引標籤。

4. 設定 hello**佈建模式**太**自動**。 

    ![佈建](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. 在 hello**系統管理員認證**區段中，提供下列組態設定的 hello:
   
    a. 在 hello **Jive 管理使用者名稱**文字方塊中，輸入 Jive 帳戶名稱已 hello**系統管理員**在 Jive.com 中的設定檔。
   
    b. 在 hello **Jive 管理密碼**文字方塊中，此帳戶類型 hello 密碼。
   
    c. 在 hello **Jive 租用戶 URL**文字方塊中，型別 hello Jive 租用戶 URL。
      
      > [!NOTE]
      > hello Jive 租用戶 URL 是由您的組織 toolog tooJive 中的 URL。  
      > 一般而言，hello URL 具有下列格式的 hello: **www。\<組織\>。 jive.com**。          

6. 在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 的 tooyour Jive 的應用程式可以連接。

7. 輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊下方。

8. 按一下 [儲存]。

9. 在 hello 對應區段中，選取**tooJive 同步處理 Azure Active Directory 使用者。**

10. 在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooJive 同步。 hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶 Jive 中進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

11. tooenable hello Azure AD 佈建服務 jive，變更 hello**佈建狀態**太**上**hello 設定 區段中

12. 按一下 [儲存]。

它會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooJive 在 hello 使用者和群組 > 一節。 hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。 您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Jive 的應用程式上執行的所有動作。

您現在可以建立測試帳戶了。 等候總 tooverify hello 帳戶已經過同步處理 tooJive too20 分鐘。

## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定單一登入](active-directory-saas-jive-tutorial.md)
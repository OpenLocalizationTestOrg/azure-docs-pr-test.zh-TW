---
title: "教學課程：Azure Active Directory 與 Citrix GoToMeeting 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Citrix GoToMeeting 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a>教學課程︰設定自動使用者佈建的 Citrix GoToMeeting

本教學課程的 hello 目標是 tooshow hello 需要 tooperform Citrix GoToMeeting 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooCitrix GoToMeeting 中的步驟。

## <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

*   Azure Active Directory 租用戶。
*   已啟用 Citrix GoToMeeting 單一登入的訂用帳戶。
*   具有小組系統管理員權限的 Citrix GoToMeeting 使用者帳戶。

## <a name="assigning-users-toocitrix-gotomeeting"></a>指派使用者 tooCitrix GoToMeeting

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。

之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooyour Citrix GoToMeeting 的應用程式。 一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Citrix GoToMeeting 的應用程式：

[指派使用者或群組的 tooan 企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a>指派使用者 tooCitrix GoToMeeting 的重要秘訣

*   建議在單一 tooCitrix GoToMeeting tootest hello 佈建組態指派給 Azure AD 使用者。 其他使用者及/或群組可能會稍後再指派。

*   指派使用者 tooCitrix GoToMeeting 時，您必須選取有效的使用者角色。 hello 「 預設的存取 」 角色不適用於佈建。

## <a name="enable-automated-user-provisioning"></a>啟用自動使用者佈建

本節會引導您完成連接您 Azure AD tooCitrix GoToMeeting 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello，更新，請停用指派的使用者帳戶 Citrix GoToMeeting 中的根據使用者和群組Azure AD 中的指派。

> [!TIP]
> 您也可以選擇 tooenabled SAML 型單一登入 Citrix gotomeeting，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure 自動帳戶佈建使用者：

1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。

2. 如果您已經設定進行單一登入 Citrix GoToMeeting，搜尋您使用 hello 搜尋欄位中的 Citrix GoToMeeting 的執行個體。 否則，請選取**新增**並搜尋**Citrix GoToMeeting** hello 應用程式庫中。 從 hello 搜尋結果中，選取 Citrix GoToMeeting，並將它新增 tooyour 的應用程式的清單。

3. 選取您的 Citrix GoToMeeting 的執行個體，然後選取 hello**佈建** 索引標籤。

4. 設定 hello**佈建**模式太**自動**。 

    ![佈建](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. 在下 hello 系統管理員認證 區段中，執行下列步驟的 hello:
   
    a. 在 hello **Citrix GoToMeeting 系統管理員使用者名稱**文字方塊中，輸入 hello 的使用者名稱的系統管理員。

    b. 在 [hello **Citrix GoToMeeting 管理員密碼**hello 系統管理員密碼] 文字方塊中。

6. 在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 可連接 tooyour Citrix GoToMeeting 的應用程式。 如果 hello 連線失敗，請確定您的 Citrix GoToMeeting 帳戶具有小組系統管理員權限，然後再次嘗試 hello **[系統管理認證]**步驟一次。

7. 輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊。

8. 按一下 [儲存]。

9. 在 hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooCitrix GoToMeeting。**

10. 在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooCitrix GoToMeeting 同步。 hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在 Citrix GoToMeeting 中進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

11. tooenable hello Azure AD 佈建服務 Citrix gotomeeting，變更 hello**佈建狀態**太**上**hello 設定 區段中

12. 按一下 [儲存]。

啟動 hello 初始同步處理的任何使用者和/或群組指派 tooCitrix GoToMeeting hello 使用者和群組 區段中。 hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。 您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Citrix GoToMeeting 的應用程式上執行的所有動作。

## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定單一登入](active-directory-saas-citrix-gotomeeting-tutorial.md)



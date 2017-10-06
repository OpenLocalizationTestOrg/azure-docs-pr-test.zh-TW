---
title: "教學課程：Azure Active Directory 與 Concur 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Concur 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a>教學課程：設定 Concur 的使用者佈建

本教學課程的 hello 目標是 tooshow hello 需要 tooperform Concur 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooConcur 中的步驟。

## <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

*   Azure Active Directory 租用戶。
*   已啟用 Concur 單一登入的訂用帳戶。
*   具有小組系統管理員權限的 Concur 使用者帳戶。

## <a name="assigning-users-tooconcur"></a>指派使用者 tooConcur

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。

之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour Concur 的應用程式中的群組。 一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Concur 應用程式：

[指派使用者或群組的 tooan 企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a>指派使用者 tooConcur 的重要秘訣

*   建議在單一 Azure AD 使用者被指派 tooConcur tootest hello 佈建的組態。 其他使用者及/或群組可能會稍後再指派。

*   指派使用者 tooConcur 時，您必須選取有效的使用者角色。 hello 「 預設的存取 」 角色不適用於佈建。

## <a name="enable-user-provisioning"></a>啟用使用者佈建

本節會引導您完成連接您的 Azure AD tooConcur 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用 Azure AD 中的使用者和群組指派為基礎的 Concur 中指派的使用者帳戶。

> [!Tip] 
> 您也可以選擇 tooenabled SAML 型單一登入 concur，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure 使用者帳戶佈建：

hello 本節目標在於 toooutline 如何 tooenable 佈建的 Active Directory 使用者帳戶 tooConcur。

tooenable 應用程式在 hello 費用的服務，有 toobe 適當設定並使用 Web 服務系統管理員設定檔。 請勿將加入 hello WS 管理員角色 tooyour 現有系統管理員設定檔，您用於 t&e 管理功能。

Concur 顧問或 hello 用戶端系統管理員必須建立不同的 Web 服務系統管理員設定檔和 hello 用戶端系統管理員必須使用此設定檔的 hello Web 服務系統管理員的功能 （例如，啟用應用程式）。 這些設定檔必須有所區隔 hello 用戶端系統管理員的每日 t&e 系統管理員設定檔 （hello T & 電子管理員設定檔不應該有 hello T&e 角色指派）。

當您建立 hello 設定檔 toobe 用於啟用 hello 應用程式時，輸入 hello 使用者設定檔欄位 hello 用戶端系統管理員的名稱。 這會指派擁有權 toohello 設定檔。 一旦建立一或多個設定檔，hello 用戶端必須登入這個設定檔 tooclick hello"*啟用*"合作夥伴應用程式內 hello Web 服務] 功能表上的按鈕。

Hello 下列原因，此動作不應該與用於一般 t&e 管理 hello 設定檔。

* hello 用戶端有 toobe hello 按下的其中一個"*是*"上的應用程式啟用後會顯示 hello 對話方塊視窗。 此點選動作 hello 用戶端願意 hello 協力廠商應用程式 tooaccess 針對其資料，讓您或使用 hello 夥伴不能按一下 [是] 按鈕，可確認。

* 如果已啟用使用 hello T & 電子管理員設定檔的應用程式的用戶端系統管理員離開 hello 公司 （導致 hello 設定檔正在停用狀態），使用該設定檔啟用任何應用程式無法運作 hello 應用程式啟用與另一個使用中的 WS 管理員之前設定檔。 這就是為什麼您應該 toocreate 相異 WS 管理員設定檔。

* 如果系統管理員離開 hello 公司，hello 名稱相關聯的 toohello WS 管理員設定檔可以變更的 toohello 取代系統管理員，視需要而不會影響 hello 啟用應用程式因為該設定檔不需要停用狀態。

**tooconfigure 使用者佈建，執行下列步驟的 hello:**

1. 登入 tooyour **Concur**租用戶。

2. 從 hello**管理**功能表上，選取**Web 服務**。
   
    ![Concur 租用戶](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur 租用戶")

3. 在左方、 從 hello hello **Web 服務**窗格中，選取**啟用夥伴應用程式**。
   
    ![啟用合作夥伴應用程式](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "啟用合作夥伴應用程式")

4. 從 hello**啟用應用程式**清單中，選取**Azure Active Directory**，然後按一下 [**啟用**。
   
    ![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")

5. 按一下**是**tooclose hello**確認動作**對話方塊。
   
    ![確認動作](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "確認動作")

6. 在 [hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。

7. 如果您已經設定進行單一登入 Concur，搜尋您的 Concur 使用 hello 搜尋欄位中的執行個體。 否則，請選取**新增**並搜尋**Concur** hello 應用程式庫中。 從 hello 搜尋結果中，選取 [Concur，並將它新增 tooyour 的應用程式的清單。

8. 選取您的 Concur，執行個體，然後選取 hello**佈建**] 索引標籤。

9. 設定 hello**佈建模式**太**自動**。 
 
    ![佈建](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. 在 hello**系統管理員認證**區段中，輸入 hello**使用者名**和 hello**密碼**Concur 系統管理員。

11. 在 [hello Azure 入口網站，按一下 [**測試連接**tooensure Azure AD 的 tooyour Concur 的應用程式可以連接。 如果 hello 連線失敗，請確定您的 Concur 帳戶具有小組系統管理員權限。

12. 輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊。

13. 按一下 [儲存]。

14. 在 [hello 對應區段中，選取**tooConcur 同步處理 Azure Active Directory 使用者。**

15. 在 [hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooConcur 同步。 hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在 Concur 中進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

16. tooenable hello Azure AD 佈建服務 concur，變更 hello**佈建狀態**太**上**在 hello**設定**區段

17. 按一下 [儲存]。

您現在可以建立測試帳戶了。 等候總 tooverify hello 帳戶已經過同步處理 tooConcur too20 分鐘。

## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定單一登入](active-directory-saas-concur-tutorial.md)


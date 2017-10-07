---
title: "教學課程：Azure Active Directory 與 Box 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與方塊之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e92baabb174642c22c99e2a30bc9c71845b3b75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a>教學課程︰設定自動使用者佈建的 Box

本教學課程的 hello 目標是在您需要在方塊和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooBox tooperform tooshow hello 步驟。

## <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

*   Azure Active Directory 租用戶。
*   已啟用 Box 單一登入功能的訂用帳戶。
*   具有小組系統管理員權限的 Box 使用者帳戶。

## <a name="assigning-users-toobox"></a>指派使用者 tooBox 

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。

之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour Box 應用程式中的群組。 一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Box 應用程式：

[指派使用者或群組的 tooan 企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a>指派使用者和群組
hello**方塊 > 使用者和群組**hello Azure 入口網站中的索引標籤可讓您的使用者和群組應該被授與存取 tooBox toospecify。 使用者或群組的指派會導致下列項目 toooccur hello:

* Azure AD 可允許 hello 指派使用者 （無論是直接指派或群組成員資格） tooauthenticate tooBox。 如果未指派使用者，Azure AD 不允許它們 toosign tooBox 中，並在 hello Azure AD 登入頁面上會傳回錯誤。
* 方塊的應用程式磚加入 toohello 使用者[應用程式啟動器](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)。
* 如果已啟用自動佈建，然後 hello 指派使用者和/或群組加入 toohello 佈建佇列 toobe 自動佈建。
  
  * 如果只有使用者物件已設定的 toobe 佈建，然後在 hello 佈建佇列中，位於所有直接指派的使用者和任何指派的群組成員的所有使用者會都放在 hello 佈建佇列。 
  * 如果已設定的 toobe 佈建群組物件，然後所有指派的群組物件是佈建的 tooBox 和群組成員的所有使用者。 hello 群組和使用者成員資格會保留在時寫入 tooBox。

您可以使用 hello**屬性 > 單一登入**索引標籤上的使用者屬性 （或宣告） 會呈現在 SAML 為基礎的驗證和 hello tooBox tooconfigure**屬性 > 佈建**從 Azure AD tooBox 使用者和群組屬性流程佈建作業期間如何 tooconfigure 索引標籤。

### <a name="important-tips-for-assigning-users-toobox"></a>指派使用者 tooBox 的重要秘訣 

*   建議單一 Azure AD 使用者指派 tooBox tootest hello 佈建的組態。 其他使用者及/或群組可能會稍後再指派。

*   指派使用者 toobox 時，您必須選取有效的使用者角色。 hello 「 預設的存取 」 角色不適用於佈建。

## <a name="enable-automated-user-provisioning"></a>啟用自動使用者佈建

本節引導連接您的 Azure AD tooBox 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用根據 Azure AD 中的使用者和群組指派 方塊中的指派的使用者帳戶。

如果已啟用自動佈建，然後 hello 指派使用者和/或群組加入 toohello 佈建佇列 toobe 自動佈建。
    
 * 如果只有使用者物件設定的 toobe 佈建，然後直接指派的使用者會放入 hello 佈建的佇列，並置於 hello 佈建佇列的任何指派的群組成員的所有使用者。 
    
 * 如果已設定的 toobe 佈建群組物件，然後所有指派的群組物件是佈建的 tooBox 和群組成員的所有使用者。 hello 群組和使用者成員資格會保留在時寫入 tooBox。

> [!TIP] 
> 您也可以選擇 SAML 型單一登入方塊中，遵循所提供的 hello 指示 tooenabled [Azure 入口網站](https://portal.azure.com)。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure 自動帳戶佈建使用者：

hello 本節目標在於 toooutline 如何 tooenable 佈建的 Active Directory 使用者帳戶 tooBox。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。

2. 如果您已經進行單一登入設定 方塊中，搜尋方塊中，使用 hello 搜尋欄位中的執行個體。 否則，請選取**新增**並搜尋**方塊**hello 應用程式庫中。 從 hello 搜尋結果中，選取方塊，並將它新增 tooyour 的應用程式的清單。

3. 選取您的執行個體的方塊，然後選取 hello**佈建** 索引標籤。

4. 設定 hello**佈建模式**太**自動**。 

    ![佈建](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. 在 hello**系統管理員認證**區段中，按一下**授權**tooopen 新的瀏覽器視窗中的登入對話方塊。

6. 在 hello**登入 toogrant 存取 tooBox**頁面上，提供所需的 hello 認證，然後按一下**授權**。 
   
    ![啟用自動使用者佈建](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "啟用自動使用者佈建")

7. 按一下**授與存取 tooBox** tooauthorize 此作業並 tooreturn toohello Azure 入口網站。 
   
    ![啟用自動使用者佈建](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "啟用自動使用者佈建")

8. 在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 可連接 tooyour Box 應用程式。 如果 hello 連線失敗，請確定您的 Box 帳戶具有小組系統管理員權限，然後再次嘗試 hello **「 授權 」**步驟一次。

9. 輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊。

10. 按一下 [儲存]。

11. 在 hello 對應區段中，選取**tooBox 同步處理 Azure Active Directory 使用者。**

12. 在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooBox 同步。 hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶 方塊中進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

13. tooenable hello Azure AD 佈建服務 方塊中，變更 hello**佈建狀態**太**上**hello 設定 區段中

14. 按一下 [儲存]。

啟動 hello 初始同步任何的處理使用者和/或群組指派 tooBox 在 hello 使用者和群組 > 一節。 hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。 您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述 hello 佈建服務應用程式 方塊上的所執行的所有動作。

您現在可以建立測試帳戶了。 等候總 tooverify hello 帳戶已經過同步處理 toobox too20 分鐘。

Box 租用戶中已同步處理的使用者會列在**受管理的使用者**在 hello**管理主控台**。

![整合狀態](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "整合狀態")


## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定單一登入](active-directory-saas-box-tutorial.md)
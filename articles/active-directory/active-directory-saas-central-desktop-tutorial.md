---
title: "教學課程：Azure Active Directory 與 Central Desktop 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Central Desktop 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a>教學課程：Azure Active Directory 與 Central Desktop 整合
本教學課程的 hello 目標是 Azure 與 Central Desktop tooshow hello 整合。 本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

* 有效的 Azure 訂閱
* 啟用 Central Desktop 單一登入的訂用帳戶/Central Desktop 租用戶

本教學課程所述的 hello 案例包含下列建置組塊的 hello:

* 啟用 Central Desktop 的 hello 應用程式整合
* 設定單一登入 (SSO)
* 設定使用者佈建
* 指派使用者

![案例](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "案例")

## <a name="enable-hello-application-integration-for-central-desktop"></a>啟用 Central Desktop 的 hello 應用程式整合
本節 hello 目標是 toooutline 如何 Central Desktop tooenable hello 應用程式整合。

**tooenable hello 應用程式整合 Central desktop，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。
   
   ![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
   ![應用程式](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "應用程式")
4. 按一下**新增**hello hello 頁底端。
   
   ![新增應用程式](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "新增應用程式")
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
   ![從資源庫新增應用程式](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "從資源庫新增應用程式")
6. 在 hello**搜尋方塊**，型別**Central Desktop**。
   
   ![應用程式資源庫](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "應用程式資源庫")
7. 在 hello 結果窗格中，選取  **Central Desktop**，然後按一下**完成**tooadd hello 應用程式。
   
   ![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")
   
## <a name="configure-single-sign-on"></a>設定單一登入

hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooCentral 桌面的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。

此程序的一部分，您就需要的 tooupload base 64 編碼的憑證 tooyour Central Desktop 租用戶。  
如果您不熟悉這個程序，請參閱[如何 tooconvert 二進位憑證到文字檔](http://youtu.be/PlgrzUZ-Y1o)。

**tooconfigure 單一登入，請執行下列步驟的 hello:**

1. 在 Azure 傳統入口網站，在 hello hello **Central Desktop**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello * * 設定單一登入 * * 對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "設定單一登入")
2. 在 hello**如何想您使用者 toosign tooCentral 桌面上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
   ![設定單一登入](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "設定單一登入")
3. 在 hello**設定應用程式 URL**頁面上，執行下列步驟，hello，然後按一下**下一步**: 
   
   1. 在 hello **Central Desktop 登入 URL**文字方塊中，您的 Central Desktop 租用戶的型別 hello URL (例如： *http://contoso.centraldesktop.com*)。
   2. 在 [hello Central Desktop 回覆 URL] 文字方塊中，輸入您的 Central Desktop AssertionConsumerService URL (例如： https://contoso.centraldesktop.com/saml2-assertion.php)。
   
   >[!NOTE]
   >您可以從 hello central desktop 中繼資料取得 hello 值 (例如： *http://contoso.centraldesktop.com*)。
   >  
   
   ![設定應用程式 URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "設定應用程式 URL")
4. 在 hello**於 Central Desktop 設定單一登入**頁面、 toodownload 憑證，請按一下**下載憑證**，然後儲存您的電腦上的 hello 憑證檔案。
   
  ![設定單一登入](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "設定單一登入")
5. 登入 tooyour **Central Desktop**租用戶。
6. 跳過**設定**，按一下 **進階**，然後按一下**單一登入**。
   
  ![設定 - 進階](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "設定 - 進階")
7. 在 hello**單一登入設定**頁面上，執行下列步驟的 hello:
   
  ![單一登入設定](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "單一登入設定")
   
  1. 選取 [啟用 SAML v2 單一登入] 。
  2. 在 Azure 傳統入口網站，在 hello hello**於 Central Desktop 設定單一登入**頁面上，複製 hello**簽發者 URL**值並貼到 hello **SSO URL**文字方塊。
  3. 在 Azure 傳統入口網站，在 hello hello**於 Central Desktop 設定單一登入**頁面上，複製 hello**遠端登入 URL**值並貼到 hello **SSO 登入 URL**文字方塊。
  4. 在 Azure 傳統入口網站，在 hello hello**於 Central Desktop 設定單一登入**頁面上，複製 hello**單一登出服務 URL**值並貼到 hello **SSO 登出 URL**文字方塊。
8. 在 hello**訊息簽章驗證方法**區段中，執行下列步驟的 hello:
   
   ![訊息簽章驗證方法](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "訊息簽章驗證方法")
   
  1. 選取 [憑證] 。
  2. 從 hello **SSO 憑證**清單中，選取**RSH SHA256**。
  3. 從 hello 下載的憑證，複製 hello 內容的 hello 文字檔案，請建立文字檔，然後將它貼到 hello **SSO 憑證**欄位。  
     >[!TIP]
     >如需詳細資訊，請參閱[如何 tooconvert 二進位憑證到文字檔案](http://youtu.be/PlgrzUZ-Y1o)
      >  
   4. 選取**顯示連結 tooyour SAMLv2 登入頁面**。
9. 按一下 [更新] 。
10. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。
    
    ![設定單一登入](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "設定單一登入")
    
## <a name="configure-user-provisioning"></a>設定使用者佈建

AAD 使用者 toobe 無法 toosign 中，它們必須已佈建的 toohello Central Desktop 應用程式。 本章節描述如何 toocreate AAD 使用者帳戶在 Central Desktop。

**使用者帳戶 tooCentral 桌面 tooprovision:**
1. 登入 tooyour Central Desktop 租用戶。
2. 跳過**人員\>內部成員**。
3. 按一下 [加入內部成員] 。
   
  ![人員](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "人員")
4. 在 hello**新成員的電子郵件地址**文字方塊中，輸入您想 tooprovision，，然後按一下的 AAD 帳戶**下一步**。
   
  ![新成員的電子郵件地址](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "新成員的電子郵件地址")
5. 按一下 [加入內部成員] 。
   
  ![加入內部成員](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "加入內部成員")
   
   >[!NOTE]
   >您加入的 hello 使用者會收到電子郵件，其中包含確認連結需要他們點 tooclick tooactivate hello 帳戶。
   > 

>[!NOTE]
>您可以使用任何其他 Central Desktop 使用者帳戶建立工具或 Api 提供 Central Desktop tooprovision AAD 使用者帳戶
>  

## <a name="assign-users"></a>指派使用者
tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。

**tooassign 使用者 tooCentral Desktop 中，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，建立測試帳戶。
2. 在 hello **Central Desktop**應用程式整合頁面上，按一下 **指派使用者**。
   
   ![指派使用者](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "指派使用者")
3. 選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。
   
   ![是](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "是")

如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。


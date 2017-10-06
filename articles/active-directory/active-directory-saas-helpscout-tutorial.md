---
title: "教學課程：Azure Active Directory 與 Help Scout 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與協助 Scout 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a>教學課程：Azure Active Directory 與 Help Scout 整合

在本教學課程中，您學習如何 toointegrate 協助搜索與 Azure Active Directory (Azure AD)。

您會收到 hello 協助 Scout 整合與 Azure AD 中的下列優點：

- 在 Azure AD 中，您可以控制誰可以存取 tooHelp Scout。
- 您可以自動登入您的使用者 tooHelp Scout 使用單一登入和使用者的 Azure AD 帳戶。
- 您可以管理您的帳戶，在一個集中位置，hello Azure 入口網站。

toolearn 進一步了解軟體即服務 (SaaS) 應用程式與 Azure AD 整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

Azure AD 整合，以協助搜索 tooset，您需要下列項目 hello:

- Azure AD 訂用帳戶
- Help Scout 訂用帳戶，並開啟單一登入 

> [!NOTE]
> 如果您在測試 hello 步驟在本教學課程，我們建議您不要在生產環境中測試它們。

測試本教學課程中的 hello 步驟建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，可以[取得一個月的免費試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 

本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫新增協助搜索。
2. 設定和測試 Azure AD 單一登入。

## <a name="add-help-scout-from-hello-gallery"></a>從 hello 圖庫新增協助 Scout
協助 Scout 與 Azure AD，hello 圖庫中的 hello 整合 tooset 協助 Scout tooyour 之新增受管理的 SaaS 應用程式。

tooadd 協助 Scout 從 hello 組件庫：

1. 在 hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的功能表中選取**Azure Active Directory**。 

    ![hello Azure Active Directory 按鈕][1]

2. 選取 [企業應用程式]，然後選取 [所有應用程式]。

    ![hello 企業應用程式 頁面][2]
    
3. tooadd 新的應用程式中，選取**新的應用程式**。

    ![hello 新應用程式按鈕][3]

4. 在 [hello] 搜尋方塊中，輸入**協助 Scout**。 在 hello 搜尋結果中，選取 **協助 Scout**，然後選取**新增**。

    ![協助 Scout hello [結果] 清單中](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 Britta Simon 的測試使用者作為基礎，設定及測試與 Help Scout 搭配運作的 Azure AD 單一登入。

Azure AD 單一登入 toowork，需要 tooknow hello Azure AD 中協助搜索的對等項目的使用者。 必須先建立 Azure AD 使用者與協助 Scout 中的 hello 相關的使用者之間的連結關聯性。

tooestablish hello 連結關聯性，以協助搜索，適用於**Username**，hello hello 值指派**使用者名**在 Azure AD 中。

tooconfigure 和測試 Azure AD 單一登入以協助搜索，完成下列工作的 hello:

1. [設定 Azure AD 單一登入](#set-up-azure-ad-single-sign-on)。 設定使用者 toouse 這項功能。
2. [建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)。 測試 Azure AD 單一登入與 hello 使用者許 Simon。
3. [建立 Help Scout 測試使用者](#create-a-help-scout-test-user)。 協助 Scout 是連結的 toohello hello 使用者表示 Azure AD 中建立許 Simon 對應項目。
4. [指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)。 設定 Azure AD 單一登入許 Simon toouse。
5. [測試單一登入](#test-single-sign-on)。 請確認該 hello 設定可正常運作。

### <a name="set-up-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您設定 Azure AD 單一登入 hello Azure 入口網站中。 然後，您要在 Help Scout 應用程式中設定單一登入。

Azure AD 單一登入以協助搜索 tooset:

1. 在 Azure 入口網站上 hello hello**協助 Scout**應用程式整合頁面上，選取**單一登入**。
 
    ![設定單一登入連結][4]

2. 在 hello**單一登入** 頁面上，針對**模式**，選取**SAML 型登入**。
 
    ![單一登入對話方塊](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. 在下**協助 Scout 網域和 Url**，如果您想 tooset hello 應用程式在 IDP 初始化模式中，完成下列步驟的 hello:

    1. 在 hello**識別碼**方塊中，輸入 URL，其中具有 hello 下列模式：`urn:auth0:helpscout:<instancename>`

    2. 在 hello**回覆 URL**方塊中，輸入 URL，其中具有 hello 下列模式：`https://helpscout.auth0.com/login/callback?connection=<instancename>`

    ![Help Scout 網域與 URL 單一登入資訊](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. 如果您想 tooset hello 應用程式在 SP 初始模式中，選取 hello**顯示進階的 URL 設定**核取方塊，並執行再 hello 遵循：

    * 在 hello**登入 URL**方塊中，輸入 URL，其中具有下列格式的 hello:`https://secure.helpscout.net/members/login/`

    ![Help Scout 網域與 URL 單一登入資訊](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > 這些 Url 中的 hello 值為僅供示範之。 更新 hello 值與 hello 實際的識別項 URL 和回覆 URL。 tooget 這些值，請連絡[協助 Scout 支援小組](mailto:help@helpscout.com)。 

5. 在下**SAML 簽章憑證**，選取**中繼資料 XML**，然後儲存您的電腦上的 hello 中繼資料檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. 選取 [ **儲存**]。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. tooset 設定單一登入 hello 協助 Scout 端、 傳送嗨下載中繼資料 XML 檔案 toohello[協助 Scout 支援小組](mailto:help@helpscout.com)。 hello 協助 Scout 支援小組適用於這項設定，以便雙方 hello SAML 單一登入連接已正確設定。

> [!TIP]
> 您可以讀取這些指示 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定您的應用程式 ！ 選取 [新增 hello 應用程式之後**Active Directory** > **企業應用程式**，選取 hello**單一登入**] 索引標籤。您可以存取 hello 內嵌文件以 hello**組態**區段中的，在 hello hello 頁面底部。 如需詳細資訊，請參閱 [Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)。

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

在本節中的 hello Azure 入口網站，您會建立名為許 Simon 的測試使用者。

![建立 Azure AD 測試使用者][100]

toocreate 在 Azure AD 中的測試使用者：

1. 在 hello Azure 入口網站，在 hello 左功能表中，選取  **Azure Active Directory**。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. toodisplay hello 使用者清單，選取**使用者和群組**，然後選取**所有使用者**。

    ![選取 [使用者和群組]，然後選取 [所有使用者]](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. tooopen hello**使用者**對話方塊頂端的 hello hello**所有使用者**頁面上，選取**新增**。

    ![hello [新增] 按鈕](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. 在 hello**使用者**對話方塊中，完成下列步驟的 hello:

    1. 在 hello**名稱**方塊中，輸入**BrittaSimon**。

    2. 在 hello**使用者名**方塊中，輸入使用者許 Simon hello 電子郵件地址。

    3. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。

    4. 選取 [ **建立**]。

        ![hello [使用者] 對話方塊](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a>建立 Help Scout 測試使用者

本章節的 hello 物件是 toocreate 名為許 Simon 協助 Scout 中的使用者。 Help Scout 支援預設啟用的 Just-In-Time (JIT) 佈建。

在本節中，沒有任何動作或工作 toocomplete。 如果使用者不存在於協助 Scout，當您嘗試 tooaccess 協助 Scout 被建立一個新。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您允許 hello 使用者許 Simon toouse Azure AD 單一登入授與 hello 使用者帳戶存取 tooHelp Scout。

![指派 hello 使用者角色][200] 

tooassign 許 Simon tooHelp Scout:

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，並前往 toohello 目錄檢視。 選取 [企業應用程式]，然後選取 [所有應用程式]。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**協助 Scout**。

    ![hello 應用程式清單中的 hello 協助 Scout 連結](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. 在 hello 左窗格中，選取 **使用者和群組**。

    ![hello 使用者和群組連結][202]

4. 選取 [新增] 。 然後，在 hello**將作業加入**頁面上，選取**使用者和群組**。

    ![hello 將作業加入窗格][203]

5. 在 hello**使用者和群組**頁面 hello 清單中的使用者，選取**許 Simon**。

6. 在 hello**使用者和群組**頁面上，選取**選取**。

7. 在 hello**將作業加入**頁面上，選取**指派**。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您測試您 Azure AD 單一登入組態使用 hello 存取面板。

當您選取 hello 協助 Scout 磚 hello 存取面板中時，您應該會自動登入 tooyour 協助 Scout 應用程式。

如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png


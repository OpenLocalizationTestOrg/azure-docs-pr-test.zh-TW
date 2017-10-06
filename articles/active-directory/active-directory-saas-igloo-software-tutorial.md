---
title: "教學課程：Azure Active Directory 與 Igloo Software 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Igloo Software 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a>教學課程：Azure Active Directory 與 Igloo Software 整合

在此教學課程中，您學會如何 toointegrate Igloo Software 與 Azure Active Directory (Azure AD)。

整合 Azure AD 與 Igloo Software 可以提供下列優點 hello:

- 您可以控制存取 tooIgloo 軟體的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooIgloo （單一登入） 的軟體與他們的 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 Igloo Software 的整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Igloo Software 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Igloo Software
2. 設定並測試 Azure AD 單一登入

## <a name="adding-igloo-software-from-hello-gallery"></a>從 hello 圖庫加入 Igloo Software
tooconfigure hello 整合 Igloo Software 的 Azure AD，您需要 tooadd Igloo Software hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Igloo Software 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Igloo Software**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. 在 hello 結果 窗格中，選取  **Igloo Software**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Igloo Software 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 對應項目中 Igloo Software 的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 Igloo Software 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

Igloo Software 中指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 Azure AD 單一登入與 Igloo Software 的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Igloo Software](#creating-an-igloo-software-test-user)**  -toohave 許 Simon Igloo Software 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Igloo Software 的應用程式中。

**tooconfigure Azure AD 單一登入與 Igloo Software，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Igloo Software**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. 在 hello **Igloo 軟體網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.igloocommmunities.com`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.igloocommmunities.com/saml.digest`

    c. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.igloocommmunities.com/saml.digest`

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。 請連絡[Igloo 軟體用戶端支援小組](https://www.igloosoftware.com/services/support)tooget 這些值。 

4. 在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. 在 hello **Igloo 軟體組態**區段中，按一下**設定 Igloo Software** tooopen**設定登入**視窗。 複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. 在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour Igloo Software 公司網站。

8. 移 toohello**控制台**。
   
     ![控制台](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "控制台")

9. 在 hello**成員資格**索引標籤上，按一下 **登入設定**。
   
    ![登入設定](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "登入設定")

10. 在 hello SAML 組態 區段中，按一下 **設定 SAML 驗證**。
   
    ![SAML 設定](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML 設定")
   
11. 在 hello**一般組態**區段中，執行下列步驟的 hello:
   
    ![一般組態](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "一般組態")

    a. 在 hello**連接名稱**文字方塊中，輸入您的組態的自訂名稱。
   
    b. 在 hello **IdP 登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。
   
    c. 在 hello **IdP 登出 URL**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。
    
    d. 選取 [登出回應與要求 HTTP 類型] 作為 [POST]。
   
    e. 開啟您**base-64**編碼從 Azure 入口網站中，複製到剪貼簿，其內容的 hello 下載 [記事本] 中的憑證，然後將它貼入 toohello**公開憑證**文字方塊。
    
12. 在 hello**回應和驗證設定**，執行下列步驟的 hello:
    
    ![回應和驗證設定](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "回應和驗證設定")
  
      a. 在 [識別提供者]，選取 [Microsoft ADFS]。
      
      b.這是另一個 C# 主控台應用程式。 在 [識別元類型]，選取 [電子郵件地址]。 

      c. 在 hello**電子郵件屬性**文字方塊中，輸入**emailaddress**。

      d. 在 hello**名字屬性**文字方塊中，輸入**givenname**。

      e. 在 hello**姓氏**文字方塊中，輸入**姓氏**。

13. 執行下列步驟 toocomplete hello 組態 hello:
    
    ![登入時建立使用者](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "登入時建立使用者") 

     a. 在 [登入時建立使用者]，選取 [使用者登入您的網站時建立新的使用者]。

     b.這是另一個 C# 主控台應用程式。 在 [登入設定]，選取 [在「登入」畫面使用 SAML 按鈕]。

     c. 按一下 [儲存] 。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-an-igloo-software-test-user"></a>建立 Igloo Software 測試使用者

沒有您 tooconfigure 使用者佈建 tooIgloo 軟體的動作項目。  

當指派的使用者嘗試 toolog 中 tooIgloo 軟體使用 hello 存取面板，Igloo Software 會檢查 hello 使用者是否存在。  如果尚無可用的使用者帳戶，Igloo Software 會自動予以建立。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooIgloo 軟體。

![指派使用者][200] 

**tooassign 許 Simon tooIgloo 軟體，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Igloo Software**。

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello Igloo Software 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 Igloo Software 的應用程式。
如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png


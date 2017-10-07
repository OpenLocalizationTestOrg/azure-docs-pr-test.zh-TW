---
title: "教學課程：Azure Active Directory 與 iLMS 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 iLMS 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a>教學課程：Azure Active Directory 與 iLMS 整合

在此教學課程中，您學會如何 toointegrate iLMS 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 iLMS 可以提供下列優點 hello:

- 您可以控制存取 tooiLMS Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooiLMS （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure iLMS 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 iLMS 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 iLMS
2. 設定並測試 Azure AD 單一登入

## <a name="adding-ilms-from-hello-gallery"></a>從 hello 圖庫加入 iLMS
tooconfigure hello 整合 iLMS 到 Azure AD，您需要 tooadd iLMS hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd iLMS 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**iLMS**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. 在 hello 結果 窗格中，選取  **iLMS**，然後按一下 **新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 iLMS 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 iLMS 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello iLMS 中相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** iLMS 中。

tooconfigure 及 iLMS 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 iLMS](#creating-an-ilms-test-user)**  -toohave 是連結的 toohello Azure AD 表示她的 iLMS 的許 Simon 的對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 iLMS 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 iLMS，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **iLMS**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. 在 hello **iLMS 網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    a. 在 hello**識別碼**文字方塊中，貼上 hello**識別碼**您複製的值**服務提供者**iLMS 系統管理入口網站中的 SAML 設定 區段。

    b. 在 [hello**回覆 URL**文字方塊中，貼上 hello**端點 (URL)**您複製的值**服務提供者**iLMS 擁有 hello 下列的系統管理員入口網站中的 SAML 設定] 區段模式`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`

    >[!Note]
    >這個 '123456' 是識別項的範例值。

4. 請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    在 hello**登入 URL**文字方塊中，貼上 hello**端點 (URL)**您複製的值**服務提供者**SAML 設定在為 iLMS 管理入口網站中的區段`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`     

5. tooenable JIT 佈建，iLMS 應用程式預期 hello SAML 判斷提示以特定格式。 設定下列宣告為此應用程式的 hello。 您可以從 hello 管理這些屬性的 hello 值**使用者屬性**應用程式整合頁面上的一節。 hello 下列螢幕擷取畫面會顯示這個範例。
    
    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/4.png)
    
    建立**部門、 區域**和**除法**屬性並新增 iLMS hello 的這些屬性的名稱。 上述的所有屬性都是必要屬性。    

    > [!NOTE] 
    > 您有 tooenable**建立 Un-recognized 使用者帳戶**iLMS toomap 中這些屬性。 請依照下列指示 hello[這裡](http://support.inspiredelearning.com/customer/portal/articles/2204526)tooget hello 屬性設定了解。

6. 在 hello**使用者屬性**區段 hello**單一登入** 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:
    
    | 屬性名稱 | 屬性值 |
    | ---------------| --------------- |    
    | division | user.department |
    | region | user.state |
    | department | user.jobtitle |

    a. 按一下**加入屬性**tooopen hello**加入屬性**對話方塊。

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    b. 在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。
    
    c. 從 hello**值**清單，顯示該資料列的型別 hello 屬性值。
    
    d. 按一下 [確定]。

7. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. 在不同的網頁瀏覽器視窗中，登入 tooyour **iLMS 管理入口**身為系統管理員。

10. 按一下**SSO:SAML**下**設定**tooopen SAML 設定 索引標籤，並執行下列步驟的 hello:
    
    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/1.png) 

    a. 展開 hello**服務提供者**> 一節，並複製 hello**識別碼**和**端點 (URL)**值。

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/2.png) 

    b. 在 [識別提供者] 區段中，按一下 [匯入中繼資料]。
    
    c. 選取 hello**中繼資料**從 Azure 入口網站下載檔案**SAML 簽章憑證**> 一節。

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    d. 如果您想 tooenable JIT 為佈建 toocreate iLMS 帳戶取消-辨識使用者，請遵循下列步驟：
        
       - 請勾選 [建立無法辨識的使用者帳戶]。
       
       ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  Azure AD 與 iLMS 中的 hello 屬性會對應 hello 屬性。 在 hello 屬性資料行，指定 hello 屬性名稱或 hello 預設值。

    e. 跳過**商務規則**索引標籤，然後執行下列步驟的 hello: 
        
       ![設定單一登入](./media/active-directory-saas-ilms-tutorial/5.png)

       - 請檢查**建立 Un-recognized 區域、 單位和部門**toocreate 區域，以及不存在時的單一登入 hello 的部門。
        
       - 請檢查**更新使用者設定檔期間登入**toospecify 是否 hello 使用者設定檔會更新每個單一登入。 
        
       - 如果 hello **「 更新空白值的非必要欄位在使用者設定檔 」**核取選項，選擇性的設定檔的欄位空白時登入將也會導致 hello 使用者 iLMS 設定檔 toocontain 空白值，這些欄位。
        
       - 請檢查**傳送錯誤通知電子郵件**，然後輸入 hello 電子郵件的 hello 使用者希望 tooreceive hello 錯誤通知的電子郵件。

11. 按一下**儲存**按鈕 toosave hello 設定。

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
    
### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-an-ilms-test-user"></a>建立 iLMS 測試使用者

應用程式支援恰好在即時使用者佈建，以及之後驗證使用者會自動建立 hello 應用程式中。 JIT 也能運作，如果您已按下 hello**建立 Un-recognized 使用者帳戶**iLMS 系統管理入口網站在 SAML 組態設定期間的核取方塊。

若要手動 toocreate 使用者，然後依照下列步驟：

1. 系統管理員身分登入 tooyour iLMS 公司網站。

2. 按一下**「 註冊使用者 」**下**使用者**索引標籤上 tooopen**註冊使用者**頁面。 
   
   ![新增員工](./media/active-directory-saas-ilms-tutorial/3.png)

3. 在 hello **「 註冊使用者 」**頁面上，執行下列步驟的 hello。

    ![新增員工](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    a. 在 hello**名字**文字方塊中，型別 hello 名字許。
   
    b. 在 hello**姓氏**文字方塊中，型別 hello 姓氏 Simon。

    c. 在 [hello**電子郵件識別碼**許 Simon 帳戶類型 hello 電子郵件地址] 文字方塊中。

    d. 在 hello**區域**下拉式清單中，選取 hello 區域的值。

    e. 在 hello**除法**下拉式清單中，選取 hello 除數的值。

    f. 在 hello**部門**下拉式清單中，選取 hello 部門的值。

    g. 按一下 [儲存] 。

    > [!NOTE] 
    > 您可以透過選取傳送註冊郵件 toouser**傳送註冊郵件**核取方塊。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與他們存取 tooiLMS 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooiLMS，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**iLMS**。

    ![設定單一登入](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下的 hello iLMS 磚 hello 存取面板中時，您應該取得自動登入 tooyour iLMS 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png


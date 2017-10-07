---
title: "教學課程：Azure Active Directory 與 Marketo 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 和 Marketo 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a>教學課程：Azure Active Directory 與 Marketo 整合

在此教學課程中，您學會如何 toointegrate Marketo 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Marketo 可以提供下列優點 hello:

- 您可以控制存取 tooMarketo Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooMarketo （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Marketo 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Marketo 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Marketo
2. 設定並測試 Azure AD 單一登入

## <a name="adding-marketo-from-hello-gallery"></a>從 hello 圖庫加入 Marketo
tooconfigure hello 整合 Marketo 到 Azure AD，您需要 tooadd Marketo hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Marketo hello 圖庫中，從執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Marketo**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. 在 hello 結果 窗格中，選取  **Marketo**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您將以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Marketo 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者於 Marketo 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Marketo 中相關的使用者之間的連結關聯性需要 toobe 建立。

於 Marketo，指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 Marketo 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Marketo](#creating-a-marketo-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Marketo 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您的 Marketo 應用程式中。

**tooconfigure Azure AD 單一登入與 Marketo，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Marketo**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. 在 hello **Marketo 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    a. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://saml.marketo.com/sp`

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://login.marketo.com/saml/assertion/\<munchkinid\>`

    > [!NOTE] 
    > 這些都不是真正的值。 以 hello 實際的識別項和回覆 URL 更新這些值。 請連絡[Marketo 支援小組](http://investors.marketo.com/contactus.cfm)tooget 這些值。
 
4. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. 在 hello **Marketo 組態**區段中，按一下**設定 Marketo** tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. tooget Munchkin 識別碼，應用程式的登入 tooMarketo 使用管理員認證，然後執行下列動作：
   
    a. 登入 tooMarketo 應用程式使用系統管理員認證。
   
    b. 按一下 hello **Admin** hello 上方瀏覽窗格上的按鈕。
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. 瀏覽 toohello 整合功能表上，按一下 hello **Munchkin 連結**。
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    d. 複製 hello Munchkin 識別碼 hello 螢幕上顯示，並完成您的回覆 URL 在 hello Azure AD 設定精靈。
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. tooconfigure hello SSO hello 應用程式中，請遵循下列步驟 hello:
   
    a. 登入 tooMarketo 應用程式使用系統管理員認證。
   
    b. 按一下 hello **Admin** hello 上方瀏覽窗格上的按鈕。
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. 瀏覽 toohello 整合功能表上，按一下**單一登入**。
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    d. 按一下 [tooenable hello SAML 設定**編輯**] 按鈕。
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    e. **已啟用**單一登入設定。
   
    f. 貼上 hello **SAML 實體識別碼**，在 hello**簽發者 ID**文字方塊。
   
    g. 在 hello**實體識別碼**文字方塊中，輸入 hello URL 做為`http://saml.marketo.com/sp`。
   
    h. 選取 hello 使用者識別碼位置做為**名稱識別碼元素**。
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > 如果您的使用者識別碼不是 UPN 值則變更 hello 屬性 索引標籤中的 hello 值。
   
    i. 上傳 hello 憑證，您已下載從 Azure AD 組態精靈。 **儲存**hello 設定。
   
    j. 編輯 hello 重新導向頁面設定。
   
    k. 貼上 hello **SAML 單一登入服務 URL**在 hello**登入 URL**文字方塊。
   
    l. 貼上 hello**登出 URL**在 hello**登出 URL**文字方塊。
   
    m. 在 hello**錯誤 URL**，複製您**Marketo 的執行個體 URL**按一下**儲存**按鈕 toosave 設定。
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. tooenable hello SSO 的使用者，完成下列動作的 hello:
   
    a. 登入 tooMarketo 應用程式使用系統管理員認證。
   
    b. 按一下 hello **Admin** hello 上方瀏覽窗格上的按鈕。
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. 瀏覽 toohello**安全性**功能表，然後按一下**登入設定**。
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    d. 檢查 hello**需要 SSO**選項和**儲存**hello 設定。
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-marketo-test-user"></a>建立 Marketo 測試使用者

在本節中，您要在 Marketo 中建立名為 Britta Simon 的使用者。 請遵循這些步驟 toocreate Marketo 平台的使用者。

1. 登入 tooMarketo 應用程式使用系統管理員認證。

2. 按一下 hello **Admin** hello 上方瀏覽窗格上的按鈕。
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. 瀏覽 toohello**安全性**功能表，然後按一下**使用者和角色**
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. 按一下 hello**邀請新使用者**hello 使用者 索引標籤上的連結
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. 在下列資訊的 hello 邀請新增使用者精靈填滿 hello
   
    a. 輸入 hello 使用者**電子郵件**hello 文字方塊中的位址
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    b. 輸入 hello**名字**hello 文字方塊中
   
    c. 輸入 hello**姓氏**hello 文字方塊中
   
    d. 按一下 [下一步] 

6. 在 hello**權限**索引標籤，選取 hello **userRoles**按一下**下一步**
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. 按一下 hello**傳送**按鈕 toosend hello 使用者邀請
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. 使用者會收到 hello 電子郵件通知，並擁有 tooclick hello 連結，並變更 hello 密碼 tooactivate hello 帳戶。 

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooMarketo 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooMarketo，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Marketo**。

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello Marketo 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Marketo 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png


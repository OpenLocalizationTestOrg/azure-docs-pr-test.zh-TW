---
title: "教學課程：Azure Active Directory 與 SAP Cloud for Customer 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與客戶的 SAP 雲端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a>教學課程：Azure Active Directory 與 SAP Cloud for Customer 整合

在此教學課程中，您學習如何 toointegrate SAP 客戶與 Azure Active Directory (Azure AD) 的雲端。

SAP 雲端整合與 Azure AD 的客戶可以提供下列優點 hello:

- 您可以控制存取 tooSAP 雲端客戶的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooSAP 雲端 （單一登入） 的客戶使用其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure SAP 雲端與客戶的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 SAP Cloud for Customer 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 加入 SAP 雲端的客戶，從 hello 組件庫
2. 設定並測試 Azure AD 單一登入

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a>加入 SAP 雲端的客戶，從 hello 組件庫
tooconfigure hello 整合 SAP 雲端至 Azure AD 的客戶，您需要 tooadd SAP 雲端客戶的 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd SAP 雲端客戶的 hello 圖庫中，執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**客戶的 SAP 雲端**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. 在 [hello [結果] 窗格中，選取**SAP 雲端客戶的**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAP Cloud for Customer 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow 客戶的 SAP 雲端中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者和客戶的 SAP 雲端中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

在 SAP 雲端中的客戶，指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 Azure AD 單一登入 SAP 雲端與客戶，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 SAP 雲端客戶測試使用者](#creating-a-sap-cloud-for-customer-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示的客戶的 SAP 雲端中的對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您的客戶應用程式的 SAP 雲端中。

**Azure AD 單一登入與 SAP 雲端客戶的 tooconfigure 執行 hello 下列步驟：**

1. 在 Azure 入口網站上 hello hello**客戶的 SAP 雲端**應用程式整合頁面上，按一下**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. 在 [hello**客戶網域和 Url 的 SAP 雲端**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    a. 在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server name>.crm.ondemand.com`

    b. 在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server name>.crm.ondemand.com`

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello 登入 URL 和識別項。 請連絡[客戶用戶端支援小組的 SAP 雲端](https://www.sap.com/about/agreements.sap-cloud-services-customers.html)tooget 這些值。 

4. 在 [hello**使用者屬性**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    a. 在**使用者識別碼**清單中，選取 hello **ExtractMailPrefix()**函式。

    b. 從 hello**郵件**清單中，您想要實作 toouse 選取 hello 使用者屬性。
    例如，如果您想 toouse hello EmployeeID 做為唯一的使用者識別碼，而且您已在 hello ExtensionAttribute2 儲存 hello 屬性值，然後選取 user.extensionattribute2。  

5. 在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. 在 hello**客戶設定的 SAP 雲端**區段中，按一下**客戶設定 SAP 雲端**tooopen**設定登入**視窗。 複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. tooget SSO 設定，執行下列步驟的 hello:
   
    a. 使用系統管理員權限登入 SAP Cloud for Customer 入口網站。
   
    b. 瀏覽 toohello**應用程式和使用者管理的一般工作**按一下 hello**身分識別提供者**] 索引標籤。
   
    c. 按一下**新的身分識別提供者**和選取 hello 從 hello Azure 入口網站下載的中繼資料 XML 檔案。 匯入 hello 中繼資料，hello 系統會自動上傳 hello 需要的簽章憑證和加密憑證。
   
    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    d. Azure Active Directory 需要 hello SAML 要求中的 hello 項目判斷提示取用者服務 URL 中，因此選取 hello**包括判斷提示取用者服務 URL**核取方塊。
   
    e. 按一下 [啟用單一登入]。
   
    f. 儲存您的變更。
   
    g. 按一下 hello**我系統**] 索引標籤。
   
    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    h. 在 [Azure AD 登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 **SAML 單一登入服務 URL**。
   
    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    i. 指定是否 hello 員工可以手動選擇選取 hello 登入以使用者識別碼和密碼或 SSO**手動身分識別提供者選取**。
   
    j. 在 [hello **SSO URL**區段中，指定應由您的員工 toosign toohello 系統上的 hello URL。 
    在 [hello **URL 傳送 tooEmployee** ] 清單中，您可以選擇下列選項的 hello:
   
    **非 SSO URL**
   
    hello 系統會傳送只 hello 一般系統 URL toohello 員工。 hello 員工無法登入使用 SSO，且必須使用密碼或改為憑證。
   
    **SSO URL** 
   
    hello 系統會傳送只 hello SSO URL toohello 員工。 hello 員工可以登入使用 SSO。 驗證要求重新導向到 [hello IdP。
   
    **自動選取**
   
    如果並未啟用 SSO，hello 系統會傳送 hello 一般系統 URL toohello 員工。 如果 SSO 為作用中，hello 系統會檢查 hello 員工是否有密碼。 如果密碼功能，同時 SSO URL 和非 SSO URL 傳送 toohello 員工。 不過，如果 hello 員工沒有密碼，hello SSO URL 會傳送 toohello 員工。
   
    k. 儲存您的變更。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a>建立 SAP Cloud for Customer 測試使用者

在本節中，您要在 SAP Cloud for Customer 中建立名為 Britta Simon 的使用者。 請使用[客戶支援服務團隊的 SAP 雲端](https://www.sap.com/about/agreements.sap-cloud-services-customers.html)tooadd hello hello SAP 雲端客戶的平台的使用者。 

> [!NOTE]
> 請確定 NameID 值應該符合與 hello 客戶平台的 hello SAP 雲端中的使用者名稱欄位。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

本節中，在您啟用 Azure 單一登入許 Simon toouse 客戶授與存取 tooSAP 雲端。

![指派使用者][200] 

**tooassign 許 Simon tooSAP 定域機組的客戶，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**客戶的 SAP 雲端**。

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello SAP 雲端客戶磚 hello 存取面板中時，您應該取得自動登入 tooyour SAP 雲端客戶應用程式。
如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png


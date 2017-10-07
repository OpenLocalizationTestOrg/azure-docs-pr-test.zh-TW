---
title: "教學課程：Azure Active Directory 與 SAP Business ByDesign 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SAP Business ByDesign 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a>教學課程：Azure Active Directory 與 SAP Business ByDesign 整合

在此教學課程中，您學習如何 toointegrate SAP Business ByDesign 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 SAP Business ByDesign 可以提供下列優點的 hello:

- 您可以控制存取 tooSAP 商務 ByDesign Azure AD 中。
- 您可以使用其 Azure AD 帳戶啟用您使用者 tooautomatically get 登入 tooSAP 商務 ByDesign （單一登入）。
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與 SAP Business ByDesign 的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 SAP Business ByDesign 單一登入功能的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 加入 SAP Business ByDesign 從 hello 組件庫
2. 設定並測試 Azure AD 單一登入

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a>加入 SAP Business ByDesign 從 hello 組件庫
tooconfigure hello 整合 SAP Business ByDesign 到 Azure AD，您需要 tooadd SAP Business ByDesign hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd SAP Business ByDesign 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory] 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 [hello] 搜尋方塊中，輸入**SAP Business ByDesign**，選取**SAP Business ByDesign**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![SAP Business ByDesign hello [結果] 清單中](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAP Business ByDesign 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 SAP Business ByDesign 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello SAP Business ByDesign 中相關的使用者之間的連結關聯性需要 toobe 建立。

在 SAP Business ByDesign，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 SAP Business ByDesign 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 SAP Business ByDesign 測試使用者](#create-an-sap-business-bydesign-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 SAP 商業 ByDesign 中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 SAP Business ByDesign 應用程式中。

**tooconfigure Azure AD 單一登入與 SAP Business ByDesign，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **SAP Business ByDesign**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入連結][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. 在 [hello **SAP 商務 ByDesign 網域和 Url**區段中，執行下列步驟的 hello:

    ![SAP Business ByDesign 網域及 URL 單一登入資訊](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    a. 在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<servername>.sapbydesign.com`

    b. 在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<servername>.sapbydesign.com`

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello 登入 URL 和識別項。 請連絡[SAP 商務 ByDesign 用戶端支援小組](https://www.sap.com/products/cloud-analytics.support.html)tooget 這些值。

4. 在 [hello**使用者屬性**區段中，執行下列步驟的 hello:

    ![[SAP Business ByDesign 屬性] 區段](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    a. 在**使用者識別碼**清單中，選取 hello **ExtractMailPrefix()**函式。
    
    b. 從 hello**郵件**清單中，您想要實作 toouse 選取 hello 使用者屬性。 例如，如果您想 toouse hello EmployeeID 做為唯一的使用者識別碼，而且您已在 hello ExtensionAttribute2 儲存 hello 屬性值，然後選取 user.extensionattribute2。   

5. 在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. 在 hello **SAP 商務 ByDesign 組態**區段中，按一下**設定 SAP Business ByDesign** tooopen**設定登入**視窗。 複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![SAP Business ByDesign 設定](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. tooget SSO 設定應用程式執行下列步驟的 hello:
   
    a. 登入 tooyour SAP Business ByDesign 入口網站，以系統管理員權限。
   
    b. 瀏覽過**應用程式和使用者管理的一般工作**按一下 hello**身分識別提供者**] 索引標籤。
   
    c. 按一下**新的身分識別提供者**和從 hello Azure 入口網站下載的選取 hello 中繼資料 XML 檔案。 匯入 hello 中繼資料，hello 系統會自動上傳 hello 需要的簽章憑證和加密憑證。
   
    ![設定單一登入](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    d. tooinclude hello**判斷提示取用者服務 URL**入 hello SAML 要求，請選取**包括判斷提示取用者服務 URL**。
   
    e. 按一下 [啟用單一登入]。
   
    f. 儲存您的變更。
   
    g. 按一下 hello**我系統**] 索引標籤。
   
    ![設定單一登入](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    h. 貼上**SAML 單一登入服務 URL**，您已複製 hello Azure 入口網站從它到 hello **Azure AD 登入 URL**文字方塊。
   
    ![設定單一登入](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    i. 指定是否 hello 員工可以手動選擇選取登入以使用者識別碼和密碼或 SSO**手動身分識別提供者選取**。
   
    j. 在 [hello **SSO URL**區段中，指定應該由 hello 員工 toologon toohello 系統的 hello URL。 
    Hello URL 傳送 tooEmployee 下拉式清單中，您可以選擇下列選項的 hello:
   
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

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello Azure 入口網站，hello 左窗格中，按一下 [hello **Azure Active Directory** ] 按鈕。

    ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下 [**所有使用者**。

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。

    ![hello [新增] 按鈕](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. 在 [hello**使用者**對話方塊方塊中，執行下列步驟的 hello:

    ![hello [使用者] 對話方塊](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    a. 在 [hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。

    c. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 [hello**密碼**方塊。

    d. 按一下 [建立] 。
 
### <a name="create-an-sap-business-bydesign-test-user"></a>建立 SAP Business ByDesign 測試使用者

在本節中，您要在 SAP Business ByDesign 中建立名為 Britta Simon 的使用者。 請使用[SAP 商務 ByDesign 用戶端支援小組](https://www.sap.com/products/cloud-analytics.support.html)tooadd hello hello SAP Business ByDesign 平台的使用者。 

> [!NOTE]
> 請確定 NameID 值應該符合與 hello hello SAP Business ByDesign 平台中的使用者名稱欄位。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooSAP 商務 ByDesign 啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooSAP 商務 ByDesign，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**SAP Business ByDesign**。

    ![hello 應用程式清單中的 hello SAP Business ByDesign 連結](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello SAP Business ByDesign 磚 hello 存取面板中的時，您應該取得自動登入 tooyour SAP Business ByDesign 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png


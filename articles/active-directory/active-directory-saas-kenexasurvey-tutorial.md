---
title: "教學課程：Azure Active Directory 與 IBM Kenexa Survey Enterprise 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 IBM Kenexa 調查企業之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a>教學課程：Azure Active Directory 與 IBM Kenexa Survey Enterprise 整合

在此教學課程中，您學會如何 toointegrate IBM Kenexa 調查企業與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 IBM Kenexa 調查 Enterprise 可以提供下列優點 hello:

- 您可以控制存取 tooIBM Kenexa 調查 Enterprise 的 Azure AD 中。
- 您可以啟用您的使用者 tooautomatically 登入 tooIBM Kenexa 調查企業單一登入 (SSO) 使用其 Azure AD 帳戶。
- 您可以管理您的帳戶，在單一中央位置： hello Azure 入口網站。

如果您想 tooknow 更多關於軟體使用 Azure AD 服務 (SaaS) 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與 IBM Kenexa 調查 Enterprise 的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 IBM Kenexa Survey Enterprise SSO 的訂用帳戶

> [!NOTE]
> 當您測試 hello 步驟在本教學課程時，我們建議您不要使用實際執行環境。

tootest hello 步驟在本教學課程，請遵循下列建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD SSO。 hello hello 教學課程所述的案例包含兩個主要建置組塊：

* 從 hello 圖庫加入 IBM Kenexa 調查 Enterprise
* 設定並測試 Azure AD SSO

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a>從 hello 圖庫新增 IBM Kenexa 調查 Enterprise
tooconfigure hello 整合 IBM Kenexa 調查企業到 Azure AD 中，加入 IBM Kenexa 調查企業 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

tooadd IBM Kenexa 調查企業 hello 圖庫中，從 hello 遵循：

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，在 hello 左的窗格中按一下 hello **Azure Active Directory** ] 按鈕。 

    ![hello Azure Active Directory 按鈕][1]

2. 選取 [企業應用程式]，然後選取 [所有應用程式]。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. 按一下 [應用程式，tooadd hello**新的應用程式**] 按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 [hello] 搜尋方塊中，輸入**IBM Kenexa 調查企業**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. 在 hello 結果清單中，選取**IBM Kenexa 調查企業**，然後按一下hello**新增**按鈕 tooadd hello 應用程式。

    ![IBM Kenexa 調查企業 hello [結果] 清單中](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 IBM Kenexa Survey Enterprise 搭配運作的 Azure AD SSO。

Azure AD SSO toowork tooidentify hello IBM Kenexa 調查企業使用者對應項目需要在 Azure AD 中。 換句話說，必須在 Azure AD 使用者和 IBM Kenexa Survey Enterprise 中的相關使用者之間，建立連結關聯性。

tooestablish hello 連結關聯性，hello 分派 hello 值**使用者名**做為 hello hello 值 IBM Kenexa 調查企業中**Username**在 Azure AD 中。

tooconfigure 和測試使用 IBM Kenexa 調查 Enterprise，完整的 Azure AD SSO hello hello 下兩節中的建置組塊。

### <a name="configure-azure-ad-sso"></a>設定 Azure AD SSO

在本節中，您在 hello Azure 入口網站中啟用 Azure AD 的 SSO 和 IBM Kenexa 調查企業應用程式中設定 SSO，藉由 hello 下列：

1. 在 Azure 入口網站上 hello hello **IBM Kenexa 調查企業**應用程式整合頁面上，按一下 **單一登入**。

    ![IBM Kenexa Survey Enterprise 設定單一登入連結][4]

2. 在 hello**單一登入**對話方塊中的，在 hello**模式**方塊中，選取**SAML 型登入**tooenable SSO。
 
    ![單一登入對話方塊](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. 在 hello **IBM Kenexa 調查企業網域和 Url**區段中，執行下列步驟的 hello:

    ![IBM Kenexa Survey Enterprise 網域及 URL 單一登入資訊](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    a. 在 hello**識別碼**文字方塊中，輸入 URL 以 hello 下列模式：`https://surveys.kenexa.com/<companycode>`

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL 以 hello 下列模式：`https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    > [!NOTE] 
    > hello 上述值不是實際。 更新 hello 實際識別項，回覆 URL。 tooobtain hello 實際的值，請連絡 hello [IBM Kenexa 調查企業支援小組](https://www.ibm.com/support/home/?lnk=fcw)。

4. 在下**SAML 簽章憑證**，按一下 **憑證 (Base64)**，然後儲存 hello 憑證檔案 tooyour 電腦。

    ![hello 憑證 (Base64) 下載連結](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    hello IBM Kenexa 調查企業應用程式特定的格式，這需要您 tooadd 自訂屬性對應 toohello 設定您的 SAML 權杖屬性的預期 tooreceive hello 安全性判斷提示標記語言 (SAML) 判斷提示。 hello hello 回應 hello 使用者識別項宣告的值必須符合已設定 hello Kenexa 系統中的 SSO 識別碼 hello。 toomap hello 做為 SSO 網際網路資料包通訊協定 (IDP) 您組織中適當的使用者識別碼，與 hello 搭配[IBM Kenexa 調查企業支援小組](https://www.ibm.com/support/home/?lnk=fcw)。 

    根據預設，Azure AD 會設定為 hello 使用者主要名稱 (UPN) 值 hello 使用者識別項。 您可以變更此值在 hello**屬性**索引標籤上，如下列螢幕擷取畫面的 hello 中所示。 只有在您完成 hello 正確對應之後，才 hello 整合的運作方式。
    
    ![hello 使用者屬性 對話方塊](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. 按一下 [儲存] 。

    ![hello 設定單一登入儲存按鈕](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. tooopen hello**設定登入**視窗底下**IBM Kenexa 調查企業設定**，按一下 **設定 IBM Kenexa 調查企業**。 
 
    ![hello 設定 IBM Kenexa 調查企業連結](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. 複製 hello**登出 URL**， **SAML 實體識別碼**，和**SAML 單一登入服務 URL**值 hello**快速參考**> 一節。

8. 在 hello**設定登入**視窗底下**快速參考**，複製 hello**登出 URL**， **SAML 實體識別碼**，和**SAML 單一登入服務 URL**值。

9. 在 hello tooconfigure SSO **IBM Kenexa 調查企業**端、 傳送嗨下載**憑證 (Base64)**，**登出 URL**， **SAML 實體識別碼**，和**SAML 單一登入服務 URL**值 toohello [IBM Kenexa 調查企業支援小組](https://www.ibm.com/support/home/?lnk=fcw)。

> [!TIP]
> 您可以使用參照 tooa 精簡版本的這些指示 hello [Azure 入口網站](https://portal.azure.com)當您在設定 hello 應用程式的設定。 從 hello 新增 hello 應用程式之後**Active Directory** > **企業應用程式**區段中，只要按一下 hello**單一登入**索引標籤，然後再存取hello 內嵌文件，透過 hello**組態**hello 結尾區段。 toolearn 進一步了解 hello embedded 文件功能，請參閱[Azure AD 的內嵌文件](https://go.microsoft.com/fwlink/?linkid=845985)。
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
在本節中，您可以建立 hello Azure 入口網站中的測試使用者許 Simon 執行 hello 下列：

![建立 Azure AD 測試使用者][100]

1. 在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。
 
    ![hello [新增] 按鈕](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。

    c. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。

    d. 按一下 [建立] 。
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a>建立 IBM Kenexa Survey Enterprise 測試使用者

在本節中，您要在 IBM Kenexa Survey Enterprise 中建立名為 Britta Simon 的使用者。 

toocreate hello IBM Kenexa 調查企業系統和它們對應 hello SSO 識別碼中的使用者，您可以使用 hello [IBM Kenexa 調查企業支援小組](https://www.ibm.com/support/home/?lnk=fcw)。 這個 SSO 識別碼值也應該對應從 Azure AD toohello 使用者識別碼值。 您可以變更此預設設定在 hello**屬性** 索引標籤。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，以啟用使用者許 Simon toouse Azure SSO 授與存取 tooIBM Kenexa 調查企業。

![指派 hello 使用者角色][200] 

tooassign 使用者許 Simon tooIBM Kenexa 調查企業，請勿 hello 遵循：

1. 在 hello Azure 入口網站，開啟 hello**應用程式**檢視，請進入 toohello**目錄**檢視中，選取**企業應用程式**，然後按一下**所有應用程式**。

    ![hello [企業應用程式] 和 [所有應用程式] 連結][201] 

2. 在 hello**應用程式**清單中，選取**IBM Kenexa 調查企業**。

    ![hello 應用程式清單中的 hello IBM Kenexa 調查企業連結](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. 在 hello 左窗格中，按一下 **使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202] 

4. 按一下 hello**新增** 按鈕，然後在 hello**將作業加入**窗格中，選取**使用者和群組**。

    ![hello 將作業加入窗格][203]

5. 在 hello**使用者和群組**對話方塊中的，在 hello**使用者**清單中，選取**許 Simon**。

6. 在 [hello**使用者和群組**對話方塊方塊中，按一下 hello**選取**] 按鈕。

7. 在 [hello**將作業加入**對話方塊方塊中，按一下 hello**指派**] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

本節中，在中，您可以測試您的 Azure AD 的 SSO 組態使用 hello 存取面板。

當您按一下 hello **IBM Kenexa 調查企業**以並排顯示 hello 存取面板中，您應該自動登入 tooyour IBM Kenexa 調查企業應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 

---
title: "教學課程：Azure Active Directory 與 SAP HANA 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SAP HANA 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a>教學課程：Azure Active Directory 與 SAP HANA 整合

在此教學課程中，您學習如何 toointegrate SAP HANA 與 Azure Active Directory (Azure AD)。

整合與 Azure AD 的 SAP HANA 可以提供下列優點 hello:

- 您可以控制存取 tooSAP HANA Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooSAP HANA （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與 SAP HANA 的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 SAP HANA 單一登入的訂用帳戶
- 執行中的 HANA 執行個體，無論是位於任何公用 IaaS、內部部署、Azure VM 還是 Azure 中的 SAP 大型執行個體
- hello XSA 管理 Web 介面，以及 HANA Studio hello HANA 執行個體上安裝。

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用 SAP HANA 的實際執行環境。 開發，或預備環境的 hello 應用程式，然後使用 hello 實際執行環境中的第一次測試 hello 整合。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 SAP HANA
2. 設定並測試 Azure AD 單一登入

## <a name="adding-sap-hana-from-hello-gallery"></a>從 hello 圖庫加入 SAP HANA
tooconfigure hello 整合 SAP HANA 到 Azure AD，您需要 tooadd SAP HANA hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd SAP HANA hello 圖庫中，從執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**SAP HANA**，選取**SAP HANA**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。 

    ![hello 新的應用程式](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAP HANA 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 SAP HANA 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 SAP HANA 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

在 SAP HANA hello hello 值指派**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 Azure AD 單一登入 SAP HANA，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 SAP HANA 測試使用者](#creating-a-sap-hana-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 SAP HANA 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 SAP HANA 應用程式中。

**tooconfigure Azure AD 單一登入 SAP HANA，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **SAP HANA**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. 在 hello **SAP HANA 網域和 Url**區段中，執行下列步驟的 hello:

    ![網域與 URL 單一登入資訊](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    a. 在 hello**識別碼**文字方塊中，做為輸入：`HA100` 

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`

    > [!NOTE] 
    > 這些都不是真正的值。 以 hello 實際的識別項和回覆 URL 更新這些值。 請連絡[SAP HANA 用戶端支援小組](https://cloudplatform.sap.com/contact.html)tooget 這些值。 

4. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    >如果憑證不在作用中然後讓它成為按一下 hello 「 使新憑證作用中 」 的核取方塊 hello Azure AD 中。 

5. SAP HANA 應用程式預期 hello SAML 判斷提示，以特定格式。 hello 下列螢幕擷取畫面會顯示這個範例。 我們已在這裡對應 hello**使用者識別碼**與**ExtractMailPrefix()**函式的**user.mail**。 這可讓 hello 的前置詞值，這是唯一的使用者 id。 hello hello 使用者的電子郵件 這是在每個成功的回應中傳送 toohello SAP HANA 應用程式。

    ![設定單一登入](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. 在 hello**使用者屬性**區段 hello**單一登入**對話方塊：

    a. 在 hello**使用者識別碼**下拉式清單中選取**ExtractMailPrefix**。
    
    b. 在 hello**郵件**下拉式清單中選取**user.mail**。

7. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. tooconfigure 單一登入上**SAP HANA** ，登入 tooyour **HANA XSA Web 主控台**toohello 瀏覽個別的 HTTPS 端點。

    > [!Note]
    > 在 hello 預設組態中，hello URL 重新導向 hello 要求 tooa 登入畫面，而這需要 hello 認證已驗證 SAP HANA 資料庫使用者 toocomplete hello 登入處理程序。 hello 登入使用者都必須有 hello 權限需要的 tooperform SAML 系統管理工作。

9. Hello XSA Web 介面，在瀏覽過**SAML 身分識別提供者**並從該處，按一下 [hello **"+"** -hello hello 螢幕 toodisplay hello 新增身分識別提供者資訊] 窗格底部的按鈕，然後執行hello 下列步驟：

    ![新增識別提供者](./media/active-directory-saas-saphana-tutorial/sap1.png)

    a. 在 [hello**新增身分識別提供者資訊**] 窗格中，貼上 hello 內容的中繼資料 XML，您從 Azure 入口網站下載到 hello hello**中繼資料**文字方塊。

    ![[新增識別提供者] 設定](./media/active-directory-saas-saphana-tutorial/sap2.png)

    b. 如果 hello hello XML 文件內容有效，hello 剖析程序會 hello 所需的資訊 tooinsert 擷取至 hello**主旨、 實體識別碼和簽發者**hello 一般資料欄位螢幕區域，以及 hello hello URL 欄位目的地的螢幕區域，例如**基底 URL 和單一登入 URL (*)**。

    ![[新增識別提供者] 設定](./media/active-directory-saas-saphana-tutorial/sap3.png)

    c. 在 hello 名稱方塊中的 hello 一般資料畫面區域中，輸入 hello 新 SAML SSO 身分識別提供者的名稱。

    > [!Note]
    > hello SAML IDP hello 名稱是強制性，而且必須是唯一的。它會出現在 hello 清單可用的 SAML IDPs 顯示，如果您選取 SAML 作為 hello SAP HANA XS 應用程式 toouse，驗證方法，例如 hello 驗證畫面區域中的 hello XS 成品管理工具。

10. 儲存 hello hello 新 SAML 身分識別提供者的詳細資料。 選擇**儲存**toosave hello hello SAML 身分識別提供者的詳細資料，並加入 hello 新 SAML IDP toohello 清單的已知 SAML IDPs。

    ![[儲存] 按鈕](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. HANA Studio 中的 hello hello 系統內容中**組態**索引標籤上，只要篩選設定**saml**並調整 hello **assertion_timeout**從**10 秒**太**120 秒**。

    ![assertion_timeout 設定](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![hello [新增] 按鈕](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-sap-hana-test-user"></a>建立 SAP HANA 測試使用者

tooenable Azure AD 使用者 toolog 中 tooSAP HANA，它們必須佈建到 SAP HANA。
SAP HANA 支援預設啟用的 Just-In-Time 佈建。

若要手動 toocreate 使用者，執行下列步驟的 hello:

>[!Note]
>您可以變更 hello hello 使用者所使用的外部驗證。
外部使用者會使用外部系統 (例如 Kerberos 系統) 來進行驗證。 如需外部身分識別的詳細資訊，請連絡[網域系統管理員](https://cloudplatform.sap.com/contact.html)。

1. 開啟 hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us)為系統管理員，並且啟用 hello SAML SSO 資料庫使用者。

    ![建立使用者](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. 刻度 hello 不可見的核取方塊 toohello 方**SAML**並遵循 hello [設定] 連結。

3. 按一下**新增**tooadd hello SAML IDP，然後按一下**確定**選取 hello 適當 SAML IDP。

4. 新增 hello**外部識別**（例如。 這裡 BrittaSimon)，或選擇**"Any"**按一下**確定**。

    >[!Note]
    >如果未核取 「 任何 」 核取方塊，則 hello HANA 中的使用者名稱需要 tooexactly 符合 hello 名稱之前 hello 網域尾碼 hello UPN 中的 hello 使用者 (亦即BrittaSimon@contoso.com就會變成 BrittaSimon HANA 中的)。

5. 為了測試用途，指派所有**"XS"**角色 toohello 使用者。

    ![指派角色](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > 您只應該提供適用於您使用案例的權限。

6. 儲存 hello 的使用者。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooSAP HANA 啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooSAP HANA，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**SAP HANA**。

    ![指派使用者](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello SAP HANA 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 SAP HANA 應用程式。
如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png


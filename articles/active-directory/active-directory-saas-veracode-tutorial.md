---
title: "教學課程：Azure Active Directory 與 Veracode 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Veracode 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a>教學課程：Azure Active Directory 與 Veracode 整合

在此教學課程中，您學會如何 toointegrate Veracode 與 Azure Active Directory (Azure AD)。

Veracode 整合與 Azure AD 可以提供下列優點 hello:

- 您可以控制存取 tooVeracode Azure AD 中。
- 您可以啟用您的使用者 tooautomatically get 登入 tooVeracode （單一登入） 具有其 Azure AD 帳戶。
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 Veracode 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Veracode 單一登入功能的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫新增 Veracode
2. 設定和測試 Azure AD 單一登入

## <a name="add-veracode-from-hello-gallery"></a>從 hello 圖庫新增 Veracode
tooconfigure hello 整合 Veracode 到 Azure AD，您需要 tooadd Veracode hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Veracode 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**Veracode**，選取**Veracode**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![Veracode hello [結果] 清單中](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Veracode 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Veracode 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 Veracode 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

Veracode 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 和測試 Azure AD 單一登入與 Veracode，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Veracode](#create-a-veracode-test-user)**  -toohave 許 Simon Veracode 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Veracode 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 Veracode，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Veracode**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入連結][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. 在 [hello **Veracode 網域和 Url** ] 區段中，使用者沒有 tooperform 任何步驟，因為與 Azure 已預先整合 hello 應用程式。 

    ![設定單一登入](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooVeracode 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。

    Veracode 應用程式需要特定格式，這需要您 tooadd 自訂屬性對應 tooyour hello SAML 判斷提示**saml 權杖屬性**組態。 hello 下列螢幕擷取畫面會顯示這個範例。
    
    ![屬性](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "屬性")

6. tooadd hello 必要屬性對應，執行下列步驟的 hello:

    | 屬性名稱 | 屬性值 |
    |--- |--- |
    | firstname |User.givenname |
    | lastname |User.surname |
    | 電子郵件 |User.mail |
    
    a. 上述的 hello 資料表中每個資料列，按一下 **新增使用者屬性**。
    
    ![屬性](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "屬性")
    
    ![屬性](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "屬性")
    
    b. 在 hello**屬性名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。
    
    c. 在 hello**屬性值**文字方塊中，顯示該資料列選取 hello 屬性值。
    
    d. 按一下 [確定] 。

7. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. 在 hello **Veracode 組態**區段中，按一下**設定 Veracode** tooopen**設定登入**視窗。 複製 hello **SAML 實體識別碼**從 hello**快速參考 > 一節。**

    ![Veracode 組態](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Veracode 公司網站。

10. 在 hello 最上層顯示 hello 功能表上，按一下**設定**，然後按一下**管理員**。
   
    ![管理](./media/active-directory-saas-veracode-tutorial/ic802911.png "管理")

11. 按一下 hello **SAML**  索引標籤。

12. 在 hello**組織 SAML 設定**區段中，執行下列步驟的 hello:
   
    ![管理](./media/active-directory-saas-veracode-tutorial/ic802912.png "管理")
   
    a.  在**簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。
    
    b. 您下載的憑證，從 Azure 入口網站中，按一下 tooupload**選擇檔案**。
   
    c. 選取 [啟用自動註冊] 。

13. 在 hello**自我登錄設定**區段中，執行下列步驟，hello，然後按一下**儲存**:
   
    ![管理](./media/active-directory-saas-veracode-tutorial/ic802913.png "管理")
   
    a. 在 [啟用新的使用者] 選取 [不需要啟用]。
   
    b.這是另一個 C# 主控台應用程式。 在 [使用者資料更新] 選取 [Veracode 使用者資料喜好設定]。
   
    c. 如**SAML 屬性的詳細資料**，選取下列 hello:
      * **[使用者角色]**
      * **[原則系統管理員]**
      * **[檢閱者]**
      * **[安全性負責人]**
      * **[行政人員]**
      * **[傳送者]**
      * **[建立者]**
      * **[所有掃描類型]**
      * **[小組成員資格]**
      * **[預設小組]**

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。

    ![hello [新增] 按鈕](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. 在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:

    ![hello [使用者] 對話方塊](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    a. 在 hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。

    c. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。

    d. 按一下 [建立] 。
 
### <a name="create-a-veracode-test-user"></a>建立 Veracode 測試使用者
在訂單 tooenable Azure AD 使用者 toolog Veracode 成，它們必須佈建到 Veracode。 中的 Veracode hello 案例中，佈建是自動化的工作。 沒有您適用的動作項目。 使用者會自動建立必要 hello 第一個單一登入嘗試期間。

> [!NOTE]
> 您可以使用任何其他 Veracode 使用者帳戶建立工具或 Api 提供 Veracode tooprovision Azure AD 使用者帳戶。
> 

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooVeracode 啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooVeracode，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Veracode**。

    ![hello 應用程式清單中的 hello Veracode 連結](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello Veracode 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Veracode 應用程式。
如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png


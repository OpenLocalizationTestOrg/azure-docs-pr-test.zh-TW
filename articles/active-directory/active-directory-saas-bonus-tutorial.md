---
title: "教學課程：Azure Active Directory 與 Bonusly 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Bonusly 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a>教學課程：Azure Active Directory 與 Bonusly 整合

在此教學課程中，您學會如何 toointegrate Bonusly 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Bonusly 可以提供下列優點 hello:

- 您可以控制存取 tooBonusly Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooBonusly （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Bonusly 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Bonusly 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Bonusly
2. 設定並測試 Azure AD 單一登入

## <a name="adding-bonusly-from-hello-gallery"></a>從 hello 圖庫加入 Bonusly
tooconfigure hello 整合 Bonusly 到 Azure AD，您需要 tooadd Bonusly hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Bonusly 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**Bonusly**，選取**Bonusly**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![Bonusly hello [結果] 清單中](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Bonusly 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Bonusly 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Bonusly 中相關的使用者之間的連結關聯性需要 toobe 建立。

Bonusly 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 Bonusly 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 Bonusly 測試使用者](#create-a-bonusly-test-user)** -toohave 許 Simon Bonusly 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Bonusly 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 Bonusly，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Bonusly**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. 在 hello **Bonusly 網域和 Url**區段中，執行下列步驟的 hello:

    ![Bonusly 網域及 URL 單一登入資訊](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://Bonus.ly/saml/<tenant-name>`

    > [!NOTE] 
    > hello 值不是真正的。 更新 hello 值與 hello 實際的回覆 URL。 請連絡[Bonusly 支援小組](https://Bonusly/contact)tooget hello 值。
 
4. 在 hello **SAML 簽章憑證**區段，複製 hello**指紋**hello 憑證中的值。

    ![hello 憑證下載連結](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. 在 hello **Bonusly 組態**區段中，按一下**Bonusly 設定**tooopen**設定登入**視窗。 複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![Bonusly 組態](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. 在不同的瀏覽器視窗中，登入 tooyour **Bonusly**租用戶。

8. 在 hello hello 上方的工具列中按一下**設定**，然後選取**整合和應用程式**。
   
    ![Bonusly 社交區段](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")
9. 在 [單一登入] 下方，選取 [SAML]。

10. 在 hello **SAML**對話方塊頁面上，執行下列步驟的 hello:
   
    ![Bonusly Saml 對話方塊頁面](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")
   
    a. 在 hello **IdP SSO 目標 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。
   
    b. 在 hello **IdP 簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。 

    c. 在 hello **IdP 登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。

    d. 貼上**指紋**值從 Azure 入口網站複製到 hello**憑證指紋**文字方塊。
   
11. 按一下 [儲存] 。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![hello [新增] 按鈕](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="create-a-bonusly-test-user"></a>建立 Bonusly 測試使用者

在訂單 tooenable Azure AD 使用者 toolog tooBonusly 中，您必須是佈建到 Bonusly。 中的 Bonusly hello 案例中，佈建須手動進行。

>[!NOTE]
>您可以使用任何其他 Bonusly 使用者帳戶建立工具或 Api 提供 Bonusly tooprovision AAD 使用者帳戶。
>  

**tooconfigure 使用者佈建，執行下列步驟的 hello:**

1. 在網頁瀏覽器視窗中，登入 tooyour Bonusly 租用戶。

2. 按一下 [設定] 。
 
    ![設定](./media/active-directory-saas-bonus-tutorial/ic781041.png "設定")

3. 按一下 hello**使用者和加分** 索引標籤。
   
    ![使用者和獎勵](./media/active-directory-saas-bonus-tutorial/ic781042.png "使用者和獎勵")

4. 按一下 [管理使用者] 。
   
    ![管理使用者](./media/active-directory-saas-bonus-tutorial/ic781043.png "管理使用者")

5. 按一下 [加入使用者] 。
   
    ![新增使用者](./media/active-directory-saas-bonus-tutorial/ic781044.png "新增使用者")

6. 在 [hello**新增使用者**] 對話方塊中，執行下列步驟的 hello:
   
    ![新增使用者](./media/active-directory-saas-bonus-tutorial/ic781045.png "新增使用者")  

    a. 在 hello**名字**文字方塊中，輸入 hello 名字，例如使用者的**許**。

    b. 在 hello**姓氏**文字方塊中，輸入 hello 姓氏的使用者，例如**Simon**。
 
    c. 在 hello**電子郵件**文字方塊中，輸入 hello 電子郵件的使用者，例如 **brittasimon@contoso.com** 。

    d. 按一下 [儲存] 。
   
     >[!NOTE]
     >hello Azure AD 帳戶持有者會收到電子郵件，其中包含連結 tooconfirm hello 帳戶之前就會生效。
     >  

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooBonusly 啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooBonusly，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Bonusly**。

    ![hello Bonusly hello 應用程式清單中的連結](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。

當您按一下 hello Bonusly 磚中的 hello 存取面板，您應該取得自動登入 tooyour Bonusly 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png


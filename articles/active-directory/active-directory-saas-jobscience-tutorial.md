---
title: "教學課程：Azure Active Directory 與 Jobscience 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Jobscience 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a>教學課程：Azure Active Directory 與 Jobscience 整合

在此教學課程中，您學會如何 toointegrate Jobscience 與 Azure Active Directory (Azure AD)。

整合 Azure AD 與 Jobscience 可以提供下列優點 hello:

- 您可以控制存取 tooJobscience Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooJobscience （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 Jobscience 的整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Jobscience 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Jobscience
2. 設定並測試 Azure AD 單一登入

## <a name="adding-jobscience-from-hello-gallery"></a>從 hello 圖庫加入 Jobscience
tooconfigure hello 整合 Jobscience 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Jobscience。

**tooadd Jobscience 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Jobscience**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. 在 hello 結果 窗格中，選取  **Jobscience**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Jobscience 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Jobscience 中是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 Jobscience 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

在 Jobscience 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 和測試 Azure AD 單一登入與 Jobscience，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Jobscience](#creating-a-jobscience-test-user)**  -toohave 許 Simon Jobscience 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Jobscience 的應用程式中。

**tooconfigure Azure AD 單一登入 Jobscience 中，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Jobscience**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. 在 hello **Jobscience 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`http://<company name>.my.salesforce.com`
    
    > [!NOTE] 
    > 這不是真實的值。 更新此值以 hello 實際的登入 URL。 取得此值[Jobscience 用戶端支援小組](https://www.jobscience.com/support)或 hello SSO 設定檔從您將建立在 hello 教學課程後面的說明。 
 
4. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. 在 hello **Jobscience 組態**區段中，按一下**設定 Jobscience** tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. 登入 tooyour Jobscience 公司網站的系統管理員身分。

8. 跳過**安裝**。
   
   ![設定](./media/active-directory-saas-jobscience-tutorial/IC784358.png "設定")

9. 在 hello 左側瀏覽窗格中，在 hello**管理**區段中，按一下**定義域管理**tooexpand hello 相關的區段，然後按一下**我的網域**tooopen hello **我的網域**頁面。 
   
   ![我的網域](./media/active-directory-saas-jobscience-tutorial/ic767825.png "我的網域")

10. tooverify，您的網域是否已正確設定，請確定它是在 「**步驟 4 部署 tooUsers**」，並檢閱您"**我的網域設定**"。

    ![網域部署 tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "網域部署 tooUser")

11. Hello Jobscience 公司網站上，按一下 **安全性控制**，然後按一下**單一登入設定**。
    
    ![安全性控制項](./media/active-directory-saas-jobscience-tutorial/ic784364.png "安全性控制項")

12. 在 hello**單一登入設定**區段中，執行下列步驟的 hello:
    
    ![單一登入設定](./media/active-directory-saas-jobscience-tutorial/ic781026.png "單一登入設定")
    
    a. 選取 [已啟用 SAML] 。

    b.這是另一個 C# 主控台應用程式。 按一下 [新增] 。

13. 在 [hello **SAML 單一登入設定編輯**] 對話方塊中，執行下列步驟的 hello:
    
    ![SAML 單一登入設定](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML 單一登入設定")
    
    a. 在 hello**名稱**文字方塊中，輸入您的組態名稱。

    b. 在**簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。

    c. 在 hello**實體識別碼**文字方塊中，輸入`https://salesforce-jobscience.com`

    d. 按一下**瀏覽**tooupload 您 Azure AD 的憑證。

    e. 做為**SAML 識別類型**，選取**判斷提示包含從 hello 使用者物件的同盟識別碼 hello**。

    f. 做為**SAML 識別位置**，選取**身分識別位於 Subject 陳述式 hello hello NameIdentfier 元素**。

    g. 在**身分識別提供者登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。

    h. 在**身分識別提供者登出 URL**文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。

    i. 按一下 [儲存] 。

14. 在 hello 左側瀏覽窗格中，在 hello**管理**區段中，按一下**定義域管理**tooexpand hello 相關的區段，然後按一下**我的網域**tooopen hello **我的網域**頁面。 
    
    ![我的網域](./media/active-directory-saas-jobscience-tutorial/ic767825.png "我的網域")

15. 在 [hello**我的網域**] 頁面的 hello**登入頁面品牌**區段中，按一下**編輯**。
    
    ![登入頁面商標](./media/active-directory-saas-jobscience-tutorial/ic767826.png "登入頁面商標")

16. 在 hello**登入頁面品牌** 頁面的 hello**驗證服務**區段、 hello 名稱您**SAML SSO 設定**隨即出現。 請選取該名稱，然後按一下儲存 。
    
    ![登入頁面商標](./media/active-directory-saas-jobscience-tutorial/ic784366.png "登入頁面商標")

17. tooget hello 預存程序會初始化單一登入 URL，請按一下上 hello**單一登入設定**在 hello**安全性控制**功能表區段。

    ![安全性控制項](./media/active-directory-saas-jobscience-tutorial/ic784368.png "安全性控制項")
    
    按一下您已建立 hello 上述步驟中的 hello SSO 設定檔。 此頁面會顯示 hello 單一登入 URL 公司 (例如， [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid)。    

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-jobscience-test-user"></a>建立 Jobscience 測試使用者

在訂單 tooenable Azure AD 使用者 toolog tooJobscience 中，您必須是佈建到 Jobscience。 在 Jobscience 的 hello 案例中，佈建須手動進行。

>[!NOTE]
>您可以使用任何其他 Jobscience 使用者帳戶建立工具或 Api 提供 Jobscience tooprovision Azure Active Directory 使用者帳戶。
>  
        
**tooconfigure 使用者佈建，執行下列步驟的 hello:**

1. 登入 tooyour **Jobscience**以系統管理員身分的公司網站。

2. 移 tooSetup。
   
   ![設定](./media/active-directory-saas-jobscience-tutorial/ic784358.png "設定")
3. 跳過**管理使用者\>使用者**。
   
   ![使用者](./media/active-directory-saas-jobscience-tutorial/ic784369.png "使用者")
4. 按一下 [新使用者] 。
   
   ![所有使用者](./media/active-directory-saas-jobscience-tutorial/ic784370.png "所有使用者")
5. 在 [hello**編輯使用者**] 對話方塊中，執行下列步驟的 hello:
   
   ![使用者編輯](./media/active-directory-saas-jobscience-tutorial/ic784371.png "使用者編輯")
   
   a. 在 hello**名字**文字方塊中，輸入像許 hello 使用者的名字。
   
   b. 在 hello**姓氏**文字方塊中，輸入像 Simon hello 使用者的姓氏。
   
   c. 在 hello**別名**文字方塊中，輸入像 brittas hello 使用者的別名。

   d. 在 hello**電子郵件**文字方塊中，輸入 hello 電子郵件地址的使用者喜歡Brittasimon@contoso.com。

   e. 在 hello**使用者名**使用者的使用者名稱文字方塊中，輸入要Brittasimon@contoso.com。

   f. 在 hello**別名**文字方塊中，輸入 nick 名稱，Simon 類似使用者。

   g. 按一下 [儲存] 。

    
> [!NOTE]
> hello Azure Active Directory 帳戶持有者會收到一封電子郵件，並且遵循連結 tooconfirm 他們的帳戶之前就會生效。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooJobscience 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooJobscience，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Jobscience**。

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello Jobscience 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Jobscience 的應用程式。
如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png


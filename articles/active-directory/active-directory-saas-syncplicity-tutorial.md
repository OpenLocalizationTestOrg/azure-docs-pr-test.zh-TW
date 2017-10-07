---
title: "教學課程：Azure Active Directory 與 Syncplicity 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Syncplicity 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a>教學課程：Azure Active Directory 與 Syncplicity 整合

在此教學課程中，您學會如何 toointegrate Syncplicity 與 Azure Active Directory (Azure AD)。

整合 Azure AD 與 Syncplicity 可以提供下列優點 hello:

- 您可以控制存取 tooSyncplicity Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooSyncplicity （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 Syncplicity 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Syncplicity 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Syncplicity
2. 設定並測試 Azure AD 單一登入

## <a name="adding-syncplicity-from-hello-gallery"></a>從 hello 圖庫加入 Syncplicity
tooconfigure hello 整合 Syncplicity 到 Azure AD，您需要 tooadd Syncplicity hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Syncplicity 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Syncplicity**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. 在 hello 結果 窗格中，選取  **Syncplicity**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Syncplicity 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Syncplicity 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 Syncplicity 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

在 Syncplicity，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 Azure AD 單一登入與 Syncplicity 的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Syncplicity](#creating-a-syncplicity-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Syncplicity 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Syncplicity 應用程式中。

**tooconfigure Azure AD 單一登入與 Syncplicity，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Syncplicity**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. 在 hello **Syncplicity 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.syncplicity.com`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.syncplicity.com/sp`

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello 登入 URL 和識別項。 請連絡[Syncplicity 用戶端支援小組](https://www.syncplicity.com/contact-us)tooget 這些值。 
 

4. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. 在 hello **Syncplicity 組態**區段中，按一下**設定 Syncplicity** tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. 登入 tooyour **Syncplicity**租用戶。

8. 在 hello 最上層顯示 hello 功能表上，按一下**admin**，選取**設定**，然後按一下**自訂網域和單一登入**。
   
    ![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")

9. 在 hello**單一登入 (SSO)**對話方塊頁面上，執行下列步驟的 hello:
   
    ![單一登入 \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")   

    a. 在 hello**自訂網域**文字方塊中，您的網域類型 hello 名稱。
  
    b. 在 [單一登入狀態] 中選取 [啟用]。

    c. 在 hello**實體識別碼**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。

    d. 在 hello**登入頁面 URL**文字方塊中，貼上 hello **SAML 單一登入服務 URL**您從 Azure 入口網站複製的。

    e. 在 hello**登出頁面 URL**文字方塊中，貼上 hello**登出 URL**您從 Azure 入口網站複製的。

    f. 在**身分識別提供者憑證**，按一下 **選擇檔案**，然後再上傳您從 hello Azure 入口網站下載 hello 憑證。 

    g. 按一下 [儲存變更]。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-syncplicity-test-user"></a>建立 Syncplicity 測試使用者
AAD 使用者 toobe 無法 toosign 中，它們必須已佈建的 tooSyncplicity 應用程式。 本章節描述在 Syncplicity toocreate AAD 使用者帳戶的方式。

**tooprovision 使用者帳戶 tooSyncplicity，執行下列步驟的 hello:**

1. 登入 tooyour **Syncplicity**租用戶 (例如： `https://company.Syncplicity.com`)。

2. 按一下 [管理員]，然後選取 [使用者帳戶]。

3. 按一下 [新增使用者]。
   
    ![管理使用者](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "管理使用者")

4. 型別 hello**經由電子郵件**您想要選取 tooprovision AAD 帳戶的**使用者**做為**角色**，然後按一下**下一步**。
   
    ![帳戶資訊](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "帳戶資訊")
   
    >[!NOTE]
    >hello AAD 帳戶持有者取得包含連結 tooconfirm 的電子郵件，並啟用 hello 帳戶。 
    > 

5. 選取要讓新使用者成為成員的公司群組，然後按一下下一步。
   
    ![群組成員資格](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "群組成員資格")
   
    >[!NOTE]
    >如果未列出群組，請按一下 [下一步]。 
    > 

6. 選取您想要 tooplace hello 使用者的電腦上的 Syncplicity 控制之下，然後按一下 hello 資料夾**下一步**。
   
    ![Syncplicity 資料夾](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity 資料夾")

>[!NOTE]
>您可以使用任何其他 Syncplicity 使用者帳戶建立工具或 Api 提供 Syncplicity tooprovision AAD 使用者帳戶。 

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooSyncplicity 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooSyncplicity，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Syncplicity**。

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。

當您按一下 hello Syncplicity 的圖格 hello 存取面板中時，您應該取得 tooyour 自動登入 Syncplicity 應用程式。
## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png


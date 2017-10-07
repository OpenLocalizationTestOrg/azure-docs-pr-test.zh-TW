---
title: "教學課程：Azure Active Directory 與 Netsuite 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Netsuite 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a>教學課程：Azure Active Directory 與 Netsuite 整合

在此教學課程中，您學會如何 toointegrate Netsuite 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Netsuite 可以提供下列優點 hello:

- 您可以控制存取 tooNetsuite Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooNetsuite （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與 Netsuite 的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Netsuite 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Netsuite
2. 設定並測試 Azure AD 單一登入

## <a name="adding-netsuite-from-hello-gallery"></a>從 hello 圖庫加入 Netsuite
tooconfigure hello 整合 Netsuite 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Netsuite。

**tooadd Netsuite 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新的應用程式**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Netsuite**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. 在 hello 結果 窗格中，選取  **Netsuite**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Netsuite 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Netsuite 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Netsuite 中相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Netsuite 中。

tooconfigure 及測試 Azure AD 單一登入 Netsuite，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Netsuite](#creating-a-netsuite-test-user)**  -toohave 許 Simon Netsuite 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您 Netsuite 的應用程式中。

**tooconfigure Azure AD 單一登入 Netsuite，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Netsuite**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. 在 hello **Netsuite 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`

    > [!NOTE] 
    > 這不是真實的值。 更新 hello 值與 hello 實際的回覆 URL。 請連絡[Netsuite 支援小組](http://www.netsuite.com/portal/services/support.shtml)tooget 此值。
 
4. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. 在 hello **Netsuite 設定**區段中，按一下**設定 Netsuite** tooopen**設定登入**視窗。 複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. 在瀏覽器中開啟新索引標籤，以系統管理員的身分登入您的 Netsuite 公司站台。

8. 在 hello hello hello 頁頂端的工具列中按一下**安裝**，然後按一下 **安裝管理員**。

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. 從 hello**安裝工作**清單中，選取**整合**。

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. 在 hello**管理驗證**區段中，按一下**SAML 單一登入**。

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. 在 hello **SAML 設定**頁面上，執行下列步驟的 hello:
   
    a. 複製 hello **SAML 單一登入服務 URL**值**快速參考**區段**設定登入**並將它貼到 hello**身分識別提供者登入頁面**Netsuite 欄位。

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    b.這是另一個 C# 主控台應用程式。 在 Netsuite 中，選取 [主要驗證方法] 。

    c. Hello 欄位標示為**SAMLV2 身分識別提供者中繼資料**，選取**上傳 IDP 中繼資料檔案**。 然後按一下 **瀏覽**tooupload hello 中繼資料檔從 Azure 入口網站下載。

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    d. 按一下 [提交] 。

12. 在 Azure AD 中，按一下 [檢視及編輯所有其他使用者屬性] 核取方塊並新增屬性。

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. Hello**屬性名稱**欄位中，輸入`account`。 Hello**屬性值**欄位中，輸入您的 Netsuite 帳戶識別碼。這個值是常數，而與帳戶的變更。 指示如何 toofind 列入您的帳戶識別碼：

      ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    a. 在 Netsuite，按一下 **安裝**hello 上方瀏覽功能表中。

    b. 然後按一下 下 hello**安裝工作**區段 hello 左的導覽功能表上，選取 hello**整合**區段，然後按一下  **Web 服務喜好設定**。

    c. 複製您 Netsuite 的帳戶識別碼，並將它貼到 hello**屬性值**在 Azure AD 中的欄位。

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. 使用者可以執行單一登入 Netsuite 之前，必須先指派 hello Netsuite 中的適當權限。 請遵循以下 tooassign hello 指示這些權限。

    a. 在 hello 頂端導覽功能表上，按一下 **安裝**，然後按一下 **安裝管理員**。
      
      ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    b. 在 hello 左的導覽功能表上，選取 **使用者/角色**，然後按一下 **管理角色**。
      
      ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    c. 按一下 [新角色] 。

    d. 在中輸入**名稱**新角色，及選取 hello**單一登入只**核取方塊。
      
      ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    e. 按一下 [儲存] 。

    f. 在 hello 最上層顯示 hello 功能表上，按一下**權限**。 然後按一下 [設定] 。
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    g. 選取 設定 SAM 單一登入，然後按一下新增。

    h. 按一下 [儲存] 。

    i. 在 hello 頂端導覽功能表上，按一下 **安裝**，然後按一下 **安裝管理員**。
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    j. 在 hello 左的導覽功能表上，選取 **使用者/角色**，然後按一下 **管理使用者**。
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    k. 選取測試使用者。 然後按一下 [編輯] 。
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    l. 在 hello 角色對話方塊中，選取 hello 角色，您已建立，並按一下**新增**。
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    m. 按一下 [儲存] 。
    
> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端，按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。 

### <a name="creating-a-netsuite-test-user"></a>建立 Netsuite 測試使用者

本節會在 Netsuite 中建立名為 Britta Simon 的使用者。 Netsuite 支援預設啟用的 Just-In-Time 佈建。
在這一節沒有您需要進行的動作項目。 如果使用者不存在於 Netsuite，當您嘗試 tooaccess Netsuite 時，會建立一個新。


### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooNetsuite 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooNetsuite，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Netsuite**。

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

您的單一登入設定，開啟 hello 存取面板的 tootest [https://myapps.microsoft.com](https://myapps.microsoft.com/)，登入 hello 測試帳戶，然後按一下**Netsuite**。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定使用者佈建](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png


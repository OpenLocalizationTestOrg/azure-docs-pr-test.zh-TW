---
title: "教學課程：Azure Active Directory 與 IQNavigator VMS 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 IQNavigator VM 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 5a5a7dd3f427acfba2f0ae10552a7179db730118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a>教學課程：Azure Active Directory 與 IQNavigator VMS 整合

在此教學課程中，您學會如何 toointegrate IQNavigator VM 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 IQNavigator VM 可以提供下列優點 hello:

- 您可以控制存取 tooIQNavigator VM 的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooIQNavigator （單一登入） 的 VM 與 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure IQNavigator VM 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 IQNavigator VMS 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 IQNavigator VM
2. 設定並測試 Azure AD 單一登入

## <a name="adding-iqnavigator-vms-from-hello-gallery"></a>從 hello 圖庫加入 IQNavigator VM
tooconfigure hello 整合 IQNavigator VM 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd IQNavigator VM。

**tooadd IQNavigator VM 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**IQNavigator VM**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. 在 hello 結果 窗格中，選取  **IQNavigator VM**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 IQNavigator VMS 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow IQNavigator VM 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello IQNavigator VM 中的相關的使用者之間的連結關聯性需要 toobe 建立。

IQNavigator VM 中指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 IQNavigator VM 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 IQNavigator VM](#creating-a-iqnavigator-vms-test-user)**  -toohave 許 Simon IQNavigator VM 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 IQNavigator VM 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 IQNavigator VM 執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **IQNavigator VM**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. 在 hello **IQNavigator VM 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    a. 在 hello**識別碼**文字方塊中，型別 hello URL:`iqn.com`

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`

4. 請檢查**顯示進階的 URL 設定**，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    在 hello**轉送狀態**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.iqnavigator.com`

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與 hello 實際的回覆 URL 和轉送狀態。 請連絡[IQNavigator VM 用戶端支援小組](https://www.beeline.com/iqn-product-support/)tooget 這些值。 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. toogenerate hello**中繼資料**url，請執行下列步驟的 hello:

    a. 按一下 [應用程式註冊]。
    
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    b. 按一下**端點**tooopen**端點** 對話方塊。  
    
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    c. 按一下 hello 複製按鈕 toocopy**同盟中繼資料文件**url 並將它貼到 [記事本]。
    
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    d. 現在請 toohello 屬性頁的**IQNavigator VM**和複製 hello**應用程式識別碼**使用**複製**按鈕，並將它貼到 [記事本]。
 
    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    e. 產生 hello**中繼資料 URL**使用 hello 下列模式：`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`

7. IQNavigator 應用程式預期 hello 名稱識別碼宣告中的 hello 唯一的使用者識別碼值。 客戶可以將對應 hello 正確 hello 名稱識別碼宣告值。 在此情況下，我們有對應 hello 使用者。UserPrincipalName hello 示範用途。 但是，根據 tooyour 組織設定您應該對應 hello 正確的值為它。   

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. 在 hello **IQNavigator VM 組態**區段中，按一下**設定 IQNavigator VM** tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. tooconfigure 單一登入上**IQNavigator VM**側邊，您需要 toosend hello**中繼資料 URL**，**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**太[IQNavigator VM 支援小組](https://www.beeline.com/iqn-product-support/)。 設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-iqnavigator-vms-test-user"></a>建立 IQNavigator VM 測試使用者

hello 本節目標在於 toocreate 呼叫許 Simon IQNavigator VM 中的使用者。 使用[IQNavigator VM 支援小組](https://www.beeline.com/iqn-product-support/)tooadd hello hello IQNavigator VM 帳戶的使用者。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooIQNavigator VM。

![指派使用者][200] 

**tooassign 許 Simon tooIQNavigator VM，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**IQNavigator VM**。

    ![設定單一登入](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello IQNavigator VM 磚 hello 存取面板中時，您應該取得自動登入 tooyour IQNavigator VM 應用程式。
如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png


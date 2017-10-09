---
title: "教學課程：Azure Active Directory 與 Zscaler Private Access (ZPA) 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Zscaler 私用存取 (ZPA) 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a>教學課程：Azure Active Directory 與 Zscaler Private Access (ZPA) 整合

在此教學課程中，您學會如何 toointegrate Zscaler 私用存取 (ZPA)，與 Azure Active Directory (Azure AD)。

整合 Azure AD 與 Zscaler 私用存取 (ZPA) 可以提供下列優點 hello:

- 您可以控制存取 tooZscaler 私用存取 (ZPA) 的 Azure AD 中
- 您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooZscaler 私用存取 (ZPA) （單一登入）
- 您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 整合與 Zscaler 私用存取 (ZPA)，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Zscaler Private Access (ZPA) 單一登入的訂用帳戶


> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。


在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。


## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Zscaler 私用存取 (ZPA)
2. 設定並測試 Azure AD 單一登入


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a>從 hello 圖庫加入 Zscaler 私用存取 (ZPA)
tooconfigure hello 整合的 Zscaler 私用存取 (ZPA) 至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Zscaler 私用存取 (ZPA)。

**tooadd Zscaler 私用存取 (ZPA)，從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新增**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Zscaler 私用存取 (ZPA)**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. 在 hello 結果 窗格中，選取  **Zscaler 私用存取 (ZPA)**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Zscaler Private Access (ZPA) 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Zscaler 私用存取 (ZPA) 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello 相關的使用者在 Zscaler 私用存取 (ZPA) 之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username**中 Zscaler 私用存取 (ZPA)。

tooconfigure 和測試 Azure AD 單一登入與 Zscaler 私用存取 (ZPA)，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 Zscaler 私用存取 (ZPA) 測試使用者](#creating-a-zscaler-private-access-(zpa)-test-user)** -toohave 許 Simon 中 Zscaler 私用存取 (ZPA) 是連結的 toohello Azure AD 的她的表示法的對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並設定單一登入 Zscaler 私用存取 (ZPA) 應用程式中。

**Azure AD 單一登入的 tooconfigure 與 Zscaler 私用存取 (ZPA)，執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站上 hello **Zscaler 私用存取 (ZPA)**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. 在 hello **Zscaler 私用存取 (ZPA) 網域和 Url**區段中，執行下列步驟的 hello:
    
    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`

    b. 在 hello**識別碼**文字方塊中，輸入：`https://samlsp.private.zscaler.com/auth/metadata`

    > [!NOTE] 
    > 請注意這些不是 hello 實際值。 您有的 tooupdate 這些值與實際的 hello 登入 URL 和識別碼。 這裡我們建議您 toouse hello 中唯一值的 URL hello 識別項。 請連絡[Zscaler 私用存取 (ZPA) 支援小組](https://help.zscaler.com/zpa-submit-ticket)tooget 這些值。

4. 在 hello **SAML 簽章憑證**區段中，按一下**建立新憑證**。

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. 在 [hello**建立新的憑證**] 對話方塊中，按一下 hello 日曆圖示，然後選取**到期日**。 然後按一下 [儲存] 按鈕。

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. 在 hello **SAML 簽章憑證**區段中，選取**啟用新的憑證**按一下**儲存** 按鈕。

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. Hello 快顯視窗上**變換憑證**視窗中，按一下 **確定**。

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. 在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Zscaler Private Access (ZPA) 公司網站。

10. 瀏覽過**管理員**，然後按一下 **Idp 組態**。

    ![在應用程式端設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. 在 hello **Idp 組態**區段中，按一下**加入新的 IDP 組態**。

    ![在應用程式端設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. 在 hello**新 IDP 組態**區段中，執行下列步驟的 hello:

    ![在應用程式端設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    a. 按一下 [選取檔案]，然後上傳您下載的中繼資料檔。

    b. 按一下 [儲存]  按鈕。
    


### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a>建立 Zscaler Private Access (ZPA) 測試使用者

在本節中，您要在 Zscaler Private Access (ZPA) 中建立名為 Britta Simon 的使用者。 請使用[Zscaler 私用存取 (ZPA) 支援小組](https://help.zscaler.com/zpa-submit-ticket)tooadd hello hello Zscaler 私用存取 (ZPA) 平台的使用者。


### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與他們存取 tooZscaler 私用存取 (ZPA)。

![指派使用者][200] 

**tooassign 許 Simon tooZscaler 私用存取 (ZPA) 執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Zscaler 私用存取 (ZPA)**。

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    


### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello Zscaler 私用存取 (ZPA) 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 Zscaler 私用存取 (ZPA) 應用程式。


## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png
---
title: "教學課程：Azure Active Directory 與 FirmPlay - Employee Advocacy for Recruiting 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 FirmPlay-招募的員工關注之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a>教學課程：Azure Active Directory 與 FirmPlay - Employee Advocacy for Recruiting 整合

在此教學課程中，您學會如何 toointegrate FirmPlay-招募與 Azure Active Directory (Azure AD) 的員工關注。

整合 FirmPlay-招募與 Azure AD 的員工關注可以提供下列優點 hello:

- 您可以控制存取 tooFirmPlay-招募的員工關注 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooFirmPlay-招募 （單一登入） 的員工關注他們的 Azure AD 帳戶與
- 您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與 FirmPlay-招募的員工關注的 Azure AD 整合您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 FirmPlay - Employee Advocacy for Recruiting 單一登入的訂用帳戶


> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。


在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。


## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 加入 FirmPlay-招募從 hello 組件庫的員工關注
2. 設定並測試 Azure AD 單一登入


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a>加入 FirmPlay-招募從 hello 組件庫的員工關注
tooconfigure hello 整合 FirmPlay 位員工關注，如招募到 Azure AD，您需要 tooadd FirmPlay-招募 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式的員工關注。

**tooadd FirmPlay-hello 庫、 招募的員工關注執行 hello 下列步驟：**

1. 在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新增**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**FirmPlay-招募的員工關注**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. 在 hello 結果 窗格中，選取  **FirmPlay-招募的員工關注**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FirmPlay - Employee Advocacy for Recruiting 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 FirmPlay-招募的員工關注是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello FirmPlay-招募的員工關注中相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** FirmPlay-招募的員工關注中。

tooconfigure 和測試 Azure AD 單一登入與 FirmPlay 位員工關注，如招募，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 FirmPlay-招募測試使用者的員工關注](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** -toohave 許 Simon FirmPlay 中對應項目： 員工關注，如招募也就連結 toohello Azure AD 的她的表示法。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並設定單一登入您 FirmPlay 位員工關注招募應用程式中。

**Azure AD 單一登入與 FirmPlay-招募的員工關注的 tooconfigure 執行 hello 下列步驟：**

1. 在 hello Azure 管理入口網站上 hello **FirmPlay-招募的員工關注**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. 在 hello **FirmPlay-招募網域和 Url 的員工關注**區段中的，在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<your-subdomain>.firmplay.com/`

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > 請注意，這不是 hello 真正的價值。 您有的 tooupdate 這個值與實際的 hello 登入 URL。 請連絡[FirmPlay-招募支援小組的員工關注](mailto:engineering@firmplay.com)tooget 此值。 

4. 在 hello **SAML 簽章憑證**區段中，按一下**建立新憑證**。

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. 在 [hello**建立新的憑證**] 對話方塊中，按一下 hello 日曆圖示，然後選取**到期日**。 然後按一下 [儲存] 按鈕。

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. 在 hello **SAML 簽章憑證**區段中，選取**啟用新的憑證**按一下**儲存** 按鈕。

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. Hello 快顯視窗上**變換憑證**視窗中，按一下 **確定**。

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (base64)**然後儲存您的電腦上的 hello 憑證檔案。 

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. 在 hello **FirmPlay-招募組態的員工關注**區段中，按一下**設定 FirmPlay-招募的員工關注**tooopen**設定登入**對話方塊。

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. tooget SSO 設定應用程式，請連絡[FirmPlay-招募支援小組的員工關注](mailto:engineering@firmplay.com)，提供下列 hello: 

    • hello 下載**憑證檔案**

    • hello **SAML 單一登入服務 URL**

    • hello **SAML 實體識別碼**

    • hello**登出 URL**
  

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a>建立 FirmPlay - Employee Advocacy for Recruiting 測試使用者

在本節中，您要在 FirmPlay - Employee Advocacy for Recruiting 中建立名為 Britta Simon 的使用者。 請使用[FirmPlay-招募支援小組的員工關注](mailto:engineering@firmplay.com)tooadd hello hello FirmPlay 位員工關注招募平台的使用者。


### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與他們存取 tooFirmPlay-招募的員工關注。

![指派使用者][200] 

**tooassign 許 Simon tooFirmPlay 位員工關注，如招募，執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**FirmPlay-招募的員工關注**。

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    


### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello FirmPlay-招募磚 hello 存取面板中的員工關注您應該取得自動登入 tooyour FirmPlay-招募應用程式的員工關注。


## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png
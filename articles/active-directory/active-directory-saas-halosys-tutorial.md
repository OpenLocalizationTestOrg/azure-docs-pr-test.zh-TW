---
title: "教學課程：Azure Active Directory 與 Halosys 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Halosys 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a>教學課程：Azure Active Directory 與 Halosys 整合

在此教學課程中，您學會如何 toointegrate Halosys 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Halosys 可以提供下列優點 hello:

- 您可以控制存取 tooHalosys Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooHalosys （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Halosys 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Halosys 單一登入的訂用帳戶


> [!NOTE] 
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。


在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。


## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。

本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Halosys
2. 設定並測試 Azure AD 單一登入


## <a name="adding-halosys-from-hello-gallery"></a>從 hello 圖庫加入 Halosys
tooconfigure hello 整合 Halosys 到 Azure AD，您需要 tooadd Halosys hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Halosys 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。

    ![Active Directory][1]
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。

    ![應用程式][2]

4. 按一下**新增**hello hello 頁底端。

    ![應用程式][3]

5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。

    ![應用程式][4]

6. 在 [hello] 搜尋方塊中，輸入**Halosys**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. 在 hello 結果窗格中，選取  **Halosys**，然後按一下**完成**tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Halosys 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Halosys 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Halosys 中相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Halosys 中。

tooconfigure 及 Halosys 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Halosys](#creating-a-halosys-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Halosys 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello 傳統入口網站中，並 Halosys 應用程式中設定單一登入。


**tooconfigure Azure AD 單一登入與 Halosys，執行下列步驟的 hello:**

1. Hello 傳統入口網站中，在 hello **Halosys**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。
     
    ![設定單一登入][6] 

2. 在 hello**如何想您使用者 toosign tooHalosys 上**頁面上，選取**Azure AD 單一登入**，然後按一下**下一步**。

    ![設定單一登入](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. 在 hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    a. 在 hello**登入 URL**文字方塊中，應用程式所使用的使用者 toosign 上 tooyour Halosys 使用 hello 遵循模式的型別 hello URL: `https://<company-name>.Halosys.com/client-api/api`。

    b.In hello**識別項 URL** hello 遵循模式中的型別 hello URL 文字方塊中： `https://<company-name>.Halosys.com`。 
         
4. 在 hello **Halosys 在設定單一登入**頁面上，按一下**下載中繼資料**，然後儲存您的電腦上的 hello 檔案：

    ![設定單一登入](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. 設定應用程式的 SSO tooget 連絡 Halosys 支援小組，並提供他們最 hello 下列：

    • hello 下載**中繼資料檔案**
    
    • hello **SAML SSO URL**
    

6. Hello 傳統入口網站中選取 hello 單一登入組態確認，然後**下一步**。
    
    ![Azure AD 單一登入][10]

7. 在 hello**單一登入確認**頁面上，按一下**完成**。  
 
    ![Azure AD 單一登入][11]


### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
在本節中，您可以建立測試使用者呼叫許 Simon hello 傳統入口網站中。


![建立 Azure AD 使用者][20]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. 在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png) 

    a. 針對 [使用者類型]，選取 [您組織中的新使用者]。

    b. 在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。

    c. 按一下 [下一步] 。

6.  在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 

    a. 在 hello**名字**文字方塊中，輸入**許**。  

    b. 在 hello**姓氏**文字方塊中，輸入， **Simon**。

    c. 在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。

    d. 在 hello**角色**清單中，選取**使用者**。

    e. 按一下 [下一步] 。

7. 在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. 在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    a. 請記下 hello hello 值**新密碼**。

    b. 按一下頁面底部的 [新增] 。   



### <a name="creating-a-halosys-test-user"></a>建立 Halosys 測試使用者

在本節中，您要在 Halosys 中建立名為 Britta Simon 的使用者。 請使用 Halosys 支援小組 tooadd hello 使用者在 hello Halosys 平台。


### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與他們存取 tooHalosys 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooHalosys，執行下列步驟的 hello:**

1. Hello 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Halosys**。

    ![設定單一登入](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. 在 hello 最上層顯示 hello 功能表上，按一下**使用者**。

    ![指派使用者][203]

4. 在 hello 使用者清單中選取**許 Simon**。

5. 在 hello hello 底部的工具列中按一下**指派**。

    ![指派使用者][205]


### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下的 hello Halosys 磚 hello 存取面板中時，您應該取得自動登入 tooyour Halosys 應用程式。


## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png

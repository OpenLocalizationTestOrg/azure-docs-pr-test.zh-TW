---
title: "教學課程：Azure Active Directory 與 Splunk Enterprise and Splunk Cloud 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Splunk 企業和 Splunk 雲端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a>教學課程：Azure Active Directory 與 Splunk Enterprise and Splunk Cloud 整合

在此教學課程中，您學會如何 toointegrate Splunk 企業和 Splunk 雲端與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Splunk 企業和 Splunk 雲端可以提供下列優點 hello:

- 您可以控制可以存取 Azure AD 中 tooSplunk 企業和 Splunk 雲端
- 您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooSplunk 企業和雲端 Splunk 單一登入 (SSO)
- 您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Splunk 企業與 Splunk 雲端的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Splunk Enterprise or Splunk Cloud SSO 的訂用帳戶


>[!NOTE]
>本教學課程中的步驟 tootest hello，不建議使用實際執行環境。
>

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。


## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。

本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Splunk 企業和 Splunk 雲端
2. 設定並測試 Azure AD SSO


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a>從 hello 圖庫新增 Splunk 企業和 Splunk 雲端
tooconfigure hello 整合 Splunk 企業和 Splunk 雲端到 Azure AD，您需要 tooadd Splunk 企業和 Splunk 雲端 hello 圖庫 tooyour 清單中的受管理 SaaS 應用程式。

**tooadd Splunk 企業和 Splunk 雲端 hello 圖庫中，從執行下列步驟的 hello:**

1. 在 [hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。

    ![Active Directory][1]

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。

    ![應用程式][2]

4. 按一下**新增**hello hello 頁底端。

    ![應用程式][3]

5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。

    ![應用程式][4]

6. 在 [hello] 搜尋方塊中，輸入**Splunk 企業或 Splunk 雲端**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. 在 [hello] 結果窗格中，選取 [ **Splunk 企業和 Splunk 雲端**，然後按一下 [**完成**tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Splunk Enterprise and Splunk Cloud 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow Splunk 企業和 Splunk 雲端中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Splunk 企業和 Splunk 雲端中的相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Splunk 企業和 Splunk 雲端中。

tooconfigure 及測試 Azure AD 單一登入與 Splunk 企業和 Splunk 雲端，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Splunk 企業和 Splunk 雲端](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** -toohave 許 Simon Splunk 企業中，她連結的 toohello Azure AD 表示 Splunk 雲端對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以 hello 傳統入口網站中啟用 Azure AD SSO，並 Splunk 企業和 Splunk 雲端應用程式中設定單一登入。


**Azure AD 單一登入的 tooconfigure Splunk 企業與 Splunk 雲端執行 hello 下列步驟：**

1. Hello 傳統入口網站中，在 [hello **Splunk 企業和 Splunk 雲端**應用程式整合頁面上，按一下 [**設定單一登入**tooopen hello**設定單一登入**對話方塊。
     
    ![設定單一登入][6] 

2. 在 hello**要如何讓使用者 toosign 上 tooSplunk 企業和 Splunk 雲端**頁面上，選取**Azure AD 單一登入**，然後按一下 [**下一步**。

    ![設定單一登入](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. 在 [hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. 在 [hello**登入 URL**文字方塊中，您的使用者 toosign 上 tooyour Splunk 企業和使用下列模式的 hello Splunk 雲端應用程式所使用的型別 hello URL:`https://<splunkserverUrl>/en-US/app/launcher/home`
  2. 在 [hello**識別碼**Splunk 伺服器的型別 hello URL] 文字方塊中。
  3. 在 [hello**回覆 URL**文字方塊中，以下列模式的 hello 類型 hello URL:`https://<splunkserver>/saml/acs`
  4. 按一下 [下一步] 。
 
4. 在 [hello **Splunk 企業和 Splunk 雲端在設定單一登入**頁面上，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. 按一下**下載中繼資料**，然後儲存您的電腦上的 hello 檔案。
  2. 按一下 [下一步] 。

5. tooget SSO 設定應用程式連絡 Splunk 企業和雲端 Splunk 支援小組，並提供 hello 下列：

    * 下載的 hello **federaton 中繼資料**
6. Hello 傳統入口網站中選取 hello 單一登入組態確認，然後**下一步**。
    
    ![Azure AD 單一登入][10]

7. 在 [hello**單一登入確認**頁面上，按一下**完成**。  
 
    ![Azure AD 單一登入][11]

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
在本節中，您可以建立測試使用者呼叫許 Simon hello 傳統入口網站中。

![建立 Azure AD 使用者][20]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. 在 [hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. 針對 [使用者類型]，選取 [您組織中的新使用者]。
  2. 在 [hello 使用者名稱**文字方塊**，型別**BrittaSimon**。
  3. 按一下 [下一步] 。

6.  在 [hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:
  
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. 在 [hello**名字**文字方塊中，輸入**許**。  
  2. 在 [hello**姓氏**文字方塊中，輸入， **Simon**。
  3. 在 [hello**顯示名稱**文字方塊中，輸入**許 Simon**。
  4. 在 [hello**角色**清單中，選取**使用者**。
  5. 按一下 [下一步] 。

7. 在 [hello**取得暫時密碼**對話方塊頁面上，按一下 [**建立**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. 在 [hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. 請記下 hello hello 值**新密碼**。
  2. 按一下頁面底部的 [新增] 。   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a>建立 Splunk Enterprise and Splunk Cloud 測試使用者

在本節中，您要在 Splunk Enterprise and Splunk Cloud 中建立名為 Britta Simon 的使用者。 請使用 Splunk 企業和雲端 Splunk 支援小組 tooadd hello 使用者在 hello Splunk 企業和 Splunk 雲端平台。


### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以啟用許 Simon toouse Azure SSOy 授與他們存取 tooSplunk 企業和 Splunk 雲端。

![指派使用者][200] 

**tooassign 許 Simon tooSplunk 企業和 Splunk 雲端，執行下列步驟的 hello:**

1. Hello 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Splunk 企業和 Splunk 雲端**。

    ![設定單一登入](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. 在 [hello 最上層顯示 hello 功能表上，按一下**使用者**。

    ![指派使用者][203]

4. 在 hello 使用者清單中選取**許 Simon**。

5. 在 hello hello 底部的工具列中按一下**指派**。

    ![指派使用者][205]

### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您可以測試使用存取面板 hello 您 Azure AD SSOonfiguration。

當您按一下 hello Splunk 企業和雲端 Splunk 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Splunk 企業和 Splunk 雲端應用程式。


## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png

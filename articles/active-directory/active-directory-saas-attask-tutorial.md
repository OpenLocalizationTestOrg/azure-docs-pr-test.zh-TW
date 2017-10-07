---
title: "教學課程： Azure Active Directory 整合與@Task|Microsoft 文件"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間和@Task。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a>教學課程：Azure Active Directory 與 @Task 整合
本教學課程的 hello 目標是 tooshow 您如何 toointegrate@Task與 Azure Active Directory (Azure AD)。  
整合@Task與 Azure AD 為您提供下列優點 hello: 

* 您可以控制可以存取 Azure AD 中too@Task
* 您可以讓的使用者登入取得 tooautomatically too@Task （單一登入） 具有其 Azure AD 帳戶
* 您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件
與 tooconfigure Azure AD 整合@Task，您需要下列項目 hello:

* Azure AD 訂用帳戶
* 啟用 @Task 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。
> 
> 

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

* 除非必要，否則您不應使用生產環境，。
* 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。 

## <a name="scenario-description"></a>案例描述
本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 單一登入的測試環境中。  
本教學課程所述的 hello 案例包含三個主要建置組塊：

1. 加入@Task從 hello 組件庫 
2. 設定並測試 Azure AD 單一登入

## <a name="adding-task-from-hello-gallery"></a>加入@Task從 hello 組件庫
tooconfigure hello 整合@Task到 Azure AD，您需要 tooadd @Task hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd @Task hello 圖庫中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。 
   
    ![Active Directory][1] 
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
    ![應用程式][2] 
4. 按一下**新增**hello hello 頁底端。
   
    ![應用程式][3] 
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
    ![應用程式][4] 
6. 在 [hello] 搜尋方塊中，輸入 **@Task** 。
   
    ![應用程式][5] 
7. 在 hello 結果窗格中，選取   **@Task** ，然後按一下**完成**tooadd hello 應用程式。
   
    ![應用程式][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
hello 本節的目標是您 tooconfigure 和測試 Azure AD 的單一登入與 tooshow@Task根據稱為 「 許 Simon"的測試使用者。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中@Tasktooan 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello 中相關的使用者之間的連結關聯性@Task需要 toobe 建立。   
此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username**中@Task。

tooconfigure 和測試 Azure AD 單一登入與@Task，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立@Tasktest使用者](#creating-a-halogen-software-test-user)** -toohave 的對應項目中的許 Simon@Taskthat是連結的 toohello Azure AD 的她的表示法。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入
hello 本節目標在於 tooenable Azure AD 單一登入 Azure 傳統入口網站 hello 和 tooconfigure 單一登入您@Task應用程式。

**使用 Azure AD 單一登入 tooconfigure @Task，執行下列步驟的 hello:**

1. 在 Azure 傳統入口網站，在 hello hello  **@Task** 應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入** 對話方塊。
   
    ![設定單一登入][6] 
2. 在 hello**如何想您使用者 toosign 上too@Task**頁面上，選取**Azure AD 單一登入**，然後按一下**下一步**。
   
    ![Azure AD 單一登入][7] 
3. 在 hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello:
   
    ![設定 App 設定][8] 
   
     a. 在 hello**登入 URL**文字方塊中，供您使用者 toosign 上 tooyour 類型 hello URL@Task應用程式 (例如：*https://<Tenant name>.attask ondemand.com*)。
   
     b. 按一下 [下一步] 。
4. 在 hello**設定單一登入在@Task**頁面上，按一下**下載中繼資料**，儲存在本機電腦上的 hello 中繼資料檔案，然後按一下**下一步**。
   
    ![何謂 Azure AD Connect][9] 
5. 登入 tooyour@Task以系統管理員身分的公司網站。
6. 跳過**單一登入組態**。
7. 在 [hello**單一登入**] 對話方塊中，執行下列步驟的 hello
   
    ![設定單一登入][23]
   
    a. 針對 [類型]，選取 [SAML 2.0]。
   
    b. 選取 [服務提供者識別碼]。
   
    c. 在 hello Azure 傳統入口網站中，複製 hello**遠端登入 URL**，然後將它貼入 hello**登入入口網站 URL**文字方塊。
   
    d. 在 hello Azure 傳統入口網站中，複製 hello**單一登出服務 URL**，然後將它貼入 hello**登出 URL**文字方塊。
   
    e. 在 hello Azure 傳統入口網站中，複製 hello**變更密碼 URL**，然後將它貼入 hello**變更密碼 URL**文字方塊。
   
    f. 按一下 [儲存] 。
8. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**下一步**。 
   
    ![何謂 Azure AD Connect][10]
9. 在 hello**單一登入確認**頁面上，按一下**完成**。  
   
    ![何謂 Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 傳統入口網站中的測試使用者。  

![建立 Azure AD 使用者][20]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. 在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello: 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    a. 針對 [使用者類型]，選取 [您組織中的新使用者]。
   
    b. 在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。
   
    c. 按一下 [下一步] 。
6. 在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello: 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    a. 在 hello**名字**文字方塊中，輸入**許**。  
   
    b. 在 hello**姓氏**文字方塊中，輸入， **Simon**。
   
    c. 在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。
   
    d. 在 hello**角色**清單中，選取**使用者**。

    e. 按一下 [下一步] 。

7. 在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. 在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    a. 請記下 hello hello 值**新密碼**。
   
    b. 按一下 [完成]。   

### <a name="creating-an-task-test-user"></a>建立 @Task 測試使用者
hello 本節目標在於 toocreate 使用者，在呼叫許 Simon @Task。

**使用者在呼叫許 Simon toocreate @Task，執行下列步驟的 hello:**

1. 登入 tooyour@Task以系統管理員身分的公司網站。
2. 在 hello 最上層顯示 hello 功能表上，按一下**人員**。
3. 按一下 [新增人員] 。 
4. 在 hello 新增人員 對話方塊中，執行下列步驟的 hello:
   
    ![建立 @Task 測試使用者][21] 
   
    a. 在 hello**名字**文字方塊中，輸入 「 許"。
   
    b. 在 hello**姓氏**文字方塊中，輸入 「 Simon"。
   
    c. 在 hello**電子郵件地址**文字方塊中，輸入 Azure Active Directory 中許 Simon 的電子郵件地址。
   
    d. 按一下 [新增人員] 。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者
本節 hello 目標是 tooenabling 許 Simon toouse Azure 單一登入授與他們存取too@Task。

![指派使用者][200] 

**tooassign 許 Simon too@Task，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，tooopen hello 應用程式 檢視，在 hello 目錄檢視中，按一下 **應用程式**hello 上方功能表中。
   
    ![指派使用者][201] 
2. 在 [hello] 應用程式清單中，選取 **@Task** 。
   
    ![指派使用者][202] 
3. 在 hello 最上層顯示 hello 功能表上，按一下**使用者**。
   
    ![指派使用者][203] 
4. 在 hello 使用者清單中選取**許 Simon**。
5. 在 hello hello 底部的工具列中按一下**指派**。
   
    ![指派使用者][205]

### <a name="testing-single-sign-on"></a>測試單一登入
hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。  
當您按一下 hello@Task以並排顯示 hello 存取面板中，您應該取得自動登入 tooyour@Task應用程式。

## <a name="additional-resources"></a>其他資源
* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png







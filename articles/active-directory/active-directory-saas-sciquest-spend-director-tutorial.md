---
title: "教學課程：Azure Active Directory 與 SciQuest Spend Director 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SciQuest Spend Director 之間的單一登入。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 84b707668dc45e92e6151f422f1c919f638533b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a>教學課程：Azure Active Directory 與 SciQuest Spend Director 整合
本教學課程旨在說明如何整合 SciQuest Spend Director 與 Azure Active Directory (Azure AD)。  
SciQuest Spend Director 與 Azure AD 整合提供下列優點： 

* 您可以在 Azure AD 中控制可存取 SciQuest Spend Director 的人員。 
* 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SciQuest Spend Director (單一登入)
* 您可以在 Azure 傳統入口網站中集中管理您的帳戶

若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件
若要使用 SciQuest Spend Director 設定 Azure AD 整合，您需要以下項目：

* Azure AD 訂用帳戶
* 啟用 SciQuest Spend Director 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。
> 
> 

若要測試本教學課程中的步驟，您應該遵循這些建議：

* 除非必要，否則您不應使用生產環境，。
* 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。 

## <a name="scenario-description"></a>案例描述
此教學課程的目標是讓您在測試環境中測試 Azure AD 單一登入。  
本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 SciQuest Spend Director 
2. 設定並測試 Azure AD 單一登入

## <a name="adding-sciquest-spend-director-from-the-gallery"></a>從資源庫新增 SciQuest Spend Director
若要設定 SciQuest Spend Director 與 Azure AD 整合，您需要從資源庫將 SciQuest Spend Director 加入 受管理 SaaS app 的清單。

**若要從資源庫新增 SciQuest Spend Director，請執行下列步驟：**

1. 在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。 
   
    ![Active Directory][1]

2. 從 [目錄]  清單中，選取要啟用目錄整合的目錄。

3. 若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。
   
    ![應用程式][2]

4. 按一下頁面底部的 [新增]  。
   
    ![應用程式][3]

5. 在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。
   
    ![應用程式][4]

6. 在搜尋方塊中，輸入 **sciQuest spend director**。
   
    ![應用程式][5]

7. 在結果窗格中，選取 [SciQuest Spend Director]，然後按一下 [完成] 來新增應用程式。
   
    ![應用程式][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
本節的目標是說明如何以名為 "Britta Simon" 的測試使用者為基礎，使用 SciQuest Spend Director 來設定及測試 Azure AD 單一登入。

單一登入若要運作，Azure AD 必須知道 SciQuest Spend Director 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者與 SciQuest Spend Director 中的相關使用者之間建立連結關聯性。  
建立此連結關聯性的方法是將 Azure AD 中的**使用者名稱**的值指定為 SciQuest Spend Director 中 **Username**的值。

若要使用 SciQuest Spend Director 設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 SciQuest Spend Director 測試使用者](#creating-a-halogen-software-test-user)** - 使 SciQuest Spend Director 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-single-sign-on"></a>設定 Azure AD 單一登入
本節目標是在 Azure 傳統入口網站啟用 Azure AD 單一登入，並在您的 SciQuest Spend Director 應用程式中設定單一登入。

**若要使用 SciQuest Spend Director 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 傳統入口網站的 [SciQuest Spend Director] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。
   
    ![設定單一登入][8]

2. 在 [要如何讓使用者登入 SciQuest Spend Director] 頁面上，選取 [Azure AD 單一登入]，然後按 [下一步]。
   
    ![Azure AD 單一登入][9]

3. 在 [設定應用程式設定]  對話方塊頁面上，執行下列步驟： 
   
    ![設定 App 設定][10]
   
     a. 在 [登入 URL] 文字方塊中，使用以下模式輸入使用者登入您的 SciQuest Spend Director 應用程式時所使用的 URL：*https://.*sciquest.com/.**
   
     b. 在 [回覆 URL] 文字方塊中，輸入您在 [登入 URL] 文字方塊所輸入的相同值。 
   
     c. 按一下 [下一步] 。

4. 在 [設定在 SciQuest Spend Director 單一登入] 頁面上，按一下 [下載中繼資料]，然後將中繼資料檔儲存在您的本機電腦上。
   
    ![何謂 Azure AD Connect][11]

5. 連絡 SciQuest 支援來啟用使用上述下載的中繼資料進行驗證的方法。

6. 在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。 
   
    ![何謂 Azure AD Connect][15]

7. 在 [單一登入確認] 頁面上，按一下 [完成]。  

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 傳統入口網站中建立一個名為 Britta Simon 的測試使用者。

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。
   
    ![何謂 Azure AD Connect][100] 

2. 從 [目錄]  清單中，選取要啟用目錄整合的目錄。

3. 若要顯示使用者清單，請按一下頂端功能表中的 [使用者] 。
   
    ![何謂 Azure AD Connect][101] 

4. 若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。 
   
    ![何謂 Azure AD Connect][102] 

5. 在 [告訴我們這位使用者]  對話方塊頁面上，執行下列步驟：
   
    ![何謂 Azure AD Connect][103] 
   
    a. 針對 [使用者類型]，選取 [您組織中的新使用者]。
   
    b. 在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。
   
    c. 按一下 [下一步] 。

6. 在 [使用者設定檔]  對話方塊頁面上，執行下列步驟： 
   
    ![何謂 Azure AD Connect][104] 
   
    a. 在 [名字] 文字方塊中，輸入 **Britta**。  
   
    b. 在 [姓氏] 文字方塊中輸入 **Simon**。
   
    c. 在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。
   
    d. 在 [角色] 清單中選取 [使用者]。
   
    e. 按一下 [下一步] 。

7. 在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。
   
    ![何謂 Azure AD Connect][105]  

8. 在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：
   
    ![何謂 Azure AD Connect][106]   
   
    a. 記下 [新密碼] 的值。
   
    b. 按一下 [完成]。   

### <a name="creating-a-sciquest-spend-director-test-user"></a>建立 SciQuest Spend Director 測試使用者
本節目標是在 SciQuest Spend Director 中建立名為 Britta Simon 的使用者。

您需要連絡您的 SciQuest Spend Director 支援小組，並提供他們與您的測試帳戶有關的詳細資料來建立帳戶。

您也可以利用 Just-In-Time 佈建功能，這是 SciQuest Spend Director 支援的單一登入功能。  
啟用 Just-In-Time 佈建時，如果使用者不存在，SciQuest Spend Director 就會在使用者嘗試執行單一登入期間自動建立使用者。 使用此功能時就不需要手動建立單一登入對應使用者。

若要啟用 Just-In-Time 佈建，您需要連絡您的 SciQuest Spend Director 支援小組。

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者
本節目標是授與 Britta Simon 對 SciQuest Spend Director 的存取權，讓她能夠使用 Azure 單一登入。

![何謂 Azure AD Connect][200]

**若要指派 Britta Simon 到 SciQuest Spend Director，請執行以下步驟：**

1. 在 Azure 傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。
   
    ![何謂 Azure AD Connect][201]

2. 在應用程式清單中，選取 [SciQuest Spend Director] 。
   
    ![何謂 Azure AD Connect][202]

3. 在頂端的功能表中，按一下 [使用者] 。
   
    ![何謂 Azure AD Connect][203]

4. 在 [使用者] 清單中，選取 [Britta Simon] 。
   
    ![何謂 Azure AD Connect][204]

5. 在底部的工具列中，按一下 [指派] 。
   
    ![何謂 Azure AD Connect][205]

### <a name="testing-single-sign-on"></a>測試單一登入
本節的目標是要使用存取面板來測試您的 Azure AD 單一登入組態。  
當您在存取面板中按一下 [SciQuest Spend Director] 圖格時，您應該會自動登入您的 SciQuest Spend Director 應用程式。

## <a name="additional-resources"></a>其他資源
* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png


---
title: "教學課程：Azure Active Directory 與 SciQuest Spend Director 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SciQuest 花主管之間。"
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
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a>教學課程：Azure Active Directory 與 SciQuest Spend Director 整合
本教學課程的 hello 目標是 tooshow 您如何 toointegrate SciQuest 花導向器搭配 Azure Active Directory (Azure AD)。  
與 Azure AD 整合 SciQuest 花主管可以提供下列優點的 hello: 

* 您可以在 Azure AD 中已存取 tooSciQuest 支出主管人員控制 
* 您可以啟用您的使用者 tooautomatically get 登入 tooSciQuest （單一登入） 具有其 Azure AD 帳戶的支出導向器
* 您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件
tooconfigure SciQuest 花導向器與 Azure AD 整合，您需要下列項目 hello:

* Azure AD 訂用帳戶
* 啟用 SciQuest Spend Director 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。
> 
> 

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

* 除非必要，否則您不應使用生產環境，。
* 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。 

## <a name="scenario-description"></a>案例描述
本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 單一登入的測試環境中。  
本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 SciQuest 花導向器 
2. 設定並測試 Azure AD 單一登入

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a>從 hello 圖庫加入 SciQuest 花導向器
tooconfigure hello 整合 SciQuest 花主管到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd SciQuest 花導向器。

**tooadd SciQuest 花導演 hello 圖庫中，執行下列步驟的 hello:**

1. 在 [hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。 
   
    ![Active Directory][1]

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
    ![應用程式][2]

4. 按一下**新增**hello hello 頁底端。
   
    ![應用程式][3]

5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
    ![應用程式][4]

6. 在 [hello] 搜尋方塊中，輸入**sciQuest 花主管**。
   
    ![應用程式][5]

7. 在 [hello] 結果窗格中，選取**SciQuest 花主管**，然後按一下**完成**tooadd hello 應用程式。
   
    ![應用程式][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Azure AD 單一登入與 SciQuest 花導向器根據稱為 「 許 Simon"的測試使用者。

單一登入 toowork，Azure AD 需要 tooknow SciQuest 花主管 tooan 使用者在 Azure AD 中哪些 hello 對等項目的使用者。 換句話說，Azure AD 使用者與 hello SciQuest 花導向器中的相關的使用者之間的連結關聯性需要 toobe 建立。  
此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**SciQuest 花導向器中。

tooconfigure 及測試 Azure AD 單一登入與 SciQuest 花導向器，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 SciQuest 花主管](#creating-a-halogen-software-test-user)** -toohave 許 Simon SciQuest 花導向器所連結的 toohello Azure AD 的她的表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-single-sign-on"></a>設定 Azure AD 單一登入
本節 hello 目標是 tooenable Azure AD 單一登入 Azure 傳統入口網站 hello 和 tooconfigure 單一登入 SciQuest 花導向器應用程式中。

**Azure AD 單一登入的 tooconfigure SciQuest 花導向器，以執行 hello 下列步驟：**

1. 在 Azure 傳統入口網站，在 [hello hello **SciQuest 花主管**應用程式整合頁面上，按一下 [**設定單一登入**tooopen hello**設定單一登入**對話方塊。
   
    ![設定單一登入][8]

2. Hello 上**如何想您 tooSciQuest 支出導向器上的使用者 toosign**頁面上，選取**Azure AD 單一登入**，然後按一下 [**下一步**。
   
    ![Azure AD 單一登入][9]

3. 在 [hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello: 
   
    ![設定 App 設定][10]
   
     a. 在 [hello**登入 URL**文字方塊中，輸入您的使用者 toosign 上使用下列模式的 hello tooyour SciQuest 花導向器應用程式所使用的 URL: *https://。*sciquest.com/.**
   
     b. 在 [hello**回覆 URL**文字方塊中，型別 hello 相同值已輸入 hello**登入 URL**文字方塊。 
   
     c. 按一下 [下一步] 。

4. 在 [hello **SciQuest 花主管在設定單一登入**頁面上，按一下**下載中繼資料**，然後儲存在本機電腦上的 hello 中繼資料檔案。
   
    ![何謂 Azure AD Connect][11]

5. 請連絡 SciQuest 支援 tooenable 這種驗證方法使用 hello 上述下載中繼資料。

6. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。 
   
    ![何謂 Azure AD Connect][15]

7. 在 [hello**單一登入確認**頁面上，按一下**完成**。  

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 傳統入口網站中的測試使用者。

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![何謂 Azure AD Connect][100] 

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。
   
    ![何謂 Azure AD Connect][101] 

4. tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。 
   
    ![何謂 Azure AD Connect][102] 

5. 在 [hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:
   
    ![何謂 Azure AD Connect][103] 
   
    a. 針對 [使用者類型]，選取 [您組織中的新使用者]。
   
    b. 在 [hello 使用者名稱**文字方塊**，型別**BrittaSimon**。
   
    c. 按一下 [下一步] 。

6. 在 [hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello: 
   
    ![何謂 Azure AD Connect][104] 
   
    a. 在 [hello**名字**文字方塊中，輸入**許**。  
   
    b. 在 [hello**姓氏**txtbox，型別， **Simon**。
   
    c. 在 [hello**顯示名稱**文字方塊中，輸入**許 Simon**。
   
    d. 在 [hello**角色**清單中，選取**使用者**。
   
    e. 按一下 [下一步] 。

7. 在 [hello**取得暫時密碼**對話方塊頁面上，按一下 [**建立**。
   
    ![何謂 Azure AD Connect][105]  

8. 在 [hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:
   
    ![何謂 Azure AD Connect][106]   
   
    a. 請記下 hello hello 值**新密碼**。
   
    b. 按一下 [完成]。   

### <a name="creating-a-sciquest-spend-director-test-user"></a>建立 SciQuest Spend Director 測試使用者
hello 本節目標在於 toocreate 呼叫許 Simon SciQuest 花導向器中的使用者。

您需要 toocontact SciQuest 花主管支援小組，並為他們提供有關您建立它的測試帳戶 tooget hello 詳細資料。

您也可以利用 Just-In-Time 佈建功能，這是 SciQuest Spend Director 支援的單一登入功能。  
啟用 Just-In-Time 佈建時，如果使用者不存在，SciQuest Spend Director 就會在使用者嘗試執行單一登入期間自動建立使用者。 這項功能會排除 hello 需要 toomanually 建立單一登入對等項目的使用者。

tooget 中 just-in-time 佈建啟用，您需要 toocontact 正在 SciQuest 花主管支援小組。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者
本節 hello 目標是 tooenabling 許 Simon toouse Azure 單一登入授與他們存取 tooSciQuest 支出導向器。

![何謂 Azure AD Connect][200]

**tooassign 許 Simon tooSciQuest 支出導向器，執行下列步驟的 hello:**

1. 在 [hello Azure 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。
   
    ![何謂 Azure AD Connect][201]

2. 在 [hello] 應用程式清單中，選取**SciQuest 花主管**。
   
    ![何謂 Azure AD Connect][202]

3. 在 [hello 最上層顯示 hello 功能表上，按一下**使用者**。
   
    ![何謂 Azure AD Connect][203]

4. 在 hello 使用者清單中選取**許 Simon**。
   
    ![何謂 Azure AD Connect][204]

5. 在 hello hello 底部的工具列中按一下**指派**。
   
    ![何謂 Azure AD Connect][205]

### <a name="testing-single-sign-on"></a>測試單一登入
hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。  
當您按一下 hello SciQuest 花主管磚 hello 存取面板中的時，您應該取得自動登入 tooyour SciQuest 花導向器應用程式。

## <a name="additional-resources"></a>其他資源
* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
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


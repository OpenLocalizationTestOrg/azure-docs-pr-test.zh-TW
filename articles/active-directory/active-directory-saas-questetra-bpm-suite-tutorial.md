---
title: "教學課程：Azure Active Directory 與 Questetra BPM Suite 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Questetra BPM 套件之間。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>教學課程：Azure Active Directory 與 Questetra BPM Suite 整合
本教學課程的 hello 目標是 tooshow 您如何 toointegrate Questetra BPM Suite 與 Azure Active Directory (Azure AD)。  
與 Azure AD 整合 Questetra BPM 套件可以提供下列優點 hello: 

* 您可以控制存取 tooQuestetra BPM 套件的 Azure AD 中 
* 您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooQuestetra BPM 套件 （單一登入）
* 您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件
tooconfigure Questetra BPM Suite 與 Azure AD 整合，您需要下列項目 hello:

* Azure AD 訂用帳戶
* 已啟用 [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) 單一登入的訂用帳戶

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

1. 從 hello 圖庫加入 Questetra BPM 套件 
2. 設定並測試 Azure AD 單一登入

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a>從 hello 圖庫加入 Questetra BPM 套件
tooconfigure hello 整合 Questetra BPM 套件到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Questetra BPM 套件。

**tooadd Questetra BPM 套件從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。 
   
    ![Active Directory][1]

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
    ![應用程式][2]

4. 按一下**新增**hello hello 頁底端。
   
    ![應用程式][3]

5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
    ![應用程式][4]

6. 在 [hello] 搜尋方塊中，輸入**Questetra BPM 套件**。
   
    ![應用程式][5]

7. 在 hello 結果窗格中，選取  **Questetra BPM 套件**，然後按一下**完成**tooadd hello 應用程式。

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Azure AD 單一登入與 Questetra BPM 套件根據稱為 「 許 Simon"的測試使用者。

單一登入 toowork，Azure AD 需要 tooknow Questetra BPM 套件 tooan 使用者在 Azure AD 中哪些 hello 對等項目的使用者。 換句話說，Azure AD 使用者與 hello Questetra BPM 套件中的相關的使用者之間的連結關聯性需要 toobe 建立。  
此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Questetra BPM 套件中。

tooconfigure 及 Questetra BPM Suite 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 Questetra BPM 套件的測試使用者](#creating-a-questetra-bpm-suite-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Questetra BPM 套件中的對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入
本節 hello 目標是 tooenable Azure AD 單一登入 Azure 傳統入口網站 hello 和 tooconfigure 單一登入 Questetra BPM Suite 應用程式中。

**利用 Questetra BPM Suite，Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**

1. 在 Azure 傳統入口網站，在 hello hello **Questetra BPM 套件**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入** 對話方塊。
   
    ![設定單一登入][8]

2. Hello 上**如何想您 tooQuestetra BPM 套件上的使用者 toosign**頁面上，選取**Azure AD 單一登入**，然後按一下**下一步**。
   
    ![Azure AD 單一登入][9]

3. 在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 **Questetra BPM Suite** 公司網站。

4. 在 hello 最上層顯示 hello 功能表上，按一下**系統設定**。 
   
    ![Azure AD 單一登入][10]

5. tooopen hello **SingleSignOnSAML**頁面上，按一下**SSO (SAML)**。 
   
    ![Azure AD 單一登入][11]

6. 在 Azure 傳統入口網站，在 hello hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello: 
   
    ![設定 App 設定][13]
   
    a. 在您**Questetra BPM 套件**hello 預存程序資訊 」 一節中的公司網站中，複製 hello **ACS URL**，然後將它貼入 hello**登入 URL**文字方塊。
   
    b. 在您**Questetra BPM 套件**hello 預存程序資訊 」 一節中的公司網站中，複製 hello**實體識別碼**，然後將它貼入 hello**簽發者 URL**文字方塊。
   
    c. 在您**Questetra BPM 套件**hello 預存程序資訊 」 一節中的公司網站中，複製 hello **ACS URL**，然後將它貼入 hello**回覆 URL**文字方塊。
   
    d. 按一下 [下一步] 。

7. 在 hello **Questetra BPM 套件在設定單一登入**頁面上，按一下**下載憑證**，然後儲存在本機電腦上的 hello 憑證檔案。
   
    ![設定單一登入][14]

8. 在您**Questetra BPM 套件**公司網站中，執行下列步驟的 hello: 
   
    ![設定單一登入][15]
   
    a. 選取 [啟用單一登入] 。
   
    b. 在 hello Azure 傳統入口網站中，複製 hello**簽發者 URL**值並貼到 hello**實體識別碼**文字方塊。
   
    c. 在 hello Azure 傳統入口網站中，複製 hello**單一登入服務 URL**值並貼到 hello**登入頁面 URL**文字方塊。
   
    d. 在 hello Azure 傳統入口網站中，複製 hello**單一登出服務 URL**值並貼到 hello**登出頁面 URL**文字方塊。
   
    e. 在 hello **NameID 格式**文字方塊中，輸入**urn: oasis： 名稱： tc: saml: 1.1 nameid-format-: emailAddress**。

    f. 從您下載的憑證建立 Base-64 編碼檔案。 

    >[!TIP] 
    >如需詳細資訊，請參閱[如何 tooconvert 二進位憑證到文字檔](http://youtu.be/PlgrzUZ-Y1o)。

    g. [記事本]，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後將它貼到 hello**驗證憑證**文字方塊。 

    h. 按一下 [儲存] 。

1. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**下一步**。 
   
    ![何謂 Azure AD Connect][17]

2. 在 hello**單一登入確認**頁面上，按一下**完成**。  
   
    ![何謂 Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 傳統入口網站中的測試使用者。

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![建立 Azure AD 測試使用者][100] 

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。
   
    ![建立 Azure AD 測試使用者][101] 

4. tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。 
   
    ![建立 Azure AD 測試使用者][102] 

5. 在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者][103]
   
    a. 針對 [使用者類型]，選取 [您組織中的新使用者]。
   
    b. 在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。
   
    c. 按一下 [下一步]。

6. 在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello: 
   
    ![建立 Azure AD 測試使用者][104] 
   
    a. 在 hello**名字**文字方塊中，輸入**許**。 
   
    b. 在 hello**姓氏**文字方塊中，輸入， **Simon**。
   
    c. 在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。
   
    d. 在 hello**角色**清單中，選取**使用者**。
   
    e. 按一下 [下一步] 。

7. 在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。
   
    ![建立 Azure AD 測試使用者][105]  

8. 在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者][106]   
   
    a. 請記下 hello hello 值**新密碼**。
   
    b. 按一下頁面底部的 [新增] 。   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>建立 Questetra BPM Suite 測試使用者
hello 本節目標在於 toocreate 呼叫許 Simon Questetra BPM 套件中的使用者。

**toocreate 呼叫許 Simon Questetra BPM 套件中的使用者執行下列步驟的 hello:**

1. 以系統管理員身分登入 tooyour Questetra BPM 套件公司網站。
2. 跳過**系統設定 > 使用者清單 > 新的使用者**。 
3. 在 hello 新使用者 對話方塊，執行下列步驟的 hello: 
   
    ![建立測試使用者][300] 
   
    a. 在 hello**名稱**文字方塊中，輸入 Azure AD 中的許的使用者名稱。
   
    b. 在 hello**電子郵件**文字方塊中，輸入 Azure AD 中的許的使用者名稱。
   
    c. 在 hello**密碼**文字方塊中，輸入密碼。

4. 按一下 [新增使用者] 。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者
本節 hello 目標是 tooenabling 許 Simon toouse Azure 單一登入授與他們存取 tooQuestetra BPM 套件。

![何謂 Azure AD Connect][200]

**tooassign 許 Simon tooQuestetra BPM 套件時，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，tooopen hello 應用程式 檢視，在 hello 目錄檢視中，按一下 **應用程式**hello 上方功能表中。
   
    ![何謂 Azure AD Connect][201]
2. 在 [hello] 應用程式清單中，選取**Questetra BPM 套件**。
   
    ![何謂 Azure AD Connect][205]
3. 在 hello 最上層顯示 hello 功能表上，按一下**使用者**。
   
    ![何謂 Azure AD Connect][202]
4. 在 hello 使用者清單中選取**許 Simon**。
   
    ![何謂 Azure AD Connect][203]
5. 在 hello hello 底部的工具列中按一下**指派**。
   
    ![何謂 Azure AD Connect][204]

### <a name="testing-single-sign-on"></a>測試單一登入
hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。  
當您按一下 hello Questetra BPM 套件磚 hello 存取面板中的時，您應該取得自動登入 tooyour Questetra BPM Suite 應用程式。

## <a name="additional-resources"></a>其他資源
* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 

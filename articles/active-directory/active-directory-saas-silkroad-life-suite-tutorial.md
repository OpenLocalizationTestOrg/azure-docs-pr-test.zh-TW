---
title: "教學課程：Azure Active Directory 與 SilkRoad Life Suite 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SilkRoad 生命套件之間。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a>教學課程：Azure Active Directory 與 SilkRoad Life Suite 整合
本教學課程的 hello 目標是 tooshow 您如何 toointegrate SilkRoad 生命 Suite 與 Azure Active Directory (Azure AD)。 

與 Azure AD 整合 SilkRoad 生命套件可以提供下列優點 hello: 

* 您可以控制存取 tooSilkRoad 生命套件的 Azure AD 中 
* 您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooSilkRoad 生命套件單一登入 (SSO)

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件
tooconfigure SilkRoad 生命 Suite 與 Azure AD 整合，您需要下列項目 hello:

* Azure AD 訂用帳戶
* 已啟用 SilkRoad Life Suite SSO 的訂用帳戶

>[!NOTE]
>本教學課程中的步驟 tootest hello，不建議使用實際執行環境。 
> 

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

* 除非必要，否則您不應使用生產環境，。
* 如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。 

## <a name="scenario-description"></a>案例描述
本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 的 SSO 在測試環境中。

本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 SilkRoad 生命套件 
2. 設定並測試 Azure AD SSO

## <a name="add-silkroad-life-suite-from-hello-gallery"></a>從 hello 圖庫加入 SilkRoad 生命套件
tooconfigure hello 整合 SilkRoad 生命套件到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd SilkRoad 生命套件。

**tooadd SilkRoad 生命套件從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。 
   
    ![Active Directory][1]

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
    ![應用程式][2]

4. 按一下**新增**hello hello 頁底端。
   
    ![應用程式][3]

5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
    ![應用程式][4]

6. 在 [hello] 搜尋方塊中，輸入**SilkRoad 生命套件**。
   
    ![應用程式][5]

7. 在 hello 結果窗格中，選取  **SilkRoad 生命套件**，然後按一下**完成**tooadd hello 應用程式。
   
    ![應用程式][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Azure AD SSO 與 SilkRoad 生命套件根據稱為 「 許 Simon"的測試使用者。

SSO toowork Azure AD 需要 tooknow SilkRoad 生命套件 tooan 使用者在 Azure AD 中哪些 hello 對等項目的使用者。 換句話說，Azure AD 使用者與 hello SilkRoad 生命套件中的相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** SilkRoad 生命套件中。

tooconfigure 及 SilkRoad 生命 Suite 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 SilkRoad 生命套件的測試使用者](#creating-a-silkroad-life-suite-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 SilkRoad 生命套件中的對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入
本節 hello 目標是 hello Azure 傳統入口網站中的 Azure AD 的 SSO tooenable 和 tooconfigure SSO SilkRoad 生命 Suite 應用程式中。

**利用 SilkRoad 生命 Suite，Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**

1. 以系統管理員身分登入 tooyour SilkRoad 公司網站。 

  >[!NOTE] 
  > tooobtain 存取 toohello SilkRoad 生命套件驗證應用程式中設定同盟時與 Microsoft Azure AD，請連絡 SilkRoad 支援或 SilkRoad 服務人員。
  > 

2. 跳過**服務提供者**，然後按一下**同盟的詳細資料**。 
   
    ![Azure AD 單一登入][10] 

3. 按一下**下載同盟中繼資料**，然後儲存您的電腦上的 hello 中繼資料檔案。
   
    ![Azure AD 單一登入][11] 

4. 在 Azure 傳統入口網站，在 hello hello **SilkRoad 生命套件**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入** 對話方塊。
   
    ![設定單一登入][6] 

5. Hello 上**如何想您 tooSilkRoad 生命套件上的使用者 toosign**頁面上，選取**Azure AD 單一登入**，然後按一下**下一步**。
   
    ![Azure AD 單一登入][7] 

6. 在 hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello:
   
    ![Azure AD 單一登入][8]   
 1. 在 hello**登入 URL**文字方塊中，使用者 toosign 上 tooyour SilkRoad 生命套件站台所使用的型別 hello URL (例如： *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*)。  
 2. 開啟下載的 hello **Silkroad**中繼資料檔案。 
 3. 找出 hello **AssertionConsumerService**標記，然後再複製 hello**位置**屬性。         
   
    ![Azure AD 單一登入][21] 
 4. Hello 值貼到 hello**回覆 URL**文字方塊。  
 5. 按一下 [下一步] 。

6. 在 hello **SilkRoad 生命套件在設定單一登入**頁面上，執行下列步驟的 hello:
   
    ![Azure AD 單一登入][9]  
 1. 按一下 下載憑證，然後儲存您的電腦上的 hello 檔案。  
 2. 按一下 [下一步] 。

7. 在您的 **SilkRoad** 應用程式中，按一下 [驗證來源]。
   
    ![Azure AD 單一登入][12] 

8. 按一下 [加入驗證來源] 。 
   
    ![Azure AD 單一登入][13] 

9. 在 hello**加入驗證來源**區段中，執行下列步驟的 hello: 
   
    ![Azure AD 單一登入][14]  
 1. 在下**選項 2-中繼資料檔案**，按一下 **瀏覽**tooupload hello 下載中繼資料檔案。  
 2. 按一下 [使用檔案資料建立身分識別提供者]。

10. 在 hello**驗證來源**區段中，按一下**編輯**。 
    
     ![Azure AD 單一登入][15] 

11. 在 [hello**編輯驗證來源**] 對話方塊中，執行下列步驟的 hello: 
    
     ![Azure AD 單一登入][16] 
 1. 對 [已啟用] 選取 [是]。   
 2. 在 hello **IdP 描述**文字方塊中，輸入您的組態的描述 (例如： *Azure AD 的 SSO*)。  
 3. 在 hello **IdP 名稱**文字方塊中，輸入特定 tooyour 組態的名稱 (例如： *Azure SP*)。  
 4. 按一下 [儲存] 。

12. 停用所有其他驗證來源。 
    
     ![Azure AD 單一登入][17]

13. 在 Azure 傳統入口網站，在 hello hello**單一登入確認**頁面上，按一下**下一步**。  
    
     ![Azure AD 單一登入][18]

14. 在 hello**單一登入確認**頁面上，按一下**完成**。
    
     ![Azure AD 單一登入][19]

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 傳統入口網站中的測試使用者。

![建立 Azure AD 使用者][20]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. 在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello: 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. 針對 [使用者類型]，選取 [您組織中的新使用者]。  
 2. 在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。 
 3. 按一下 [下一步] 。

6. 在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello: 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. 在 hello**名字**文字方塊中，輸入**許**。    
 2. 在 hello**姓氏**文字方塊中，輸入， **Simon**。 
 3. 在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。 
 4. 在 hello**角色**清單中，選取**使用者**。
 5. 按一下 [下一步] 。

7. 在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. 在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. 請記下 hello hello 值**新密碼**。 
 2. 按一下頁面底部的 [新增] 。   

### <a name="create-a-silkroad-life-suite-test-user"></a>建立 SilkRoad Life Suite 測試使用者
hello 本節目標在於 toocreate 呼叫許 Simon SilkRoad 生命套件中的使用者。 許的必須具有 SSO 識別碼 (有時稱為 tooas *AuthParam*) 符合許的**emailaddress**在 Azure AD 中。

**toocreate 呼叫許 Simon SilkRoad 生命套件中的使用者執行下列步驟的 hello:**

- 詢問使用者，其具有與您 SilkRoad 生命套件支援小組 toocreate **SSO 識別碼**屬性 hello 相同的值為 hello **emailaddress**許 Simon 在 Azure AD 中。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者
本節 hello 目標是 tooenable 許 Simon toouse Azure SSO 授與他們存取 tooSilkRoad 生命套件。

![指派使用者][200] 

**tooassign 許 Simon tooSilkRoad 生命套件時，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，tooopen hello 應用程式 檢視，在 hello 目錄檢視中，按一下 **應用程式**hello 上方功能表中。
   
    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**SilkRoad 生命套件**。
   
    ![指派使用者][202] 

3. 在 hello 最上層顯示 hello 功能表上，按一下**使用者**。
   
    ![指派使用者][203] 

4. 在 hello 使用者清單中選取**許 Simon**。

5. 在 hello hello 底部的工具列中按一下**指派**。
   
    ![指派使用者][205]

### <a name="test-single-sign-on"></a>測試單一登入
hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。  

當您按一下 hello SilkRoad 生命套件磚 hello 存取面板中的時，您應該取得自動登入 tooyour SilkRoad 生命 Suite 應用程式。

## <a name="additional-resources"></a>其他資源
* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png






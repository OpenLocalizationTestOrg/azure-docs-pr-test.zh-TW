---
title: "教學課程：Azure Active Directory 與 FreshDesk 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 FreshDesk 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a>教學課程：Azure Active Directory 與 FreshDesk 整合

在此教學課程中，您學會如何 toointegrate FreshDesk 與 Azure Active Directory (Azure AD)。

整合 Azure AD 與 FreshDesk 可以提供下列優點 hello:

- 您可以控制存取 tooFreshDesk Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooFreshDesk （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 FreshDesk 的整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 FreshDesk 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 FreshDesk
2. 設定並測試 Azure AD 單一登入

## <a name="adding-freshdesk-from-hello-gallery"></a>從 hello 圖庫加入 FreshDesk
tooconfigure hello 整合 FreshDesk 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd FreshDesk。

**tooadd FreshDesk 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 [hello ** [Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新增**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**FreshDesk**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. 在 [hello [結果] 窗格中，選取 [ **FreshDesk**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FreshDesk 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 FreshDesk 中是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello FreshDesk 中相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** FreshDesk 中。

tooconfigure 和測試 Azure AD 單一登入與 FreshDesk，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 FreshDesk](#creating-a-freshdesk-test-user) ** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 FreshDesk 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並設定單一登入 Freshservice 應用程式中。

**tooconfigure Azure AD 單一登入 FreshDesk 中，執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站上 hello **FreshDesk**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. 在 [hello **FreshDesk 網域和 Url**區段中，請輸入 hello**登入 URL**做為：`https://<tenant-name>.freshdesk.com`或 Freshdesk 有建議的任何其他值。

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > 請注意，這不是真正的值。 您必須使用實際的「登入 URL」來更新此值。 請連絡 [FreshDesk 用戶端支援小組](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg)以取得此值。  

4. 在 [hello **SAML 簽章憑證**區段中，按一下**憑證**，然後儲存您的電腦上的 [hello 憑證。

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. 在 [hello **FreshDesk 組態**區段中，按一下**設定 FreshDesk** tooopen 設定登入視窗。 Hello SAML 單一登入服務 URL 和登出 URL 複製 hello**快速參考**> 一節。

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Freshdesk 公司網站。

8. 在 [hello 最上層顯示 hello 功能表上，按一下**Admin**。
   
   ![管理](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "管理")

9. 在 [hello**一般設定**索引標籤上，按一下 [**安全性**。
   
   ![安全性](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "安全性")

10. 在 [hello**安全性**區段中，執行下列步驟的 hello:
   
    ![單一登入](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "單一登入")
   
    a. 針對 [單一登入 (SSO)] 選取 [啟用]。

    b.這是另一個 C# 主控台應用程式。 選取 [SAML SSO] 。

    c. 型別 hello **SAML 單一登入服務 URL**您從 Azure 入口網站複製到 hello **SAML 登入 URL**文字方塊。

    d. 型別 hello**登出 URL**您從 Azure 入口網站複製到 hello**登出 URL**文字方塊。

    e. 複製 hello**指紋**真品從 Azure 入口網站下載的 hello 值並貼到 hello**安全性憑證指紋**文字方塊。  
 
    >[!TIP]
    >如需詳細資訊，請參閱[如何 tooretrieve 憑證的指紋值](http://youtu.be/YKQF266SAxI)。 
    
    f. 按一下 [儲存] 。


### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-freshdesk-test-user"></a>建立 FreshDesk 測試使用者

在訂單 tooenable Azure AD 使用者 toolog 入 FreshDesk，它們必須佈建到 FreshDesk。  
在 FreshDesk 的 hello 案例中，佈建須手動進行。

**tooprovision 使用者帳戶，執行下列步驟 hello:**

1. 登入 tooyour **Freshdesk**租用戶。
2. 在 [hello 最上層顯示 hello 功能表上，按一下**Admin**。
   
   ![管理](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "管理")

3. 在 [hello**一般設定**索引標籤上，按一下 [**代理程式**。
   
   ![代理程式](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "代理程式")

4. 按一下 [新增代理程式] 。
   
    ![新代理程式](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "新代理程式")

5. 在 hello 代理程式資訊] 對話方塊中，執行下列步驟的 hello:
   
   ![代理程式資訊](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "代理程式資訊")
   
   a. 在 [hello**全名**文字方塊中，您想要讓 tooprovision 的 hello Azure AD 帳戶 hello 型別名稱。

   b. 在 [hello**電子郵件**文字方塊中，型別 hello Azure AD 電子郵件地址將要 hello Azure AD 帳戶 tooprovision。

   c. 在 [hello**標題**文字方塊中，您想 tooprovision 的 hello Azure AD 帳戶類型 hello 標題。

   d. 選取 [代理程式角色]，然後按一下 [指派]。
       
   e. 按一下 [儲存] 。     
   
    >[!NOTE]
    >hello Azure AD 帳戶持有者會收到電子郵件，其中包含連結 tooconfirm hello 帳戶之前，它便啟動。 
    > 
    
    >[!NOTE]
    >您可以使用任何其他 Freshdesk 使用者帳戶建立工具或 Api 提供 Freshdesk tooprovision AAD 使用者帳戶。 tooFreshDesk。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與他們存取 tooBox 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooFreshDesk，執行下列步驟的 hello:**

1. 在 [hello Azure 管理入口網站中，開啟 [hello 應用程式] 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**FreshDesk**。

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello FreshDesk 磚 hello 存取面板中的時，您應該取得登入頁面 tooget 登入 tooyour FreshDesk 的應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png


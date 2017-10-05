---
title: "教學課程：Azure Active Directory 與 Origami 整合 | Microsoft Docs"
description: "了解如何在 Azure Active Directory 與 Origami 之間設定單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3420409b72ff032e64ac59365083dd141dfc3c1b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a>教學課程：Azure Active Directory 與 Origami 整合

在本教學課程中，您會了解如何整合 Origami 與 Azure Active Directory (Azure AD)。

Origami 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 Origami 的人員
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Origami (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Origami 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Origami 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫加入 Origami
2. 設定並測試 Azure AD 單一登入

## <a name="adding-origami-from-the-gallery"></a>從資源庫加入 Origami
若要設定將 Origami 整合到 Azure AD 中，您需要從資源庫將 Origami 加入到受管理的 SaaS 應用程式清單。

**若要從資源庫加入 Origami，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **Origami**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. 在結果窗格中，選取 [Origami]，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Origami 設定及測試 Azure AD 單一登入。

若要讓單一登入運作，Azure AD 必須知道 Origami 與 Azure AD 中互相對應的使用者。 換句話說，必須要建立某位 Azure AD 使用者與 Origami 中相關使用者之間的連結關聯性。

在 Origami 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。

若要使用 Origami 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Origami 測試使用者](#creating-an-origami-test-user)** - 在 Origami 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Origami 中設定單一登入。

**若要設定與 Origami 搭配運作的 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [Origami] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. 在 [Origami 網域與 URL] 區段上，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://live.origamirisk.com/origami/account/login?account=<companyname>`

    > [!NOTE] 
    > 這不是真正的值。 請使用實際的「登入 URL」來更新此值。 請連絡 [Origami 客戶支援小組](https://wordpress.org/support/theme/origami)以取得此值。 
 
4. 在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. 在 [Origami 組態] 區段上，按一下 [設定 Origami] 以開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. 以系統管理員權限登入 Origami 帳戶。

8. 在頂端的功能表中，按一下 [系統管理員] 。
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. 在 [單一登入設定] 對話方塊頁面執行下列步驟：
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    a. 選取 [啟用單一登入] 。

    b.這是另一個 C# 主控台應用程式。 在 [識別提供者的登入頁面 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。

    c. 在 [識別提供者的登出頁面 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。

    d. 按一下 [瀏覽] 以上傳您從 Azure 入口網站下載的憑證。

    e. 按一下 [儲存變更] 。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-an-origami-test-user"></a>建立 Origami 測試使用者

在本節中，您要在 Origami 中建立名為 Britta Simon 的使用者。 

1. 以系統管理員權限登入 Origami 帳戶。

2. 在頂端的功能表中，按一下 [系統管理員] 。
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. 在 [使用者與安全性] 對話方塊中，按一下 [使用者]。
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. 按一下 [新增使用者] 。
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. 在 [新增使用者] 對話方塊上，執行下列步驟：
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    a. 在 [使用者名稱] 文字方塊中，輸入使用者的電子郵件，例如 **brittasimon@contoso.com**。

    b.這是另一個 C# 主控台應用程式。 在 [密碼] 文字方塊中輸入密碼。

    c. 在 [確認密碼] 文字方塊中再次輸入密碼。

    d. 在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。

    e. 在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。

    f. 按一下 [儲存] 。
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. 將**使用者角色**和**用戶端存取**指派給使用者。 
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會把 Origami 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派給 Origami，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Origami] 。

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您在存取面板中按一下 [Origami] 圖格時，應該會自動登入您的 Origami 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png


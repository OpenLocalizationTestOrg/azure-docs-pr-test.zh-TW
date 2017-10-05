---
title: "教學課程：Azure Active Directory 與 Lecorpio 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Lecorpio 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 35c94e2d9d8a938971f85ea732a74a7e1655545e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a>教學課程：Azure Active Directory 與 Lecorpio 整合

在本教學課程中，您會了解如何整合 Lecorpio 與 Azure Active Directory (Azure AD)。

將 Lecorpio 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 Lecorpio 的人員
- 您可以讓使用者使用其 Azure AD 帳戶自動登入 Lecorpio (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Lecorpio 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Lecorpio 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 Lecorpio
2. 設定並測試 Azure AD 單一登入

## <a name="adding-lecorpio-from-the-gallery"></a>從資源庫新增 Lecorpio
若要設定將 Lecorpio 整合到 Azure AD 中，您需要從資源庫將 Lecorpio 新增到受管理的 SaaS 應用程式清單。

**若要從資源庫新增 Lecorpio，執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **Lecorpio**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. 在結果窗格中，選取 [Lecorpio]，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以測試使用者 "Britta Simon" 的身分，設定及測試 Azure AD 與 Lecorpio 的單一登入。

若要讓單一登入運作，Azure AD 必須知道 Lecorpio 與 Azure AD 中互相對應的使用者。 換句話說，必須建立 Azure AD 使用者和 Lecorpio 中相關使用者之間的連結關聯性。

建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 Lecorpio 中**使用者名稱**的值。

若要設定及測試 Azure AD 與 Lecorpio 的單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Lecorpio 測試使用者](#creating-a-lecorpio-test-user)** - 使 Lecorpio 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Lecorpio 應用程式中設定單一登入。

**若要設定 Azure AD 與 Lecorpio 的單一登入，執行下列步驟：**

1. 在 Azure 入口網站的 [Lecorpio] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. 在 [Lecorpio 網域與 URL] 區段上，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    a. 在 [登入 URL] 文字方塊中，以下列模式輸入值：`https://<instance name>.lecorpio.com/<customer name>`

    b.這是另一個 C# 主控台應用程式。 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<instance name>.lecorpio.com/<customer name>`

    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的「登入 URL」及「識別碼」來更新這些值。 在此建議您在 [識別碼] 中使用唯一的字串值。 請連絡 [Lecorpio 客戶支援小組](mailto:info@lecorpio.com)以取得這些值。 
 
4. 在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. 若要在 **Lecorpio** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Lecorpio 支援小組](mailto:info@lecorpio.com)。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. 移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. 在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-a-lecorpio-test-user"></a>建立 Lecorpio 測試使用者

在本節中，您要在 Lecorpio 中建立名為 Britta Simon 的使用者。 

為了在 Lecorpio 應用程式中新增使用者，您必須連絡 [Lecorpio 客戶支援小組](mailto:info@lecorpio.com)。

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Lecorpio 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派到 Lecorpio，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Lecorpio]。

    ![設定單一登入](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您在存取面板中按一下 Lecorpio 圖格時，應該會自動登入 Lecorpio 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

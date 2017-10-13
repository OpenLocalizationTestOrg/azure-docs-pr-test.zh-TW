---
title: "教學課程：Azure Active Directory 與 O.C.  Tanner - AppreciateHub 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 O.C. 之間的單一登入。 Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 9af12372b30d9ee1575e46be3b4144fc3b73ec69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a>教學課程：Azure Active Directory 與 O.C.  Tanner - AppreciateHub 的人員

在本教學課程中，您會了解如何將 O.C.  Tanner - AppreciateHub 與 Azure Active Directory (Azure AD) 整合。

整合 O.C. Tanner - AppreciateHub 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 O.C. Tanner - AppreciateHub 的人員
- 您可以讓使用者使用其 Azure AD 帳戶自動登入到 O.C. Tanner - AppreciateHub (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 O.C. Tanner - AppreciateHub 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 啟用 O.C. Tanner - AppreciateHub 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從組件庫新增 O.C. Tanner - AppreciateHub
2. 設定並測試 Azure AD 單一登入

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a>從組件庫新增 O.C. Tanner - AppreciateHub
若要設定將 O.C. Tanner - AppreciateHub 整合到 Azure AD，您需要從組件庫將 O.C. Tanner - AppreciateHub 新增至受管理的 SaaS 應用程式清單。

**若要從組建庫新增 O.C.Tanner - AppreciateHub，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **O.C.Tanner - AppreciateHub**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. 在 [結果] 窗格中選取 **[O.C.Tanner - AppreciateHub]**，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會設定及測試與 O.C. 搭配運作的 Azure AD 單一登入 Tanner - AppreciateHub。

為使單一登入運作，Azure AD 必須知道 O.C. Tanner - AppreciateHub 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者和 O.C.  Tanner - AppreciateHub 中的相關使用者之間建立連結關聯性。

在 O.C.  Tanner - AppreciateHub 中，將**使用者名稱**的值指派為 Azure AD 中**使用者名稱**的值，以建立連結關聯性。

若要設定和測試 Azure AD 單一登入與 O.C. Tanner - AppreciateHub，您必須完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 O.C.Tanner - AppreciateHub 測試使用者](#creating-a-oc-tanner---appreciatehub-test-user)** - 為了在 O.C.  Tanner - AppreciateHub 中有對應 Britta Simon 的使用者，以連結到 Azure AD 中代表的使用者。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 O.C.  Tanner - AppreciateHub 應用程式。

**若要設定 Azure AD 單一登入與 O.C.Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者，請執行下列步驟：**

1. 在 Azure 入口網站上**O.C.Tanner-AppreciateHub**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. 在**O.C.Tanner-AppreciateHub 網域和 Url**區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    a. 在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`

    > [!NOTE] 
    > 這不是真實的值。 請使用實際的「回覆 URL」來更新此值。 請連絡[O.C.Tanner-AppreciateHub 支援小組](mailto:sso@octanner.com)取得此值。

    b. 使用下列連結開啟中繼資料檔案：[https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata)。
   
    c. 找出 [md:AssertionConsumerService] 節點。 
   
    d. 複製 [位置] 屬性的值。 
   
    ![設定 App 設定][12]
   
    e. 在[登入 URL] 文字方塊中，貼上您在上一個步驟中取得的值。

4. 在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. 若要設定單一登入上**O.C.Tanner-AppreciateHub**端，您需要傳送下載**中繼資料 XML**至[O.C.Tanner-AppreciateHub 支援小組](mailto:sso@octanner.com)。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a>建立 O.C. Tanner - AppreciateHub 測試使用者

本節目標是在 O.C. Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者。

**若要在 O.C.Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者，請執行下列步驟：**

請要求您[O.C.Tanner-AppreciateHub 支援小組](mailto:sso@octanner.com)建立使用者，其具有與 nameID 屬性許 Simon 的使用者名稱相同的值在 Azure AD 中。

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 O.C. Tanner - AppreciateHub 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。 Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者。

![指派使用者][200] 

**若要將 Britta Simon 指派給 O.C.Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 **O.C.Tanner - AppreciateHub**。

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。  
當您在 存取面板 按一下 O.C. Tanner - AppreciateHub 磚時，應該會自動登入您的 O.C. Tanner - AppreciateHub 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png


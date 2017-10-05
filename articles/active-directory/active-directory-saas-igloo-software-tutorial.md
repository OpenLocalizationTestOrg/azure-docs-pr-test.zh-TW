---
title: "教學課程：Azure Active Directory 與 Igloo Software 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Igloo Software 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ab3891e11eb33b4d233e4fc967a40c7df06e4f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a>教學課程：Azure Active Directory 與 Igloo Software 整合

在此教學課程中，您將了解如何整合 Igloo Software 與 Azure Active Directory (Azure AD)。

Igloo Software 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 Igloo Software 的人員。
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Igloo Software (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Igloo Software 整合，您需要以下項目：

- Azure AD 訂用帳戶
- 已啟用 Igloo Software 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 Igloo Software
2. 設定並測試 Azure AD 單一登入

## <a name="adding-igloo-software-from-the-gallery"></a>從資源庫新增 Igloo Software
若要設定將 Igloo Software 整合到 Azure AD 中，您需要從資源庫將 Igloo Software 新增到受管理的 SaaS 應用程式清單。

**若要從資源庫新增 Igloo Software，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **Igloo Software**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. 在結果窗格中，選取 [Igloo Software]，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Igloo Software 搭配運作的 Azure AD 單一登入。

單一登入若要運作，Azure AD 必須知道 Igloo Software 與 Azure AD 中互相對應的使用者。 換句話說，Azure AD 使用者和 Igloo Software 中的相關使用者之間必須建立連結關聯性。

在 Igloo Software 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。

若要設定及測試與 Igloo Software 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Igloo Software 測試使用者](#creating-an-igloo-software-test-user)** - 在 Igloo Software 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Igloo Software 應用程式中設定單一登入。

**若要使用 Igloo Software 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [Igloo Software] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. 在 [Igloo Software 網域與 URL] 區段上，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    a. 在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<company name>.igloocommmunities.com`

    b. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<company name>.igloocommmunities.com/saml.digest`

    c. 在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<company name>.igloocommmunities.com/saml.digest`

    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。 請連絡 [Igloo Software 用戶端支援小組](https://www.igloosoftware.com/services/support)以取得這些值。 

4. 在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. 在 [Igloo Software 組態] 區段上，按一下 [設定 Igloo Software] 以開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Igloo Software 公司網站。

8. 移至 [控制台] 。
   
     ![控制台](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "控制台")

9. 在 [成員資格] 索引標籤中，按一下 [登入設定]。
   
    ![登入設定](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "登入設定")

10. 在 [SAML 設定] 區段，按一下 [設定 SAML 驗證] 。
   
    ![SAML 組態](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML 組態")
   
11. 在 [一般設定]  區段，執行下列步驟：
   
    ![一般組態](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "一般組態")

    a. 在 [連接名稱]  文字方塊中，輸入組態的自訂名稱。
   
    b.這是另一個 C# 主控台應用程式。 在 [IdP 登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。
   
    c. 在 [IdP 登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。
    
    d. 選取 [登出回應與要求 HTTP 類型] 作為 [POST]。
   
    e. 在從 Azure 入口網站下載的記事本檔案中開啟您的 **base-64** 編碼憑證，將憑證的內容複製到剪貼簿，再貼到 [公開憑證] 文字方塊。
    
12. 在 [回應與驗證設定] ，執行以下步驟：
    
    ![回應和驗證設定](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "回應和驗證設定")
  
      a. 在 [識別提供者]，選取 [Microsoft ADFS]。
      
      b.這是另一個 C# 主控台應用程式。 在 [識別元類型]，選取 [電子郵件地址]。 

      c. 在 [電子郵件屬性] 文字方塊中，輸入**電子郵件地址**。

      d. 在 [名字屬性] 文字方塊中，輸入**名字**。

      e. 在 [姓氏屬性] 文字方塊中，輸入**姓氏**。

13. 執行以下步驟來完成設定：
    
    ![登入時建立使用者](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "登入時建立使用者") 

     a. 在 [登入時建立使用者]，選取 [使用者登入您的網站時建立新的使用者]。

     b.這是另一個 C# 主控台應用程式。 在 [登入設定]，選取 [在「登入」畫面使用 SAML 按鈕]。

     c. 按一下 [儲存] 。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-an-igloo-software-test-user"></a>建立 Igloo Software 測試使用者

沒有動作項目可讓您設定  Igloo Software 使用者佈建。  

當已指派的使用者透過存取面板嘗試登入 Igloo Software 時，Igloo Software 會檢查使用者是否存在。  如果尚無可用的使用者帳戶，Igloo Software 會自動予以建立。

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Igloo Software 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要指派 Britta Simon 到 Igloo Software，請執行以下步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Igloo Software]。

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您在 [存取面板] 中按一下 [Igloo Software] 圖格時，您應該會自動登入您的 Igloo Software 應用程式。
如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png


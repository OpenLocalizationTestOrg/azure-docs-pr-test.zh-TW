---
title: "教學課程：Azure Active Directory 與 Atlassian Cloud 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Atlassian Cloud 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 2891838b56dd15cb5f97dcae391770143a80c781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a>教學課程：Azure Active Directory 與 Atlassian Cloud 整合

在本教學課程中，您會了解如何整合 Atlassian Cloud 與 Azure Active Directory (Azure AD)。

Atlassian Cloud 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 Atlassian Cloud 的人員
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Atlassian Cloud (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Atlassian Cloud 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Atlassian Cloud 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 Atlassian Cloud
2. 設定並測試 Azure AD 單一登入

## <a name="adding-atlassian-cloud-from-the-gallery"></a>從資源庫新增 Atlassian Cloud
若要設定將 Atlassian Cloud 整合到 Azure AD 中，您需要從資源庫將 Atlassian Cloud 新增到受管理的 SaaS 應用程式清單。

**若要從資源庫新增 Atlassian Cloud，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **Atlassian Cloud**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. 在結果面板中，選取 [Atlassian Cloud]，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Atlassian Cloud 搭配運作的 Azure AD 單一登入。

若要讓單一登入能夠運作，Azure AD 必須知道 Atlassian Cloud 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者與 Atlassian Cloud 中的相關使用者之間建立連結關聯性。

建立此連結關聯性的方法是將 Azure AD 中**使用者名稱**的值指定為 Atlassian Cloud 中 **Username** 的值。

若要設定及測試與 Atlassian Cloud 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Atlassian Cloud 測試使用者](#creating-an-atlassian-cloud-test-user)** - 在 Atlassian Cloud 中建立一個與 Azure AD 中代表使用者的項目連結的 Britta Simon 對應項目。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Atlassian Cloud 應用程式中設定單一登入。

**若要使用 Atlassian Cloud 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [Atlassian Cloud] 應用程式整合分頁上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. 如果您想要以 **IDP** 起始模式設定應用程式，請在 [Atlassian Cloud 網域和 URL] 區段上執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    a. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<instancename>.atlassian.net/admin/saml/edit`

    b.這是另一個 C# 主控台應用程式。 在 [回覆 URL] 文字方塊中，輸入 URL 為：`https://id.atlassian.com/login/saml/acs`

4. 如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]，然後執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<instancename>.atlassian.net`

    > [!NOTE] 
    > 這些都不是真正的值。 請使用實際的識別碼和登入 URL 將這些值更新。 您可以從 [Atlassian Cloud SAML 設定] 畫面取得確切值。
 
5. 在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. 在 [Atlassian Cloud 設定] 區段中，按一下 [設定 Atlassian Cloud] 以開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 [SAML 實體 ID 和 SAML 單一登入服務 URL]。

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. 若要取得針對您的應用程式設定的 SSO，請使用系統管理員權限登入 Atlassian 入口網站。

8. 在左側導覽列的 [驗證] 區段中按一下 [網域]。

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    a. 在文字方塊中，輸入您的網域名稱，然後按一下 [新增網域]。
        
    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    b.這是另一個 C# 主控台應用程式。 若要驗證網域，請按一下 [驗證]。 

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    c. 下載網域驗證 html 檔案，將它上傳至您的網域網站的根資料夾，然後按一下 [驗證網域]。
    
    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    d. 驗證網域後，[狀態] 欄位的值會是 [已驗證]。

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. 在左側瀏覽列中，按一下 [SAML]。
 
    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. 建立 SAML 設定並新增識別提供者設定。

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    a. 在 [識別提供者實體識別碼] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。

    b.這是另一個 C# 主控台應用程式。 在 [識別提供者 SSO URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。

    c. 開啟從 Azure 入口網站下載的憑證，複製不含開始和結束行的值，並將它貼在 [公用 X509 憑證] 方塊中。
    
    d. 按一下 [儲存設定] 以儲存設定。
     
11. 更新 Azure AD 設定，確定您已設定正確的識別項 URL。
  
    a. 從 [SAML] 畫面複製 [SP身分識別碼]，然後將它貼在 Azure AD 中作為 [識別碼] 值。

    b.這是另一個 C# 主控台應用程式。 [登入 URL] 是 Atlassian Cloud 的租用戶 URL。   

     ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. 在 Azure 入口網站中，按一下 [儲存] 按鈕。

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-an-atlassian-cloud-test-user"></a>建立 Atlassian Cloud 測試使用者

若要讓 Azure AD 使用者能夠登入 Atlassian Cloud，必須將他們佈建到 Atlassian Cloud。  
Atlassian Cloud 需以手動方式佈建。

**若要佈建使用者帳戶，請執行下列步驟：**

1. 在 [網站管理] 區段中，按一下 [使用者] 按鈕。

    ![建立 Atlassian Cloud 使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. 按一下 [建立使用者] 按鈕，以在 Atlassian Cloud 中建立使用者。

    ![建立 Atlassian Cloud 使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. 輸入使用者的 [電子郵件地址]、[使用者名稱] 和 [完整名稱]，然後指派應用程式存取權。 

    ![建立 Atlassian Cloud 使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. 按一下 [建立使用者] 按鈕，便會傳送電子郵件邀請給使用者，而使用者在接受邀請之後便可在系統中作業。 

>[!NOTE] 
>您也可以按一下 [使用者] 區段中的 [大量建立] 按鈕，建立大量使用者。

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Atlassian Cloud 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派給 Atlassian Cloud，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Atlassian Cloud]。

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD SSO 組態。

在存取面板中按一下 [Atlassian Cloud] 圖格時，您應該會自動登入您的 Atlassian Cloud 應用程式。 如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png


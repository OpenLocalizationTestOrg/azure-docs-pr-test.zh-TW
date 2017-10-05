---
title: "教學課程：Azure Active Directory 與 TalentLMS 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 TalentLMS 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: f28d6fbfad9dae578a20db7218b7e3b174ed859c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a>教學課程：Azure Active Directory 與 TalentLMS 整合

在本教學課程中，您將了解如何整合 TalentLMS 與 Azure Active Directory (Azure AD)。

TalentLMS 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 TalentLMS 的人員
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 TalentLMS (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

如要設定 Azure AD 與 TalentLMS 的整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 TalentLMS 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 TalentLMS
2. 設定並測試 Azure AD 單一登入

## <a name="adding-talentlms-from-the-gallery"></a>從資源庫新增 TalentLMS
若要設定將 TalentLMS 整合到 Azure AD 中，您需要從資源庫將 TalentLMS 新增到受管理的 SaaS app 清單。

**若要從資源庫新增 TalentLMS，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **TalentLMS**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. 在結果窗格中，選取 [TalentLMS]，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 TalentLMS 搭配運作的 Azure AD 單一登入。

若要讓單一登入能夠運作，Azure AD 必須知道 TalentLMS 與 Azure AD 中互相對應的使用者。 換句話說，必須建立 Azure AD 使用者和 TalentLMS 中相關使用者之間的連結關聯性。

在 TalentLMS 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。

若要設定及測試與 TalentLMS 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 TalentLMS 測試使用者](#creating-a-talentlms-test-user)** - 使 TalentLMS 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 TalentLMS 應用程式中設定單一登入。

**若要使用 TalentLMS 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [TalentLMS] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. 在 [TalentLMS 網域與 URL] 區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    a. 在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenant-name>.TalentLMSapp.com`

    b. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`http://<tenant-name>.talentlms.com`

    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的「登入 URL」及「識別碼」來更新這些值。 請連絡 [TalentLMS 客戶支援小組](https://www.talentlms.com/contact)以取得這些值。 
 
4. 在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. 在 [TalentLMS 組態] 區段上，按一下 [設定 TalentLMS] 以開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 TalentLMS 公司網站。

8. 在 [帳戶和設定] 區段中，按一下 [使用者] 索引標籤。
   
    ![帳戶和設定](./media/active-directory-saas-talentlms-tutorial/IC777296.png "帳戶和設定")

9. 按一下 [單一登入 (SSO)] 。

10. 在 [單一登入] 區段中，執行下列步驟：
   
    ![單一登入](./media/active-directory-saas-talentlms-tutorial/IC777297.png "單一登入")   

    a. 從 [SSO 整合類型] 清單中，選取 [SAML 2.0]。

    b.這是另一個 C# 主控台應用程式。 在 [識別提供者]\(IdP\) 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。
 
    c. 將 Azure 入口網站的 [指紋] 值貼至 [憑證指紋] 文字方塊。    

    d.  在 [遠端登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的**「SAML 單一登入服務 URL」**值。
 
    e. 在 [遠端登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。

    f. 填寫下列各項： 

    * 在 [TargetedID] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`
     
    * 在 [名字] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`
    
    * 在 [姓氏] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`
    
    * 在 [電子郵件] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`
    
11. 按一下 [儲存] 。
 
> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-a-talentlms-test-user"></a>建立 TalentLMS 測試使用者

若要讓 Azure AD 使用者可以登入 TalentLMS，則必須將他們佈建到 TalentLMS。 TalentLMS 需以手動的方式佈建。

**若要佈建使用者帳戶，請執行下列步驟：**

1. 登入您的 **TalentLMS** 租用戶。

2. 按一下 [使用者]，然後按一下 [加入使用者]。

3. 在 [加入使用者]  對話頁面上，執行下列步驟：
   
    ![新增使用者](./media/active-directory-saas-talentlms-tutorial/IC777299.png "新增使用者")  

    a. 在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。

    b.這是另一個 C# 主控台應用程式。 在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。
 
    c. 在 [電子郵件地址] 文字方塊中，輸入使用者的電子郵件，例如 **brittasimon@contoso.com**。

    d. 按一下 [加入使用者] 。

>[!NOTE]
>您可以使用任何其他的 TalentLMS 使用者帳戶建立工具或 TalentLMS 提供的 API 來佈建 AAD 使用者帳戶。
 

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 TalentLMS 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派給 TalentLMS，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [TalentLMS]。

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。

當您在存取面板中按一下 [TalentLMS] 圖格時，應該會自動登入您的 TalentLMS 應用程式

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

---
title: "教學課程：Azure Active Directory 與 Coupa 整合 | Microsoft Docs"
description: "了解如何設定單一登入 Azure Active Directory 與 Coupa 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2017
ms.author: jeedes
ms.openlocfilehash: 30149f181d8b0ebdc1ae6820da5d561f3a942fa3
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/12/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>教學課程：Azure Active Directory 與 Coupa 整合

在本教學課程中，您可以了解如何與 Azure Active Directory (Azure AD) 整合 Coupa。

使用 Azure AD 整合 Coupa 可以提供下列優點：

- 您可以控制可以存取 Coupa 的 Azure AD 中。
- 您可以讓您自動取得登入 Coupa （單一登入） 具有其 Azure AD 帳戶的使用者。
- 您可以在 Azure 入口網站中集中管理您的帳戶。

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 整合與 Coupa，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Coupa 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二項主要的基本工作組成：

1. 從資源庫加入 Coupa
2. 設定並測試 Azure AD 單一登入

## <a name="adding-coupa-from-the-gallery"></a>從資源庫加入 Coupa
若要設定 Coupa 整合 Azure AD，您需要加入 Coupa 從資源庫，您的受管理的 SaaS 應用程式清單。

**若要從資源庫加入 Coupa，執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Azure Active Directory 按鈕][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![企業應用程式刀鋒視窗][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![新增應用程式按鈕][3]

4. 在 搜尋 方塊中，輸入**Coupa**，選取**Coupa**然後按一下 從結果面板**新增**按鈕以加入應用程式。

    ![在 [結果] 清單中的 Coupa](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您可以設定及測試 Azure AD 單一登入 Coupa 根據稱為 「 許 Simon"的測試使用者。

單一登入工作，如 Azure AD 需要知道在 Coupa 中對等項目的使用者是使用者在 Azure AD 中。 換句話說，必須建立 Azure AD 使用者和相關的使用者在 Coupa 之間的連結關聯性。

在 Coupa 中，將指派的值**使用者名稱**做為值的 Azure AD 中**Username**建立的連結關聯性。

若要設定和測試 Azure AD 單一登入與 Coupa，您需要完成下列的建置組塊：

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立測試使用者 Coupa](#create-a-coupa-test-user)**  -若要在連結至使用者的 Azure AD 表示的 Coupa 許 Simon 對應項目。
4. **[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 Azure 入口網站中，並設定單一登入 Coupa 應用程式中。

**若要設定 Azure AD 單一登入與 Coupa，執行下列步驟：**

1. 在 Azure 入口網站上**Coupa**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入連結][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_samlbase.png)

3. 在**Coupa 網域和 Url**區段中，執行下列步驟：

    ![Coupa 網域和 Url 的單一登入資訊](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_url.png)

    a. 在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`http://<companyname>.Coupa.com`

    b. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`<companyname>.coupahost.com`

    c. 在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<companyname>.coupahost.com/sp/ACS.saml2`

    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的「單一登入 URL」、「識別碼」及「回覆 URL」來更新這些值。 請連絡[Coupa 用戶端支援小組](https://success.coupa.com/Support/Contact_Us?)取得這些值。 您會取得回覆 URL 值從中繼資料，在本教學課程稍後會說明。

4. 在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。

    ![憑證下載連結](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-coupa-tutorial/tutorial_general_400.png)

6. 以系統管理員身分登入您的 Coupa 公司網站。

7. 移至 [設定] \> [安全性控制]。
   
   ![安全性控制項](./media/active-directory-saas-coupa-tutorial/ic791900.png "安全性控制項")

8. 在 [使用 Coupa 認證登入]  區段中，執行下列步驟：

    ![Coupa 預存程序中繼資料](./media/active-directory-saas-coupa-tutorial/ic791901.png "Coupa 預存程序中繼資料")
    
    a. 選取 [使用 SAML 登入] 。
    
    b. 若要將 Coupa 中繼資料檔案下載至您的電腦，按一下 [下載和匯入預存程序的中繼資料] 。 開啟 [中繼資料和複本**AssertionConsumerService index/URL**值，請將該值貼入**回覆 URL** ] 文字方塊中的**Coupa 網域和 Url** > 一節。 
    
    c. 按一下**瀏覽**上傳從 Azure 入口網站下載的中繼資料。
    
    d. 按一下 [檔案] 。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。

    ![Azure Active Directory 按鈕](./media/active-directory-saas-coupa-tutorial/create_aaduser_01.png)

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-coupa-tutorial/create_aaduser_02.png)

3. 若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。

    ![[新增] 按鈕](./media/active-directory-saas-coupa-tutorial/create_aaduser_03.png)

4. 在 [使用者] 對話方塊中，執行下列步驟：

    ![[使用者] 對話方塊](./media/active-directory-saas-coupa-tutorial/create_aaduser_04.png)

    a. 在 [名稱] 方塊中，輸入 **BrittaSimon**。

    b. 在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。

    c. 選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。

    d. 按一下頁面底部的 [新增] 。
 
### <a name="create-a-coupa-test-user"></a>建立 Coupa 測試使用者

若要讓 Azure AD 使用者可以登入 Coupa，則必須將他們佈建到 Coupa。  

* Coupa 需以手動的方式佈建。

**若要設定使用者佈建，請執行下列步驟：**

1. 以系統管理員身分登入您的 **Coupa** 公司網站。

2. 在頂端的功能表中，按一下 [設定]，然後按一下 [使用者]。
   
   ![使用者](./media/active-directory-saas-coupa-tutorial/ic791908.png "使用者")

3. 按一下頁面底部的 [新增] 。
   
   ![建立使用者](./media/active-directory-saas-coupa-tutorial/ic791909.png "建立使用者")

4. 在 [使用者建立]  區段中，執行下列步驟：
   
   ![使用者詳細資料](./media/active-directory-saas-coupa-tutorial/ic791910.png "使用者詳細資料")
   
   a. 在相關的文字方塊中，輸入您要佈建之有效 Azure Active Directory 帳戶的 [登入]、[名字]、[姓氏]、[單一登入識別碼]、[電子郵件] 屬性。

   b. 按一下頁面底部的 [新增] 。   
   
   >[!NOTE]
   >Azure Active Directory 帳戶的持有者會收到一封包含連結的電子郵件，以在啟用帳戶前進行確認。 
   > 

>[!NOTE]
>您可以使用任何其他的 Coupa 使用者帳戶建立工具或 Coupa 提供的 API 來佈建 AAD 使用者帳戶。 

### <a name="assign-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，以啟用要使用 Azure 單一登入授與存取權給 Coupa 許 Simon。

![指派使用者角色][200] 

**若要指派給 Coupa 的許 Simon，執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取**Coupa**。

    ![應用程式清單中的 [Coupa] 連結](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_app.png)  

3. 在左側功能表中，按一下 [使用者和群組]。

    ![[使用者和群組] 連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![[新增指派] 窗格][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您按一下 Coupa 磚，在存取面板時，您應該取得自動登入 Coupa 應用程式。
如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_203.png


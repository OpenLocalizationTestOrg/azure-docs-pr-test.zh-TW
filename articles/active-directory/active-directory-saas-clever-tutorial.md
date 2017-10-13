---
title: "教學課程：Azure Active Directory 與 Clever 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Clever 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 84082ff567e37d7fff80be9e089c67cfab911861
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a>教學課程：Azure Active Directory 與 Clever 整合

在本教學課程中，您會了解如何將 Clever 與 Azure Active Directory (Azure AD) 進行整合。

Clever 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 Clever 的人員。
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Clever (單一登入)。
- 您可以在 Azure 入口網站中集中管理您的帳戶。

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Clever 整合，您需要下列項目：

- Azure AD 訂用帳戶
- Clever 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 Clever
2. 設定並測試 Azure AD 單一登入

## <a name="adding-clever-from-the-gallery"></a>從資源庫新增 Clever
若要設定將 Clever 整合到 Azure AD 中，您需要從資源庫將 Clever 新增到受管理的 SaaS 應用程式清單中。

**若要從資源庫新增 Clever，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Azure Active Directory 按鈕][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![企業應用程式刀鋒視窗][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![新增應用程式按鈕][3]

4. 在搜尋方塊中，輸入 **Clever**，從結果面板中選取 [Clever]，然後按一下 [新增] 按鈕以新增應用程式。

    ![結果清單中的 Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Clever 搭配運作的 Azure AD 單一登入。

若要讓單一登入運作，Azure AD 必須知道 Clever 與 Azure AD 中互相對應的使用者。 換句話說，必須建立 Azure AD 使用者和 Clever 中相關使用者之間的連結關聯性。

在 Clever 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。

若要設定及測試與 Clever 搭配運作的 Azure AD 單一登入，您需要完成下列建構元素：

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Clever 測試使用者](#create-a-clever-test-user)** - 使 Clever 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。
4. **[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會於 Azure 入口網站啟用 Azure AD 單一登入，然後在您的 Clever 應用程式中設定單一登入。

**若要設定與 Clever 搭配運作的 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [Clever] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入連結][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. 在 [Clever 網域及 URL] 區段上，執行下列步驟：

    ![Clever 網域及 URL 單一登入資訊](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    a. 在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://clever.com/in/<companyname>`

    b. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://clever.com/<companyname>`

    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的「登入 URL」及「識別碼」來更新這些值。 請連絡 [Clever 用戶端支援小組](https://clever.com/about/contact/)以取得這些值。

4. 在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。

    ![憑證下載連結](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. Clever 應用程式需要特定格式的 SAML 判斷提示，因此您必須將自訂屬性對應加入 **SAML Token 屬性**組態。

    以下螢幕擷取畫面顯示上述的範例。

    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. 在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如上圖所示設定 SAML 權杖屬性，然後執行下列步驟：
    
    | 屬性名稱  | 屬性值 |
    | --------------- | -------------------- |    
    | clever.student.credentials.district\_username  | user.userprincipalname |
    | Firstname  | user.givenname |
    | lastname  | user.surname |    

    a. 按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。

    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    b. 在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。

    c. 在 [值] 清單中，選取該列所顯示的值。

    d. [命名空間] 文字方塊保持空白。
    
    d. 按一下 [確定] 。     

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. 若要產生**中繼資料** URL，執行下列步驟︰

    a. 按一下 [應用程式註冊]。
    
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    b.這是另一個 C# 主控台應用程式。 按一下 [端點] 以開啟 [端點] 對話方塊。  
    
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    c. 按一下複製按鈕複製 [同盟中繼資料文件] URL，並將它貼到 [記事本]。
    
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    d. 現在，移至 [Clever] 的屬性頁面，使用 [複製] 按鈕複製 [應用程式識別碼]，並將它貼到記事本。
 
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    e. 使用下列模式產生**中繼資料 URL**︰`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`   

9. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Clever 公司網站。

10. 在工具列中，按一下 [立即登入] 。

    ![立即登入](./media/active-directory-saas-clever-tutorial/ic798984.png "立即登入")

11. 在 [立即登入]  頁面上，執行下列步驟：
      
      ![立即登入](./media/active-directory-saas-clever-tutorial/ic798985.png "立即登入")
      
      a. 輸入 [登入 URL] 。
      
      >[!NOTE]
      >[登入 URL] 是自訂值。 請連絡 [Clever 用戶端支援小組](https://clever.com/about/contact/)以取得此值。
      
      b. 針對 [識別系統]，選取 [ADFS]。

      c. 在 [中繼資料 URL]文字方塊中輸入**中繼資料 URL**。
      
      d. 按一下 [儲存] 。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。

    ![Azure Active Directory 按鈕](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. 若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。

    ![[新增] 按鈕](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. 在 [使用者] 對話方塊中，執行下列步驟：

    ![[使用者] 對話方塊](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    a. 在 [名稱] 方塊中，輸入 **BrittaSimon**。

    b. 在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。

    c. 選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。

    d. 按一下 [建立] 。
 
### <a name="create-a-clever-test-user"></a>建立 Clever 測試使用者

若要讓 Azure AD 使用者可以登入 Clever，必須將他們佈建到 Clever。

對於 Clever，配合 [Clever Client 支援小組](https://clever.com/about/contact/)，在 Clever 平台中新增使用者。 您必須先建立和啟動使用者，然後才能使用單一登入。 

>[!NOTE]
>您可以使用任何其他的 Clever 使用者帳戶建立工具，或是使用 Clever 提供的 API 來佈建 Azure AD 使用者帳戶。

### <a name="assign-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Clever 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者角色][200] 

**若要將 Britta Simon 指派給 Clever，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Clever]。

    ![應用程式清單中的 Clever 連結](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. 在左側功能表中，按一下 [使用者和群組]。

    ![[使用者和群組] 連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![[新增指派] 窗格][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您在「存取面板」中按一下 Clever 圖格時，應該會自動登入您的 Clever 應用程式。
如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png


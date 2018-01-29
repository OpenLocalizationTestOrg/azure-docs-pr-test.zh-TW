---
title: "教學課程：Azure Active Directory 與 Pluralsight 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Pluralsight 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/18/2017
ms.author: jeedes
ms.openlocfilehash: 62d148d78d9f98b6a3ddf1259177936b3976aeab
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a>教學課程：Azure Active Directory 與 Pluralsight 整合

在本教學課程中，您會了解如何整合 Pluralsight 與 Azure Active Directory (Azure AD)。

Pluralsight 與 Azure AD 整合提供下列優點：

- 您可以控制可以存取 Pluralsight 的 Azure AD 中。
- 您可以啟用自動取得登入 (Single Sign-on) Pluralsight 其 Azure AD 帳戶的使用者。
- 您可以在 Azure 入口網站中集中管理您的帳戶。

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定與 Pluralsight 的 Azure AD 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Pluralsight 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二項主要的基本工作組成：

1. 從資源庫新增 Pluralsight
2. 設定並測試 Azure AD 單一登入

## <a name="adding-pluralsight-from-the-gallery"></a>從資源庫新增 Pluralsight
若要設定 Pluralsight 與 Azure AD 整合，您需要從資源庫將 Pluralsight 加入到受控 SaaS 應用程式清單。

**若要從資源庫加入 Pluralsight，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Azure Active Directory 按鈕][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![企業應用程式刀鋒視窗][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![新增應用程式按鈕][3]

4. 在 搜尋 方塊中，輸入**Pluralsight**，選取**Pluralsight**然後按一下 從結果面板**新增**按鈕以加入應用程式。

    ![在 [結果] 清單中的 Pluralsight](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Pluralsight 設定及測試 Azure AD 單一登入。

若要讓單一登入運作，Azure AD 必須知道 Pluralsight 與 Azure AD 中互相對應的使用者。 換句話說，必須建立 Azure AD 使用者和 Pluralsight 中相關使用者之間的連結關聯性。

在 Pluralsight 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。

若要設定及測試對 Pluralsight 的 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立測試使用者 Pluralsight](#create-a-pluralsight-test-user)**  -若要在連結至使用者的 Azure AD 表示 Pluralsight 許 Simon 對應項目。
4. **[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Pluralsight 應用程式中設定單一登入。

**若要設定與 Pluralsight 搭配運作的 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [Pluralsight] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入連結][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. 在**Pluralsight 網域和 Url**區段中，執行下列步驟：

    ![Pluralsight 網域和 Url 的單一登入資訊](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    a. 在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<instancename>.pluralsight.com/sso/<companyname>`

    b. 在 [識別碼] 文字方塊中，輸入 URL：`www.pluralsight.com`

    c. 在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<instancename>.pluralsight.com/sp/ACS.saml2`
     
    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的回覆 URL 與登入 URL 更新這些值。 請連絡[Pluralsight 用戶端支援小組](mailto:support@pluralsight.com)取得這些值。 

4. 在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。

    ![憑證下載連結](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. 本節的目標是要在 Azure 入口網站中啟用 Azure AD 單一登入，並在 Pluralsight 應用程式中設定 SSO。

    Pluralsight 應用程式需要特定格式的 SAML 判斷提示，需要您加入自訂屬性對應到您的 SAML token 屬性設定。 以下螢幕擷取畫面顯示上述的範例。

    ![設定單一登入](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    >您也可以利用適當的值新增 **"Unique ID"** 屬性，例如 EmployeeID 和其他適合貴組織的值。 另請注意，這不是必要的屬性，但您可以新增它以識別唯一的使用者。 

6. 若要加入必要的 [SAML Token 屬性] ，請對下表顯示的每一列執行下列步驟：
   
   | 屬性名稱 | 屬性值 |
   | ---| --- |
   | 名字 |user.givenname |
   | 姓氏 |user.surname |
   | 電子郵件 |user.mail |
   
   a. 按一下 [加入使用者屬性] 來開啟 [加入使用者屬性] 對話方塊。
    
     ![設定單一登入](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   b. 在 [屬性名稱]  文字方塊中，輸入該資料列所顯示的屬性名稱。
  
   c. 在 [屬性值]  清單中，選取該資料列所顯示的屬性名稱。
  
   d. 按一下 [確定] 。    

7. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. 若要為您的應用程式設定 SSO，請連絡 [Pluralsight 專業服務](mailTo:professionalservices@pluralsight.com) 小組，並提供下載的中繼資料檔案。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。

    ![Azure Active Directory 按鈕](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png)

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png)

3. 若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。

    ![[新增] 按鈕](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png)

4. 在 [使用者] 對話方塊中，執行下列步驟：

    ![[使用者] 對話方塊](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png)

    a. 在 [名稱] 方塊中，輸入 **BrittaSimon**。

    b. 在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。

    c. 選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。

    d. 按一下頁面底部的 [新增] 。
 
### <a name="create-a-pluralsight-test-user"></a>建立 Pluralsight 測試使用者

本節目標是在 Pluralsight 中建立名為 Britta Simon 的使用者。 請與 [Pluralsight 客戶支援小組](mailto:support@pluralsight.com)合作，在 Pluralsight 帳戶中新增使用者。

### <a name="assign-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Pluralsight 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者角色][200] 

**若要將 Britta Simon 指派到 Pluralsight，請執行以下步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Pluralsight] 。

    ![應用程式清單中的 [Pluralsight] 連結](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png)  

3. 在左側功能表中，按一下 [使用者和群組]。

    ![[使用者和群組] 連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![[新增指派] 窗格][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您在存取面板中按一下 Pluralsight 圖格時，應該會自動登入您的 Pluralsight 應用程式。
如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png


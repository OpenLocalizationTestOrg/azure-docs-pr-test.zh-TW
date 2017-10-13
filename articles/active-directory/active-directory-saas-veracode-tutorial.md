---
title: "教學課程：Azure Active Directory 與 Veracode 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Veracode 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d49349c5ae08e67d91e30967f3644623211823ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a>教學課程：Azure Active Directory 與 Veracode 整合

在本教學課程中，您會了解如何整合 Veracode 與 Azure Active Directory (Azure AD)。

Veracode 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中管控可存取 Veracode 的人員。
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Veracode (單一登入)。
- 您可以在 Azure 入口網站中集中管理您的帳戶。

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Veracode 的整合作業，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Veracode 單一登入功能的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 Veracode
2. 設定和測試 Azure AD 單一登入

## <a name="add-veracode-from-the-gallery"></a>從資源庫新增 Veracode
若要設定將 Veracode 整合到 Azure AD 中，您需要從資源庫將 Veracode 新增到受管理的 SaaS 應用程式清單。

**若要從資源庫新增 Veracode，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Azure Active Directory 按鈕][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![企業應用程式刀鋒視窗][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![新增應用程式按鈕][3]

4. 在搜尋方塊中，輸入 **Veracode**，從結果面板中選取 **Veracode**，然後按一下 [新增] 按鈕以新增應用程式。

    ![結果清單中的 Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Veracode 設定及測試 Azure AD 單一登入。

若要讓單一登入運作，Azure AD 必須知道 Veracode 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者和 Veracode 中的相關使用者之間建立連結關聯性。

在 Veracode 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。

若要使用 Veracode 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Veracode 測試使用者](#create-a-veracode-test-user)** - 讓 Veracode 中對應的 Britta Simon 連結到使用者在 Azure AD 中的代表項目。
4. **[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Veracode 應用程式中設定單一登入。

**若要使用 Veracode 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [Veracode] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入連結][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. 在 [Veracode 網域和 URL] 區段中，使用者不需要執行任何步驟，因為應用程式已預先與 Azure 整合。 

    ![設定單一登入](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. 在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。

    ![憑證下載連結](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. 本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己的 Azure AD 帳戶驗證到 Veracode。

    Veracode 應用程式需要特定格式的 SAML 判斷提示，要求您加入自訂屬性對應到您的 **SAML 權杖屬性** 組態。 以下螢幕擷取畫面顯示上述的範例。
    
    ![屬性](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "屬性")

6. 若要加入必要的屬性對應，請執行下列步驟：

    | 屬性名稱 | 屬性值 |
    |--- |--- |
    | firstname |User.givenname |
    | lastname |User.surname |
    | 電子郵件 |User.mail |
    
    a. 針對上表中的每個資料列，按一下 [新增使用者屬性] 。
    
    ![屬性](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "屬性")
    
    ![屬性](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "屬性")
    
    b. 在 [屬性名稱]  文字方塊中，輸入該資料列所顯示的屬性名稱。
    
    c. 在 [屬性值]  文字方塊中，選取該資料列所顯示的屬性值。
    
    d. 按一下 [確定] 。

7. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. 在 [Veracode 組態] 區段上，按一下 [設定 Veracode] 以開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 [SAML 實體識別碼]。

    ![Veracode 組態](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Veracode 公司網站。

10. 在頂端功能表中，按一下 [設定]，然後按一下 [管理員]。
   
    ![管理](./media/active-directory-saas-veracode-tutorial/ic802911.png "管理")

11. 按一下 [SAML]  索引標籤。

12. 在 [組織 SAML 設定]  區段中，執行下列步驟：
   
    ![管理](./media/active-directory-saas-veracode-tutorial/ic802912.png "管理")
   
    a.  在 [簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。
    
    b. 若要上傳從 Azure 入口網站下載的憑證，請按一下 [選擇檔案]。
   
    c. 選取 [啟用自動註冊] 。

13. 在 [自動註冊設定] 區段上，執行下列步驟，然後按一下 [儲存]：
   
    ![管理](./media/active-directory-saas-veracode-tutorial/ic802913.png "管理")
   
    a. 在 [啟用新的使用者] 選取 [不需要啟用]。
   
    b.這是另一個 C# 主控台應用程式。 在 [使用者資料更新] 選取 [Veracode 使用者資料喜好設定]。
   
    c. 針對 [SAML 屬性詳細資料] ，請選取下列選項：
      * **[使用者角色]**
      * **[原則系統管理員]**
      * **[檢閱者]**
      * **[安全性負責人]**
      * **[行政人員]**
      * **[傳送者]**
      * **[建立者]**
      * **[所有掃描類型]**
      * **[小組成員資格]**
      * **[預設小組]**

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。

    ![Azure Active Directory 按鈕](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. 若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。

    ![[新增] 按鈕](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. 在 [使用者] 對話方塊中，執行下列步驟：

    ![[使用者] 對話方塊](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    a. 在 [名稱] 方塊中，輸入 **BrittaSimon**。

    b. 在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。

    c. 選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。

    d. 按一下 [建立] 。
 
### <a name="create-a-veracode-test-user"></a>建立 Veracode 測試使用者
若要讓 Azure AD 使用者可以登入 Veracode，則必須將他們佈建到 Veracode。 若是 Veracode 的情況 來佈建是自動化的工作。 沒有您適用的動作項目。 第一次嘗試單一登入時，會視需要自動建立使用者。

> [!NOTE]
> 您可以使用任何其他的 Veracode 使用者帳戶建立工具或Veracode 提供的 API 來佈建 Azure AD 使用者帳戶。
> 

### <a name="assign-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Veracode 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者角色][200] 

**若要將 Britta Simon 指派給 Veracode，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Veracode]。

    ![應用程式清單中的 Veracode 連結](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. 在左側功能表中，按一下 [使用者和群組]。

    ![[使用者和群組] 連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![[新增指派] 窗格][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您在存取面板中按一下 [Veracode] 圖格時，應該會自動登入您的 Veracode 應用程式。
如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png


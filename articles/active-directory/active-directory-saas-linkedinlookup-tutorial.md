---
title: "教學課程：Azure Active Directory 與 LinkedIn Lookup 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 LinkedIn 查閱之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a>教學課程：Azure Active Directory 與 LinkedIn Lookup 整合

在此教學課程中，您學會如何 toointegrate LinkedIn 查閱與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 LinkedIn 查閱可以提供下列優點 hello:

- 您可以控制存取 tooLinkedIn 查閱 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooLinkedIn （單一登入） 查閱使用其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure LinkedIn 查閱與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 LinkedIn Lookup 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 LinkedIn 查閱
2. 設定並測試 Azure AD 單一登入

## <a name="adding-linkedin-lookup-from-hello-gallery"></a>從 hello 圖庫加入 LinkedIn 查閱
tooconfigure hello 整合 LinkedIn 查閱到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd LinkedIn 查閱。

**tooadd LinkedIn 查閱，從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新的應用程式**上 hello hello 對話方塊 tooadd 新應用程式頂端的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**LinkedIn 查閱**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. 在 hello 結果 窗格中，選取  **LinkedIn 查閱**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 LinkedIn Lookup 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow LinkedIn 查閱中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者和 LinkedIn 查閱中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** LinkedIn 查閱中。

tooconfigure 及 LinkedIn 查閱與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 LinkedIn 查閱](#creating-an-linkedin-lookup-test-user)** -toohave 許 Simon LinkedIn 查閱所連結的 toohello Azure AD 的表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 LinkedIn 查閱應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入搭配 LinkedIn 查閱，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **LinkedIn 查閱**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊，請在**模式**選取**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. 在不同的網頁瀏覽器視窗中，登入 tooyour **LinkedIn 查閱**身為系統管理員的網站。

4. 在 [帳戶中心] 中，按一下 [設定] 底下的 [全域設定]。 此外，選取**查閱**hello 下拉式清單中。

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. 按一下**或按一下這裡 tooload 並複製個別欄位從 hello 表單**和複製**實體識別碼**和**判斷提示取用者存取 (ACS) Url**

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. 在 Azure 入口網站，在**LinkedIn 查閱網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    a. 在 hello**識別碼**文字方塊中，輸入 hello**實體識別碼**從 LinkedIn 入口網站複製 

    b. 在 hello**回覆 URL**文字方塊中，輸入 hello**判斷提示取用者存取 (ACS) Url**從 LinkedIn 入口網站複製

7. 請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`
     
    > [!NOTE] 
    > 這不是真正的值。 hello 使用者具有 tooupdate 這些值以 hello 實際的登入 URL。 請連絡[LinkedIn 查閱用戶端支援小組](https://business.LinkedIn.com/lookup)tooget 此值。

8. 您**LinkedIn 查閱**應用程式特定的格式預期 hello SAML 判斷提示。 hello 使用者具有 tooadd 自訂屬性對應 toohello SAML 權杖屬性的組態。 下列螢幕擷取畫面的 hello 顯示範例。 hello 預設值是**使用者識別碼**是**user.userprincipalname**但 LinkedIn 查閱預期這個 toobe hello 使用者的電子郵件地址的對應。 您可以使用**user.mail**屬性從 hello 清單或使用您組織的組態為基礎的 hello 適當的屬性值。 

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. 在**使用者屬性**區段中，按一下**檢視和編輯所有其他使用者屬性**，並設定 hello 屬性。 hello 使用者需要 tooadd 四個宣告名為**電子郵件**，**部門**， **firstname**，和**lastname** hello 值是使用對應的 toobe**user.mail**， **user.department**， **user.givenname**，和**user.surname**分別

    | 屬性名稱 | 屬性值 |
    | --- | --- |
    | 電子郵件| user.mail |    
    | department| user.department |
    | firstname| user.givenname |
    | lastname| user.surname |

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    a. 按一下**加入屬性**tooopen hello**加入屬性**對話方塊。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    b. 在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。
    
    c. 從 hello**值**清單，顯示該資料列的型別 hello 屬性值。
    
    d. 按一下 [確定]。

10. 執行下列步驟在 hello hello**名稱**屬性-

    a. 按一下 hello 屬性 tooopen hello**編輯屬性**視窗。

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    b. 從 hello 刪除 hello URL 值**命名空間**。
    
    c. 按一下**確定**toosave hello 設定。

10. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. 跳過**LinkedIn 的管理設定**> 一節。 上傳 hello XML 檔案從 hello Azure 入口網站下載按一下 hello**上載 XML 檔案**選項。

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. 按一下**上**tooenable SSO。 SSO 狀態變更從**未連接**太**已連線**

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. 按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**許 Simon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**許 Simon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-an-linkedin-lookup-test-user"></a>建立 LinkedIn Lookup 測試使用者

連結的查閱應用程式支援恰好在 Time (JIT) 使用者佈建，以及之後驗證使用者會自動建立 hello 應用程式中。 啟動**自動指派授權**tooassign 授權 toohello 使用者。
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooLinkedIn 查閱。

![指派使用者][200] 

**tooassign 許 Simon tooLinkedIn 查閱，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**LinkedIn 查閱**。

    ![設定單一登入](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。

    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下的 hello LinkedIn 查閱磚 hello 存取面板中時，您應該重新導向的 tooOrganizational 頁面具有 tooprovide 您個人的 LinkedIn 帳戶詳細資料。 它會連結您的個人帳戶與您的 LinkedIn 商務帳戶。 

如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png


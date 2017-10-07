---
title: "教學課程：Azure Active Directory 與 O.C.  Tanner - AppreciateHub 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 O.C.之間 Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者。"
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
ms.openlocfilehash: 45052cf56e35746d7df5910162e40e3bbcad1aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a>教學課程：Azure Active Directory 與 O.C.  Tanner - AppreciateHub 的人員

在此教學課程中，您學會如何 toointegrate O.C. Tanner - AppreciateHub 與 Azure Active Directory (Azure AD) 整合。

整合 O.C. Tanner-AppreciateHub 與 Azure AD 提供下列優點 hello:

- 您可以控制存取 tooO.C Azure AD 中。 Tanner - AppreciateHub 的人員
- 您可以啟用您的使用者 tooautomatically get 登入 tooO.C。 Tanner - AppreciateHub (單一登入)
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure O.C.與 Azure AD 整合 Tanner-AppreciateHub，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 O.C. Tanner - AppreciateHub 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從組件庫新增 O.C. Tanner-AppreciateHub 從 hello 組件庫
2. 設定並測試 Azure AD 單一登入

## <a name="adding-oc-tanner---appreciatehub-from-hello-gallery"></a>從組件庫新增 O.C. Tanner-AppreciateHub 從 hello 組件庫
tooconfigure hello 整合的 O.C. Tanner-AppreciateHub 到 Azure AD，您需要 tooadd O.C. Tanner-AppreciateHub hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd O.C.Tanner-AppreciateHub 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**O.C.Tanner - AppreciateHub**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. 在 hello 結果 窗格中，選取  **O.C.Tanner-AppreciateHub**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會設定及測試與 O.C. 搭配運作的 Azure AD 單一登入 Tanner - AppreciateHub。

單一登入 toowork，Azure AD 需要 tooknow O.C.中的 hello 對等項目的使用者 Tanner-AppreciateHub 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者和 hello O.C.中相關的使用者之間的連結關聯性 Tanner-AppreciateHub 需要 toobe 建立。

在 O.C.  Hello Tanner-AppreciateHub，指派 hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 和測試 Azure AD 單一登入與 O.C. Tanner-AppreciateHub，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 O.C.Tanner-AppreciateHub 測試使用者](#creating-a-oc-tanner---appreciatehub-test-user)** -toohave 許 Simon O.C.中對應項目 Tanner-AppreciateHub 所連結的 toohello Azure AD 使用者表示法。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，方法，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您 O.C.中 Tanner - AppreciateHub 應用程式。

**tooconfigure Azure AD 單一登入與 O.C.Tanner-AppreciateHub，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **O.C.Tanner-AppreciateHub**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. 在 hello **O.C.Tanner-AppreciateHub 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    a. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`

    > [!NOTE] 
    > 這不是真實的值。 更新此值與 hello 實際的回覆 URL。 請連絡[O.C.Tanner-AppreciateHub 支援小組](mailto:sso@octanner.com)tooget 此值。

    b. 使用下列連結的 hello 開啟 hello 中繼資料檔案： [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata)。
   
    c. 找出 hello **md:AssertionConsumerService**節點。 
   
    d. 複製 hello hello 值**位置**屬性。 
   
    ![設定 App 設定][12]
   
    e. 在 hello**登入 URL**文字方塊中，超過 hello hello 上一個步驟中取得的值。

4. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. tooconfigure 單一登入上**O.C.Tanner-AppreciateHub**端，您需要下載 toosend hello**中繼資料 XML**太[O.C.Tanner-AppreciateHub 支援小組](mailto:sso@octanner.com)。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a>建立 O.C. Tanner - AppreciateHub 測試使用者

hello 本節目標在於 toocreate O.C.中呼叫許 Simon 的使用者 Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者。

**toocreate 使用者呼叫許 Simon O.C.Tanner-AppreciateHub，執行下列步驟的 hello:**

請要求您[O.C.Tanner-AppreciateHub 支援小組](mailto:sso@octanner.com)toocreate 具有做為 nameID 屬性 hello 相同的值為 hello 使用者名稱，Simon 許在 Azure AD 中的使用者。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooO.C 啟用許 Simon toouse Azure 單一登入。 Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者。

![指派使用者][200] 

**tooassign 許 Simon tooO.C。Tanner-AppreciateHub，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**O.C.Tanner - AppreciateHub**。

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。  
當您按一下 hello O.C. Tanner-AppreciateHub 磚 hello 存取面板中，您應該取得自動登入 tooyour O.C. Tanner - AppreciateHub 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
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


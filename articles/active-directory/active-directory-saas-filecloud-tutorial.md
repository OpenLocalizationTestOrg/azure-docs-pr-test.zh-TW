---
title: "教學課程：Azure Active Directory 與 FileCloud 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 FileCloud 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: fe58d01f02d6ce99ee9e2f83e7dc72c4434e13b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a>教學課程：Azure Active Directory 與 FileCloud 整合

在此教學課程中，您學會如何 toointegrate FileCloud 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 FileCloud 可以提供下列優點 hello:

- 您可以控制存取 tooFileCloud Azure AD 中。
- 您可以啟用您的使用者 tooautomatically get 登入 tooFileCloud （單一登入） 具有其 Azure AD 帳戶。
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure FileCloud 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 FileCloud 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 FileCloud
2. 設定並測試 Azure AD 單一登入

## <a name="adding-filecloud-from-hello-gallery"></a>從 hello 圖庫加入 FileCloud
tooconfigure hello 整合 FileCloud 到 Azure AD，您需要 tooadd FileCloud hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd FileCloud 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**FileCloud**，選取**FileCloud**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![FileCloud hello [結果] 清單中](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FileCloud 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 FileCloud 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello FileCloud 中相關的使用者之間的連結關聯性需要 toobe 建立。

FileCloud 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 FileCloud 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 FileCloud](#create-a-filecloud-test-user)**  -toohave 許 Simon FileCloud 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 FileCloud 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 FileCloud，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **FileCloud**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入連結][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. 在 hello **FileCloud 網域和 Url**區段中，執行下列步驟的 hello:

    ![FileCloud 網域和 URL 單一登入資訊](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.filecloudhosted.com`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello 登入 URL 和識別項。 請連絡[FileCloud 用戶端支援小組](mailto:support@codelathe.com)tooget 這些值。

4. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. 在 hello **FileCloud 組態**區段中，按一下**設定 FileCloud** tooopen**設定登入**視窗。 複製 hello **SAML 實體識別碼**從 hello**快速參考 > 一節。**

    ![FileCloud 設定](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour FileCloud 租用戶。

8. 在 hello 左側瀏覽窗格中，按一下 **設定**。 
   
    ![應用程式端上的設定區段](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. 按一下 [設定] 區段上的 [SSO] 索引標籤。 
   
    ![應用程式端上的單一登入索引標籤](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. 在 **Single Sign On (SSO) Settings** (單一登入 (SSO) 設定) 面板上，選取 **SAML** 作為 **Default SSO Type** (預設 SSO 類型)。
   
    ![應用程式端上的單一登入設定面板](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. 貼上**SAML 實體識別碼**，其中您從 Azure 入口網站複製到 hello **IdP 端點 URL**文字方塊。

    ![IDP 端點 URL 文字方塊](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. 在 [記事本]，複製到剪貼簿，其內容的 hello 中開啟下載的中繼資料檔案，然後將它貼入 toohello **IdP 中繼資料**上的文字方塊**SAML 設定**面板。

    ![應用程式端上的 IDP 中繼資料區段](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. 按一下 [儲存]  按鈕。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。

    ![hello [新增] 按鈕](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. 在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:

    ![hello [使用者] 對話方塊](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    a. 在 hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。

    c. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。

    d. 按一下 [建立] 。
 
### <a name="create-a-filecloud-test-user"></a>建立 FileCloud 測試使用者

hello 本節目標在於 toocreate FileCloud 中呼叫許 Simon 的使用者。 FileCloud 支援預設啟用的 Just-In-Time 佈建。 在這一節沒有您需要進行的動作項目。 如果尚未存在期間嘗試 tooaccess FileCloud，建立新的使用者。

>[!NOTE]
>若要手動 toocreate 使用者，您需要 toocontact hello [FileCloud 用戶端支援小組](mailto:support@codelathe.com)。 

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooFileCloud 啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooFileCloud，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**FileCloud**。

    ![hello 應用程式清單中的 hello FileCloud 連結](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。

當您按一下 hello FileCloud 磚 hello 存取面板中的時，您應該取得自動登入 tooyour FileCloud 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png


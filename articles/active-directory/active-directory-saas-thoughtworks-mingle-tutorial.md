---
title: "教學課程：Azure Active Directory 與 Thoughtworks Mingle 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Thoughtworks Mingle 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a>教學課程：Azure Active Directory 與 Thoughtworks Mingle 整合

在此教學課程中，您學會如何 toointegrate Thoughtworks Mingle 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 [Thoughtworks Mingle 可以提供下列優點 hello:

- 您可以控制存取 tooThoughtworks Mingle Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooThoughtworks Mingle （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 Thoughtworks Mingle 的整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Thoughtworks Mingle 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 組件庫中加入 [Thoughtworks Mingle
2. 設定並測試 Azure AD 單一登入

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a>從 hello 組件庫中加入 [Thoughtworks Mingle
tooconfigure hello 整合 Thoughtworks Mingle 到 Azure AD，您需要 tooadd Thoughtworks Mingle hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Thoughtworks Mingle 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory] 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 [hello] 搜尋方塊中，輸入**Thoughtworks Mingle**，選取**Thoughtworks Mingle**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![Thoughtworks Mingle hello [結果] 清單中](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Thoughtworks Mingle 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Thoughtworks Mingle 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Thoughtworks Mingle 中相關的使用者之間的連結關聯性需要 toobe 建立。

在 Thoughtworks Mingle 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 Azure AD 單一登入 Thoughtworks Mingle，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user) ** -toohave 許 Simon Thoughtworks Mingle 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Thoughtworks Mingle 應用程式中。

**tooconfigure Azure AD 單一登入 Thoughtworks Mingle 中，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Thoughtworks Mingle**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. 在 [hello **Thoughtworks Mingle 網域和 Url**區段中，執行下列步驟的 hello:

    ![Thoughtworks Mingle 網域和 URL 單一登入資訊](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.mingle.thoughtworks.com`

    > [!NOTE] 
    > hello 值不是真正的。 更新 hello 值與 hello 實際的登入 URL。 請連絡[Thoughtworks Mingle 的用戶端支援小組](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support)tooget hello 值。 
 
4. 在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. 登入 tooyour **Thoughtworks Mingle**以系統管理員身分的公司網站。

7. 按一下 hello **Admin**索引標籤，然後按 [下**SSO 組態**。
   
    ![[管理] 索引標籤](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO 組態")

8. 在 [hello **SSO 組態**區段中，執行下列步驟的 hello:
   
    ![SSO 組態](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO 組態")
    
    a. tooupload hello 中繼資料檔案，按一下 [**選擇檔案**。 

    b. 按一下 [儲存變更] 。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![hello [新增] 按鈕](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="create-a-thoughtworks-mingle-test-user"></a>建立 Thoughtworks Mingle 測試使用者

Azure AD 使用者 toobe 無法 toosign 中，它們必須已佈建的 toohello Thoughtworks Mingle 的應用程式使用他們的 Azure Active Directory 使用者名稱。 在 Thoughtworks Mingle 的 hello 情況下，佈建須手動進行。

**tooconfigure 使用者佈建，執行下列步驟的 hello:**

1. Tooyour Thoughtworks Mingle 公司網站 administrator 身分登入。

2. 按一下 [設定檔] 。
   
    ![第一個專案](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "第一個專案")

3. 按一下 hello **Admin**索引標籤，然後再按一下**使用者**。
   
    ![使用者](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "使用者")

4. 按一下 [新使用者] 。
   
    ![新增使用者](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "新增使用者")

5. 在 [hello**新使用者**對話方塊頁面上，執行下列步驟的 hello:
   
    ![[新增使用者] 對話方塊](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "[新增使用者]")  
 
    a. 型別 hello**登入名稱**，**顯示名稱**，**選擇密碼**，**確認密碼**的有效 azure AD 帳戶想 tooprovisionhello 到相關的文字方塊。 

    b. 選取 [完整使用者] 做為 [使用者類型]。

    c. 按一下 [建立這個設定檔] 。

>[!NOTE]
>您可以使用任何其他 Thoughtworks Mingle 使用者帳戶建立工具或 Api 提供 Thoughtworks Mingle tooprovision AAD 使用者帳戶。
> 

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooThoughtworks Mingle 啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooThoughtworks Mingle，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Thoughtworks Mingle**。

    ![hello 應用程式清單中的 hello Thoughtworks Mingle 連結](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。

當您按一下 hello Thoughtworks Mingle 並排顯示 hello 存取面板中的時，您應該取得自動登入 tooyour Thoughtworks Mingle 的應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png


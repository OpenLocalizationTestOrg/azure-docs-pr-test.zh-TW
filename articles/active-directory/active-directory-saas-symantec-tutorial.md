---
title: "教學課程：Azure Active Directory 與 Symantec Web Security Service (WSS) 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Symantec 網站安全性服務 (WSS) 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a>教學課程：Azure Active Directory 與 Symantec Web Security Service (WSS) 整合

在此教學課程中，您將學習如何 toointegrate 您 Symantec 網站安全性服務 (WSS) 帳戶與您的 Azure Active Directory (Azure AD) 帳戶，讓 WSS 可以驗證在 hello Azure AD 中佈建使用者使用 SAML 驗證並強制執行使用者或群組層級原則規則。

與 Azure AD 整合 Symantec 網站安全性服務 (WSS) 可以提供下列優點 hello:

- 管理所有 hello 一般使用者與您的 WSS 帳戶與您的 Azure AD 入口網站所使用的群組。 

- 允許 hello 結束使用者 tooauthenticate 本身中 WSS 使用其 Azure AD 認證。

- 啟用 hello 強制的使用者和群組 WSS 帳戶中所定義的層級原則規則。

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 整合與 Symantec 網站安全性服務 (WSS)，您需要下列項目 hello:

- Azure AD 訂用帳戶
- Symantec Web Security Service (WSS) 帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用 WSS 帳戶目前正用於生產用途。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用目前正用於生產用途的 WSS 帳戶來進行這項測試。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您將設定您 Azure AD tooenable 單一登入 tooWSS 使用 Azure AD 帳戶中定義的 hello 終端使用者認證。
本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 hello Symantec 網站安全性服務 (WSS) 應用程式
2. 設定並測試 Azure AD 單一登入

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a>從 hello 圖庫加入 Symantec 網站安全性服務 (WSS)
tooconfigure hello 整合 Symantec 網站安全性服務 (WSS) 至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Symantec 網站安全性服務 (WSS)。

**tooadd Symantec 網站安全性服務 (WSS) 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**Symantec 網站安全性服務 (WSS)**，選取**Symantec 網站安全性服務 (WSS)**然後按一下 從結果面板**新增**按鈕 tooadd hello應用程式。

    ![Symantec 網站安全性服務 (WSS) hello [結果] 清單中](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Symantec Web Security Service (WSS) 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Symantec 網站安全性服務 (WSS) 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello 相關的使用者在 Symantec 網站安全性服務 (WSS) 之間的連結關聯性需要 toobe 建立。

在 Symantec 網站安全性服務 (WSS)，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 和測試 Azure AD 單一登入與 Symantec 網站安全性服務 (WSS)，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 Symantec 網站安全性服務 (WSS) 測試使用者](#create-a-symantec-web-security-service-wss-test-user)** -toohave 許 Simon 中 Symantec Web 安全性服務 (WSS) 表示法連結的 toohello Azure AD 使用者的對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您的 Symantec 網站安全性服務 (WSS) 應用程式中。

**tooconfigure Azure AD 單一登入與 Symantec 網站安全性服務 (WSS)，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Symantec 網站安全性服務 (WSS)**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入連結][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. 在 hello **Symantec 網站安全性服務 (WSS) 網域和 Url**區段中，執行下列步驟的 hello:

    ![Symantec Web Security Service (WSS) 的網域和 URL 單一登入資訊](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    a. 在 hello**識別碼**文字方塊中，型別 hello URL:`https://saml.threatpulse.net:8443/saml/saml_realm`

    b. 在 hello**回覆 URL**文字方塊中，型別 hello URL:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`

    > [!NOTE]
    > Hello，請連絡[Symantec 網站安全性服務 (WSS) 用戶端支援小組](https://www.symantec.com/contact-us)如果值為 hello 的 hello**識別碼**和**回覆 URL**基於某些原因無法運作。

4. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. tooconfigure 單一登入 hello Symantec 網站安全性服務 (WSS) 端上，請參閱 toohello WSS 線上文件。 下載的 hello**中繼資料 XML**檔案需要 toobe 匯入 hello WSS 入口網站。 連絡 hello [Symantec 網站安全性服務 (WSS) 支援小組](https://www.symantec.com/contact-us)如果您需要協助以 hello hello WSS 入口網站上的組態。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。

    ![hello [新增] 按鈕](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. 在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:

    ![hello [使用者] 對話方塊](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    a. 在 hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。

    c. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。

    d. 按一下 [建立] 。
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a>建立 Symantec Web Security Service (WSS) 測試使用者

在本節中，您要在 Symantec Web Security Service (WSS) 中建立名為 Britta Simon 的使用者。 hello 對應結束使用者名稱可以 hello WSS 入口網站中手動建立，或您可以等候 hello 使用者/群組佈建在 hello Azure AD 同步處理的 toobe toohello WSS 網站後幾分鐘的時間 （~ 15 分鐘）。 您必須先建立和啟動使用者，然後才能使用單一登入。 hello 終端使用者電腦，將會使用的 toobrowse 網站的 hello 公用 IP 位址也需要 toobe hello Symantec 網站安全性服務 (WSS) 網站中佈建。

> [!NOTE]
> 請[按一下這裡](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1)tooget 您機器的公用 IPaddress。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooSymantec Web 安全性服務 (WSS)。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooSymantec Web 安全性服務 (WSS) 執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Symantec 網站安全性服務 (WSS)**。

    ![hello 應用程式清單中的 hello Symantec 網站安全性服務 (WSS) 連結](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您將測試 hello 單一登入功能，現在您已設定您的 WSS 帳戶 toouse SAML 驗證您的 Azure AD。

設定之後會 tooWSS，當您開啟網頁瀏覽器並 toobrowse tooa 站台，然後再試一次您網頁瀏覽器 tooproxy 流量重新導向 toohello Azure 登入頁面。 輸入 hello Azure AD (也就是 BrittaSimon) 中的 hello 的已佈建的 hello 測試終端使用者的認證，以及相關聯的密碼。 驗證之後，您會選擇可以 toobrowse toohello 網站。 您應該從瀏覽 tooa 特定站台，則當您以使用者 BrittaSimon 嘗試 toobrowse toothat 站台時，您應該看見 hello WSS 區塊頁面 hello WSS 端 tooblock BrittaSimon 中建立的原則規則。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png


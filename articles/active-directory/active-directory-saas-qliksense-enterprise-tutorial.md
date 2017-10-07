---
title: "教學課程：Azure Active Directory 與 Qlik Sense Enterprise 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Qlik 意義企業之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a>教學課程：Azure Active Directory 與 Qlik Sense Enterprise 整合

在此教學課程中，您學會如何 toointegrate Qlik 意義企業與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Qlik 意義 Enterprise 可以提供下列優點 hello:

- 您可以控制存取 tooQlik 意義 Enterprise 的 Azure AD 中。
- 您可以啟用您的使用者 tooautomatically get 登入 tooQlik （單一登入） 的意義上企業與他們的 Azure AD 帳戶。
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Qlik 意義企業與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Qlik Sense Enterprise 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Qlik 意義 Enterprise
2. 設定並測試 Azure AD 單一登入

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a>從 hello 圖庫加入 Qlik 意義 Enterprise
tooconfigure hello 整合 Qlik 意義企業到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Qlik 意義企業。

**tooadd Qlik 意義企業 hello 圖庫中，從執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory] 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**Qlik 意義企業**，選取**Qlik 意義企業**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![Qlik hello [結果] 清單中的意義上企業](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Qlik Sense Enterprise 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow Qlik 意義企業中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Qlik 意義企業中的相關的使用者之間的連結關聯性需要 toobe 建立。

在 Qlik 意義 Enterprise 中，指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 Qlik 意義企業與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Qlik 意義企業](#create-a-qlik-sense-enterprise-test-user)** -toohave 許 Simon Qlik 是連結的 toohello Azure AD 使用者表示的意義上企業中的對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Qlik 意義企業應用程式中設定單一登入。

**Qlik 意義企業，使用 Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**

1. 在 Azure 入口網站上 hello hello **Qlik 意義企業**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入連結][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. 在 [hello **Qlik 意義企業網域和 Url**區段中，執行下列步驟的 hello:

    ![Qlik Sense Enterprise 網域與 URL 單一登入資訊](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    a. 在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`
    
    > [!NOTE]
    > 請注意結尾的斜線結尾 hello 這個 URI 的 hello。 這是必要的。
    
    b. 在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > 這些都不是真正的值。 這些值與 hello 實際登入 URL 和識別碼，稍後在本教學課程中或連絡所說明的更新[Qlik 意義企業用戶端支援小組](https://www.qlik.com/us/services/support)tooget 這些值。 

4. 在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. 準備 hello 同盟中繼資料 XML 檔案，以便您可以上傳該 tooQlik 意義上伺服器。
   
    > [!NOTE]
    > 上傳之前 hello IdP 中繼資料 toohello Qlik 意義伺服器，hello 檔案需要編輯 toobe tooremove 資訊 tooensure 正常運作之間 Azure AD 和 Qlik 意義上伺服器。
    
    ![QlikSense][qs24]
   
    a. 開啟 hello FederationMetaData.xml 檔案，從文字編輯器中的 Azure 入口網站下載。
   
    b. 搜尋的 hello value **RoleDescriptor**。  共會有四個項目 (兩對開頭和結尾元素標籤)。
   
    c. 從 hello 檔案之間刪除 hello RoleDescriptor 標記和所有資訊。
   
    d. 儲存 hello 檔案，並將它附近保留供稍後在這份文件中使用。

7. 瀏覽 toohello Qlik 意義 Qlik 管理主控台 (QMC)，使用者可以建立虛擬 proxy 組態。

8. 在 [hello QMC，按一下 hello**虛擬 Proxy**功能表項目。
   
    ![QlikSense][qs6] 

9. 在 hello 囉 」 畫面底部，按一下 [hello**建立新**] 按鈕。
   
    ![QlikSense][qs7]

10. hello 虛擬 proxy 編輯畫面隨即出現。  Hello hello 螢幕的右邊是顯示組態選項的功能表。
   
    ![QlikSense][qs9]

11. 檢查 hello 識別功能表選項，輸入 hello hello Azure 的虛擬 proxy 組態的識別資訊。
    
    ![QlikSense][qs8]  
    
    a. hello**描述**欄位是 hello 虛擬 proxy 組態的易記名稱。  輸入說明的值。
    
    b. hello**首碼**欄位識別 hello 虛擬 proxy 端點連接 tooQlik 意義上與 Azure AD 單一登入。  輸入此虛擬 Proxy 的獨特前置詞名稱。
    
    c. **工作階段閒置逾時 （分鐘）** hello 逾時，透過此虛擬 proxy 的連線。
    
    d. hello**工作階段 cookie 標頭名稱**是 hello cookie 名稱儲存 hello 的 hello Qlik 意義上，使用者的工作階段收到驗證成功後的工作階段識別項。  此名稱必須是唯一的。

12. 按一下 hello 驗證功能表選項 toomake 看到它。  hello 驗證畫面隨即出現。
    
    ![QlikSense][qs10]
    
    a. hello**匿名存取模式**下拉式清單決定匿名使用者可能會透過 hello 虛擬 proxy 存取 Qlik 意義。  hello 預設選項為匿名使用者。
    
    b. hello**驗證方法**下拉式清單可讓您決定要使用 hello 驗證配置 hello 虛擬 proxy。  選取 [SAML hello 下拉式清單中。  此時會顯示更多選項。
    
    c. 在 [hello **SAML 主機 URI 欄位**，輸入的 hello 主機名稱的使用者輸入 tooaccess Qlik 意義上的，透過這個 SAML 虛擬 proxy。  hello 主機名稱為 hello Qlik 意義伺服器 hello uri。
    
    d. 在 [hello **SAML 實體識別碼**，輸入的 hello hello SAML 主機 URI 欄位中輸入相同的值。
    
    e. hello **SAML Ldp 中繼資料**是稍早在 hello 中編輯 hello 檔案**編輯同盟中繼資料從 Azure AD 設定**> 一節。  **上傳之前 hello IdP 中繼資料，hello 檔案需要編輯 toobe** Azure AD 之間的 tooremove 資訊 tooensure 正常運作和 Qlik 意義上伺服器。  **請如果 hello 檔案有尚未 toobe 編輯，參閱上述的 toohello 指示。**  如果已編輯 hello 檔案按一下 hello 瀏覽按鈕並選取 hello 編輯過的中繼資料檔案 tooupload 它 toohello 虛擬的 proxy 設定。
    
    f. 輸入代表 hello hello SAML 屬性 hello 屬性名稱或結構描述參照**UserID** Azure AD 會傳送 toohello Qlik 意義上伺服器。  提供設定 hello Azure 應用程式的螢幕前結構描述參考資訊。  toouse hello name 屬性，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`。
    
    g. 輸入 hello hello 值**使用者目錄**tooQlik 意義伺服器透過 Azure AD 驗證時，這會是附加的 toousers。  硬式編碼值必須以**方括號 []** 括住。  toouse 屬性傳送 hello Azure AD SAML 判斷提示，在此文字方塊中輸入 hello 屬性名稱的 hello**沒有**方括號。
    
    h. hello **SAML 簽章演算法**集 hello 服務提供者 （在此案例的 Qlik 意義伺服器） 的憑證簽署 hello 虛擬的 proxy 設定。  如果 Qlik 意義伺服器使用信任的憑證，使用 Microsoft Enhanced RSA 與 AES 密碼編譯提供者所產生，變更 hello SAML 簽章演算法太**sha-256**。
    
    i. hello SAML 屬性的對應區段可讓您在安全性規則中使用的群組傳送 toobe tooQlik 意義之類的其他屬性。

13. 按一下 hello**負載平衡**功能表選項 toomake 看到它。  hello 負載平衡畫面隨即出現。
    
    ![QlikSense][qs11]

14. 按一下 hello**新增新的伺服器節點**按鈕，選取引擎] 節點或節點 Qlik 意義上會傳送工作階段 toofor 負載平衡的目的，然後按一下 [hello**新增**] 按鈕。
    
    ![QlikSense][qs12]

15. 按一下 hello 進階] 功能表選項 toomake 看到它。 hello 進階的畫面隨即出現。
    
    ![QlikSense][qs13]
    
    hello 主機白名單識別時連接 toohello Qlik 意義伺服器可接受的主機名稱。  **輸入 hello tooQlik 意義伺服器連線時，使用者將指定的主機名稱。** hello 主機名稱為 hello 相同的值為 hello hello https:// 沒有 SAML 主機 uri。

16. 按一下 hello**套用**] 按鈕。
    
    ![QlikSense][qs14]

17. 按一下 [確定] tooaccept hello 警告訊息，指出將會重新啟動連結的 toohello 虛擬 proxy 的 proxy。
    
    ![QlikSense][qs15]

18. 右側 hello 囉 」 畫面，hello 相關聯的項目功能表隨即出現。  按一下 hello **Proxy**功能表選項。
    
    ![QlikSense][qs16]

19. hello proxy 畫面隨即出現。  按一下 hello**連結**按鈕 hello 底部 toolink proxy toohello 虛擬 proxy。
    
    ![QlikSense][qs17]

20. 選取 hello proxy 節點，將會支援此虛擬 proxy 連線並按一下 hello**連結**] 按鈕。  之後連結，hello proxy 會列在相關聯 proxy。
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. 後約五 tooten 秒 hello 重新整理 QMC 訊息會出現。  按一下 hello**重新整理 QMC** ] 按鈕。
    
    ![QlikSense][qs20]

22. 當 hello QMC 重新整理時，按一下以 hello**虛擬 proxy**功能表項目。 hello 新 SAML 虛擬 proxy 的項目會列在 hello 囉 」 畫面上的資料表。  只要在 hello 虛擬 proxy 項目上按一下。
    
    ![QlikSense][qs51]

23. 在 hello 囉 」 畫面底部，將會啟動 hello 下載 SP 中繼資料] 按鈕。  按一下 hello**下載 SP 中繼資料**按鈕 toosave hello 中繼資料 tooa 檔案。
    
    ![QlikSense][qs52]

24. 開啟 hello sp 中繼資料檔案。  觀察 hello **entityID**項目和 hello **AssertionConsumerService**項目。  這些值是對等 toohello**識別碼**和 hello**登入 URL** hello Azure AD 應用程式組態中。 將這些值貼入中 hello **Qlik 意義企業網域和 Url**如果它們不相符，則您應該將它們取代 hello Azure AD 應用程式組態精靈中的 hello Azure AD 的應用程式組態中的區段。
    
    ![QlikSense][qs53]

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello Azure 入口網站，hello 左窗格中，按一下 [hello **Azure Active Directory** ] 按鈕。

   ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下 [**所有使用者**。

   ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。

   ![hello [新增] 按鈕](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. 在 [hello**使用者**對話方塊方塊中，執行下列步驟的 hello:

   ![hello [使用者] 對話方塊](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   a. 在 [hello**名稱**方塊中，輸入**BrittaSimon**。

   b. 在 [hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。

   c. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 [hello**密碼**方塊。

   d. 按一下 [建立] 。
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a>建立 Qlik Sense Enterprise 測試使用者

在本節中，您要在 Qlik Sense Enterprise 中建立名為 Britta Simon 的使用者。 使用[Qlik 意義企業用戶端支援小組](https://www.qlik.com/us/services/support)hello Qlik 意義企業平台中新增 hello 使用者。 您必須先建立和啟動使用者，然後才能使用單一登入。 

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooQlik 意義企業啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooQlik 意義企業執行 hello 下列步驟：**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Qlik 意義企業**。

    ![hello 應用程式清單中的 hello Qlik 意義企業連結](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello Qlik 意義企業磚 hello 存取面板中的時，您應該取得自動登入 tooyour Qlik 意義企業應用程式。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png


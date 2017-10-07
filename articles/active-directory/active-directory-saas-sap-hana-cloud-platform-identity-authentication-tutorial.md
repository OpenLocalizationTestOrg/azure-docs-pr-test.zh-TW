---
title: "教學課程：Azure Active Directory 與 SAP HANA Cloud Platform Identity Authentication 整合 | Microsoft Docs"
description: "了解如何 tooconfigure 單一登入 Azure Active Directory 之間，以及 SAP HANA 雲端平台身分識別驗證。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a>教學課程：Azure Active Directory 與 SAP HANA Cloud Platform Identity Authentication 整合

在此教學課程中，您學習如何 toointegrate SAP HANA 雲端平台與 Azure Active Directory (Azure AD) 的身分識別驗證。 SAP HANA 雲端平台身分識別驗證做為 proxy IdP tooaccess SAP 應用程式使用 Azure AD 作為 hello 主要 IdP。

SAP HANA 雲端平台身分識別驗證整合與 Azure AD 可以提供下列優點 hello:

- 您可以控制存取 tooSAP 應用程式的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get tooSAP 已登入的應用程式單一登入 (SSO) 與他們的 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。


## <a name="prerequisites"></a>必要條件

tooconfigure 與 SAP HANA 雲端平台身分識別驗證的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 SSO 的 **SAP HANA Cloud Platform Identity Authentication** 訂用帳戶


>[!NOTE] 
>本教學課程中的步驟 tootest hello，不建議使用實際執行環境。
>

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。

本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 加入 SAP HANA 雲端平台身分識別驗證從 hello 組件庫
2. 設定並測試 Azure AD SSO

一頭栽進 hello 技術詳細資料之前, 有您要在 toolook 重要 toounderstand hello 概念。 hello SAP HANA 雲端平台識別身分驗證與 Azure Active Directory 的同盟可讓您跨應用程式或服務受到 AAD （做為 IdP) SAP 應用程式與服務保護的 SAP HANA 雲端平台識別 tooimplement SSO驗證。

目前，SAP HANA 雲端平台身分識別驗證會做為 Proxy 身分識別提供者的 tooSAP 應用程式。 Azure Active Directory 輪流做為前置身分識別提供者在此安裝程式中的 hello。 

hello 下列圖表將說明這點：    

![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

透過此設定，您的 SAP HANA Cloud Platform Identity Authentication 租用戶會設定為 Azure Active Directory 中信任的應用程式。 

後續 hello SAP HANA 雲端平台身分識別驗證管理主控台中設定所有的 SAP 應用程式和您想要透過這種方式 tooprotect 服務 ！

這表示該授權授與存取 tooSAP 應用程式，並服務需求 tootake 置於 SAP HANA 雲端平台身分識別驗證 （做為 Azure Active Directory 中的相對於的 tooconfiguring 授權） 這類安裝程式。

藉由設定為透過 hello Azure Active Directory Marketplace 應用程式的 SAP HANA 雲端平台身分識別驗證，您不需要設定所需的個別宣告 care of tootake / 需要 tooproduce SAML 判斷提示和轉換SAP 應用程式的有效驗證 token。

>[!NOTE] 
>Web SSO 目前只經過這兩個合作夥伴測試。 應用程式對 API 或 API 對 API 通訊所需的流程應能運作，但尚未經過測試。 它們會在後續活動中進行測試。
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a>從 hello 圖庫新增 SAP HANA 雲端平台身分識別驗證
tooconfigure hello 整合 SAP HANA 雲端平台身分識別驗證至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd SAP HANA 雲端平台身分識別驗證。

**tooadd SAP HANA 雲端平台身分識別驗證從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 [hello [ **Azure 管理入口網站**](https://portal.azure.com)，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新增**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**SAP HANA 雲端平台身分識別驗證**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. 在 [hello [結果] 窗格中，選取 [ **SAP HANA 雲端平台身分識別驗證**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAP HANA Cloud Platform Identity Authentication 設定及測試 Azure AD SSO。

SSO toowork Azure AD 需要 tooknow hello 對應項目在 SAP HANA 雲端平台身分識別驗證的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 SAP HANA 雲端平台身分識別驗證中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username**在 SAP HANA 雲端平台身分識別驗證。

tooconfigure 及測試與 SAP HANA 雲端平台身分識別驗證 Azure AD SSO，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 SAP HANA 雲端平台身分識別驗證測試使用者](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** -toohave 許 Simon SAP HANA 雲端平台身分識別的驗證連結的 toohello Azure AD 的她的表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-sso"></a>設定 Azure AD SSO

在本節中，您可以 hello Azure 管理入口網站中啟用 Azure AD SSO，並設定單一登入 SAP HANA 雲端平台身分識別驗證應用程式中。

SAP HANA 雲端平台身分識別驗證應用程式預期 hello SAML 判斷提示，以特定格式。 您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。 hello 下列螢幕擷取畫面會顯示這個範例。

![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

**tooconfigure 與 SAP HANA 雲端平台身分識別驗證，Azure AD SSO 執行 hello 下列步驟：**

1. 在 hello Azure 管理入口網站上 hello **SAP HANA 雲端平台身分識別驗證**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入][5]

3. 在 [hello**使用者屬性**區段 hello**單一登入**] 對話方塊中，如果您的 SAP 應用程式預期的屬性，例如"firstName"。 在 hello SAML token 屬性對話方塊中，加入 hello"firstName"屬性。
 1. 按一下**加入屬性**tooopen hello**加入屬性**對話方塊。
 
    ![設定單一登入][6]

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. 在 [hello**屬性名稱**文字方塊中，型別 hello 屬性名稱"firstName"。
 3. 從 hello**屬性值**清單，選取 hello"user.givenname"的屬性值。
 4. 按一下 [確定] 。

4. 在 [hello **SAP HANA 雲端平台識別身分驗證網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. 在 [hello**登入 URL**文字方塊中，輸入 hello 登入 URL hello SAP 應用程式。
 2. 在 [hello**識別碼**文字方塊中，類型 hello 值下列模式：`<entity-id>.accounts.ondemand.com` 
    * 如果您不知道此值，請遵循 hello SAP HANA 雲端平台身分識別驗證文件[SAML 2.0 設定租用戶](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html)。

5. 在 [hello **SAP HANA 雲端平台身分識別驗證組態**區段中，按一下**設定 SAP HANA 雲端平台身分識別驗證**tooopen**設定登入**對話方塊。 然後按一下 [上**SAML XML 中繼資料**將 hello 檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. 設定應用程式的 SSO tooget 移 tooSAP HANA 雲端平台身分識別驗證管理主控台。 hello URL 具有下列模式的 hello:`https://<tenant-id>.accounts.ondemand.com/admin`
 * 然後，遵循 hello 文件上 SAP HANA 雲端平台身分識別驗證太[設定 Microsoft Azure AD 成為公司身分識別提供者，在 SAP HANA 雲端平台身分識別驗證](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html)。 

7. 在 [hello Azure 管理入口網站中，按一下 [**儲存**] 按鈕。
8. 繼續執行下列步驟，只有當您想 tooadd，並針對另一個的 SAP 應用程式啟用 SSO 的 hello。 重複步驟 hello > 一節 「 加入 SAP HANA 雲端平台身分識別驗證從 hello 組件庫 」 tooadd SAP HANA 雲端平台身分識別驗證的另一個執行個體。
9. 在 hello Azure 管理入口網站上 hello **SAP HANA 雲端平台身分識別驗證**應用程式整合頁面上，按一下 [**連結登入**。

    ![設定連結的登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. 然後，儲存 hello 組態。

>[!NOTE] 
>hello 新應用程式將會利用 hello 舊版 SAP 應用程式的 hello SSO 組態。 請確定您使用 hello hello SAP HANA 雲端平台身分識別驗證管理主控台中相同公司身分識別提供者。
>

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節 hello 目標是 toocreate 測試使用者呼叫許 Simon hello 新入口網站中。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。
  2. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。
  3. 選取**顯示密碼**記下 hello hello 值**密碼**。
  4. 按一下 [建立] 。 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a>建立 SAP HANA Cloud Platform Identity Authentication 測試使用者

您不需要 toocreate 上 SAP HANA 雲端平台身分識別驗證的使用者。 Hello Azure AD 使用者存放區中的使用者可以使用 hello SSO 功能。

SAP HANA 雲端平台身分識別驗證支援 hello 識別身分同盟選項。 這個選項允許 hello 應用程式 toocheck hello hello 公司身分識別提供者所驗證的使用者有在 hello 使用者存放區的 SAP HANA 雲端平台身分識別驗證。 

Hello 預設設定，在 hello 識別身分同盟選項已停用。 如果已啟用識別身分同盟，只有 hello 會匯入 SAP HANA 雲端平台身分識別驗證的使用者都能 tooaccess hello 應用程式。 

如需有關如何在 tooenable 或停用識別身分同盟與 SAP HANA 雲端平台身分識別驗證，請參閱啟用識別身分同盟與 SAP HANA 雲端平台身分識別驗證中[設定識別身分同盟以 hello 使用者存放區的 SAP HANA 雲端平台身分識別驗證。](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與他們存取 tooSAP HANA 雲端平台身分識別驗證。

![指派使用者][200] 

**tooassign 許 Simon tooSAP HANA 雲端平台身分識別驗證，執行下列步驟的 hello:**

1. 在 [hello Azure 管理入口網站中，開啟 [hello 應用程式] 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**SAP HANA 雲端平台身分識別驗證**。

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    

### <a name="test-single-sign-on"></a>測試單一登入

本節中，您可以測試使用存取面板 hello Azure AD 的 SSO 組態。

當您按一下 hello SAP HANA 雲端平台身分識別驗證磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 SAP HANA 雲端平台身分識別驗證應用程式。


## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png
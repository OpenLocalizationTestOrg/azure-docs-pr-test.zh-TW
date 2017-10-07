---
title: "教學課程：Azure Active Directory 與 SAP HANA 雲端平台整合 | Microsoft Docs"
description: "了解如何與 Azure Active Directory tooenable toouse SAP HANA Cloud Platform 的單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>教學課程：Azure Active Directory 與 SAP HANA 雲端平台整合
本教學課程的 hello 目標是 Azure 與 SAP HANA Cloud Platform tooshow hello 整合。

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

* 有效的 Azure 訂閱
* SAP HANA 雲端平台帳戶

完成本教學課程之後, hello 您已指派的 tooSAP HANA 雲端平台將會無法 toosingle 登入使用 hello hello 應用程式的 Azure AD 使用者[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

>[!IMPORTANT]
>您需要 toodeploy 自己的應用程式，或訂閱 tooan 應用程式帳戶 tootest 單一登入您 SAP HANA 雲端平台上。 在此教學課程中，應用程式被部署在 hello 帳戶。
> 
> 

本教學課程所述的 hello 案例包含下列建置組塊的 hello:

1. 啟用 SAP HANA Cloud Platform 的 hello 應用程式整合
2. 設定單一登入 (SSO)
3. 指派角色 tooa 使用者
4. 指派使用者

![案例](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "案例")

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a>啟用 SAP HANA Cloud Platform 的 hello 應用程式整合
本節 hello 目標是 toooutline 如何 SAP HANA Cloud Platform tooenable hello 應用程式整合。

**tooenable hello 應用程式整合，SAP HANA Cloud platform，執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站中，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。
   
    ![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
    ![應用程式](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "應用程式")
4. 按一下**新增**hello hello 頁底端。
   
    ![新增應用程式](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "新增應用程式")
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
    ![從資源庫新增應用程式](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "從資源庫新增應用程式")
6. 在 hello**搜尋方塊**，型別**SAP HANA Cloud Platform**。
   
    ![應用程式資源庫](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "應用程式資源庫")
7. 在 hello 結果窗格中，選取  **SAP HANA Cloud Platform**，然後按一下**完成**tooadd hello 應用程式。
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>設定單一登入

hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooSAP HANA 雲端平台與 Azure AD 的同盟，使用的帳戶如何 hello SAML 通訊協定為基礎。

此程序的一部分，您就需要的 tooupload base 64 編碼的憑證 tooyour SAP HANA Cloud Platform 租用戶。  

如果您不熟悉這個程序，請參閱[如何 tooconvert 二進位憑證到文字檔案](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure 單一登入，請執行下列步驟的 hello:**

1. 在 Azure 傳統入口網站，在 hello hello **SAP HANA Cloud Platform**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。
   
    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "設定單一登入")
2. Hello 上**如何想您 tooSAP HANA 雲端平台上的使用者 toosign**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "設定單一登入")
3. 在不同的網頁瀏覽器視窗中，登入在 https://account toohello SAP HANA Cloud Platform Cockpit。\<橫向主機\>.ondemand.com/cockpit (例如： *https://account.hanatrial.ondemand.com/cockpit*)。
4. 按一下 hello**信任** 索引標籤。
   
    ![信任](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "信任")
5. 在信任管理區段中，執行下列步驟的 hello:
   
    ![取得中繼資料](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "取得中繼資料")
   
   1. 按一下 hello**本機服務提供者** 索引標籤。
   2. toodownload hello SAP HANA Cloud Platform 中繼資料檔案中，按一下**取得中繼資料**。
6. Hello 作用中的 Azure 傳統入口網站中，在 hello**設定應用程式 URL**頁面上，執行下列步驟，hello，然後按一下**下一步**。
   
    ![設定應用程式 URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "設定應用程式 URL")
   
   1. 在 hello**登入 URL**文字方塊中，為您的使用者 toosign 所使用的型別 hello URL 您**SAP HANA Cloud Platform**應用程式。 這是 SAP HANA Cloud Platform 應用程式中某個受保護資源的 hello 帳戶特有 URL。 hello URL 根據下列模式的 hello: *https://\<applicationName\>\<accountName\>。\<橫向主機\>.ondemand.com/\<路徑\_至\_保護\_資源\>* (例如： *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >這是您需要 hello 使用者 tooauthenticate 的 SAP HANA Cloud Platform 應用程式中的 hello URL。
     > 

   2. 開啟 hello 下載 SAP HANA Cloud Platform 中繼資料檔案，然後再找出 hello **ns3: assertionconsumerservice**標記。
   3. 複製 hello hello 值**位置**屬性，然後再將它貼到 hello **SAP HANA Cloud Platform 回覆 URL**文字方塊。

7. 在 hello**於 SAP HANA Cloud Platform 設定單一登入**頁面、 toodownload 中繼資料，按一下**下載中繼資料**，然後儲存您的電腦上的 hello 檔案。
   
    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "設定單一登入")
8. 在 hello hello SAP HANA Cloud Platform Cockpit 上**本機服務提供者**區段中，執行下列步驟的 hello:
   
    ![信任管理](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "信任管理")
   
  1. 按一下 [ **編輯**]。
  2. 針對 [組態類型]，選取 [自訂]。
  3. 做為**本機提供者名稱**，保留 hello 預設值。
  4. toogenerate**簽署金鑰**和**簽署憑證**金鑰組，請按一下**產生金鑰組**。
  5. 針對 [主體傳播]，選取 [已停用]。
  6. 針對 [強制驗證]，選取 [已停用]。
  7. 按一下 [儲存] 。

9. 按一下 hello**信任身分識別提供者**索引標籤，然後再按一下**新增信任身分識別提供者**。
   
    ![信任管理](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "信任管理")
   
    >[!NOTE]
    >toomanage hello 清單中的受信任的身分識別提供者，您需要 toohave hello 本機服務提供者 區段中選擇 hello 自訂組態類型。 預設組態類型，您會有非可編輯與隱含信任 toohello SAP ID 服務。 針對 [無]，您不具任何信任設定。
    > 
    > 

10. 按一下 hello**一般**索引標籤，然後再按一下**瀏覽**tooupload hello 下載中繼資料檔案。
    
    ![信任管理](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "信任管理")
    
    >[!NOTE]
    >上傳 hello 中繼資料檔案之後, hello 值**單一登入 URL**，**單一登出 URL**和**簽署憑證**會自動填入。
    > 
    > 

11. 按一下 hello**屬性** 索引標籤。
12. 在 hello**屬性**索引標籤上，執行下列步驟的 hello:
    
    ![屬性](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "屬性") 
  * 按一下**新增屬性**，然後加入下列判斷提示型屬性的 hello:
       
    | 判斷提示屬性 | 主體屬性 |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname |firstname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname |lastname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress |電子郵件 
   
     >[!NOTE]
     >hello 組態的 hello 屬性取決於如何在 HCP 上的 hello 應用程式開發，也就是預期在 SAML 回應 hello 和 （主體屬性） 的名稱下他們存取 hello 程式碼中的此屬性的屬性。
     > 
     >  

    1.  hello**預設屬性**在 hello 螢幕擷取畫面是只供說明之用。 它不需要 toomake hello 案例的工作。   
    2.  hello 名稱和值**主體屬性**示 hello 螢幕擷取畫面，取決於 hello 應用程式的開發方式。 您的應用程式很可能需要不同的對應。
     
13. 在 Azure 傳統入口網站，在 hello hello**於 SAP HANA Cloud Platform 設定單一登入**頁面，選取 hello 單一登入組態確認，然後按**完成**。
    
    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "設定單一登入")

###<a name="assertion-based-groups"></a>以判斷提示為基礎的群組
在選擇性的步驟中，您可以為 Azure Active Directory 識別提供者設定以判斷提示為基礎的群組。

使用 SAP HANA 雲端平台上的群組可讓您 toodynamically 指派一個或多個使用者 tooone 或多個角色，在 SAP HANA Cloud Platform 的應用程式，取決於中 hello SAML 屬性的值 2.0 判斷提示。 

例如，如果 hello 判斷提示包含 hello 屬性 」*合約 = 暫存*"，您可能要讓所有受影響的使用者 toobe 加入的 toohello 群組"*暫存*"。 hello 群組 」*暫存*」 可能包含一或多個角色部署 SAP HANA Cloud Platform 帳戶中的一個或多個應用程式。
 
當您想 toosimultaneously 指派許多使用者 tooone 或多個角色的應用程式在 SAP HANA Cloud Platform 帳戶中，請使用判斷提示型群組。 如果您想 tooassign 只有少數使用者 toospecific 角色數目，我們建議您直接在 hello 分派給他們"**授權**"hello SAP HANA Cloud Platform cockpit 索引標籤。

## <a name="assign-a-role-tooa-user"></a>指派給某個角色 tooa 使用者
在訂單 tooenable Azure AD 使用者 toolog 入 SAP HANA Cloud Platform，您必須指派 hello SAP HANA Cloud Platform toothem 中的角色。

**tooassign 角色 tooa 使用者時，執行下列步驟的 hello:**

1. 登入 tooyour **SAP HANA Cloud Platform** cockpit。
2. 執行下列 hello:
   
   ![授權](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "授權")
   
  1. 按一下 [授權]。
  2. 按一下 hello**使用者** 索引標籤。
  3. 在 hello**使用者**文字方塊中，型別 hello 使用者的電子郵件地址。
  4. 按一下**指派**tooassign hello 使用者 tooa 角色。
  5. 按一下 [儲存] 。

## <a name="assign-users"></a>指派使用者
tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。

**tooassign 使用者 tooSAP HANA Cloud Platform 中，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，建立測試帳戶。
2. 在 hello **SAP HANA Cloud Platform**應用程式整合頁面上，按一下 **指派使用者**。
   
   ![指派使用者](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "指派使用者")
3. 選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。
   
   ![是](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "是")

如果您想 tootest SSO 設定，請開啟 hello 存取面板。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。


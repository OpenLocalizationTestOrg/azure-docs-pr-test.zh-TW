---
title: "aaaHeader 式驗證搭配 PingAccess 的 Azure AD Application Proxy |Microsoft 文件"
description: "發行應用程式與 PingAccess 和應用程式 Proxy toosupport 標頭為基礎的驗證。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a>使用應用程式 Proxy 與 PingAccess 的單一登入之標頭式驗證

Azure Active Directory 應用程式 Proxy 及 PingAccess 通力合作，同時存取 tooeven tooprovide Azure Active Directory 客戶更多應用程式。 PingAccess 展開 hello[現有應用程式 Proxy 的供應項目](active-directory-application-proxy-get-started.md)tooinclude 單一登入存取 tooapplications 使用驗證標頭。

## <a name="what-is-pingaccess-for-azure-ad"></a>什麼是 Azure AD 的 PingAccess？

Azure Active directory PingAccess 是 PingAccess，可讓您 toogive 使用者存取權和單一登入 tooapplications 使用驗證標頭的供應項目。 應用程式 Proxy 會將如同任何其他的這些應用程式，使用 Azure AD tooauthenticate 存取權，然後讓流量通過 hello 連接器服務。 PingAccess 位於前面 hello 應用程式，並將 hello 來自 Azure AD 存取權杖轉譯成標頭，以便 hello 應用程式收到 hello 驗證 hello 它可以讀取的格式。

登入時 toouse 您公司的應用程式時，您的使用者將不會採取任何不同發現。 這些還是可以在任何裝置上從任何地方運作。 

Hello 應用程式 Proxy 連接器直接遠端流量 tooall 應用程式，不論其驗證類型，因為它們將會自動，以及繼續 tooload 平衡。

## <a name="how-do-i-get-access"></a>如何取得存取權？

因為這種情況是透過 Azure Active Directory 和 PingAccess 之間的合作關係提供，您會需要這兩種服務的授權。 不過，Azure Active Directory Premium 訂閱包含遮蓋 too20 應用程式的基本 PingAccess 授權。 如果您需要 toopublish 20 個以上的標頭應用程式，您可以從 PingAccess 購買額外的授權。 

如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。

## <a name="publish-your-application-in-azure"></a>在 Azure 中發佈應用程式

這篇文章僅供人發行應用程式，但此案例中的 hello 第一次。 它引導 tooget 啟動方式使用應用程式和 PingAccess，此外 toohello 發行步驟。 如果您已經設定這兩項服務，但是想發行步驟 hello 的重新整理程式，您可以略過 hello 連接器安裝，移太[加入您的應用程式 tooAzure 應用程式 Proxy 與 AD](#add-your-app-to-Azure-AD-with-Application-Proxy)。

>[!NOTE]
>由於此案例是 Azure AD 之間的合作關係，而且 PingAccess，hello 指示的某些存在 hello Ping 識別站台上。

### <a name="install-an-application-proxy-connector"></a>安裝應用程式 Proxy 連接器

如果您已經有應用程式 Proxy 已啟用，並已安裝的連接器，您可以略過本節並移過[加入您的應用程式 tooAzure 應用程式 Proxy 與 AD](#add-your-app-to-azure-ad-with-application-proxy)。

hello 應用程式 Proxy 連接器是 Windows Server 會將從遠端員工 tooyour hello 流量導向的服務發行的應用程式。 如需詳細的安裝指示，請參閱[hello Azure 入口網站中啟用應用程式 Proxy](active-directory-application-proxy-enable.md)。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)身為全域管理員。
2. 選取 **Azure Active Directory** > **應用程式 Proxy**。
3. 選取**下載連接器**toostart hello 應用程式 Proxy 連接器的下載。 請遵循 hello 安裝指示。

   ![啟用應用程式 Proxy 並下載 hello 連接器](./media/application-proxy-ping-access/install-connector.png)

4. 下載 hello connector 應該會自動會啟用您的目錄，但如果不是您可以選取的應用程式 Proxy**啟用應用程式 Proxy**。


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a>加入您的應用程式 tooAzure AD 應用程式 proxy

有兩個動作需要 tootake hello Azure 入口網站中。 首先，您需要 toopublish 應用程式 Proxy 的應用程式。 然後，您必須 toocollect hello 應用程式，可以在 hello PingAccess 步驟時使用的一些資訊。

請遵循這些步驟 toopublish 您的應用程式。 如需步驟 1-8 的更詳細逐步解說，請參閱[使用 Azure AD Application Proxy 發佈應用程式](application-proxy-publish-azure-portal.md)。

1. 如果未指定 hello 最後一節中，登入 toohello [Azure 入口網站](https://portal.azure.com)身為全域管理員。
2. 選取 [Azure Active Directory]  >  [企業應用程式]。
3. 選取**新增**在 hello hello 刀鋒視窗最上方。
4. 選取**內部部署應用程式**。
5. 填寫所需的 hello 欄位，新的應用程式的相關資訊。 使用下列指導方針 hello 設定 hello:
   - **內部 URL**： 您提供 hello URL，會帶領您 toohello 應用程式的簽署頁面中當你 hello 公司網路上的一般。 在此案例 hello 連接器會需要 tootreat hello PingAccess proxy 以 hello 前端 hello 應用程式頁面。 使用此格式︰`https://<host name of your PA server>:<port>`。 hello 通訊埠是 3000 根據預設，但您可以在 PingAccess 中進行設定。
   - **預先驗證方法**︰Azure Active Directory
   - **轉譯標頭中的 URL**：否

   >[!NOTE]
   >如果這是您的第一個應用程式，使用連接埠 3000 toostart 回來 tooupdate 這項設定如果您變更 PingAccess 組態。 如果這是您第二個或更新版本的應用程式，這需要 toomatch hello PingAccess 中設定接聽程式。 深入了解 [PingAccess 中的接聽程式](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html)。

6. 選取**新增**在 hello hello 刀鋒視窗的底部。 您的應用程式會加入，而且 hello 快速入門 功能表隨即開啟。
7. 在 [hello 快速入門] 功能表中選取**指派給使用者的測試**，新增至少一名使用者 toohello 應用程式。 請確定此測試帳戶具有存取 toohello 在內部部署應用程式。
8. 選取**指派**toosave hello 測試使用者指派。
9. 在 hello 應用程式管理刀鋒視窗中，選取 **單一登入**。
10. 選擇**標頭型登入**從 hello 下拉式選單。 選取 [ **儲存**]。

   >[!TIP]
   >如果這是您第一次使用標頭型單一登入，您會需要 tooinstall PingAccess。 toomake 確定您的 Azure 訂用帳戶會自動關聯於 PingAccess 安裝，此單一登入頁面 toodownload PingAccess 上使用 hello 連結。 您可以開啟 hello 下載網站，或 toothis 頁面稍後再回來。 

   ![選取標頭形式的登入](./media/application-proxy-ping-access/sso-header.PNG)

11. 關閉 hello 企業應用程式 刀鋒視窗，或捲動所有 hello 方式 toohello 左的 tooreturn toohello Azure Active Directory 功能表。
12. 選取 [應用程式註冊]。

   ![選取 [應用程式註冊]](./media/application-proxy-ping-access/app-registrations.png)

13. 您剛剛加入，然後選取 hello 應用程式**回覆 Url**。

   ![選取 [回覆 URL]](./media/application-proxy-ping-access/reply-urls.png)

14. 請檢查 toosee 如果 hello 外部 URL，您指派的 tooyour 應用程式在步驟 5 中 hello 回覆 Url 清單中。 如果不存在，請立即新增。
15. 在 hello 應用程式設定 刀鋒視窗，選取 **必要的權限**。

  ![選取 [必要權限]](./media/application-proxy-ping-access/required-permissions.png)

16. 選取 [新增] 。 Hello 應用程式開發介面中，選擇  **Windows Azure Active Directory**，然後**選取**。 Hello 權，請選擇**讀取和寫入所有的應用程式**和**登入並讀取使用者設定檔**，然後**選取**和**完成**。  

  ![選取權限](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a>收集 hello PingAccess 步驟的資訊

1. 在應用程式設定刀鋒視窗中，選取 [屬性]。 

  ![選取 [屬性]](./media/application-proxy-ping-access/properties.png)

2. 儲存 hello**應用程式識別碼**值。 當您設定 PingAccess 時，這用於 hello 用戶端識別碼。
3. 在 hello 應用程式設定 刀鋒視窗，選取 **金鑰**。

  ![選取 [金鑰]](./media/application-proxy-ping-access/Keys.png)

4. 輸入索引鍵的描述，然後從 hello 下拉功能表中選擇到期日建立金鑰。
5. 選取 [ **儲存**]。 GUID 會出現在 hello**值**欄位。

  儲存此值現在，當您將不會無法 toosee 它一次之後關閉此視窗。

  ![建立新的金鑰](./media/application-proxy-ping-access/create-keys.png)

6. 請關閉刀鋒視窗中的應用程式註冊 hello 或捲動所有 hello 方式 toohello 左的 tooreturn toohello Azure Active Directory 功能表。
7. 選取 [屬性] 。
8. 儲存 hello**目錄識別碼**GUID。

### <a name="optional---update-graphapi-toosend-custom-fields"></a>（選擇性） 更新 GraphAPI toosend 自訂欄位

如需 Azure AD 傳送以進行驗證的安全性權杖清單，請參閱 [Azure AD 權杖參考](./develop/active-directory-token-and-claims.md)。 如果您需要傳送其他語彙基元的自訂宣告，請使用 GraphAPI tooset hello 應用程式欄位*acceptMappedClaims*太**True**。 您可以使用 Azure AD Graph 總管或 MS 圖形 toomake 這項設定。 

此範例使用 Graph Explorer：

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a>下載 PingAccess 及設定您的應用程式

既然您已經完成所有 hello Azure Active Directory 的設定步驟，您可以移動 tooconfiguring PingAccess 上。 

hello hello PingAccess 屬於此案例的詳細的步驟繼續在 hello Ping 識別文件，[設定 Azure ad 的 PingAccess](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)。

這些步驟會引導您完成取得 PingAccess 帳戶，如果您還沒有其中一個、 安裝 hello PingAccess 伺服器及建立 Azure AD OIDC 提供者的連接以 hello 從 hello Azure 入口網站複製的目錄識別碼 hello 程序。 然後，您使用 PingAccess hello 應用程式識別碼和金鑰值 toocreate Web 工作階段。 之後，您可以設定身分識別對應，並建立虛擬主機、網站和應用程式。

### <a name="test-your-app"></a>測試應用程式

當您完成所有這些步驟時，您的應用程式應該啟動並執行。 tootest，開啟瀏覽器並瀏覽 toohello 您在 Azure 中發行 hello 應用程式時所建立的外部 URL。 使用登入 hello 測試帳戶，您指派的 toohello 應用程式。

## <a name="next-steps"></a>後續步驟

- [設定 Azure AD 的 PingAccess](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [Azure AD 應用程式 Proxy 如何提供單一登入？](application-proxy-sso-overview.md)
- [疑難排解應用程式 Proxy](active-directory-application-proxy-troubleshoot.md)

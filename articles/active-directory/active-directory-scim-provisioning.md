---
title: "aaaUsing 跨網域的識別管理的系統自動佈建使用者和群組從 Azure Active Directory tooapplications |Microsoft 文件"
description: "Azure Active Directory 會自動佈建使用者及群組 tooany 應用程式或身分識別存放區由 web 服務 fronted hello hello SCIM 通訊協定規格中定義的介面"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a>使用來自 Azure Active Directory tooapplications 跨網域身分識別管理 tooautomatically 佈建使用者和群組的系統

## <a name="overview"></a>概觀
Azure Active Directory (Azure AD) 可自動佈建使用者及群組 tooany 應用程式或身分識別存放區由 web 服務 fronted hello 介面定義中 hello[系統跨網域身分識別管理 (SCIM) 2.0通訊協定規格](https://tools.ietf.org/html/draft-ietf-scim-api-19)。 Azure Active Directory 可以傳送要求 toocreate、 修改或刪除指定的使用者和群組 toohello web 服務。 hello web 服務可以再將這些要求轉譯成 hello 目標身分識別存放區上的作業。 

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 



![][0]
*圖 1： 佈建 Azure Active Directory web 服務透過 tooan 身分識別存放區從*

這項功能可搭配 Azure AD tooenable 單一登入和自動使用者佈建來提供或為 fronted SCIM web 服務應用程式中的 hello 「 攜帶您自己的應用程式 」 功能。

在 Azure Active Directory 中使用 SCIM 有兩個使用案例：

* **佈建使用者及群組 tooapplications 支援 SCIM**支援 SCIM 2.0 和使用的驗證可搭配不需設定 Azure AD 的 OAuth 承載語彙基元的應用程式。
* **建置您自己的佈建解決方案針對支援其他應用程式開發介面為基礎的佈建應用程式**非 SCIM 應用程式，您可以建立 SCIM 端點 tootranslate hello Azure AD SCIM 端點之間任何 API hello 應用程式支援進行使用者佈建。 toohelp 開發 SCIM 端點，我們提供通用語言基礎結構 (CLI) 文件庫，以及程式碼範例會示範如何 toodo 提供 SCIM 端點，以及將 SCIM 訊息轉譯。  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a>佈建使用者及群組 tooapplications 支援 SCIM
Azure AD 可設定的 tooautomatically 指派的佈建使用者及群組 tooapplications 可實作[跨網域 2 (SCIM) 的身分識別管理系統](https://tools.ietf.org/html/draft-ietf-scim-api-19)web 服務，並接受驗證的 OAuth 承載語彙基元. Hello SCIM 2.0 規格中的應用程式必須符合下列需求：

* 建立使用者和/或群組，根據 3.3 節 hello SCIM 通訊協定的支援。  
* 修改使用者和/或群組與修補程式要求依照區段 3.5.2 hello SCIM 通訊協定的支援。  
* 擷取已知的資源，根據區段 3.4.1 hello SCIM 通訊協定的支援。  
* 查詢使用者和/或群組，依據區段 3.4.2 hello SCIM 通訊協定的支援。  依預設會依 externalId 來查詢使用者，並依 displayName 查詢群組。  
* 查詢使用者 ID 和由管理員根據區段 3.4.2 hello SCIM 通訊協定的支援。  
* 查詢群組 ID 和成員根據區段 3.4.2 hello SCIM 通訊協定的支援。  
* 接受授權 > 一節 2.1 根據 hello SCIM 通訊協定的 OAuth 承載語彙基元。

洽詢應用程式提供者，或參閱應用程式提供者文件中的相關陳述，以了解是否符合這些需求。

### <a name="getting-started"></a>開始使用
支援在本文中所述的 hello SCIM 設定檔的應用程式可連接的 tooAzure Active Directory 使用 hello Azure AD 應用程式庫中的 hello 「 非組件庫應用程式 」 功能。 一旦連線、 Azure AD 執行同步處理程序會用來查詢應用程式 hello SCIM 端點每隔 20 分鐘指派使用者和群組，並建立或修改它們根據 toohello 指派詳細資料。

**tooconnect 支援 SCIM 的應用程式：**

1. 登入太[hello Azure 入口網站](https://portal.azure.com)。 
2. 瀏覽過 * * Azure Active Directory > 企業應用程式，然後選取**新的應用程式 > 所有 > 非組件庫的應用程式**。
3. 輸入您的應用程式的名稱，然後按一下**新增**圖示 toocreate 應用程式物件。
    
  ![][1]
  圖 2：使用 Azure AD 應用程式庫
    
4. 在 hello 結果 畫面上，選取 hello**佈建**hello 左側資料行中的索引標籤。
5. 在 hello**佈建模式**功能表上，選取**自動**。
    
  ![][2]
  *圖 3： 設定 hello Azure 入口網站中佈建*
    
6. 在 hello**租用戶 URL**欄位中，輸入 hello hello 應用程式的 SCIM 端點 URL。 範例：https://api.contoso.com/scim/v2/
7. 如果 hello SCIM 端點需要簽發者以外的 Azure AD 中，從 OAuth 承載權杖，則複製 hello required OAuth 承載權杖到 hello 選擇性**密碼語彙基元**欄位。 如果此欄位保留空白，則 Azure AD 會在每個要求包含從 Azure AD 簽發的 OAuth 持有人權杖。 使用 Azure AD 作為識別提供者的應用程式，可以驗證此 Azure AD 簽發的權杖。
8. 按一下 hello**測試連接**按鈕 toohave Azure Active Directory 嘗試 tooconnect toohello SCIM 端點。 如果 hello 嘗試都失敗，則會顯示資訊時發生錯誤。  
9. 如果成功 hello 嘗試 tooconnect toohello 應用程式，然後按一下**儲存**toosave hello 系統管理員認證。
10. 在 hello**對應**區段中，有兩組可選取的屬性對應： 一個給使用者物件，一個群組物件。 選取同步處理每一個 tooreview hello 屬性從 Azure Active Directory tooyour 應用程式。 hello 做為所選取的屬性**比對**屬性是您的應用程式進行更新作業中使用的 toomatch hello 使用者和群組。 選取 hello 儲存按鈕 toocommit 任何變更。

    >[!NOTE]
    >您可以選擇性地停用正在同步處理群組物件的停用 hello 「 群組 」 對應。 

11. 在下**設定**，hello**範圍**欄位會定義哪些使用者或工作群組同步處理。 選取 「 同步處理只指派使用者和群組 （建議選項） 只會同步使用者和群組指派在 hello**使用者和群組** 索引標籤。
12. 您的設定完成之後，請變更 hello**佈建狀態**太**上**。
13. 按一下**儲存**toostart hello Azure AD 佈建服務。 
14. 如果同步處理只會指派使用者和群組 （建議選項），是確定 tooselect hello**使用者和群組**索引標籤上，並指派 hello 使用者和/或您想 toosync 的群組。

一旦啟動 hello 初始同步處理後，您可以使用 hello**稽核記錄檔**toomonitor 進度會顯示 hello 佈建應用程式上的服務所執行的所有動作索引標籤上。 如需有關 tooread hello Azure AD 佈建的記錄方式的詳細資訊，請參閱[報告使用者自動帳戶佈建](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。

>[!NOTE]
>hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。 


## <a name="building-your-own-provisioning-solution-for-any-application"></a>為任何應用程式建置您自己的佈建解決方案
建立可與 Azure Active Directory 互動的 SCIM Web 服務後，您即可為提供 REST 或 SOAP 使用者佈建 API 的絕大多數應用程式啟用單一登入和自動使用者佈建。

其運作方式如下：

1. Azure AD 提供名為 [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/)的通用語言基礎結構程式庫。 系統整合人員和開發人員可以使用此程式庫 toocreate 並部署 SCIM 為基礎的 web 服務端點連接的 Azure AD tooany 應用程式的身分識別存放區功能。
2. 對應會實作 hello web 服務 toomap hello 標準的使用者結構描述 toohello 使用者結構描述和 hello 應用程式所需的通訊協定。
3. hello 應用程式庫中的自訂應用程式一部分的 Azure AD 中註冊 hello 端點 URL。
4. 使用者和群組指派 toothis 應用程式在 Azure AD 中。 指派，時，它們被放入佇列進行同步處理的 toobe toohello 目標應用程式。 處理 hello 佇列 hello 同步處理程序執行每隔 20 分鐘。

### <a name="code-samples"></a>程式碼範例
toomake 此程序會更容易，一組[程式碼範例](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)會提供可建立 SCIM web 服務端點，並示範自動佈建。 其中一個範例是維護代表使用者和群組、具有逗號分隔值資料列檔案的提供者。  其他 hello 是 hello Amazon Web Services 識別和存取管理服務上運作的提供者。  

**必要條件**

* Visual Studio 2013 或更新版本
* [Azure SDK for .NET](https://azure.microsoft.com/downloads/)
* Hello SCIM 端點作為支援 hello ASP.NET framework 4.5 toobe 的 Windows 電腦。 此電腦必須能夠從 hello 雲端存取
* [具有 Azure AD Premium 試用版或授權版的 Azure 訂用帳戶](https://azure.microsoft.com/services/active-directory/)
* hello Amazon AWS 範例需要程式庫 hello [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html)。 如需詳細資訊，請參閱 hello 讀我檔案包含 hello 範例檔。

### <a name="getting-started"></a>開始使用
hello 可接受佈建 SCIM 端點會從 Azure AD 要求最簡單方式 tooimplement toobuild 並部署 hello 輸出 hello 佈建的使用者 tooa 逗點分隔值 (CSV) 檔案的程式碼範例。

**toocreate 範例 SCIM 端點：**

1. 下載 hello 程式碼範例套件[https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)
2. 解壓縮 hello 封裝，並將它放在您的 Windows 電腦，例如 C:\AzureAD-BYOA-Provisioning-Samples\ 位置上。
3. 在這個資料夾中，啟動 Visual Studio 中的 hello FileProvisioningAgent 方案。
4. 選取**工具 > 程式庫套件管理員 > Package Manager Console**，並執行下列命令 hello FileProvisioningAgent 專案 tooresolve hello 解決方案參考的 hello:
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. 建置 hello FileProvisioningAgent 專案。
6. Hello 命令提示字元中啟動應用程式視窗 （以系統管理員身分），並使用 hello **cd**命令 toochange hello 目錄 tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug**資料夾。
7. 執行下列命令，以 hello prb: hello Windows 電腦的發生 IP 位址或網域名稱取代 < 位址 > hello:
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. 在 Windows 下**Windows 設定 > 網路和網際網路設定**，選取 hello **Windows 防火牆 > 進階設定**，並建立**輸入規則**，允許對內的存取 tooport 9000。
9. 如果 hello Windows 電腦之路由器的後面，hello 路由器需求設定 toobe tooperform 網路存取轉譯其連接埠 9000 之間所公開的 toohello 網際網路及連接埠 9000 hello Windows 電腦上的。 這是必要的 Azure AD toobe 無法 tooaccess hello 雲端中的這個端點。

**tooregister hello 範例 SCIM 端點在 Azure AD 中：**

1. 登入太[hello Azure 入口網站](https://portal.azure.com)。 
2. 瀏覽過 * * Azure Active Directory > 企業應用程式，然後選取**新的應用程式 > 所有 > 非組件庫的應用程式**。
3. 輸入您的應用程式的名稱，然後按一下**新增**圖示 toocreate 應用程式物件。 建立 hello 應用程式物件是預定的 toorepresent hello 目標應用程式會提供 tooand 實作單一登入，並不只是 hello SCIM 端點。
4. 在 hello 結果 畫面上，選取 hello**佈建**hello 左側資料行中的索引標籤。
5. 在 hello**佈建模式**功能表上，選取**自動**。
    
  ![][2]
  *圖 4： 設定 hello Azure 入口網站中佈建*
    
6. 在 hello**租用戶 URL**欄位中，輸入 hello 網際網路公開的 URL 和連接埠 SCIM 端點。 這看起來應該像 http://testmachine.contoso.com:9000 或 http://<ip-address>:9000/，其中 < 位址 > 是 hello 網際網路公開 IP 位址。  
7. 如果 hello SCIM 端點需要簽發者以外的 Azure AD 中，從 OAuth 承載權杖，則複製 hello required OAuth 承載權杖到 hello 選擇性**密碼語彙基元**欄位。 如果此欄位保留空白，則 Azure AD 將在每個要求包含從 Azure AD 簽發的 OAuth 持有人權杖。 使用 Azure AD 作為識別提供者的應用程式，可以驗證此 Azure AD 簽發的權杖。
8. 按一下 hello**測試連接**按鈕 toohave Azure Active Directory 嘗試 tooconnect toohello SCIM 端點。 如果 hello 嘗試都失敗，則會顯示資訊時發生錯誤。  
9. 如果成功 hello 嘗試 tooconnect toohello 應用程式，然後按一下**儲存**toosave hello 系統管理員認證。
10. 在 hello**對應**區段中，有兩組可選取的屬性對應： 一個給使用者物件，一個群組物件。 選取同步處理每一個 tooreview hello 屬性從 Azure Active Directory tooyour 應用程式。 hello 做為所選取的屬性**比對**屬性是您的應用程式進行更新作業中使用的 toomatch hello 使用者和群組。 選取 hello 儲存按鈕 toocommit 任何變更。
11. 在下**設定**，hello**範圍**欄位會定義哪些使用者或工作群組同步處理。 選取 「 同步處理只指派使用者和群組 （建議選項） 只會同步使用者和群組指派在 hello**使用者和群組** 索引標籤。
12. 您的設定完成之後，請變更 hello**佈建狀態**太**上**。
13. 按一下**儲存**toostart hello Azure AD 佈建服務。 
14. 如果同步處理只會指派使用者和群組 （建議選項），是確定 tooselect hello**使用者和群組**索引標籤上，並指派 hello 使用者和/或您想 toosync 的群組。

一旦啟動 hello 初始同步處理後，您可以使用 hello**稽核記錄檔**toomonitor 進度會顯示 hello 佈建應用程式上的服務所執行的所有動作索引標籤上。 如需有關 tooread hello Azure AD 佈建的記錄方式的詳細資訊，請參閱[報告使用者自動帳戶佈建](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。

hello 驗證 hello 範例的最後一個步驟是 tooopen hello Windows 電腦上的 TargetFile.csv 檔 hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug 資料夾中。 一旦執行 hello 佈建程序時，此檔案會顯示 hello 詳細資料，所有的指派，並佈建使用者和群組。

### <a name="development-libraries"></a>開發程式庫
toodevelop 您自己的 web 服務，並符合 toohello SCIM 規格，先熟悉下列程式庫，提供由 Microsoft toohelp 加速 hello 開發程序的 hello: 

1. 提供通用語言基礎結構 (CLI) 程式庫，可與以該基礎結構為基礎的語言 (例如 C#) 搭配使用。 這些程式庫，其中[Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/)，宣告的介面，Microsoft.SystemForCrossDomainIdentityManagement.IProvider，hello 下列圖例所示： A使用 hello 程式庫的開發人員會實作該介面，也就是，一般提供者的類別。 hello 程式庫可讓 hello 開發人員 toodeploy 符合 toohello SCIM 規格的 web 服務。 hello web 服務可以被裝載在 Internet Information Services 或任何可執行的通用語言基礎結構組件。 要求會轉譯成呼叫 toohello 提供者的方法，會由 hello 某些身分識別存放區上的開發人員 toooperate 編寫程式。
  
  ![][3]
  
2. [Express 路由處理常式](http://expressjs.com/guide/routing.html)供剖析 node.js 要求物件，代表所呼叫 （它是由定義 hello SCIM 規格），的進行 tooa node.js web 服務。   

### <a name="building-a-custom-scim-endpoint"></a>建置自訂 SCIM 端點
使用 hello CLI 程式庫，使用這些程式庫的開發人員可以裝載任何可執行檔的通用語言基礎結構組件，或 Internet Information Services 中其服務。 以下是裝載在 hello 位址 http://localhost:9000 可執行組件內的服務範例程式碼： 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

此服務必須要有 HTTP 位址和伺服器驗證憑證的 hello 的根憑證授權單位是 hello 下列其中一種： 

* CNNIC
* Comodo
* CyberTrust
* DigiCert
* GeoTrust
* GlobalSign
* Go Daddy
* Verisign
* WoSign

伺服器驗證憑證可以是使用 hello 網路殼層公用程式的 Windows 主機上的繫結的 tooa 連接埠： 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

此處 hello 值提供給 hello certhash 引數都是 hello 憑證的指紋 hello，而 hello 值提供給 hello appid 引數是任意的全域唯一識別碼。  

toohost hello Internet Information Services 中的服務，開發人員會使用類別 hello hello 組件的預設命名空間中的啟動建置 CLA 程式碼程式庫組件。  以下是這種類別的範例： 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a>處理端點驗證
來自 Azure Active Directory 的要求包括 OAuth 2.0 持有人權杖。   任何服務接收 hello 要求應該驗證為 Azure Active Directory 代表 hello 必須是 Azure Active Directory 租用戶，如存取 toohello Azure Active Directory Graph web 服務的 hello 簽發者。  Hello 語彙基元，在 hello 簽發者由 iss 宣告，像是 「 iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/"。  在此範例中，基底位址 hello 宣告值 hello https://sts.windows.net，會識別 Azure Active Directory，為 hello 簽發者、 時 hello cbb1a5ac-f33b-45fa-9bf5-f37db0fed422，相對位址區段的唯一識別碼 hello Azure Active代表的 hello 發行權杖的目錄租用戶。  如果發行的存取 hello Azure Active Directory Graph web 服務，該服務，然後 hello 識別碼 hello 權杖 00000002-0000-0000-c000-000000000000，應該是 hello 語彙基元則 hello 值中宣告。  

使用由 Microsoft 提供的建置 SCIM 服務的 hello CLA 程式庫的開發人員可以驗證要求，從 Azure Active Directory 使用 hello Microsoft.Owin.Security.ActiveDirectory 套件，依照下列步驟： 

1. 提供者，讓它傳回 hello 服務啟動時呼叫方法 toobe 實作 hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior 屬性： 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. 加入下列程式碼 toothat 方法 toohave hello hello 服務端點為 bearing 代表指定的租用戶，存取 toohello Azure AD Graph web 服務的 Azure Active Directory 所發出的權杖進行驗證的任何要求 tooany: 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a>使用者和群組結構描述
Azure Active Directory 可以佈建兩種類型的資源 tooSCIM web 服務。  這些類型的資源是使用者和群組。  

使用者資源由識別碼所識別 hello 結構描述，urn: ietf:params:scim:schemas:extension:enterprise:2.0:User，隨附於此通訊協定規格： http://tools.ietf.org/html/draft-ietf-scim-core-schema。  資料表 1，底下提供 hello 預設對應的 hello 屬性的 urn: ietf:params:scim:schemas:extension:enterprise:2.0:User 資源的 Azure Active Directory toohello 屬性中的使用者。  

群組資源會 hello 結構描述識別碼識別，http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group。  資料表 2 的下方顯示 hello 預設對應的 Azure Active Directory toohello 屬性在資源群組的 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group 的 hello 屬性。  

### <a name="table-1-default-user-attribute-mapping"></a>表 1：預設使用者屬性對應
| Azure Active Directory 使用者 | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User |
| --- | --- |
| IsSoftDeleted |作用中 |
| displayName |displayName |
| Facsimile-TelephoneNumber |phoneNumbers[type eq "fax"].value |
| givenName |name.givenName |
| jobTitle |title |
| mail |emails[type eq "work"].value |
| mailNickname |externalId |
| manager |manager |
| mobile |phoneNumbers[type eq "mobile"].value |
| objectId |id |
| postalCode |addresses[type eq "work"].postalCode |
| proxy-Addresses |emails[type eq "other"].Value |
| physical-Delivery-OfficeName |addresses[type eq "other"].Formatted |
| streetAddress |addresses[type eq "work"].streetAddress |
| surname |name.familyName |
| telephone-Number |phoneNumbers[type eq "work"].value |
| user-PrincipalName |userName |

### <a name="table-2-default-group-attribute-mapping"></a>表 2：預設群組屬性對應
| Azure Active Directory 群組 | http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group |
| --- | --- |
| displayName |externalId |
| mail |emails[type eq "work"].value |
| mailNickname |displayName |
| members |members |
| objectId |id |
| proxyAddresses |emails[type eq "other"].Value |

## <a name="user-provisioning-and-de-provisioning"></a>使用者佈建和取消佈建
下列圖例顯示 hello 訊息，而 Azure Active Directory 會將 tooa SCIM 服務 toomanage hello 生命週期的使用者傳送另一個身分識別存放區中的 hello。 hello 圖表也會示範如何實作使用 hello CLI 程式庫的 SCIM 服務由 Microsoft 提供建置這類服務會將這些要求轉譯成提供者的呼叫 toohello 方法。  

![][4]
圖 5：使用者佈建和取消佈建順序

1. Azure Active Directory 查詢 hello 使用者的服務與 Azure AD 中的比對使用者的 hello mailNickname 屬性的值為 externalId 屬性值。 hello 查詢會以超文字傳輸通訊協定 (HTTP) 的要求，例如此範例中，其中 jyoung 是 Azure Active Directory 中使用者的郵件別名的範例： 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  如果使用實作 SCIM 服務由 Microsoft 提供的 hello 通用語言基礎結構程式庫來建置 hello 服務時，則 hello 要求時轉譯為呼叫 toohello hello 服務提供者的查詢方法。  以下是 hello 該方法的簽章： 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  以下是 hello hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters 介面定義： 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  在下列範例，具有給定值為 hello externalId 屬性查詢使用者的 hello，hello 傳遞 toohello 查詢方法的引數的值為： 
  * parameters.AlternateFilters.Count: 1
  * parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"
  * parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"
  * correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"] 

2. 如果 hello 回應 tooa 查詢 toohello web 服務的使用者具有 externalId 屬性值符合使用者的 hello mailNickname 屬性的值不會傳回任何使用者，Azure Active Directory 要求該 hello 服務佈建使用者對應 toohello 其中一個 Azure Active Directory 中。  以下是這類要求的範例： 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  hello 實作 SCIM 服務由 Microsoft 提供的通用語言基礎結構程式庫會將該要求轉譯成呼叫 toohello hello 服務提供者的建立方法。  Create 方法 hello 具有此簽章： 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  要求 tooprovision 使用者，在 hello hello 資源引數是 hello Microsoft.SystemForCrossDomainIdentityManagement 的執行個體。 Hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas 文件庫中定義的 Core2EnterpriseUser 類別。  如果 hello 要求 tooprovision hello 使用者成功，則 hello hello 方法的實作是預期的 tooreturn hello Microsoft.SystemForCrossDomainIdentityManagement 的執行個體。 Core2EnterpriseUser 類別，具有 hello 屬性值的 hello 識別碼設定 toohello hello 新佈建使用者的唯一識別碼。  

3. tooupdate 已知 tooexist fronted 由 SCIM，Azure Active Directory 會繼續進行這類要求 hello 服務要求 hello 目前狀態，該使用者的身分識別存放區中的使用者： 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  在服務中使用 hello 實作 SCIM 服務由 Microsoft 提供的通用語言基礎結構程式庫所建置，hello 要求會轉譯成呼叫 toohello hello 服務提供者的擷取方法。  以下是 hello hello 擷取方法簽章： 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  在 hello 範例中的使用者要求 tooretrieve hello 目前狀態，hello hello hello 物件提供給 hello hello 參數引數的值屬性的值如下： 
  
  * 識別碼："54D382A4-2050-4C03-94D1-E769F1D15682"
  * SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

4. 如果不論 hello hello 身分識別存放區中的 hello 參考屬性的目前值 fronted 所參考屬性 toobe 更新，然後 Azure Active Directory 查詢 hello 服務 toodetermine hello 服務就會與 hello 該屬性的值在 Azure Active Directory。 對於使用者而言 hello 的目前值會以這種方式查詢的唯一屬性是 hello 的 hello 經理屬性。 以下是要求 toodetermine 的範例，特定的使用者物件的 hello 經理屬性目前已為某個值是否： 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  hello 值 hello 屬性查詢參數的識別碼，表示如果使用者物件存在，可滿足 hello 運算式提供給 hello 值 hello 篩選查詢參數，則 hello 服務是預期的 urn: ietf:params:scim:schemas toorespond:核心： 2.0:User 或 urn: ietf:params:scim:schemas:extension:enterprise:2.0:User 資源，包括只有 hello 該資源的 id 屬性的值。  hello 值 hello**識別碼**已知 toohello 要求者的屬性。 它包含在 hello 值 hello 篩選查詢參數。hello 目的要求它是實際 toorequest 滿足 hello 篩選運算式，以表示有這類物件存在資源的最小表示法。   

  如果使用實作 SCIM 服務由 Microsoft 提供的 hello 通用語言基礎結構程式庫來建置 hello 服務時，則 hello 要求時轉譯為呼叫 toohello hello 服務提供者的查詢方法。 hello hello hello 物件提供給 hello hello 參數引數的值屬性的值如下所示： 
  
  * parameters.AlternateFilters.Count: 2
  * parameters.AlternateFilters.ElementAt(x).AttributePath: "id"
  * parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"
  * parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"
  * parameters.RequestedAttributePaths.ElementAt(0): "id"
  * parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

  在這裡，hello hello 索引 x 值可能是 0 和 hello hello 索引的 y 值可能是 1，或 hello x 值的值可能是 1 和 hello y 的值可能是 0，hello hello filter 查詢參數運算式中的 hello 順序而定。   

5. 從 Azure Active Directory tooan SCIM 服務 tooupdate 使用者要求的範例如下： 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  hello Microsoft 通用語言基礎結構程式庫實作 SCIM 服務會將 hello 要求轉譯成呼叫 toohello hello 服務提供者的更新方法。 以下是 hello hello Update 方法簽章： 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    在 hello 範例中的要求 tooupdate 使用者，提供給 hello 修補程式引數的 hello 值 hello 物件會具有這些屬性值： 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
  * (PatchRequest as PatchRequest2).Operations.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646

6. toode 佈建的使用者身分識別存放區 fronted SCIM 服務，例如 Azure AD 傳送的要求： 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  如果使用實作 SCIM 服務由 Microsoft 提供的 hello 通用語言基礎結構程式庫來建置 hello 服務時，則 hello 要求時轉譯為呼叫 toohello hello 服務提供者的 Delete 方法。   該方法具有此簽章： 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  hello 物件提供給 hello hello resourceIdentifier 引數的值具有這些屬性值在 hello 範例中的要求 toode 佈建使用者： 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

## <a name="group-provisioning-and-de-provisioning"></a>群組佈建和取消佈建
下列圖例顯示 hello 訊息，而 Azure AcD 傳送 tooa SCIM 服務 toomanage hello 生命週期的群組，另一個身分識別存放區中的 hello。  這些郵件差異 hello 訊息相關 toousers 三種方式： 

* hello 結構描述的群組資源會被視為 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group。  
* Tooretrieve 群組中保證該 hello 成員屬性的要求是 toobe 排除回應 toohello 要求中提供的任何資源。  
* 要求 toodetermine 參考屬性是否具有特定值，會要求有關 hello 成員屬性。  

![][5]
圖 6：群組佈建和取消佈建順序

## <a name="related-articles"></a>相關文章
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [自動化使用者佈建/取消佈建 tooSaaS 應用程式](active-directory-saas-app-provisioning.md)
* [自訂使用者佈建的屬性對應](active-directory-saas-customizing-attribute-mappings.md)
* [撰寫屬性對應的運算式](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [適用於使用者佈建的範圍篩選器](active-directory-saas-scoping-filters.md)
* [帳戶佈建通知](active-directory-saas-account-provisioning-notifications.md)
* [如何教學課程清單 tooIntegrate SaaS 應用程式](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG

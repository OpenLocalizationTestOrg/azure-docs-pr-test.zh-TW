---
title: "Azure AD 驗證 tooaccess 與.NET 的 Azure 媒體服務 API aaaUse |Microsoft 文件"
description: "本主題說明如何 toouse Azure Active Directory (Azure AD) 驗證 tooaccess Azure 媒體服務 (AMS) 中.NET API。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a>使用 Azure AD 驗證 tooaccess Azure Media Services API 的.NET

從 windowsazure.mediaservices 4.0.0.4 開始，Azure 媒體服務支援以 Azure Active Directory (Azure AD) 為主的驗證。 本主題說明如何 toouse Azure AD 驗證 tooaccess 與 Microsoft.NET 的 Azure 媒體服務 API。

## <a name="prerequisites"></a>必要條件

- 一個 Azure 帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 
- 媒體服務帳戶。 如需詳細資訊，請參閱[建立 Azure 媒體服務帳戶使用 Azure 入口網站 hello](media-services-portal-create-account.md)。
- 最新 hello [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices)封裝。
- 熟悉 hello 主題[存取 Azure 媒體服務應用程式開發介面使用 AAD 驗證概觀](media-services-use-aad-auth-to-access-ams-api.md)。 

使用 Azure AD 驗證搭配 Azure 媒體服務時，您可以下列其中一種方式進行驗證：

- **使用者驗證**驗證使用 hello 應用程式 toointeract 和 Azure Media Services 資源的人員。 hello 互動式應用程式應該會先提示 hello 使用者提供認證。 例如，授權的使用者 toomonitor 編碼工作會使用或即時資料流中的管理主控台應用程式。 
- **服務主體驗證**會驗證服務。 通常使用這種驗證方法的應用程式有執行精靈服務、中介層服務或排程的工作的應用程式：例如，Web 應用程式、函數應用程式、邏輯應用程式、API 或微服務。

>[!IMPORTANT]
>Azure 媒體服務目前支援 Azure 存取控制服務驗證模型。 不過，存取控制授權即將 toobe 上 2018 年 6 月 1，已被取代。 我們建議您儘速移轉 tooan Azure Active Directory 驗證模型。

## <a name="get-an-azure-ad-access-token"></a>取得 Azure AD 存取權杖

tooconnect toohello Azure 媒體服務 API 與 Azure AD 驗證，hello 用戶端應用程式需要 toorequest Azure AD 存取權杖。 當您使用 Media Services.NET 用戶端 hello SDK hello 和詳細資料如何 tooacquire Azure AD 存取權杖會包裝在 hello 簡化您的許多[AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs)和[AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs)類別。 

例如，您不需要 tooprovide hello Azure AD 授權單位、 Media Services 資源的 URI 或原生 Azure AD 應用程式詳細資料。 這些是已知的 hello Azure AD 存取權杖提供者類別已設定的值。 

如果您未使用 Azure 媒體服務.NET SDK，我們建議您使用 hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md)。 請參閱 hello 參數，您需要與 Azure AD 驗證程式庫 toouse tooget 值[使用 hello Azure 入口網站 tooaccess Azure AD 驗證設定](media-services-portal-get-started-with-aad.md)。

您也可以取代 hello hello 預設實作的 hello 選項**AzureAdTokenProvider**與您自己的實作。

## <a name="install-and-configure-azure-media-services-net-sdk"></a>安裝及設定 Azure 媒體服務 .NET SDK

>[!NOTE] 
>以 Media Services.NET SDK hello toouse Azure AD 驗證，您需要 toohave hello 最新[NuGet](https://www.nuget.org/packages/windowsazure.mediaservices)封裝。 此外，請加入參考 toohello **Microsoft.IdentityModel.Clients.ActiveDirectory**組件。 如果您使用現有的應用程式，包括 hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll**組件。 

1. 在 Visual Studio 中，建立新的 C# 主控台應用程式。
2. 使用 hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet 封裝 tooinstall **Azure Media Services.NET SDK**。 

    使用 NuGet，tooadd 參考採取下列步驟的 hello： 在**方案總管 中**，hello 專案名稱，以滑鼠右鍵按一下，然後選取**管理 NuGet 封裝**。 接著，搜尋 **windowsazure.mediaservices**，然後選取 [安裝]。
    
    -或-

    執行 hello 下列中的命令**Package Manager Console** Visual Studio 中。

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. 新增**使用**tooyour 原始程式碼。

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a>使用使用者驗證

tooconnect toohello Azure 媒體服務 API 與 hello 使用者驗證選項，hello 用戶端應用程式需要的 toorequest 使用 Azure AD 權杖 hello 下列參數：  

- Azure AD 租用戶端點。 hello 租用戶資訊可以擷取從 hello Azure 入口網站。 將滑鼠停留在 hello 登入的使用者在 hello 右上角。
- 媒體服務資源 URI。
- 媒體服務 (原生) 應用程式用戶端識別碼。 
- 媒體服務 (原生) 應用程式重新導向 URI。 

這些參數的 hello 值位於**AzureEnvironments.AzureCloudEnvironment**。 hello **AzureEnvironments.AzureCloudEnvironment**常數是 helper hello.NET SDK tooget 中的公開的 Azure 資料中心的 hello 正確的環境變數設定值。 

它包含預先定義的環境設定存取 Media Services 在 hello 公用資料中心內。 對於 sovereign 或政府雲端區域，分別可以使用 **AzureChinaCloudEnvironment****AzureUsGovernmentEnvrionment** 或 **AzureGermanCloudEnvironment**。

下列程式碼範例的 hello 建立語彙基元：
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
toostart 針對媒體服務進行程式設計，您需要 toocreate **CloudMediaContext**代表 hello 伺服器內容的執行個體。 hello **CloudMediaContext**包含參考 tooimportant 集合，包括工作、 資產、 檔案、 存取原則和定位器。 

您也需要 toopass hello**資源的媒體服務 REST 服務的 URI** toohello **CloudMediaContext**建構函式。 tooget hello 資源 URI 媒體 REST 服務，登入 toohello Azure 入口網站中，選取您的 Azure Media Services 帳戶選取**API 存取**，然後選取**連接 tooAzure Media Services 與使用者驗證**。 

hello 下列程式碼範例會建立**CloudMediaContext**執行個體：

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

hello 下列範例顯示如何 toocreate hello Azure AD 權杖和 hello 內容：

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
>如果您收到例外狀況指出"hello 遠端伺服器傳回錯誤: (401) 未授權，「 請參閱 hello[存取控制](media-services-use-aad-auth-to-access-ams-api.md#access-control)存取 Azure Media Services API 的區段與 Azure AD 驗證的概觀。

## <a name="use-service-principal-authentication"></a>使用服務主體驗證
    
與 hello 服務主體選項 tooconnect toohello Azure Media Services API 中, 介層應用程式 （web API 或 web 應用程式） 需要 toorequests Azure AD 權杖以 hello 下列參數：  

- Azure AD 租用戶端點。 hello 租用戶資訊可以擷取從 hello Azure 入口網站。 將滑鼠停留在 hello 登入的使用者在 hello 右上角。
- 媒體服務資源 URI。
- Azure AD 應用程式的值： hello**用戶端識別碼**和**用戶端密碼**。

hello 值 hello**用戶端識別碼**和**用戶端密碼**參數可以在 hello Azure 入口網站中找到。 如需詳細資訊，請參閱[開始使用 Azure AD 驗證使用 hello Azure 入口網站](media-services-portal-get-started-with-aad.md)。

hello 下列程式碼範例會建立語彙基元使用 hello **AzureAdTokenCredentials**建構函式**AzureAdClientSymmetricKey**做為參數： 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

您也可以指定 hello **AzureAdTokenCredentials**建構函式**AzureAdClientCertificate**做為參數。 

如需有關如何指示 toocreate 及設定憑證的形式，可由 Azure AD，請參閱[驗證與憑證-手動組態步驟的精靈應用程式中的 AD tooAzure](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md)。

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

toostart 針對媒體服務進行程式設計，您需要 toocreate **CloudMediaContext**代表 hello 伺服器內容的執行個體。 您也需要 toopass hello**資源的媒體服務 REST 服務的 URI** toohello **CloudMediaContext**建構函式。 您可以取得 hello**資源的媒體服務 REST 服務的 URI** hello Azure 的入口網站中的值。

hello 下列程式碼範例會建立**CloudMediaContext**執行個體：

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
hello 下列範例顯示如何 toocreate hello Azure AD 權杖和 hello 內容：

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a>後續步驟

開始使用[上傳檔案 tooyour 帳戶](media-services-dotnet-upload-files.md)。

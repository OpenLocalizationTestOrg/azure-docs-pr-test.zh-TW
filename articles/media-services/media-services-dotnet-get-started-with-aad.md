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
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a><span data-ttu-id="b06d3-103">使用 Azure AD 驗證 tooaccess Azure Media Services API 的.NET</span><span class="sxs-lookup"><span data-stu-id="b06d3-103">Use Azure AD authentication tooaccess Azure Media Services API with .NET</span></span>

<span data-ttu-id="b06d3-104">從 windowsazure.mediaservices 4.0.0.4 開始，Azure 媒體服務支援以 Azure Active Directory (Azure AD) 為主的驗證。</span><span class="sxs-lookup"><span data-stu-id="b06d3-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="b06d3-105">本主題說明如何 toouse Azure AD 驗證 tooaccess 與 Microsoft.NET 的 Azure 媒體服務 API。</span><span class="sxs-lookup"><span data-stu-id="b06d3-105">This topic shows you how toouse Azure AD  authentication tooaccess Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b06d3-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="b06d3-106">Prerequisites</span></span>

- <span data-ttu-id="b06d3-107">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b06d3-107">An Azure account.</span></span> <span data-ttu-id="b06d3-108">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b06d3-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="b06d3-109">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="b06d3-109">A Media Services account.</span></span> <span data-ttu-id="b06d3-110">如需詳細資訊，請參閱[建立 Azure 媒體服務帳戶使用 Azure 入口網站 hello](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="b06d3-110">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="b06d3-111">最新 hello [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices)封裝。</span><span class="sxs-lookup"><span data-stu-id="b06d3-111">hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="b06d3-112">熟悉 hello 主題[存取 Azure 媒體服務應用程式開發介面使用 AAD 驗證概觀](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="b06d3-112">Familiarity with hello topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="b06d3-113">使用 Azure AD 驗證搭配 Azure 媒體服務時，您可以下列其中一種方式進行驗證：</span><span class="sxs-lookup"><span data-stu-id="b06d3-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="b06d3-114">**使用者驗證**驗證使用 hello 應用程式 toointeract 和 Azure Media Services 資源的人員。</span><span class="sxs-lookup"><span data-stu-id="b06d3-114">**User authentication** authenticates a person who is using hello app toointeract with Azure Media Services resources.</span></span> <span data-ttu-id="b06d3-115">hello 互動式應用程式應該會先提示 hello 使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="b06d3-115">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="b06d3-116">例如，授權的使用者 toomonitor 編碼工作會使用或即時資料流中的管理主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b06d3-116">An example is a management console app that's used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="b06d3-117">**服務主體驗證**會驗證服務。</span><span class="sxs-lookup"><span data-stu-id="b06d3-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="b06d3-118">通常使用這種驗證方法的應用程式有執行精靈服務、中介層服務或排程的工作的應用程式：例如，Web 應用程式、函數應用程式、邏輯應用程式、API 或微服務。</span><span class="sxs-lookup"><span data-stu-id="b06d3-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b06d3-119">Azure 媒體服務目前支援 Azure 存取控制服務驗證模型。</span><span class="sxs-lookup"><span data-stu-id="b06d3-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="b06d3-120">不過，存取控制授權即將 toobe 上 2018 年 6 月 1，已被取代。</span><span class="sxs-lookup"><span data-stu-id="b06d3-120">However, Access Control authorization is going toobe deprecated on June 1, 2018.</span></span> <span data-ttu-id="b06d3-121">我們建議您儘速移轉 tooan Azure Active Directory 驗證模型。</span><span class="sxs-lookup"><span data-stu-id="b06d3-121">We recommend that you migrate tooan Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="b06d3-122">取得 Azure AD 存取權杖</span><span class="sxs-lookup"><span data-stu-id="b06d3-122">Get an Azure AD access token</span></span>

<span data-ttu-id="b06d3-123">tooconnect toohello Azure 媒體服務 API 與 Azure AD 驗證，hello 用戶端應用程式需要 toorequest Azure AD 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="b06d3-123">tooconnect toohello Azure Media Services API with Azure AD authentication, hello client app needs toorequest an Azure AD access token.</span></span> <span data-ttu-id="b06d3-124">當您使用 Media Services.NET 用戶端 hello SDK hello 和詳細資料如何 tooacquire Azure AD 存取權杖會包裝在 hello 簡化您的許多[AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs)和[AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs)類別。</span><span class="sxs-lookup"><span data-stu-id="b06d3-124">When you use hello Media Services .NET client SDK, many of hello details about how tooacquire an Azure AD access token are wrapped and simplified for you in hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="b06d3-125">例如，您不需要 tooprovide hello Azure AD 授權單位、 Media Services 資源的 URI 或原生 Azure AD 應用程式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b06d3-125">For example, you don't need tooprovide hello Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="b06d3-126">這些是已知的 hello Azure AD 存取權杖提供者類別已設定的值。</span><span class="sxs-lookup"><span data-stu-id="b06d3-126">These are well-known values that are already configured by hello Azure AD access token provider class.</span></span> 

<span data-ttu-id="b06d3-127">如果您未使用 Azure 媒體服務.NET SDK，我們建議您使用 hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="b06d3-127">If you are not using Azure Media Service .NET SDK, we recommend that you use hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="b06d3-128">請參閱 hello 參數，您需要與 Azure AD 驗證程式庫 toouse tooget 值[使用 hello Azure 入口網站 tooaccess Azure AD 驗證設定](media-services-portal-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="b06d3-128">tooget values for hello parameters that you need toouse with Azure AD Authentication Library, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="b06d3-129">您也可以取代 hello hello 預設實作的 hello 選項**AzureAdTokenProvider**與您自己的實作。</span><span class="sxs-lookup"><span data-stu-id="b06d3-129">You also have hello option of replacing hello default implementation of hello **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="b06d3-130">安裝及設定 Azure 媒體服務 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b06d3-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="b06d3-131">以 Media Services.NET SDK hello toouse Azure AD 驗證，您需要 toohave hello 最新[NuGet](https://www.nuget.org/packages/windowsazure.mediaservices)封裝。</span><span class="sxs-lookup"><span data-stu-id="b06d3-131">toouse Azure AD authentication with hello Media Services .NET SDK, you need toohave hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="b06d3-132">此外，請加入參考 toohello **Microsoft.IdentityModel.Clients.ActiveDirectory**組件。</span><span class="sxs-lookup"><span data-stu-id="b06d3-132">Also, add a reference toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="b06d3-133">如果您使用現有的應用程式，包括 hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll**組件。</span><span class="sxs-lookup"><span data-stu-id="b06d3-133">If you are using an existing app, include hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="b06d3-134">在 Visual Studio 中，建立新的 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b06d3-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="b06d3-135">使用 hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet 封裝 tooinstall **Azure Media Services.NET SDK**。</span><span class="sxs-lookup"><span data-stu-id="b06d3-135">Use hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package tooinstall **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="b06d3-136">使用 NuGet，tooadd 參考採取下列步驟的 hello： 在**方案總管 中**，hello 專案名稱，以滑鼠右鍵按一下，然後選取**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="b06d3-136">tooadd references by using NuGet, take hello following steps: in **Solution Explorer**, right-click hello project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="b06d3-137">接著，搜尋 **windowsazure.mediaservices**，然後選取 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="b06d3-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="b06d3-138">-或-</span><span class="sxs-lookup"><span data-stu-id="b06d3-138">-or-</span></span>

    <span data-ttu-id="b06d3-139">執行 hello 下列中的命令**Package Manager Console** Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="b06d3-139">Run hello following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="b06d3-140">新增**使用**tooyour 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="b06d3-140">Add **using** tooyour source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="b06d3-141">使用使用者驗證</span><span class="sxs-lookup"><span data-stu-id="b06d3-141">Use user authentication</span></span>

<span data-ttu-id="b06d3-142">tooconnect toohello Azure 媒體服務 API 與 hello 使用者驗證選項，hello 用戶端應用程式需要的 toorequest 使用 Azure AD 權杖 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="b06d3-142">tooconnect toohello Azure Media Service API with hello user authentication option, hello client app needs toorequest an Azure AD token by using hello following parameters:</span></span>  

- <span data-ttu-id="b06d3-143">Azure AD 租用戶端點。</span><span class="sxs-lookup"><span data-stu-id="b06d3-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="b06d3-144">hello 租用戶資訊可以擷取從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b06d3-144">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="b06d3-145">將滑鼠停留在 hello 登入的使用者在 hello 右上角。</span><span class="sxs-lookup"><span data-stu-id="b06d3-145">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="b06d3-146">媒體服務資源 URI。</span><span class="sxs-lookup"><span data-stu-id="b06d3-146">Media Services resource URI.</span></span>
- <span data-ttu-id="b06d3-147">媒體服務 (原生) 應用程式用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="b06d3-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="b06d3-148">媒體服務 (原生) 應用程式重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="b06d3-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="b06d3-149">這些參數的 hello 值位於**AzureEnvironments.AzureCloudEnvironment**。</span><span class="sxs-lookup"><span data-stu-id="b06d3-149">hello values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="b06d3-150">hello **AzureEnvironments.AzureCloudEnvironment**常數是 helper hello.NET SDK tooget 中的公開的 Azure 資料中心的 hello 正確的環境變數設定值。</span><span class="sxs-lookup"><span data-stu-id="b06d3-150">hello **AzureEnvironments.AzureCloudEnvironment** constant is a helper in hello .NET SDK tooget hello right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="b06d3-151">它包含預先定義的環境設定存取 Media Services 在 hello 公用資料中心內。</span><span class="sxs-lookup"><span data-stu-id="b06d3-151">It contains pre-defined environment settings for accessing Media Services in hello public data centers only.</span></span> <span data-ttu-id="b06d3-152">對於 sovereign 或政府雲端區域，分別可以使用 **AzureChinaCloudEnvironment****AzureUsGovernmentEnvrionment** 或 **AzureGermanCloudEnvironment**。</span><span class="sxs-lookup"><span data-stu-id="b06d3-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="b06d3-153">下列程式碼範例的 hello 建立語彙基元：</span><span class="sxs-lookup"><span data-stu-id="b06d3-153">hello following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="b06d3-154">toostart 針對媒體服務進行程式設計，您需要 toocreate **CloudMediaContext**代表 hello 伺服器內容的執行個體。</span><span class="sxs-lookup"><span data-stu-id="b06d3-154">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="b06d3-155">hello **CloudMediaContext**包含參考 tooimportant 集合，包括工作、 資產、 檔案、 存取原則和定位器。</span><span class="sxs-lookup"><span data-stu-id="b06d3-155">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="b06d3-156">您也需要 toopass hello**資源的媒體服務 REST 服務的 URI** toohello **CloudMediaContext**建構函式。</span><span class="sxs-lookup"><span data-stu-id="b06d3-156">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="b06d3-157">tooget hello 資源 URI 媒體 REST 服務，登入 toohello Azure 入口網站中，選取您的 Azure Media Services 帳戶選取**API 存取**，然後選取**連接 tooAzure Media Services 與使用者驗證**。</span><span class="sxs-lookup"><span data-stu-id="b06d3-157">tooget hello resource URI for Media REST Services, sign in toohello Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect tooAzure Media Services with user authentication**.</span></span> 

<span data-ttu-id="b06d3-158">hello 下列程式碼範例會建立**CloudMediaContext**執行個體：</span><span class="sxs-lookup"><span data-stu-id="b06d3-158">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="b06d3-159">hello 下列範例顯示如何 toocreate hello Azure AD 權杖和 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="b06d3-159">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

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
><span data-ttu-id="b06d3-160">如果您收到例外狀況指出"hello 遠端伺服器傳回錯誤: (401) 未授權，「 請參閱 hello[存取控制](media-services-use-aad-auth-to-access-ams-api.md#access-control)存取 Azure Media Services API 的區段與 Azure AD 驗證的概觀。</span><span class="sxs-lookup"><span data-stu-id="b06d3-160">If you get an exception that says "hello remote server returned an error: (401) Unauthorized," see hello [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="b06d3-161">使用服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="b06d3-161">Use service principal authentication</span></span>
    
<span data-ttu-id="b06d3-162">與 hello 服務主體選項 tooconnect toohello Azure Media Services API 中, 介層應用程式 （web API 或 web 應用程式） 需要 toorequests Azure AD 權杖以 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="b06d3-162">tooconnect toohello Azure Media Services API with hello service principal option, your middle-tier app (web API or web application) needs toorequests an Azure AD token with hello following parameters:</span></span>  

- <span data-ttu-id="b06d3-163">Azure AD 租用戶端點。</span><span class="sxs-lookup"><span data-stu-id="b06d3-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="b06d3-164">hello 租用戶資訊可以擷取從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b06d3-164">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="b06d3-165">將滑鼠停留在 hello 登入的使用者在 hello 右上角。</span><span class="sxs-lookup"><span data-stu-id="b06d3-165">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="b06d3-166">媒體服務資源 URI。</span><span class="sxs-lookup"><span data-stu-id="b06d3-166">Media Services resource URI.</span></span>
- <span data-ttu-id="b06d3-167">Azure AD 應用程式的值： hello**用戶端識別碼**和**用戶端密碼**。</span><span class="sxs-lookup"><span data-stu-id="b06d3-167">Azure AD application values: hello **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="b06d3-168">hello 值 hello**用戶端識別碼**和**用戶端密碼**參數可以在 hello Azure 入口網站中找到。</span><span class="sxs-lookup"><span data-stu-id="b06d3-168">hello values for hello **Client ID** and **Client secret** parameters can be found in hello Azure portal.</span></span> <span data-ttu-id="b06d3-169">如需詳細資訊，請參閱[開始使用 Azure AD 驗證使用 hello Azure 入口網站](media-services-portal-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="b06d3-169">For more information, see [Getting started with Azure AD authentication using hello Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="b06d3-170">hello 下列程式碼範例會建立語彙基元使用 hello **AzureAdTokenCredentials**建構函式**AzureAdClientSymmetricKey**做為參數：</span><span class="sxs-lookup"><span data-stu-id="b06d3-170">hello following code example creates a token by using hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="b06d3-171">您也可以指定 hello **AzureAdTokenCredentials**建構函式**AzureAdClientCertificate**做為參數。</span><span class="sxs-lookup"><span data-stu-id="b06d3-171">You can also specify hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="b06d3-172">如需有關如何指示 toocreate 及設定憑證的形式，可由 Azure AD，請參閱[驗證與憑證-手動組態步驟的精靈應用程式中的 AD tooAzure](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md)。</span><span class="sxs-lookup"><span data-stu-id="b06d3-172">For instructions about how toocreate and configure a certificate in a form that can be used by Azure AD, see [Authenticating tooAzure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="b06d3-173">toostart 針對媒體服務進行程式設計，您需要 toocreate **CloudMediaContext**代表 hello 伺服器內容的執行個體。</span><span class="sxs-lookup"><span data-stu-id="b06d3-173">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="b06d3-174">您也需要 toopass hello**資源的媒體服務 REST 服務的 URI** toohello **CloudMediaContext**建構函式。</span><span class="sxs-lookup"><span data-stu-id="b06d3-174">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="b06d3-175">您可以取得 hello**資源的媒體服務 REST 服務的 URI** hello Azure 的入口網站中的值。</span><span class="sxs-lookup"><span data-stu-id="b06d3-175">You can get hello **resource URI for Media REST Services** value from hello Azure portal as well.</span></span>

<span data-ttu-id="b06d3-176">hello 下列程式碼範例會建立**CloudMediaContext**執行個體：</span><span class="sxs-lookup"><span data-stu-id="b06d3-176">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="b06d3-177">hello 下列範例顯示如何 toocreate hello Azure AD 權杖和 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="b06d3-177">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b06d3-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b06d3-178">Next steps</span></span>

<span data-ttu-id="b06d3-179">開始使用[上傳檔案 tooyour 帳戶](media-services-dotnet-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="b06d3-179">Get started with [uploading files tooyour account](media-services-dotnet-upload-files.md).</span></span>

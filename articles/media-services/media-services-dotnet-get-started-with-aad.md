---
title: "使用 Azure AD 驗證搭配 .NET 存取 Azure 媒體服務 API | Microsoft Docs"
description: "本主題說明如何使用 Azure Active Directory (Azure AD) 驗證搭配 .NET 存取 Azure 媒體服務 (AMS) API。"
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
ms.openlocfilehash: a9355200a05a3aa1b494b76977d38ddc42bfe179
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-ad-authentication-to-access-azure-media-services-api-with-net"></a><span data-ttu-id="ac52a-103">使用 Azure AD 驗證搭配 .NET 存取 Azure 媒體服務 API</span><span class="sxs-lookup"><span data-stu-id="ac52a-103">Use Azure AD authentication to access Azure Media Services API with .NET</span></span>

<span data-ttu-id="ac52a-104">從 windowsazure.mediaservices 4.0.0.4 開始，Azure 媒體服務支援以 Azure Active Directory (Azure AD) 為主的驗證。</span><span class="sxs-lookup"><span data-stu-id="ac52a-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ac52a-105">本主題說明如何使用 Azure AD 驗證搭配 Microsoft .NET 存取 Azure 媒體服務 API。</span><span class="sxs-lookup"><span data-stu-id="ac52a-105">This topic shows you how to use Azure AD  authentication to access Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac52a-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="ac52a-106">Prerequisites</span></span>

- <span data-ttu-id="ac52a-107">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac52a-107">An Azure account.</span></span> <span data-ttu-id="ac52a-108">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ac52a-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="ac52a-109">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac52a-109">A Media Services account.</span></span> <span data-ttu-id="ac52a-110">如需詳細資訊，請參閱[使用 Azure 入口網站建立 Azure 媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="ac52a-110">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="ac52a-111">最新的 [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) 封裝。</span><span class="sxs-lookup"><span data-stu-id="ac52a-111">The latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="ac52a-112">熟讀[使用 AAD 驗證存取 Azure 媒體服務 API 概觀](media-services-use-aad-auth-to-access-ams-api.md)主題。</span><span class="sxs-lookup"><span data-stu-id="ac52a-112">Familiarity with the topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="ac52a-113">使用 Azure AD 驗證搭配 Azure 媒體服務時，您可以下列其中一種方式進行驗證：</span><span class="sxs-lookup"><span data-stu-id="ac52a-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="ac52a-114">**使用者驗證**可驗證使用應用程式與 Azure 媒體服務資源互動的人員。</span><span class="sxs-lookup"><span data-stu-id="ac52a-114">**User authentication** authenticates a person who is using the app to interact with Azure Media Services resources.</span></span> <span data-ttu-id="ac52a-115">互動式應用程式應該會先提示使用者輸入認證。</span><span class="sxs-lookup"><span data-stu-id="ac52a-115">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="ac52a-116">例如，授權的使用者用來監控編碼工作或即時串流的管理主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac52a-116">An example is a management console app that's used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="ac52a-117">**服務主體驗證**會驗證服務。</span><span class="sxs-lookup"><span data-stu-id="ac52a-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="ac52a-118">通常使用這種驗證方法的應用程式有執行精靈服務、中介層服務或排程的工作的應用程式：例如，Web 應用程式、函數應用程式、邏輯應用程式、API 或微服務。</span><span class="sxs-lookup"><span data-stu-id="ac52a-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="ac52a-119">Azure 媒體服務目前支援 Azure 存取控制服務驗證模型。</span><span class="sxs-lookup"><span data-stu-id="ac52a-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="ac52a-120">不過，存取控制授權將在 2018 年 6 月 1 日被取代。</span><span class="sxs-lookup"><span data-stu-id="ac52a-120">However, Access Control authorization is going to be deprecated on June 1, 2018.</span></span> <span data-ttu-id="ac52a-121">建議您儘速移轉至 Azure Active Directory 驗證模型。</span><span class="sxs-lookup"><span data-stu-id="ac52a-121">We recommend that you migrate to an Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="ac52a-122">取得 Azure AD 存取權杖</span><span class="sxs-lookup"><span data-stu-id="ac52a-122">Get an Azure AD access token</span></span>

<span data-ttu-id="ac52a-123">若要使用 Azure AD 驗證連線到 Azure 媒體服務 API，用戶端應用程式必須要求 Azure AD 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="ac52a-123">To connect to the Azure Media Services API with Azure AD authentication, the client app needs to request an Azure AD access token.</span></span> <span data-ttu-id="ac52a-124">當您使用媒體服務 .NET 用戶端 SDK 時，許多有關如何取得 Azure AD 存取權杖的詳細資料已為您包裝並簡化於 [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) 和 [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) 類別中。</span><span class="sxs-lookup"><span data-stu-id="ac52a-124">When you use the Media Services .NET client SDK, many of the details about how to acquire an Azure AD access token are wrapped and simplified for you in the [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="ac52a-125">例如，您不需要提供 Azure AD 授權單位、媒體服務資源 URI 或原生 Azure AD 應用程式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ac52a-125">For example, you don't need to provide the Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="ac52a-126">這些是已由 Azure AD 存取權杖提供者類別設定的已知值。</span><span class="sxs-lookup"><span data-stu-id="ac52a-126">These are well-known values that are already configured by the Azure AD access token provider class.</span></span> 

<span data-ttu-id="ac52a-127">如果您未使用 Azure 媒體服務 .NET SDK，建議您使用 [Azure AD 驗證程式庫](../active-directory/develop/active-directory-authentication-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="ac52a-127">If you are not using Azure Media Service .NET SDK, we recommend that you use the [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="ac52a-128">若要取得搭配 Azure AD 驗證程式庫使用所需之參數的值，請參閱[使用 Azure 入口網站存取 Azure AD 驗證設定](media-services-portal-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="ac52a-128">To get values for the parameters that you need to use with Azure AD Authentication Library, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="ac52a-129">您也可以選擇使用您自己的實作來取代預設的 **AzureAdTokenProvider** 實作。</span><span class="sxs-lookup"><span data-stu-id="ac52a-129">You also have the option of replacing the default implementation of the **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="ac52a-130">安裝及設定 Azure 媒體服務 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ac52a-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="ac52a-131">若要使用 Azure AD 驗證搭配媒體服務 .NET SDK，您需要最新的 [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) 封裝。</span><span class="sxs-lookup"><span data-stu-id="ac52a-131">To use Azure AD authentication with the Media Services .NET SDK, you need to have the latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="ac52a-132">此外，請將參考加入 **Microsoft.IdentityModel.Clients.ActiveDirectory** 組件。</span><span class="sxs-lookup"><span data-stu-id="ac52a-132">Also, add a reference to the **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="ac52a-133">如果您使用現有的應用程式，請包含 **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** 組件。</span><span class="sxs-lookup"><span data-stu-id="ac52a-133">If you are using an existing app, include the **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="ac52a-134">在 Visual Studio 中，建立新的 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac52a-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="ac52a-135">使用 [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet 封裝來安裝 **Azure 媒體服務 .NET SDK**。</span><span class="sxs-lookup"><span data-stu-id="ac52a-135">Use the [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package to install **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="ac52a-136">若要使用 NuGet 加入參考，請採取下列步驟︰在 [方案總管] 中，以滑鼠右鍵按一下專案名稱，然後選取 [管理 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="ac52a-136">To add references by using NuGet, take the following steps: in **Solution Explorer**, right-click the project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="ac52a-137">接著，搜尋 **windowsazure.mediaservices**，然後選取 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="ac52a-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="ac52a-138">-或-</span><span class="sxs-lookup"><span data-stu-id="ac52a-138">-or-</span></span>

    <span data-ttu-id="ac52a-139">在 Visual Studio 的 [封裝管理員主控台] 中，執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="ac52a-139">Run the following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="ac52a-140">新增 **using** 至您的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="ac52a-140">Add **using** to your source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="ac52a-141">使用使用者驗證</span><span class="sxs-lookup"><span data-stu-id="ac52a-141">Use user authentication</span></span>

<span data-ttu-id="ac52a-142">若要利用使用者驗證選項連線到 Azure 媒體服務 API，用戶端應用程式必須使用下列參數要求 Azure AD 權杖：</span><span class="sxs-lookup"><span data-stu-id="ac52a-142">To connect to the Azure Media Service API with the user authentication option, the client app needs to request an Azure AD token by using the following parameters:</span></span>  

- <span data-ttu-id="ac52a-143">Azure AD 租用戶端點。</span><span class="sxs-lookup"><span data-stu-id="ac52a-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="ac52a-144">租用戶資訊可從 Azure 入口網站擷取。</span><span class="sxs-lookup"><span data-stu-id="ac52a-144">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="ac52a-145">將滑鼠游標停留在右上角登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="ac52a-145">Hover over the signed-in user in the upper-right corner.</span></span>
- <span data-ttu-id="ac52a-146">媒體服務資源 URI。</span><span class="sxs-lookup"><span data-stu-id="ac52a-146">Media Services resource URI.</span></span>
- <span data-ttu-id="ac52a-147">媒體服務 (原生) 應用程式用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="ac52a-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="ac52a-148">媒體服務 (原生) 應用程式重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="ac52a-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="ac52a-149">這些參數的值位於 **AzureEnvironments.AzureCloudEnvironment**。</span><span class="sxs-lookup"><span data-stu-id="ac52a-149">The values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="ac52a-150">**AzureEnvironments.AzureCloudEnvironment** 常數是 .NET SDK 中的協助程式，用來取得公用 Azure 資料中心正確的環境變數設定。</span><span class="sxs-lookup"><span data-stu-id="ac52a-150">The **AzureEnvironments.AzureCloudEnvironment** constant is a helper in the .NET SDK to get the right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="ac52a-151">它包含預先定義的環境設定，只用於存取公用資料中心的媒體服務。</span><span class="sxs-lookup"><span data-stu-id="ac52a-151">It contains pre-defined environment settings for accessing Media Services in the public data centers only.</span></span> <span data-ttu-id="ac52a-152">對於 sovereign 或政府雲端區域，分別可以使用 **AzureChinaCloudEnvironment****AzureUsGovernmentEnvrionment** 或 **AzureGermanCloudEnvironment**。</span><span class="sxs-lookup"><span data-stu-id="ac52a-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="ac52a-153">下列程式碼範例會建立權杖：</span><span class="sxs-lookup"><span data-stu-id="ac52a-153">The following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="ac52a-154">若要開始針對媒體服務進行程式設計，您需要建立可呈現伺服器內容的 **CloudMediaContext** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ac52a-154">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="ac52a-155">**CloudMediaContext** 包含重要集合的參考，包括工作、資產、檔案、存取原則和定位器。</span><span class="sxs-lookup"><span data-stu-id="ac52a-155">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="ac52a-156">您還需要將**媒體 REST 服務的資源 URI** 傳遞至 **CloudMediaContext** 建構函式。</span><span class="sxs-lookup"><span data-stu-id="ac52a-156">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span></span> <span data-ttu-id="ac52a-157">若要取得媒體 REST 服務的資源 URI，請登入 Azure 入口網站，選取您的 Azure 媒體服務帳戶，選取 [API 存取權]，然後選取 [使用使用者驗證連線到 Azure 媒體服務]。</span><span class="sxs-lookup"><span data-stu-id="ac52a-157">To get the resource URI for Media REST Services, sign in to the Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect to Azure Media Services with user authentication**.</span></span> 

<span data-ttu-id="ac52a-158">下列程式碼範例會建立 **CloudMediaContext** 執行個體：</span><span class="sxs-lookup"><span data-stu-id="ac52a-158">The following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="ac52a-159">下列範例說明如何建立 Azure AD 權杖和內容：</span><span class="sxs-lookup"><span data-stu-id="ac52a-159">The following example shows how to create the Azure AD token and the context:</span></span>

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
><span data-ttu-id="ac52a-160">如果您收到指出「遠端伺服器傳回一個錯誤: (401) 未經授權」的例外狀況，請參閱使用 Azure AD 驗證存取 Azure 媒體服務 API 概觀的[存取控制](media-services-use-aad-auth-to-access-ams-api.md#access-control)一節。</span><span class="sxs-lookup"><span data-stu-id="ac52a-160">If you get an exception that says "The remote server returned an error: (401) Unauthorized," see the [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="ac52a-161">使用服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="ac52a-161">Use service principal authentication</span></span>
    
<span data-ttu-id="ac52a-162">若要利用服務主體選項連線到 Azure 媒體服務 API，您的中介層應用程式 (Web API 或 Web 應用程式) 必須要求具有下列參數的 Azure AD 權杖：</span><span class="sxs-lookup"><span data-stu-id="ac52a-162">To connect to the Azure Media Services API with the service principal option, your middle-tier app (web API or web application) needs to requests an Azure AD token with the following parameters:</span></span>  

- <span data-ttu-id="ac52a-163">Azure AD 租用戶端點。</span><span class="sxs-lookup"><span data-stu-id="ac52a-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="ac52a-164">租用戶資訊可從 Azure 入口網站擷取。</span><span class="sxs-lookup"><span data-stu-id="ac52a-164">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="ac52a-165">將滑鼠游標停留在右上角登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="ac52a-165">Hover over the signed-in user in the upper-right corner.</span></span>
- <span data-ttu-id="ac52a-166">媒體服務資源 URI。</span><span class="sxs-lookup"><span data-stu-id="ac52a-166">Media Services resource URI.</span></span>
- <span data-ttu-id="ac52a-167">Azure AD 應用程式的值：**用戶端識別碼**和**用戶端祕密**。</span><span class="sxs-lookup"><span data-stu-id="ac52a-167">Azure AD application values: the **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="ac52a-168">**用戶端識別碼**和**用戶端祕密**參數的值可以在 Azure 入口網站中找到。</span><span class="sxs-lookup"><span data-stu-id="ac52a-168">The values for the **Client ID** and **Client secret** parameters can be found in the Azure portal.</span></span> <span data-ttu-id="ac52a-169">如需詳細資訊，請參閱[利用 Azure 入口網站開始使用 Azure AD 驗證](media-services-portal-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="ac52a-169">For more information, see [Getting started with Azure AD authentication using the Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="ac52a-170">下列程式碼範例會使用以 **AzureAdClientSymmetricKey** 做為參數的 **AzureAdTokenCredentials** 建構函式建立權杖：</span><span class="sxs-lookup"><span data-stu-id="ac52a-170">The following code example creates a token by using the **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="ac52a-171">您也可以指定以 **AzureAdClientCertificate** 做為參數的 **AzureAdTokenCredentials** 建構函式。</span><span class="sxs-lookup"><span data-stu-id="ac52a-171">You can also specify the **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="ac52a-172">如需有關如何以可供 Azure AD 使用之形式建立及設定憑證的指示，請參閱[在精靈應用程式中使用憑證向 Azure AD 驗證 - 手動設定步驟](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md)。</span><span class="sxs-lookup"><span data-stu-id="ac52a-172">For instructions about how to create and configure a certificate in a form that can be used by Azure AD, see [Authenticating to Azure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="ac52a-173">若要開始針對媒體服務進行程式設計，您需要建立可呈現伺服器內容的 **CloudMediaContext** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ac52a-173">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="ac52a-174">您還需要將**媒體 REST 服務的資源 URI** 傳遞至 **CloudMediaContext** 建構函式。</span><span class="sxs-lookup"><span data-stu-id="ac52a-174">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span></span> <span data-ttu-id="ac52a-175">您也可以從 Azure 入口網站取得**媒體 REST 服務的資源 URI** 值。</span><span class="sxs-lookup"><span data-stu-id="ac52a-175">You can get the **resource URI for Media REST Services** value from the Azure portal as well.</span></span>

<span data-ttu-id="ac52a-176">下列程式碼範例會建立 **CloudMediaContext** 執行個體：</span><span class="sxs-lookup"><span data-stu-id="ac52a-176">The following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="ac52a-177">下列範例說明如何建立 Azure AD 權杖和內容：</span><span class="sxs-lookup"><span data-stu-id="ac52a-177">The following example shows how to create the Azure AD token and the context:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ac52a-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac52a-178">Next steps</span></span>

<span data-ttu-id="ac52a-179">開始使用[上傳檔案至您的帳戶](media-services-dotnet-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="ac52a-179">Get started with [uploading files to your account](media-services-dotnet-upload-files.md).</span></span>

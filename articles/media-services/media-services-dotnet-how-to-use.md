---
title: "如何使用 .NET 設定用於媒體服務開發的電腦"
description: "了解將 Media Services SDK for .NET 用於媒體服務的必要條件。 同時了解如何建立 Visual Studio 應用程式。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: 15828bc74937a036871b26493498232ec7cf6f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="87e26-104">使用 .NET 進行媒體服務開發</span><span class="sxs-lookup"><span data-stu-id="87e26-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="87e26-105">本主題討論如何使用 .NET 開始開發媒體服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e26-105">This topic discusses how to start developing Media Services applications using .NET.</span></span>

<span data-ttu-id="87e26-106">**Azure Media Services .NET SDK 程式庫** 可讓您使用 .NET 對媒體服務進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="87e26-106">The **Azure Media Services .NET SDK** library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="87e26-107">為了讓使用 .NET 進行開發更為簡單，會提供 **Azure Media Services .NET SDK 延伸模組** 程式庫。</span><span class="sxs-lookup"><span data-stu-id="87e26-107">To make it even easier to develop with .NET, the **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="87e26-108">此程式庫包含一組延伸方法和協助程式函數，以簡化 .NET 程式碼。</span><span class="sxs-lookup"><span data-stu-id="87e26-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="87e26-109">這兩個程式庫都是透過 **NuGet** 和 **GitHub** 取得。</span><span class="sxs-lookup"><span data-stu-id="87e26-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87e26-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="87e26-110">Prerequisites</span></span>
* <span data-ttu-id="87e26-111">新的或現有 Azure 訂用帳戶中的媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="87e26-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="87e26-112">請參閱主題 [如何建立媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="87e26-112">See the topic [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="87e26-113">作業系統：Windows 10、Windows 7、Windows 2008 R2 或 Windows 8。</span><span class="sxs-lookup"><span data-stu-id="87e26-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="87e26-114">.NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="87e26-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="87e26-115">Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="87e26-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="87e26-116">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="87e26-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="87e26-117">本節說明如何在 Visual Studio 中建立專案並設定來進行媒體服務開發。</span><span class="sxs-lookup"><span data-stu-id="87e26-117">This section shows you how to create a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="87e26-118">在此案例中，專案是 C# Windows 主控台應用程式，但這裡顯示的設定步驟也適用於可以為媒體服務應用程式建立的其他專案類型 (例如，Windows Forms 應用程式或 ASP.NET Web 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="87e26-118">In this case, the project is a C# Windows console application, but the same setup steps shown here apply to other types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="87e26-119">本節顯示如何使用 **NuGet** 新增 Media Services .NET SDK 延伸模組和其他相依程式庫。</span><span class="sxs-lookup"><span data-stu-id="87e26-119">This section shows how to use **NuGet** to add Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="87e26-120">或者，您可以從 GitHub 取得最新 Media Services .NET SDK 位元 ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) 或 [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions))、建置方案，並新增至用戶端專案的參考。</span><span class="sxs-lookup"><span data-stu-id="87e26-120">Alternatively, you can get the latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build the solution, and add the references to the client project.</span></span> <span data-ttu-id="87e26-121">所有必要相依性皆會自動下載並解壓縮。</span><span class="sxs-lookup"><span data-stu-id="87e26-121">All the necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="87e26-122">在 Visual Studio 中，建立新的 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e26-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="87e26-123">輸入 [名稱]、[位置] 和 [方案名稱]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="87e26-123">Enter the **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="87e26-124">建置方案。</span><span class="sxs-lookup"><span data-stu-id="87e26-124">Build the solution.</span></span>
3. <span data-ttu-id="87e26-125">使用 **NuGet** 來安裝和新增 **Azure 媒體服務 .NET SDK 延伸模組** (**windowsazure.mediaservices.extensions**)。</span><span class="sxs-lookup"><span data-stu-id="87e26-125">Use **NuGet** to install and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="87e26-126">安裝這個封裝，也會安裝 **Media Services .NET SDK** ，並新增所有其他必要相依性。</span><span class="sxs-lookup"><span data-stu-id="87e26-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="87e26-127">確定您已安裝 NuGet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="87e26-127">Ensure that you have the newest version of NuGet installed.</span></span> <span data-ttu-id="87e26-128">如需詳細資訊和安裝指示，請參閱 [NuGet](http://nuget.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="87e26-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="87e26-129">在 [方案總管] 中，於專案名稱上按一下滑鼠右鍵，然後選擇 [管理 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="87e26-129">In Solution Explorer, right-click the name of the project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="87e26-130">[管理 NuGet 封裝] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="87e26-130">The Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="87e26-131">在線上資源庫中，搜尋 [Azure MediaServices 延伸模組]，並選擇 [Azure Media Services .NET SDK 延伸模組]，然後按一下 [安裝] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="87e26-131">In the Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click the Install button.</span></span>
   
    <span data-ttu-id="87e26-132">會修改專案，並新增 Media Services .NET SDK 延伸模組、Media Services .NET SDK 和其他相依組件的參考。</span><span class="sxs-lookup"><span data-stu-id="87e26-132">The project is modified and references to the Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="87e26-133">若要提升更乾淨的開發環境，請考慮啟用 [NuGet 封裝還原]。</span><span class="sxs-lookup"><span data-stu-id="87e26-133">To promote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="87e26-134">如需詳細資訊，請參閱 [NuGet 封裝還原](http://docs.nuget.org/consume/package-restore)。</span><span class="sxs-lookup"><span data-stu-id="87e26-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="87e26-135">加入 **System.Configuration** 組件的參考。</span><span class="sxs-lookup"><span data-stu-id="87e26-135">Add a reference to **System.Configuration** assembly.</span></span> <span data-ttu-id="87e26-136">此組件包含用來存取組態檔 (例如 App.config) 的 System.Configuration.**ConfigurationManager** 類別。</span><span class="sxs-lookup"><span data-stu-id="87e26-136">This assembly contains the System.Configuration.**ConfigurationManager** class that is used to access configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="87e26-137">若要使用 [管理參考] 對話方塊新增參考，請以滑鼠右鍵按一下 [方案總管] 中的專案名稱。</span><span class="sxs-lookup"><span data-stu-id="87e26-137">To add references using the Manage References dialog, right-click the project name in the Solution Explorer.</span></span> <span data-ttu-id="87e26-138">然後，依序選取 [加入] 和 [參考]。</span><span class="sxs-lookup"><span data-stu-id="87e26-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="87e26-139">[管理參考] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="87e26-139">The Manage References dialog appears.</span></span>
8. <span data-ttu-id="87e26-140">在 .NET Framework 組件下，尋找並選取 System.Configuration 組件，然後按 [確定]。</span><span class="sxs-lookup"><span data-stu-id="87e26-140">Under .NET framework assemblies, find and select the System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="87e26-141">開啟 App.config 檔案並將 *appSettings* 區段新增至檔案。</span><span class="sxs-lookup"><span data-stu-id="87e26-141">Open the App.config file and add an *appSettings* section to the file.</span></span>     
   
    <span data-ttu-id="87e26-142">設定連接媒體服務 API 時所需的值。</span><span class="sxs-lookup"><span data-stu-id="87e26-142">Set the values that are needed to connect to the Media Services API.</span></span> <span data-ttu-id="87e26-143">如需詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="87e26-143">For more information, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="87e26-144">如果您使用[使用者驗證](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication)，您的設定檔可能會有 Azure AD 租用戶網域和 AMS REST API 端點的值。</span><span class="sxs-lookup"><span data-stu-id="87e26-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and the AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="87e26-145">Azure 媒體服務文件集中大多數的程式碼範例，以使用者 (互動式) 的驗證類型連線到 AMS API。</span><span class="sxs-lookup"><span data-stu-id="87e26-145">Most code samples in the Azure Media Services documentation set, use a user (interactive) type of authentication to connect to the AMS API.</span></span> <span data-ttu-id="87e26-146">這種驗證方法適用於管理或監控原生應用程式：行動應用程式、Windows 應用程式和主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e26-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="87e26-147">這種驗證方法不適用於伺服器、Web 服務、API 類型的應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e26-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="87e26-148">如需詳細資訊，請參閱[使用 Azure AD 驗證存取 AMS API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="87e26-148">For more information, see [Access the AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="87e26-149">在 Program.cs 檔案的開頭，使用下列程式碼來覆寫現有的 **using** 陳述式。</span><span class="sxs-lookup"><span data-stu-id="87e26-149">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="87e26-150">現在，您可以開始開發媒體服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e26-150">At this point, you are ready to start developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="87e26-151">範例</span><span class="sxs-lookup"><span data-stu-id="87e26-151">Example</span></span>

<span data-ttu-id="87e26-152">以下是一個小範例，它會連接到 AMS API，並列出所有可用的媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="87e26-152">Here is a small example that connects to the AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a><span data-ttu-id="87e26-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87e26-153">Next steps</span></span>

<span data-ttu-id="87e26-154">現在[您可以連接到 AMS API](media-services-use-aad-auth-to-access-ams-api.md)並開始[開發](media-services-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="87e26-154">Now [you can connect to the AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="87e26-155">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="87e26-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="87e26-156">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="87e26-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


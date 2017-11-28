---
title: "aaaHow tooSet 與.NET 的 Media Services 開發的總電腦"
description: "深入了解使用 hello Media Services SDK for.NET 的 Media Services 的 hello 必要條件。 也了解如何 toocreate Visual Studio 應用程式。"
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
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="6eaea-104">使用 .NET 進行媒體服務開發</span><span class="sxs-lookup"><span data-stu-id="6eaea-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="6eaea-105">本主題討論 toostart 開發媒體服務如何使用.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eaea-105">This topic discusses how toostart developing Media Services applications using .NET.</span></span>

<span data-ttu-id="6eaea-106">hello **Azure Media Services.NET SDK**程式庫可讓您針對使用.NET 的 Media Services tooprogram。</span><span class="sxs-lookup"><span data-stu-id="6eaea-106">hello **Azure Media Services .NET SDK** library enables you tooprogram against Media Services using .NET.</span></span> <span data-ttu-id="6eaea-107">它甚至.NET 中，以更容易 toodevelop hello toomake **Azure Media Services.NET SDK Extensions**提供程式庫。</span><span class="sxs-lookup"><span data-stu-id="6eaea-107">toomake it even easier toodevelop with .NET, hello **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="6eaea-108">此程式庫包含一組延伸方法和協助程式函數，以簡化 .NET 程式碼。</span><span class="sxs-lookup"><span data-stu-id="6eaea-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="6eaea-109">這兩個程式庫都是透過 **NuGet** 和 **GitHub** 取得。</span><span class="sxs-lookup"><span data-stu-id="6eaea-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6eaea-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6eaea-110">Prerequisites</span></span>
* <span data-ttu-id="6eaea-111">新的或現有 Azure 訂用帳戶中的媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="6eaea-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="6eaea-112">請參閱 hello 主題[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="6eaea-112">See hello topic [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="6eaea-113">作業系統：Windows 10、Windows 7、Windows 2008 R2 或 Windows 8。</span><span class="sxs-lookup"><span data-stu-id="6eaea-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="6eaea-114">.NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="6eaea-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="6eaea-115">Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6eaea-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="6eaea-116">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="6eaea-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="6eaea-117">這個區段會顯示如何 toocreate Visual Studio 中的專案將它設定 Media Services 開發。</span><span class="sxs-lookup"><span data-stu-id="6eaea-117">This section shows you how toocreate a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="6eaea-118">在此情況下，hello 專案是 C# Windows 主控台應用程式，但 hello 相同的設定步驟，如下所示套用 tooother 類型，您可以建立媒體服務應用程式 （例如，在 Windows Forms 應用程式或 ASP.NET Web 應用程式） 的專案。</span><span class="sxs-lookup"><span data-stu-id="6eaea-118">In this case, hello project is a C# Windows console application, but hello same setup steps shown here apply tooother types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="6eaea-119">此區段會顯示如何 toouse **NuGet** tooadd Media Services.NET SDK 延伸模組和其他相依程式庫。</span><span class="sxs-lookup"><span data-stu-id="6eaea-119">This section shows how toouse **NuGet** tooadd Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="6eaea-120">或者，您可以從 GitHub 取得 hello 最新的媒體服務.NET SDK 位元 ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services)或[github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions))，建立 hello 方案，並新增 hello 參考 toohello 用戶端專案。</span><span class="sxs-lookup"><span data-stu-id="6eaea-120">Alternatively, you can get hello latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build hello solution, and add hello references toohello client project.</span></span> <span data-ttu-id="6eaea-121">下載並自動擷取所有與 hello 必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="6eaea-121">All hello necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="6eaea-122">在 Visual Studio 中，建立新的 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eaea-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="6eaea-123">輸入 hello**名稱**，**位置**，和**方案名稱**，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="6eaea-123">Enter hello **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="6eaea-124">建置 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="6eaea-124">Build hello solution.</span></span>
3. <span data-ttu-id="6eaea-125">使用**NuGet** tooinstall 並加入**Azure Media Services.NET SDK Extensions** (**windowsazure.mediaservices.extensions**)。</span><span class="sxs-lookup"><span data-stu-id="6eaea-125">Use **NuGet** tooinstall and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="6eaea-126">安裝這個封裝，也會安裝 **Media Services .NET SDK** ，並新增所有其他必要相依性。</span><span class="sxs-lookup"><span data-stu-id="6eaea-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="6eaea-127">確定您擁有 hello NuGet 安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="6eaea-127">Ensure that you have hello newest version of NuGet installed.</span></span> <span data-ttu-id="6eaea-128">如需詳細資訊和安裝指示，請參閱 [NuGet](http://nuget.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="6eaea-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="6eaea-129">在 方案總管 hello hello 專案名稱上按一下滑鼠右鍵並選擇 管理 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="6eaea-129">In Solution Explorer, right-click hello name of hello project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="6eaea-130">hello [管理 NuGet 封裝] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="6eaea-130">hello Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="6eaea-131">在 hello 線上圖庫中，搜尋 Azure MediaServices Extensions，選擇 Azure Media Services.NET SDK Extensions，，然後按一下 hello [安裝] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6eaea-131">In hello Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click hello Install button.</span></span>
   
    <span data-ttu-id="6eaea-132">hello 專案會修改，並參考 toohello Media Services.NET SDK Extensions，Media Services.NET SDK，並加入其他相依的組件。</span><span class="sxs-lookup"><span data-stu-id="6eaea-132">hello project is modified and references toohello Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="6eaea-133">toopromote 清除工具開發環境中，請考慮啟用 NuGet 封裝還原。</span><span class="sxs-lookup"><span data-stu-id="6eaea-133">toopromote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="6eaea-134">如需詳細資訊，請參閱 [NuGet 封裝還原](http://docs.nuget.org/consume/package-restore)。</span><span class="sxs-lookup"><span data-stu-id="6eaea-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="6eaea-135">將參考加入太**System.Configuration**組件。</span><span class="sxs-lookup"><span data-stu-id="6eaea-135">Add a reference too**System.Configuration** assembly.</span></span> <span data-ttu-id="6eaea-136">這個組件包含 hello System.Configuration。**ConfigurationManager**類別也就是使用的 tooaccess 組態檔案 (例如，App.config)。</span><span class="sxs-lookup"><span data-stu-id="6eaea-136">This assembly contains hello System.Configuration.**ConfigurationManager** class that is used tooaccess configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="6eaea-137">tooadd 參考使用 hello 管理參考 對話方塊中，以滑鼠右鍵按一下 hello hello 方案總管 中的專案名稱。</span><span class="sxs-lookup"><span data-stu-id="6eaea-137">tooadd references using hello Manage References dialog, right-click hello project name in hello Solution Explorer.</span></span> <span data-ttu-id="6eaea-138">然後，依序選取 [加入] 和 [參考]。</span><span class="sxs-lookup"><span data-stu-id="6eaea-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="6eaea-139">hello 管理參考 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="6eaea-139">hello Manage References dialog appears.</span></span>
8. <span data-ttu-id="6eaea-140">在.NET framework 組件，尋找並選取 hello System.Configuration 組件，按下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6eaea-140">Under .NET framework assemblies, find and select hello System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="6eaea-141">開啟 hello App.config 檔案，然後加入*appSettings*節 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="6eaea-141">Open hello App.config file and add an *appSettings* section toohello file.</span></span>     
   
    <span data-ttu-id="6eaea-142">設定所需的 tooconnect toohello Media Services API 的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="6eaea-142">Set hello values that are needed tooconnect toohello Media Services API.</span></span> <span data-ttu-id="6eaea-143">如需詳細資訊，請參閱[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="6eaea-143">For more information, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="6eaea-144">如果您使用[使用者驗證](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication)組態檔可能會有值為您的 Azure AD 租用戶網域和 hello AMS REST API 端點。</span><span class="sxs-lookup"><span data-stu-id="6eaea-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and hello AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="6eaea-145">Hello Azure Media Services 文件中的大部分程式碼範例會設定，請使用使用者驗證 tooconnect toohello AMS 應用程式開發介面的類型 （互動式）。</span><span class="sxs-lookup"><span data-stu-id="6eaea-145">Most code samples in hello Azure Media Services documentation set, use a user (interactive) type of authentication tooconnect toohello AMS API.</span></span> <span data-ttu-id="6eaea-146">這種驗證方法適用於管理或監控原生應用程式：行動應用程式、Windows 應用程式和主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eaea-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="6eaea-147">這種驗證方法不適用於伺服器、Web 服務、API 類型的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eaea-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="6eaea-148">如需詳細資訊，請參閱[存取 hello AMS API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="6eaea-148">For more information, see [Access hello AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="6eaea-149">覆寫現有的 hello**使用**hello Program.cs 檔案，以下列程式碼的 hello 的 hello 開頭的陳述式。</span><span class="sxs-lookup"><span data-stu-id="6eaea-149">Overwrite hello existing **using** statements at hello beginning of hello Program.cs file with hello following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="6eaea-150">此時，您就準備好 toostart 開發媒體服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eaea-150">At this point, you are ready toostart developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="6eaea-151">範例</span><span class="sxs-lookup"><span data-stu-id="6eaea-151">Example</span></span>

<span data-ttu-id="6eaea-152">以下是小型的範例連接 toohello AMS 應用程式開發介面，並列出所有可用的媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="6eaea-152">Here is a small example that connects toohello AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from hello App.config file.
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

##<a name="next-steps"></a><span data-ttu-id="6eaea-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6eaea-153">Next steps</span></span>

<span data-ttu-id="6eaea-154">現在[您可以連接 toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md)並啟動[開發](media-services-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6eaea-154">Now [you can connect toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="6eaea-155">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="6eaea-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6eaea-156">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="6eaea-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


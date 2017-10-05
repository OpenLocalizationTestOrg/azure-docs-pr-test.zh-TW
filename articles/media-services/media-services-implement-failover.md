---
title: "使用 Azure 媒體服務實作容錯移轉串流 | Microsoft Docs"
description: "本主題說明如何實作容錯移轉串流案例。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fc45d849-eb0d-4739-ae91-0ff648113445
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako
ms.openlocfilehash: aed104c9c74606e0ad69fc2d0bfb2f38d85d795d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="implement-failover-streaming-with-azure-media-services"></a><span data-ttu-id="bded0-103">使用 Azure 媒體服務實作容錯移轉串流</span><span class="sxs-lookup"><span data-stu-id="bded0-103">Implement failover streaming with Azure Media Services</span></span>

<span data-ttu-id="bded0-104">本逐步解說示範如何將內容 (Blob) 從一個資產複製到另一個資產，以便處理隨選資料流處理的備援。</span><span class="sxs-lookup"><span data-stu-id="bded0-104">This walkthrough demonstrates how to copy content (blobs) from one asset into another in order to handle redundancy for on-demand streaming.</span></span> <span data-ttu-id="bded0-105">如果您想要設定 Azure 內容傳遞網路，以便在某個資料中心發生中斷時在兩個資料中心之間進行容錯移轉，這個案例會很有用。</span><span class="sxs-lookup"><span data-stu-id="bded0-105">This scenario is useful if you want to set up Azure Content Delivery Network to fail over between two datacenters, in case of an outage in one datacenter.</span></span> <span data-ttu-id="bded0-106">本逐步解說使用 Azure 媒體服務 SDK、Azure 媒體服務 REST API 和 Azure 儲存體 SDK 來示範下列工作：</span><span class="sxs-lookup"><span data-stu-id="bded0-106">This walkthrough uses the Azure Media Services SDK, the Azure Media Services REST API, and the Azure Storage SDK to demonstrate the following tasks:</span></span>

1. <span data-ttu-id="bded0-107">在「資料中心 A」中設定媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="bded0-107">Set up a Media Services account in "Data Center A."</span></span>
2. <span data-ttu-id="bded0-108">將夾層檔上傳到來源資產。</span><span class="sxs-lookup"><span data-stu-id="bded0-108">Upload a mezzanine file into a source asset.</span></span>
3. <span data-ttu-id="bded0-109">將資產編碼為多位元速率 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="bded0-109">Encode the asset into multi-bit rate MP4 files.</span></span> 
4. <span data-ttu-id="bded0-110">建立唯讀的共用存取簽章定位器。</span><span class="sxs-lookup"><span data-stu-id="bded0-110">Create a read-only shared access signature locator.</span></span> <span data-ttu-id="bded0-111">這是為了讓來源資產能夠存取與來源資產相關聯之儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="bded0-111">This is for the source asset to have read access to the container in the storage account that is associated with the source asset.</span></span>
5. <span data-ttu-id="bded0-112">從上一個步驟中建立的唯讀共用存取簽章定位器取得來源資產的容器名稱。</span><span class="sxs-lookup"><span data-stu-id="bded0-112">Get the container name of the source asset from the read-only shared access signature locator created in the previous step.</span></span> <span data-ttu-id="bded0-113">必須有此名稱，才能在儲存體帳戶之間複製 Blob (本主題稍後說明)。</span><span class="sxs-lookup"><span data-stu-id="bded0-113">This is necessary for copying blobs between storage accounts (explained later in the topic.)</span></span>
6. <span data-ttu-id="bded0-114">為編碼工作所建立的資產建立原始定位器。</span><span class="sxs-lookup"><span data-stu-id="bded0-114">Create an origin locator for the asset that was created by the encoding task.</span></span> 

<span data-ttu-id="bded0-115">接著，若要處理容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="bded0-115">Then, to handle the failover:</span></span>

1. <span data-ttu-id="bded0-116">在「資料中心 B」中設定媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="bded0-116">Set up a Media Services account in "Data Center B."</span></span>
2. <span data-ttu-id="bded0-117">在目標媒體服務帳戶中建立目標空資產。</span><span class="sxs-lookup"><span data-stu-id="bded0-117">Create a target empty asset in the target Media Services account.</span></span>
3. <span data-ttu-id="bded0-118">建立寫入共用存取簽章定位器。</span><span class="sxs-lookup"><span data-stu-id="bded0-118">Create a write shared access signature locator.</span></span> <span data-ttu-id="bded0-119">這是為了讓目標空白資產能夠寫入到與目標資產相關聯之目標儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="bded0-119">This is for the target empty asset to have write access to the container in the target storage account that is associated with the target asset.</span></span>
4. <span data-ttu-id="bded0-120">使用「Azure 儲存體 SDK」在「資料中心 A」中的來源儲存體帳戶與「資料中心 B」中的目標儲存體帳戶之間複製 Blob (資產檔案)。</span><span class="sxs-lookup"><span data-stu-id="bded0-120">Use the Azure Storage SDK to copy blobs (asset files) between the source storage account in "Data Center A" and the target storage account in "Data Center B."</span></span> <span data-ttu-id="bded0-121">這些儲存體帳戶會與相關資產關聯。</span><span class="sxs-lookup"><span data-stu-id="bded0-121">These storage accounts are associated with the assets of interest.</span></span>
5. <span data-ttu-id="bded0-122">讓複製到目標 Blob 容器的 Blob (資產檔案) 與目標資產產生關聯。</span><span class="sxs-lookup"><span data-stu-id="bded0-122">Associate blobs (asset files) that were copied to the target blob container with the target asset.</span></span> 
6. <span data-ttu-id="bded0-123">為「資料中心 B」中的資產建立原始定位器，並指定為「資料中心 A」中的資產所產生的定位器識別碼。</span><span class="sxs-lookup"><span data-stu-id="bded0-123">Create an origin locator for the asset in "Data Center B", and specify the locator ID that was generated for the asset in "Data Center A."</span></span>

<span data-ttu-id="bded0-124">這可提供串流 URL，其中 URL 的相對路徑相同 (只有基底 URL 不同)。</span><span class="sxs-lookup"><span data-stu-id="bded0-124">This gives you the streaming URLs where the relative paths of the URLs are the same (only the base URLs are different).</span></span> 

<span data-ttu-id="bded0-125">然後，若要處理任何中斷情形，您可以在這些原始定位器之上建立內容傳遞網路。</span><span class="sxs-lookup"><span data-stu-id="bded0-125">Then, to handle any outages, you can create a Content Delivery Network on top of these origin locators.</span></span> 

<span data-ttu-id="bded0-126">您必須考量下列事項：</span><span class="sxs-lookup"><span data-stu-id="bded0-126">The following considerations apply:</span></span>

* <span data-ttu-id="bded0-127">目前的媒體服務 SDK 版本不支援以程式設計方式產生可讓資產和資產檔案產生關聯的 IAssetFile 資訊。</span><span class="sxs-lookup"><span data-stu-id="bded0-127">The current version of Media Services SDK does not support programmatically generating IAssetFile information that would associate an asset with asset files.</span></span> <span data-ttu-id="bded0-128">請改為使用 CreateFileInfos 媒體服務 REST API 來進行此操作。</span><span class="sxs-lookup"><span data-stu-id="bded0-128">Instead, use the CreateFileInfos Media Services REST API to do this.</span></span> 
* <span data-ttu-id="bded0-129">儲存體加密資產 (AssetCreationOptions.StorageEncrypted) 不支援複寫 (因為兩個媒體服務帳戶中的加密金鑰不同)。</span><span class="sxs-lookup"><span data-stu-id="bded0-129">Storage encrypted assets (AssetCreationOptions.StorageEncrypted) are not supported for replication (because the encryption key is different in both Media Services accounts).</span></span> 
* <span data-ttu-id="bded0-130">如果您想要利用動態封裝，請確定您想要從中串流內容的串流端點是處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="bded0-130">If you want to take advantage of dynamic packaging, make sure the streaming endpoint from which you want to stream  your content is in the **Running** state.</span></span>

> [!NOTE]
> <span data-ttu-id="bded0-131">請考慮使用媒體服務 [複寫器工具](http://replicator.codeplex.com/) 做為手動實作容錯移轉串流案例的替代方式。</span><span class="sxs-lookup"><span data-stu-id="bded0-131">Consider using the Media Services [Replicator Tool](http://replicator.codeplex.com/) as an alternative to implementing a failover streaming scenario manually.</span></span> <span data-ttu-id="bded0-132">這項工具可讓您跨兩個媒體服務帳戶複製資產。</span><span class="sxs-lookup"><span data-stu-id="bded0-132">This tool allows you to replicate assets across two Media Services accounts.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="bded0-133">必要條件</span><span class="sxs-lookup"><span data-stu-id="bded0-133">Prerequisites</span></span>
* <span data-ttu-id="bded0-134">在新的或現有的 Azure 訂用帳戶中有兩個媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="bded0-134">Two Media Services accounts in a new or existing Azure subscription.</span></span> <span data-ttu-id="bded0-135">請參閱 [如何建立媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="bded0-135">See [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="bded0-136">作業系統：Windows 7、Windows 2008 R2 或 Windows 8。</span><span class="sxs-lookup"><span data-stu-id="bded0-136">Operating system: Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="bded0-137">.NET Framework 4.5 或 .NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="bded0-137">.NET Framework 4.5 or .NET Framework 4.</span></span>
* <span data-ttu-id="bded0-138">Visual Studio 2010 SP1 或更新版本 (Professional, Premium、Ultimate 或 Express)。</span><span class="sxs-lookup"><span data-stu-id="bded0-138">Visual Studio 2010 SP1 or later version (Professional, Premium, Ultimate, or Express).</span></span>

## <a name="set-up-your-project"></a><span data-ttu-id="bded0-139">設定專案</span><span class="sxs-lookup"><span data-stu-id="bded0-139">Set up your project</span></span>
<span data-ttu-id="bded0-140">在本節中，您會建立 C# Console Application 專案。</span><span class="sxs-lookup"><span data-stu-id="bded0-140">In this section, you create and set up a C# Console Application project.</span></span>

1. <span data-ttu-id="bded0-141">使用 Visual Studio 建立一個包含 C# Console Application 專案的新方案。</span><span class="sxs-lookup"><span data-stu-id="bded0-141">Use Visual Studio to create a new solution that contains the C# Console Application project.</span></span> <span data-ttu-id="bded0-142">輸入 **HandleRedundancyForOnDemandStreaming** 做為名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="bded0-142">Enter **HandleRedundancyForOnDemandStreaming** for the name, and then click **OK**.</span></span>
2. <span data-ttu-id="bded0-143">在與 **HandleRedundancyForOnDemandStreaming.csproj** 專案檔案相同的層級上建立 **SupportFiles** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="bded0-143">Create the **SupportFiles** folder on the same level as the **HandleRedundancyForOnDemandStreaming.csproj** project file.</span></span> <span data-ttu-id="bded0-144">在 **SupportFiles** 資料夾下建立 **OutputFiles** 和 **MP4Files** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="bded0-144">Under the **SupportFiles** folder, create the **OutputFiles** and **MP4Files** folders.</span></span> <span data-ttu-id="bded0-145">將 .mp4 檔案複製到 **MP4Files** 資料夾 </span><span class="sxs-lookup"><span data-stu-id="bded0-145">Copy an .mp4 file into the **MP4Files** folder.</span></span> <span data-ttu-id="bded0-146">(在此範例中，會使用 **BigBuckBunny.mp4** 檔案)。</span><span class="sxs-lookup"><span data-stu-id="bded0-146">(In this example, the **BigBuckBunny.mp4** file is used.)</span></span> 
3. <span data-ttu-id="bded0-147">使用 **Nuget** 將參考新增至與媒體服務相關的 DLL。</span><span class="sxs-lookup"><span data-stu-id="bded0-147">Use **Nuget** to add references to DLLs related to Media Services.</span></span> <span data-ttu-id="bded0-148">在 **Visual Studio 主要功能表**中，選取 [工具] > [Library Package Manager] > [Package Manager Console]。</span><span class="sxs-lookup"><span data-stu-id="bded0-148">In **Visual Studio Main Menu**, select **TOOLS** > **Library Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="bded0-149">在主控台視窗中輸入 **Install-package windowsazure.mediaservices**，然後按下 Enter。</span><span class="sxs-lookup"><span data-stu-id="bded0-149">In the console window, type **Install-Package windowsazure.mediaservices**, and press Enter.</span></span>
4. <span data-ttu-id="bded0-150">新增此專案所需的其他參考：System.Configuration、System.Runtime.Serialization 和 System.Web。</span><span class="sxs-lookup"><span data-stu-id="bded0-150">Add other references that are required for this project: System.Configuration, System.Runtime.Serialization, and System.Web.</span></span>
5. <span data-ttu-id="bded0-151">將預設新增至 **Programs.cs** 檔的 **using** 陳述式取代為下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="bded0-151">Replace **using** statements that were added to the **Programs.cs** file by default with the following ones:</span></span>
   
        using System;
        using System.Configuration;
        using System.Globalization;
        using System.IO;
        using System.Net;
        using System.Runtime.Serialization.Json;
        using System.Text;
        using System.Threading;
        using System.Threading.Tasks;
        using System.Web;
        using System.Xml;
        using System.Linq;
        using Microsoft.WindowsAzure;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using Microsoft.WindowsAzure.Storage.Auth;
6. <span data-ttu-id="bded0-152">將 **appSettings** 區段新增至 **.config** 檔中，並根據媒體服務與儲存體金鑰與名稱值將值更新。</span><span class="sxs-lookup"><span data-stu-id="bded0-152">Add the **appSettings** section to the **.config** file, and update the values based on your Media Services and Storage key and name values.</span></span> 
   
        <appSettings>
          <add key="MediaServicesAccountNameSource" value="Media-Services-Account-Name-Source"/>
          <add key="MediaServicesAccountKeySource" value="Media-Services-Account-Key-Source"/>
          <add key="MediaServicesStorageAccountNameSource" value="Media-Services-Storage-Account-Name-Source"/>
          <add key="MediaServicesStorageAccountKeySource" value="Media-Services-Storage-Account-Key-Source"/>
          <add key="MediaServicesAccountNameTarget" value="Media-Services-Account-Name-Target" />
          <add key="MediaServicesAccountKeyTarget" value=" Media-Services-Account-Key-Target" />
          <add key="MediaServicesStorageAccountNameTarget" value=" Media-Services-Storage-Account-Name-Target" />
          <add key="MediaServicesStorageAccountKeyTarget" value=" Media-Services-Storage-Account-Key-Target" />
        </appSettings>

## <a name="add-code-that-handles-redundancy-for-on-demand-streaming"></a><span data-ttu-id="bded0-153">新增可為隨選資料流處理備援的程式碼</span><span class="sxs-lookup"><span data-stu-id="bded0-153">Add code that handles redundancy for on-demand streaming</span></span>
<span data-ttu-id="bded0-154">在本節中，您會建立處理備援的能力。</span><span class="sxs-lookup"><span data-stu-id="bded0-154">In this section, you create the ability to handle redundancy.</span></span>

1. <span data-ttu-id="bded0-155">將下列類別層級欄位加入至 Program 類別。</span><span class="sxs-lookup"><span data-stu-id="bded0-155">Add the following class-level fields to the Program class.</span></span>
       
        // Read values from the App.config file.
        private static readonly string MediaServicesAccountNameSource = ConfigurationManager.AppSettings["MediaServicesAccountNameSource"];
        private static readonly string MediaServicesAccountKeySource = ConfigurationManager.AppSettings["MediaServicesAccountKeySource"];
        private static readonly string StorageNameSource = ConfigurationManager.AppSettings["MediaServicesStorageAccountNameSource"];
        private static readonly string StorageKeySource = ConfigurationManager.AppSettings["MediaServicesStorageAccountKeySource"];
        
        private static readonly string MediaServicesAccountNameTarget = ConfigurationManager.AppSettings["MediaServicesAccountNameTarget"];
        private static readonly string MediaServicesAccountKeyTarget = ConfigurationManager.AppSettings["MediaServicesAccountKeyTarget"];
        private static readonly string StorageNameTarget = ConfigurationManager.AppSettings["MediaServicesStorageAccountNameTarget"];
        private static readonly string StorageKeyTarget = ConfigurationManager.AppSettings["MediaServicesStorageAccountKeyTarget"];
        
        // Base support files path.  Update this field to point to the base path  
        // for the local support files folder that you create. 
        private static readonly string SupportFiles = Path.GetFullPath(@"../..\SupportFiles");
        
        // Paths to support files (within the above base path). 
        private static readonly string SingleInputMp4Path = Path.GetFullPath(SupportFiles + @"\MP4Files\BigBuckBunny.mp4");
        private static readonly string OutputFilesFolder = Path.GetFullPath(SupportFiles + @"\OutputFiles");
        
        // Class-level field used to keep a reference to the service context.
        static private CloudMediaContext _contextSource = null;
        static private CloudMediaContext _contextTarget = null;
        static private MediaServicesCredentials _cachedCredentialsSource = null;
        static private MediaServicesCredentials _cachedCredentialsTarget = null;

2. <span data-ttu-id="bded0-156">以下列其中一項取代預設的 Main 方法定義。</span><span class="sxs-lookup"><span data-stu-id="bded0-156">Replace the default Main method definition with the following one.</span></span> <span data-ttu-id="bded0-157">從 Main 呼叫的方法定義會定義如下。</span><span class="sxs-lookup"><span data-stu-id="bded0-157">Method definitions that are called from Main are defined below.</span></span>
        
        static void Main(string[] args)
        {
            _cachedCredentialsSource = new MediaServicesCredentials(
                            MediaServicesAccountNameSource,
                            MediaServicesAccountKeySource);
        
            _cachedCredentialsTarget = new MediaServicesCredentials(
                            MediaServicesAccountNameTarget,
                            MediaServicesAccountKeyTarget);
        
            // Get server context.    
            _contextSource = new CloudMediaContext(_cachedCredentialsSource);
            _contextTarget = new CloudMediaContext(_cachedCredentialsTarget);
        
            IAsset assetSingleFile = CreateAssetAndUploadSingleFile(_contextSource,
                                        AssetCreationOptions.None,
                                        SingleInputMp4Path);
        
            IJob job = CreateEncodingJob(_contextSource, assetSingleFile);
        
            if (job.State != JobState.Error)
            {
                IAsset sourceOutputAsset = job.OutputMediaAssets[0];
                // Get the locator for Smooth Streaming
                var sourceOriginLocator = GetStreamingOriginLocator(_contextSource, sourceOutputAsset);
        
                Console.WriteLine("Locator Id: {0}", sourceOriginLocator.Id);
                
                // 1.Create a read-only SAS locator for the source asset to have read access to the container in the source Storage account (associated with the source Media Services account)
                var readSasLocator = GetSasReadLocator(_contextSource, sourceOutputAsset);
        
                // 2.Get the container name of the source asset from the read-only SAS locator created in the previous step
                string containerName = (new Uri(readSasLocator.Path)).Segments[1];
        
                // 3.Create a target empty asset in the target Media Services account
                var targetAsset = CreateTargetEmptyAsset(_contextTarget, containerName);
        
                // 4.Create a write SAS locator for the target empty asset to have write access to the container in the target Storage account (associated with the target Media Services account)
                ILocator writeSasLocator = CreateSasWriteLocator(_contextTarget, targetAsset);
        
                // Get asset container name.
                string targetContainerName = (new Uri(writeSasLocator.Path)).Segments[1];
        
                // 5.Copy the blobs in the source container (source asset) to the target container (target empty asset)
                CopyBlobsFromDifferentStorage(containerName, targetContainerName, StorageNameSource, StorageKeySource, StorageNameTarget, StorageKeyTarget);
        
                // 6.Use the CreateFileInfos Media Services REST API to automatically generate all the IAssetFile’s for the target asset. 
                //      This API call is not supported in the current Media Services SDK for .NET. 
                CreateFileInfosForAssetWithRest(_contextTarget, targetAsset, MediaServicesAccountNameTarget, MediaServicesAccountKeyTarget);
        
                // Check if the AssetFiles are now  associated with the asset.
                Console.WriteLine("Asset files assocated with the {0} asset:", targetAsset.Name);
                foreach (var af in targetAsset.AssetFiles)
                {
                    Console.WriteLine(af.Name);
                }
        
                // 7.Copy the Origin locator of the source asset to the target asset by using the same Id
                var replicatedLocatorPath = CreateOriginLocatorWithRest(_contextTarget,
                            MediaServicesAccountNameTarget, MediaServicesAccountKeyTarget,
                            sourceOriginLocator.Id, targetAsset.Id);
        
                // Create a full URL to the manifest file. Use this for playback
                // in streaming media clients. 
                string originalUrlForClientStreaming = sourceOriginLocator.Path + GetPrimaryFile(sourceOutputAsset).Name + "/manifest";
        
                Console.WriteLine("Original Locator Path: {0}\n", originalUrlForClientStreaming);
        
                string replicatedUrlForClientStreaming = replicatedLocatorPath + GetPrimaryFile(sourceOutputAsset).Name + "/manifest";
        
                Console.WriteLine("Replicated Locator Path: {0}", replicatedUrlForClientStreaming);
        
                readSasLocator.Delete();
                writeSasLocator.Delete();
        }

3. <span data-ttu-id="bded0-158">從 Main 呼叫下列方法定義。</span><span class="sxs-lookup"><span data-stu-id="bded0-158">The following method definitions are called from Main.</span></span>

    >[!NOTE]
    ><span data-ttu-id="bded0-159">對於不同的媒體服務原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="bded0-159">There is a limit of 1,000,000 policies for different Media Services policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="bded0-160">如果您總是使用相同的天數和存取權限，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="bded0-160">You should use the same policy ID if you are always using the same days and access permissions.</span></span> <span data-ttu-id="bded0-161">例如，為預定要長時間維持就地 (非上傳原則) 的定位器原則，使用相同的識別碼。</span><span class="sxs-lookup"><span data-stu-id="bded0-161">For example, use the same ID for policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="bded0-162">如需詳細資訊，請參閱[這個主題](media-services-dotnet-manage-entities.md#limit-access-policies)。</span><span class="sxs-lookup"><span data-stu-id="bded0-162">For more information, see [this topic](media-services-dotnet-manage-entities.md#limit-access-policies).</span></span>

        public static IAsset CreateAssetAndUploadSingleFile(CloudMediaContext context,
                                                        AssetCreationOptions assetCreationOptions,
                                                        string singleFilePath)
        {
            var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
   
            var asset = context.Assets.Create(assetName, assetCreationOptions);
   
            Console.WriteLine("Asset name: " + asset.Name);
   
            var fileName = Path.GetFileName(singleFilePath);
   
            var assetFile = asset.AssetFiles.Create(fileName);
   
            Console.WriteLine("Created assetFile {0}", assetFile.Name);
   
            Console.WriteLine("Upload {0}", assetFile.Name);
   
            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);
   
            return asset;
        }
   
        public static IJob CreateEncodingJob(CloudMediaContext context, IAsset asset)
        {
            // Declare a new job.
            IJob job = context.Jobs.Create("My encoding job");
   
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName(context,
                                                    "Media Encoder Standard");
   
            // Create a task with the encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.ProtectedConfiguration);
   
            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
   
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is in the clear (unencrypted). 
            var outputAssetName = "OutputAsset_" + Guid.NewGuid();
            task.OutputAssets.AddNew(outputAssetName,
                AssetCreationOptions.None);
   
            // Use the following event handler to check job progress.  
            job.StateChanged += new
                    EventHandler<JobStateChangedEventArgs>(StateChanged);
   
            // Launch the job.
            job.Submit();
   
            // Optionally log job details. This displays basic job details
            // to the console and saves them to a JobDetails-{JobId}.txt file 
            // in your output folder.
            LogJobDetails(context, job.Id);
   
            // Check job execution and wait for job to finish. 
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
            progressJobTask.Wait();
   
            // Get an updated job reference.
            job = GetJob(context, job.Id);
   
            // Since we the output asset contains a set of Smooth Streaming files,
            // set the .ism file to be the primary file
            if (job.State != JobState.Error)
                SetPrimaryFile(job.OutputMediaAssets[0]);
   
            return job;
        }
   
        public static ILocator GetStreamingOriginLocator(CloudMediaContext context, IAsset assetToStream)
        {
            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset. 
            IAssetFile manifestFile = GetPrimaryFile(assetToStream);
   
            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
   
            IAccessPolicy policy = context.AccessPolicies.Create("Streaming policy",
                TimeSpan.FromDays(30),
                AccessPermissions.Read);
   
            // Create a locator to the streaming content on an origin. 
            ILocator originLocator = context.Locators.CreateLocator(LocatorType.OnDemandOrigin,
                assetToStream,
                policy,
                DateTime.UtcNow.AddMinutes(-5));
   
            // Return the locator. 
            return originLocator;
        }
   
        public static ILocator GetSasReadLocator(CloudMediaContext context, IAsset asset)
        {
            IAccessPolicy accessPolicy = context.AccessPolicies.Create("File Download Policy",
                TimeSpan.FromDays(30), AccessPermissions.Read);
   
            ILocator sasLocator = context.Locators.CreateLocator(LocatorType.Sas,
                asset, accessPolicy);
   
            return sasLocator;
        }
   
        public static ILocator CreateSasWriteLocator(CloudMediaContext context, IAsset asset)
        {
   
            IAccessPolicy writePolicy = context.AccessPolicies.Create("Write Policy",
                TimeSpan.FromDays(30), AccessPermissions.Write);
   
            ILocator sasLocator = context.Locators.CreateLocator(LocatorType.Sas,
                asset, writePolicy);
   
            return sasLocator;
        }
   
        public static IAsset CreateTargetEmptyAsset(CloudMediaContext context, string containerName)
        {
            // Create a new asset.
            IAsset assetToBeProcessed = context.Assets.Create(containerName,
                AssetCreationOptions.None);
   
            return assetToBeProcessed;
        }
   
        public static void CreateFileInfosForAssetWithRest(CloudMediaContext context, IAsset asset, string mediaServicesAccountNameTarget,
            string mediaServicesAccountKeyTarget)
        {
            string apiServer = "";
            string scope = "";
            string acsBaseAddress = "";
   
            string acsToken = GetAcsBearerToken(mediaServicesAccountNameTarget,
                                    mediaServicesAccountKeyTarget, scope, acsBaseAddress);
   
            if (!string.IsNullOrEmpty(acsToken))
            {
                CreateFileInfos(apiServer, acsToken, asset.Id);
            }
        }
   
        public static string CreateOriginLocatorWithRest(CloudMediaContext context, string mediaServicesAccountNameTarget,
            string mediaServicesAccountKeyTarget, string locatorIdToReplicate, string targetAssetId)
        {
            //Make sure we are not asking for a duplicate:
            var locator = context.Locators.Where(l => l.Id == locatorIdToReplicate).FirstOrDefault();
            if (locator != null)
                return "";
   
            string locatorNewPath = "";
            string apiServer = "";
            string scope = "";
            string acsBaseAddress = "";
   
            string acsToken = GetAcsBearerToken(mediaServicesAccountNameTarget,
                                    mediaServicesAccountKeyTarget, scope, acsBaseAddress);
   
            if (!string.IsNullOrEmpty(acsToken))
            {
                var asset = context.Assets.Where(a => a.Id == targetAssetId).FirstOrDefault();
   
                // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
                var accessPolicy = context.AccessPolicies.Create("RestTest", TimeSpan.FromDays(100),
                                                                    AccessPermissions.Read);
                if (asset != null)
                {
                    string redirectedServiceUri = null;
   
                    var xmlResponse = CreateLocator(apiServer, out redirectedServiceUri, acsToken,
                                                                asset.Id, accessPolicy.Id,
                                                                (int)LocatorType.OnDemandOrigin,
                                                                DateTime.UtcNow.AddMinutes(-10), locatorIdToReplicate);
   
                    Console.WriteLine("Redirected to: " + redirectedServiceUri);
                    if (xmlResponse != null)
                    {
                        Console.WriteLine(String.Format("Locator Id: {0}",
                                                        xmlResponse.GetElementsByTagName("Id")[0].InnerText));
                        Console.WriteLine(String.Format("Locator Path: {0}",
                                xmlResponse.GetElementsByTagName("Path")[0].InnerText));

                        locatorNewPath = xmlResponse.GetElementsByTagName("Path")[0].InnerText;
                    }
                }
            }

            return locatorNewPath;
        }

        public static void SetPrimaryFile(IAsset asset)
        {

            var ismAssetFiles = asset.AssetFiles.ToList().
                        Where(f => f.Name.EndsWith(".ism", StringComparison.OrdinalIgnoreCase))
                        .ToArray();

            if (ismAssetFiles.Count() != 1)
                throw new ArgumentException("The asset should have only one, .ism file");

            ismAssetFiles.First().IsPrimary = true;
            ismAssetFiles.First().Update();
        }

        public static IAssetFile GetPrimaryFile(IAsset asset)
        {
            var theManifest =
                    from f in asset.AssetFiles
                    where f.Name.EndsWith(".ism")
                    select f;

            // Cast the reference to a true IAssetFile type. 
            IAssetFile manifestFile = theManifest.First();

            return manifestFile;
        }

        public static IAsset RefreshAsset(CloudMediaContext context, IAsset asset)
        {
            asset = context.Assets.Where(a => a.Id == asset.Id).FirstOrDefault();
            return asset;
        }

        public static void CopyBlobsFromDifferentStorage(string sourceContainerName, string targetContainerName,
                                            string srcAccountName, string srcAccountKey,
                                            string destAccountName, string destAccountKey)
        {
            var srcAccount = new CloudStorageAccount(new StorageCredentials(srcAccountName, srcAccountKey), true);
            var destAccount = new CloudStorageAccount(new StorageCredentials(destAccountName, destAccountKey), true);

            var cloudBlobClient = srcAccount.CreateCloudBlobClient();
            var targetBlobClient = destAccount.CreateCloudBlobClient();

            var sourceContainer = cloudBlobClient.GetContainerReference(sourceContainerName);
            var targetContainer = targetBlobClient.GetContainerReference(targetContainerName);
            targetContainer.CreateIfNotExists();

            string blobToken = sourceContainer.GetSharedAccessSignature(new SharedAccessBlobPolicy()
            {
                // Specify the expiration time for the signature.
                SharedAccessExpiryTime = DateTime.Now.AddDays(1),
                // Specify the permissions granted by the signature.
                Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read
            });

            foreach (var sourceBlob in sourceContainer.ListBlobs())
            {
                string fileName = (sourceBlob as ICloudBlob).Name;
                var sourceCloudBlob = sourceContainer.GetBlockBlobReference(fileName);
                sourceCloudBlob.FetchAttributes();

                if (sourceCloudBlob.Properties.Length > 0)
                {
                    // In Azure Media Services, the files are stored as block blobs. 
                    // Page blobs are not supported by Azure Media Services.  
                    var destinationBlob = targetContainer.GetBlockBlobReference(fileName);
                    destinationBlob.StartCopyFromBlob(new Uri(sourceBlob.Uri.AbsoluteUri + blobToken));

                    while (true)
                    {
                        // The StartCopyFromBlob is an async operation, 
                        // so we want to check if the copy operation is completed before proceeding. 
                        // To do that, we call FetchAttributes on the blob and check the CopyStatus. 
                        destinationBlob.FetchAttributes();
                        if (destinationBlob.CopyState.Status != CopyStatus.Pending)
                        {
                            break;
                        }
                        //It's still not completed. So wait for some time.
                        System.Threading.Thread.Sleep(1000);
                    }
                }

                Console.WriteLine(fileName);
            }

            Console.WriteLine("Done copying.");
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(CloudMediaContext context, string mediaProcessorName)
        {

            var processor = context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        // This method is a handler for events that track job progress.   
        private static void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
                case JobState.Finished:
                    Console.WriteLine();
                    Console.WriteLine("********************");
                    Console.WriteLine("Job is finished.");
                    Console.WriteLine("Please wait while local tasks or downloads complete...");
                    Console.WriteLine("********************");
                    Console.WriteLine();
                    Console.WriteLine();
                    break;
                case JobState.Canceling:
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    Console.WriteLine("Please wait...\n");
                    break;
                case JobState.Canceled:
                case JobState.Error:
                    // Cast sender as a job.
                    IJob job = (IJob)sender;
                    // Display or log error details as needed.
                    LogJobStop(null, job.Id);
                    break;
                default:
                    break;
            }
        }

        private static void LogJobStop(CloudMediaContext context, string jobId)
        {
            StringBuilder builder = new StringBuilder();
            IJob job = GetJob(context, jobId);

            builder.AppendLine("\nThe job stopped due to cancellation or an error.");
            builder.AppendLine("***************************");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Job Name: " + job.Name);
            builder.AppendLine("Job State: " + job.State.ToString());
            builder.AppendLine("Job started (server UTC time): " + job.StartTime.ToString());
            // Log job errors if they exist.  
            if (job.State == JobState.Error)
            {
                builder.Append("Error Details: \n");
                foreach (ITask task in job.Tasks)
                {
                    foreach (ErrorDetail detail in task.ErrorDetails)
                    {
                        builder.AppendLine("  Task Id: " + task.Id);
                        builder.AppendLine("    Error Code: " + detail.Code);
                        builder.AppendLine("    Error Message: " + detail.Message + "\n");
                    }
                }
            }
            builder.AppendLine("***************************\n");
            // Write the output to a local file and to the console. The template 
            // for an error output file is:  JobStop-{JobId}.txt
            string outputFile = OutputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
            WriteToFile(outputFile, builder.ToString());
            Console.Write(builder.ToString());
        }

        private static void LogJobDetails(CloudMediaContext context, string jobId)
        {
            StringBuilder builder = new StringBuilder();
            IJob job = GetJob(context, jobId);

            builder.AppendLine("\nJob ID: " + job.Id);
            builder.AppendLine("Job Name: " + job.Name);
            builder.AppendLine("Job submitted (client UTC time): " + DateTime.UtcNow.ToString());

            // Write the output to a local file and to the console. The template 
            // for an error output file is:  JobDetails-{JobId}.txt
            string outputFile = OutputFilesFolder + @"\JobDetails-" + JobIdAsFileName(job.Id) + ".txt";
            WriteToFile(outputFile, builder.ToString());
            Console.Write(builder.ToString());
        }

        // Replace ":" with "_" in Job id values so they can 
        // be used as log file names.  
        private static string JobIdAsFileName(string jobID)
        {
            return jobID.Replace(":", "_");
        }

        // Write method output to the output files folder.
        private static void WriteToFile(string outFilePath, string fileContent)
        {
            StreamWriter sr = File.CreateText(outFilePath);
            sr.WriteLine(fileContent);
            sr.Close();
        }

        private static IJob GetJob(CloudMediaContext context, string jobId)
        {
            // Use a Linq select query to get an updated 
            // reference by Id. 
            var jobInstance =
                from j in context.Jobs
                where j.Id == jobId
                select j;

            // Return the job reference as an Ijob. 
            IJob job = jobInstance.FirstOrDefault();

            return job;
        }

        private static IAsset GetAsset(CloudMediaContext context, string assetId)
        {
            // Use a LINQ Select query to get an asset.
            var assetInstance =
                from a in context.Assets
                where a.Id == assetId
                select a;

            // Reference the asset as an IAsset.
            IAsset asset = assetInstance.FirstOrDefault();

            return asset;
        }

        public static void DeleteAllAssets(CloudMediaContext context)
        {
            // Loop through and delete all assets.
            foreach (IAsset asset in context.Assets)
            {
                DeleteLocatorsForAsset(context, asset);

                asset.Delete();
            }
        }

        public static void DeleteLocatorsForAsset(CloudMediaContext context, IAsset asset)
        {
            string assetId = asset.Id;
            var locators = from a in context.Locators
                            where a.AssetId == assetId
                            select a;
            foreach (var locator in locators)
            {
                Console.WriteLine("Deleting locator {0} for asset {1}", locator.Path, assetId);

                locator.Delete();
            }
        }

        public static void DeleteAccessPolicy(CloudMediaContext context, string existingPolicyId)
        {
            // To delete a specific access policy, get a reference to the policy.  
            // based on the policy Id passed to the method.
            var policyInstance =
                    from p in context.AccessPolicies
                    where p.Id == existingPolicyId
                    select p;

            IAccessPolicy policy = policyInstance.FirstOrDefault();

            policy.Delete();

        }

        //////////////////////////////////////////////////////
        /// The following methods use REST calls.
        //////////////////////////////////////////////////////

        public static string GetAcsBearerToken(string clientId, string clientSecret, string scope, string accessControlServiceUri)
        {
            if (string.IsNullOrEmpty(clientId))
                throw new ArgumentNullException("clientId");

            if (string.IsNullOrEmpty(clientSecret))
                throw new ArgumentNullException("clientSecret");

            if (string.IsNullOrEmpty(scope))
            {
                scope = "urn:WindowsAzureMediaServices";
            }
            else if (!scope.ToLower().StartsWith("urn:"))
            {
                scope = "urn:" + scope;
            }

            if (string.IsNullOrEmpty(accessControlServiceUri))
            {
                accessControlServiceUri = "https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13";
            }
            else if (!accessControlServiceUri.ToLower().EndsWith("/v2/oauth2-13"))
            {
                accessControlServiceUri = accessControlServiceUri.TrimEnd('/') + "/v2/OAuth2-13";
            }

            HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(accessControlServiceUri);
            request.Method = "POST";
            request.ContentType = "application/x-www-form-urlencoded";
            request.KeepAlive = true;
            string acsBearerToken = null;

            var requestBytes = Encoding.ASCII.GetBytes("grant_type=client_credentials&client_id=" +
                clientId + "&client_secret=" + HttpUtility.UrlEncode(clientSecret) +
                "&scope=" + HttpUtility.UrlEncode(scope));
            request.ContentLength = requestBytes.Length;

            var requestStream = request.GetRequestStream();
            requestStream.Write(requestBytes, 0, requestBytes.Length);
            requestStream.Close();

            var response = (HttpWebResponse)request.GetResponse();

            if (response.StatusCode == HttpStatusCode.OK)
            {
                using (Stream responseStream = response.GetResponseStream())
                {
                    using (StreamReader stream = new StreamReader(responseStream))
                    {
                        string responseString = stream.ReadToEnd();
                        var reader = JsonReaderWriterFactory.CreateJsonReader(Encoding.UTF8.GetBytes(responseString),
                            new XmlDictionaryReaderQuotas());

                        while (reader.Read())
                        {
                            if ((reader.Name == "access_token") && (reader.NodeType == XmlNodeType.Element))
                            {
                                if (reader.Read())
                                {
                                    acsBearerToken = reader.Value;
                                    break;
                                }
                            }
                        }
                    }
                }
            }

            return acsBearerToken;
        }

        public static XmlDocument CreateLocator(string mediaServicesApiServerUri,
                                                out string redirectedMediaServicesApiServerUri,
                                                string acsBearerToken, string assetId,
                                                string accessPolicyId, int locatorType,
                                                DateTime startTime, string locatorIdToReplicate = null,
                                                bool autoRedirect = true)
        {
            if (string.IsNullOrEmpty(mediaServicesApiServerUri))
            {
                mediaServicesApiServerUri = "https://media.windows.net/api/";
            }
            if (!mediaServicesApiServerUri.EndsWith("/"))
                mediaServicesApiServerUri = mediaServicesApiServerUri + "/";

            if (string.IsNullOrEmpty(acsBearerToken)) throw new ArgumentNullException("acsBearerToken");
            if (string.IsNullOrEmpty(assetId)) throw new ArgumentNullException("assetId");
            if (string.IsNullOrEmpty(accessPolicyId)) throw new ArgumentNullException("accessPolicyId");

            redirectedMediaServicesApiServerUri = null;
            XmlDocument xmlResponse = null;

            StringBuilder sb = new StringBuilder();
            sb.Append("{ \"AssetId\" : \"" + assetId + "\"");
            sb.Append(", \"AccessPolicyId\" : \"" + accessPolicyId + "\"");
            sb.Append(", \"Type\" : \"" + locatorType + "\"");
            if (startTime != DateTime.MinValue)
                sb.Append(", \"StartTime\" : \"" + startTime.ToString("G", CultureInfo.CreateSpecificCulture("en-us")) + "\"");
            if (!string.IsNullOrEmpty(locatorIdToReplicate))
                sb.Append(", \"Id\" : \"" + locatorIdToReplicate + "\"");
            sb.Append("}");

            string requestbody = sb.ToString();

            try
            {
                var request = GenerateRequest("POST", mediaServicesApiServerUri, "Locators",
                    null, acsBearerToken, requestbody);
                var response = (HttpWebResponse)request.GetResponse();

                switch (response.StatusCode)
                {
                    case HttpStatusCode.MovedPermanently:
                        //Recurse once with the mediaServicesApiServerUri redirect Location:
                        if (autoRedirect)
                        {
                            redirectedMediaServicesApiServerUri = response.Headers["Location"];
                            string secondRedirection = null;
                            xmlResponse = CreateLocator(redirectedMediaServicesApiServerUri,
                                                        out secondRedirection, acsBearerToken,
                                                        assetId, accessPolicyId, locatorType,
                                                        startTime, locatorIdToReplicate, false);
                        }
                        else
                        {
                            Console.WriteLine("Redirection to {0} failed.",
                                mediaServicesApiServerUri);
                            return null;
                        }
                        break;
                    case HttpStatusCode.Created:
                        using (Stream responseStream = response.GetResponseStream())
                        {
                            using (StreamReader stream = new StreamReader(responseStream))
                            {
                                string responseString = stream.ReadToEnd();
                                var reader = JsonReaderWriterFactory.
                                    CreateJsonReader(Encoding.UTF8.GetBytes(responseString),
                                        new XmlDictionaryReaderQuotas());

                                xmlResponse = new XmlDocument();
                                reader.Read();
                                xmlResponse.LoadXml(reader.ReadInnerXml());
                            }
                        }
                        break;

                    default:
                        Console.WriteLine(response.StatusDescription);
                        break;
                }
            }
            catch (WebException ex)
            {
                Console.WriteLine(ex.Message);
            }

            return xmlResponse;
        }

        public static void CreateFileInfos(string mediaServicesApiServerUri,
                                    string acsBearerToken,
                                    string assetId
                                    )
        {
            if (String.IsNullOrEmpty(mediaServicesApiServerUri))
            {
                mediaServicesApiServerUri = "https://media.windows.net/api/";
            }
            if (!mediaServicesApiServerUri.EndsWith("/"))
                mediaServicesApiServerUri = mediaServicesApiServerUri + "/";

            if (String.IsNullOrEmpty(acsBearerToken)) throw new ArgumentNullException("acsBearerToken");
            if (String.IsNullOrEmpty(assetId)) throw new ArgumentNullException("assetId");


            string id = assetId.Replace(":", "%");

            UriBuilder builder = new UriBuilder(mediaServicesApiServerUri);
            builder.Path = Path.Combine(builder.Path, "CreateFileInfos");
            builder.Query = String.Format(CultureInfo.InvariantCulture, "assetid='{0}'", assetId);

            try
            {
                var request = GenerateRequest("GET", mediaServicesApiServerUri, "CreateFileInfos",
                    String.Format(CultureInfo.InvariantCulture, "assetid='{0}'", assetId), acsBearerToken, null);

                using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                {
                    if (response.StatusCode == HttpStatusCode.MovedPermanently)
                    {
                        string redirectedMediaServicesApiUrl = response.Headers["Location"];

                        CreateFileInfos(redirectedMediaServicesApiUrl, acsBearerToken, assetId);
                    }
                    else if ((response.StatusCode != HttpStatusCode.OK) &&
                        (response.StatusCode != HttpStatusCode.Accepted) &&
                        (response.StatusCode != HttpStatusCode.Created) &&
                        (response.StatusCode != HttpStatusCode.NoContent))
                    {
                        // TODO: Throw a more specific exception.
                        throw new Exception("Invalid response received ");
                    }
                }
            }
            catch (WebException ex)
            {
                Console.WriteLine(ex.Message);
            }
        }

        private static HttpWebRequest GenerateRequest(string verb,
                                                        string mediaServicesApiServerUri,
                                                        string resourcePath, string query,
                                                        string acsBearerToken, string requestbody)
        {
            var uriBuilder = new UriBuilder(mediaServicesApiServerUri);
            uriBuilder.Path += resourcePath;
            if (query != null)
            {
                uriBuilder.Query = query;
            }
            HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(uriBuilder.Uri);
            request.AllowAutoRedirect = false; //We manage our own redirects.
            request.Method = verb;

            if (resourcePath == "$metadata")
                request.MediaType = "application/xml";
            else
            {
                request.ContentType = "application/json;odata=verbose";
                request.Accept = "application/json;odata=verbose";
            }

            request.Headers.Add("DataServiceVersion", "3.0");
            request.Headers.Add("MaxDataServiceVersion", "3.0");
            request.Headers.Add("x-ms-version", "2.1");
            request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + acsBearerToken);

            if (requestbody != null)
            {
                var requestBytes = Encoding.ASCII.GetBytes(requestbody);
                request.ContentLength = requestBytes.Length;

                var requestStream = request.GetRequestStream();
                requestStream.Write(requestBytes, 0, requestBytes.Length);
                requestStream.Close();
            }
            else
            {
                request.ContentLength = 0;
            }
            return request;
        }

## <a name="next-steps"></a><span data-ttu-id="bded0-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bded0-163">Next steps</span></span>
<span data-ttu-id="bded0-164">您現在可以使用流量管理員在兩個資料中心之間路由傳送要求，因此在任何中斷的情況下容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="bded0-164">You can now use a traffic manager to route requests between the two datacenters, and thus fail over in case of any outages.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="bded0-165">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="bded0-165">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bded0-166">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="bded0-166">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


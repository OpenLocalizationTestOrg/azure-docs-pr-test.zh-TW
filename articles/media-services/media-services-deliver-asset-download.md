---
title: "將媒體服務資產下載到您的電腦 - Azure | Microsoft Docs"
description: "了解如何將資產下載到您的電腦。 程式碼範例以 C# 撰寫，並使用 Media Services SDK for .NET。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: d8e740e969f68c85842f42c109328423da1b4414
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="3c5d8-104">作法：透過下載來傳遞資產</span><span class="sxs-lookup"><span data-stu-id="3c5d8-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="3c5d8-105">此主題將討論已上傳至媒體服務的媒體資產有哪些傳遞選項。</span><span class="sxs-lookup"><span data-stu-id="3c5d8-105">This topic discusses options for delivering media assets uploaded to Media Services.</span></span> <span data-ttu-id="3c5d8-106">您可以透過多種應用程式案例來傳遞媒體服務內容。</span><span class="sxs-lookup"><span data-stu-id="3c5d8-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="3c5d8-107">您可以下載媒體資產，或使用定位器加以存取。</span><span class="sxs-lookup"><span data-stu-id="3c5d8-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="3c5d8-108">您可以將媒體內容傳送至另一個應用程式，或是另一個內容提供者。</span><span class="sxs-lookup"><span data-stu-id="3c5d8-108">You can send media content to another application or to another content provider.</span></span> <span data-ttu-id="3c5d8-109">若要改善效能和延展性，您也可以使用內容傳遞網路 (CDN) 傳遞內容。</span><span class="sxs-lookup"><span data-stu-id="3c5d8-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="3c5d8-110">這個範例示範如何從媒體服務下載媒體資產到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="3c5d8-110">This example shows how to download media assets from Media Services to your local computer.</span></span> <span data-ttu-id="3c5d8-111">程式碼會以工作 ID 查詢與媒體服務帳戶相關聯的工作，並存取其 **OutputMediaAssets** 集合 (這是執行工作後所產生的一或多個輸出媒體資產)。</span><span class="sxs-lookup"><span data-stu-id="3c5d8-111">The code queries the jobs associated with the Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is the set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="3c5d8-112">此範例將說明如何從作業下載輸出媒體資產，但您也可以用相同的方式來下載其他資產。</span><span class="sxs-lookup"><span data-stu-id="3c5d8-112">This  example shows how to download output media assets from a job, but you can apply the same approach to download other assets.</span></span>

>[!NOTE]
><span data-ttu-id="3c5d8-113">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="3c5d8-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="3c5d8-114">如果您一律使用相同的日期 / 存取權限，例如，要長時間維持就地 (非上載原則) 的定位器原則，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="3c5d8-114">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="3c5d8-115">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="3c5d8-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download the output asset of the specified job to a local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how to download a single asset. 
        // However, you can iterate through the OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference to the job. 
        IJob job = GetJob(jobId);

        // Get a reference to the first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator to download the asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use the following event handler to check download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="3c5d8-116">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="3c5d8-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3c5d8-117">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="3c5d8-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="3c5d8-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3c5d8-118">See Also</span></span>
[<span data-ttu-id="3c5d8-119">傳遞串流內容</span><span class="sxs-lookup"><span data-stu-id="3c5d8-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)


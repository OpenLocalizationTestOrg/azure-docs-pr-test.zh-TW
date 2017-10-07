---
title: "aaaDownload Media Services 資產 tooyour 電腦 Azure |Microsoft 文件"
description: "深入了解 toodownload 資產 tooyour 電腦。 程式碼範例會以 C# 所撰寫，並使用 hello Media Services SDK for.NET。"
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
ms.openlocfilehash: 6c6e764720caa59d8371178a2682700345f7bc57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="fbc48-104">作法：透過下載來傳遞資產</span><span class="sxs-lookup"><span data-stu-id="fbc48-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="fbc48-105">本主題將討論傳遞媒體資產上傳 tooMedia 服務的選項。</span><span class="sxs-lookup"><span data-stu-id="fbc48-105">This topic discusses options for delivering media assets uploaded tooMedia Services.</span></span> <span data-ttu-id="fbc48-106">您可以透過多種應用程式案例來傳遞媒體服務內容。</span><span class="sxs-lookup"><span data-stu-id="fbc48-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="fbc48-107">您可以下載媒體資產，或使用定位器加以存取。</span><span class="sxs-lookup"><span data-stu-id="fbc48-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="fbc48-108">您可以傳送媒體內容 tooanother 應用程式或 tooanother 內容提供者。</span><span class="sxs-lookup"><span data-stu-id="fbc48-108">You can send media content tooanother application or tooanother content provider.</span></span> <span data-ttu-id="fbc48-109">若要改善效能和延展性，您也可以使用內容傳遞網路 (CDN) 傳遞內容。</span><span class="sxs-lookup"><span data-stu-id="fbc48-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="fbc48-110">這個範例會示範如何從本機電腦的 Media Services tooyour toodownload 媒體資產。</span><span class="sxs-lookup"><span data-stu-id="fbc48-110">This example shows how toodownload media assets from Media Services tooyour local computer.</span></span> <span data-ttu-id="fbc48-111">hello 程式碼查詢 hello 依工作識別碼和存取與 hello Media Services 帳戶相關聯的作業其**Outputmediaasset** （即 hello 一或多個輸出媒體資產所產生的集合從執行的作業） 的集合。</span><span class="sxs-lookup"><span data-stu-id="fbc48-111">hello code queries hello jobs associated with hello Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is hello set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="fbc48-112">這個範例會示範如何 toodownload 輸出媒體資產作業，但您可以套用會 hello 相同方法 toodownload 其他資產。</span><span class="sxs-lookup"><span data-stu-id="fbc48-112">This  example shows how toodownload output media assets from a job, but you can apply hello same approach toodownload other assets.</span></span>

>[!NOTE]
><span data-ttu-id="fbc48-113">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="fbc48-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="fbc48-114">您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。</span><span class="sxs-lookup"><span data-stu-id="fbc48-114">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="fbc48-115">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="fbc48-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download hello output asset of hello specified job tooa local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how toodownload a single asset. 
        // However, you can iterate through hello OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference toohello job. 
        IJob job = GetJob(jobId);

        // Get a reference toohello first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator toodownload hello asset
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
            // Use hello following event handler toocheck download progress.
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="fbc48-116">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="fbc48-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fbc48-117">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="fbc48-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="fbc48-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fbc48-118">See Also</span></span>
[<span data-ttu-id="fbc48-119">傳遞串流內容</span><span class="sxs-lookup"><span data-stu-id="fbc48-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)


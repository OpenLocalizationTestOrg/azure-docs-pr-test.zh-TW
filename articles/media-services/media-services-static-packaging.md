---
title: "aaaUsing Azure Media Packager tooaccomplish 靜態封裝工作 |Microsoft 文件"
description: "本主題說明使用 Azure Media Packager 完成的各種工作。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0582628e-a525-4a78-90ac-9f7fc1cd909f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 64e8ba217bcd3074f5819ac3b74d2969432db5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-media-packager-tooaccomplish-static-packaging-tasks"></a><span data-ttu-id="85a0f-103">使用 Azure Media Packager tooaccomplish 靜態封裝工作</span><span class="sxs-lookup"><span data-stu-id="85a0f-103">Using Azure Media Packager tooaccomplish static packaging tasks</span></span>
> [!NOTE]
> <span data-ttu-id="85a0f-104">Microsoft Azure Media Packager 和 Microsoft Azure Media Encryptor 的生命日期的 hello 結尾已經過擴充 tooMarch 1，2017年。</span><span class="sxs-lookup"><span data-stu-id="85a0f-104">hello end of life date for Microsoft Azure Media Packager and Microsoft Azure Media Encryptor has been extended tooMarch 1, 2017.</span></span> <span data-ttu-id="85a0f-105">此日期之前，這些處理器 hello 功能將會加入 tooMedia 編碼器標準 (MES)。</span><span class="sxs-lookup"><span data-stu-id="85a0f-105">Before that date, hello functionalities of these processors will be added tooMedia Encoder Standard (MES).</span></span> <span data-ttu-id="85a0f-106">客戶將會提供指示 toomigrate 其工作流程 toosend 作業 tooMES。</span><span class="sxs-lookup"><span data-stu-id="85a0f-106">Customers will be provided with instructions on how toomigrate their workflows toosend Jobs tooMES.</span></span> <span data-ttu-id="85a0f-107">格式轉換和加密功能也可透過動態封裝與動態加密進行。</span><span class="sxs-lookup"><span data-stu-id="85a0f-107">Format conversion and encryption capabilities may also be available through dynamic packaging and dynamic encryption.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="85a0f-108">概觀</span><span class="sxs-lookup"><span data-stu-id="85a0f-108">Overview</span></span>
<span data-ttu-id="85a0f-109">在訂單 toodeliver 數位視訊透過 hello hello 的網際網路，您必須壓縮媒體。</span><span class="sxs-lookup"><span data-stu-id="85a0f-109">In order toodeliver digital video over hello internet you must compress hello media.</span></span> <span data-ttu-id="85a0f-110">數位視訊檔案相當大，而可能會太大 toodeliver hello 透過網際網路或您的客戶裝置 toodisplay 正確。</span><span class="sxs-lookup"><span data-stu-id="85a0f-110">Digital video files are quite large and may be too big toodeliver over hello internet or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="85a0f-111">編碼是壓縮視訊和音訊，使您的客戶可以檢視您的媒體 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="85a0f-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span> <span data-ttu-id="85a0f-112">完成視訊編碼後，即可將其放到其他檔案容器中。</span><span class="sxs-lookup"><span data-stu-id="85a0f-112">Once a video has been encoded it can be placed into different file containers.</span></span> <span data-ttu-id="85a0f-113">編碼媒體放到容器的 hello 程序稱為封裝。</span><span class="sxs-lookup"><span data-stu-id="85a0f-113">hello process of placing encoded media into a container is called packaging.</span></span> <span data-ttu-id="85a0f-114">例如，您可以將 MP4 檔案，並將它轉換成 Smooth Streaming 或 HLS 內容中，使用 Azure Media Packager hello。</span><span class="sxs-lookup"><span data-stu-id="85a0f-114">For example, you can take an MP4 file and convert it into Smooth Streaming or HLS content by using hello Azure Media Packager.</span></span> 

<span data-ttu-id="85a0f-115">媒體服務支援靜態和動態封裝。</span><span class="sxs-lookup"><span data-stu-id="85a0f-115">Media Services supports dynamic and static packaging.</span></span> <span data-ttu-id="85a0f-116">使用靜態封裝時您會需要 toocreate 一份您客戶所需的每一種格式的內容。</span><span class="sxs-lookup"><span data-stu-id="85a0f-116">When using static packaging you need toocreate a copy of your content in each format required by your customers.</span></span> <span data-ttu-id="85a0f-117">您只需要動態封裝是 toocreate 包含一組彈性位元速率 MP4 或 Smooth Streaming 檔案的資產。</span><span class="sxs-lookup"><span data-stu-id="85a0f-117">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 or Smooth Streaming files.</span></span> <span data-ttu-id="85a0f-118">然後，根據 hello hello 資訊清單中指定的格式或片段要求，hello 隨選串流伺服器可確保您的使用者所選的 hello 通訊協定接收 hello 資料流。</span><span class="sxs-lookup"><span data-stu-id="85a0f-118">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that your users receive hello stream in hello protocol they have chosen.</span></span> <span data-ttu-id="85a0f-119">如此一來，您只需要 toostore 及支付一種儲存格式和 Media Services 服務中的 hello 檔案將會建立及傳遞 hello 適當的回應，根據用戶端的要求。</span><span class="sxs-lookup"><span data-stu-id="85a0f-119">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

> [!NOTE]
> <span data-ttu-id="85a0f-120">建議 toouse[動態封裝](media-services-dynamic-packaging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="85a0f-120">It is recommended toouse [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>
> 
> 

<span data-ttu-id="85a0f-121">不過，在某些情況下，您需要使用靜態封裝：</span><span class="sxs-lookup"><span data-stu-id="85a0f-121">However, there are some scenarios that require static packaging:</span></span> 

* <span data-ttu-id="85a0f-122">驗證使用外部編碼器 (例如使用第三方編碼器) 編碼的調適型位元速率 MP4。</span><span class="sxs-lookup"><span data-stu-id="85a0f-122">Validating adaptive bitrate MP4s encoded with external encoders (for example, using third party encoders).</span></span>

<span data-ttu-id="85a0f-123">您也可以使用靜態封裝 tooperform hello 下列工作。</span><span class="sxs-lookup"><span data-stu-id="85a0f-123">You can also use static packaging tooperform hello following tasks.</span></span> <span data-ttu-id="85a0f-124">不過，建議您使用 toouse 動態加密。</span><span class="sxs-lookup"><span data-stu-id="85a0f-124">However it is recommended toouse dynamic encryption.</span></span>

* <span data-ttu-id="85a0f-125">使用 playready 靜態加密 tooprotect Smooth 和 MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="85a0f-125">Using static encryption tooprotect your Smooth and MPEG DASH with PlayReady</span></span>
* <span data-ttu-id="85a0f-126">使用 aes-128 靜態加密 tooprotect HLSv3</span><span class="sxs-lookup"><span data-stu-id="85a0f-126">Using static encryption tooprotect HLSv3 with AES-128</span></span>
* <span data-ttu-id="85a0f-127">使用 PlayReady 以靜態加密 tooprotect HLSv3</span><span class="sxs-lookup"><span data-stu-id="85a0f-127">Using static encryption tooprotect HLSv3 with PlayReady</span></span>

## <a name="validating-adaptive-bitrate-mp4s-encoded-with-external-encoders"></a><span data-ttu-id="85a0f-128">驗證使用外部編碼器編碼的調適型位元速率 MP4</span><span class="sxs-lookup"><span data-stu-id="85a0f-128">Validating Adaptive Bitrate MP4s Encoded with External Encoders</span></span>
<span data-ttu-id="85a0f-129">如果您想 toouse 不編碼的彈性位元速率 （多位元速率） MP4 檔案的一組使用 Media Services 編碼器時，您應該驗證檔案，再進一步處理。</span><span class="sxs-lookup"><span data-stu-id="85a0f-129">If you want toouse a set of adaptive bitrate (multi-bitrate) MP4 files that were not encoded with Media Services' encoders, you should validate your files before further processing.</span></span> <span data-ttu-id="85a0f-130">hello Media Services 封裝程式可以驗證包含一組 MP4 檔案的資產，並檢查是否為 hello 資產封裝的 tooSmooth Streaming 或 HLS。</span><span class="sxs-lookup"><span data-stu-id="85a0f-130">hello Media Services Packager can validate an asset that contains a set of MP4 files and check whether hello asset can be packaged tooSmooth Streaming or HLS.</span></span> <span data-ttu-id="85a0f-131">如果 hello 驗證工作失敗，已處理 hello 工作的 hello 工作會完成時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="85a0f-131">If hello validation task fails, hello job that was processing hello task will complete with an error.</span></span> <span data-ttu-id="85a0f-132">hello XML 可定義預設值為 hello 驗證工作可以在 hello hello[工作預設的 Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="85a0f-132">hello XML that defines hello preset for hello validation task can be found in hello [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

> [!NOTE]
> <span data-ttu-id="85a0f-133">使用 hello 媒體編碼器標準 tooproduce 或 hello Media Services 封裝程式 toovalidate 您的內容中順序 tooavoid 執行階段問題。</span><span class="sxs-lookup"><span data-stu-id="85a0f-133">Use hello Media Encoder Standard tooproduce or hello Media Services Packager toovalidate your content in order tooavoid runtime issues.</span></span> <span data-ttu-id="85a0f-134">如果不能 tooparse hello 隨選串流伺服器。 您的來源檔案在執行階段，您會收到 HTTP 1.1 錯誤 「 415 不受支援的媒體類型 」。</span><span class="sxs-lookup"><span data-stu-id="85a0f-134">If hello On-Demand Streaming server is not able tooparse your source files at runtime, you will receive HTTP 1.1 error “415 Unsupported Media Type”.</span></span> <span data-ttu-id="85a0f-135">重複造成 hello 伺服器 toofail tooparse 原始程式檔會影響 hello 隨選串流伺服器的效能，並可能會降低 hello 頻寬可用 tooserving 其他要求。</span><span class="sxs-lookup"><span data-stu-id="85a0f-135">Repeatedly causing hello server toofail tooparse your source files affects performance of hello On-Demand Streaming server and may reduce hello bandwidth available tooserving other requests.</span></span> <span data-ttu-id="85a0f-136">Azure Media Services 提供其隨選串流服務 」; 在服務等級協定 (SLA)不過，如果上面所述的 hello 方式誤用 hello 伺服器無法接受本 SLA。</span><span class="sxs-lookup"><span data-stu-id="85a0f-136">Azure Media Services offers a Service Level Agreement (SLA) on its On-Demand Streaming services; however, this SLA cannot be honored if hello server is misused in hello fashion described above.</span></span>
> 
> 

<span data-ttu-id="85a0f-137">本節說明如何 tooprocess hello 驗證工作。</span><span class="sxs-lookup"><span data-stu-id="85a0f-137">This section shows how tooprocess hello validation task.</span></span> <span data-ttu-id="85a0f-138">它也會示範如何 toosee hello hello 工作隨著 JobStatus.Error 完成狀態和 hello 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="85a0f-138">It also shows how toosee hello status and hello error message of hello job that completes with JobStatus.Error.</span></span>

<span data-ttu-id="85a0f-139">toovalidate 您 MP4 檔案與媒體服務封裝程式，您必須建立您自己的資訊清單 (.ism) 檔案，並將它上傳 hello 原始程式檔連同到 hello Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="85a0f-139">toovalidate your MP4 files with Media Services Packager, you must create your own manifest (.ism) file and upload it together with hello source files into hello Media Services account.</span></span> <span data-ttu-id="85a0f-140">以下是 hello hello 標準媒體編碼器所產生的.ism 檔案範例。</span><span class="sxs-lookup"><span data-stu-id="85a0f-140">Below is a sample of hello .ism file produced by hello Media Encoder Standard.</span></span> <span data-ttu-id="85a0f-141">hello 檔案名稱不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="85a0f-141">hello file names are case sensitive.</span></span> <span data-ttu-id="85a0f-142">此外，請確定 hello.ism 檔案中的 hello 文字以 utf-8 編碼。</span><span class="sxs-lookup"><span data-stu-id="85a0f-142">Also, make sure hello text in hello .ism file is encoded with UTF-8.</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
    <!-- Tells hello server that these input files are MP4s – specific tooDynamic Packaging -->
        <meta name="formats" content="mp4" /> 
      </head>
      <body>
        <switch>
          <video src="BigBuckBunny_1000.mp4" />
          <video src="BigBuckBunny_1500.mp4" />
          <video src="BigBuckBunny_2250.mp4" />
          <video src="BigBuckBunny_3400.mp4" />
          <video src="BigBuckBunny_400.mp4" />
          <video src="BigBuckBunny_650.mp4" />
          <audio src="BigBuckBunny_400.mp4" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="85a0f-143">一旦您擁有 hello 自動調整位元速率 MP4 集您可以利用動態封裝。</span><span class="sxs-lookup"><span data-stu-id="85a0f-143">Once you have hello adaptive bitrate MP4 set you can take advantage of Dynamic Packaging.</span></span> <span data-ttu-id="85a0f-144">動態封裝可讓您指定的 hello toodeliver 資料流通訊協定，而不需要進一步封裝。</span><span class="sxs-lookup"><span data-stu-id="85a0f-144">Dynamic Packaging allows you toodeliver streams in hello specified protocol without further packaging.</span></span> <span data-ttu-id="85a0f-145">如需詳細資訊，請參閱 [動態封裝](media-services-dynamic-packaging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="85a0f-145">For more information, see [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="85a0f-146">下列程式碼範例會使用 Azure Media Services.NET SDK Extensions hello。</span><span class="sxs-lookup"><span data-stu-id="85a0f-146">hello following code sample uses Azure Media Services .NET SDK Extensions.</span></span>  <span data-ttu-id="85a0f-147">請確定 tooupdate hello 程式碼 toopoint toohello 您輸入的 MP4 檔案和.ism 檔案所在資料夾。</span><span class="sxs-lookup"><span data-stu-id="85a0f-147">Make sure tooupdate hello code toopoint toohello folder where your input MP4 files and .ism file are located.</span></span> <span data-ttu-id="85a0f-148">而且也 toowhere MediaPackager_ValidateTask.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="85a0f-148">And also toowhere your MediaPackager_ValidateTask.xml file is located.</span></span> <span data-ttu-id="85a0f-149">[Azure Media Packager 工作預設值](http://msdn.microsoft.com/library/azure/hh973635.aspx) 主題中已說明此 XML 檔案的定義。</span><span class="sxs-lookup"><span data-stu-id="85a0f-149">This XML file is defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Xml.Linq;

    namespace MediaServicesStaticPackaging
    {
        class Program
        {
            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            // hello MultibitrateMP4Files folder should also
            // contain hello .ism manifest file.
            private static readonly string _multibitrateMP4s =
                Path.Combine(_mediaFiles, @"MultibitrateMP4Files");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations";

            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServicesAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServicesAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Use hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Ingest a set of multibitrate MP4s.
                //
                // Use hello SDK extension method toocreate a new asset by 
                // uploading files from a local directory.
                IAsset multibitrateMP4sAsset = _context.Assets.CreateFromFolder(
                    _multibitrateMP4s,
                    AssetCreationOptions.None,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                // Use Azure Media Packager toovalidate hello files.
                IAsset validatedMP4s =
                    ValidateMultibitrateMP4s(multibitrateMP4sAsset);

                // Publish hello asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    validatedMP4s,
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                                     // Get hello streaming URLs.
                Console.WriteLine("Smooth Streaming URL:");
                Console.WriteLine(validatedMP4s.GetSmoothStreamingUri().ToString());
                Console.WriteLine("MPEG DASH URL:");
                Console.WriteLine(validatedMP4s.GetMpegDashUri().ToString());
                Console.WriteLine("HLS URL:");
                Console.WriteLine(validatedMP4s.GetHlsUri().ToString());
            }

            public static IAsset ValidateMultibitrateMP4s(IAsset multibitrateMP4sAsset)
            {
                // Set .ism as a primary file 
                // in a multibitrate MP4 set.
                SetISMFileAsPrimary(multibitrateMP4sAsset);

                // Create a new job.
                IJob job = _context.Jobs.Create("MP4 validation and converstion tooSmooth Stream job.");

                // Read hello task configuration data into a string. 
                string configMp4Validation = File.ReadAllText(Path.Combine(
                        _configurationXMLFiles,
                        "MediaPackager_ValidateTask.xml"));

                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Create a task with hello conversion details, using hello configuration data. 
                ITask task = job.Tasks.AddNew("Mp4 Validation Task",
                    processor,
                    configMp4Validation,
                    TaskOptions.None);

                // Specify hello input asset toobe validated.
                task.InputAssets.Add(multibitrateMP4sAsset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted). 
                task.OutputAssets.AddNew("Validated output asset",
                        AssetCreationOptions.None);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // If hello validation task fails and job completes with JobState.Error,
                // display hello error message and throw an exception.
                if (job.State == JobState.Error)
                {
                    Console.WriteLine("  Job ID: " + job.Id);
                    Console.WriteLine("  Name: " + job.Name);
                    Console.WriteLine("  State: " + job.State);

                    foreach (var jobTask in job.Tasks)
                    {
                        Console.WriteLine("  Task Id: " + jobTask.Id);
                        Console.WriteLine("  Name: " + jobTask.Name);
                        Console.WriteLine("  Progress: " + jobTask.Progress);
                        Console.WriteLine("  Configuration: " + jobTask.Configuration);
                        Console.WriteLine("  Running time: " + jobTask.RunningDuration);
                        if (jobTask.ErrorDetails != null)
                        {
                            foreach (var errordetail in jobTask.ErrorDetails)
                            {

                                Console.WriteLine("  Error Message:" + errordetail.Message);
                                Console.WriteLine("  Error Code:" + errordetail.Code);
                            }
                        }
                    }
                    throw new Exception("hello specified multi-bitrate MP4 set is not valid.");
                }


                return job.OutputMediaAssets[0];
            }

            static void SetISMFileAsPrimary(IAsset asset)
            {
                var ismAssetFiles = asset.AssetFiles.ToList().
                    Where(f => f.Name.EndsWith(".ism", StringComparison.OrdinalIgnoreCase)).ToArray();

                // hello following code assigns hello first .ism file as hello primary file in hello asset.
                // An asset should have one .ism file.  
                ismAssetFiles.First().IsPrimary = true;
                ismAssetFiles.First().Update();
            }
        }
    }

## <a name="using-static-encryption-tooprotect-your-smooth-and-mpeg-dash-with-playready"></a><span data-ttu-id="85a0f-150">使用 playready 靜態加密 tooProtect Smooth 和 MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="85a0f-150">Using Static Encryption tooProtect your Smooth and MPEG DASH with PlayReady</span></span>
<span data-ttu-id="85a0f-151">如果您想 tooprotect 您使用 PlayReady 的內容，您可以選擇使用[動態加密](media-services-protect-with-drm.md)(hello 建議選項) 或靜態加密 （如本節所述）。</span><span class="sxs-lookup"><span data-stu-id="85a0f-151">If you want tooprotect your content with PlayReady, you have a choice of using [dynamic encryption](media-services-protect-with-drm.md) (hello recommended option) or static encryption (as described in this section).</span></span>

<span data-ttu-id="85a0f-152">本節中的 hello 範例會將夾層檔 （在此情況下 MP4） 編碼成彈性位元速率 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="85a0f-152">hello example in this section encodes a mezzanine file (in this case MP4) into adaptive bitrate MP4 files.</span></span> <span data-ttu-id="85a0f-153">接著，該範例會將 MP4 封裝為 Smooth Streaming，然後使用 PlayReady 將其加密。</span><span class="sxs-lookup"><span data-stu-id="85a0f-153">It then packages MP4s into Smooth Streaming and then encrypts Smooth Streaming with PlayReady.</span></span> <span data-ttu-id="85a0f-154">如此一來您就可以 toostream Smooth Streaming 或 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="85a0f-154">As a result you are able toostream Smooth Streaming or MPEG DASH.</span></span>

<span data-ttu-id="85a0f-155">媒體服務現在提供一種服務，來傳遞 Microsoft PlayReady 授權。</span><span class="sxs-lookup"><span data-stu-id="85a0f-155">Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="85a0f-156">hello 本文範例示範如何 tooconfigure hello Media Services PlayReady 授權傳遞服務 （請參閱以下的 hello 程式碼中定義的 hello ConfigureLicenseDeliveryService 方法）。</span><span class="sxs-lookup"><span data-stu-id="85a0f-156">hello example in this article shows how tooconfigure hello Media Services PlayReady license delivery service (see hello ConfigureLicenseDeliveryService method defined in hello code below).</span></span> <span data-ttu-id="85a0f-157">如需關於媒體服務 PlayReady 授權傳遞服務的詳細資訊，請參閱 [使用 PlayReady 動態加密和授權傳遞服務](media-services-protect-with-drm.md)。</span><span class="sxs-lookup"><span data-stu-id="85a0f-157">For more information about Media Services PlayReady license delivery service, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="85a0f-158">以 PlayReady 加密的 MPEG DASH toodeliver 設定藉此確定 toouse CENC 選項 hello 方法是將 useSencBox 和 adjustSubSamples 屬性 (hello 中所述[工作預設的 Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx)主題) tootrue。</span><span class="sxs-lookup"><span data-stu-id="85a0f-158">toodeliver MPEG DASH encrypted with PlayReady, make sure toouse CENC options by setting hello useSencBox and adjustSubSamples properties (described in hello [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic) tootrue.</span></span>  
> 
> 

<span data-ttu-id="85a0f-159">請確定下列程式碼 toopoint toohello 資料夾位於您輸入的 MP4 檔案所在的 tooupdate hello。</span><span class="sxs-lookup"><span data-stu-id="85a0f-159">Make sure tooupdate hello following code toopoint toohello folder where your input MP4 file is located.</span></span>

<span data-ttu-id="85a0f-160">以及也 toowhere MediaPackager_MP4ToSmooth.xml 和 MediaEncryptor_PlayReadyProtection.xml 檔案的所在。</span><span class="sxs-lookup"><span data-stu-id="85a0f-160">And also toowhere your MediaPackager_MP4ToSmooth.xml and MediaEncryptor_PlayReadyProtection.xml files are located.</span></span> <span data-ttu-id="85a0f-161">中所定義的 MediaPackager_MP4ToSmooth.xml[為 Azure Media Packager 預設工作](http://msdn.microsoft.com/library/azure/hh973635.aspx)而 MediaEncryptor_PlayReadyProtection.xml 定義在 hello[為 Azure Media Encryptor 預設工作](http://msdn.microsoft.com/library/azure/hh973610.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="85a0f-161">MediaPackager_MP4ToSmooth.xml is defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) and MediaEncryptor_PlayReadyProtection.xml is defined in hello [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic.</span></span> 

<span data-ttu-id="85a0f-162">hello 範例會定義您可以使用 toodynamically 更新 hello MediaEncryptor_PlayReadyProtection.xml 檔案 hello UpdatePlayReadyConfigurationXMLFile 方法。</span><span class="sxs-lookup"><span data-stu-id="85a0f-162">hello example defines hello UpdatePlayReadyConfigurationXMLFile method that you can use toodynamically update hello MediaEncryptor_PlayReadyProtection.xml file.</span></span> <span data-ttu-id="85a0f-163">如果您擁有 hello 金鑰種子可用時，您可以使用 hello CommonEncryption.GeneratePlayReadyContentKey 方法 toogenerate hello 內容金鑰 hello keySeedValue 和 KeyId 為基礎。</span><span class="sxs-lookup"><span data-stu-id="85a0f-163">If you have hello key seed available, you can use hello CommonEncryption.GeneratePlayReadyContentKey method toogenerate hello content key based on hello keySeedValue and KeyId values.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Xml.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace PlayReadyStaticEncryptAndKeyDeliverySvc
    {
        class Program
        {

            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
                Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations\";


            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServiceAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServiceAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Use hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Encoding and encrypting assets //////////////////////
                // Load a single MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file tooa set of multibitrate MP4s.
                // Then, package a set of MP4s tooclear Smooth Streaming.
                IAsset clearSmoothStreamAsset =
                    ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create a common encryption content key that is used 
                // a) tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
                //    that is used for encryption.
                // b) tooconfigure hello license delivery service and 
                //
                Guid keyId;
                byte[] contentKey;

                IContentKey key = CreateCommonEncryptionKey(out keyId, out contentKey);

                // hello content key authorization policy must be configured by you 
                // and met by hello client in order for hello PlayReady license
                // toobe delivered toohello client. 
                // In this example hello Media Services PlayReady license delivery service is used.
                ConfigureLicenseDeliveryService(key);

                // Get hello Media Services PlayReady license delivery URL.
                // This URL will be assigned toohello licenseAcquisitionUrl property 
                // of hello MediaEncryptor_PlayReadyProtection.xml file.
                Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

                // Update hello MediaEncryptor_PlayReadyProtection.xml file with hello key and URL info.
                UpdatePlayReadyConfigurationXMLFile(keyId, contentKey, acquisitionUrl);


                // Encrypt your clear Smooth Streaming tooSmooth Streaming with PlayReady.
                IAsset outputAsset = CreateSmoothStreamEncryptedWithPlayReady(clearSmoothStreamAsset);


                // You can use hello http://smf.cloudapp.net/healthmonitor player 
                // tootest hello smoothStreamURL URL.
                string smoothStreamURL = outputAsset.GetSmoothStreamingUri().ToString();
                Console.WriteLine("Smooth Streaming URL:");
                Console.WriteLine(smoothStreamURL);

                // You can use hello http://dashif.org/reference/players/javascript/ player 
                // tootest hello dashURL URL.
                string dashURL = outputAsset.GetMpegDashUri().ToString();
                Console.WriteLine("MPEG DASH URL:");
                Console.WriteLine(dashURL);
            }

            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 toomultibitrate MP4s,
            /// 2 task - packages MP4s tooSmooth Streaming.
            /// </summary>
            /// <returns>hello output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 tooSmooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set tooClear Smooth Stream.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get hello output asset that contains hello Smooth Streaming asset.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Encrypts Smooth Stream with PlayReady.
            /// Then creates a Smooth Streaming Url.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>hello output asset.</returns>
            public static IAsset CreateSmoothStreamEncryptedWithPlayReady(IAsset clearSmoothStreamAsset)
            {
                // Create a job.
                IJob job = _context.Jobs.Create("Encrypt tooPlayReady Smooth Streaming.");

                // Add task 1 - Encrypt Smooth Streaming with PlayReady 
                IAsset encryptedSmoothAsset =
                    EncryptSmoothStreamWithPlayReadyTask(job, clearSmoothStreamAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // hello OutputMediaAssets[0] contains hello desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[0],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[0];
            }

            /// <summary>
            /// Create a common encryption content key that is used 
            /// tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
            /// that is used for encryption.
            /// </summary>
            /// <param name="keyId"></param>
            /// <param name="contentKey"></param>
            /// <returns></returns>
            public static IContentKey CreateCommonEncryptionKey(out Guid keyId, out byte[] contentKey)
            {
                keyId = Guid.NewGuid();
                contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            /// <summary>
            /// Update your configuration .xml file dynamically.
            /// </summary>
            public static void UpdatePlayReadyConfigurationXMLFile(Guid keyId, byte[] keyValue, Uri licenseAcquisitionUrl)
            {
                string xmlFileName = Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml");

                XNamespace xmlns = "http://schemas.microsoft.com/iis/media/v4/TM/TaskDefinition#";

                // Prepare hello encryption task template
                XDocument doc = XDocument.Load(xmlFileName);

                var licenseAcquisitionUrlEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "licenseAcquisitionUrl")
                        .FirstOrDefault();
                var contentKeyEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "contentKey")
                        .FirstOrDefault();
                var keyIdEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "keyId")
                        .FirstOrDefault();

                // Update hello "value" property.
                if (licenseAcquisitionUrlEl != null)
                    licenseAcquisitionUrlEl.Attribute("value").SetValue(licenseAcquisitionUrl.ToString());

                if (contentKeyEl != null)
                    contentKeyEl.Attribute("value").SetValue(Convert.ToBase64String(keyValue));

                if (keyIdEl != null)
                    keyIdEl.Attribute("value").SetValue(keyId);

                doc.Save(xmlFileName);
            }

            /// <summary>
            /// Uploads a single file.
            /// </summary>
            /// <param name="fileDir">hello location of hello files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify hello following encryption options for hello AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded tooAzure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: hello files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use hello SDK extension method toocreate a new asset by 
                // uploading a mezzanine file from a local path.
                IAsset asset = _context.Assets.CreateFromFile(
                    fileDir,
                    assetCreationOptions,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                return asset;
            }

            /// <summary>
            /// Creates a task tooencode tooAdaptive Bitrate. 
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncodeMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 tooAdaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify hello input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s",
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task tooconvert hello MP4 file(s) tooa Smooth Streaming asset.
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles,
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task tooconvert adaptive bitrate tooSmooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 tooSmooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify hello input Asset, which is hello output Asset from hello first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset smoothOutputAsset =
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Stream",
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }


            /// <summary>
            /// Creates a task tooencrypt Smooth Streaming with PlayReady.
            /// Note: toodeliver DASH, make sure tooset hello useSencBox and adjustSubSamples 
            /// configuration properties tootrue. 
            /// In this example, MediaEncryptor_PlayReadyProtection.xml contains configuration.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncryptSmoothStreamWithPlayReadyTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Encryptor.
                IMediaProcessor playreadyProcessor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaEncryptor);

                // Read hello configuration XML.
                //
                // Note that hello configuration defined in MediaEncryptor_PlayReadyProtection.xml
                // is using keySeedValue. It is recommended that you do this only for testing 
                // and not in production. For more information, see 
                // http://msdn.microsoft.com/library/windowsazure/dn189154.aspx.
                //
                string configPlayReady = File.ReadAllText(Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml"));

                ITask playreadyTask = job.Tasks.AddNew("My PlayReady Task",
                   playreadyProcessor,
                   configPlayReady,
                   TaskOptions.ProtectedConfiguration);

                playreadyTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.CommonEncryptionProtected.
                IAsset playreadyAsset = playreadyTask.OutputAssets.AddNew(
                                                "PlayReady Smooth Streaming",
                                                AssetCreationOptions.CommonEncryptionProtected);

                return playreadyAsset;
            }

            /// <summary>
            /// Configures authorization policy for hello content key. 
            /// </summary>
            /// <param name="contentKey">hello content key.</param>
            static public void ConfigureLicenseDeliveryService(IContentKey contentKey)
            {
                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                    new ContentKeyAuthorizationPolicyRestriction 
                    { 
                        Name = "Open", 
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                        Requirements = null
                    }
                };

                // Configure PlayReady license template.
                string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                IContentKeyAuthorizationPolicyOption policyOption =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, newLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(policyOption);

                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            static private string ConfigurePlayReadyLicenseTemplate()
            {
                // hello following code configures PlayReady License Template using .NET classes
                // and returns hello XML string.

                PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }

            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }
        }
    }

## <a name="using-static-encryption-tooprotect-hlsv3-with-aes-128"></a><span data-ttu-id="85a0f-164">使用 aes-128 靜態加密 tooProtect HLSv3</span><span class="sxs-lookup"><span data-stu-id="85a0f-164">Using Static Encryption tooProtect HLSv3 with AES-128</span></span>
<span data-ttu-id="85a0f-165">如果您想 tooencrypt HLS 以 AES 128 時，您可以選擇使用動態加密 (建議選項 hello) 或靜態加密 （如本節所示）。</span><span class="sxs-lookup"><span data-stu-id="85a0f-165">If you want tooencrypt your HLS with AES-128, you have a choice of using dynamic encryption (hello recommended option) or static encryption (as shown in this section).</span></span> <span data-ttu-id="85a0f-166">如果您決定 toouse 動態加密，請參閱[使用 aes-128 動態加密和金鑰傳遞服務](media-services-protect-with-aes128.md)。</span><span class="sxs-lookup"><span data-stu-id="85a0f-166">If you decide toouse dynamic encryption, see [Using AES-128 Dynamic Encryption and Key Delivery Service](media-services-protect-with-aes128.md).</span></span>

> [!NOTE]
> <span data-ttu-id="85a0f-167">若要 tooconvert 您的內容為 HLS，您必須先轉換/編碼您的內容為 Smooth Streaming。</span><span class="sxs-lookup"><span data-stu-id="85a0f-167">In order tooconvert your content into HLS, you must first convert/encode your content into Smooth Streaming.</span></span>
> <span data-ttu-id="85a0f-168">此外，hello HLS 以 AES 加密 tooget 請確定 tooset hello 下列 MediaPackager_SmoothToHLS.xml 檔案中的屬性： 組 hello 加密屬性 tootrue、 hello 機碼值組和 hello keyuri 值 toopoint tooyour authentication\授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="85a0f-168">Also, for hello HLS tooget encrypted with AES make sure tooset hello following properties in your MediaPackager_SmoothToHLS.xml file: set hello encrypt property tootrue, set hello key value, and hello keyuri value toopoint tooyour authentication\authorization server.</span></span>
> <span data-ttu-id="85a0f-169">媒體服務會建立金鑰檔案，並將它放在 hello 資產容器中。</span><span class="sxs-lookup"><span data-stu-id="85a0f-169">Media Services will create a key file and place it in hello asset container.</span></span> <span data-ttu-id="85a0f-170">您應該複製 hello /asset-containerguid/*.key 檔案 tooyour 伺服器 （或建立您自己金鑰的檔案），然後從 hello 資產容器刪除 hello *.key 檔案。</span><span class="sxs-lookup"><span data-stu-id="85a0f-170">You should copy hello /asset-containerguid/*.key file tooyour server (or create your own key file) and then delete hello *.key file from hello asset container.</span></span>
> 
> 

<span data-ttu-id="85a0f-171">本節中的 hello 範例會編碼夾層檔 （在此情況下 MP4） 為多位元速率 MP4 檔案，然後將 mp4 封裝為 Smooth Streaming。</span><span class="sxs-lookup"><span data-stu-id="85a0f-171">hello example in this section encodes a mezzanine file (in this case MP4) into multibitrate MP4 files and then packages MP4s into Smooth Streaming.</span></span> <span data-ttu-id="85a0f-172">接著，該範例會將 Smooth Streaming 封裝為 HTTP Live Streaming (HLS)，該格式使用進階加密標準 (AES) 128 位元串流加密進行加密。</span><span class="sxs-lookup"><span data-stu-id="85a0f-172">It then packages Smooth Streaming into HTTP Live Streaming (HLS) encrypted with Advanced Encryption Standard (AES) 128-bit stream encryption.</span></span> <span data-ttu-id="85a0f-173">請確定下列程式碼 toopoint toohello 資料夾位於您輸入的 MP4 檔案所在的 tooupdate hello。</span><span class="sxs-lookup"><span data-stu-id="85a0f-173">Make sure tooupdate hello following code toopoint toohello folder where your input MP4 file is located.</span></span> <span data-ttu-id="85a0f-174">和也 toowhere 您 MediaPackager_MP4ToSmooth.xml 和 MediaPackager_SmoothToHLS.xml 設定檔的位置。</span><span class="sxs-lookup"><span data-stu-id="85a0f-174">And also toowhere your MediaPackager_MP4ToSmooth.xml and MediaPackager_SmoothToHLS.xml configuration files are located.</span></span> <span data-ttu-id="85a0f-175">您可以在 hello 找到這些檔案的 hello 定義[工作預設的 Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="85a0f-175">You can find hello definition for these files in hello [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Xml.Linq;

    namespace MediaServicesContentProtection
    {
        class Program
        {
            // Paths toosupport files (within hello above base path). You can use 
            // hello provided sample media files from hello "SupportFiles" folder, or 
            // provide paths tooyour own media files below toorun these samples.

            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
                Path.Combine(_mediaFiles, @"SingleMP4\BigBuckBunny.mp4");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations\";

            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName = 
                ConfigurationManager.AppSettings["MediaServiceAccountName"];
            private static readonly string _mediaServicesAccountKey = 
                ConfigurationManager.AppSettings["MediaServiceAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName, 
                                _mediaServicesAccountKey);
                // Use hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Encoding and encrypting assets //////////////////////

                // Load an MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file tooa set of multibitrate MP4s.
                // Then, package a set of MP4s tooclear Smooth Streaming.
                IAsset clearSmoothStreamAsset = ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create HLS encrypted with AES.
                IAsset HLSEncryptedWithAESAsset = CreateHLSEncryptedWithAES(clearSmoothStreamAsset);

                // You can use hello following player tootest hello HLS with AES stream.
                // http://apps.microsoft.com/windows/app/3ivx-hls-player/f79ce7d0-2993-4658-bc4e-83dc182a0614 
                string hlsWithAESURL = HLSEncryptedWithAESAsset.GetHlsUri().ToString();
                Console.WriteLine("HLS with AES URL:");
                Console.WriteLine(hlsWithAESURL);
            }


            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 toomultibitrate MP4s,
            /// 2 task - packages MP4s tooSmooth Streaming.
            /// </summary>
            /// <returns>hello output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 tooSmooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeSingleMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set tooClear Smooth Streaming.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get hello output asset that contains Smooth Streaming.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Encrypts an HLS with AES-128.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>hello output asset.</returns>
            public static IAsset CreateHLSEncryptedWithAES(IAsset clearSmoothStreamAsset)
            {
                IJob job = _context.Jobs.Create("Encrypt tooHLS with AES.");

                // Add task 1 - Package clear Smooth Streaming tooHLS with AES.
                PackageSmoothStreamToHLS(job, clearSmoothStreamAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // hello OutputMediaAssets[0] contains hello desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[0],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[0];
            }

            /// <summary>
            /// Uploads a single file.
            /// </summary>
            /// <param name="fileDir">hello location of hello files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify hello following encryption options for hello AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded tooAzure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: hello files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use hello SDK extension method toocreate a new asset by 
                // uploading a mezzanine file from a local path.
                IAsset asset = _context.Assets.CreateFromFile(
                    fileDir,
                    assetCreationOptions,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                return asset;
            }

            /// <summary>
            /// Creates a task tooencode tooAdaptive Bitrate. 
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncodeSingleMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 tooAdaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify hello input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s", 
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task tooconvert hello MP4 file(s) tooa Smooth Streaming asset.
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles, 
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task tooconvert adaptive bitrate tooSmooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 tooSmooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify hello input Asset, which is hello output Asset from hello first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset smoothOutputAsset = 
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Streaming", 
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }

            /// <summary>
            /// Converts Smooth Streaming tooHLS.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello Smooth Streaming asset.</param>
            /// <returns>hello asset that was packaged tooHLS.</returns>
            private static IAsset PackageSmoothStreamToHLS(IJob job, IAsset smoothStreamAsset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Read hello configuration data into a string. 
                // For hello HLS tooget encrypted with AES make sure tooset the
                // encrypt configuration property tootrue.
                //
                // In production, it is recommended toodo hello following:
                //    Set a Key url for your authn/authz server.
                //    Copy hello /asset-containerguid/*.key file tooyour server (or craft a key file for yourself).
                //    Delete *.key from hello asset container.
                //
                string configuration = File.ReadAllText(Path.Combine(_configurationXMLFiles, @"MediaPackager_SmoothToHLS.xml"));

                // Create a task with hello encoding details, using a configuration file.
                ITask task = job.Tasks.AddNew("My Smooth Streaming tooHLS Task",
                   processor,
                   configuration,
                   TaskOptions.ProtectedConfiguration);

                // Specify hello input asset toobe encoded.
                task.InputAssets.Add(smoothStreamAsset);

                // Add an output asset toocontain hello results of hello job. 
                IAsset outputAsset = 
                    task.OutputAssets.AddNew("HLS asset", AssetCreationOptions.None);


                return outputAsset;
            }
        }
    }

## <a name="using-static-encryption-tooprotect-hlsv3-with-playready"></a><span data-ttu-id="85a0f-176">使用 PlayReady 以靜態加密 tooProtect HLSv3</span><span class="sxs-lookup"><span data-stu-id="85a0f-176">Using Static Encryption tooProtect HLSv3 with PlayReady</span></span>
<span data-ttu-id="85a0f-177">如果您想 tooprotect 您使用 PlayReady 的內容，您可以選擇使用[動態加密](media-services-protect-with-drm.md)(hello 建議選項) 或靜態加密 （如本節所述）。</span><span class="sxs-lookup"><span data-stu-id="85a0f-177">If you want tooprotect your content with PlayReady, you have a choice of using [dynamic encryption](media-services-protect-with-drm.md) (hello recommended option) or static encryption (as described in this section).</span></span>

> [!NOTE]
> <span data-ttu-id="85a0f-178">順序 tooprotect 在您使用 PlayReady 的內容您必須先轉換/編碼您的內容轉換為 Smooth Streaming 格式。</span><span class="sxs-lookup"><span data-stu-id="85a0f-178">In order tooprotect your content using PlayReady you must first convert/encode your content into a Smooth Streaming format.</span></span>
> 
> 

<span data-ttu-id="85a0f-179">本節中的 hello 範例會編碼夾層檔 （在此情況下 MP4） 為多位元速率 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="85a0f-179">hello example in this section encodes a mezzanine file (in this case MP4) into multibitrate MP4 files.</span></span> <span data-ttu-id="85a0f-180">接著，該範例會將 MP4 封裝為 Smooth Streaming，然後使用 PlayReady 將其加密。</span><span class="sxs-lookup"><span data-stu-id="85a0f-180">It then packages MP4s into Smooth Streaming and encrypts Smooth Streaming with PlayReady.</span></span> <span data-ttu-id="85a0f-181">tooproduce HTTP Live Streaming (HLS) 以 PlayReady 加密，hello PlayReady Smooth Streaming 資產需要封裝為 HLS toobe。</span><span class="sxs-lookup"><span data-stu-id="85a0f-181">tooproduce HTTP Live Streaming (HLS) encrypted with PlayReady, hello PlayReady Smooth Streaming asset needs toobe packaged into HLS.</span></span> <span data-ttu-id="85a0f-182">本主題示範如何 tooperform 所有這些步驟。</span><span class="sxs-lookup"><span data-stu-id="85a0f-182">This topic demonstrates how tooperform all these steps.</span></span>

<span data-ttu-id="85a0f-183">媒體服務現在提供一種服務，來傳遞 Microsoft PlayReady 授權。</span><span class="sxs-lookup"><span data-stu-id="85a0f-183">Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="85a0f-184">hello 本文範例示範如何 tooconfigure hello Media Services PlayReady 授權傳遞服務 (請參閱 hello **ConfigureLicenseDeliveryService** hello 的下列程式碼中定義的方法)。</span><span class="sxs-lookup"><span data-stu-id="85a0f-184">hello example in this article shows how tooconfigure hello Media Services PlayReady license delivery service (see hello **ConfigureLicenseDeliveryService** method defined in hello code below).</span></span> 

<span data-ttu-id="85a0f-185">請確定下列程式碼 toopoint toohello 資料夾位於您輸入的 MP4 檔案所在的 tooupdate hello。</span><span class="sxs-lookup"><span data-stu-id="85a0f-185">Make sure tooupdate hello following code toopoint toohello folder where your input MP4 file is located.</span></span> <span data-ttu-id="85a0f-186">以及也 toowhere MediaPackager_MP4ToSmooth.xml、 MediaPackager_SmoothToHLS.xml 和 MediaEncryptor_PlayReadyProtection.xml 檔案的所在。</span><span class="sxs-lookup"><span data-stu-id="85a0f-186">And also toowhere your MediaPackager_MP4ToSmooth.xml, MediaPackager_SmoothToHLS.xml, and MediaEncryptor_PlayReadyProtection.xml files are located.</span></span> <span data-ttu-id="85a0f-187">中定義 MediaPackager_MP4ToSmooth.xml 和 MediaPackager_SmoothToHLS.xml[工作預設的 Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx)而 MediaEncryptor_PlayReadyProtection.xml 定義在 hello[工作預設 azureMedia Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="85a0f-187">MediaPackager_MP4ToSmooth.xml and MediaPackager_SmoothToHLS.xml are defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) and MediaEncryptor_PlayReadyProtection.xml is defined in hello [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Xml.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace MediaServicesContentProtection
    {
        class Program
        {
            // Paths toosupport files (within hello above base path). You can use 
            // hello provided sample media files from hello "SupportFiles" folder, or 
            // provide paths tooyour own media files below toorun these samples.

            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
                Path.Combine(_mediaFiles, @"SingleMP4\BigBuckBunny.mp4");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations\";


            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServiceAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServiceAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Used hello chached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Load an MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file tooa set of multibitrate MP4s.
                // Then, package a set of MP4s tooclear Smooth Streaming.
                IAsset clearSmoothStreamAsset = ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create a common encryption content key that is used 
                // a) tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
                //    that is used for encryption.
                // b) tooconfigure hello license delivery service and 
                //
                Guid keyId;
                byte[] contentKey;

                IContentKey key = CreateCommonEncryptionKey(out keyId, out contentKey);

                // hello content key authorization policy must be configured by you 
                // and met by hello client in order for hello PlayReady license
                // toobe delivered toohello client. 
                // In this example hello Media Services PlayReady license delivery service is used.
                ConfigureLicenseDeliveryService(key);

                // Get hello Media Services PlayReady license delivery URL.
                // This URL will be assigned toohello licenseAcquisitionUrl property 
                // of hello MediaEncryptor_PlayReadyProtection.xml file.
                Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

                // Update hello MediaEncryptor_PlayReadyProtection.xml file with hello key and URL info.
                UpdatePlayReadyConfigurationXMLFile(keyId, contentKey, acquisitionUrl);

                // Create HLS encrypted with PlayReady.
                IAsset playReadyHLSAsset = CreateHLSEncryptedWithPlayReady(clearSmoothStreamAsset);
                //
                string hlsWithPlayReadyURL = playReadyHLSAsset.GetHlsUri().ToString();
                Console.WriteLine("HLS with PlayReady URL:");
                Console.WriteLine(hlsWithPlayReadyURL);
            }

            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 toomultibitrate MP4s,
            /// 2 task - packages MP4s tooSmooth Streaming.
            /// </summary>
            /// <returns>hello output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 tooSmooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeSingleMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set tooClear Smooth Streaming.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get hello output asset that contains Smooth Streaming.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Create a common encryption content key that is used 
            /// tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
            /// that is used for encryption.
            /// </summary>
            /// <param name="keyId"></param>
            /// <param name="contentKey"></param>
            /// <returns></returns>
            public static IContentKey CreateCommonEncryptionKey(out Guid keyId, out byte[] contentKey)
            {
                keyId = Guid.NewGuid();
                contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            /// <summary>
            /// Update your configuration .xml file dynamically.
            /// </summary>
            public static void UpdatePlayReadyConfigurationXMLFile(Guid keyId, byte[] keyValue, Uri licenseAcquisitionUrl)
            {
                string xmlFileName = Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml");

                XNamespace xmlns = "http://schemas.microsoft.com/iis/media/v4/TM/TaskDefinition#";

                // Prepare hello encryption task template
                XDocument doc = XDocument.Load(xmlFileName);

                var licenseAcquisitionUrlEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "licenseAcquisitionUrl")
                        .FirstOrDefault();
                var contentKeyEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "contentKey")
                        .FirstOrDefault();
                var keyIdEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "keyId")
                        .FirstOrDefault();

                // Update hello "value" property.
                if (licenseAcquisitionUrlEl != null)
                    licenseAcquisitionUrlEl.Attribute("value").SetValue(licenseAcquisitionUrl.ToString());

                if (contentKeyEl != null)
                    contentKeyEl.Attribute("value").SetValue(Convert.ToBase64String(keyValue));

                if (keyIdEl != null)
                    keyIdEl.Attribute("value").SetValue(keyId);

                doc.Save(xmlFileName);
            }

            /// <summary>
            // Encrypts clear Smooth Streaming tooSmooth Streaming with PlayReady.
            // Then, packages hello PlayReady Smooth Streaming tooHLS with PlayReady.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>hello output asset.</returns>
            public static IAsset CreateHLSEncryptedWithPlayReady(IAsset clearSmoothStreamAsset)
            {
                IJob job = _context.Jobs.Create("Encrypt tooHLS with PlayReady.");

                // Add task 1 - Encrypt Smooth Streaming with PlayReady 
                IAsset encryptedSmoothAsset =
                    EncryptSmoothStreamWithPlayReadyTask(job, clearSmoothStreamAsset);

                // Add task 2 - Package tooHLS with PlayReady.
                PackageSmoothStreamToHLS(job, encryptedSmoothAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Since we had two tasks, hello OutputMediaAssets[1]
                // contains hello desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[1],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Uploads a single file.
            /// </summary>
            /// <param name="fileDir">hello location of hello files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify hello following encryption options for hello AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded tooAzure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: hello files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use hello SDK extension method toocreate a new asset by 
                // uploading a mezzanine file from a local path.
                IAsset asset = _context.Assets.CreateFromFile(
                    fileDir,
                    assetCreationOptions,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });


                return asset;

            }
            /// <summary>
            /// Creates a task tooencode tooAdaptive Bitrate. 
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncodeSingleMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 tooAdaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify hello input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s",
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task tooconvert hello MP4 file(s) tooa Smooth Streaming asset.
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles,
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task tooconvert adaptive bitrate tooSmooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 tooSmooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify hello input Asset, which is hello output Asset from hello first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset smoothOutputAsset =
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Streaming",
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }


            /// <summary>
            /// Converts Smooth Stream tooHLS.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello Smooth Stream asset.</param>
            /// <returns>hello asset that was packaged tooHLS.</returns>
            private static IAsset PackageSmoothStreamToHLS(IJob job, IAsset smoothStreamAsset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Read hello configuration data into a string. 
                //
                string configuration = File.ReadAllText(
                            Path.Combine(_configurationXMLFiles,
                                        @"MediaPackager_SmoothToHLS.xml"));

                // Create a task with hello encoding details, using a configuration file.
                ITask task = job.Tasks.AddNew("My Smooth tooHLS Task",
                   processor,
                   configuration,
                   TaskOptions.ProtectedConfiguration);

                // Specify hello input asset toobe encoded.
                task.InputAssets.Add(smoothStreamAsset);

                // Add an output asset toocontain hello results of hello job. 
                IAsset outputAsset =
                    task.OutputAssets.AddNew("HLS asset", AssetCreationOptions.None);


                return outputAsset;
            }

            /// <summary>
            /// Creates a task tooencrypt Smooth Streaming with PlayReady.
            /// Note: Do deliver DASH, make sure tooset hello useSencBox and adjustSubSamples 
            /// configuration properties tootrue.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncryptSmoothStreamWithPlayReadyTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Encryptor.
                IMediaProcessor playreadyProcessor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaEncryptor);

                // Read hello configuration XML.
                //
                // Note that hello configuration defined in MediaEncryptor_PlayReadyProtection.xml
                // is using keySeedValue. It is recommended that you do this only for testing 
                // and not in production. For more information, see 
                // http://msdn.microsoft.com/library/windowsazure/dn189154.aspx.
                //
                string configPlayReady = File.ReadAllText(Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml"));

                ITask playreadyTask = job.Tasks.AddNew("My PlayReady Task",
                   playreadyProcessor,
                   configPlayReady,
                   TaskOptions.ProtectedConfiguration);

                playreadyTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.CommonEncryptionProtected.
                IAsset playreadyAsset = playreadyTask.OutputAssets.AddNew(
                                                "PlayReady Smooth Streaming",
                                                AssetCreationOptions.CommonEncryptionProtected);


                return playreadyAsset;
            }


            /// <summary>
            /// Configures authorization policy for hello content key. 
            /// </summary>
            /// <param name="contentKey">hello content key.</param>
            static public void ConfigureLicenseDeliveryService(IContentKey contentKey)
            {
                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                    new ContentKeyAuthorizationPolicyRestriction 
                    { 
                        Name = "Open", 
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                        Requirements = null
                    }
                };

                // Configure PlayReady license template.
                string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                IContentKeyAuthorizationPolicyOption policyOption =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, newLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(policyOption);

                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            static private string ConfigurePlayReadyLicenseTemplate()
            {
                // hello following code configures PlayReady License Template using .NET classes
                // and returns hello XML string.

                PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }
            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }

        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="85a0f-188">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="85a0f-188">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="85a0f-189">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="85a0f-189">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


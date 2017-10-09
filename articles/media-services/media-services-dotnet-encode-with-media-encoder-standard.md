---
title: "媒體編碼器標準使用.NET 資產 aaaEncode |Microsoft 文件"
description: "本主題說明如何 toouse.NET tooencode 使用媒體編碼器 Strandard 資產。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="274c4-103">使用 .NET 透過 Media Encoder Standard 為資產編碼</span><span class="sxs-lookup"><span data-stu-id="274c4-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="274c4-104">編碼工作是在 Media Services hello 大多數處理作業。</span><span class="sxs-lookup"><span data-stu-id="274c4-104">Encoding jobs are one of hello most common processing operations in Media Services.</span></span> <span data-ttu-id="274c4-105">您從一個編碼 tooanother 建立編碼工作 tooconvert 媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="274c4-105">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="274c4-106">當編碼時，您可以使用 hello Media Services 內建 Media Encoder。</span><span class="sxs-lookup"><span data-stu-id="274c4-106">When you encode, you can use hello Media Services built-in Media Encoder.</span></span> <span data-ttu-id="274c4-107">您也可以使用 Media Services 合作夥伴; 提供的編碼器第三方編碼器皆可透過 hello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="274c4-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through hello Azure Marketplace.</span></span> 

<span data-ttu-id="274c4-108">本主題說明如何 toouse.NET tooencode 您資產的媒體編碼器標準 (MES)。</span><span class="sxs-lookup"><span data-stu-id="274c4-108">This topic shows how toouse .NET tooencode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="274c4-109">媒體編碼器標準設定時，使用其中一個所述的 hello 編碼器預設[這裡](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="274c4-109">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="274c4-110">建議 tooalways 原始程式檔編碼成彈性位元速率 MP4 集，然後將轉換 hello 組 toohello 所要的格式使用 hello[動態封裝](media-services-dynamic-packaging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="274c4-110">It is recommended tooalways encode your source files into an adaptive bitrate MP4 set and then convert hello set toohello desired format using hello [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="274c4-111">如果您的輸出資產是儲存體加密，必須設定資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="274c4-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="274c4-112">如需詳細資訊，請參閱 [設定資產傳遞原則](media-services-dotnet-configure-asset-delivery-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="274c4-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="274c4-113">輸出檔的名稱，其中包含與 hello 前 32 個字元的 MES 產生 hello 輸入的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="274c4-113">MES produces an output file with a name that contains hello first 32 characters of hello input file name.</span></span> <span data-ttu-id="274c4-114">hello 名稱根據 hello 預設檔案中指定的內容。</span><span class="sxs-lookup"><span data-stu-id="274c4-114">hello name is based on what is specified in hello preset file.</span></span> <span data-ttu-id="274c4-115">例如，"FileName": "{Basename}_{Index}{Extension}"。</span><span class="sxs-lookup"><span data-stu-id="274c4-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="274c4-116">{Basename} 取代為 hello hello 輸入的檔案名稱的前 32 個字元。</span><span class="sxs-lookup"><span data-stu-id="274c4-116">{Basename} is replaced by hello first 32 characters of hello input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="274c4-117">MES 格式</span><span class="sxs-lookup"><span data-stu-id="274c4-117">MES Formats</span></span>
[<span data-ttu-id="274c4-118">格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="274c4-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="274c4-119">MES 預設值</span><span class="sxs-lookup"><span data-stu-id="274c4-119">MES Presets</span></span>
<span data-ttu-id="274c4-120">媒體編碼器標準設定時，使用其中一個所述的 hello 編碼器預設[這裡](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="274c4-120">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="274c4-121">輸入和輸出中繼資料</span><span class="sxs-lookup"><span data-stu-id="274c4-121">Input and output metadata</span></span>
<span data-ttu-id="274c4-122">當您編碼的輸入的資產或多個使用 EMS 時，您會取得輸出資產在 hello，成功完成編碼工作。</span><span class="sxs-lookup"><span data-stu-id="274c4-122">When you encode an input asset (or assets) using MES, you get an output asset at hello successful completion of that encode task.</span></span> <span data-ttu-id="274c4-123">hello 輸出資產包含視訊、 音訊、 縮圖、 資訊清單等根據您使用的 hello 編碼預設。</span><span class="sxs-lookup"><span data-stu-id="274c4-123">hello output asset contains video, audio, thumbnails, manifest, etc. based on hello encoding preset you use.</span></span>

<span data-ttu-id="274c4-124">hello 輸出資產也包含 hello 輸入資產的相關中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="274c4-124">hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="274c4-125">hello hello 中繼資料 XML 檔案名稱具有下列格式的 hello: < a > _metadata.xml (例如，41114ad3-eb5e-4 c 57-8 d 92-5354e2b7d4a4_metadata.xml)，其中 < a > 是 hello 的 hello 輸入資產的 AssetId 值。</span><span class="sxs-lookup"><span data-stu-id="274c4-125">hello name of hello metadata XML file has hello following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is hello AssetId value of hello input asset.</span></span> <span data-ttu-id="274c4-126">hello 這個輸入的中繼資料 XML 結構描述會描述[這裡](media-services-input-metadata-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="274c4-126">hello schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="274c4-127">hello 輸出資產也包含 hello 輸出資產的相關中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="274c4-127">hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="274c4-128">hello hello 中繼資料 XML 檔案名稱具有下列格式的 hello: < s > l (例如，BigBuckBunny_manifest.xml)。</span><span class="sxs-lookup"><span data-stu-id="274c4-128">hello name of hello metadata XML file has hello following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="274c4-129">hello 這個輸出中繼資料架構的 XML 會說明[這裡](media-services-output-metadata-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="274c4-129">hello schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="274c4-130">如果您想要 tooexamine 任一 hello 兩個中繼資料檔案，您可以建立 SAS 定位器和下載 hello 檔案 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="274c4-130">If you want tooexamine either of hello two metadata files, you can create a SAS locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="274c4-131">您可以找到範例上如何 toocreate SAS 定位器和下載檔案使用 hello 媒體服務.NET SDK 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="274c4-131">You can find an example on how toocreate a SAS locator and download a file Using hello Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="274c4-132">下載範例</span><span class="sxs-lookup"><span data-stu-id="274c4-132">Download sample</span></span>
<span data-ttu-id="274c4-133">您可以取得及執行範例，示範如何與從 MES tooencode[這裡](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/)。</span><span class="sxs-lookup"><span data-stu-id="274c4-133">You can get and run a sample that shows how tooencode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="274c4-134">.NET 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="274c4-134">.NET sample code</span></span>

<span data-ttu-id="274c4-135">hello，下列程式碼範例會使用 Media Services.NET SDK tooperform hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="274c4-135">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="274c4-136">建立編碼工作。</span><span class="sxs-lookup"><span data-stu-id="274c4-136">Create an encoding job.</span></span>
* <span data-ttu-id="274c4-137">取得參考 toohello 媒體編碼器標準編碼器。</span><span class="sxs-lookup"><span data-stu-id="274c4-137">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="274c4-138">指定 toouse hello[彈性資料流](media-services-autogen-bitrate-ladder-with-mes.md)預設。</span><span class="sxs-lookup"><span data-stu-id="274c4-138">Specify toouse hello [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="274c4-139">加入單一編碼工作 toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="274c4-139">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="274c4-140">指定 hello 輸入資產 toobe 編碼。</span><span class="sxs-lookup"><span data-stu-id="274c4-140">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="274c4-141">建立會包含 hello 編碼資產的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="274c4-141">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="274c4-142">加入事件處理常式 toocheck hello 工作進度。</span><span class="sxs-lookup"><span data-stu-id="274c4-142">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="274c4-143">送出 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="274c4-143">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="274c4-144">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="274c4-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="274c4-145">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="274c4-145">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="274c4-146">範例</span><span class="sxs-lookup"><span data-stu-id="274c4-146">Example</span></span> 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    // Get an uploaded asset.
                    var asset = _context.Assets.FirstOrDefault();

                    // Encode and generate hello output using hello "Adaptive Streaming" preset.
                    EncodeToAdaptiveBitrateMP4Set(asset);

                    Console.ReadLine();
                }

                static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Media Encoder Standard Job");
                    // Get a media processor reference, and pass tooit hello name of hello 
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
                        processor,
                        "Adaptive Streaming",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(asset);
                    // Add an output asset toocontain hello results of hello job. 
                    // This output is specified as AssetCreationOptions.None, which 
                    // means hello output asset is not encrypted. 
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
                    job.Submit();
                    job.GetExecutionProgressTask(CancellationToken.None).Wait();

                    return job.OutputMediaAssets[0];
                }

                private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
                {
                    Console.WriteLine("Job state changed event:");
                    Console.WriteLine("  Previous state: " + e.PreviousState);
                    Console.WriteLine("  Current state: " + e.CurrentState);
                    switch (e.CurrentState)
                    {
                        case JobState.Finished:
                            Console.WriteLine();
                            Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
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
                            break;
                        default:
                            break;
                    }
                }

                private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
                {
                    var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                    ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

                    if (processor == null)
                        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

                    return processor;
                }
            }
        }

## <a name="media-services-learning-paths"></a><span data-ttu-id="274c4-147">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="274c4-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="274c4-148">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="274c4-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="274c4-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="274c4-149">Next steps</span></span>
<span data-ttu-id="274c4-150">[如何搭配.NET 使用媒體編碼器標準 toogenerate 縮圖](media-services-dotnet-generate-thumbnail-with-mes.md)
[媒體服務編碼方式的概觀](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="274c4-150">[How toogenerate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>


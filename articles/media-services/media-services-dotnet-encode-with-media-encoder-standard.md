---
title: "使用 .NET 透過媒體編碼器標準為資產編碼 | Microsoft Docs"
description: "本主題說明如何使用 .NET 來使用 Media Encoder Standard 為資產編碼。"
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
ms.openlocfilehash: 929592368501c54277748bf46b2160c9058db3fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="07c97-103">使用 .NET 透過 Media Encoder Standard 為資產編碼</span><span class="sxs-lookup"><span data-stu-id="07c97-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="07c97-104">編碼工作是媒體服務中最常見的處理作業。</span><span class="sxs-lookup"><span data-stu-id="07c97-104">Encoding jobs are one of the most common processing operations in Media Services.</span></span> <span data-ttu-id="07c97-105">您建立編碼工作以將媒體檔案從一種編碼轉換成另一種編碼。</span><span class="sxs-lookup"><span data-stu-id="07c97-105">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="07c97-106">編碼時，您可以使用媒體服務內建的 Media Encoder。</span><span class="sxs-lookup"><span data-stu-id="07c97-106">When you encode, you can use the Media Services built-in Media Encoder.</span></span> <span data-ttu-id="07c97-107">您也可以使用媒體服務合作夥伴提供的編碼器；第三方編碼器可透過 Azure Marketplace 取得。</span><span class="sxs-lookup"><span data-stu-id="07c97-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through the Azure Marketplace.</span></span> 

<span data-ttu-id="07c97-108">本主題說明如何使用 .NET 透過 Media Encoder Standard (MES) 將您的資產編碼。</span><span class="sxs-lookup"><span data-stu-id="07c97-108">This topic shows how to use .NET to encode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="07c97-109">Media Encoder Standard 使用 [這裡](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)描述的其中一個編碼器預設值進行設定。</span><span class="sxs-lookup"><span data-stu-id="07c97-109">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="07c97-110">建議一律將來源檔編碼為調適性位元速率 MP4 集，然後使用[動態封裝](media-services-dynamic-packaging-overview.md)將該集合轉換為所要的格式。</span><span class="sxs-lookup"><span data-stu-id="07c97-110">It is recommended to always encode your source files into an adaptive bitrate MP4 set and then convert the set to the desired format using the [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="07c97-111">如果您的輸出資產是儲存體加密，必須設定資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="07c97-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="07c97-112">如需詳細資訊，請參閱 [設定資產傳遞原則](media-services-dotnet-configure-asset-delivery-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="07c97-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="07c97-113">MES 會產生一個輸出檔案，其名稱包含輸入檔案名稱的前 32 個字元。</span><span class="sxs-lookup"><span data-stu-id="07c97-113">MES produces an output file with a name that contains the first 32 characters of the input file name.</span></span> <span data-ttu-id="07c97-114">名稱是以預設檔案中指定的名稱為基礎。</span><span class="sxs-lookup"><span data-stu-id="07c97-114">The name is based on what is specified in the preset file.</span></span> <span data-ttu-id="07c97-115">例如，"FileName": "{Basename}_{Index}{Extension}"。</span><span class="sxs-lookup"><span data-stu-id="07c97-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="07c97-116">{Basename} 會由輸入檔案名稱的前 32 個字元取代。</span><span class="sxs-lookup"><span data-stu-id="07c97-116">{Basename} is replaced by the first 32 characters of the input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="07c97-117">MES 格式</span><span class="sxs-lookup"><span data-stu-id="07c97-117">MES Formats</span></span>
[<span data-ttu-id="07c97-118">格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="07c97-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="07c97-119">MES 預設值</span><span class="sxs-lookup"><span data-stu-id="07c97-119">MES Presets</span></span>
<span data-ttu-id="07c97-120">Media Encoder Standard 使用 [這裡](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)描述的其中一個編碼器預設值進行設定。</span><span class="sxs-lookup"><span data-stu-id="07c97-120">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="07c97-121">輸入和輸出中繼資料</span><span class="sxs-lookup"><span data-stu-id="07c97-121">Input and output metadata</span></span>
<span data-ttu-id="07c97-122">如果您使用 MES 為輸入資產 (或資產) 編碼，在該編碼工作完成時，您便能取得輸出資產。</span><span class="sxs-lookup"><span data-stu-id="07c97-122">When you encode an input asset (or assets) using MES, you get an output asset at the successful completion of that encode task.</span></span> <span data-ttu-id="07c97-123">輸出資產包含視訊、音訊、縮圖、資訊清單等等，依據您所使用的編碼預設格式而定。</span><span class="sxs-lookup"><span data-stu-id="07c97-123">The output asset contains video, audio, thumbnails, manifest, etc. based on the encoding preset you use.</span></span>

<span data-ttu-id="07c97-124">輸出資產也包含隨附關於輸入資產中繼資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="07c97-124">The output asset also contains a file with metadata about the input asset.</span></span> <span data-ttu-id="07c97-125">中繼資料 XML 檔案的名稱具備下列格式︰<asset_id>_metadata.xml (例如：41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml)，其中的 <asset_id> 是輸入資產的 AssetId 值。</span><span class="sxs-lookup"><span data-stu-id="07c97-125">The name of the metadata XML file has the following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is the AssetId value of the input asset.</span></span> <span data-ttu-id="07c97-126">[這裡](media-services-input-metadata-schema.md)說明了此輸入中繼資料 XML 的結構描述。</span><span class="sxs-lookup"><span data-stu-id="07c97-126">The schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="07c97-127">輸出資產也包含隨附關於輸出資產中繼資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="07c97-127">The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="07c97-128">中繼資料 XML 檔案的名稱具備下列格式︰<source_file_name>_manifest.xml (例如：BigBuckBunny_manifest.xml)。</span><span class="sxs-lookup"><span data-stu-id="07c97-128">The name of the metadata XML file has the following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="07c97-129">[這裡](media-services-output-metadata-schema.md)說明了此輸出中繼資料 XML 的結構描述。</span><span class="sxs-lookup"><span data-stu-id="07c97-129">The schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="07c97-130">如果您想要檢查這兩個中繼資料檔案的任一個，可以建立 SAS 定位器並將檔案下載到您的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="07c97-130">If you want to examine either of the two metadata files, you can create a SAS locator and download the file to your local computer.</span></span> <span data-ttu-id="07c97-131">您可以找到關於如何建立 SAS 定位器的範例，並且下載使用媒體服務 .NET SDK 擴充功能的檔案。</span><span class="sxs-lookup"><span data-stu-id="07c97-131">You can find an example on how to create a SAS locator and download a file Using the Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="07c97-132">下載範例</span><span class="sxs-lookup"><span data-stu-id="07c97-132">Download sample</span></span>
<span data-ttu-id="07c97-133">您可以從[這裡 (英文)](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/) 取得並執行示範如何使用 MES 進行編碼的範例。</span><span class="sxs-lookup"><span data-stu-id="07c97-133">You can get and run a sample that shows how to encode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="07c97-134">.NET 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="07c97-134">.NET sample code</span></span>

<span data-ttu-id="07c97-135">下列程式碼範例使用媒體服務 .NET SDK 執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="07c97-135">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="07c97-136">建立編碼工作。</span><span class="sxs-lookup"><span data-stu-id="07c97-136">Create an encoding job.</span></span>
* <span data-ttu-id="07c97-137">取得對 Media Encoder Standard 編碼器的參考</span><span class="sxs-lookup"><span data-stu-id="07c97-137">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="07c97-138">指定要使用[彈性資料流](media-services-autogen-bitrate-ladder-with-mes.md)預設值。</span><span class="sxs-lookup"><span data-stu-id="07c97-138">Specify to use the [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="07c97-139">將單一編碼工作加入工作。</span><span class="sxs-lookup"><span data-stu-id="07c97-139">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="07c97-140">指定要編碼的輸入資產。</span><span class="sxs-lookup"><span data-stu-id="07c97-140">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="07c97-141">建立將包含已編碼資產的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="07c97-141">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="07c97-142">加入事件處理常式來檢查工作進度。</span><span class="sxs-lookup"><span data-stu-id="07c97-142">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="07c97-143">提交作業。</span><span class="sxs-lookup"><span data-stu-id="07c97-143">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="07c97-144">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="07c97-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="07c97-145">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="07c97-145">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="07c97-146">範例</span><span class="sxs-lookup"><span data-stu-id="07c97-146">Example</span></span> 

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

                    // Encode and generate the output using the "Adaptive Streaming" preset.
                    EncodeToAdaptiveBitrateMP4Set(asset);

                    Console.ReadLine();
                }

                static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Media Encoder Standard Job");
                    // Get a media processor reference, and pass to it the name of the 
                    // processor to use for the specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                    // Create a task with the encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
                        processor,
                        "Adaptive Streaming",
                        TaskOptions.None);

                    // Specify the input asset to be encoded.
                    task.InputAssets.Add(asset);
                    // Add an output asset to contain the results of the job. 
                    // This output is specified as AssetCreationOptions.None, which 
                    // means the output asset is not encrypted. 
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="07c97-147">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="07c97-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="07c97-148">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="07c97-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="07c97-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07c97-149">Next steps</span></span>
<span data-ttu-id="07c97-150">[如何使用媒體編碼器標準搭配 .NET 產生縮圖](media-services-dotnet-generate-thumbnail-with-mes.md)
[媒體服務編碼概觀](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="07c97-150">[How to generate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>


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
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a>使用 .NET 透過 Media Encoder Standard 為資產編碼
編碼工作是在 Media Services hello 大多數處理作業。 您從一個編碼 tooanother 建立編碼工作 tooconvert 媒體檔案。 當編碼時，您可以使用 hello Media Services 內建 Media Encoder。 您也可以使用 Media Services 合作夥伴; 提供的編碼器第三方編碼器皆可透過 hello Azure Marketplace。 

本主題說明如何 toouse.NET tooencode 您資產的媒體編碼器標準 (MES)。 媒體編碼器標準設定時，使用其中一個所述的 hello 編碼器預設[這裡](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)。

建議 tooalways 原始程式檔編碼成彈性位元速率 MP4 集，然後將轉換 hello 組 toohello 所要的格式使用 hello[動態封裝](media-services-dynamic-packaging-overview.md)。 

如果您的輸出資產是儲存體加密，必須設定資產傳遞原則。 如需詳細資訊，請參閱 [設定資產傳遞原則](media-services-dotnet-configure-asset-delivery-policy.md)。

> [!NOTE]
> 輸出檔的名稱，其中包含與 hello 前 32 個字元的 MES 產生 hello 輸入的檔案名稱。 hello 名稱根據 hello 預設檔案中指定的內容。 例如，"FileName": "{Basename}_{Index}{Extension}"。 {Basename} 取代為 hello hello 輸入的檔案名稱的前 32 個字元。
> 
> 

### <a name="mes-formats"></a>MES 格式
[格式和轉碼器](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a>MES 預設值
媒體編碼器標準設定時，使用其中一個所述的 hello 編碼器預設[這裡](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)。

### <a name="input-and-output-metadata"></a>輸入和輸出中繼資料
當您編碼的輸入的資產或多個使用 EMS 時，您會取得輸出資產在 hello，成功完成編碼工作。 hello 輸出資產包含視訊、 音訊、 縮圖、 資訊清單等根據您使用的 hello 編碼預設。

hello 輸出資產也包含 hello 輸入資產的相關中繼資料檔案。 hello hello 中繼資料 XML 檔案名稱具有下列格式的 hello: < a > _metadata.xml (例如，41114ad3-eb5e-4 c 57-8 d 92-5354e2b7d4a4_metadata.xml)，其中 < a > 是 hello 的 hello 輸入資產的 AssetId 值。 hello 這個輸入的中繼資料 XML 結構描述會描述[這裡](media-services-input-metadata-schema.md)。

hello 輸出資產也包含 hello 輸出資產的相關中繼資料檔案。 hello hello 中繼資料 XML 檔案名稱具有下列格式的 hello: < s > l (例如，BigBuckBunny_manifest.xml)。 hello 這個輸出中繼資料架構的 XML 會說明[這裡](media-services-output-metadata-schema.md)。

如果您想要 tooexamine 任一 hello 兩個中繼資料檔案，您可以建立 SAS 定位器和下載 hello 檔案 tooyour 本機電腦。 您可以找到範例上如何 toocreate SAS 定位器和下載檔案使用 hello 媒體服務.NET SDK 延伸模組。

## <a name="download-sample"></a>下載範例
您可以取得及執行範例，示範如何與從 MES tooencode[這裡](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/)。

## <a name="net-sample-code"></a>.NET 範例程式碼

hello，下列程式碼範例會使用 Media Services.NET SDK tooperform hello 下列工作：

* 建立編碼工作。
* 取得參考 toohello 媒體編碼器標準編碼器。
* 指定 toouse hello[彈性資料流](media-services-autogen-bitrate-ladder-with-mes.md)預設。 
* 加入單一編碼工作 toohello 作業。 
* 指定 hello 輸入資產 toobe 編碼。
* 建立會包含 hello 編碼資產的輸出資產。
* 加入事件處理常式 toocheck hello 工作進度。
* 送出 hello 作業。

#### <a name="create-and-configure-a-visual-studio-project"></a>建立和設定 Visual Studio 專案

設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。 

#### <a name="example"></a>範例 

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

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>後續步驟
[如何搭配.NET 使用媒體編碼器標準 toogenerate 縮圖](media-services-dotnet-generate-thumbnail-with-mes.md)
[媒體服務編碼方式的概觀](media-services-encode-asset.md)


---
title: "媒體編碼器高階工作流程的編碼 aaaAdvanced |Microsoft 文件"
description: "深入了解如何 tooencode 與媒體編碼器高階工作流程。 程式碼範例會以 C# 所撰寫，並使用 hello Media Services SDK for.NET。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a>使用 Media Encoder Premium Workflow 進行進階編碼
> [!NOTE]
> 本主題中討論的媒體編碼器高階工作流程媒體處理器無法在中國使用。
>
>

如有進階編碼器的問題，請傳送電子郵件到 mepd@Microsoft.com。

## <a name="overview"></a>概觀
Microsoft Azure Media Services 推出 hello**媒體編碼器高階工作流程**媒體處理器。 此處理器為高階隨選工作流程提供先進的編碼功能。

hello 下列主題簡述太相關詳細資料，**媒體編碼器高階工作流程**:

* [Hello 媒體編碼器高階工作流程來格式化支援](media-services-premium-workflow-encoder-formats.md)– 討論 hello 檔案格式和轉碼器支援**媒體編碼器高階工作流程**。
* [概觀與比較 Azure 上要求的媒體編碼器](media-services-encode-asset.md)比較 hello 的編碼能力**媒體編碼器高階工作流程**和**媒體編碼器標準**。

本主題示範如何使用 tooencode**媒體編碼器高階工作流程**使用.NET。

編碼工作的 hello**媒體編碼器高階工作流程**需要不同的組態檔，稱為工作流程檔案。 這些檔案具有.workflow 副檔名，而且會建立使用 hello[工作流程設計工具](media-services-workflow-designer.md)工具。

您也可以取得 hello 預設工作流程檔案[這裡](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)。 hello 資料夾也包含 hello 描述這些檔案。

hello 工作流程檔案需要上傳 toobe tooyour 媒體服務帳戶為資產，，這項資產應該 toohello 編碼工作中進行傳遞。

## <a name="create-and-configure-a-visual-studio-project"></a>建立和設定 Visual Studio 專案

設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。 

## <a name="encoding-example"></a>編碼範例

hello 下列範例會示範如何使用 tooencode**媒體編碼器高階工作流程**。

會執行下列步驟的 hello:

1. 建立資產並上傳工作流程檔案。
2. 建立資產並上傳來源媒體檔案。
3. 收到 hello"媒體編碼器高階工作流程"媒體處理器。
4. 建立工作 (Job) 和工作 (Task)。

    在大部分情況下，hello hello 工作的組態字串是空的 （如下列範例中的 hello 中）。 有一些進階的案例 （需要的 tootooset 執行階段屬性動態地） 在此情況下，您會提供 XML 字串 toohello 編碼工作。 這類案例的範例包括：建立疊加、平行或循序的媒體編結、顯示字幕。
5. 加入兩個輸入的資產 toohello 工作。

    1. 第 1 – hello 工作流程的資產。
    2. 第 2 – hello 視訊資產。

    >[!NOTE]
    >hello 工作流程資產必須加入 toohello 工作之前 hello 媒體資產。
   這項工作中的 hello 組態字串應為空白。
   
6. 送出 hello 編碼工作。

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
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

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
                    }

                    return job.OutputMediaAssets[0];
                }

                static private void StateChanged(object sender, JobStateChangedEventArgs e)
                {
                    Console.WriteLine("Job state changed event:");
                    Console.WriteLine("  Previous state: " + e.PreviousState);
                    Console.WriteLine("  Current state: " + e.CurrentState);

                    switch (e.CurrentState)
                    {
                        case JobState.Finished:
                            Console.WriteLine();
                            Console.WriteLine("Job is finished.");
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
                            // LogJobStop(job.Id);
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

如有進階編碼器的問題，請傳送電子郵件到 mepd@Microsoft.com。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

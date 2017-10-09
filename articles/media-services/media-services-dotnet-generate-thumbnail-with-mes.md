---
title: "搭配.NET 使用媒體編碼器標準 aaaHow toogenerate 縮圖"
description: "本主題說明如何 toouse.NET tooencode 資產，並產生縮圖在 hello 同時使用媒體編碼程式標準。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: juliako
ms.openlocfilehash: 23d3e4d9bf64a688d45499c045f19d2792167990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a>如何搭配.NET 使用媒體編碼器標準 toogenerate 縮圖

您可以使用標準的媒體編碼器 toogenerate 一或多個縮圖從視訊在您輸入[JPEG](https://en.wikipedia.org/wiki/JPEG)， [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics)，或[BMP](https://en.wikipedia.org/wiki/BMP_file_format)影像檔案格式。 您可以送出只產生影像的工作，或是結合縮圖產生與編碼。 本主題會提供幾個對於這類情況的範例 XML 和 JSON 縮圖預設。 在 hello hello 主題結尾，沒有[範例程式碼](#code_sample)toouse hello Media Services.NET SDK tooaccomplish hello 編碼工作的方式，它會顯示。

如需有關範例的預設設定中所使用的 hello 元素的詳細資訊，您應該檢閱[媒體編碼器標準結構描述](media-services-mes-schema.md)。

請確定 tooreview hello[考量](media-services-dotnet-generate-thumbnail-with-mes.md#considerations)> 一節。

## <a name="example--single-png-file"></a>範例 – 單一 PNG 檔案

hello 下列 JSON 和 XML 預設可以是單一輸出 PNG 檔案超出 hello 前幾個使用的 tooproduce hello 輸入視訊，其中 hello 編碼器會進行全力嘗試在尋找 「 有趣 」 的框架秒數。 請注意 hello 輸出影像尺寸，已設定 too100%，表示這些設定將會符合 hello 輸入視訊的 hello 維度。 也請注意 「 輸出 」 中的 hello 「 格式 」 設定的必要方式 toomatch hello"PngLayers"hello"轉碼器 」 一節中使用。 

### <a name="json-preset"></a>JSON 預設值

    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a>XML 預設值

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--a-series-of-jpeg-images"></a>範例 – 一系列的 JPEG 影像

hello 下列 JSON 和 XML 預設可以使用的 tooproduce 一組在 5%的時間戳記的 10 個映像的 15%，95%的 hello 輸入時間軸，其中 hello 映像大小會是指定的 toobe 輸入視訊的 hello 一季。

### <a name="json-preset"></a>JSON 預設值

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }

### <a name="xml-preset"></a>XML 預設值
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--one-image-at-a-specific-timestamp"></a>範例 – 在特定時間戳記的一個影像

hello 下列 JSON 和 XML 預設可以使用的 tooproduce hello 輸入視訊的標記的單一 JPEG 影像 hello 在 30 秒。 此預設預期 hello 輸入的 toobe 的持續時間超過 30 秒 （其他 hello 作業將會失敗）。

### <a name="json-preset"></a>JSON 預設值

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a>XML 預設值
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:02" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a id="code_sample"></a>範例 – 編碼視訊，並產生縮圖

hello，下列程式碼範例會使用 Media Services.NET SDK tooperform hello 下列工作：

* 建立編碼工作。
* 取得參考 toohello 媒體編碼器標準編碼器。
* 預設負載 hello [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml)或[JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json)包含 hello 編碼預設值，以及所需的資訊 toogenerate 縮圖。 您可以儲存此[XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml)或[JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json)檔，並使用 hello，下列程式碼 tooload hello 檔中。
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* 加入單一編碼工作 toohello 作業。 
* 指定 hello 輸入資產 toobe 編碼。
* 建立會包含 hello 編碼資產的輸出資產。
* 加入事件處理常式 toocheck hello 工作進度。
* 送出 hello 作業。

請參閱 hello[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)directions on 如何主題 tooset 開發環境。

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace EncodeAndGenerateThumbnails
        {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static CloudMediaContext _context = null;

            private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            static void Main(string[] args)
            {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello thumbnails.
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

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
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

## <a id="json"></a>縮圖 JSON 預設
如需結構描述的資訊，請參閱 [這個主題](https://msdn.microsoft.com/library/mt269962.aspx) 。

    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
    
            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="xml"></a>縮圖 XML 預設
如需結構描述的資訊，請參閱 [這個主題](https://msdn.microsoft.com/library/mt269962.aspx) 。
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="considerations"></a>考量
hello 下列考量適用於：

* hello 使用明確的時間戳記的開始/步驟/範圍假設該 hello 輸入的來源是在至少 1 分鐘長。
* 具有 Start、Step 和 Range 字串屬性的 Jpg/Png/BmpImage 項目 – 這些可以解譯為：
  
  * 畫面格數目 (如果是非負整數)，例如： "Start"："120"，
  * 如果以 %-後置字元，例如表示相對 toosource 持續時間。 "Start"："15%" 或
  * 時間戳記 (如果以 HH:MM:SS... format。 例如 "Start"："00:01:00"
    
    您可以隨意混合使用標記法。
    
    此外，開始也支援特殊的巨集: {最佳}，其中嘗試 toodetermine hello 第一個 「 有趣 」 畫面格的 hello 內容附註: (步驟和範圍時開始設定得忽略 {最佳})
  * 預設值：Start:{Best}
* 輸出格式需要明確地提供每個影像格式 toobe: Jpg/Png/BmpFormat。 如果有，MES 會比對 JpgVideo tooJpgFormat，依此類推。 OutputFormat 導入了新的影像轉碼器特定巨集: {}，而且需要 toobe 存在 （一次，一次） 用於索引的影像輸出格式。

## <a name="next-steps"></a>後續步驟

您可以檢查 hello[作業進度](media-services-check-job-progress.md)時 hello 編碼工作已暫止。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>另請參閱
[媒體服務編碼概觀](media-services-encode-asset.md)


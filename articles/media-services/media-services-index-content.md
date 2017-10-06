---
title: "aaaIndexing 透過 Azure Media Indexer 媒體檔案"
description: "Azure Media Indexer 可讓您的媒體檔案可搜尋的 toomake 內容和 toogenerate 全文檢索文字記錄的關閉字幕和關鍵字。 本主題說明如何 toouse Media Indexer。"
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.assetid: 827a56b2-58a5-4044-8d5c-3e5356488271
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: adsolank;juliako;johndeu
ms.openlocfilehash: c1bed774e302e61ca3510668645dc2015b434a0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer"></a>使用 Azure Media Indexer 編輯媒體檔案索引
Azure Media Indexer 可讓您的媒體檔案可搜尋的 toomake 內容和 toogenerate 全文檢索文字記錄的關閉字幕和關鍵字。 您可以處理一份媒體檔或是批次處理多個媒體檔案。  

> [!IMPORTANT]
> 建立索引時的內容，請確定 toouse （沒有背景音樂、 噪音、 效果或麥克風雜音） 語音非常清楚的媒體檔案。 適當內容的一些範例有：錄製的會議、演講或簡報。 hello 下列內容可能不適合編製索引： 電影、 電視節目，任何具有混音效果與音效，錄製不佳的內容有背景噪音 （雜音））。
> 
> 

索引作業可以產生下列輸出的 hello:

* 在下列格式的 hello 字幕檔案：**沙米文**， **TTML**，和**WebVTT**。
  
    隱藏式的字幕檔案包含稱為的 Recognizability，索引作業會根據 hello 來源視訊中的 hello 語音辨識程度的分數是標記。  您可以使用 hello 值 Recognizability tooscreen 輸出檔的可用性。 分數低表示由於 tooaudio 品質不良索引的結果。
* 關鍵字檔案 (XML)。
* 與 SQL Server 搭配使用的音訊編製索引 blob 檔案 (AIB)。
  
    如需詳細資訊，請參閱 [搭配 Azure Media Indexer 和 SQL Server 使用 AIB 檔案](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)。

本主題說明如何 toocreate 索引太作業**索引資產**和**多個檔案編製索引**。

如需最新 Azure Media Indexer 更新 hello，請參閱[媒體服務部落格](#preset)。

## <a name="using-configuration-and-manifest-files-for-indexing-tasks"></a>針對索引工作使用組態和資訊清單檔
您可以使用工作組態來為索引工作指定更多詳細資料。 例如，您可以指定哪些中繼資料 toouse 媒體檔案。 此中繼資料是由 hello 語言引擎 tooexpand 其詞彙，並可大幅提升 hello 語音辨識準確度。  您也會無法 toospecify 您想要的輸出檔案。

您也可以使用資訊清單檔，一次處理多個媒體檔案。

如需詳細資訊，請參閱 [Azure Media Indexer 的工作預設](https://msdn.microsoft.com/library/dn783454.aspx)。

## <a name="index-an-asset"></a>編製資產索引
hello 下列方法將上傳媒體檔案儲存為資產，並建立工作 tooindex hello 資產。

請注意，是否沒有組態檔指定，hello 媒體檔案會被編製索引使用所有預設設定。

    static bool RunIndexingJob(string inputMediaFilePath, string outputFolder, string configurationFile = "")
    {
        // Create an asset and upload hello input media file toostorage.
        IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Indexing Input Asset",
            AssetCreationOptions.None);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration from file if specified.
        string configuration = string.IsNullOrEmpty(configurationFile) ? "" : File.ReadAllText(configurationFile);

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }  
<!-- __ -->
### <a id="output_files"></a>輸出檔案
根據預設，索引作業會產生下列輸出檔案的 hello。 hello 檔案會儲存在 hello 第一個輸出資產。

多個輸入的媒體檔案時，索引子會產生名為 'JobResult.txt' 的 hello 工作輸出資訊清單檔案。 每個輸入的媒體檔案，hello AIB、 SAMI、 TTML、 WebVTT 和關鍵字檔案會循序編號，且使用 hello"Alias"命名。

| 檔案名稱 | 說明 |
| --- | --- |
| **InputFileName.aib** |音訊索引 blob 檔案。 <br/><br/> 音訊索引 Blob (AIB) 檔案是二進位檔案，可以使用全文檢索搜尋在 Microsoft SQL Server 中搜尋。  hello AIB 檔案是 hello 單純的字幕檔案，比功能更強大，因為它包含的每個單字，允許更豐富的搜尋經驗的替代項目。 <br/> <br/>它需要 hello hello Indexer SQL 附加元件的電腦執行 Microsoft SQL server 2008 或更新版本上安裝。 搜尋 hello AIB 使用 Microsoft SQL server 全文檢索搜尋會提供更精確的搜尋結果比搜尋 hello 關閉 WAMI 所產生的字幕檔案。 這是因為 hello AIB 包含發音類似而 hello 關閉字幕檔案則包含每個區段 hello 音訊 hello 最高信賴度文字的文字替代項目。 如果搜尋口語文字是您的重要性，它會建議 toouse hello Aib 與 Microsoft SQL Server 搭配。<br/><br/> toodownload hello 附加元件，請按一下<a href="http://aka.ms/indexersql">Azure Media Indexer SQL 附加元件</a>。 <br/><br/>它也可能 tooutilize 其他搜尋引擎例如 Apache Lucene/Solr toosimply 索引 hello 視訊依據 hello 關閉標題和關鍵字 XML 檔案，但這將導致較不精確的搜尋結果。 |
| **InputFileName.smi**<br/>**InputFileName.ttml**<br/>**InputFileName.vtt** |SAMI、TTML 和 WebVTT 格式的隱藏式輔助字幕 (CC) 檔案。<br/><br/>也可以使用的 toomake 音訊和視訊檔案存取 toopeople 聽覺時。<br/><br/>已關閉的標題檔案包含標記，稱為<b>Recognizability</b>評分索引作業根據 hello 來源視訊中的 hello 語音辨識程度是。  您可以使用 hello 值<b>Recognizability</b> tooscreen 輸出檔。 分數低表示由於 tooaudio 品質不良索引的結果。 |
| **InputFileName.kw.xml<br/>InputFileName.info** |關鍵字與資訊檔案。 <br/><br/>關鍵字檔案是 XML 檔案，其中包含從 hello 語音內容，擷取使用頻率與偏移的資訊的關鍵字。 <br/><br/>資訊檔案是純文字檔案，包含每個已辨識字詞的細微資訊。 hello 第一行是特殊的並包含 hello Recognizability 分數。 每個後續的行是 hello 下列資料的索引標籤分隔清單： 開始時間、 結束時間、 word/片語、 信心。 以秒為單位指定 hello 時間和 hello 信心根據 0-1 指定的數字。 <br/><br/>範例行："1.20    1.45    word    0.67" <br/><br/>這些檔案可以用於許多用途，例如 tooperform 語音分析，或公開的 toosearch 引擎例如 Bing、 Google 或 Microsoft SharePoint toomake hello 媒體檔案更容易找到或甚至使用的 toodeliver 更有相關性的廣告。 |
| **JobResult.txt** |輸出資訊清單中，多個檔案，其中包含下列資訊的 hello 編製索引時，才存在：<br/><br/><table border="1"><tr><th>InputFile</th><th>Alias</th><th>MediaLength</th><th>錯誤</th></tr><tr><td>a.mp4</td><td>Media_1</td><td>300</td><td>0</td></tr><tr><td>b.mp4</td><td>Media_2</td><td>0</td><td>3000</td></tr><tr><td>c.mp4</td><td>Media_3</td><td>600</td><td>0</td></tr></table><br/> |

如果不是所有的輸入的媒體檔案在成功編製索引，hello 索引工作將會失敗，錯誤碼為 4000。 如需詳細資訊，請參閱 [錯誤碼](#error_codes)。

## <a name="index-multiple-files"></a>編製多個檔案的索引
hello 下列方法將多個媒體檔案上傳為資產，並建立工作 tooindex 批次中的所有這些檔案。

Hello.lst 副檔名的資訊清單檔案是建立和上傳到 hello 資產。 hello 資訊清單檔包含 hello hello asset 的所有檔案清單。 如需詳細資訊，請參閱 [Azure Media Indexer 的工作預設](https://msdn.microsoft.com/library/dn783454.aspx)。

    static bool RunBatchIndexingJob(string[] inputMediaFiles, string outputFolder)
    {
        // Create an asset and upload toostorage.
        IAsset asset = CreateAssetAndUploadMultipleFiles(inputMediaFiles,
            "My Indexing Input Asset - Batch Mode",
            AssetCreationOptions.None);

        // Create a manifest file that contains all hello asset file names and upload toostorage.
        string manifestFile = "input.lst";            
        File.WriteAllLines(manifestFile, asset.AssetFiles.Select(f => f.Name).ToArray());
        var assetFile = asset.AssetFiles.Create(Path.GetFileName(manifestFile));
        assetFile.Upload(manifestFile);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job - Batch Mode");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration.
        string configuration = File.ReadAllText("batch.config");

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task - Batch Mode",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset - Batch Mode", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    private static IAsset CreateAssetAndUploadMultipleFiles(string[] filePaths, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        foreach (string filePath in filePaths)
        {
            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);
        }

        return asset;
    }

### <a name="partially-succeeded-job"></a>部分成功的工作
如果不是所有的輸入的媒體檔案在成功編製索引，hello 索引工作將會失敗，錯誤碼為 4000。 如需詳細資訊，請參閱 [錯誤碼](#error_codes)。

hello 相同的輸出 （與成功的工作） 所產生。 您可以參考 toohello 輸出資訊清單檔案 toofind 哪一個輸入的檔將會失敗，根據 toohello 錯誤資料行值。 失敗的輸入檔，產生的 AIB、 SAMI、 TTML、 WebVTT hello 和關鍵字檔案將不會產生。

### <a id="preset"></a> Azure 媒體索引器的工作預設
藉由提供選擇性的工作預設 hello 工作旁邊，您可以自訂處理從 Azure Media Indexer hello。  hello 以下說明這個組態 xml hello 格式。

| 名稱 | 必要 | 說明 |
| --- | --- | --- |
| **input** |false |您想 tooindex 資產檔案。</p><p>Azure Media Indexer 支援下列媒體檔案格式的 hello: MP4、 WMV、 MP3、 M4A、 WMA、 AAC、 WAV。</p><p>您可以指定 hello 檔案名稱 (s) 中 hello**名稱**或**清單**屬性 hello**輸入**項目 （如下所示）。如果您未指定的資產檔案 tooindex，會挑出 hello 主要檔案。 如果設定主要資產檔案，hello hello 輸入資產中的第一個檔案編製索引。</p><p>tooexplicitly 指定 hello 資產檔案名稱，執行：<br/>`<input name="TestFile.wmv">`<br/><br/>您也可以索引次 （向上 too10 檔案） 的多個資產檔案。 toodo 這樣：<br/><br/><ol class="ordered"><li><p>建立文字檔 (資訊清單檔) 並指定 .lst 副檔名。 </p></li><li><p>您輸入的資產 toothis 資訊清單檔中加入所有 hello 資產檔案名稱的清單。 </p></li><li><p>加入 （上傳） thanifest 檔案 toohello 資產。  </p></li><li><p>Hello 輸入清單屬性中指定 hello hello 資訊清單檔案名稱。<br/>`<input list="input.lst">`</li></ol><br/><br/>注意： 如果您將加入 10 個以上檔案 toohello 資訊清單檔案，hello 編製索引作業會失敗並 hello 2006 錯誤碼。 |
| **metadata** |false |指定用於詞彙調資產檔案 hello 的中繼資料。  有用的 tooprepare 索引子 toorecognize 非標準的詞彙 」 等字詞專有名詞。<br/>`<metadata key="..." value="..."/>` <br/><br/>您可以提供預先定義的**索引鍵**的**值**。 目前支援下列索引鍵的 hello:<br/><br/>「 標題 」 和 「 描述 」-用於詞彙調 tootweak hello 語言模型適用於您作業，並增進語音辨識準確度。  hello 值植入網際網路搜尋 toofind 內容相關的文字文件，使用 hello 內容 tooaugment hello 內部字典索引工作 hello 持續期間。<br/>`<metadata key="title" value="[Title of hello media file]" />`<br/>`<metadata key="description" value="[Description of hello media file] />"` |
| **features** <br/><br/> 在 1.2 版中新增。 目前，僅支援 hello 功能是語音辨識 ("ASR")。 |false |hello 語音辨識功能具有下列設定索引鍵的 hello:<table><tr><th><p>Key</p></th>        <th><p>說明</p></th><th><p>範例值</p></th></tr><tr><td><p>語言</p></td><td><p>hello 自然語言 toobe 辨識 hello 多媒體檔案中。</p></td><td><p>英文、西班牙文</p></td></tr><tr><td><p>CaptionFormats</p></td><td><p>以分號分隔的清單所需的 hello 輸出標題格式 （如果有的話）</p></td><td><p>ttml;sami;webvtt</p></td></tr><tr><td><p>GenerateAIB</p></td><td><p>布林值旗標指出 AIB 檔案必要 （適用於 SQL Server 和 hello 客戶索引子 IFilter）。  如需詳細資訊，請參閱 <a href="http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/">搭配 Azure Media Indexer 和 SQL Server 使用 AIB 檔案</a>。</p></td><td><p>True; False</p></td></tr><tr><td><p>GenerateKeywords</p></td><td><p>布林值旗標，用於指定是否需要關鍵字 XML 檔案。</p></td><td><p>True; False。 </p></td></tr><tr><td><p>ForceFullCaption</p></td><td><p>布林值的旗標，指定完整 tooforce 隱藏式字幕 （不論信心層級）。  </p><p>預設為 false，在此情況下單字和片語具有小於 50%的信心層級會省略 hello 最終標題輸出和被省略符號 （"…"） 取代。  hello 省略符號是適用於標題品質控制和稽核。</p></td><td><p>True; False。 </p></td></tr></table> |

### <a id="error_codes"></a>錯誤碼
Azure Media Indexer 應在 hello 案例中的錯誤，報告下移一 hello 下列錯誤碼：

| 代碼 | 名稱 | 可能的原因 |
| --- | --- | --- |
| 2000 |無效的組態 |無效的組態 |
| 2001 |無效的輸入資產 |遺漏輸入資產或資產是空的。 |
| 2002 |無效的資訊清單 |資訊清單是空的或資訊清單包含無效的項目。 |
| 2003 |失敗的 toodownload 媒體檔案 |資訊清單檔中的 URL 無效。 |
| 2004 |不支援的通訊協定 |不支援媒體 URL 的通訊協定。 |
| 2005 |不支援的檔案類型 |不支援輸入媒體檔案類型。 |
| 2006 |太多輸入檔案 |Hello 輸入資訊清單中有 10 個以上的檔案。 |
| 3000 |失敗的 toodecode 媒體檔案 |不支援的媒體轉碼器  <br/>或<br/> 損毀的媒體檔案 <br/>或<br/> 輸入媒體沒有音訊資料流。 |
| 4000 |批次編製索引已部分成功 |Hello 輸入媒體檔案的某些失敗 toobe 編製索引。 如需詳細資訊，請參閱<a href="#output_files">輸出檔案</a>。 |
| 其他 |內部錯誤 |請連絡技術支援小組。 indexer@microsoft.com |

## <a id="supported_languages"></a>支援的語言
目前支援 hello 英文和西班牙文語言。 如需詳細資訊，請參閱[hello v1.2 發行部落格文章](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/)。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>相關連結
[Azure 媒體服務分析概觀](media-services-analytics-overview.md)

[搭配 Azure Media Indexer 和 SQL Server 使用 AIB 檔案](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)

[使用 Azure Media Indexer 2 Preview 編製媒體檔案索引](media-services-process-content-with-indexer2.md)


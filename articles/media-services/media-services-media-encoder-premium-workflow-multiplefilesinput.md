---
title: "aaaMultiple 輸入檔案，並使用 Premium 編碼器-Azure 元件屬性 |Microsoft 文件"
description: "本主題說明如何 toouse setRuntimeProperties toouse 多個輸入檔案，並傳遞自訂資料 toohello 媒體編碼器高階工作流程媒體處理器。"
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a>搭配進階編碼器使用多個輸入檔案和元件屬性
## <a name="overview"></a>概觀
您可能需要 toocustomize 元件內容 的情況下指定剪輯清單的 XML 內容，或傳送多個輸入的檔，當您送出 hello 的工作**媒體編碼器高階工作流程**媒體處理器。 部分範例如下：

* 視訊重疊顯示文字，並設定在執行階段針對每個輸入視訊的 hello 文字值 (例如，hello 目前的日期)。
* 自訂 hello 剪輯清單 XML (toospecify 一或多個原始程式檔，不論修剪，等等)。。
* Hello 視訊會編碼時，請在 hello 輸入視訊重疊標誌影像。
* 多重音訊語言編碼。

toolet hello**媒體編碼器高階工作流程**知道您要變更 hello 工作流程中的某些屬性，當您建立 hello 工作或傳送多個輸入的檔，設定字串，包含有 toouse **setRuntimeProperties**及/或**transcodeSource**。 本主題說明如何 toouse 它們。

## <a name="configuration-string-syntax"></a>組態字串語法
hello 組態字串 tooset hello 編碼工作中的使用 XML 文件看起來像這樣：

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

hello 以下是從檔案讀取 hello XML 組態的 hello C# 程式碼，更新其與 hello 右視訊檔名，並將其作業中傳遞 toohello 工作：

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a>自訂元件屬性
### <a name="property-with-a-simple-value"></a>具有簡單值的屬性
在某些情況下，很有用 toocustomize hello 即將 toobe 媒體編碼器高階工作流程所執行的工作流程檔案以及元件屬性。

假設您在您的視訊，設計工作流程的影像覆疊文字的 hello 文字 (例如，hello 目前的日期) 應該在執行階段 toobe 組。 您可以傳送 hello 文字 toobe 從編碼工作的 hello 設定作為 hello hello 重疊元件的 hello 文字屬性的新值。 您可以在 hello （例如 hello 位置或 hello 重疊的色彩、 hello 位元速率 hello AVC 編碼器等等） 的工作流程中使用這個機制 toochange 元件的其他屬性。

**setRuntimeProperties**是使用的 toooverride hello 元件 hello 工作流程中的屬性。

範例：

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a>具有 XML 值的屬性
使用封裝 tooset XML 值，必須要有屬性`<![CDATA[ and ]]>`。

範例：

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> 請確定 tooput 歸位字元之後傳回`<![CDATA[`。

### <a name="propertypath-value"></a>propertyPath 值
Hello propertyPath 已在 hello 前一個範例中，"/ 媒體檔案輸入/filename"或"/ inactiveTimeout"或"clipListXml"。
一般情況下，這是 hello hello 元件名稱則 hello hello 屬性名稱。 hello 路徑可以有更多或較少的層級，例如"/ primarySourceFile 」 （因為 hello 屬性是根目錄 hello 工作流程的 hello） 或"/ 視訊處理/圖形重疊不透明度 」 （因為 hello 重疊所屬的群組）。    

toocheck hello 路徑和屬性名稱，會立即出現在每個屬性旁邊的使用 hello 動作按鈕。 您可以按一下這個動作按鈕，然後選取 [編輯] 。 這會顯示您 hello 實際名稱的 hello 屬性，並立即上面，hello 命名空間。

![動作/編輯](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![屬性](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a>多個輸入檔案
每個工作在提交 toohello**媒體編碼器高階工作流程**需要兩個資產：

* hello 第一次是*工作流程資產*，其中包含工作流程檔案。 您可以使用 hello 來設計工作流程檔案[工作流程設計工具](media-services-workflow-designer.md)。
* hello 第二個是*媒體資產*，其中包含您想 tooencode hello 媒體檔案。

當您要傳送多個媒體檔案 toohello**媒體編碼器高階工作流程**編碼器，將套用下列條件約束的 hello:

* 檔案必須位於所有都 hello 媒體都 hello 相同*媒體資產*。 不支援使用多個媒體資產。
* 您必須設定 hello 主要檔案中此媒體資產 (理想情況下，這是 hello 主要 hello 編碼器的視訊檔會要求 tooprocess)。
* 它是必要的 toopass 組態資料，包括 hello **setRuntimeProperties**及/或**transcodeSource**元素 toohello 處理器。
  * **setRuntimeProperties**使用的 toooverride hello filename 屬性或 hello 元件 hello 工作流程中的另一個屬性。
  * **transcodeSource**為使用的 toospecify hello 剪輯清單的 XML 內容。

Hello 工作流程中的連線：

* 如果您使用一或多個媒體檔案輸入元件，並計劃 toouse **setRuntimeProperties** toospecify hello 檔案名稱，則不要連線 hello 主要檔案元件 pin toothem。 請確定沒有 hello 主要檔案 」 物件與 hello 媒體檔案輸入之間的連線。
* 如果您偏好 toouse 剪輯清單 XML 和一個媒體來源元件，然後您可以連接兩者都在一起。

![從主要原始程式檔 tooMedia 檔案輸入沒有連接](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

*如果您使用 setRuntimeProperties tooset hello filename 屬性，沒有 hello 主要檔案 tooMedia 檔案輸入元件的連接。*

![從剪輯清單 XML tooClip 清單來源的連接](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

*您可以連接剪輯清單 XML tooMedia 來源，並使用 transcodeSource。*

### <a name="clip-list-xml-customization"></a>剪輯清單 XML 自訂
您也可以使用在執行階段的 hello 工作流程中指定 hello 剪輯清單 XML **transcodeSource** hello 組態中的 XML 字串。 這需要 hello 剪輯清單中的 XML pin toobe 連接 toohello 媒體來源元件 hello 工作流程。

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

如果您想 toospecify /primarySourceFile toouse 屬性 tooname hello 輸出檔案使用 '運算式'，則我們建議當做屬性傳遞 hello 剪輯清單 XML*之後*hello /primarySourceFile 屬性、 tooavoid具有 hello 剪輯清單可覆寫 hello /primarySourceFile 設定。

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

具有其他框架精確修剪︰

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a>範例 1： 重疊在 hello 視訊頂端的影像

### <a name="presentation"></a>展示
請考慮使用的範例想 toooverlay 標誌影像上 hello 輸入視訊時 hello 視訊會編碼。 在此範例中，名為"Microsoft_HoloLens_Possibilities_816p24.mp4"hello 輸入的視訊和名為"logo.png"hello 標誌。 您應該執行下列步驟的 hello:

* 建立工作流程資產 hello 工作流程檔案 （請參閱下列範例中的 hello）。
* 建立媒體資產，其中包含兩個檔案： MyInputVideo.mp4 hello 主要檔案和 MyLogo.png 如下。
* 傳送工作 toohello 媒體編碼器高階工作流程媒體處理器 hello 上述輸入資產，並指定下列組態字串 hello。

組態:

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Hello 上述範例中，在傳送 toohello 媒體檔案輸入元件和 hello primarySourceFile 屬性 hello hello 視訊檔名稱。 hello hello 標誌檔案名稱會傳送 tooanother 媒體檔案輸入，其中連接的 toohello 圖形重疊部分。

> [!NOTE]
> toohello primarySourceFile 屬性時，會傳送 hello 視訊檔名稱。 hello 這個錯誤的原因是 toouse hello 工作流程建置 hello 正確輸出檔案名稱，例如使用運算式，這個屬性。

### <a name="step-by-step-workflow-creation"></a>逐步建立工作流程
以下是使用兩個檔案做為輸入的工作流程 hello 步驟 toocreate： 視訊和影像。 它將會重疊在 hello 視訊頂端 hello 映像。

開啟**工作流程設計工具**，然後選取 [檔案] > [新增工作區] > [轉碼藍圖]。

hello 新工作流程將示範三個項目：

* 主要來源檔案
* 剪輯清單 XML
* 輸出檔案/資產  

![新編碼工作流程](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

*新編碼工作流程*

在訂單 tooaccept hello 輸入的媒體檔案中，開始新增媒體檔案輸入的元件。 tooadd 元件 toohello 的工作流程，hello 儲存機制搜尋 方塊中尋找它，並將 hello 預期項目拖曳至 hello 設計工具窗格。

接下來，加入 hello 視訊檔 toobe 用來設計您的工作流程。 toodo，按一下 工作流程設計工具中的 hello 背景窗格，並尋找在 hello 右側的屬性窗格中的 hello 主要原始程式檔屬性。 按一下 hello 資料夾圖示，並選取 hello 適當的視訊檔案。

![主要檔案來源](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

*主要檔案來源*

接下來，指定 hello 媒體檔案輸入元件中的 hello 視訊檔案。   

![媒體檔案輸入來源](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

*媒體檔案輸入來源*

進行此設定，如 hello 媒體檔案輸入元件會檢查 hello 檔案，並填入它檢查其輸出 pin tooreflect hello 檔案。

hello 下一個步驟是 tooadd"視訊資料型別 Updater"toospecify hello 色彩空間 tooRec.709。 新增 「 視訊格式轉換程式 」 設定 tooData 配置/配置類型 = 可設定平面。 這會將轉換為 hello 重疊元件的來源可以採取的 hello 視訊串流 tooa 格式。

![視訊資料類型更新器和格式轉換器](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

*視訊資料類型更新器和格式轉換器*

![配置類型 = 可設定平面](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<bpt id="p1">*</bpt>Layout type is Configurable Planar<ept id="p1">*</ept>

接下來，將視訊重疊的元件，並連接到 hello （未壓縮） 視訊 pin toohello （未壓縮） 視訊 pin 的 hello 媒體檔案輸入。

加入另一個媒體檔案輸入 （tooload hello 標誌檔案），然後按一下此元件再將它重新命名過 「 媒體檔案輸入標誌 」，然後選取 hello 檔案屬性中的映像 （例如.png 檔案）。 連接到 hello 未壓縮映像 pin toohello 未壓縮映像 pin 的 hello 重疊。

![覆疊元件和影像檔案來源](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

*覆疊元件和影像檔案來源*

如果您想要的 hello 視訊的 hello 標誌 toomodify hello 位置 (例如，您可能想 tooposition 它在遠離 hello 前百分之 10 的左上角 hello 視訊)，請清除 hello 「 手動輸入 」 核取方塊。 您可以執行這項操作，因為您使用的媒體檔案輸入 tooprovide hello 標誌檔案 toohello 重疊元件。

![覆疊位置](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

*覆疊位置*

tooencode hello tooH.264 視訊資料流中，新增 hello AVC 視訊編碼程式 AAC 編碼器元件 toohello 設計工具介面。 連接 hello 的 pin。
設定 hello AAC 編碼器，並選取音訊格式轉換/預設值： 2.0 （L、 R）。

![音訊和視訊編碼器](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

*音訊和視訊編碼器*

現在，加入 hello **ISO mpeg-4 多工器**和**檔案輸出**元件和連線 hello 的 pin 所示。

![MP4 多工器和輸出檔案](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

*MP4 多工器和輸出檔案*

您需要 tooset hello hello 輸出檔的名稱。 按一下 hello**檔案輸出**hello 檔案的元件，並編輯 hello 運算式：

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![檔案輸出名稱](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

*檔案輸出名稱*

您可以執行 hello 工作流程在本機 toocheck 已正確執行。

完成之後，您就可以在 Azure 媒體服務中執行它。

首先，準備在 Azure Media Services 資產含有兩個檔案中： hello 視訊檔和 hello 標誌。 您可以使用 hello.NET 或 REST API。 您同樣可以這樣使用 hello Azure 入口網站或[Azure 媒體服務總管](https://github.com/Azure/Azure-Media-Services-Explorer)(AMSE)。

本教學課程示範如何使用 AMSE toomanage 資產。 有兩種方式 tooadd 檔案 tooan 資產：

* 建立本機資料夾、 hello 兩個檔案複製，並拖曳和卸除 hello 資料夾 toohello**資產** 索引標籤。
* 為資產的 hello 視訊檔案上傳顯示 hello 資產資訊、 toohello 檔案 索引標籤，請上傳其他檔案 （標誌）。

> [!NOTE]
> 請確定 tooset 主要檔案 hello 資產 （hello 主視訊檔案） 中。

![AMSE 中的資產檔案](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

*AMSE 中的資產檔案*

選取 hello 資產，並選擇 tooencode Premium 編碼器使用。 上傳 hello 工作流程，並加以選取。

按一下 [hello] 按鈕 toopass 資料 toohello 處理器，並加入下列 XML tooset hello 執行階段屬性的 hello:

![AMSE 中的進階編碼器](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

*AMSE 中的進階編碼器*

然後，貼上下列 XML 資料的 hello。 您需要 hello 媒體檔案輸入和 primarySourceFile toospecify hello hello 視訊檔案名稱。 太指定 hello 名稱 hello hello 標誌的檔案名稱。

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

*setRuntimeProperties*

如果您使用 hello.NET SDK toocreate 執行 hello 工作時，此 XML 資料具有 toobe hello 組態字串形式傳遞。

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

Hello 工作完成後，在 hello hello MP4 檔案輸出資產會顯示 hello 重疊 ！

![在 hello 視訊重疊](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

*在 hello 視訊重疊*

您可以下載 hello 範例工作流程從[GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/)。

## <a name="example-2--multiple-audio-language-encoding"></a>範例 2：多重音訊語言編碼

您可以在 [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding) 上取得多重音訊語言編碼工作流程的範例。

此資料夾包含範例工作流程可以是使用的 tooencode MXF 檔案 tooa 多重 MP4 檔案資產多重音訊音軌。

此工作流程會假設該 hello MXF 檔案包含一個音訊播放軌。hello 其他音訊音軌應該傳遞為不同的音訊檔案 （WAV 或 MP4...）。

tooencode，請遵循下列步驟：

* 建立 Media Services 資產 hello MXF 檔案與 hello 音訊檔案 （0 too18 音訊檔案）。
* 請確定該 hello MXF 檔案已設定為主要檔案。
* 建立作業和工作，使用 hello 高階工作流程編碼器處理器。 使用 hello (MultiMP4-1080p-19audio-v1.workflow) 所提供的工作流程。
* （如果您使用 Azure 媒體服務總管 中，使用 hello"pass xml 資料 toohello 工作流程"按鈕），請傳遞 hello setruntime.xml 資料 toohello 工作。
  * 請更新 hello XML 資料 toospecify hello 正確的檔案名稱和語言標記。
  * hello 工作流程具有名為音訊 1 tooAudio 18 音訊的元件。
  * 支援 RFC5646 hello 語言標記。

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* hello 編碼資產將會包含多重語言音訊音軌，這些追蹤都應該是在 Azure Media Player 中可選取。

## <a name="see-also"></a>另請參閱
* [介紹 Azure 媒體服務中的 Premium 編碼](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [如何在 Azure Media Services 編碼 Premium toouse](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [使用 Azure 媒體服務編碼隨選內容](media-services-encode-asset.md#media-encoder-premium-workflow)
* [媒體編碼器高階工作流程格式和轉碼器](media-services-premium-workflow-encoder-formats.md)
* [範例工作流程檔案](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [Azure 媒體服務總管工具](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

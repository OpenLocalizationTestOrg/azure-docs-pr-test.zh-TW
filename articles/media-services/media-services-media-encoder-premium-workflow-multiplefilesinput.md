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
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="d52e5-103">搭配進階編碼器使用多個輸入檔案和元件屬性</span><span class="sxs-lookup"><span data-stu-id="d52e5-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="d52e5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d52e5-104">Overview</span></span>
<span data-ttu-id="d52e5-105">您可能需要 toocustomize 元件內容 的情況下指定剪輯清單的 XML 內容，或傳送多個輸入的檔，當您送出 hello 的工作**媒體編碼器高階工作流程**媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="d52e5-105">There are scenarios in which you might need toocustomize component properties, specify Clip List XML content, or send multiple input files when you submit a task with hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="d52e5-106">部分範例如下：</span><span class="sxs-lookup"><span data-stu-id="d52e5-106">Some examples are:</span></span>

* <span data-ttu-id="d52e5-107">視訊重疊顯示文字，並設定在執行階段針對每個輸入視訊的 hello 文字值 (例如，hello 目前的日期)。</span><span class="sxs-lookup"><span data-stu-id="d52e5-107">Overlaying text on video and setting hello text value (for example, hello current date) at runtime for each input video.</span></span>
* <span data-ttu-id="d52e5-108">自訂 hello 剪輯清單 XML (toospecify 一或多個原始程式檔，不論修剪，等等)。。</span><span class="sxs-lookup"><span data-stu-id="d52e5-108">Customizing hello Clip List XML (toospecify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="d52e5-109">Hello 視訊會編碼時，請在 hello 輸入視訊重疊標誌影像。</span><span class="sxs-lookup"><span data-stu-id="d52e5-109">Overlaying a logo image on hello input video while hello video is encoded.</span></span>
* <span data-ttu-id="d52e5-110">多重音訊語言編碼。</span><span class="sxs-lookup"><span data-stu-id="d52e5-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="d52e5-111">toolet hello**媒體編碼器高階工作流程**知道您要變更 hello 工作流程中的某些屬性，當您建立 hello 工作或傳送多個輸入的檔，設定字串，包含有 toouse **setRuntimeProperties**及/或**transcodeSource**。</span><span class="sxs-lookup"><span data-stu-id="d52e5-111">toolet hello **Media Encoder Premium Workflow** know that you are changing some properties in hello workflow when you create hello task or send multiple input files, you have toouse a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="d52e5-112">本主題說明如何 toouse 它們。</span><span class="sxs-lookup"><span data-stu-id="d52e5-112">This topic explains how toouse them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="d52e5-113">組態字串語法</span><span class="sxs-lookup"><span data-stu-id="d52e5-113">Configuration string syntax</span></span>
<span data-ttu-id="d52e5-114">hello 組態字串 tooset hello 編碼工作中的使用 XML 文件看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="d52e5-114">hello configuration string tooset in hello encoding task uses an XML document that looks like this:</span></span>

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

<span data-ttu-id="d52e5-115">hello 以下是從檔案讀取 hello XML 組態的 hello C# 程式碼，更新其與 hello 右視訊檔名，並將其作業中傳遞 toohello 工作：</span><span class="sxs-lookup"><span data-stu-id="d52e5-115">hello following is hello C# code that reads hello XML configuration from a file, update it with hello right video filename and passes it toohello task in a job:</span></span>

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

## <a name="customizing-component-properties"></a><span data-ttu-id="d52e5-116">自訂元件屬性</span><span class="sxs-lookup"><span data-stu-id="d52e5-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="d52e5-117">具有簡單值的屬性</span><span class="sxs-lookup"><span data-stu-id="d52e5-117">Property with a simple value</span></span>
<span data-ttu-id="d52e5-118">在某些情況下，很有用 toocustomize hello 即將 toobe 媒體編碼器高階工作流程所執行的工作流程檔案以及元件屬性。</span><span class="sxs-lookup"><span data-stu-id="d52e5-118">In some cases, it is useful toocustomize a component property together with hello workflow file that is going toobe executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="d52e5-119">假設您在您的視訊，設計工作流程的影像覆疊文字的 hello 文字 (例如，hello 目前的日期) 應該在執行階段 toobe 組。</span><span class="sxs-lookup"><span data-stu-id="d52e5-119">Suppose you designed a workflow that overlays text on your videos, and hello text (for example, hello current date) is supposed toobe set at runtime.</span></span> <span data-ttu-id="d52e5-120">您可以傳送 hello 文字 toobe 從編碼工作的 hello 設定作為 hello hello 重疊元件的 hello 文字屬性的新值。</span><span class="sxs-lookup"><span data-stu-id="d52e5-120">You can do this by sending hello text toobe set as hello new value for hello text property of hello overlay component from hello encoding task.</span></span> <span data-ttu-id="d52e5-121">您可以在 hello （例如 hello 位置或 hello 重疊的色彩、 hello 位元速率 hello AVC 編碼器等等） 的工作流程中使用這個機制 toochange 元件的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="d52e5-121">You can use this mechanism toochange other properties of a component in hello workflow (such as hello position or color of hello overlay, hello bitrate of hello AVC encoder, etc.).</span></span>

<span data-ttu-id="d52e5-122">**setRuntimeProperties**是使用的 toooverride hello 元件 hello 工作流程中的屬性。</span><span class="sxs-lookup"><span data-stu-id="d52e5-122">**setRuntimeProperties** is used toooverride a property in hello components of hello workflow.</span></span>

<span data-ttu-id="d52e5-123">範例：</span><span class="sxs-lookup"><span data-stu-id="d52e5-123">Example:</span></span>

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

### <a name="property-with-an-xml-value"></a><span data-ttu-id="d52e5-124">具有 XML 值的屬性</span><span class="sxs-lookup"><span data-stu-id="d52e5-124">Property with an XML value</span></span>
<span data-ttu-id="d52e5-125">使用封裝 tooset XML 值，必須要有屬性`<![CDATA[ and ]]>`。</span><span class="sxs-lookup"><span data-stu-id="d52e5-125">tooset a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="d52e5-126">範例：</span><span class="sxs-lookup"><span data-stu-id="d52e5-126">Example:</span></span>

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
> <span data-ttu-id="d52e5-127">請確定 tooput 歸位字元之後傳回`<![CDATA[`。</span><span class="sxs-lookup"><span data-stu-id="d52e5-127">Make sure not tooput a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="d52e5-128">propertyPath 值</span><span class="sxs-lookup"><span data-stu-id="d52e5-128">propertyPath value</span></span>
<span data-ttu-id="d52e5-129">Hello propertyPath 已在 hello 前一個範例中，"/ 媒體檔案輸入/filename"或"/ inactiveTimeout"或"clipListXml"。</span><span class="sxs-lookup"><span data-stu-id="d52e5-129">In hello previous examples, hello propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="d52e5-130">一般情況下，這是 hello hello 元件名稱則 hello hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="d52e5-130">This is, in general, hello name of hello component, then hello name of hello property.</span></span> <span data-ttu-id="d52e5-131">hello 路徑可以有更多或較少的層級，例如"/ primarySourceFile 」 （因為 hello 屬性是根目錄 hello 工作流程的 hello） 或"/ 視訊處理/圖形重疊不透明度 」 （因為 hello 重疊所屬的群組）。</span><span class="sxs-lookup"><span data-stu-id="d52e5-131">hello path can have more or fewer levels, like "/primarySourceFile" (because hello property is at hello root of hello workflow) or "/Video Processing/Graphic Overlay/Opacity" (because hello Overlay is in a group).</span></span>    

<span data-ttu-id="d52e5-132">toocheck hello 路徑和屬性名稱，會立即出現在每個屬性旁邊的使用 hello 動作按鈕。</span><span class="sxs-lookup"><span data-stu-id="d52e5-132">toocheck hello path and property name, use hello action button that is immediately beside each property.</span></span> <span data-ttu-id="d52e5-133">您可以按一下這個動作按鈕，然後選取 [編輯] 。</span><span class="sxs-lookup"><span data-stu-id="d52e5-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="d52e5-134">這會顯示您 hello 實際名稱的 hello 屬性，並立即上面，hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="d52e5-134">This will show you hello actual name of hello property, and immediately above it, hello namespace.</span></span>

![動作/編輯](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![屬性](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="d52e5-137">多個輸入檔案</span><span class="sxs-lookup"><span data-stu-id="d52e5-137">Multiple input files</span></span>
<span data-ttu-id="d52e5-138">每個工作在提交 toohello**媒體編碼器高階工作流程**需要兩個資產：</span><span class="sxs-lookup"><span data-stu-id="d52e5-138">Each task that you submit toohello **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="d52e5-139">hello 第一次是*工作流程資產*，其中包含工作流程檔案。</span><span class="sxs-lookup"><span data-stu-id="d52e5-139">hello first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="d52e5-140">您可以使用 hello 來設計工作流程檔案[工作流程設計工具](media-services-workflow-designer.md)。</span><span class="sxs-lookup"><span data-stu-id="d52e5-140">You can design workflow files by using hello [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="d52e5-141">hello 第二個是*媒體資產*，其中包含您想 tooencode hello 媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="d52e5-141">hello second one is a *Media Asset* that contains hello media file(s) that you want tooencode.</span></span>

<span data-ttu-id="d52e5-142">當您要傳送多個媒體檔案 toohello**媒體編碼器高階工作流程**編碼器，將套用下列條件約束的 hello:</span><span class="sxs-lookup"><span data-stu-id="d52e5-142">When you're sending multiple media files toohello **Media Encoder Premium Workflow** encoder, hello following constraints apply:</span></span>

* <span data-ttu-id="d52e5-143">檔案必須位於所有都 hello 媒體都 hello 相同*媒體資產*。</span><span class="sxs-lookup"><span data-stu-id="d52e5-143">All hello media files must be in hello same *Media Asset*.</span></span> <span data-ttu-id="d52e5-144">不支援使用多個媒體資產。</span><span class="sxs-lookup"><span data-stu-id="d52e5-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="d52e5-145">您必須設定 hello 主要檔案中此媒體資產 (理想情況下，這是 hello 主要 hello 編碼器的視訊檔會要求 tooprocess)。</span><span class="sxs-lookup"><span data-stu-id="d52e5-145">You must set hello primary file in this Media Asset (ideally, this is hello main video file that hello encoder is asked tooprocess).</span></span>
* <span data-ttu-id="d52e5-146">它是必要的 toopass 組態資料，包括 hello **setRuntimeProperties**及/或**transcodeSource**元素 toohello 處理器。</span><span class="sxs-lookup"><span data-stu-id="d52e5-146">It is necessary toopass configuration data that includes hello **setRuntimeProperties** and/or **transcodeSource** element toohello processor.</span></span>
  * <span data-ttu-id="d52e5-147">**setRuntimeProperties**使用的 toooverride hello filename 屬性或 hello 元件 hello 工作流程中的另一個屬性。</span><span class="sxs-lookup"><span data-stu-id="d52e5-147">**setRuntimeProperties** is used toooverride hello filename property or another property in hello components of hello workflow.</span></span>
  * <span data-ttu-id="d52e5-148">**transcodeSource**為使用的 toospecify hello 剪輯清單的 XML 內容。</span><span class="sxs-lookup"><span data-stu-id="d52e5-148">**transcodeSource** is used toospecify hello Clip List XML content.</span></span>

<span data-ttu-id="d52e5-149">Hello 工作流程中的連線：</span><span class="sxs-lookup"><span data-stu-id="d52e5-149">Connections in hello workflow:</span></span>

* <span data-ttu-id="d52e5-150">如果您使用一或多個媒體檔案輸入元件，並計劃 toouse **setRuntimeProperties** toospecify hello 檔案名稱，則不要連線 hello 主要檔案元件 pin toothem。</span><span class="sxs-lookup"><span data-stu-id="d52e5-150">If you use one or several Media File Input components and plan toouse **setRuntimeProperties** toospecify hello file name, then do not connect hello primary file component pin toothem.</span></span> <span data-ttu-id="d52e5-151">請確定沒有 hello 主要檔案 」 物件與 hello 媒體檔案輸入之間的連線。</span><span class="sxs-lookup"><span data-stu-id="d52e5-151">Make sure that there is no connection between hello primary file object and hello Media File Input(s).</span></span>
* <span data-ttu-id="d52e5-152">如果您偏好 toouse 剪輯清單 XML 和一個媒體來源元件，然後您可以連接兩者都在一起。</span><span class="sxs-lookup"><span data-stu-id="d52e5-152">If you prefer toouse Clip List XML and one Media Source component, then you can connect both together.</span></span>

![從主要原始程式檔 tooMedia 檔案輸入沒有連接](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="d52e5-154">*如果您使用 setRuntimeProperties tooset hello filename 屬性，沒有 hello 主要檔案 tooMedia 檔案輸入元件的連接。*</span><span class="sxs-lookup"><span data-stu-id="d52e5-154">*There is no connection from hello primary file tooMedia File Input component(s) if you use setRuntimeProperties tooset hello filename property.*</span></span>

![從剪輯清單 XML tooClip 清單來源的連接](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="d52e5-156">*您可以連接剪輯清單 XML tooMedia 來源，並使用 transcodeSource。*</span><span class="sxs-lookup"><span data-stu-id="d52e5-156">*You can connect Clip List XML tooMedia Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="d52e5-157">剪輯清單 XML 自訂</span><span class="sxs-lookup"><span data-stu-id="d52e5-157">Clip List XML customization</span></span>
<span data-ttu-id="d52e5-158">您也可以使用在執行階段的 hello 工作流程中指定 hello 剪輯清單 XML **transcodeSource** hello 組態中的 XML 字串。</span><span class="sxs-lookup"><span data-stu-id="d52e5-158">You can specify hello Clip List XML in hello workflow at runtime by using **transcodeSource** in hello configuration string XML.</span></span> <span data-ttu-id="d52e5-159">這需要 hello 剪輯清單中的 XML pin toobe 連接 toohello 媒體來源元件 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="d52e5-159">This requires hello Clip List XML pin toobe connected toohello Media Source component in hello workflow.</span></span>

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

<span data-ttu-id="d52e5-160">如果您想 toospecify /primarySourceFile toouse 屬性 tooname hello 輸出檔案使用 '運算式'，則我們建議當做屬性傳遞 hello 剪輯清單 XML*之後*hello /primarySourceFile 屬性、 tooavoid具有 hello 剪輯清單可覆寫 hello /primarySourceFile 設定。</span><span class="sxs-lookup"><span data-stu-id="d52e5-160">If you want toospecify /primarySourceFile toouse this property tooname hello output files by using 'Expressions', then we recommend passing hello Clip List XML as a property *after* hello /primarySourceFile property, tooavoid having hello Clip List be overridden by hello /primarySourceFile setting.</span></span>

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

<span data-ttu-id="d52e5-161">具有其他框架精確修剪︰</span><span class="sxs-lookup"><span data-stu-id="d52e5-161">With additional frame-accurate trimming:</span></span>

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

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a><span data-ttu-id="d52e5-162">範例 1： 重疊在 hello 視訊頂端的影像</span><span class="sxs-lookup"><span data-stu-id="d52e5-162">Example 1 : Overlay an image on top of hello video</span></span>

### <a name="presentation"></a><span data-ttu-id="d52e5-163">展示</span><span class="sxs-lookup"><span data-stu-id="d52e5-163">Presentation</span></span>
<span data-ttu-id="d52e5-164">請考慮使用的範例想 toooverlay 標誌影像上 hello 輸入視訊時 hello 視訊會編碼。</span><span class="sxs-lookup"><span data-stu-id="d52e5-164">Consider an example in which you want toooverlay a logo image on hello input video while hello video is encoded.</span></span> <span data-ttu-id="d52e5-165">在此範例中，名為"Microsoft_HoloLens_Possibilities_816p24.mp4"hello 輸入的視訊和名為"logo.png"hello 標誌。</span><span class="sxs-lookup"><span data-stu-id="d52e5-165">In this example, hello input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and hello logo is named "logo.png".</span></span> <span data-ttu-id="d52e5-166">您應該執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d52e5-166">You should perform hello following steps:</span></span>

* <span data-ttu-id="d52e5-167">建立工作流程資產 hello 工作流程檔案 （請參閱下列範例中的 hello）。</span><span class="sxs-lookup"><span data-stu-id="d52e5-167">Create a Workflow Asset with hello workflow file (see hello following example).</span></span>
* <span data-ttu-id="d52e5-168">建立媒體資產，其中包含兩個檔案： MyInputVideo.mp4 hello 主要檔案和 MyLogo.png 如下。</span><span class="sxs-lookup"><span data-stu-id="d52e5-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as hello primary file and MyLogo.png.</span></span>
* <span data-ttu-id="d52e5-169">傳送工作 toohello 媒體編碼器高階工作流程媒體處理器 hello 上述輸入資產，並指定下列組態字串 hello。</span><span class="sxs-lookup"><span data-stu-id="d52e5-169">Send a task toohello Media Encoder Premium Workflow media processor with hello above input assets and specify hello following configuration string.</span></span>

<span data-ttu-id="d52e5-170">組態:</span><span class="sxs-lookup"><span data-stu-id="d52e5-170">Configuration:</span></span>

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

<span data-ttu-id="d52e5-171">Hello 上述範例中，在傳送 toohello 媒體檔案輸入元件和 hello primarySourceFile 屬性 hello hello 視訊檔名稱。</span><span class="sxs-lookup"><span data-stu-id="d52e5-171">In hello example above, hello name of hello video file is sent toohello Media File Input component and hello primarySourceFile property.</span></span> <span data-ttu-id="d52e5-172">hello hello 標誌檔案名稱會傳送 tooanother 媒體檔案輸入，其中連接的 toohello 圖形重疊部分。</span><span class="sxs-lookup"><span data-stu-id="d52e5-172">hello name of hello logo file is sent tooanother Media File Input that is connected toohello graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="d52e5-173">toohello primarySourceFile 屬性時，會傳送 hello 視訊檔名稱。</span><span class="sxs-lookup"><span data-stu-id="d52e5-173">hello video file name is sent toohello primarySourceFile property.</span></span> <span data-ttu-id="d52e5-174">hello 這個錯誤的原因是 toouse hello 工作流程建置 hello 正確輸出檔案名稱，例如使用運算式，這個屬性。</span><span class="sxs-lookup"><span data-stu-id="d52e5-174">hello reason for this is toouse this property in hello workflow for building hello correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="d52e5-175">逐步建立工作流程</span><span class="sxs-lookup"><span data-stu-id="d52e5-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="d52e5-176">以下是使用兩個檔案做為輸入的工作流程 hello 步驟 toocreate： 視訊和影像。</span><span class="sxs-lookup"><span data-stu-id="d52e5-176">Here are hello steps toocreate a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="d52e5-177">它將會重疊在 hello 視訊頂端 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="d52e5-177">It will overlay hello image on top of hello video.</span></span>

<span data-ttu-id="d52e5-178">開啟**工作流程設計工具**，然後選取 [檔案] > [新增工作區] > [轉碼藍圖]。</span><span class="sxs-lookup"><span data-stu-id="d52e5-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="d52e5-179">hello 新工作流程將示範三個項目：</span><span class="sxs-lookup"><span data-stu-id="d52e5-179">hello new workflow shows three elements:</span></span>

* <span data-ttu-id="d52e5-180">主要來源檔案</span><span class="sxs-lookup"><span data-stu-id="d52e5-180">Primary Source File</span></span>
* <span data-ttu-id="d52e5-181">剪輯清單 XML</span><span class="sxs-lookup"><span data-stu-id="d52e5-181">Clip List XML</span></span>
* <span data-ttu-id="d52e5-182">輸出檔案/資產</span><span class="sxs-lookup"><span data-stu-id="d52e5-182">Output File/Asset</span></span>  

![新編碼工作流程](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="d52e5-184">*新編碼工作流程*</span><span class="sxs-lookup"><span data-stu-id="d52e5-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="d52e5-185">在訂單 tooaccept hello 輸入的媒體檔案中，開始新增媒體檔案輸入的元件。</span><span class="sxs-lookup"><span data-stu-id="d52e5-185">In order tooaccept hello input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="d52e5-186">tooadd 元件 toohello 的工作流程，hello 儲存機制搜尋 方塊中尋找它，並將 hello 預期項目拖曳至 hello 設計工具窗格。</span><span class="sxs-lookup"><span data-stu-id="d52e5-186">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span>

<span data-ttu-id="d52e5-187">接下來，加入 hello 視訊檔 toobe 用來設計您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="d52e5-187">Next, add hello video file toobe used for designing your workflow.</span></span> <span data-ttu-id="d52e5-188">toodo，按一下 工作流程設計工具中的 hello 背景窗格，並尋找在 hello 右側的屬性窗格中的 hello 主要原始程式檔屬性。</span><span class="sxs-lookup"><span data-stu-id="d52e5-188">toodo so, click hello background pane in Workflow Designer and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="d52e5-189">按一下 hello 資料夾圖示，並選取 hello 適當的視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="d52e5-189">Click hello folder icon and select hello appropriate video file.</span></span>

![主要檔案來源](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="d52e5-191">*主要檔案來源*</span><span class="sxs-lookup"><span data-stu-id="d52e5-191">*Primary File Source*</span></span>

<span data-ttu-id="d52e5-192">接下來，指定 hello 媒體檔案輸入元件中的 hello 視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="d52e5-192">Next, specify hello video file in hello Media File Input component.</span></span>   

![媒體檔案輸入來源](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="d52e5-194">*媒體檔案輸入來源*</span><span class="sxs-lookup"><span data-stu-id="d52e5-194">*Media File Input Source*</span></span>

<span data-ttu-id="d52e5-195">進行此設定，如 hello 媒體檔案輸入元件會檢查 hello 檔案，並填入它檢查其輸出 pin tooreflect hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="d52e5-195">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file that it inspected.</span></span>

<span data-ttu-id="d52e5-196">hello 下一個步驟是 tooadd"視訊資料型別 Updater"toospecify hello 色彩空間 tooRec.709。</span><span class="sxs-lookup"><span data-stu-id="d52e5-196">hello next step is tooadd a "Video Data Type Updater" toospecify hello color space tooRec.709.</span></span> <span data-ttu-id="d52e5-197">新增 「 視訊格式轉換程式 」 設定 tooData 配置/配置類型 = 可設定平面。</span><span class="sxs-lookup"><span data-stu-id="d52e5-197">Add a "Video Format Converter" that is set tooData Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="d52e5-198">這會將轉換為 hello 重疊元件的來源可以採取的 hello 視訊串流 tooa 格式。</span><span class="sxs-lookup"><span data-stu-id="d52e5-198">This will convert hello video stream tooa format that can be taken as a source of hello overlay component.</span></span>

![視訊資料類型更新器和格式轉換器](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="d52e5-200">*視訊資料類型更新器和格式轉換器*</span><span class="sxs-lookup"><span data-stu-id="d52e5-200">*Video Data Type Updater and Format Converter*</span></span>

![配置類型 = 可設定平面](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<bpt id="p1">*</bpt>Layout type is Configurable Planar<ept id="p1">*</ept>

<span data-ttu-id="d52e5-203">接下來，將視訊重疊的元件，並連接到 hello （未壓縮） 視訊 pin toohello （未壓縮） 視訊 pin 的 hello 媒體檔案輸入。</span><span class="sxs-lookup"><span data-stu-id="d52e5-203">Next, add a Video Overlay component and connect hello (uncompressed) video pin toohello (uncompressed) video pin of hello media file input.</span></span>

<span data-ttu-id="d52e5-204">加入另一個媒體檔案輸入 （tooload hello 標誌檔案），然後按一下此元件再將它重新命名過 「 媒體檔案輸入標誌 」，然後選取 hello 檔案屬性中的映像 （例如.png 檔案）。</span><span class="sxs-lookup"><span data-stu-id="d52e5-204">Add another Media File Input (tooload hello logo file), click on this component and rename it too"Media File Input Logo", and select an image (a .png file for example) in hello file property.</span></span> <span data-ttu-id="d52e5-205">連接到 hello 未壓縮映像 pin toohello 未壓縮映像 pin 的 hello 重疊。</span><span class="sxs-lookup"><span data-stu-id="d52e5-205">Connect hello Uncompressed image pin toohello Uncompressed image pin of hello overlay.</span></span>

![覆疊元件和影像檔案來源](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="d52e5-207">*覆疊元件和影像檔案來源*</span><span class="sxs-lookup"><span data-stu-id="d52e5-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="d52e5-208">如果您想要的 hello 視訊的 hello 標誌 toomodify hello 位置 (例如，您可能想 tooposition 它在遠離 hello 前百分之 10 的左上角 hello 視訊)，請清除 hello 「 手動輸入 」 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d52e5-208">If you want toomodify hello position of hello logo on hello video (for example, you might want tooposition it at 10 percent off of hello top left corner of hello video), clear hello "Manual Input" check box.</span></span> <span data-ttu-id="d52e5-209">您可以執行這項操作，因為您使用的媒體檔案輸入 tooprovide hello 標誌檔案 toohello 重疊元件。</span><span class="sxs-lookup"><span data-stu-id="d52e5-209">You can do this because you are using a Media File Input tooprovide hello logo file toohello overlay component.</span></span>

![覆疊位置](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="d52e5-211">*覆疊位置*</span><span class="sxs-lookup"><span data-stu-id="d52e5-211">*Overlay position*</span></span>

<span data-ttu-id="d52e5-212">tooencode hello tooH.264 視訊資料流中，新增 hello AVC 視訊編碼程式 AAC 編碼器元件 toohello 設計工具介面。</span><span class="sxs-lookup"><span data-stu-id="d52e5-212">tooencode hello video stream tooH.264, add hello AVC Video Encoder and AAC encoder components toohello designer surface.</span></span> <span data-ttu-id="d52e5-213">連接 hello 的 pin。</span><span class="sxs-lookup"><span data-stu-id="d52e5-213">Connect hello pins.</span></span>
<span data-ttu-id="d52e5-214">設定 hello AAC 編碼器，並選取音訊格式轉換/預設值： 2.0 （L、 R）。</span><span class="sxs-lookup"><span data-stu-id="d52e5-214">Set up hello AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![音訊和視訊編碼器](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="d52e5-216">*音訊和視訊編碼器*</span><span class="sxs-lookup"><span data-stu-id="d52e5-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="d52e5-217">現在，加入 hello **ISO mpeg-4 多工器**和**檔案輸出**元件和連線 hello 的 pin 所示。</span><span class="sxs-lookup"><span data-stu-id="d52e5-217">Now add hello **ISO Mpeg-4 Multiplexer** and **File Output** components and connect hello pins as shown.</span></span>

![MP4 多工器和輸出檔案](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="d52e5-219">*MP4 多工器和輸出檔案*</span><span class="sxs-lookup"><span data-stu-id="d52e5-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="d52e5-220">您需要 tooset hello hello 輸出檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="d52e5-220">You need tooset hello name for hello output file.</span></span> <span data-ttu-id="d52e5-221">按一下 hello**檔案輸出**hello 檔案的元件，並編輯 hello 運算式：</span><span class="sxs-lookup"><span data-stu-id="d52e5-221">Click hello **File Output** component and edit hello expression for hello file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![檔案輸出名稱](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="d52e5-223">*檔案輸出名稱*</span><span class="sxs-lookup"><span data-stu-id="d52e5-223">*File output name*</span></span>

<span data-ttu-id="d52e5-224">您可以執行 hello 工作流程在本機 toocheck 已正確執行。</span><span class="sxs-lookup"><span data-stu-id="d52e5-224">You can run hello workflow locally toocheck that it is running correctly.</span></span>

<span data-ttu-id="d52e5-225">完成之後，您就可以在 Azure 媒體服務中執行它。</span><span class="sxs-lookup"><span data-stu-id="d52e5-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="d52e5-226">首先，準備在 Azure Media Services 資產含有兩個檔案中： hello 視訊檔和 hello 標誌。</span><span class="sxs-lookup"><span data-stu-id="d52e5-226">First, prepare an asset in Azure Media Services with two files in it: hello video file and hello logo.</span></span> <span data-ttu-id="d52e5-227">您可以使用 hello.NET 或 REST API。</span><span class="sxs-lookup"><span data-stu-id="d52e5-227">You can do this by using hello .NET or REST API.</span></span> <span data-ttu-id="d52e5-228">您同樣可以這樣使用 hello Azure 入口網站或[Azure 媒體服務總管](https://github.com/Azure/Azure-Media-Services-Explorer)(AMSE)。</span><span class="sxs-lookup"><span data-stu-id="d52e5-228">You can also do this by using hello Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="d52e5-229">本教學課程示範如何使用 AMSE toomanage 資產。</span><span class="sxs-lookup"><span data-stu-id="d52e5-229">This tutorial shows you how toomanage assets with AMSE.</span></span> <span data-ttu-id="d52e5-230">有兩種方式 tooadd 檔案 tooan 資產：</span><span class="sxs-lookup"><span data-stu-id="d52e5-230">There are two ways tooadd files tooan asset:</span></span>

* <span data-ttu-id="d52e5-231">建立本機資料夾、 hello 兩個檔案複製，並拖曳和卸除 hello 資料夾 toohello**資產** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d52e5-231">Create a local folder, copy hello two files in it, and drag and drop hello folder toohello **Asset** tab.</span></span>
* <span data-ttu-id="d52e5-232">為資產的 hello 視訊檔案上傳顯示 hello 資產資訊、 toohello 檔案 索引標籤，請上傳其他檔案 （標誌）。</span><span class="sxs-lookup"><span data-stu-id="d52e5-232">Upload hello video file as an asset, display hello asset information, go toohello files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="d52e5-233">請確定 tooset 主要檔案 hello 資產 （hello 主視訊檔案） 中。</span><span class="sxs-lookup"><span data-stu-id="d52e5-233">Make sure tooset a primary file in hello asset (hello main video file).</span></span>

![AMSE 中的資產檔案](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="d52e5-235">*AMSE 中的資產檔案*</span><span class="sxs-lookup"><span data-stu-id="d52e5-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="d52e5-236">選取 hello 資產，並選擇 tooencode Premium 編碼器使用。</span><span class="sxs-lookup"><span data-stu-id="d52e5-236">Select hello asset and choose tooencode it with Premium Encoder.</span></span> <span data-ttu-id="d52e5-237">上傳 hello 工作流程，並加以選取。</span><span class="sxs-lookup"><span data-stu-id="d52e5-237">Upload hello workflow and select it.</span></span>

<span data-ttu-id="d52e5-238">按一下 [hello] 按鈕 toopass 資料 toohello 處理器，並加入下列 XML tooset hello 執行階段屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="d52e5-238">Click hello button toopass data toohello processor, and add hello following XML tooset hello runtime properties:</span></span>

![AMSE 中的進階編碼器](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="d52e5-240">*AMSE 中的進階編碼器*</span><span class="sxs-lookup"><span data-stu-id="d52e5-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="d52e5-241">然後，貼上下列 XML 資料的 hello。</span><span class="sxs-lookup"><span data-stu-id="d52e5-241">Then, paste hello following XML data.</span></span> <span data-ttu-id="d52e5-242">您需要 hello 媒體檔案輸入和 primarySourceFile toospecify hello hello 視訊檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="d52e5-242">You need toospecify hello name of hello video file for both hello Media File Input and primarySourceFile.</span></span> <span data-ttu-id="d52e5-243">太指定 hello 名稱 hello hello 標誌的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="d52e5-243">Specify hello name of hello file name for hello logo too.</span></span>

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

<span data-ttu-id="d52e5-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="d52e5-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="d52e5-246">如果您使用 hello.NET SDK toocreate 執行 hello 工作時，此 XML 資料具有 toobe hello 組態字串形式傳遞。</span><span class="sxs-lookup"><span data-stu-id="d52e5-246">If you use hello .NET SDK toocreate and run hello task, this XML data has toobe passed as hello configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="d52e5-247">Hello 工作完成後，在 hello hello MP4 檔案輸出資產會顯示 hello 重疊 ！</span><span class="sxs-lookup"><span data-stu-id="d52e5-247">After hello job is complete, hello MP4 file in hello output asset displays hello overlay!</span></span>

![在 hello 視訊重疊](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="d52e5-249">*在 hello 視訊重疊*</span><span class="sxs-lookup"><span data-stu-id="d52e5-249">*Overlay on hello video*</span></span>

<span data-ttu-id="d52e5-250">您可以下載 hello 範例工作流程從[GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/)。</span><span class="sxs-lookup"><span data-stu-id="d52e5-250">You can download hello sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="d52e5-251">範例 2：多重音訊語言編碼</span><span class="sxs-lookup"><span data-stu-id="d52e5-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="d52e5-252">您可以在 [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding) 上取得多重音訊語言編碼工作流程的範例。</span><span class="sxs-lookup"><span data-stu-id="d52e5-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="d52e5-253">此資料夾包含範例工作流程可以是使用的 tooencode MXF 檔案 tooa 多重 MP4 檔案資產多重音訊音軌。</span><span class="sxs-lookup"><span data-stu-id="d52e5-253">This folder contains a sample workflow which can be used tooencode a MXF file tooa multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="d52e5-254">此工作流程會假設該 hello MXF 檔案包含一個音訊播放軌。hello 其他音訊音軌應該傳遞為不同的音訊檔案 （WAV 或 MP4...）。</span><span class="sxs-lookup"><span data-stu-id="d52e5-254">This workflow assumes that hello MXF file contains one audio track ; hello additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="d52e5-255">tooencode，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d52e5-255">tooencode, please follow these steps:</span></span>

* <span data-ttu-id="d52e5-256">建立 Media Services 資產 hello MXF 檔案與 hello 音訊檔案 （0 too18 音訊檔案）。</span><span class="sxs-lookup"><span data-stu-id="d52e5-256">Create a Media Services asset with hello MXF file and hello Audio files (0 too18 audio files).</span></span>
* <span data-ttu-id="d52e5-257">請確定該 hello MXF 檔案已設定為主要檔案。</span><span class="sxs-lookup"><span data-stu-id="d52e5-257">Make sure that hello MXF file is set as a primary file.</span></span>
* <span data-ttu-id="d52e5-258">建立作業和工作，使用 hello 高階工作流程編碼器處理器。</span><span class="sxs-lookup"><span data-stu-id="d52e5-258">Create a job and a task using hello Premium Workflow Encoder processor.</span></span> <span data-ttu-id="d52e5-259">使用 hello (MultiMP4-1080p-19audio-v1.workflow) 所提供的工作流程。</span><span class="sxs-lookup"><span data-stu-id="d52e5-259">Use hello workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="d52e5-260">（如果您使用 Azure 媒體服務總管 中，使用 hello"pass xml 資料 toohello 工作流程"按鈕），請傳遞 hello setruntime.xml 資料 toohello 工作。</span><span class="sxs-lookup"><span data-stu-id="d52e5-260">Pass hello setruntime.xml data toohello task (if you use Azure Media Services Explorer, use hello “pass xml data toohello workflow” button).</span></span>
  * <span data-ttu-id="d52e5-261">請更新 hello XML 資料 toospecify hello 正確的檔案名稱和語言標記。</span><span class="sxs-lookup"><span data-stu-id="d52e5-261">Please update hello XML data toospecify hello correct file names and languages tags.</span></span>
  * <span data-ttu-id="d52e5-262">hello 工作流程具有名為音訊 1 tooAudio 18 音訊的元件。</span><span class="sxs-lookup"><span data-stu-id="d52e5-262">hello workflow has audio components named Audio 1 tooAudio 18.</span></span>
  * <span data-ttu-id="d52e5-263">支援 RFC5646 hello 語言標記。</span><span class="sxs-lookup"><span data-stu-id="d52e5-263">RFC5646 is supported for hello language tag.</span></span>

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

* <span data-ttu-id="d52e5-264">hello 編碼資產將會包含多重語言音訊音軌，這些追蹤都應該是在 Azure Media Player 中可選取。</span><span class="sxs-lookup"><span data-stu-id="d52e5-264">hello encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="d52e5-265">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d52e5-265">See also</span></span>
* [<span data-ttu-id="d52e5-266">介紹 Azure 媒體服務中的 Premium 編碼</span><span class="sxs-lookup"><span data-stu-id="d52e5-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="d52e5-267">如何在 Azure Media Services 編碼 Premium toouse</span><span class="sxs-lookup"><span data-stu-id="d52e5-267">How toouse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="d52e5-268">使用 Azure 媒體服務編碼隨選內容</span><span class="sxs-lookup"><span data-stu-id="d52e5-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="d52e5-269">媒體編碼器高階工作流程格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="d52e5-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="d52e5-270">範例工作流程檔案</span><span class="sxs-lookup"><span data-stu-id="d52e5-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="d52e5-271">Azure 媒體服務總管工具</span><span class="sxs-lookup"><span data-stu-id="d52e5-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="d52e5-272">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="d52e5-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d52e5-273">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="d52e5-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

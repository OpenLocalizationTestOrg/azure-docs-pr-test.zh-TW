---
title: "使用進階編碼器的多個輸入檔案和元件屬性 - Azure | Microsoft Docs"
description: "本主題說明如何使用 setRuntimeProperties 來使用多個輸入檔案，並將自訂資料傳遞給「媒體編碼器高階工作流程」媒體處理器。"
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
ms.openlocfilehash: df1ee5089a0af6ffce1431b658843fcb34a66ce5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="13ec6-103">搭配進階編碼器使用多個輸入檔案和元件屬性</span><span class="sxs-lookup"><span data-stu-id="13ec6-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="13ec6-104">概觀</span><span class="sxs-lookup"><span data-stu-id="13ec6-104">Overview</span></span>
<span data-ttu-id="13ec6-105">在某些情況下，您可能需要在使用「媒體編碼器高階工作流程」  媒體處理器提交工作時，自訂元件屬性、指定剪輯清單 XML 內容，或傳送多個輸入檔案。</span><span class="sxs-lookup"><span data-stu-id="13ec6-105">There are scenarios in which you might need to customize component properties, specify Clip List XML content, or send multiple input files when you submit a task with the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="13ec6-106">部分範例如下：</span><span class="sxs-lookup"><span data-stu-id="13ec6-106">Some examples are:</span></span>

* <span data-ttu-id="13ec6-107">在每個輸入視訊的執行階段在視訊上覆疊文字並設定文字值 (例如，目前的日期)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-107">Overlaying text on video and setting the text value (for example, the current date) at runtime for each input video.</span></span>
* <span data-ttu-id="13ec6-108">自訂剪輯清單 XML (以指定一或多個包含或不含修剪的來源檔案等)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-108">Customizing the Clip List XML (to specify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="13ec6-109">視訊編碼時在輸入視訊上覆疊標誌影像。</span><span class="sxs-lookup"><span data-stu-id="13ec6-109">Overlaying a logo image on the input video while the video is encoded.</span></span>
* <span data-ttu-id="13ec6-110">多重音訊語言編碼。</span><span class="sxs-lookup"><span data-stu-id="13ec6-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="13ec6-111">若要在建立工作或傳送多個輸入檔案時，讓**「媒體編碼器高階工作流程」**知道您要變更工作流程中的某些屬性，您必須使用包含 **setRuntimeProperties** 及/或 **transcodeSource** 的組態字串。</span><span class="sxs-lookup"><span data-stu-id="13ec6-111">To let the **Media Encoder Premium Workflow** know that you are changing some properties in the workflow when you create the task or send multiple input files, you have to use a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="13ec6-112">本主題說明如何使用它們。</span><span class="sxs-lookup"><span data-stu-id="13ec6-112">This topic explains how to use them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="13ec6-113">組態字串語法</span><span class="sxs-lookup"><span data-stu-id="13ec6-113">Configuration string syntax</span></span>
<span data-ttu-id="13ec6-114">在編碼工作中設定的組態字串會使用類似下面的 XML 文件︰</span><span class="sxs-lookup"><span data-stu-id="13ec6-114">The configuration string to set in the encoding task uses an XML document that looks like this:</span></span>

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

<span data-ttu-id="13ec6-115">下列 C# 程式碼會從檔案讀取 XML 設定、使用正確的視訊檔名加以更新，並以作業的形式傳遞給工作：</span><span class="sxs-lookup"><span data-stu-id="13ec6-115">The following is the C# code that reads the XML configuration from a file, update it with the right video filename and passes it to the task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass to it the name of the 
// processor to use for the specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with the encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify the input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset to contain the results of the job. 
// This output is specified as AssetCreationOptions.None, which 
// means the output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="13ec6-116">自訂元件屬性</span><span class="sxs-lookup"><span data-stu-id="13ec6-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="13ec6-117">具有簡單值的屬性</span><span class="sxs-lookup"><span data-stu-id="13ec6-117">Property with a simple value</span></span>
<span data-ttu-id="13ec6-118">在某些情況下，適合在「媒體編碼器高階工作流程」將要執行的工作流程檔案中一起自訂元件屬性。</span><span class="sxs-lookup"><span data-stu-id="13ec6-118">In some cases, it is useful to customize a component property together with the workflow file that is going to be executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="13ec6-119">假設您設計了一個在視訊上覆疊文字的工作流程，要在執行階段設定文字 (例如，目前的日期)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-119">Suppose you designed a workflow that overlays text on your videos, and the text (for example, the current date) is supposed to be set at runtime.</span></span> <span data-ttu-id="13ec6-120">您可以從編碼工作傳送要設定為覆疊元件文字屬性新值的文字，執行此動作。</span><span class="sxs-lookup"><span data-stu-id="13ec6-120">You can do this by sending the text to be set as the new value for the text property of the overlay component from the encoding task.</span></span> <span data-ttu-id="13ec6-121">您可以使用這項機制來變更工作流程中元件的其他屬性 (例如覆疊的位置或色彩、AVC 編碼器的位元速率等等)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-121">You can use this mechanism to change other properties of a component in the workflow (such as the position or color of the overlay, the bitrate of the AVC encoder, etc.).</span></span>

<span data-ttu-id="13ec6-122">**setRuntimeProperties** 可用來覆寫工作流程元件中的屬性。</span><span class="sxs-lookup"><span data-stu-id="13ec6-122">**setRuntimeProperties** is used to override a property in the components of the workflow.</span></span>

<span data-ttu-id="13ec6-123">範例：</span><span class="sxs-lookup"><span data-stu-id="13ec6-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text To Image Converter/text" value="Today is Friday the 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="13ec6-124">具有 XML 值的屬性</span><span class="sxs-lookup"><span data-stu-id="13ec6-124">Property with an XML value</span></span>
<span data-ttu-id="13ec6-125">若要設定預期會有 XML 值的屬性，請使用 `<![CDATA[ and ]]>`進行封裝。</span><span class="sxs-lookup"><span data-stu-id="13ec6-125">To set a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="13ec6-126">範例：</span><span class="sxs-lookup"><span data-stu-id="13ec6-126">Example:</span></span>

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
> <span data-ttu-id="13ec6-127">在 `<![CDATA[` 後面請務必不要放入歸位字元。</span><span class="sxs-lookup"><span data-stu-id="13ec6-127">Make sure not to put a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="13ec6-128">propertyPath 值</span><span class="sxs-lookup"><span data-stu-id="13ec6-128">propertyPath value</span></span>
<span data-ttu-id="13ec6-129">在上一個範例中，propertyPath 是 "/Media File Input/filename" 或 "/inactiveTimeout" 或 "clipListXml"。</span><span class="sxs-lookup"><span data-stu-id="13ec6-129">In the previous examples, the propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="13ec6-130">這通常是元件的名稱，然後是屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="13ec6-130">This is, in general, the name of the component, then the name of the property.</span></span> <span data-ttu-id="13ec6-131">路徑可以有更多或更少層級，例如 "/primarySourceFile" (因為屬性是在工作流程的根目錄)，或 "/Video Processing/Graphic Overlay/Opacity" (因為覆疊是在群組中)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-131">The path can have more or fewer levels, like "/primarySourceFile" (because the property is at the root of the workflow) or "/Video Processing/Graphic Overlay/Opacity" (because the Overlay is in a group).</span></span>    

<span data-ttu-id="13ec6-132">若要檢查路徑和屬性名稱，請使用緊鄰每個屬性的動作按鈕。</span><span class="sxs-lookup"><span data-stu-id="13ec6-132">To check the path and property name, use the action button that is immediately beside each property.</span></span> <span data-ttu-id="13ec6-133">您可以按一下這個動作按鈕，然後選取 [編輯] 。</span><span class="sxs-lookup"><span data-stu-id="13ec6-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="13ec6-134">這會對您顯示屬性的實際名稱，並在其正上方顯示命名空間。</span><span class="sxs-lookup"><span data-stu-id="13ec6-134">This will show you the actual name of the property, and immediately above it, the namespace.</span></span>

![動作/編輯](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![屬性](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="13ec6-137">多個輸入檔案</span><span class="sxs-lookup"><span data-stu-id="13ec6-137">Multiple input files</span></span>
<span data-ttu-id="13ec6-138">提交給「媒體編碼器高階工作流程」  的每個工作都需要兩個資產︰</span><span class="sxs-lookup"><span data-stu-id="13ec6-138">Each task that you submit to the **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="13ec6-139">第一個是「工作流程資產」  ，其中包含工作流程檔案。</span><span class="sxs-lookup"><span data-stu-id="13ec6-139">The first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="13ec6-140">您可以使用 [工作流程設計工具](media-services-workflow-designer.md)設計工作流程檔案。</span><span class="sxs-lookup"><span data-stu-id="13ec6-140">You can design workflow files by using the [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="13ec6-141">第二個是「媒體資產」  ，其中包含您想要編碼的媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="13ec6-141">The second one is a *Media Asset* that contains the media file(s) that you want to encode.</span></span>

<span data-ttu-id="13ec6-142">傳送多個媒體檔案給「媒體編碼器高階工作流程」  編碼器時有以下限制︰</span><span class="sxs-lookup"><span data-stu-id="13ec6-142">When you're sending multiple media files to the **Media Encoder Premium Workflow** encoder, the following constraints apply:</span></span>

* <span data-ttu-id="13ec6-143">所有媒體檔案必須位於同一個「媒體資產」 。</span><span class="sxs-lookup"><span data-stu-id="13ec6-143">All the media files must be in the same *Media Asset*.</span></span> <span data-ttu-id="13ec6-144">不支援使用多個媒體資產。</span><span class="sxs-lookup"><span data-stu-id="13ec6-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="13ec6-145">您必須在此媒體資產中設定主要檔案 (在理想情況下，這是要求編碼器處理的主要視訊檔案)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-145">You must set the primary file in this Media Asset (ideally, this is the main video file that the encoder is asked to process).</span></span>
* <span data-ttu-id="13ec6-146">必須將包含 **setRuntimeProperties** 及/或 **transcodeSource** 元素的組態資料傳遞至處理器。</span><span class="sxs-lookup"><span data-stu-id="13ec6-146">It is necessary to pass configuration data that includes the **setRuntimeProperties** and/or **transcodeSource** element to the processor.</span></span>
  * <span data-ttu-id="13ec6-147">**setRuntimeProperties** 可用來覆寫工作流程元件中的檔案名稱屬性或其他屬性。</span><span class="sxs-lookup"><span data-stu-id="13ec6-147">**setRuntimeProperties** is used to override the filename property or another property in the components of the workflow.</span></span>
  * <span data-ttu-id="13ec6-148">**transcodeSource** 可用來指定剪輯清單 XML 內容。</span><span class="sxs-lookup"><span data-stu-id="13ec6-148">**transcodeSource** is used to specify the Clip List XML content.</span></span>

<span data-ttu-id="13ec6-149">工作流程中的連接：</span><span class="sxs-lookup"><span data-stu-id="13ec6-149">Connections in the workflow:</span></span>

* <span data-ttu-id="13ec6-150">如果您使用一或多個媒體檔案輸入元件，並計劃使用 **setRuntimeProperties** 來指定檔案名稱，則請勿將主要檔案元件接點連接到這些元件。</span><span class="sxs-lookup"><span data-stu-id="13ec6-150">If you use one or several Media File Input components and plan to use **setRuntimeProperties** to specify the file name, then do not connect the primary file component pin to them.</span></span> <span data-ttu-id="13ec6-151">確認主要檔案物件和媒體檔案輸入之間沒有連接。</span><span class="sxs-lookup"><span data-stu-id="13ec6-151">Make sure that there is no connection between the primary file object and the Media File Input(s).</span></span>
* <span data-ttu-id="13ec6-152">如果您想要使用剪輯清單 XML 和一個媒體來源元件，則您可以將兩者連接在一起。</span><span class="sxs-lookup"><span data-stu-id="13ec6-152">If you prefer to use Clip List XML and one Media Source component, then you can connect both together.</span></span>

![主要來源檔案未連接至媒體檔案輸入](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="13ec6-154">如果您使用 setRuntimeProperties 來設定檔案名稱屬性，則主要檔案與媒體檔案輸入元件之間不會有連接。</span><span class="sxs-lookup"><span data-stu-id="13ec6-154">*There is no connection from the primary file to Media File Input component(s) if you use setRuntimeProperties to set the filename property.*</span></span>

![剪輯清單 XML 連接至剪輯清單來源](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="13ec6-156">您可以將剪輯清單 XML 連接到媒體來源並使用 transcodeSource。</span><span class="sxs-lookup"><span data-stu-id="13ec6-156">*You can connect Clip List XML to Media Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="13ec6-157">剪輯清單 XML 自訂</span><span class="sxs-lookup"><span data-stu-id="13ec6-157">Clip List XML customization</span></span>
<span data-ttu-id="13ec6-158">您可以在組態字串 XML 中使用 **transcodeSource** ，以在執行階段於工作流程中指定剪輯清單 XML。</span><span class="sxs-lookup"><span data-stu-id="13ec6-158">You can specify the Clip List XML in the workflow at runtime by using **transcodeSource** in the configuration string XML.</span></span> <span data-ttu-id="13ec6-159">這需要剪輯清單 XML 接點才能連接到工作流程中的媒體來源元件。</span><span class="sxs-lookup"><span data-stu-id="13ec6-159">This requires the Clip List XML pin to be connected to the Media Source component in the workflow.</span></span>

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

<span data-ttu-id="13ec6-160">如果您想要指定 /primarySourceFile 使用此屬性，以使用 'Expressions' 來命名輸出檔案，我們建議在 /primarySourceFile 屬性「之後」  將剪輯清單 XML 傳遞為屬性，以避免剪輯清單遭到 /primarySourceFile 設定覆寫。</span><span class="sxs-lookup"><span data-stu-id="13ec6-160">If you want to specify /primarySourceFile to use this property to name the output files by using 'Expressions', then we recommend passing the Clip List XML as a property *after* the /primarySourceFile property, to avoid having the Clip List be overridden by the /primarySourceFile setting.</span></span>

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

<span data-ttu-id="13ec6-161">具有其他框架精確修剪︰</span><span class="sxs-lookup"><span data-stu-id="13ec6-161">With additional frame-accurate trimming:</span></span>

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

## <a name="example-1--overlay-an-image-on-top-of-the-video"></a><span data-ttu-id="13ec6-162">範例 1：在視訊頂端覆疊影像</span><span class="sxs-lookup"><span data-stu-id="13ec6-162">Example 1 : Overlay an image on top of the video</span></span>

### <a name="presentation"></a><span data-ttu-id="13ec6-163">展示</span><span class="sxs-lookup"><span data-stu-id="13ec6-163">Presentation</span></span>
<span data-ttu-id="13ec6-164">請設想視訊編碼時要在輸入視訊上覆疊標誌影像的範例。</span><span class="sxs-lookup"><span data-stu-id="13ec6-164">Consider an example in which you want to overlay a logo image on the input video while the video is encoded.</span></span> <span data-ttu-id="13ec6-165">在此範例中，輸入視訊的名稱為 "Microsoft_HoloLens_Possibilities_816p24.mp4"，而標誌的名稱為 "logo.png"。</span><span class="sxs-lookup"><span data-stu-id="13ec6-165">In this example, the input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and the logo is named "logo.png".</span></span> <span data-ttu-id="13ec6-166">您應執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="13ec6-166">You should perform the following steps:</span></span>

* <span data-ttu-id="13ec6-167">使用工作流程檔案建立工作流程資產 (參閱下列範例)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-167">Create a Workflow Asset with the workflow file (see the following example).</span></span>
* <span data-ttu-id="13ec6-168">建立媒體資產，其中包含兩個檔案︰MyInputVideo.mp4 (主要檔案) 和 MyLogo.png。</span><span class="sxs-lookup"><span data-stu-id="13ec6-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as the primary file and MyLogo.png.</span></span>
* <span data-ttu-id="13ec6-169">使用上述輸入資產將工作傳送至「媒體編碼器高階工作流程」媒體處理器，並指定下列組態字串。</span><span class="sxs-lookup"><span data-stu-id="13ec6-169">Send a task to the Media Encoder Premium Workflow media processor with the above input assets and specify the following configuration string.</span></span>

<span data-ttu-id="13ec6-170">組態:</span><span class="sxs-lookup"><span data-stu-id="13ec6-170">Configuration:</span></span>

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

<span data-ttu-id="13ec6-171">在上述範例中，視訊檔案的名稱會傳送至媒體檔案輸入元件及 primarySourceFile 屬性。</span><span class="sxs-lookup"><span data-stu-id="13ec6-171">In the example above, the name of the video file is sent to the Media File Input component and the primarySourceFile property.</span></span> <span data-ttu-id="13ec6-172">標誌檔案的名稱會傳送至另一個連接至圖形覆疊元件的媒體檔案輸入。</span><span class="sxs-lookup"><span data-stu-id="13ec6-172">The name of the logo file is sent to another Media File Input that is connected to the graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="13ec6-173">視訊檔案名稱會傳送至 primarySourceFile 屬性。</span><span class="sxs-lookup"><span data-stu-id="13ec6-173">The video file name is sent to the primarySourceFile property.</span></span> <span data-ttu-id="13ec6-174">其原因是要在工作流程中使用這個屬性，以便 (舉例來說) 使用運算式建置正確的輸出檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="13ec6-174">The reason for this is to use this property in the workflow for building the correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="13ec6-175">逐步建立工作流程</span><span class="sxs-lookup"><span data-stu-id="13ec6-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="13ec6-176">以下步驟會建立工作流程來將兩個檔案做為輸入︰視訊和影像。</span><span class="sxs-lookup"><span data-stu-id="13ec6-176">Here are the steps to create a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="13ec6-177">它會在視訊頂端覆疊影像。</span><span class="sxs-lookup"><span data-stu-id="13ec6-177">It will overlay the image on top of the video.</span></span>

<span data-ttu-id="13ec6-178">開啟**工作流程設計工具**，然後選取 [檔案] > [新增工作區] > [轉碼藍圖]。</span><span class="sxs-lookup"><span data-stu-id="13ec6-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="13ec6-179">新的工作流程會顯示三個元素︰</span><span class="sxs-lookup"><span data-stu-id="13ec6-179">The new workflow shows three elements:</span></span>

* <span data-ttu-id="13ec6-180">主要來源檔案</span><span class="sxs-lookup"><span data-stu-id="13ec6-180">Primary Source File</span></span>
* <span data-ttu-id="13ec6-181">剪輯清單 XML</span><span class="sxs-lookup"><span data-stu-id="13ec6-181">Clip List XML</span></span>
* <span data-ttu-id="13ec6-182">輸出檔案/資產</span><span class="sxs-lookup"><span data-stu-id="13ec6-182">Output File/Asset</span></span>  

![新編碼工作流程](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="13ec6-184">*新編碼工作流程*</span><span class="sxs-lookup"><span data-stu-id="13ec6-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="13ec6-185">為了接受輸入媒體檔案，請從加入媒體檔案輸入元件開始。</span><span class="sxs-lookup"><span data-stu-id="13ec6-185">In order to accept the input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="13ec6-186">若要將元件加入至工作流程，請在 [儲存機制] 搜尋方塊中尋找它，然後將所需的項目拖曳至設計工具窗格。</span><span class="sxs-lookup"><span data-stu-id="13ec6-186">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span></span>

<span data-ttu-id="13ec6-187">接著，新增要用於設計工作流程的視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="13ec6-187">Next, add the video file to be used for designing your workflow.</span></span> <span data-ttu-id="13ec6-188">若要這樣做，請按一下工作流程設計工具的背景窗格，並在右手邊的屬性窗格中尋找 [主要來源檔案] 屬性。</span><span class="sxs-lookup"><span data-stu-id="13ec6-188">To do so, click the background pane in Workflow Designer and look for the Primary Source File property on the right-hand property pane.</span></span> <span data-ttu-id="13ec6-189">按一下資料夾圖示，然後選取適當的視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="13ec6-189">Click the folder icon and select the appropriate video file.</span></span>

![主要檔案來源](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="13ec6-191">*主要檔案來源*</span><span class="sxs-lookup"><span data-stu-id="13ec6-191">*Primary File Source*</span></span>

<span data-ttu-id="13ec6-192">接下來，在媒體檔案輸入元件中指定視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="13ec6-192">Next, specify the video file in the Media File Input component.</span></span>   

![媒體檔案輸入來源](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="13ec6-194">*媒體檔案輸入來源*</span><span class="sxs-lookup"><span data-stu-id="13ec6-194">*Media File Input Source*</span></span>

<span data-ttu-id="13ec6-195">完成此動作之後，媒體檔案輸入元件會檢查檔案，並填入其輸出接點，以反映它檢查的檔案。</span><span class="sxs-lookup"><span data-stu-id="13ec6-195">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file that it inspected.</span></span>

<span data-ttu-id="13ec6-196">下一個步驟是新增「視訊資料類型更新器」以對 Rec.709 指定色彩空間。</span><span class="sxs-lookup"><span data-stu-id="13ec6-196">The next step is to add a "Video Data Type Updater" to specify the color space to Rec.709.</span></span> <span data-ttu-id="13ec6-197">新增「資料配置/配置類型 = 可設定平面」的「視訊格式轉換器」。</span><span class="sxs-lookup"><span data-stu-id="13ec6-197">Add a "Video Format Converter" that is set to Data Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="13ec6-198">這會將視訊串流轉換成可以當做覆疊元件來源的格式。</span><span class="sxs-lookup"><span data-stu-id="13ec6-198">This will convert the video stream to a format that can be taken as a source of the overlay component.</span></span>

![視訊資料類型更新器和格式轉換器](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="13ec6-200">*視訊資料類型更新器和格式轉換器*</span><span class="sxs-lookup"><span data-stu-id="13ec6-200">*Video Data Type Updater and Format Converter*</span></span>

![配置類型 = 可設定平面](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<bpt id="p1">*</bpt>Layout type is Configurable Planar<ept id="p1">*</ept>

<span data-ttu-id="13ec6-203">接下來，新增視訊覆疊元件，並將 (未壓縮的) 視訊接點連接至媒體檔案輸入的 (未壓縮的) 視訊接點。</span><span class="sxs-lookup"><span data-stu-id="13ec6-203">Next, add a Video Overlay component and connect the (uncompressed) video pin to the (uncompressed) video pin of the media file input.</span></span>

<span data-ttu-id="13ec6-204">新增另一個媒體檔案輸入 (以載入標誌檔案)、按一下這個元件、將它重新命名為「媒體檔案輸入標誌」，然後在檔案屬性中選取影像 (例如 .png 檔案)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-204">Add another Media File Input (to load the logo file), click on this component and rename it to "Media File Input Logo", and select an image (a .png file for example) in the file property.</span></span> <span data-ttu-id="13ec6-205">將未壓縮的影像接點連接到覆疊的未壓縮影像接點。</span><span class="sxs-lookup"><span data-stu-id="13ec6-205">Connect the Uncompressed image pin to the Uncompressed image pin of the overlay.</span></span>

![覆疊元件和影像檔案來源](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="13ec6-207">*覆疊元件和影像檔案來源*</span><span class="sxs-lookup"><span data-stu-id="13ec6-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="13ec6-208">如果您想要修改視訊的標誌位置 (例如，您要將它放在距離視訊左上角 10% 之處)，請清除 [手動輸入] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="13ec6-208">If you want to modify the position of the logo on the video (for example, you might want to position it at 10 percent off of the top left corner of the video), clear the "Manual Input" check box.</span></span> <span data-ttu-id="13ec6-209">由於您使用媒體檔案輸入來提供標誌檔案給覆疊元件，您可以執行此動作。</span><span class="sxs-lookup"><span data-stu-id="13ec6-209">You can do this because you are using a Media File Input to provide the logo file to the overlay component.</span></span>

![覆疊位置](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="13ec6-211">*覆疊位置*</span><span class="sxs-lookup"><span data-stu-id="13ec6-211">*Overlay position*</span></span>

<span data-ttu-id="13ec6-212">若要將視訊串流編碼成 H.264，請將 AVC 視訊編碼器和 AAC 編碼器元件加入至設計工具介面。</span><span class="sxs-lookup"><span data-stu-id="13ec6-212">To encode the video stream to H.264, add the AVC Video Encoder and AAC encoder components to the designer surface.</span></span> <span data-ttu-id="13ec6-213">連接接點。</span><span class="sxs-lookup"><span data-stu-id="13ec6-213">Connect the pins.</span></span>
<span data-ttu-id="13ec6-214">設定 AAC 編碼器，然後選取「音訊格式轉換/預設值 : 2.0 (L, R)」。</span><span class="sxs-lookup"><span data-stu-id="13ec6-214">Set up the AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![音訊和視訊編碼器](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="13ec6-216">*音訊和視訊編碼器*</span><span class="sxs-lookup"><span data-stu-id="13ec6-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="13ec6-217">現在，新增 **ISO MPEG-4 多工器**和**檔案輸出**元件並連接接點，如下所示。</span><span class="sxs-lookup"><span data-stu-id="13ec6-217">Now add the **ISO Mpeg-4 Multiplexer** and **File Output** components and connect the pins as shown.</span></span>

![MP4 多工器和輸出檔案](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="13ec6-219">*MP4 多工器和輸出檔案*</span><span class="sxs-lookup"><span data-stu-id="13ec6-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="13ec6-220">您必須設定輸出檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="13ec6-220">You need to set the name for the output file.</span></span> <span data-ttu-id="13ec6-221">按一下 [檔案輸出]  元件，然後編輯檔案的運算式︰</span><span class="sxs-lookup"><span data-stu-id="13ec6-221">Click the **File Output** component and edit the expression for the file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![檔案輸出名稱](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="13ec6-223">*檔案輸出名稱*</span><span class="sxs-lookup"><span data-stu-id="13ec6-223">*File output name*</span></span>

<span data-ttu-id="13ec6-224">您可以在本機執行工作流程，以檢查它是否正確運作。</span><span class="sxs-lookup"><span data-stu-id="13ec6-224">You can run the workflow locally to check that it is running correctly.</span></span>

<span data-ttu-id="13ec6-225">完成之後，您就可以在 Azure 媒體服務中執行它。</span><span class="sxs-lookup"><span data-stu-id="13ec6-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="13ec6-226">首先，為 Azure 媒體服務中的資產準備兩個檔案︰視訊檔案和標誌。</span><span class="sxs-lookup"><span data-stu-id="13ec6-226">First, prepare an asset in Azure Media Services with two files in it: the video file and the logo.</span></span> <span data-ttu-id="13ec6-227">您可以使用 .NET 或 REST API 進行。</span><span class="sxs-lookup"><span data-stu-id="13ec6-227">You can do this by using the .NET or REST API.</span></span> <span data-ttu-id="13ec6-228">您也可以使用 Azure 入口網站或 [Azure 媒體服務總管](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE) 來進行。</span><span class="sxs-lookup"><span data-stu-id="13ec6-228">You can also do this by using the Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="13ec6-229">本教學課程示範如何使用 AMSE 管理資產。</span><span class="sxs-lookup"><span data-stu-id="13ec6-229">This tutorial shows you how to manage assets with AMSE.</span></span> <span data-ttu-id="13ec6-230">有兩種方式可將檔案新增至資產：</span><span class="sxs-lookup"><span data-stu-id="13ec6-230">There are two ways to add files to an asset:</span></span>

* <span data-ttu-id="13ec6-231">建立本機資料夾、在其中複製這兩個檔案，然後將資料夾拖放至 [資產]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="13ec6-231">Create a local folder, copy the two files in it, and drag and drop the folder to the **Asset** tab.</span></span>
* <span data-ttu-id="13ec6-232">上傳視訊檔案做為資產、顯示資產資訊、移至檔案索引標籤，並上傳其他檔案 (標誌)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-232">Upload the video file as an asset, display the asset information, go to the files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="13ec6-233">請務必在資產中設定主要檔案 (主要的視訊檔案)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-233">Make sure to set a primary file in the asset (the main video file).</span></span>

![AMSE 中的資產檔案](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="13ec6-235">*AMSE 中的資產檔案*</span><span class="sxs-lookup"><span data-stu-id="13ec6-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="13ec6-236">選取資產，並選擇使用進階編碼器將其編碼。</span><span class="sxs-lookup"><span data-stu-id="13ec6-236">Select the asset and choose to encode it with Premium Encoder.</span></span> <span data-ttu-id="13ec6-237">上傳工作流程，並加以選取。</span><span class="sxs-lookup"><span data-stu-id="13ec6-237">Upload the workflow and select it.</span></span>

<span data-ttu-id="13ec6-238">按一下按鈕以將資料傳遞給處理器，然後新增下列 XML 來設定執行階段屬性︰</span><span class="sxs-lookup"><span data-stu-id="13ec6-238">Click the button to pass data to the processor, and add the following XML to set the runtime properties:</span></span>

![AMSE 中的進階編碼器](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="13ec6-240">*AMSE 中的進階編碼器*</span><span class="sxs-lookup"><span data-stu-id="13ec6-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="13ec6-241">然後，貼上下列 XML 資料。</span><span class="sxs-lookup"><span data-stu-id="13ec6-241">Then, paste the following XML data.</span></span> <span data-ttu-id="13ec6-242">您必須指定媒體檔案輸入和 primarySourceFile 的視訊檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="13ec6-242">You need to specify the name of the video file for both the Media File Input and primarySourceFile.</span></span> <span data-ttu-id="13ec6-243">也請指定標誌的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="13ec6-243">Specify the name of the file name for the logo too.</span></span>

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

<span data-ttu-id="13ec6-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="13ec6-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="13ec6-246">如果您使用 .NET SDK 來建立和執行工作，必須將此 XML 資料傳遞為組態字串。</span><span class="sxs-lookup"><span data-stu-id="13ec6-246">If you use the .NET SDK to create and run the task, this XML data has to be passed as the configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="13ec6-247">作業完成之後，輸出資產中的 MP4 檔案就會顯示覆疊！</span><span class="sxs-lookup"><span data-stu-id="13ec6-247">After the job is complete, the MP4 file in the output asset displays the overlay!</span></span>

![視訊上的覆疊](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="13ec6-249">*視訊上的覆疊*</span><span class="sxs-lookup"><span data-stu-id="13ec6-249">*Overlay on the video*</span></span>

<span data-ttu-id="13ec6-250">您可以從 [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/)下載範例工作流程。</span><span class="sxs-lookup"><span data-stu-id="13ec6-250">You can download the sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="13ec6-251">範例 2：多重音訊語言編碼</span><span class="sxs-lookup"><span data-stu-id="13ec6-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="13ec6-252">您可以在 [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding) 上取得多重音訊語言編碼工作流程的範例。</span><span class="sxs-lookup"><span data-stu-id="13ec6-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="13ec6-253">此資料夾包含一個範例工作流程，可用來將 MXF 檔案編碼為具有多重曲目的多重 MP4 檔案資產。</span><span class="sxs-lookup"><span data-stu-id="13ec6-253">This folder contains a sample workflow which can be used to encode a MXF file to a multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="13ec6-254">此工作流程假設 MXF 檔案包含一個曲目；應將其他曲目當成個別音訊檔來傳遞 (WAV 或 MP4...)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-254">This workflow assumes that the MXF file contains one audio track ; the additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="13ec6-255">若要編碼，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="13ec6-255">To encode, please follow these steps:</span></span>

* <span data-ttu-id="13ec6-256">建立具有 MXF 檔案與音訊檔 (0 到 18 個音訊檔) 的媒體服務資產。</span><span class="sxs-lookup"><span data-stu-id="13ec6-256">Create a Media Services asset with the MXF file and the Audio files (0 to 18 audio files).</span></span>
* <span data-ttu-id="13ec6-257">確定已將 MXF 檔案設為主要檔案。</span><span class="sxs-lookup"><span data-stu-id="13ec6-257">Make sure that the MXF file is set as a primary file.</span></span>
* <span data-ttu-id="13ec6-258">使用「高階工作流程編碼器」處理器來建立一個作業和一個工作。</span><span class="sxs-lookup"><span data-stu-id="13ec6-258">Create a job and a task using the Premium Workflow Encoder processor.</span></span> <span data-ttu-id="13ec6-259">使用提供的工作流程 (MultiMP4-1080p-19audio-v1.workflow)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-259">Use the workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="13ec6-260">將 setruntime.xml 資料傳遞至工作 (如果您使用 Azure 媒體服務總管，請使用 [將 xml 資料傳遞至工作流程] 按鈕)。</span><span class="sxs-lookup"><span data-stu-id="13ec6-260">Pass the setruntime.xml data to the task (if you use Azure Media Services Explorer, use the “pass xml data to the workflow” button).</span></span>
  * <span data-ttu-id="13ec6-261">請更新 XML 資料，以指定正確的檔案名稱和語言標記。</span><span class="sxs-lookup"><span data-stu-id="13ec6-261">Please update the XML data to specify the correct file names and languages tags.</span></span>
  * <span data-ttu-id="13ec6-262">工作流程具有名為「音訊 1」到「音訊 18」的音訊元件。</span><span class="sxs-lookup"><span data-stu-id="13ec6-262">The workflow has audio components named Audio 1 to Audio 18.</span></span>
  * <span data-ttu-id="13ec6-263">語言標記支援 RFC5646。</span><span class="sxs-lookup"><span data-stu-id="13ec6-263">RFC5646 is supported for the language tag.</span></span>

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

* <span data-ttu-id="13ec6-264">編碼的資產將會包含多種語言的曲目，而這些曲目應該可在 Azure 媒體播放器中加以選取。</span><span class="sxs-lookup"><span data-stu-id="13ec6-264">The encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="13ec6-265">另請參閱</span><span class="sxs-lookup"><span data-stu-id="13ec6-265">See also</span></span>
* [<span data-ttu-id="13ec6-266">介紹 Azure 媒體服務中的 Premium 編碼</span><span class="sxs-lookup"><span data-stu-id="13ec6-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="13ec6-267">How to use Premium Encoding in Azure Media Services (如何使用 Azure 媒體服務中的 Premium 編碼)</span><span class="sxs-lookup"><span data-stu-id="13ec6-267">How to use Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="13ec6-268">使用 Azure 媒體服務編碼隨選內容</span><span class="sxs-lookup"><span data-stu-id="13ec6-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="13ec6-269">媒體編碼器高階工作流程格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="13ec6-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="13ec6-270">範例工作流程檔案</span><span class="sxs-lookup"><span data-stu-id="13ec6-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="13ec6-271">Azure 媒體服務總管工具</span><span class="sxs-lookup"><span data-stu-id="13ec6-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="13ec6-272">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="13ec6-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="13ec6-273">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="13ec6-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

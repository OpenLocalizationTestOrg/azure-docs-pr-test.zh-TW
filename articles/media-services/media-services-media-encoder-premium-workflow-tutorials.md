---
title: "aaaAvanced 媒體編碼器高階工作流程的教學課程"
description: "本文件包含說明如何 tooperform 進階使用媒體編碼器高階工作流程工作的逐步解說也以及 toocreate 複雜工作流程與工作流程設計工具。"
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a>進階媒體編碼器 Premium 工作流程教學課程
## <a name="overview"></a>概觀
本文件說明的逐步解說如何 toocustomize 的工作流程**工作流程設計工具**。 您可以尋找 hello 實際工作流程檔案[這裡](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples)。  

## <a name="toc"></a>目錄
涵蓋下列主題中的 hello:

* [將 MXF 編碼為單一位元速率 MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [開始新的工作流程](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [使用媒體檔案輸入 hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [檢查媒體串流](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [為產生的 MP4 檔案加入視訊編碼器](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [編碼的 hello 音訊資料流](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [將音訊和視訊串流多工處理為 MP4 容器](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [寫入 hello MP4 檔案](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [從 hello 輸出檔案建立 Media Services 資產](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [測試 hello 完成在本機工作流程](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [將 MXF 編碼為多位元速率 MP4 - 動態封裝已啟用](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [加入一或多個其他的 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [設定 hello 檔案輸出名稱](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [加入個別的曲目](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [加入 hello。ISM SMIL 檔案](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [將 MXF 編碼為多位元速率 MP4 - 增強的藍圖](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [工作流程概觀 tooenhance](#workflow-overview-to-enhance)
  * [檔案命名慣例](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [發行到 hello 工作流程的根元件內容](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [讓產生的輸出檔案名稱依賴發佈的屬性值](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [加入縮圖 toomultibitrate MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [工作流程概觀 tooadd 的縮圖](#workflow-overview-to-add-thumbnails-to)
  * [加入 JPG 編碼](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [處理色彩空間轉換](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [寫入 hello 縮圖](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [偵測工作流程中的錯誤](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [工作流程完成](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [多位元速率 MP4 輸出以時間為基礎的修剪](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [加入要修剪的工作流程概觀 toostart](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [使用資料流修剪器 hello](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [工作流程完成](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [簡介 hello 編寫指令碼元件](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [工作流程內的指令碼：Hello World](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [多位元速率 MP4 輸出以畫面格為基礎的修剪](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [加入要修剪的概觀 toostart 藍圖](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [使用 hello 剪輯清單 XML](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [修改編寫指令碼元件中的 hello 剪輯清單](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [加入 ClippingEnabled 便利屬性](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <a id="MXF_to_MP4"></a>將 MXF 編碼為單一位元速率 MP4
在本逐步解說中，我們將使用來自 .MXF 輸入檔案 AAC-HE 編碼的音訊來建立單一位元速率 .MP4 檔案。

### <a id="MXF_to_MP4_start_new"></a>開始新的工作流程
開啟「工作流程設計工具」，然後選取 [檔案] - [新增工作區] - [轉碼藍圖]

hello 新的工作流程將會顯示 3 個元素：

* 主要來源檔案
* 剪輯清單 XML
* 輸出檔案/資產  

![新編碼工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

*新編碼工作流程*

### <a id="MXF_to_MP4_with_file_input"></a>使用媒體檔案輸入 hello
順序 tooaccept 在我們的輸入的媒體檔案，啟動新增媒體檔案輸入的元件。 tooadd 元件 toohello 的工作流程，hello 儲存機制搜尋 方塊中尋找它，並將 hello 預期項目拖曳至 hello 設計工具窗格。 Hello 輸入媒體檔案進行此作業並 hello 輸入媒體檔案從連接 hello 主要原始程式檔元件 toohello Filename 輸入的 pin。

![連接的媒體檔案輸入](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

*連接的媒體檔案輸入*

我們可以執行許多其他之前，我們必須先 tooindicate toohello 工作流程設計工具範例的檔案，我們都希望 toouse toodesign 我們的工作流程。 因此 toodo 按一下 hello 設計工具窗格的背景，然後尋找在 hello 右側的屬性窗格中的 hello 主要原始程式檔屬性。 按一下 hello 資料夾圖示，然後選取所需的 hello 檔案 tootest hello 的工作流程。 進行此設定，如 hello 媒體檔案輸入元件會檢查 hello 檔案，並填入它檢查其輸出 pin tooreflect hello 檔案。

![填入媒體檔案輸入](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

*填入媒體檔案輸入*

這會指定使用哪些輸入，我們都希望 toowork 與，而不知道尚未 hello 編碼的輸出應該移至。 已設定為主要原始程式檔，類似 toohow hello 現在設定 hello 正下方的輸出資料夾變數屬性。

![設定輸入和輸出屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

*設定輸入和輸出屬性*

### <a id="MXF_to_MP4_streams"></a>檢查媒體串流
通常它是所需的 hello 資料流的外觀類似的 tooknow 流經 hello 工作流程。 輸出或輸入的 pin，任何 hello 元件上，只要按一下 tooinspect hello 工作流程，在任何時間點的資料流。 在此情況下，請按一下從我們的媒體檔案輸入 hello 未壓縮視訊輸出的 pin。 對話方塊會開啟，可讓 tooinspect hello 輸出視訊。

![檢查 hello 未壓縮視訊輸出連接](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

*檢查 hello 未壓縮視訊輸出連接*

在我們的案例中，它會告訴我們，比方說我們要對一段接近 2 分鐘的視訊，以 4:2:2 取樣每秒 24 個畫面格處理 1920x1080 輸入。

### <a id="MXF_to_MP4_file_generation"></a>為產生的 MP4 檔案加入視訊編碼器
請注意，現在，[未壓縮的視訊] 和多個 [未壓縮的音訊] 輸出接點可供用於我們的媒體檔案輸入。 在訂單 tooencode hello 輸入的視訊，我們需要的編碼元件-在此情況下產生。MP4 檔案。

tooencode hello tooH.264 視訊資料流，並將 hello AVC 視訊編碼程式元件 toohello 設計工具介面。 此元件會將未壓縮的視訊串流做為輸入，並在其輸出接點上提供 AVC 壓縮視訊串流。

![未連接的 AVC 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

*未連接的 AVC 編碼器*

其屬性會決定如何 hello 編碼完全執行。 讓我們先看一些 hello 更重要的設定：

* 輸出寬度和高度輸出： 這些屬性會決定 hello 的 hello 編碼視訊的解析度。 在本例中，我們使用 640x360
* 畫面播放速率： 只要組 toopassthrough 採用 hello 來源畫面播放速率，時，可能 toooverride 這雖然。 請注意，這類的畫面格速率轉換並非動作補償。
* 設定檔和層級： 這些決定 hello AVC 設定檔與層級。 tooconveniently 取得詳細資訊需 hello 不同層級和設定檔，按一下 hello AVC 視訊編碼器元件上的 hello 問號圖示，然後 hello 說明頁面會顯示有關每 hello 層的其他詳細資料。 我們的範例，我們來使用層級 3.2 （hello 預設值） 的主要設定檔。
* 速率控制模式和位元速率 (kbps)：我們的案例中，我們選擇使用 1200 kbps 常數位元速率 (CBR) 輸出
* 視訊格式: 這是有關 hello VUI （視訊可用性資訊），取得寫入 hello H.264 資料流 （可能由解碼器 tooenhance hello 顯示但 toocorrectly 不必要的側邊資訊解碼）：
* NTSC (一般用於美國或日本，使用 30 fps)
* PAL (一般用於歐洲地區，使用 25 fps)
* GOP 大小模式：針對我們的目的，我們將設定固定的 GOP 大小，主要間隔為 2 秒，並且關閉 GOP。 這可確保與 hello 動態封裝 Azure Media Services 提供的相容性。

toofeed AVC encoder 中，從 hello 媒體檔案輸入元件 toohello 未壓縮視訊輸入 pin hello AVC 編碼器連接 hello 未壓縮視訊輸出連接。

![連接的 AVC 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

*連接的 AVC 主要編碼器*

### <a id="MXF_to_MP4_audio"></a>編碼的 hello 音訊資料流
此時，我們已編碼視訊，但 hello 原始未壓縮音訊資料流仍然需要 toobe 壓縮。 此我們會討論使用 aac 以編碼 hello AAC 編碼器 (Dolby) 元件。 將它加入 toohello 工作流程。

![未連接的 AVC 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

*未連接的 AAC 編碼器*

現在有不相容的問題： 沒有只有單一未壓縮音訊輸入的 pin hello AAC 編碼器從多個可能的 hello 輸入媒體檔案會有兩個不同未壓縮的音訊資料流可用時： 一個用於保留音訊頻道，另一個用於 hello hello權限。 (如果您正在處理環繞音效，則是 6 聲道。)如此就不可能 toodirectly hello 音訊 hello 媒體檔案輸入來源連接到 hello AAC 音訊編碼器。 hello AAC 元件必須要有所謂的 「 交錯"音訊資料流： 同時具有單一資料流 hello 與彼此交錯的左邊和 hello 右邊的通道。 我們已了解我們的來源媒體檔案從音訊音軌 hello 來源中的哪個位置，在我們可以正確地產生這類交錯的音訊資料流以 hello 指派 left 和 right 喇叭的位置。

第一次一個也會想 toogenerated 從所需的 hello 來源音訊頻道的交錯式資料流。 hello 音訊資料流 Interleaver 元件會處理這項工作給我們。 將它加入 toohello 工作流程並 hello 音訊輸出從連線到其中的媒體檔案輸入 hello。

![連接音訊串流交錯器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

*連接音訊串流交錯器*

現在，我們已經交錯的音訊資料流時，我們仍未指定 tooassign hello 左或向右喇叭来放置的位置。 在此順序 toospecify，我們可以利用 hello 喇叭位置 Assigner。

![加入喇叭位置指定器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

*加入喇叭位置指定器*

設定用於 hello 喇叭位置 Assigner 立體聲的輸入資料流編碼器預設篩選條件的 「 自訂 」 並 hello 通道預先設定稱為 「 2.0 （L、 R）"。 （這會指派 hello 左的喇叭位置 toochannel 1 和 hello 右喇叭位置 toochannel 2）。

Hello hello 喇叭位置 Assigner toohello 輸入 hello AAC 編碼器的輸出連接。 然後，告訴 hello AAC 編碼器 toowork"2.0 （L、 R）"預設通道，讓它知道 toodeal 與立體聲音訊做為輸入。

### <a id="MXF_to_MP4_audio_and_fideo"></a>將音訊和視訊串流多工處理為 MP4 容器
假設我們有 AVC 編碼的視訊串流和 AAC 編碼的音訊串流，我們可以將兩者擷取為 .MP4 容器。 hello 的成單一混用不同的資料流的程序稱為 「 多工 」 （或 「 muxing"）。 在此情況下，我們正在交錯 hello 音訊與視訊 hello 一致的單一資料流。MP4 封裝。 此作業對於協調的 hello 元件。MP4 容器稱為 hello ISO mpeg-4 多工器。 加入一個 toohello 設計工具介面，並連接 hello AVC 視訊編碼器和 hello AAC 編碼器 tooits 輸入。

![連接的 MPEG4 多工器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

*連接的 MPEG4 多工器*

### <a id="MXF_to_MP4_writing_mp4"></a>寫入 hello MP4 檔案
寫入輸出檔時，使用 hello 檔案輸出的元件。 使其輸出寫入 toodisk，我們就可以連接 ISO mpeg-4 多工器 hello toohello 的輸出。 toodo，連接到 hello 容器 (MPEG-4) 輸出 pin toohello 寫入輸入的 pin 的 hello 輸出檔。

![連接的檔案輸出](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

*連接的檔案輸出*

將使用的 hello filename 取決於 hello 檔案屬性。 雖然該屬性可能是硬式編碼 tooa 給定值，一個最有可能會想 tooset 它透過運算式改為。

toohave hello 工作流程自動判斷 hello 輸出檔案名稱屬性的運算式，請按一下 hello 按鈕下一個 toohello 檔案名稱 （下一步 toohello 資料夾圖示）。 從 hello 下拉式功能表，然後選取 「 運算式 」。 這會顯示 hello 運算式編輯器。 第一次清除 hello 編輯器 hello 內容。

![空白的運算式編輯器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

*空白的運算式編輯器*

hello 運算式編輯器可讓 tooenter 與一個或多個變數混合任何常值。 以貨幣符號開頭的變數。 當您叫用 hello $ 索引鍵，hello 編輯器會顯示下拉式清單方塊選擇可用的變數。 在我們的案例中，我們將使用 hello 輸出目錄變數和 hello 基底的輸入的檔案名稱的變數的組合：

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![填入運算式編輯器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

*填入運算式編輯器*

> [!NOTE]
> 順序 toosee 看到您在 Azure 中的編碼工作的輸出檔，您必須提供 hello 運算式編輯器中的值。
>
>

當您按下 [確定] 確認 hello 運算式時，hello 屬性視窗就會在此時間點預覽 toowhat 值 hello 檔案屬性解析。

![檔案運算式解析輸出目錄](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

*檔案運算式解析輸出目錄*

### <a id="MXF_to_MP4_asset_from_output"></a>從 hello 輸出檔案建立 Media Services 資產
雖然我們已經寫 MP4 輸出檔案，我們仍需要 tooindicate 這個檔案所屬 toohello 輸出的資產的媒體服務會產生的結果執行此工作流程。 會使用 toothis 結束時，將輸出檔案資產節點 hello hello 工作流程畫布上。 所有連入的檔案到此節點就會產生部分 hello 產生 Azure Media Services 資產。

連接 hello 檔案輸出元件 toohello 輸出檔案資產元件 toofinish hello 工作流程。

![工作流程完成](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

*工作流程完成*

### <a id="MXF_to_MP4_test"></a>測試 hello 完成在本機工作流程
在本機，tootest hello 工作流程叫用 hello hello 頂端的工具列中的 [hello] 按鈕。 Hello 工作流程執行完成時，檢查 hello hello 設定輸出資料夾中產生的輸出。 您會看見 hello 完成從 hello MXF 輸入原始程式檔已編碼的 MP4 輸出檔。

## <a id="MXF_to_MP4_with_dyn_packaging"></a>將 MXF 編碼為 MP4 - 多位元速率動態封裝已啟用
在本逐步解說中，我們將使用來單一 .MXF 輸入檔案 AAC 編碼的音訊來建立一組多位元速率 MP4 檔案。

當多位元速率資產輸出是所需的組合用於與 Azure Media Services 的每個不同的位元速率與解析度需要 toobe 產生多個 gop 之 MP4 檔案所提供的 hello 動態封裝功能。 因此，hello toodo[編碼成單一位元速率 MP4 的 MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)逐步解說提供很好的起點。

![開始工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

*開始工作流程*

### <a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>加入一或多個其他的 MP4 輸出
我們產生的 Azure 媒體服務資產中的每個 MP4 檔案，將支援不同的位元速率與解析度。 讓我們加入一個或多個 MP4 輸出檔案 toohello 工作流程。

我們有 toomake 確定所有我們視訊編碼器以建立 hello 相同的設定，它的最方便 tooduplicate hello 現有 AVC 視訊編碼程式，並設定另一個組合的解析度及位元速率 （讓我們加入一個 960 x 540 在第二個位於每 25 的畫面格2,5 Mbps)。 tooduplicate hello 現有的編碼器，複製貼上它 hello 設計工具介面上。

連接到我們新的 AVC 元件的媒體檔案輸入 hello 的 hello 未壓縮視訊輸出連接。

![連接第二個 AVC 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

*連接第二個 AVC 編碼器*

現在採用我們新 AVC 編碼器 toooutput 960 x 540 以 2,5 Mbps 的 hello 組態。 (對此使用其屬性 [輸出寬度]、[輸出高度] 和 [位元速率 (kbps)]。)

指定我們想要搭配 Azure Media Services 的動態封裝 toouse hello 產生資產，hello 串流端點必須能夠從這些 MP4 檔案 HLS/分散 MP4/DASH 片段完全對齊的 tooeach 其他的方式產生 toobe要切換不同的位元之間的用戶端會收到單一 smooth 連續視訊和音訊體驗。 發生，我們需要在這兩個 AVC 編碼器的 hello 屬性 hello GOP （「 群組的圖片 」） 的這兩個 MP4 檔案大小設定 tooensure toomake too2 秒，都可以做到：

* 設定 hello GOP 調整大小模式 tooFixed GOP 大小和
* hello 金鑰畫面格間隔 tootwo 秒數。
* 也沒有自己的相依性設定 hello GOP IDR 控制項 tooClosed GOP tooensure 長久以來的所有的 GOP

toomake 我們的工作流程方便 toounderstand，重新命名 hello 第一個 AVC 編碼器太"AVC 視訊編碼器 640x360 1200 kbps"hello 第二個 AVC 編碼器和"AVC 視訊編碼器 960 x 540 2500 kbps"。

現在加入第二個「ISO MPEG-4 多工器」和第二個 [檔案輸出]。 連接 hello 多工器 toohello 新 AVC 的編碼器，並確定其輸出導向至 hello 輸出檔。 也連接 hello AAC 音訊編碼器輸出 toohello 新多工器的輸入。 hello 檔案輸出又接著可以連接的 toohello 輸出檔案資產節點 tooadd 它 toohello 將建立的 Media Services 資產。

![連接第二個 Muxer 和檔案輸出](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

*連接第二個 Muxer 和檔案輸出*

使用 Azure Media Services 動態封裝的相容性，設定 hello 多工器的區塊模式 tooGOP 計數或持續時間，設定每個區塊 too1 hello Gop。 （這應該是 hello 預設值）。

![Muxer 區塊模式](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

*Muxer 區塊模式*

注意： 您可能想 toorepeat 此程序的位元速率與解析度組合想 toohave 加入 toohello 資產輸出。

### <a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>設定 hello 檔案輸出名稱
我們有一個以上的單一檔案加入的 toohello 輸出資產。 這會提供檔名的 hello 每個輸出檔案與彼此不同，並讓它成為 hello 檔案名稱中的 清除您要處理的可能即使套用的檔案命名慣例需要的 toomake 確定 hello。

檔案輸出命名可以控制透過 hello 設計工具中的運算式。 開啟其中一個 hello 檔案輸出元件 hello 屬性 窗格，然後開啟 hello hello 檔案屬性的運算式編輯器。 我們第一個輸出檔案是否已透過下列運算式 hello (請參閱 hello 教學課程，可從移[MXF tooa 單一位元速率 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

這表示我們的檔案名稱由兩個變數： hello 輸出目錄 toowrite 在和 hello 原始程式檔的基底名稱。 hello 前者會公開為 hello 工作流程根目錄上的屬性和 hello 後者由 hello 連入的檔案。 請注意該 hello 輸出目錄是您用於本機測試;這個屬性將會覆寫 hello 工作流程引擎 hello 工作流程由 Azure Media Services 中的 hello 以雲端為基礎的媒體處理器執行時。
toogive 這兩個輸出檔案一致輸出命名，變更 hello 第一次檔案命名運算式：

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

並以第二個 hello:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

執行中繼的測試回合 toomake 確定這兩個 MP4 輸出會正確產生檔案。

### <a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>加入個別的曲目
當我們與我們的 MP4 輸出檔案產生的.ism 檔案 toogo，我們將稍後看到，我們也需要純音訊 MP4 檔案 hello 音訊播放軌為我們的彈性資料流。 toocreate 這個檔案，加入其他 muxer toohello 流程 （ISO-mpeg-4 多工器），連接 hello AAC 編碼器的輸出連接其輸入的 pin 與追蹤 1。

![加入音訊 Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

*加入音訊 Muxer*

Hello muxer 從建立第三個檔案輸出元件 toooutput hello 輸出資料流，並設定 hello 做為檔案命名運算式：

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![音訊 Muxer 建立輸出檔案](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

*音訊 Muxer 建立輸出檔案*

### <a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>加入 hello。ISM SMIL 檔案
若是 hello 動態封裝 toowork 結合這兩個 MP4 檔案 （和 hello 純音訊 MP4） 在 Media Services 資產，我們也需要資訊清單檔案 (也稱為 「 SMIL"檔： 同步處理多媒體 Integration 語言)。 這個檔案會指出 tooAzure Media Services 哪些 MP4 檔案可供動態封裝和其中一個這些 tooconsider hello 音訊串流。 具有單一的音訊串流之一組 MP4 的一般資訊清單檔看起來像這樣：

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

hello.ism 檔案包含在 switch 陳述式，hello 個別 MP4 視訊檔案的參考 tooeach 和另外 toothose 另一個 （或以上） 音訊檔案參考 tooan 只包含 hello 音訊 MP4。

產生 hello 我們組 MP4 的資訊清單檔案可以透過稱為 hello"AMS 資訊清單的寫入器 」 元件。 toouse，拖曳至 hello 介面並從三個檔案輸出元件 toohello hello AMS 資訊清單寫入器輸入連接 hello 「 寫入完成 」 的輸出連接。 請確定 tooconnect hello 輸出 hello AMS 資訊清單的寫入器 toohello 輸出檔案資產。

如同我們檔案輸出元件，設定 hello.ism 檔案輸出名稱的運算式：

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

我們已完成的工作流程看起來像下列的 hello:

![完成的 MXF toomultibitrate MP4 工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

*完成的 MXF toomultibitrate MP4 工作流程*

## <a id="MXF_to__multibitrate_MP4"></a>將 MXF 編碼為多位元速率 MP4 - 增強的藍圖
在 hello[前一個工作流程的逐步解說](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)我們已看到如何單一 MXF 輸入的資產可以轉換成輸出資產多位元速率 MP4 檔案、 僅限音訊 MP4 檔案與 Azure 媒體搭配使用的資訊清單檔案服務動態封裝。

這個逐步解說將示範如何某些 hello 方面可以來增強和進行更方便。

### <a id="MXF_to_multibitrate_MP4_overview"></a>工作流程概觀 tooenhance
![多位元速率 MP4 工作流程 tooenhance](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

*多位元速率 MP4 工作流程 tooenhance*

### <a id="MXF_to__multibitrate_MP4_file_naming"></a>檔案命名慣例
我們已 hello 前一個工作流程中指定的簡單運算式做為產生輸出檔名的 hello 基礎。 雖然我們有一些重複： hello hello 個別輸出檔案元件的所有指定的這類運算式。

例如，我們 hello 的第一個視訊檔的檔案輸出元件必須設定此運算式：

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

針對 hello 第二個輸出視訊，我們有如下的運算式：

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

如果我們可以移除某些重複項目，並改為使得項目更可以設定，是不是比較清楚、較不容易出錯、更方便？ 幸好我們可以： hello 設計工具的運算式功能結合在我們的工作流程根目錄上的 hello 能力 toocreate 自訂屬性會提供多一層的便利性。

例如，假設我們將從 hello 種位元 hello 個別 MP4 檔案的磁碟機組態檔名。 我們將會是用在一個中央 tooconfigure 這些位元置於 （hello 根我們圖形的），從他們必須在存取的 tooconfigure 和磁碟機的檔案名稱產生。 toodo，我們一開始所發行的工作流程中，這兩個 AVC 編碼器 toohello 根 hello 位元速率屬性，使其成為可從兩個 hello 根以及從 hello AVC 編碼器存取。 (即使顯示在兩個不同的位置，只有單一的基礎值。)

### <a id="MXF_to__multibitrate_MP4_publishing"></a>發行到 hello 工作流程的根元件內容
開啟第一個 AVC 編碼器 hello，請 toohello 位元速率 (kbps) 屬性，從 hello 下拉式清單中選擇 發行。

![發行 hello 位元速率屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

*發行 hello 位元速率屬性*

設定 hello 發行對話方塊 toopublish toohello 根目錄中，我們的工作流程歷程圖中，以"video1bitrate 「 發佈的名稱 」 和 「 可讀取的顯示名稱 「 視訊 1 位元速率 」。 設定名為「串流處理位元速率」的自訂群組名稱，並按 [發佈]。

![發行 hello 位元速率屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

*位元速率屬性的發佈對話方塊*

重複的 hello、 相同的 hello hello 位元速率屬性 AVC 編碼器的第二個並將其命名"video2bitrate 」 顯示名稱 「 視訊 2 位元速率"hello 進行相同的自訂群組 」 串流處理位元"。

現在，我們會檢查 hello 工作流程的根內容，我們將會看到兩個已發行的屬性顯示的 hello 我們自訂群組。 同時會反映其各自 AVC 編碼器位元速率 hello 值。

![工作流程根目錄上發佈的位元速率屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

每當我們想要 tooaccess 從程式碼或運算式，這些屬性，我們可以這樣做就像這樣：

* 從內嵌程式碼，從正下方 hello 根元件： node.getPropertyAsString('../ video1bitrate'，便是 null)
* 在運算式內：${ROOT_video1bitrate}

讓我們藉由發行我們音訊播放軌位元速率上的也完成 hello 」 串流處理位元 」 群組。 在 hello 屬性中的 hello AAC 編碼器，搜尋 hello 位元速率設定並選取發行從 hello 下拉式清單中下一個 tooit。 發行具有名稱"audio1bitrate"hello 圖形的 toohello 根和顯示名稱"音訊 1 位元速率 「 我們的自訂群組 」 串流處理位元 」 內。

![音訊位元速率的發佈對話方塊](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

*音訊位元速率的發佈對話方塊*

![在根目錄產生視訊和音訊屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

*在根目錄產生視訊和音訊屬性*

請注意，變更任何這些三個值也會重新設定，變更 hello hello 個別的元件，它們會與連結上的值 （以及從發行）。

### <a id="MXF_to__multibitrate_MP4_output_files"></a>讓產生的輸出檔案名稱依賴發佈的屬性值
而不是硬式編碼我們產生的檔案名稱，我們現在可以變更每個 hello 檔案輸出元件 toorely hello 位元速率屬性我們 hello 圖形根上發行我們檔案名稱的運算式。 開始使用我們第一個輸出檔，尋找 hello 檔案屬性，然後編輯 hello 運算式如下：

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

此運算式中的 hello 不同參數可以存取和輸入驉 hello hello 運算式視窗中的 hello 鍵盤上的貨幣符號。 我們稍早已發佈我們 video1bitrate 屬性其中一個 hello 可用的參數。

![存取運算式內的參數](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

*存取運算式內的參數*

請勿 hello 我們的第二個視訊的 hello 檔案輸出相同的：

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

和 hello 純音訊檔案輸出：

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

如果我們現在會變更任何 hello 視訊或音訊檔案的位元速率 hello，hello 個別編碼器將重新設定，而且 hello 位元速率為基礎的檔案名稱慣例將適用於所有自動。

## <a id="thumbnails_to__multibitrate_MP4"></a>加入縮圖 toomultibitrate MP4 輸出
從產生的工作流程開始[輸入 MXF 的多位元速率 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)，我們現在將會尋找到新增縮圖 toohello 輸出。

### <a id="thumbnails_to__multibitrate_MP4_overview"></a>工作流程概觀 tooadd 的縮圖
![從多位元速率 MP4 工作流程 toostart](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

*從多位元速率 MP4 工作流程 toostart*

### <a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>加入 JPG 編碼
我們的縮圖產生 hello 核心會 hello JPG 編碼器元件可以 toooutput JPG 檔案。

![JPG 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

*JPG 編碼器*

我們無法不過從直接連接我們的未壓縮視訊資料流到 hello JPG 編碼器的媒體檔案輸入 hello。 相反地，它會預期 toobe 傳個別畫面格。 這樣，我們可以透過 hello 視訊畫面格閘道元件進行。

![連接框架閘道 toohello JPG 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

*連接框架閘道 toohello JPG 編碼器*

hello 框架閘道之後每個這麼多的秒數或框架可讓視訊畫面格 toopass。 hello 間隔和 hello 時間位移與其中發生這種情況是 hello 屬性中設定的。

![視訊畫面格閘道屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

*視訊畫面格閘道屬性*

讓我們藉由設定 hello 模式 tooTime （秒） 每隔一分鐘建立縮圖和 hello 間隔 too60。

### <a id="thumbnails_to__multibitrate_MP4_color_space"></a>處理色彩空間轉換
雖然相提並論，似乎邏輯這兩種未壓縮視訊的 hello 框架閘道與媒體檔案輸入 hello 的 pin 現在已連線，如果我們會這樣做，我們會收到警告。

![輸入色彩空間錯誤](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

*輸入色彩空間錯誤*

這是因為 hello 的色彩中資訊的表示的方式我們原始原始未壓縮視訊資料流中，來自我們 MXF，哪些 hello JPG 編碼器所預期不同。 更具體來說，所謂"色彩空間 」 的 「 RGB"或"灰階 」 是預期 tooflow 中的。 這表示該 hello 視訊畫面格閘道的輸入視訊串流需要 toohave 先套用有關其色彩空間轉換。

拖曳到 hello 工作流程 hello 色彩空間轉換程式 Intel，並將它連接 tooour 框架閘道。

![連接色彩空間轉換器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

*連接色彩空間轉換器*

在 hello 屬性 視窗中，選擇 hello BGR 24 hello 預設清單項目。

### <a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>寫入 hello 縮圖
不同於我們的 MP4 視訊，hello JPG 編碼器元件會輸出多個檔案。 在與這個順序 toodeal，場景搜尋 JPG 檔案寫入器元件都可以使用： 它會採用 hello 傳入 JPG 縮圖，並將它們，寫入正在不同的數字並後置有每個檔案名稱。 （從已繪製 hello 數字，通常表示的秒數/單位 hello 縮圖 hello 資料流中的 hello 數字）。

![介紹 hello 場景搜尋 JPG 檔案寫入器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

*介紹 hello 場景搜尋 JPG 檔案寫入器*

使用 hello 運算式設定 hello 輸出資料夾的路徑屬性: ${ROOT_outputWriteDirectory}

和 hello 與檔案名稱前置詞屬性：

    ${ROOT_sourceFileBaseName}_thumb_

hello 前置詞會決定要如何命名 hello 縮圖的檔案。 它們會加 hello 資料流中的一個數字表示 hello 捲動方塊的位置。

![場景搜尋 JPG 檔案寫入器屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

*場景搜尋 JPG 檔案寫入器屬性*

Hello 場景搜尋 JPG 檔案寫入器 toohello 輸出檔案資產節點連接。

### <a id="thumbnails_to__multibitrate_MP4_errors"></a>偵測工作流程中的錯誤
連接 hello 色彩空間轉換 toohello 原始未壓縮視訊輸出的 hello 的輸入。 現在，執行本機測試回合 hello 工作流程。 沒有機會 hello 工作流程會突然停止執行，而且發生錯誤的 hello 元件上的紅色外框表示：

![色彩空間轉換器錯誤](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

*色彩空間轉換器錯誤*

按一下 hello hello 編碼嘗試失敗的原因是什麼 hello 右上角的 hello 色彩空間轉換元件 toosee"E"hello 稍有紅色圖示。

![色彩空間轉換器錯誤對話方塊](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

*色彩空間轉換器錯誤對話方塊*

事實上，您可以看到，hello 傳入色彩空間標準 hello 色彩空間轉換具有 toobe rec601 YUV tooRGB 我們要求轉換。 顯然我們的串流並未指出它是 rec601。 (Rec 601 是以數位視訊格式編碼交錯式類比視訊訊號的標準。 它會指定涵蓋 720 亮度取樣和每一行 360 色度取樣的作用中區域。 hello 色彩編碼系統稱為 YCbCr 4:2:2。)

toofix，我們將會指出我們我們處理 rec601 內容的資料流的 hello 中繼資料。 讓我們將使用視訊資料型別 Updater 元件，請說我們原始來源與 hello 色彩空間轉換元件之間 toodo。 此資料型別 updater 允許 hello 手動更新特定視訊資料的類型屬性。 設定 tooindicate 色彩空間標準的 「 Rec 601"。 如果尚未定義任何色彩空間，這會導致 hello 視訊資料型別 Updater tootag hello 資料流與 hello"Rec 601"色彩空間。 （它不會覆寫任何現有的中繼資料，除非 hello 覆寫核取方塊已核取。）

![更新資料型別 Updater hello 色彩空間標準](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

*更新資料型別 Updater hello 色彩空間標準*

### <a id="thumbnails_to__multibitrate_MP4_finish"></a>工作流程完成
既然我們我們的工作流程已結束，請執行通過的測試回合的 toosee 另一個。

![具有縮圖的多個 mp4 輸出完成的工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

*具有縮圖的多個 mp4 輸出完成的工作流程*

## <a id="time_based_trim"></a>多位元速率 MP4 輸出以時間為基礎的修剪
從產生的工作流程開始[輸入 MXF 的多位元速率 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)，我們現在將會尋找到修剪 hello 來源視訊根據時間戳記。

### <a id="time_based_trim_start"></a>加入要修剪的工作流程概觀 toostart
![若要開始的工作流程 tooadd 修剪](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

*若要開始的工作流程 tooadd 修剪*

### <a id="time_based_trim_use_stream_trimmer"></a>使用資料流修剪器 hello
hello 資料流修剪器元件可讓 tootrim hello 開頭和結尾的輸入資料流的基礎計時資訊 （秒數、 分鐘的時間，...）。hello 修剪器不支援以框架為基礎的調整。

![串流修剪器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

*串流修剪器*

而不是直接連結 hello AVC 編碼器和喇叭位置 assigner toohello 媒體檔案輸入，我們會將這些 hello 資料流修剪器之間。 （一個 hello 視訊訊號，一個用於 hello 交錯音訊訊號）。

![在內部放入串流修剪器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

*在內部放入串流修剪器*

讓我們設定 hello 修剪器，讓我們只會處理視訊和音訊 15 秒到 hello 視訊在 60 秒之間。

請 toohello hello 視訊資料流修剪器屬性，並設定開始時間 (15) 和結束時間 （60 秒） 的內容。 確定同時我們音訊和視訊修剪器一定是相同的開始和結束值設定的 toohello toomake，我們將發佈這些 toohello hello 工作流程的根。

![串流修剪器的發佈開始時間屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

*串流修剪器的發佈開始時間屬性*

![發佈屬性對話方塊的開始時間](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

*發佈屬性對話方塊的開始時間*

![發佈屬性對話方塊的結束時間](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

*發佈屬性對話方塊的結束時間*

如果我們現在會檢查 hello 根工作流程，這兩個屬性將會清楚顯示，且可設定從該處。

![在根目錄可取得發佈的屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

*在根目錄可取得發佈的屬性*

現在從 hello 音訊修剪器開啟 hello 修剪屬性，並設定開始和結束時間的運算式可參考 toohello 發行的工作流程的 hello 根目錄上的屬性。

Hello 音訊修剪開始時間：

    ${ROOT_TrimmingStartTime}

和其結束時間：

    ${ROOT_TrimmingEndTime}

### <a id="time_based_trim_finish"></a>工作流程完成
![工作流程完成](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

*工作流程完成*

## <a id="scripting"></a>簡介 hello 編寫指令碼元件
執行指令碼的元件可以 hello 的工作流程的執行階段期間執行任意指令碼。 有四個不同的指令碼可以執行的每個都有特定的特性和自己 hello 工作流程生命週期中的位置：

* **commandScript**
* **realizeScript**
* **processInputScript**
* **lifeCycleScript**

hello 文件的 hello 編寫指令碼元件會更詳細的 hello 上述每個。 在[hello 下列區段](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)，hello **realizeScript** hello 工作流程啟動時，指令碼元件會使用的 tooconstruct hello 立即 cliplist xml。 此指令碼會呼叫 hello 元件在安裝期間，發生一次在其生命週期中。

### <a id="scripting_hello_world"></a>工作流程內的指令碼：Hello World
Hello 設計工具介面上拖曳編寫指令碼元件，並重新命名它 (例如，"SetClipListXML")。

![加入指令碼元件](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*加入指令碼元件*

當您檢查 hello 屬性 hello 編寫指令碼元件，將會顯示四種不同的指令碼類型的 hello、 每個可設定 tooa 不同的指令碼。

![指令碼元件屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*指令碼元件屬性*

清除 hello processInputScript 和 hello realizeScript 的 hello 編輯器開啟。 現在我們設定好，並準備 toostart 指令碼。

指令碼是以 Groovy，會保留與 Java 的相容性的 hello Java 平台動態編譯的指令碼語言撰寫。 事實上，大部分的 Java 程式碼是有效的 Groovy 程式碼。

讓我們我們 realizeScript hello 內容中撰寫簡單的 hello world groovy 指令碼。 Hello 編輯器中輸入 hello 下列：

    node.log("hello world");

現在執行本機測試回合。 之後此回合中，檢查 (透過 hello 系統索引標籤上 hello 編寫指令碼元件) hello 記錄屬性。

![Hello World 記錄輸出](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

*Hello World 記錄輸出*

hello 節點物件我們呼叫 hello 記錄方法，是指 tooour 目前 「 節點 」 或我們正在編寫指令碼中的 hello 元件。 每個元件在這種情況有 hello 能力 toooutput 記錄資料，可透過 hello 系統索引標籤。在此情況下，我們會輸出 hello 字串常值"hello world"。 這裡的重要 toounderstand 是，這可以證明 toobe 非常寶貴的偵錯工具，讓您深入了解哪些 hello 指令碼實際執行的動作。

從在指令碼環境中，我們也對存取 tooproperties 其他元件。 試試看：

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

我們的記錄視窗會顯示下列 hello:

![用於存取節點路徑的記錄輸出](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

*用於存取節點路徑的記錄輸出*

## <a id="frame_based_trim"></a>多位元速率 MP4 輸出以畫面格為基礎的修剪
從產生的工作流程開始[輸入 MXF 的多位元速率 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)，我們現在將會尋找到修剪 hello 來源視訊根據框架計數。

### <a id="frame_based_trim_start"></a>加入要修剪的概觀 toostart 藍圖
![加入要修剪的工作流程 toostart](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

*加入要修剪的工作流程 toostart*

### <a id="frame_based_trim_clip_list"></a>使用 hello 剪輯清單 XML
在所有先前的工作流程教學課程，我們可以使用 hello 媒體檔案輸入元件做為我們視訊的輸入來源。 針對這個特定案例，我們將使用 hello 剪輯清單來源元件改為。 請注意，這不能 hello 慣用的方法來;只使用 hello 剪輯清單來源沒有真正原因 toodo 的因此時 (如同在下列情況下，我們做了其中的 hello hello 剪輯清單調整功能的使用)。

我們的媒體檔案輸入 toohello 剪輯來源清單，從 tooswitch hello 設計介面上拖曳 hello 剪輯清單來源元件，並連接 hello 剪輯清單 pin toohello 剪輯清單 XML 的 XML 節點 hello 工作流程設計工具。 這應填入 hello 來源剪輯清單與輸出連接，根據 tooour 輸入的視訊。 現在從 hello hello 剪輯清單來源 toohello 連線 hello 未壓縮視訊和未壓縮的音訊連接個別 AVC 編碼器和音訊資料流 Interleaver。 現在要移除 hello 媒體檔案輸入。

![Hello 媒體檔案輸入取代 hello 剪輯來源清單](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

*Hello 媒體檔案輸入取代 hello 剪輯來源清單*

hello 剪輯清單來源元件會做為輸入 「 剪輯清單 XML"。 選取時 hello 來源檔案 tootest 與在本機，此剪輯清單 xml 是為您自動填入。

![自動填入剪輯清單 XML 屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

*自動填入剪輯清單 XML 屬性*

尋找位元仔細 toohello xml，這是它的外觀類似：

![編輯剪輯清單對話方塊](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

*編輯剪輯清單對話方塊*

這但是不會反映 hello hello 剪輯清單 xml 功能。 我們的其中一個選項是 tooadd 下 hello 視訊和音訊的來源，就像這樣的 「 修剪 」 項目：

![新增修剪元素 toohello 剪輯清單](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

*新增修剪元素 toohello 剪輯清單*

如果您修改 hello 剪輯清單 xml，像這樣上方，並執行本機測試回合，您會看到 hello 視訊正確已修剪介於 10 到 20 秒 hello 視訊中。

當您執行本機執行，但此相同 cliplist xml 不會有相同效果時套用的 Azure 媒體服務中執行的工作流程中的 hello，就會發生反對 toowhat。 每次同樣地，根據 hello 輸入的檔 hello 編碼產生 Azure Premium 編碼程式啟動時，hello cliplist xml 時指定作業。 這表示，我們會在 hello xml 執行的任何變更將不幸的是會被覆寫。

toocounter hello cliplist xml 抹除的編碼工作啟動時，我們可以重新產生它 hello 立即後方 hello 開始的工作流程。 透過稱為「指令碼元件」的項目即可以採取這種自訂動作。 如需詳細資訊，請參閱[簡介 hello 編寫指令碼元件](media-services-media-encoder-premium-workflow-tutorials.md#scripting)。

Hello 設計工具介面上拖曳編寫指令碼元件，並將它重新命名過"SetClipListXML"。

![加入指令碼元件](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*加入指令碼元件*

當您檢查 hello 屬性 hello 編寫指令碼元件，將會顯示四種不同的指令碼類型的 hello、 每個可設定 tooa 不同的指令碼。

![指令碼元件屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*指令碼元件屬性*

### <a id="frame_based_trim_modify_clip_list"></a>修改編寫指令碼元件中的 hello 剪輯清單
我們可以重新撰寫 hello cliplist 產生 xml，在工作流程啟動之前，我們需要 toohave 存取 toohello cliplist xml 屬性和內容。 我們可以像這樣執行：

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![記錄傳入剪輯清單](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

*記錄傳入剪輯清單*

首先我們需要方式 toodetermine 點到哪一個點為止，我們想 tootrim hello 視訊。 toomake hello 工作流程，這個方便 toohello 小於技術使用者發行 hello 圖形的兩個屬性 toohello 根。 toodo，hello 設計工具介面上按一下滑鼠右鍵，然後選取 「 新增屬性 」:

* 第一個屬性："ClippingTimeStart"，類型："TIMECODE"
* 第二個屬性："ClippingTimeEnd"，類型："TIMECODE"

![加入屬性對話方塊的剪輯開始時間](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

*加入屬性對話方塊的剪輯開始時間*

![工作流程根目錄上發佈的剪輯時間屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

*工作流程根目錄上發佈的剪輯時間屬性*

設定這兩個屬性 tooa 適當的值：

![設定開始和結束的內容和結束時間裁剪 hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

*設定開始和結束的內容和結束時間裁剪 hello*

現在，從我們的指令碼內，我們就可以存取這兩個屬性，像這樣：

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![顯示剪輯的開始與結束的記錄視窗](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

*顯示剪輯的開始與結束的記錄視窗*

讓我們更方便 toouse 表單，使用簡單的規則運算式剖析 hello 播放字串：

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![具有剖析的時間碼輸出的記錄檔視窗](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

*具有剖析的時間碼輸出的記錄檔視窗*

於此資訊，我們現在可以修改 hello cliplist xml tooreflect hello 開始與 hello 的結束時間所需的 hello 影片框架精確裁剪。

![指令碼程式碼 tooadd 修剪項目](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

*指令碼程式碼 tooadd 修剪項目*

這是透過一般的字串處理作業完成。 hello 產生的已修改的剪輯清單 xml 重新寫入 toohello clipListXML 屬性 hello 工作流程根目錄上透過 hello"setProperty 」 方法。 另一個測試回合之後，hello 記錄視窗會顯示我們 hello 遵循：

![記錄產生剪輯清單 hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

*記錄產生剪輯清單 hello*

執行測試回合 toosee hello 視訊和音訊資料流已裁剪的方式。 當您將會執行包含不同的 hello 修剪點值的多個測試回合，您會注意到，這些將不會考量不過 ！ hello 這個錯誤的原因是該 hello 設計工具，不同於 hello Azure 執行階段時，每次執行時不會不覆寫 hello cliplist xml。 這表示，只有 hello 第一次設定 hello 進出點，會導致 hello xml tootransform、 所有 hello 其他時間，我們防護子句 (如果 (clipListXML.indexOf (「<trim>") = =-1)) 會避免 hello 工作流程新增另一個修剪當已經有一個出現項目。

toomake 我們的工作流程方便 tootest 在本機，我們最佳加入如果修剪的項目已經存在，會檢查某些馬上保留程式碼。 如果是這樣，我們可以移除它，然後再繼續修改 hello 與 hello 新值的 xml。 而不是使用純文字字串操作，很可能是更安全的 toodo 透過實際的 xml 物件模型剖析。

我們可以透過新增這類程式碼之前，我們需要的 tooadd 數目在 hello 匯入陳述式先啟動指令碼：

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

在此之後，我們可以加入清除程式碼所需的 hello:

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

這個程式碼會正上方的中，我們加入 hello 修剪元素 toohello cliplist xml hello 點。

此時，我們可以執行和修改工作流程時一樣我們想要在具有 hello 變更曾經套用時的時間。    

### <a id="frame_based_trim_clippingenabled_prop"></a>加入 ClippingEnabled 便利屬性
可能不一定要修剪 toohappen，讓我們先加入方便的布林值旗標，指出完成關閉工作流程是否我們想要 tooenable 修剪 / 結束時間裁剪。

就像之前，發行我們稱為 「 ClippingEnabled 」 的工作流程的新屬性 toohello 根型別"BOOLEAN"。

![發佈啟用剪輯屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

*發佈啟用剪輯屬性*

以下列簡單的防護子句 hello，我們可以檢查是否需要調整，並決定是否我們剪輯清單在這種情況需要 toobe 修改。

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <a id="code"></a>完整程式碼
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a>另請參閱
[介紹 Azure 媒體服務中的 Premium 編碼](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[如何在 Azure Media Services 編碼 Premium tooUse](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[透過 Azure 媒體服務編碼的隨選內容](media-services-encode-asset.md#media-encoder-premium-workflow)

[Media Encoder Premium Workflow 格式和轉碼器](media-services-premium-workflow-encoder-formats.md)

[範例工作流程檔案](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[Azure 媒體服務總管工具](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

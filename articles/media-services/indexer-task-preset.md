---
title: "Azure Media Indexer 為預設的 aaaTask"
description: "本主題提供 Azure 媒體索引器工作預設的概觀。"
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: ca0b3e7aa9f6dd9fdecddfc5b3137281ed5cef35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="task-preset-for-azure-media-indexer"></a>Azure 媒體索引器的工作預設

Azure Media Indexer 為媒體處理器，您會使用下列工作的 tooperform hello： 使媒體檔案和內容可供搜尋，產生已關閉隱藏式輔助字幕追蹤和關鍵字，屬於您資產的資產檔案編製索引。

本主題描述 hello 工作預設您需要 toopass tooyour 編製索引作業。 如需完整範例，請參閱[使用 Azure 媒體索引器為媒體檔案編製索引](media-services-index-content.md)。

## <a name="azure-media-indexer-configuration-xml"></a>Azure 媒體索引器設定 XML

hello 下表說明的 hello 組態 XML 元素及屬性。

|名稱|必要|說明|
|---|---|---|
|輸入|true|您想 tooindex 資產檔案。<br/>Azure Media Indexer 支援下列媒體檔案格式的 hello: MP4、 MOV、 WMV、 MP3、 M4A、 WMA、 AAC、 WAV。 <br/><br/>您可以指定 hello 檔案名稱 (s) 中 hello**名稱**或**清單**屬性 hello**輸入**項目 （如下所示）。 如果您未指定的資產檔案 tooindex，會挑出 hello 主要檔案。 如果設定主要資產檔案，hello hello 輸入資產中的第一個檔案編製索引。<br/><br/>tooexplicitly 指定 hello 資產檔案名稱，執行：<br/>```<input name="TestFile.wmv" />```<br/><br/>您也可以索引次 （向上 too10 檔案） 的多個資產檔案。 toodo 這樣：<br/>- 建立文字檔 (資訊清單檔) 並指定 .lst 副檔名。<br/>您輸入的資產 toothis 資訊清單檔中新增所有 hello 資產檔案名稱的清單。<br/>新增 （上傳） thanifest 檔案 toohello 資產。<br/>-指定 hello 輸入清單屬性中的 hello hello 資訊清單檔案名稱。<br/>```<input list="input.lst">```<br/><br/>**注意：**加入 10 個以上檔案 toohello 資訊清單檔，如果 hello 索引工作將會失敗 hello 2006 錯誤碼。|
|中繼資料|false|Hello 的中繼資料指定資產檔案。<br/>```<metadata key="..." value="..." />```<br/><br/>您可以提供預先定義的索引鍵值。 <br/><br/>目前支援下列索引鍵的 hello:<br/><br/>**標題**和**描述**-使用 tooupdate hello 語言模型 tooimprove 語音辨識準確度。<br/>```<metadata key="title" value="[Title of hello media file]" /><metadata key="description" value="[Description of hello media file]" />```<br/><br/>**使用者名稱**和**密碼** - 透過 http 或 https 下載網際網路檔案時用於驗證。<br/>```<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />```<br/>hello 使用者名稱和密碼的值會套用 tooall 媒體 Url hello 輸入資訊清單中。|
|特性<br/><br/>在 1.2 版中新增。 目前，僅支援 hello 功能是語音辨識 ("ASR")。|false|hello 語音辨識功能具有下列設定索引鍵的 hello:<br/><br/>語言：<br/>-hello 自然語言 toobe 辨識 hello 多媒體檔案中。<br/>- 英文、西班牙文<br/><br/>CaptionFormats：<br/>-hello 的分號分隔清單所需的輸出標題格式 （如果有的話）<br/>- ttml;sami;webvtt<br/><br/><br/>GenerateAIB：<br/>的指定指出 AIB 檔案必要 （適用於 SQL Server 和 hello 客戶索引子 IFilter） 布林值旗標。 如需詳細資訊，請參閱＜以 Azure 媒體索引器和 SQL Server 使用 AIB 檔案＞。<br/>- True 或 False<br/><br/>GenerateKeywords：<br/>- 布林值旗標，用於指定是否需要關鍵字 XML 檔案。<br/>- True 或 False。|

## <a name="azure-media-indexer-configuration-xml-example"></a>Azure 媒體索引器設定 XML 範例

``` 
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of hello media file]" />  
    <metadata key="description" value="[Description of hello media file]" />  
  </input>  
  <settings>  
  </settings>  
  
  <features>  
    <feature name="ASR">    
      <settings>  
        <add key="Language" value="English"/>  
        <add key="CaptionFormats" value="ttml;sami;webvtt"/>  
        <add key="GenerateAIB" value ="true" />  
        <add key="GenerateKeywords" value ="true" />  
      </settings>  
    </feature>  
  </features>  
  
</configuration>  
```
  
## <a name="next-steps"></a>後續步驟

請參閱[使用 Azure 媒體索引器為媒體檔案編製索引](media-services-index-content.md)。


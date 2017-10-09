---
title: "aaaMedia 編碼器標準結構描述 |Microsoft 文件"
description: "hello 主題概略 hello 媒體編碼器標準結構描述。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 4c060062-8ef2-41d9-834e-e81e8eafcf2e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 82bad27b9546f75557ac691ff148b46990647632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-schema"></a>媒體編碼器標準結構描述
本主題所描述的是一些 hello 項目和 hello XML 結構描述的型別所在[標準媒體編碼器預設](media-services-mes-presets-overview.md)為基礎。 hello 主題會說明的項目和其有效的值。 將在日後發佈 hello 完整結構描述。  

## <a name="Preset"></a> 預設值 (根元素)
定義編碼預設值。  

### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **編碼** |[編碼](media-services-mes-schema.md#Encoding) |根項目，表示 toobe 編碼 hello 輸入的來源。 |
| **輸出** |[輸出](media-services-mes-schema.md#Output) |想要的輸出檔案集合。 |

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **版本**<br/><br/> 必要 |**xs:decimal** |hello 預設的版本。 hello 套用下列限制： xs:fractionDigits 值 ="1"和 xs:minInclusive value ="1"，例如**版本 ="1.0"**。 |

## <a name="Encoding"></a> 編碼
包含一連串的 hello 下列項目。  

### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **H264Video** |[H264Video](media-services-mes-schema.md#H264Video) |視訊的 H.264 編碼設定。 |
| **AACAudio** |[AACAudio](media-services-mes-schema.md#AACAudio) |音訊的 AAC 編碼設定。 |
| **BmpImage** |[BmpImage](media-services-mes-schema.md#BmpImage) |Bmp 影像的設定。 |
| **PngImage** |[PngImage](media-services-mes-schema.md#PngImage) |Png 影像的設定。 |
| **JpgImage** |[JpgImage](media-services-mes-schema.md#JpgImage) |Jpg 影像的設定。 |

## <a name="H264Video"></a> H264Video
### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **TwoPass**<br/><br/> minOccurs="0" |**xs:boolean** |目前，只支援 One-pass 編碼。 |
| **KeyFrameInterval**<br/><br/> minOccurs="0"<br/><br/> **default="00:00:02"** |**xs:time** |決定 hello 固定 IDR 畫面格，以秒為單位之間的間距。 也稱為 tooas hello GOP 持續期間。 請參閱**SceneChangeDetection** （下方） 來控制是否 hello 編碼器可以與不符合此值。 |
| **SceneChangeDetection**<br/><br/> minOccurs="0"<br/><br/> 預設值=”false” |**xs:boolean** |如果組 tootrue，編碼器嘗試 toodetect 場景 hello 視訊中變更，並將插入的 IDR 框架。 |
| **Complexity**<br/><br/> minOccurs="0"<br/><br/> 預設值="Balanced" |**xs:string** |控制項 hello 取捨編碼速度和視訊品質。 可能是其中一個值的 hello:**速度**，**平衡**，或**品質**<br/><br/> 預設值：**Balanced** |
| **SyncMode**<br/><br/> minOccurs="0" | |此功能將在未來的版本中公開。 |
| **H264Layers**<br/><br/> minOccurs="0" |[H264Layers](media-services-mes-schema.md#H264Layers) |輸出視訊圖層的集合。 |

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Condition** |**xs:string** | 當 hello 輸入有視訊時，您可能想 tooforce hello 編碼器 tooinsert 單色視訊播放軌。可使用條件 toodo ="InsertBlackIfNoVideoBottomLayerOnly 」 (tooinsert 只 hello 最低位元速率將視訊) 或條件 ="InsertBlackIfNoVideo 」 (tooinsert 所有輸出種位元速率視訊)。 如需詳細資訊，請參閱 [這個](media-services-advanced-encoding-with-mes.md#no_video) 主題。|

## <a name="H264Layers"></a> H264Layers

根據預設，如果傳送只包含音訊和不段影片中，輸入的 toohello 編碼器 hello 輸出資產會包含具有僅限音訊資料檔案。 某些播放程式可能無法再 toohandle 這類輸出資料流。 您可以使用 hello H264Video **InsertBlackIfNoVideo**設定 tooforce hello 編碼器 tooadd 視訊播放軌 toohello 輸出，在這個案例中的屬性。 如需詳細資訊，請參閱 [這個](media-services-advanced-encoding-with-mes.md#no_video) 主題。
              
### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **H264Layer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[H264Layer](media-services-mes-schema.md#H264Layer) |H264 圖層的集合。 |

## <a name="H264Layer"></a> H264Layer
> [!NOTE]
> 視訊的限制根據 hello 中所述的 hello 值[H264 層級](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Levels)資料表。  
> 
> 

### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **設定檔**<br/><br/> minOccurs="0"<br/><br/> 預設值=”Auto” |**xs:string** |可能的 hello 下列其中一種**xs: string**值：**自動**，**基準**， **Main**，**高**。 |
| **Level**<br/><br/> minOccurs="0"<br/><br/> 預設值=”Auto” |**xs:string** | |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |用於此視訊的圖層，指定單位： kbps 的 hello 位元速率。 |
| **MaxBitrate**<br/><br/> minOccurs="0" |**xs:int** |hello 最大位元速率用於此視訊的圖層，以 kbps 為單位指定。 |
| **BufferWindow**<br/><br/> minOccurs="0"<br/><br/> 預設值="00:00:05" |**xs:time** |Hello 視訊緩衝區的長度。 |
| **Width**<br/><br/> minOccurs="0" |**xs:int** |Hello 輸出視訊畫面格，單位為像素寬度。<br/><br/> 請注意，您目前必須指定 Width 和 Height。 hello 寬度和高度必須 toobe 偶數。 |
| **Height**<br/><br/> minOccurs="0" |**xs:int** |Hello 輸出視訊畫面格，單位為像素的高度。<br/><br/> 請注意，您目前必須指定 Width 和 Height。 hello 寬度和高度必須 toobe 偶數。|
| **BFrames**<br/><br/> minOccurs="0" |**xs:int** |參考畫面格之間的 B 畫面格數目。 |
| **ReferenceFrames**<br/><br/> minOccurs="0"<br/><br/> 預設值=”3” |**xs:int** |GOP 中的參考畫面格數目。 |
| **EntropyMode**<br/><br/> minOccurs="0"<br/><br/> 預設值=”Cabac” |**xs:string** |可能是其中一個值的 hello: **Cabac**和**Cavlc**。 |
| **FrameRate**<br/><br/> minOccurs="0" |有理數 |決定 hello 畫面播放速率的視訊 hello 輸出。 使用預設值是"0/1"toolet hello 編碼器使用 hello 相同框架評分為 hello 輸入視訊。 允許的值是預期的 toobe 通用視訊畫面播放速率，如下所示。 不過，允許任何有效的有理數。 例如 1/1 會是 1 fps 並且有效。<br/><br/> - 12/1 (12 fps)<br/><br/> - 15/1 (15 fps)<br/><br/> - 24/1 (24 fps)<br/><br/> - 24000/1001 (23.976 fps)<br/><br/> - 25/1 (25 fps)<br/><br/>  - 30/1 (30 fps)<br/><br/> - 30000/1001 (29.97 fps) <br/> <br/>**請注意**如果您要建立多個位元速率編碼為預設的自訂，然後 hello 的所有圖層預設**必須**使用 hello 相同的畫面播放速率的值。|
| **AdaptiveBFrame**<br/><br/> minOccurs="0" |**xs:boolean** |從 Azure 媒體編碼器複製 |
| **Slices**<br/><br/> minOccurs="0"<br/><br/> 預設值="0" |**xs:int** |決定將畫面格分成幾個片段。 建議使用預設值。 |

## <a name="AACAudio"></a> AACAudio
 包含一連串的 hello 下列項目，並分組。  

 如需有關 AAC 的詳細資訊，請參閱 [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding)。  

### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **設定檔**<br/><br/> minOccurs="0 "<br/><br/> 預設值="AACLC" |**xs:string** |可能是其中一個值的 hello: **AACLC**， **HEAACV1**，或**HEAACV2**。 |

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Condition** |**xs:string** |tooforce hello 編碼器 tooproduce 包含無訊息的音訊播放軌時輸入有沒有音訊的資產指定 hello"InsertSilenceIfNoAudio"值。<br/><br/> 根據預設，如果您傳送僅包含視訊、 且沒有音訊輸入的 toohello 編碼器則 hello 輸出資產將包含檔案，其中包含只視訊資料。 某些播放程式可能無法再 toohandle 這類輸出資料流。 在這個案例中，您可以使用此設定 tooforce hello 編碼器 tooadd 無訊息的音訊播放軌 toohello 輸出。 |

### <a name="groups"></a>群組
| 參考 | 說明 |
| --- | --- |
| [AudioGroup](media-services-mes-schema.md#AudioGroup)<br/><br/> minOccurs="0" |請參閱描述[AudioGroup](media-services-mes-schema.md#AudioGroup) tooknow hello 適當數目的通道、 取樣率，以及可以設定每個設定檔的位元速率。 |

## <a name="AudioGroup"></a> AudioGroup
如需哪些值是適用於每個設定檔的詳細資訊，請參閱 hello [音訊轉碼器詳細資料] 表格所示。  

### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Channels**<br/><br/> minOccurs="0" |**xs:int** |hello 音訊編碼的頻道數目。 hello 以下是有效的選項： 1、 2、 5、 6、 8。<br/><br/> 預設值︰2。 |
| **SamplingRate**<br/><br/> minOccurs="0" |**xs:int** |hello 音訊取樣率、 Hz 中指定。 |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |指定單位： kbps 編碼 hello 音訊時使用的 hello 位元速率。 |

### <a name="audio-codec-details"></a>音訊轉碼器詳細資訊
音訊轉碼器|詳細資料  
-----------------|---  
**AACLC**|1:<br/><br/> - 11025 : 8 &lt;= 位元速率 &lt; 16<br/><br/> - 12000 : 8 &lt;= 位元速率 &lt; 16<br/><br/> - 16000 : 8 &lt;= 位元速率 &lt;32<br/><br/>- 22050 : 24 &lt;= 位元速率 &lt; 32<br/><br/> - 24000 : 24 &lt;= 位元速率 &lt; 32<br/><br/> - 32000 : 32 &lt;= 位元速率 &lt;= 192<br/><br/> - 44100 : 56 &lt;= 位元速率 &lt;= 288<br/><br/> - 48000 : 56 &lt;= 位元速率 &lt;= 288<br/><br/> - 88200 : 128 &lt;= 位元速率 &lt;= 288<br/><br/> - 96000 : 128 &lt;= 位元速率 &lt;= 288<br/><br/> 2：<br/><br/> - 11025 : 16 &lt;= 位元速率 &lt; 24<br/><br/> - 12000 : 16 &lt;= 位元速率 &lt; 24<br/><br/> - 16000 : 16 &lt;= 位元速率 &lt; 40<br/><br/> - 22050 : 32 &lt;= 位元速率 &lt; 40<br/><br/> - 24000 : 32 &lt;= 位元速率 &lt; 40<br/><br/> - 32000 :  40 &lt;= 位元速率 &lt;= 384<br/><br/> - 44100 : 96 &lt;= 位元速率 &lt;= 576<br/><br/> - 48000 : 96 &lt;= 位元速率 &lt;= 576<br/><br/> - 88200 : 256 &lt;= 位元速率 &lt;= 576<br/><br/> - 96000 : 256 &lt;= 位元速率 &lt;= 576<br/><br/> 5/6:<br/><br/> - 32000 : 160 &lt;= 位元速率 &lt;= 896<br/><br/> - 44100 : 240 &lt;= 位元速率 &lt;= 1024<br/><br/> - 48000 : 240 &lt;= 位元速率 &lt;= 1024<br/><br/> - 88200 : 640 &lt;= 位元速率 &lt;= 1024<br/><br/> - 96000 : 640 &lt;= 位元速率 &lt;= 1024<br/><br/> 8:<br/><br/> - 32000 : 224 &lt;= 位元速率 &lt;= 1024<br/><br/> - 44100 : 384 &lt;= 位元速率 &lt;= 1024<br/><br/> - 48000 : 384 &lt;= 位元速率 &lt;= 1024<br/><br/> - 88200 : 896 &lt;= 位元速率 &lt;= 1024<br/><br/> - 96000 : 896 &lt;= 位元速率 &lt;= 1024  
**HEAACV1**|1:<br/><br/> - 22050 : 位元速率 = 8<br/><br/> - 24000 : 8 &lt;= 位元速率 &lt;= 10<br/><br/> - 32000 : 12 &lt;= 位元速率 &lt;= 64<br/><br/> - 44100 : 20 &lt;= 位元速率 &lt;= 64<br/><br/> - 48000 : 20 &lt;= 位元速率 &lt;= 64<br/><br/> - 88200 : 位元速率 = 64<br/><br/> 2：<br/><br/> - 32000 : 16 &lt;= 位元速率 &lt;= 128<br/><br/> - 44100 : 16 &lt;= 位元速率 &lt;= 128<br/><br/> - 48000 : 16 &lt;= 位元速率 &lt;= 128<br/><br/> - 88200 : 96 &lt;= 位元速率 &lt;= 128<br/><br/> - 96000 : 96 &lt;= 位元速率 &lt;= 128<br/><br/> 5/6:<br/><br/> - 32000 : 64 &lt;= 位元速率 &lt;= 320<br/><br/> - 44100 : 64 &lt;= 位元速率 &lt;= 320<br/><br/> - 48000 : 64 &lt;= 位元速率 &lt;= 320<br/><br/> - 88200 : 256 &lt;= 位元速率 &lt;= 320<br/><br/> - 96000 : 256 &lt;= 位元速率 &lt;= 320<br/><br/> 8:<br/><br/> - 32000 : 96 &lt;= 位元速率 &lt;= 448<br/><br/> - 44100 : 96 &lt;= 位元速率 &lt;= 448<br/><br/> - 48000 : 96 &lt;= 位元速率 &lt;= 448<br/><br/> - 88200 : 384 &lt;= 位元速率 &lt;= 448<br/><br/> - 96000 : 384 &lt;= 位元速率 &lt;= 448  
**HEAACV2**|2：<br/><br/> - 22050 : 8 &lt;= 位元速率 &lt;= 10<br/><br/> - 24000 : 8 &lt;= 位元速率 &lt;= 10<br/><br/> - 32000 : 12 &lt;= 位元速率 &lt;= 64<br/><br/> - 44100 : 20 &lt;= 位元速率 &lt;= 64<br/><br/> - 48000 : 20 &lt;= 位元速率 &lt;= 64<br/><br/> - 88200 : 64 &lt;= 位元速率 &lt;= 64  
  

## <a name="Clip"></a> 剪輯
### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **StartTime** |**xs:duration** |指定的簡報 hello 開始時間。 hello StartTime 值必須 toomatch hello 絕對時間戳記的 hello 輸入視訊。 例如，如果 hello hello 輸入視訊的第一個畫面格具有時間戳記的 12:00:10.000，則 StartTime 應該至少 12:00:10.000 或更高。 |
| **Duration** |**xs:duration** |指定的簡報 （例如，在 hello 視訊重疊的外觀） hello 持續時間。 |

## <a name="Output"></a> 輸出
### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **FileName** |**xs:string** |hello hello 輸出檔案名稱。<br/><br/> 您可以使用下列資料表 toobuild hello 輸出檔案名稱的 hello 中所述的巨集。 例如：<br/><br/> **"Outputs": [      {       "FileName": "{Basename}*{Resolution}*{Bitrate}.mp4",       "Format": {         "Type": "MP4Format"       }     }   ]** |

### <a name="macros"></a>巨集
| 巨集 | 說明 |
| --- | --- |
| **{Basename}** |如果您要 VoD 編碼，hello {Basename} 是 hello hello AssetFile.Name 屬性 hello hello 輸入資產中的主要檔案的前 32 個字元。<br/><br/> 如果 hello 輸入的資產是即時封存，然後 hello {Basename} 被衍生自 hello 伺服器資訊清單中的 hello trackName 屬性。 如果您正在提交 subclip 工作使用中的 hello TopBitrate，:"< VideoStream\>TopBitrate < / VideoStream\>"，然後 hello 輸出檔包含視訊、 hello {Basename} 是 hello hello trackName hello 的前 32 個字元使用 hello 最高的位元速率視訊層。<br/><br/> 如果您改為提交 subclip 工作，例如使用 hello 輸入位元的所有 「 < VideoStream\>* < / VideoStream\>"，然後 hello 輸出檔包含視訊、 {Basename} 是 hello 前 32 個字元的 hello trackNamehello 對應視訊層。 |
| **{Codec}** |對應太"H264"視訊和音訊的"AAC"。 |
| **{Bitrate}** |hello 目標視訊位元速率 hello 輸出檔包含視訊和音訊，則目標音訊位元速率如果 hello 輸出檔包含僅限聲音。 使用的 hello 值為 hello 單位： kbps 的位元速率。 |
| **{Channel}** |如果 hello 檔案包含音效的音訊聲道計數。 |
| **{Width}** |Hello 視訊，像素為單位，在 hello 輸出檔案中，如果 hello 檔案包含視訊的寬度。 |
| **{Height}** |Hello 視訊，像素為單位，在 hello 輸出檔案中，如果 hello 檔案包含視訊的高度。 |
| **{Extension}** |繼承自 hello hello 輸出檔的 [類型] 屬性。 hello 輸出檔名稱必須是其中一個延伸模組的: 「 mp4 」，「 ts 」、 「 jpg 」、"png"或"bmp"。 |
| **{Index}** |縮圖的必要項。 應該只會出現一次。 |

## <a name="Video"></a> 視訊 (複雜類型繼承自轉碼器)
### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **啟動** |**xs:string** | |
| **Step** |**xs:string** | |
| **Range** |**xs:string** | |
| **PreserveResolutionAfterRotation** |**xs:boolean** |如需詳細說明，請參閱下列區段的 hello: [PreserveResolutionAfterRotation](media-services-mes-schema.md#PreserveResolutionAfterRotation) |

### <a name="PreserveResolutionAfterRotation"></a> PreserveResolutionAfterRotation
建議 toouse hello PreserveResolutionAfterRotation 旗標組合中的使用解析值以百分比表示 (寬度 ="100%"，高度 ="100%")。  

根據預設，hello 編碼的 hello 媒體編碼器標準 (MES) 預設為目標的 0 度旋轉的視訊解析度設定 （寬度、 高度）。 例如，如果您輸入的視訊是 1280 x 720 與零度旋轉，然後 hello 預設預設確保 hello 輸出有 hello 相同的解析度。 請參閱下圖。  

![MESRoation1](./media/media-services-shemas/media-services-mes-roation1.png) 

不過，這表示，如果 hello 輸入的視訊擷取為非零旋轉 （例如。 智慧型手機或平板電腦保留垂直），則 MES 依預設會套用 hello 編碼解析度設定 （寬度、 高度） toohello 輸入視訊，然後補償 hello 旋轉。 例如，請參閱下列的 hello 圖片。 hello 預設會使用寬度 ="100%"，高度 ="100%"，其中 MES 會解譯為需要 hello 輸出 toobe 1280 像素寬、 720 像素高。 之後旋轉 hello 視訊，然後壓縮 hello 圖片 toofit 在該視窗中，左側和右側，進而 toopillar 方塊區域上 hello。  

![MESRoation2](./media/media-services-shemas/media-services-mes-roation2.png) 

如果上述 hello 不是 hello 預期行為，則您可使用的 hello PreserveResolutionAfterRotation 旗標，並將它設定為太"，則為 true 」 （預設為"false"）。 因此如果您預設的寬度 ="100%"，高度 ="100%"和 PreserveResolutionAfterRotation 設定太"true"、 1280年像素寬且 720 像素高 90 度旋轉與輸入的視訊將產生的輸出與零度旋轉，但 720 像素寬和 1280年像素高。 請參閱下列的 hello 圖片。  

![MESRoation3](./media/media-services-shemas/media-services-mes-roation3.png) 

## <a name="FormatGroup"></a> FormatGroup (群組)
### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **BmpFormat** |**BmpFormat** | |
| **PngFormat** |**PngFormat** | |
| **JpgFormat** |**JpgFormat** | |

## <a name="BmpLayer"></a> BmpLayer
### <a name="element"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="PngLayer"></a> PngLayer
### <a name="element"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="JpgLayer"></a> JpgLayer
### <a name="element"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |
| **Quality**<br/><br/> minOccurs="0" |**xs:int** |有效值：1 (最差) - 100 (最佳) |

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="PngLayers"></a> PngLayers
### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **PngLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[PngLayer](media-services-mes-schema.md#PngLayer) | |

## <a name="BmpLayers"></a> BmpLayers
### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **BmpLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[BmpLayer](media-services-mes-schema.md#BmpLayer) | |

## <a name="JpgLayers"></a> JpgLayers
### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **JpgLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[JpgLayer](media-services-mes-schema.md#JpgLayer) | |

## <a name="BmpImage"></a> BmpImage (複雜類型繼承自視訊)
### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Png 圖層 |

## <a name="JpgImage"></a> JpgImage (複雜類型繼承自視訊)
### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Png 圖層 |

## <a name="PngImage"></a> PngImage (複雜類型繼承自視訊)
### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Png 圖層 |

## <a name="examples"></a>範例
如需根據此結構描述建置的 XML 預設值範例，請參閱 [MES (媒體編碼器標準) 的工作預設值](media-services-mes-presets-overview.md)。

## <a name="next-steps"></a>後續步驟
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


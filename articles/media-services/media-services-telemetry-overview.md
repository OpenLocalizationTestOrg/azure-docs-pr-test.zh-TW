---
title: "Media Services 遙測 aaaAzure |Microsoft 文件"
description: "本文提供 Azure 媒體服務遙測的概觀。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95c20ec4-c782-4063-8042-b79f95741d28
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 659e1c947a77aad0e4acacb541d95714da4775ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-telemetry"></a>Azure 媒體服務遙測

Azure 媒體服務 (AMS) 可讓您的服務 tooaccess 遙測/度量資料。 hello AMS 目前版本可讓您即時收集遙測資料**通道**， **StreamingEndpoint**，和即時**封存**實體。 

遙測以您指定的 Azure 儲存體帳戶的 tooa 儲存體資料表 （通常您會使用 hello AMS 帳戶相關聯的儲存體帳戶）。 

hello 遙測系統不會管理資料保留。 您可以藉由刪除 hello 儲存體資料表移除 hello 舊的遙測資料。

本主題討論如何 tooconfigure 和取用 hello AMS 遙測。

## <a name="configuring-telemetry"></a>設定遙測

您可以設定元件層級細微度的遙測。 詳細資料層級可分為「正常」和「詳細資訊」兩種。 目前，這兩個層級傳回 hello 相同的資訊。 建議 toouse"Normal。 

hello 下列主題顯示如何 tooenable 遙測：

[啟用搭配 .NET 的遙測](media-services-dotnet-telemetry.md) 

[啟用搭配 REST 的遙測](media-services-rest-telemetry.md)

## <a name="consuming-telemetry-information"></a>取用遙測資訊

遙測會寫入 Azure 儲存體資料表 tooan hello 設定遙測 hello Media Services 帳戶時所指定的儲存體帳戶中。 本章節描述 hello hello 度量的儲存體資料表。

您可以使用其中一個 hello 下列方式中的遙測資料：

- 直接從 Azure 資料表儲存體 （例如使用 hello 儲存體 SDK） 中讀取資料。 Hello 的遙測的儲存體資料表的說明，請參閱 hello**取用遙測資訊**中[這](https://msdn.microsoft.com/library/mt742089.aspx)主題。

或

- 使用 hello 支援 hello Media Services.NET SDK 中，讀取儲存體資料中所述[這](media-services-dotnet-telemetry.md)主題。 


如下所述的 hello 遙測結構描述是一種設計的 toogive 良好效能 hello 的 Azure 資料表儲存體的限制範圍內：

- 負責分割資料帳戶識別碼和服務識別碼，從獨立查詢每個服務 toobe tooallow 遙測。
- 資料分割包含 hello 日期 toogive hello 分割區大小上限合理。
- 資料列索引鍵是反向時間順序 tooallow hello 最近遙測項目 toobe 針對查詢以指定的服務。

這樣應該可讓許多常見查詢 toobe hello 有效率：

- 以平行方式獨立下載個別服務的資料。
- 擷取某日期範圍內指定服務的所有資料。
- 正在擷取服務的 hello 最新資料。

### <a name="telemetry-table-storage-output-schema"></a>遙測資料表儲存體輸出結構描述

遙測資料會儲存在一個資料表，其中"20160321 」 是 hello 建立資料表的日期"TelemetryMetrics20160321 」 中彙總。 遙測系統會以 00:00 UTC 為基準，為每一天建立個別的資料表。 hello 資料表用 toostore 週期性值這類內嵌的位元速率指定視窗的時間、 傳送的位元組等等。 

屬性|值|範例/附註
---|---|---
PartitionKey|{帳戶識別碼} _ {實體識別碼}|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66<br/<br/>hello hello 資料分割索引鍵 toosimplify 工作流程撰寫多個 Media Services 帳戶 toohello 中包含識別碼的帳戶相同的儲存體帳戶。
RowKey|{秒 toomidnight} _ {隨機值}|01688_00199<br/><br/>hello 資料列索引鍵開頭 hello 秒 toomidnight tooallow 資料分割內的前 n 個樣式查詢的數目。 如需詳細資訊，請參閱[本篇文章](../cosmos-db/table-storage-design-guide.md#log-tail-pattern)。 
Timestamp|日期/時間|自動從 hello Azure 資料表 2016年的時間戳記-09-09T22:43:42.241Z
類型|hello hello 實體提供遙測資料類型|頻道/串流端點/封存<br/><br/>事件類型只是字串值。
名稱|hello hello 遙測事件名稱|ChannelHeartbeat/StreamingEndpointRequestLog
ObservedTime|hello 時間 hello 遙測事件發生 (UTC)|2016-09-09T22:42:36.924Z<br/><br/>hello 觀察到提供 hello 實體傳送嗨遙測 （例如通道） 的時間。 元件之間可能有時間同步問題，因此這個值是近似值
ServiceID|{服務識別碼}|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
實體特定屬性|Hello 事件所定義|StreamName：stream1、Bitrate 10123…<br/><br/>已定義的指定事件類型的 hello 的 hello 其餘內容。 Azure 資料表內容是機碼值組。  （也就是 hello 資料表中的不同資料列有不同的屬性集）。

### <a name="entity-specific-schema"></a>實體特定結構描述

有三種類型的每個推送以下列頻率 hello 的實體特定 telemetric 資料項目：

- 串流端點：每 30 秒
- 直播頻道︰每分鐘
- 即時封存︰每分鐘

**串流端點**

屬性|值|範例
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Azure 資料表中的自動時間戳記 2016-09-09T22:43:42.241Z
類型|類型|StreamingEndpoint
名稱|名稱|StreamingEndpointRequestLog
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|服務識別碼|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
HostName|Hello 端點的主機名稱|builddemoserver.origin.mediaservices.windows.net
StatusCode|記錄 HTTP 狀態|200
ResultCode|結果碼詳細資料|S_OK
RequestCount|在 hello 彙總的要求總數|3
BytesSent|傳送的彙總位元組|2987358
ServerLatency|平均伺服器延遲 (包括儲存體)|129
E2ELatency|平均端對端延遲|250

**直播頻道**

屬性|值|範例/附註
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|自動從 hello Azure 資料表 2016年的時間戳記-09-09T22:43:42.241Z
類型|類型|通道
名稱|名稱|ChannelHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|服務識別碼|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
TrackType|曲目視訊/音訊/文字的類型|視訊/音訊
TrackName|Hello 曲目名稱|video/audio_1
Bitrate|曲目位元速率|785000
CustomAttributes||   
IncomingBitrate|實際連入位元速率|784548
OverlapCount|內嵌 hello 重疊|0
DiscontinuityCount|曲目不連續|0
LastTimestamp|上次內嵌資料時間戳記|1800488800
NonincreasingCount|片段捨棄因 toonon 增加的時間戳記的計數|2
UnalignedKeyFrames|我們是否收到主要畫面未對齊的片段 (跨品質等級) |True
UnalignedPresentationTime|我們是否收到呈現方式時間未對齊的片段 (跨品質等級/曲目)|True
UnexpectedBitrate|如果下列條件成立則為 True：音訊/視訊曲目的計算的/實際的位元速率 > 40,000 bps，且 IncomingBitrate == 0 或 IncomingBitrate 和 actualBitrate 相差 50% |True
Healthy|如果下列條件成立則為 True <br/>overlapCount、 <br/>DiscontinuityCount、 <br/>NonIncreasingCount、 <br/>UnalignedKeyFrames、 <br/>UnalignedPresentationTime 及 <br/>UnexpectedBitrate<br/> 均為 0|True<br/><br/>狀況良好是複合函式會傳回任何 hello 遵循條件保留時，則為 false:<br/><br/>- OverlapCount > 0<br/>- DiscontinuityCount > 0<br/>- NonincreasingCount > 0<br/>- UnalignedKeyFrames == True<br/>- UnalignedPresentationTime == True<br/>- UnexpectedBitrate == True

**即時封存**

屬性|值|範例/附註
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|自動從 hello Azure 資料表 2016年的時間戳記-09-09T22:43:42.241Z
類型|類型|封存
名稱|名稱|ArchiveHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|服務識別碼|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
ManifestName|程式 URL|asset-eb149703-ed0a-483c-91c4-e4066e72cce3/a0a5cfbf-71ec-4bd2-8c01-a92a2b38c9ba.ism
TrackName|Hello 曲目名稱|audio_1
TrackType|Hello 追蹤的類型|音訊/視訊
CustomAttribute|十六進位字串，用以區別名稱和位元速率相同的不同曲目 (多重攝影機角度)|
Bitrate|曲目位元速率|785000
Healthy|如果下列條件成立則為 True：FragmentDiscardedCount == 0 && ArchiveAcquisitionError == False|（這兩個值不會出現在 hello 度量，但會出現在 hello 來源事件），則為 true。<br/><br/>狀況良好是複合函式會傳回任何 hello 遵循條件保留時，則為 false:<br/><br/>- FragmentDiscardedCount > 0<br/>- ArchiveAcquisitionError == True

## <a name="general-qa"></a>一般問答集

### <a name="how-tooconsume-metrics-data"></a>如何 tooconsume 度量資料嗎？

度量資料會儲存為一系列的 Azure 資料表 hello 客戶儲存體帳戶中。 此資料可以使用下列工具 hello 取用：

- AMS SDK
- （支援匯出 toocomma 分隔值格式和處理中的 Excel） 的 Microsoft Azure 儲存體總管
- REST API

### <a name="how-toofind-average-bandwidth-consumption"></a>如何 toofind 平均頻寬的使用量？

hello 平均頻寬耗用量是一段時間的 BytesSent hello 平均。

### <a name="how-toodefine-streaming-unit-count"></a>如何計算 toodefine 資料流處理單位？

hello 串流單位計數，可以定義為從 hello 服務串流端點除以 hello 尖峰輸送量的一個資料流端點的 hello 尖峰輸送量。 hello 可用的尖峰輸送量一個資料流端點為 160 Mbps。
例如，假設從客戶的服務的 hello 尖峰輸送量為 40 MBps （hello 最大值 BytesSent 某段時間）。 接著，就是 hello 串流單位計數等於 too(40 MBps) * （8 位元/位元組） /(160 Mbps) = 2 的資料流處理單位。

### <a name="how-toofind-average-requestssecond"></a>如何 toofind 平均要求/秒嗎？

toofind hello 的平均數秒的要求，在某段時間計算 hello 要求平均數目 （計數）。

### <a name="how-toodefine-channel-health"></a>如何 toodefine 通道健全狀況？

通道健全狀況可以定義為複合布林函數，使它為 false，當任何 hello 下列條件：

- OverlapCount > 0
- DiscontinuityCount > 0
- NonincreasingCount > 0
- UnalignedKeyFrames == True 
- UnalignedPresentationTime == True 
- UnexpectedBitrate == True


### <a name="how-toodetect-discontinuities"></a>如何 toodetect 中斷點嗎？

toodetect 中斷點，然後尋找所有通道資料的項目位置 DiscontinuityCount > 0。 hello 對應 ObservedTime 時間戳記指出 hello hello 中斷點發生的時間。

### <a name="how-toodetect-timestamp-overlaps"></a>Toodetect 時間戳記重疊的方式？

toodetect 時間戳記重疊項目，然後尋找所有通道資料的項目位置 OverlapCount > 0。 hello 對應 ObservedTime 時間戳記指出在哪些 hello 時間戳記重疊的時間發生的 hello。

### <a name="how-toofind-streaming-request-failures-and-reasons"></a>如何 toofind 串流處理要求失敗，原因？

toofind 串流處理的要求失敗，原因，找出所有資料流端點的資料項目，ResultCode 不等於 tooS_OK。 hello 對應 StatusCode 欄位指出 hello hello 要求失敗的原因。

### <a name="how-tooconsume-data-with-external-tools"></a>如何與外部工具 tooconsume 資料嗎？

Telemetric 的資料可以處理，並以視覺化方式檢視以 hello 下列工具：

- PowerBI
- Application Insights
- Azure 監視器 (先前稱為 Shoebox)
- AMS 即時儀表板
- Azure 入口網站 (擱置中版本)

### <a name="how-toomanage-data-retention"></a>如何 toomanage 資料保留嗎？

hello 遙測系統不提供資料保留管理或自動刪除舊的記錄。 因此，您需要 toomanage，手動從 hello 存放裝置資料表刪除舊的記錄。 您可以如何參照 toostorage SDK toodo 它。

## <a name="next-steps"></a>後續步驟

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

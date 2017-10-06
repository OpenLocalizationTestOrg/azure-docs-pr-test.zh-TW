---
title: "aaaAzure 媒體服務串流端點概觀 |Microsoft 文件"
description: "本主題提供 Azure 媒體服務串流端點的概觀。"
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 097ab5e5-24e1-4e8e-b112-be74172c2701
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: f27f590175dcc945d1d3299fc0cae5a68cfbf4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-endpoints-overview"></a>串流端點概觀 

##<a name="overview"></a>概觀

在 「 Microsoft Azure 媒體服務 」 (AMS)**串流端點**表示串流服務，以便可以將內容直接 tooa 用戶端播放器應用程式或 tooa 內容傳遞網路 (CDN) 進行進一步的發佈。 媒體服務也提供順暢的 Azure CDN 整合。 hello StreamingEndpoint 服務的輸出資料流可以是資產的即時資料流、 隨選，或您，Media Services 帳戶中的漸進式下載的視訊。 每個「Azure 媒體服務」帳戶皆包含一個預設的 StreamingEndpoint。 Hello 帳戶下，可以建立其他的 Streamingendpoint。 StreamingEndpoint 有 1.0 和 2.0 兩個版本。 從 2017 年 1 月 10 日開始，所有新建立的 AMS 帳戶都會包含 2.0 版**預設** StreamingEndpoint。 其他串流端點，您將加入 toothis 帳戶也會是 2.0 版。 這項變更不會影響現有帳戶 hello;現有的 Streamingendpoint 將 1.0 版，而且可以升級的 tooversion 2.0。 透過這項變更會有行為、 帳單和功能的變更 (如需詳細資訊，請參閱 hello**資料流型別和版本**章節詳述如下)。

此外，從 Azure Media Services 開始 hello 2.15 版本 （2017 年 1 月發行），加入下列屬性 toohello 串流端點實體的 hello: **CdnProvider**， **CdnProfile**， **FreeTrialEndTime**， **StreamingEndpointVersion**。 如需這些屬性的詳細概觀，請參閱[這裡](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)。 

當您建立 Azure Media Services 帳戶預設值為您建立標準的資料流端點中 hello**已停止**狀態。 您無法刪除 hello 預設串流端點。 Hello Azure CDN 可用性 hello 目標區域中，根據預設，新建立的預設串流端點也包含 「 StandardVerizon"CDN 提供者整合。 

>[!NOTE]
>Azure CDN 整合可啟動串流端點的 hello 之前停用。

本主題提供 hello 串流端點所提供的主要功能的概觀。

## <a name="streaming-types-and-versions"></a>串流類型和版本

### <a name="standardpremium-types-version-20"></a>標準/進階類型 (2.0 版)

從媒體服務的 hello 2017 年 1 月版本開始，您有兩種串流類型：**標準**和**Premium**。 這些類型是"2.0"hello 串流端點版本的一部分。

類型|說明
---|---
**標準**|這是可行的 hello 大多數的 hello 案例的 hello 預設選項。<br/>使用此選項時，取得/有限 SLA，啟動之後的前 15 天 hello 串流端點是免費的。<br/>如果您建立一個以上的串流端點，只 hello 先其中一個是免費 hello 第 15 天，只要啟動它們會計費的其他人的 hello。 <br/>請注意，免費試用版僅適用於 toonewly 建立媒體服務帳戶和預設串流端點。 現有的資料流端點，此外建立串流端點不包含免費試用期間，即使它們是升級 tooversion 2.0 或 2.0 版會建立。
**高級**|這個選項適用於需要更大規模或控制的專業案例。<br/>以購買的進階串流單位 (SU) 容量為基礎的變動 SLA，專用的串流端點位於隔離的環境，不會競用資源。

如需詳細資訊，請參閱 hello**比較資料流類型**之後 > 一節。

### <a name="classic-type-version-10"></a>傳統類型 (1.0 版)

如果先前 toohello 年 1 月 10 2017年發行建立 AMS 帳戶的使用者，您有**傳統**串流端點的型別。 此類型是 hello 串流端點版本 「 1.0 」 的一部分。

如果您**「 1.0 」 版**串流端點已經 > = 1 的進階串流單位 (SU)，它將進階串流端點，且會提供所有 AMS 功能 (如同 hello**標準/優質**類型)而不需要任何額外的設定步驟。

>[!NOTE]
>**傳統**串流端點 ("1.0" 版和 0 SU) 提供有限的功能，且不包含 SLA。 建議 toomigrate 太**標準**輸入的 tooget 更好的體驗和 toouse 功能，例如動態封裝或加密與其他功能隨附的 hello**標準**型別。 toomigrate toohello**標準**輸入，請移 toohello [Azure 入口網站](https://portal.azure.com/)選取**opt-in tooStandard**。 如需有關移轉的詳細資訊，請參閱 hello[移轉](#migration-between-types)> 一節。
>
>請注意，這項作業無法回復，而且會影響價格。
>
 
## <a name="comparing-streaming-types"></a>比較串流類型

### <a name="versions"></a>版本

|類型|StreamingEndpointVersion|ScaleUnits|CDN|計費|SLA| 
|--------------|----------|-----------------|-----------------|-----------------|-----------------|    
|傳統|1.0|0|NA|免費|NA|
|標準串流端點|2.0|0|是|付費|是|
|進階串流單位|1.0|>0|是|付費|是|
|進階串流單位|2.0|>0|是|付費|是|

### <a name="features"></a>特性

功能|標準|高級
---|---|---
前 15 天免費| 是 |否
Throughput |向上 too600 Mbps 時不會使用 Azure CDN。 隨著 CDN 調整。|每個串流單位 (SU) 200 Mbps。 隨著 CDN 調整。
SLA | 99.9|99.9 (每個 SU 200 Mbps)。
CDN|Azure CDN、協力廠商 CDN 或沒有 CDN。|Azure CDN、協力廠商 CDN 或沒有 CDN。
按比例計費| 每日|每日
動態加密|是|是
動態封裝|是|是
調整|自動依據 toohello 目標輸送量。|其他串流單位
IP 篩選/G20/自訂主機|是|是
漸進式下載|是|是
建議用法 |Hello 大部分的資料流案例的建議使用。|專業用法。<br/>如果認為您的需求已超過「標準」。 如果您預期有 50,000 位以上的觀眾同時觀看，請連絡我們 (amsstreaming at microsoft.com)。


## <a name="migration-between-types"></a>在類型之間移轉

從 | 太| 動作
---|---|---
傳統|標準|需要 tooopt 中
傳統|高級| 調整 (其他串流單位)
標準/高階|傳統|無法使用 (如果串流端點版本為 1.0。 它允許設定 scaleunits toochange tooclassic 太"0 的")
標準 (含/不含 CDN)|Premium hello 與相同的組態|允許在 hello**啟動**狀態。 (透過 Azure 入口網站)
進階 (含/不含 CDN)|標準 hello 與相同的組態|允許在 hello**啟動**狀態 （透過 Azure 入口網站）
標準 (含/不含 CDN)|進階搭配不同的設定|允許在 hello**停止**狀態 （透過 Azure 入口網站）。 不允許在執行中狀態的 hello。
進階 (含/不含 CDN)|標準搭配不同的設定|允許在 hello**停止**狀態 （透過 Azure 入口網站）。 不允許在執行中狀態的 hello。
1.0 版，SU >= 1，含 CDN|標準/進階，不含 CDN|允許在 hello**停止**狀態。 不允許在 hello**啟動**狀態。
1.0 版，SU >= 1，含 CDN|標準，含/不含 CDN|允許在 hello**停止**狀態。 不允許在 hello**啟動**狀態。 將會刪除 1.0 版 CDN 並建立和啟動新的 CDN。
1.0 版，SU >= 1，含 CDN|進階，含/不含 CDN|允許在 hello**停止**狀態。 不允許在 hello**啟動**狀態。 將會刪除傳統 CDN 並建立和啟動新的 CDN。

## <a name="next-steps"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


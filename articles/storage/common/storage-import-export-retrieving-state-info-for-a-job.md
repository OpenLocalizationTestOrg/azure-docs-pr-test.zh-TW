---
title: "Azure 匯入/匯出作業的狀態資訊 aaaRetrieving |Microsoft 文件"
description: "了解如何 tooobtain 狀態之 Microsoft Azure 匯入/匯出服務作業的資訊。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 22d7e5f0-94da-49b4-a1ac-dd4c14a423c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: muralikk
ms.openlocfilehash: cbc35660519573d92f641924ac0025c9e577d69b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retrieving-state-information-for-an-importexport-job"></a>擷取匯入/匯出作業的狀態資訊
您可以呼叫 hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get)作業 tooretrieve 資訊同時匯入和匯出工作。 傳回的 hello 資訊包括：

-   hello 的 hello 作業的目前狀態。

-   每個工作已完成 hello 的近似百分比。

-   hello 的每個磁碟機的目前狀態。

-   Blob 的 URI，其中包含錯誤記錄檔和詳細資訊記錄的資訊 (如果啟用)。

hello 下列各節說明 hello 所傳回的 hello 資訊`Get Job`作業。

## <a name="job-states"></a>作業狀態
hello 表和 hello 狀態圖表說明作業而轉換透過在其生命週期的 hello 狀態。 hello 目前作業的狀態 hello 可藉由呼叫 hello`Get Job`作業。

![JobStates](./media/storage-import-export-retrieving-state-info-for-a-job/JobStates.png "JobStates")

hello 下表描述作業可能會通過每個狀態。

|作業狀態|說明|
|---------------|-----------------|
|`Creating`|之後呼叫 hello Put Job 作業，會建立一個作業，而且其狀態會設定太`Creating`。 在 hello hello 作業時`Creating`狀態、 hello 匯入/匯出服務會假設 hello 磁碟機尚未已出貨的 toohello 資料中心。 工作可能會維持在 hello`Creating`向上 tootwo 週之後, 便會自動刪除由 hello 服務狀態。<br /><br /> 如果在 hello hello 作業時呼叫 hello Update Job Properties 作業`Creating`狀態、 hello 作業會維持在 hello`Creating`狀態，以及 hello 逾時時間間隔是重設 tootwo 週。|
|`Shipping`|您寄送您的封裝之後，您應該太呼叫 hello Update Job Properties 作業更新 hello 作業的狀態 hello`Shipping`。 hello 傳送狀態可以設定，只有當 hello `DeliveryPackage` （貨運公司和追蹤號碼） 和 hello `ReturnAddress` hello 作業已設定屬性。<br /><br /> hello 作業會保留在 hello Shipping 狀態，如總 tootwo 週。 如果過了兩週，哪些尚未收到 hello 磁碟機，系統會通知 hello 匯入/匯出服務操作員。|
|`Received`|所有磁碟都已都收到 hello 資料中心之後，hello 作業狀態將設 toohello 已都接收 」 狀態。|
|`Transferring`|Hello 工作狀態 hello 資料中心已收到 hello 磁碟機且至少一個磁碟機已開始處理之後，會設定 toohello`Transferring`狀態。 請參閱 hello`Drive States`下面章節，如需詳細資訊。|
|`Packaging`|所有磁碟機已完成處理之後，hello 作業將會置於 hello`Packaging`狀態，直到 hello 磁碟機是已出貨後 toohello 客戶。|
|`Completed`|所有磁碟機已出貨後 toohello 客戶如果 hello 作業已完成不會發生錯誤之後再 hello 工作會設定 toohello`Completed`狀態。 hello 會自動刪除工作在 hello 90 天後`Completed`狀態。|
|`Closed`|如果已有任何錯誤 hello hello 作業處理期間，所有磁碟機已被已出貨後 toohello 客戶之後，再 hello 工作會設定 toohello`Closed`狀態。 hello 會自動刪除工作在 hello 90 天後`Closed`狀態。|

您只有在特定狀態才能取消作業。 已取消的工作會略過 hello 資料複製步驟，但它會依照的 hello 相同的狀態轉換為工作未取消，否則為。

hello 下表描述發生錯誤時，每個作業的狀態，以及 hello 影響 hello 作業可以發生的錯誤。

|作業狀態|Event|解析 / 後續步驟|
|---------------|-----------|------------------------------|
|`Creating or Undefined`|工作的一或多個磁碟機已抵達，但 hello 工作不處於 hello`Shipping`狀態或沒有 hello 服務中的 hello 作業的記錄。|hello 匯入/匯出服務作業小組將會嘗試 toocontact hello 客戶 toocreate 或更新與必要的資訊 toomove hello 工作向前 hello 作業。<br /><br /> 若是 hello 作業小組無法 toocontact hello 客戶兩週內，hello 作業小組會嘗試 tooreturn hello 磁碟機。<br /><br /> 無法傳回 hello 磁碟機，而且無法達到 hello 客戶 hello 事件，請在 hello 磁碟機將會安全地銷毀 90 天內。<br /><br /> 請注意太更新其狀態之前，無法處理作業`Shipping`。|
|`Shipping`|hello 工作的包裹超過兩週未抵達。|hello 作業小組將通知 hello 客戶的 hello 遺漏的封裝。 根據 hello 客戶的回應，hello 作業小組將擴充 hello 封裝 tooarrive 的 hello 間隔 toowait 或取消 hello 工作。<br /><br /> Hello 事件中的 hello 客戶無法連絡或沒有回應 30 天內，hello 作業小組將會起始動作 toomove hello 作業從 hello`Shipping`狀態直接 toohello`Closed`狀態。|
|`Completed/Closed`|hello 磁碟機從未達到 hello 寄件地址，或者 （適用於只有 tooan 匯出工作） 的出貨中損毀。|如果 hello 磁碟機不會送達 hello 寄件地址，hello 客戶應該第一個呼叫 hello Get Job 作業，或檢查 hello 工作狀態在 hello 入口 tooensure 該磁碟機已寄出的 hello。 如果 hello 磁碟機已寄出，然後 hello 客戶應該連絡 hello 傳送提供者 tootry，並找出 hello 磁碟機。<br /><br /> 如果 hello 磁碟機在寄送過程中損毀，hello 客戶可能想要 toorequest 另一項匯出工作或下載 hello 遺漏的 blob。|
|`Transferring/Packaging`|作業的退貨地址不正確或遺失。|hello 作業小組會聯繫 toohello 聯絡人 hello 作業 tooobtain hello 正確地址。<br /><br /> Hello 事件中該 hello 客戶在無法聯繫，磁碟機將於 90 天後安全地銷毀的 hello。|
|`Creating / Shipping/ Transferring`|不會出現在匯入的磁碟機 toobe hello 清單中的磁碟機隨附於 hello 傳送封裝。|hello 額外的磁碟機將不會處理，而且將會傳回 toohello 客戶 hello 工作完成時。|

## <a name="drive-states"></a>磁碟機狀態
hello 資料表和 hello 圖說明個別磁碟機的 hello 生命週期，過程中轉換匯入或匯出工作。 您可以擷取目前的磁碟機狀態 hello 呼叫 hello`Get Job`作業並檢查 hello `State` hello 的項目`DriveList`屬性。

![DriveStates](./media/storage-import-export-retrieving-state-info-for-a-job/DriveStates.png "DriveStates")

hello 下表說明每個磁碟機可能經歷的狀態。

|磁碟機狀態|說明|
|-----------------|-----------------|
|`Specified`|匯入工作，以 hello Put Job 作業建立 hello 作業時 hello 磁碟機的初始狀態為 hello`Specified`狀態。 匯出工作，因為建立 hello 作業時，指定沒有磁碟機 hello 初始磁碟機狀態為 hello`Received`狀態。|
|`Received`|hello 磁碟機會轉換 toohello`Received`匯入/匯出服務操作員已經處理 hello 磁碟機已收到從 hello 傳送公司匯入工作的狀態時 hello。 匯出工作，hello 初始磁碟機狀態為 hello`Received`狀態。|
|`NeverReceived`|hello 磁碟機會移 toohello`NeverReceived`狀態時 hello 工作的包裹抵達但 hello 封裝不包含 hello 磁碟機。 如果已經兩週 hello 服務收到 hello 傳送的資訊，但 hello 封裝有尚未抵達 hello 資料中心，磁碟機也可以移動進入此狀態。|
|`Transferring`|磁碟機會移 toohello`Transferring`狀態時 hello 服務開始 tootransfer hello 磁碟機 tooWindows Azure 儲存體的資料。|
|`Completed`|磁碟機會移 toohello`Completed`狀態時 hello 服務已順利傳送所有 hello 資料未發生任何錯誤。|
|`CompletedMoreInfo`|磁碟機會移 toohello`CompletedMoreInfo`當 hello 服務發生一些問題複製資料時從或 toohello 磁碟機的狀態。 hello 資訊可能包括錯誤、 警告或參考用訊息有關覆寫 blob。|
|`ShippedBack`|hello 磁碟機會移 toohello`ShippedBack`已出貨從 hello 資料中心回 toohello 傳回位址時的狀態。|

hello 以下表格說明 hello 磁碟機失敗狀態，以及所採取的每個狀態的 hello 動作。

|磁碟機狀態|Event|解決方法/後續步驟|
|-----------------|-----------|-----------------------------|
|`NeverReceived`|標示為的磁碟機`NeverReceived`到達另一個 「 出貨 」 （因為它未收到 hello 作業的出貨的一部分）。|hello 作業小組會移動 hello 磁碟機 toohello`Received`狀態。|
|`N/A`|不屬於任何工作的磁碟機送達 hello 資料中心做為另一項工作的一部分。|hello 磁碟機將會標示為額外的磁碟機，並將傳回 toohello 客戶 hello 與 hello 原始封裝相關聯的工作完成時。|

## <a name="faulted-states"></a>發生錯誤的狀態
Hello 工作或磁碟機或磁碟機的作業失敗時 tooprogress 通常透過其預期的生命週期，會移入`Faulted`狀態。 此時，hello 作業小組將連絡 hello 客戶透過電子郵件或電話。 Hello 問題解決後，hello 發生錯誤的工作，或是磁碟機將會超出 hello`Faulted`狀態並移至 hello 適當的狀態。

## <a name="next-steps"></a>後續步驟

* [使用 hello 匯入/匯出服務 REST API](storage-import-export-using-the-rest-api.md)

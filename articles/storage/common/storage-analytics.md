---
title: "Azure 儲存體分析 toocollect 記錄檔和度量資料 aaaUse |Microsoft 文件"
description: "儲存體分析可讓您所有儲存體服務，tootrack 度量資料和 toocollect 記錄檔中的 Blob、 佇列和資料表儲存體。"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7894993b-ca42-4125-8f17-8f6dfe3dca76
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: aba1a236cb69fa2e60bcb8fda5d34841e36e379a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storage-analytics"></a>儲存體分析

Azure 儲存體分析會執行記錄，並提供儲存體帳戶的度量資料。 您可以使用此資料 tootrace 要求、 分析使用趨勢，以及診斷儲存體帳戶的問題。

toouse 儲存體分析，您必須先啟用個別針對每個服務要 toomonitor。 您可以啟用它從 hello [Azure 入口網站](https://portal.azure.com)。 如需詳細資訊，請參閱[監視 hello Azure 入口網站的儲存體帳戶](storage-monitor-storage-account.md)。 您也可以啟用儲存體分析，以程式設計方式透過 hello REST API 或 hello 用戶端程式庫。 使用 hello[取得 Blob 服務屬性](https://msdn.microsoft.com/library/hh452239.aspx)，[取得佇列服務屬性](https://msdn.microsoft.com/library/hh452243.aspx)，[取得表格服務屬性](https://msdn.microsoft.com/library/hh452238.aspx)，和[取得檔案服務屬性](https://msdn.microsoft.com/library/mt427369.aspx)作業 tooenable 儲存體分析的每個服務。

hello 彙總的資料儲存在已知的 blob （用於記錄） 和已知資料表 （用於度量），可能會使用 hello Blob 服務和表格服務 Api 存取。

儲存體分析會將 20 TB 限制對 hello 儲存的資料量 hello 儲存體帳戶總限制無關。 如需計費和資料保留原則的詳細資訊，請參閱 [儲存體分析和計費](https://msdn.microsoft.com/library/hh360997.aspx)。 如需儲存體帳戶限制的詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。

如需使用儲存體分析和其他工具 tooidentify 的深度指南，診斷和疑難排解 Azure 儲存體相關問題，請參閱[監視、 診斷和疑難排解 Microsoft Azure 儲存體](storage-monitoring-diagnosing-troubleshooting.md)。

## <a name="about-storage-analytics-logging"></a>關於儲存體分析記錄
儲存體分析記錄成功和失敗的要求 tooa 儲存體服務的詳細的資訊。 這項資訊可以使用的 toomonitor 個別要求和 toodiagnose 與儲存體服務的問題。 系統會以最佳方式來記錄要求。

只有在發生儲存體服務活動時，才會建立記錄檔項目。 例如，如果儲存體帳戶有活動，其 Blob 服務中，但不是在其資料表或佇列服務，會建立相關 toohello Blob 服務的記錄。

儲存體分析記錄不適用於 Azure 檔案儲存體。

### <a name="logging-authenticated-requests"></a>記錄驗證要求
會記錄下列類型的驗證要求的 hello:

* 成功的要求。
* 失敗的要求，包括逾時、節流、網路、授權和其他錯誤。
* 使用共用存取簽章 (SAS) 的要求，包括失敗和成功的要求。
* 要求 tooanalytics 資料。

系統不會記錄儲存體分析本身所提出的要求 (例如，記錄檔的建立或刪除)。 Hello 記錄資料的完整清單會記載在 hello[儲存體分析記錄作業和狀態訊息](https://msdn.microsoft.com/library/hh343260.aspx)和[儲存體分析記錄格式](https://msdn.microsoft.com/library/hh343259.aspx)主題。

### <a name="logging-anonymous-requests"></a>記錄匿名要求
會記錄下列類型的匿名要求的 hello:

* 成功的要求。
* 伺服器錯誤。
* 用戶端與伺服器的逾時錯誤。
* 失敗的 GET 要求，錯誤碼為 304 (未修改)。

系統不會記錄所有其他失敗的匿名要求。 Hello 記錄資料的完整清單會記載在 hello[儲存體分析記錄作業和狀態訊息](https://msdn.microsoft.com/library/hh343260.aspx)和[儲存體分析記錄格式](https://msdn.microsoft.com/library/hh343259.aspx)主題。

### <a name="how-logs-are-stored"></a>記錄檔的儲存方式
所有記錄檔都會儲存在名為 $logs 的容器內的區塊 Blob 中，該容器是在針對儲存體帳戶啟用儲存體分析時自動建立的。 hello $logs 容器位於 hello blob 命名空間中的 hello 儲存體帳戶，例如： `http://<accountname>.blob.core.windows.net/$logs`。 一旦啟用儲存體分析之後便無法刪除此容器，不過您可以刪除其內容。

> [!NOTE]
> hello $logs 容器不會顯示執行容器列出作業時，例如 hello [ListContainers](https://msdn.microsoft.com/library/azure/dd179352.aspx)方法。 您必須直接存取它。 例如，您可以使用 hello [ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx)方法 tooaccess hello blob 在 hello`$logs`容器。
> 記錄要求時，儲存體分析將會以區塊形式上傳中繼結果。 儲存體分析會定期認可這些區塊，並提供它們做為 Blob。
> 
> 

Hello 中建立的記錄檔可能會有重複的記錄相同的小時。 您可以判斷記錄是否為重複檢查 hello **RequestId**和**作業**數目。

### <a name="log-naming-conventions"></a>記錄檔命名慣例
每個記錄檔會採用下列格式的 hello。

    <service-name>/YYYY/MM/DD/hhmm/<counter>.log

hello 下表說明每個屬性在 hello 記錄檔名稱。

| 屬性 | 說明 |
| --- | --- |
| <service-name> |hello hello 儲存體服務的名稱。 例如：Blob、資料表或佇列。 |
| YYYY |hello hello 記錄檔的四位數年份。 例如：2011。 |
| MM |hello hello 記錄檔的兩位數月份。 例如：07。 |
| DD |hello hello 記錄檔的兩位數月份。 例如：07。 |
| hh |表示開始小時 hello hello hello 兩位數小時，採用 24 小時制 UTC 格式記錄。 例如：18。 |
| mm |表示開始分鐘的 hello 記錄檔的 hello hello 兩位數字。 在儲存體分析的 hello 目前版本中不支援此值，其值一律為 00。 |
| <counter> |以零為起始的六位數計數器，指出 hello hello 儲存體服務中一小時內產生的記錄檔 blob 數目。 此計數器會從 000000 開始。 例如：000001。 |

hello 以下是結合 hello 前一個範例的完整範例記錄檔名稱。

    blob/2011/07/31/1800/000001.log

hello 以下是範例可以使用的 tooaccess hello 先前記錄的 URI。

    https://<accountname>.blob.core.windows.net/$logs/blob/2011/07/31/1800/000001.log

記錄儲存體要求時，產生記錄檔名稱 hello 相互關聯 toohello 小時 hello 要求作業完成時。 例如，如果 GetBlob 要求已在 在 7/31/2011 hello 記錄檔寫入時會包含下列前置詞的 hello:`blob/2011/07/31/1800/`

### <a name="log-metadata"></a>記錄中繼資料
所有記錄檔 blob 會儲存並可使用的 tooidentify 包含何種記錄資料 hello blob 的中繼資料。 hello 下表描述每個中繼資料屬性。

| 屬性 | 說明 |
| --- | --- |
| LogType |描述 hello 記錄檔是否包含 tooread、 寫入或刪除作業的相關資訊。 此值可包含一個類型或是所有這三種類型的組合 (以逗號分隔)。 範例 1：write；範例 2：read,write；範例 3：read,write,delete。 |
| StartTime |hello 最早時間 YYYY hello 形式的 hello 記錄中的項目-MM-DDThh:mm:ssZ。 例如：2011-07-31T18:21:46Z。 |
| EndTime |hello 最晚時間 YYYY hello 形式的 hello 記錄中的項目-MM-DDThh:mm:ssZ。 例如：2011-07-31T18:22:09Z。 |
| LogVersion |hello hello 記錄格式版本。 目前僅支援 hello 值為 1.0。 |

hello 下列清單顯示使用 hello 前一個範例的完整範例中繼資料。

* LogType=write
* StartTime=2011-07-31T18:21:46Z
* EndTime=2011-07-31T18:22:09Z
* LogVersion=1.0

### <a name="accessing-logging-data"></a>存取記錄資料
Hello 中的所有資料`$logs`使用 hello Blob 服務 Api 也可以存取容器、 hello hello 所提供的.NET Api 包括 Azure managed 程式庫。 hello 儲存體帳戶管理員可以讀取和刪除記錄檔，但無法建立或更新它們。 查詢記錄檔時，可以使用 hello 記錄檔的中繼資料和記錄檔名稱。 很可能在指定時段內的記錄檔 tooappear 順序，但 hello 中繼資料一律會指定記錄檔項目 hello timespan 記錄檔中。 因此，您可以在搜尋特定記錄檔時使用記錄檔名稱和中繼資料的組合。

## <a name="about-storage-analytics-metrics"></a>關於儲存體分析度量
儲存體分析可儲存有關要求 tooa 儲存體服務的彙總的交易統計資料和容量資料的度量。 在這兩個 hello 應用程式開發介面作業層級，以及在 hello 儲存體服務層級報告交易和容量會報告在 hello 儲存體服務層級。 度量資料可使用的 tooanalyze 儲存體服務使用量，要求的 hello 儲存體服務，與使用服務的應用程式的 tooimprove hello 效能診斷問題。

toouse 儲存體分析，您必須先啟用個別針對每個服務要 toomonitor。 您可以啟用它從 hello [Azure 入口網站](https://portal.azure.com)。 如需詳細資訊，請參閱[監視 hello Azure 入口網站的儲存體帳戶](storage-monitor-storage-account.md)。 您也可以啟用儲存體分析，以程式設計方式透過 hello REST API 或 hello 用戶端程式庫。 使用 hello**取得服務屬性**作業 tooenable 儲存體分析的每個服務。

### <a name="transaction-metrics"></a>交易度量
系統會以每小時或每分鐘的時間間隔，為每個儲存體服務和要求的 API 作業記錄完善的資料集，其中包括輸入流量/輸出流量、可用性、錯誤，以及已分類的要求百分比。 您可以看到在 hello hello 交易詳細資料的完整清單[儲存體分析度量資料表結構描述](https://msdn.microsoft.com/library/hh343264.aspx)主題。

在兩個層級： hello 服務層級和 hello 應用程式開發介面作業層級會記錄交易資料。 在 hello 服務層級統計資料彙總所有要求的 API 作業會寫入 tooa 資料表實體的每個小時即使沒有要求進行 toohello 服務。 在 hello 應用程式開發介面作業層級，統計資料是只寫入的 tooan 實體，如果該小時內已要求 hello 作業。

例如，如果您執行**GetBlob**對 Blob 服務，儲存體分析度量的作業將記錄 hello 要求，並包含在 hello 彙總資料的同時 hello Blob 服務，以及 hello **GetBlob**作業。 不過，如果沒有**GetBlob** hello 小時期間要求作業時，實體將不會寫入 toohello`$MetricsTransactionsBlob`該作業。

系統會針對使用者要求及儲存體分析本身所提出的要求記錄交易度量。 例如，會記錄由儲存體分析 toowrite 記錄檔和資料表實體的要求。 如需這些要求之計費方式的詳細資訊，請參閱 [儲存體分析及計費](https://msdn.microsoft.com/library/hh360997.aspx)。

### <a name="capacity-metrics"></a>容量度量
> [!NOTE]
> 目前，才可 hello Blob 服務的容量度量。 Hello 表格服務和佇列服務的容量度量將可在儲存體分析的未來版本中。
> 
> 

系統每日都會針對儲存體帳戶的 Blob 服務記錄容量資料，並寫入兩個資料表實體。 一個實體提供的使用者資料的統計資料和其他 hello 提供 hello 相關統計資料`$logs`儲存體分析所使用的 blob 容器。 hello`$MetricsCapacityBlob`資料表包含下列統計資料的 hello:

* **容量**: hello hello 儲存體帳戶之 Blob 服務，以位元組為單位所使用的儲存體的數量。
* **ContainerCount**: hello hello 儲存體帳戶之 Blob 服務中的 blob 容器的數目。
* **ObjectCount**: hello 認可及未認可區塊或分頁 blob 數目 hello 儲存體帳戶之 Blob 服務中的。

如需 hello 容量度量的詳細資訊，請參閱[儲存體分析度量資料表結構描述](https://msdn.microsoft.com/library/hh343264.aspx)。

### <a name="how-metrics-are-stored"></a>度量的儲存方式
為每個 hello 儲存體服務的所有度量資料都儲存在該服務保留的三個資料表： 其中一個資料表用於交易資訊、 一個資料表用於分鐘交易資訊與另一個資料表用於容量資訊。 交易和每分鐘交易資訊都是由要求和回應資料所組成，而容量資訊是由儲存體使用量資料所組成。 小時度量、 每分鐘度量和容量的儲存體帳戶之 Blob 服務可以存取命名 hello 下表中所述的資料表中。

| 度量層級 | 資料表名稱 | 支援的版本 |
| --- | --- | --- |
| 每小時度量，主要位置 |$MetricsTransactionsBlob  <br/>$MetricsTransactionsTable <br/> $MetricsTransactionsQueue |版本先前 too2013-08-15 只。 雖然仍然支援這些名稱，但建議您先切換 toousing hello 資料表下面所列。 |
| 每小時度量，主要位置 |$MetricsHourPrimaryTransactionsBlob <br/>$MetricsHourPrimaryTransactionsTable <br/>$MetricsHourPrimaryTransactionsQueue |所有版本 (包含 2013-08-15)。 |
| 每分鐘度量，主要位置 |$MetricsMinutePrimaryTransactionsBlob <br/>$MetricsMinutePrimaryTransactionsTable <br/>$MetricsMinutePrimaryTransactionsQueue |所有版本 (包含 2013-08-15)。 |
| 每小時度量，次要位置 |$MetricsHourSecondaryTransactionsBlob  <br/>$MetricsHourSecondaryTransactionsTable <br/>$MetricsHourSecondaryTransactionsQueue |所有版本 (包含 2013-08-15)。 必須啟用讀取存取異地備援複寫。 |
| 每分鐘度量，次要位置 |$MetricsMinuteSecondaryTransactionsBlob  <br/>$MetricsMinuteSecondaryTransactionsTable <br/>$MetricsMinuteSecondaryTransactionsQueue |所有版本 (包含 2013-08-15)。 必須啟用讀取存取異地備援複寫。 |
| 容量 (僅限 Blob 服務) |$MetricsCapacityBlob |所有版本 (包含 2013-08-15)。 |

針對儲存體帳戶啟用儲存體分析時，即會自動建立這些資料表。 存取透過 hello 命名空間的 hello 儲存體帳戶，例如：`https://<accountname>.table.core.windows.net/Tables("$MetricsTransactionsBlob")`

### <a name="accessing-metrics-data"></a>存取度量資料
可以使用 hello 表格服務應用程式開發介面存取 hello 度量資料表中的所有資料，包括 hello hello 所提供的.NET Api Azure managed 程式庫。 hello 儲存體帳戶管理員可以讀取和刪除資料表實體，但無法建立或更新它們。

## <a name="billing-for-storage-analytics"></a>儲存體分析計費
所有度量資料的儲存體帳戶的 hello 服務都寫入。 因此，儲存體分析所執行的每個寫入作業都會列入計費。 此外，也會列入計費的度量資料所使用的儲存體的 hello 數量。

hello 下列儲存體分析所執行的動作會列入計費：

* 要求記錄的 toocreate blob。 
* 要求 toocreate 資料表實體的度量。

如果您已設定資料保留原則，就不需在儲存體分析刪除舊記錄和度量資料時支付刪除交易的費用。 不過，從用戶端刪除交易會列入計費。 如需保留原則的詳細資訊，請參閱 [設定儲存體分析資料保留原則](https://msdn.microsoft.com/library/azure/hh343263.aspx)。

### <a name="understanding-billable-requests"></a>了解計費要求
計費或非計費 tooan 帳戶的儲存體服務所做的每個要求。 儲存體分析記錄進行 tooa 服務，包括狀態訊息，指出如何 hello 要求已處理的每個要求。 同樣地，儲存體分析會儲存該服務，包括 hello 百分比和計數的特定狀態訊息的服務和 hello API 作業的度量。 在一起，這些功能可協助您分析計費要求、 改良您的應用程式，以及診斷要求 tooyour 服務的問題。 如需計費的詳細資訊，請參閱 [了解 Azure 儲存體計費 - 頻寬、交易和容量](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx)。

在儲存體分析資料時，您可以使用 hello 資料表中 hello[儲存體分析記錄作業和狀態訊息](https://msdn.microsoft.com/library/azure/hh343260.aspx)主題 toodetermine 哪些要求會列入計費。 然後您可以將記錄檔和度量資料 toohello 狀態訊息 toosee 如果比較支付特定要求。 您也可以使用在先前主題 tooinvestigate 可用性 hello 的 hello 資料表儲存體服務或個別的應用程式開發介面作業。

## <a name="next-steps"></a>後續步驟
### <a name="setting-up-storage-analytics"></a>設定儲存體分析
* [監視 hello Azure 入口網站的儲存體帳戶](storage-monitor-storage-account.md)
* [啟用及設定儲存體分析](https://msdn.microsoft.com/library/hh360996.aspx)

### <a name="storage-analytics-logging"></a>儲存體分析記錄
* [關於儲存體分析記錄](https://msdn.microsoft.com/library/hh343262.aspx)
* [儲存體分析記錄檔格式](https://msdn.microsoft.com/library/hh343259.aspx)
* [儲存體分析記錄作業和狀態訊息](https://msdn.microsoft.com/library/hh343260.aspx)

### <a name="storage-analytics-metrics"></a>儲存體分析度量
* [關於儲存體分析度量](https://msdn.microsoft.com/library/hh343258.aspx)
* [儲存體分析度量資料表結構描述](https://msdn.microsoft.com/library/hh343264.aspx)
* [儲存體分析記錄作業和狀態訊息](https://msdn.microsoft.com/library/hh343260.aspx)  


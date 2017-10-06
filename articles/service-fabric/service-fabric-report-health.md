---
title: "自訂服務網狀架構健全狀況報表 aaaAdd |Microsoft 文件"
description: "描述 toosend 自訂健全狀況報告 tooAzure Service Fabric 健康實體的方式。 提供設計和實作高品質健康狀態報告的建議。"
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 0a00a7d2-510e-47d0-8aa8-24c851ea847f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 12c9f664e2a457b4e1e8f340873ca60ebcefb097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-service-fabric-health-reports"></a>新增自訂 Service Fabric 健康狀態報告
Azure Service Fabric 導入了[健全狀況模型](service-fabric-health-introduction.md)設計 tooflag 狀況不良的叢集，並在特定實體的應用程式狀況。 hello 健全狀況模型使用**健全狀況 reporters** （系統元件和 watchdogs）。 hello 目標是簡單、 快速地診斷並修復。 服務寫入器需要 toothink 預先關於健全狀況。 應該報告可能會影響健全狀況的任何條件，尤其是它可以幫助旗標關閉 toohello 根本的問題。 hello 健全狀況資訊可以在偵錯及調查，節省時間與精力。 hello 效益是特別明顯一旦 hello 服務已啟動並執行 hello 雲端中大規模 （私人或 Azure）。

感興趣的條件來識別 hello Service Fabric reporters 監視器。 它們會依據其本機檢視回報這些條件。 hello[健全狀況存放區](service-fabric-health-introduction.md#health-store)彙總健全狀況資料傳送所有 reporters toodetermine 是否實體的全域狀況良好。 預定的 toobe 豐富、 彈性且容易 toouse hello 模型。 hello 健康情況報告的 hello 品質決定 hello 精確度的 hello hello 叢集健全狀況檢視。 不正確顯示出健康不良的問題之誤報，會對升級或其他使用健康狀態資料的服務產生負面影響。 這類服務的範例包括修復服務和警示機制。 因此，思考是擷取感興趣 hello 條件的所需的 tooprovide 報告的最佳可能方式。

toodesign 和實作健全狀況報告、 watchdogs 和系統元件必須：

* 定義感興趣的 hello 條件、 hello 方式會受到監控，與 hello 影響 hello 叢集或應用程式的功能。 根據這項資訊，決定 hello 健全狀況報表的屬性和健全狀況狀態。
* 判斷 hello[實體](service-fabric-health-introduction.md#health-entities-and-hierarchy)hello 報表套用至。
* 從 hello 服務，或從內部或外部的監視，請決定其中完成 hello 報告。
* 定義使用來源 tooidentify hello 報告。
* 選擇報告策略是定期或是轉換時。 hello 建議方式是定期，因為它需要更簡單的程式碼，而是較不容易出錯的 tooerrors。
* 決定多久 hello 報表，針對狀況不良的條件應該保持 hello health store 中以及應該清除。 使用這項資訊，決定 hello 報表階段 toolive 並移除上到期行為。

如前所述，報告可以從以下項目完成：

* hello 監視 Service Fabric 服務複本。
* 內部監視程式會部署為 Service Fabric 服務 (例如，可監視條件和問題報告的 Service Fabric 無狀態服務)。 可以是 hello watchdogs 部署所有的節點，或可以是相關的 toohello 監視的服務。
* 內部 watchdogs hello Service Fabric 節點上執行但*不*實作為 Service Fabric 服務。
* 外部 watchdogs 從該探查 hello 資源*外*hello Service Fabric 叢集 （例如，像是 Gomez 監視服務）。

> [!NOTE]
> Hello 現成 hello 叢集會填入傳送嗨系統元件的健康情況報告。 在此閱讀更多 [使用系統健康狀態報告進行疑難排解](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)的相關資訊。 hello 使用者必須將報表傳送[健康實體](service-fabric-health-introduction.md#health-entities-and-hierarchy)，已經建立 hello 系統。
> 
> 

一次 hello 健全狀況報表的設計已取消選取，可以輕鬆地傳送健康情況報告。 您可以使用[FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) tooreport 健全狀況，如果不是 hello 叢集[安全](service-fabric-cluster-security.md)或 hello 網狀架構用戶端是否為系統管理員權限。 報告可以透過 hello API 所使用[FabricClient.HealthManager.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth)、 PowerShell 或 REST。 組態旋鈕批次報告可提升效能。

> [!NOTE]
> 回報健全狀況是同步的並顯示只有 hello 驗證工作 hello 用戶端。 hello hello 報表的事實是 hello 健全狀況的用戶端或接受 hello`Partition`或`CodePackageActivationContext`物件並不表示套用 hello 存放區中。 它會以非同步方式傳送並可能與其他報告進行批次處理。 hello hello 伺服器上處理仍然可能會失敗： hello 序號可能會過期，必須套用報表在哪個 hello hello 實體已被刪除，等等。
> 
> 

## <a name="health-client"></a>健康狀態用戶端
hello 健全狀況報表會傳送 toohello 透過內部 hello 網狀架構用戶端的健全狀況用戶端的健全狀況存放區。 hello 健全狀況的用戶端可以設定以 hello 下列設定：

* **HealthReportSendInterval**: hello hello hello 報表之間的延遲是加入的 toohello 用戶端與 hello 時間傳送 toohello 健全狀況存放區。 使用的 toobatch 到單一訊息，而不是傳送一個訊息，每個報表的報表。 hello 批次處理可改善效能。 預設值：30 秒。
* **HealthReportRetrySendInterval**: hello 間隔在哪一個 hello 健全狀況的用戶端重新傳送累積健全狀況報告 toohello 健全狀況存放區。 預設值：30 秒。
* **HealthOperationTimeout**: hello 逾時期限報告訊息傳送 toohello 健全狀況存放區。 如果訊息逾時，hello 健全狀況的用戶端重試它之前 hello 健全狀況存放區確認已處理 hello 報表。 預設值：兩分鐘。

> [!NOTE]
> 當 hello 報表會批次處理時，必須保持 hello 網狀架構用戶端運作的至少 hello HealthReportSendInterval tooensure，才會傳送它們。 Hello 網狀架構用戶端 hello 訊息就會遺失或 hello 健全狀況存放區無法將其套用 tootransient 錯誤原因，如果必須保持運作的長 toogive 它機會 tooretry。
> 
> 

hello 緩衝 hello 用戶端上會列入考量的 hello 唯一性的 hello 報表。 例如，如果特定的錯誤報告 reporting 100 會報告每秒 hello 上相同的 hello 屬性相同的實體，報表會取代 hello 最後一個版本的 hello。 最多一個這類報表存在 hello 用戶端佇列中。 如果批次處理設定，報表的 hello 數目傳送 toohello 健全狀況存放區只是每個傳送間隔。 此報表為 hello 最新加入的報表，反映 hello hello 實體最新狀態。
指定組態參數時`FabricClient`由傳遞[FabricClientSettings](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclientsettings) hello 與預期的健全狀況的相關項目值。

hello 下列範例會建立網狀架構用戶端並指定 hello 報表應該在加入時加以傳送。 在可重試的錯誤或逾時發生時，會每 40 秒重試一次。

```csharp
var clientSettings = new FabricClientSettings()
{
    HealthOperationTimeout = TimeSpan.FromSeconds(120),
    HealthReportSendInterval = TimeSpan.FromSeconds(0),
    HealthReportRetrySendInterval = TimeSpan.FromSeconds(40),
};
var fabricClient = new FabricClient(clientSettings);
```

我們建議您保持 hello 預設網狀架構用戶端設定，設定`HealthReportSendInterval`too30 秒。 此設定可確保獲得最佳效能到期 toobatching。 對於必須儘速傳送的重要報告，在 [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) API 中使用 `HealthReportSendOptions` 且 Immediate 為 `true`。 立即報表略過 hello 批次處理間隔。 請小心; 使用這個旗標我們想要 tootake hello 健全狀況的用戶端批次處理盡可能利用。 立即傳送時也很有用 hello 網狀架構用戶端正在關閉 （例如，可判定狀態無效和需要向 tooprevent 副作用 tooshut hello 程序）。 它會確保 hello 累積報告的最佳方式傳送。 一份報表加入時立即旗標，則 hello 健全狀況的用戶端批次處理自最後一個傳送 hello 累積的所有報表。

透過 PowerShell 建立連線 tooa 叢集時，可以指定相同的參數。 下列範例中的 hello 啟動連線 tooa 本機叢集：

```powershell
PS C:\> Connect-ServiceFabricCluster -HealthOperationTimeoutInSec 120 -HealthReportSendIntervalInSec 0 -HealthReportRetrySendIntervalInSec 40
True

ConnectionEndpoint   :
FabricClientSettings : {
                       ClientFriendlyName                   : PowerShell-1944858a-4c6d-465f-89c7-9021c12ac0bb
                       PartitionLocationCacheLimit          : 100000
                       PartitionLocationCacheBucketCount    : 1024
                       ServiceChangePollInterval            : 00:02:00
                       ConnectionInitializationTimeout      : 00:00:02
                       KeepAliveInterval                    : 00:00:20
                       HealthOperationTimeout               : 00:02:00
                       HealthReportSendInterval             : 00:00:00
                       HealthReportRetrySendInterval        : 00:00:40
                       NotificationGatewayConnectionTimeout : 00:00:00
                       NotificationCacheUpdateTimeout       : 00:00:00
                       }
GatewayInformation   : {
                       NodeAddress                          : localhost:19000
                       NodeId                               : 1880ec88a3187766a6da323399721f53
                       NodeInstanceId                       : 130729063464981219
                       NodeName                             : Node.1
                       }
```

同樣地 tooAPI，可以將報表傳送使用`-Immediate`切換 toobe 不論 hello 立即傳送`HealthReportSendInterval`值。

為 rest，hello 報表會傳送 toohello Service Fabric 閘道有內部的網狀架構用戶端。 依預設，此用戶端為設定的 toosend 批次處理每隔 30 秒。 您可以使用 hello 叢集組態設定變更 hello 批次間隔`HttpGatewayHealthReportSendInterval`上`HttpGateway`。 如所述，更好的選項是使用 toosend hello 報表`Immediate`，則為 true。 

> [!NOTE]
> 未授權的服務 tooensure 無法報告健全狀況 hello hello 叢集中的實體，針對設定只能從受保護的用戶端 hello 伺服器 tooaccept 要求。 hello`FabricClient`用於報表必須已啟用安全性 toobe 無法 toocommunicate 與 hello 叢集 （例如，使用 Kerberos 或憑證驗證）。 深入了解 [叢集安全性](service-fabric-cluster-security.md)。
> 
> 

## <a name="report-from-within-low-privilege-services"></a>在低權限的服務內進行報告
如果 Service Fabric 服務沒有系統管理員存取 toohello 叢集，您可以在 hello 透過目前的內容來自實體上報告健全狀況`Partition`或`CodePackageActivationContext`。

* 針對無狀態服務，使用[IStatelessServicePartition.ReportInstanceHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatelessservicepartition.reportinstancehealth) tooreport hello 目前服務執行個體上的。
* 可設定狀態服務，使用[IStatefulServicePartition.ReportReplicaHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition.reportreplicahealth) tooreport 上目前的複本。
* 使用[IServicePartition.ReportPartitionHealth](https://docs.microsoft.com/dotnet/api/system.fabric.iservicepartition.reportpartitionhealth) tooreport hello 目前磁碟分割實體上的。
* 使用[CodePackageActivationContext.ReportApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportapplicationhealth) tooreport 上目前的應用程式。
* 使用[CodePackageActivationContext.ReportDeployedApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedapplicationhealth) tooreport hello 目前節點上部署的 hello 目前應用程式上。
* 使用[CodePackageActivationContext.ReportDeployedServicePackageHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedservicepackagehealth) tooreport hello 目前節點上部署的 hello 應用程式的服務封裝上。

> [!NOTE]
> 就內部而言，hello`Partition`和 hello`CodePackageActivationContext`保存設定預設設定的健全狀況用戶端。 所述的 hello[健全狀況的用戶端](service-fabric-report-health.md#health-client)，報表會批次處理並傳送的計時器。 hello 物件應該保持運作 toohave 機會 toosend hello 報表。
> 
> 

您可以在透過 `Partition` 和 `CodePackageActivationContext` 健康情況 API 傳送報告時指定 `HealthReportSendOptions`。 如果您有必須儘速傳送的重要報表，請使用`HealthReportSendOptions` 且 Immediate 為 `true`。 立即報表略過 hello 批次處理間隔可用 hello 內部的健全狀況的用戶端。 如前所述，請小心; 使用這個旗標我們想要 tootake hello 健全狀況的用戶端批次處理盡可能利用。

## <a name="design-health-reporting"></a>設計健康狀態報告
hello 產生高品質的報表中的第一個步驟識別可能會影響 hello hello 服務健全狀況的 hello 條件。 任何條件，可協助 hello 服務或叢集中的旗標問題，當它啟動-，或甚至更好且問題發生之前-可能會儲存數十億個 （美元）。 hello 優點包括小於停機時間，較少的系統會在晚上小時所花費的調查，並修復問題，以及更高的客戶滿意度。

一旦識別出 hello 條件，監視寫入器需要出 hello 的負擔與可用性之間取得平衡最佳方式 toomonitor toofigure。 例如，考慮可使用共用上的一些暫存檔案進行複雜計算的服務。 監視無法監視 hello 共用 tooensure 有足夠空間。 它可以接聽檔案或目錄變更的通知。 如果前方的臨界值會達到，而且如果 hello 共用已滿時報告錯誤，也無法報告警告。 上一則警告，修復系統可以開始清除較舊 hello 共用上的檔案。 發生錯誤時，修復系統無法移動 hello 服務複本 tooanother 節點。 請注意如何 hello 條件的狀態詳述健全狀況方面： hello hello 可視為狀況良好 （確定） 的條件或狀況不良 （警告或錯誤） 的狀態。

一旦設定 hello 監視詳細資料之後，監視寫入器需要 toofigure 出 tooimplement hello 監視的方式。 如果 hello 條件可由 hello 服務內，hello 監視可以是本身 hello 監視服務的一部分。 例如，hello 服務程式碼可以檢查 hello 共用使用量，並每次嘗試 toowrite 檔案，然後報告。 hello 這種方法的優點是 reporting 很簡單。 必須小心 tooprevent 監視 bug hello 服務功能造成影響。

Hello 監視服務中的報告不一定選項。 Hello 服務中的監視可能不是能 toodetect hello 條件。 它沒有 hello 邏輯或資料項目 toomake hello 判斷。 hello 的監視 hello 條件的額外負荷很高。 hello 條件也可能不是特定 tooa 服務，但而影響服務之間的互動。 另一個選項是 toohave watchdogs hello 叢集中做為個別的處理序。 hello watchdogs 監視 hello 條件和報表，而不會影響 hello 主要服務，以任何方式。 例如，無法實作這些 watchdogs hello 無狀態服務的身分部署 hello 或所有節點上的相同應用程式為 hello 服務的相同節點。

有時候，hello 叢集中執行的監視也不選項可以。 如果受監視的 hello 條件 hello 可用性或 hello 服務的功能為使用者看到的樣子，，是最佳 toohave hello watchdogs hello 相同放置為 hello 使用者用戶端中。 那里，它們可以在此測試 hello 作業 hello 中相同的方式使用者呼叫它們。 例如，您可以監視居住 hello 叢集外，toohello 服務發出要求，並檢查 hello 延遲和 hello 結果的正確性。 (例如在計算機服務中，2+2 是否會在合理的時間內傳回 4？)

一旦最終處理 hello 監視詳細資料，您應該決定來源識別碼可唯一識別它。 如果多個相同的型別會住在 hello 的 watchdogs hello 叢集，它們必須不同的實體上的報表或者，如果它們報告 hello 相同的實體、 使用不同的來源識別碼或屬性。 如此一來，其報告才可並存。 hello hello 健康情況報告 屬性應擷取 hello 監視條件。 (如 hello 上述範例中，可能是 hello 屬性**ShareSize**。)如果多個報表套用 toohello 相同條件，hello 屬性應該包含一些可讓報表 toocoexist 的動態資訊。 例如，如果多個共用需要監視 toobe，hello 屬性名稱可以是**ShareSize sharename**。

> [!NOTE]
> 請勿*不*使用 hello 健康情況存放區 tookeep 狀態資訊。 只能與健全狀況相關的資訊應該報告為健康情況，為此資訊會影響 hello 健全狀況評估的實體。 hello 健全狀況存放區的設計無法做為一般用途存放區。 它會使用健全狀況評估邏輯 tooaggregate 所有資料到 hello 健全狀況狀態。 傳送的資訊 （如 reporting 健全狀況狀態為 [確定] 狀態) 的不相關的 toohealth 不會影響 hello 彙總健全狀況狀態，但它效能造成負面影響 hello hello 健全狀況存放區。
> 
> 

hello 下一個決策點所在的實體 tooreport。 大部分的 hello 時間，hello 條件 idetifies 清楚 hello 實體。 選擇最佳的可能資料粒度的 hello 實體。 如果條件，將會影響資料分割中的所有複本，報告 hello 的磁碟分割，不是在 hello 服務。 以下為需要仔細考量的極端例子。 如果 hello 條件影響實體，例如複本，但 hello desire 是 toohave hello 條件標示為多個複本生命 hello 持續時間應 hello 磁碟分割上。 否則，請刪除 hello 複本時，hello 健全狀況存放區就會清除所有其報表。 監視程式撰寫者必須思考 hello 存留期 hello 實體與 hello 報表。 報告需從存放區中清除的時間點必須清楚說明 (例如，當實體上回報的錯誤不再適用時)。

讓我們看看將放在一起所述的 hello 點的範例。 假設有一個由主要具狀態保存服務和所有節點上部署的次要無狀態服務所組成的 Service Fabric 應用程式 (每種工作類型有一個次要服務類型)。 hello 主機具有包含次要資料庫所執行的命令 toobe 處理佇列。 hello 的次要複本執行 hello 連入要求，並傳送後認可信號。 無法監視的一個條件是 hello hello 主要處理佇列長度。 如果 hello 主要佇列長度達到臨界值時，會報告警告。 hello 警告表示 hello 的次要複本無法處理 hello 負載。 如果 hello 佇列到達 hello 最大長度，並卸除命令，則會報告錯誤，為 hello 服務將無法復原。 hello 報表可以在 hello 屬性**QueueStatus**。 hello 監視居住 hello 服務內，它會定期傳送嗨主控主要複本上。 hello 時間 toolive 兩分鐘，而且它會傳送定期每隔 30 秒。 如果主要 hello 當機時，hello 報表會自動清除從存放區。 如果 hello 服務複本已啟動，但它將會鎖死或發生其他問題，hello 報表到期 hello health store 中。 在此情況下，會在錯誤發生時加以評估 hello 實體。

其他可監視的條件為工作執行時間。 hello master 散發工作 toohello 次要根據 hello 工作類型。 根據 hello 設計 hello master 無法輪詢 hello 次要複本，以工作狀態。 它也無法等候次要複本 toosend 回復通知訊號，當他們完成時。 在 hello 第二個情況下，必須小心 toodetect 次要無效或訊息的遺失的情況。 其中一個選項是為 hello 主要 toosend ping 要求 toohello 相同次要，將其狀態傳送回。 如果仍不收到任何狀態，hello master 將其視為失敗，和 hello 工作會重新排定。 此行為是假設 hello 工作是等冪。

hello 監視條件可以轉譯為警告，如果 hello 工作不是在一段時間 (**t1**，例如 10 分鐘)。 如果 hello 工作未完成的時間 (**t2**，例如 20 分鐘)，監視的 hello 條件可以轉譯為錯誤。 此報告可以多種方式完成：

* 定期 hello 主控主要複本會報告於本身。 您可以 hello 佇列中有一個屬性的所有暫止的工作。 如果至少一個工作所花費的時間，hello 狀態報告 hello 屬性**PendingTasks**警告或錯誤，適當地。 如果沒有暫止的工作或所有工作都開始執行，hello 報告狀態為 [確定]。 hello 工作是永續性。 如果主要 hello 關閉時，最近更新的 hello 主要可以正確繼續 tooreport。
* （在 hello 雲端或外部） 的另一個監視處理序會檢查 hello 工作 （從外部，根據預期的 hello 工作結果） toosee 如果，便會完成。 如果它們不會採用 hello 臨界值，報表會傳送 hello 主要服務上。 報表也會傳送包含 hello 工作識別碼，例如每個工作上**PendingTask + taskId**。 只有在狀況不良的狀態才需傳送報告。 設定時間 toolive tooa 幾分鐘的時間，並將標示 hello 報表 toobe 移除到期 tooensure 清除。
* 它會將長度超過預期 toorun 它時，就會回報 hello 次要正在執行工作。 它會報告 hello hello 屬性上的服務執行個體上**PendingTasks**。 hello 報告指出有問題，hello 服務執行個體，但它不擷取 hello 情況 hello 執行個體中斷的位置。 hello 報表會再清除。 它無法報告 hello 次要服務上。 如果次要 hello 完成 hello 工作時，hello 次要執行個體就會清除 hello hello 存放區中的報表。 hello 報表不會擷取 hello 收條訊息就會遺失，和 hello 工作未完成從 hello 為主版頁面的觀點來看的 hello 情況。

Hello 報告在 hello 上面所述的情況下完成，不過 hello 報表中所擷取應用程式健全狀況評估健全狀況時。

## <a name="report-periodically-vs-on-transition"></a>定期報告與轉換時報告
藉由使用 hello 健全狀況報表模型，watchdogs 可以定期或受制於傳送報告。 hello 監視報告的方式被建議定期，因為 hello 的程式碼更簡單且較不容易出錯 tooerrors。 hello watchdogs 必須盡可能 toobe 越簡單越可能 tooavoid bug 觸發回報不正確。 不正確的狀況不良  報告將會影響健康狀態評估以及需依據健康狀態的情況，包括升級。 不正確*狀況良好*報表隱藏 hello 叢集中不想要使用的問題。

如需定期的報表，hello 監視可實作以計時器。 計時器回呼，在 hello 監視可檢查 hello 狀態，並傳送嗨目前狀態為基礎的報表。 沒有任何需要 toosee 報表先前傳送或任何方面傳訊的最佳化。 hello 健全狀況的用戶端已批次處理邏輯 toohelp 與效能。 Hello 健全狀況的用戶端就會保持運作，而在重試內部 hello 報表已認可 hello 健全狀況存放區或 hello 監視會產生較新的報告，以 hello 之前相同的實體、 屬性和來源。

轉換時的回報需要注意狀態處理。 hello 監視會監視某些條件，並回報僅 hello 條件變更時。 hello upside 這種方法是較少的報表所需。 hello 缺點是的 hello 看門狗的 hello 邏輯相當複雜。 hello 監視必須維護 hello 條件或 hello 報表，以便它們可檢查的 toodetermine 狀態變更。 在容錯移轉時，必須小心新增，但尚未傳送 toohello 健全狀況存放區的報表。 hello 序號必須不斷增加。 如果沒有，hello 報表將會拒絕為過時。 在 hello 造成資料遺失其中少數的情況，則可能需要 hello hello 報告狀態與 hello hello 健全狀況的儲存區狀態之間的同步處理。

透過 `Partition` 或 `CodePackageActivationContext` 進行轉換報告，對服務自行報告而言較為合理。 當 hello 本機物件 (複本或部署的服務封裝 / 部署應用程式) 會移除其所有的報表也會移除。 此自動清除會放寬 hello 需要報告和健全狀況存放區之間的同步處理。 如果 hello 報表是針對父磁碟分割或父應用程式，必須小心 hello health store 中容錯移轉 tooavoid 過時報表上。 必須將邏輯加入 toomaintain hello 正確的狀態並清除 hello 報表從存放區不需要再時。

## <a name="implement-health-reporting"></a>實作健康狀態報告
一旦 hello 實體和報表的詳細資料清除，傳送健康情況報告可以透過 hello API、 PowerShell 或 REST。

### <a name="api"></a>API
tooreport 透過 hello API，您需要 toocreate 他們想 tooreport 的健全狀況報表特定 toohello 實體類型。 給予 hello 報表 tooa 健全狀況的用戶端。 或者，建立健全狀況資訊，並將它傳遞 toocorrect 報告方法上`Partition`或`CodePackageActivationContext`tooreport 上目前的實體。

hello 下列範例示範定期監視 hello 叢集內的報告。 hello 監視會檢查是否可以外部資源的存取節點內。 hello 資源需要 hello 應用程式中的服務資訊清單。 如果 hello 資源無法使用，hello hello 應用程式的其他服務可以仍正常運作。 因此，hello 報表會傳送 hello 部署服務套件實體上每隔 30 秒。

```csharp
private static Uri ApplicationName = new Uri("fabric:/WordCount");
private static string ServiceManifestName = "WordCount.Service";
private static string NodeName = FabricRuntime.GetNodeContext().NodeName;
private static Timer ReportTimer = new Timer(new TimerCallback(SendReport), null, 30 * 1000, 30 * 1000);
private static FabricClient Client = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });

public static void SendReport(object obj)
{
    // Test whether hello resource can be accessed from hello node
    HealthState healthState = this.TestConnectivityToExternalResource();

    // Send report on deployed service package, as hello connectivity is needed by hello specific service manifest
    // and can be different on different nodes
    var deployedServicePackageHealthReport = new DeployedServicePackageHealthReport(
        ApplicationName,
        ServiceManifestName,
        NodeName,
        new HealthInformation("ExternalSourceWatcher", "Connectivity", healthState));

    // TODO: handle exception. Code omitted for snippet brevity.
    // Possible exceptions: FabricException with error codes
    // FabricHealthStaleReport (non-retryable, hello report is already queued on hello health client),
    // FabricHealthMaxReportsReached (retryable; user should retry with exponential delay until hello report is accepted).
    Client.HealthManager.ReportHealth(deployedServicePackageHealthReport);
}
```

### <a name="powershell"></a>PowerShell
使用 **Send-ServiceFabric*EntityType*HealthReport** 傳送健康狀態報告。

hello 下列範例示範定期報告 CPU 節點上的值。 每隔 30 秒，應該傳送 hello 回報，而且必須 toolive 兩分鐘的時間。 如果過期，hello reporter 會有問題，因此 hello 節點會在錯誤發生時評估。 Hello CPU 臨界值時，hello 報表就會有警告的健全狀況狀態。 當 hello CPU 保持 hello 設定時間已超過臨界值時，它會回報為錯誤。 否則，hello reporter 傳送健全狀態為 [確定]。

```powershell
PS C:\> Send-ServiceFabricNodeHealthReport -NodeName Node.1 -HealthState Warning -SourceId PowershellWatcher -HealthProperty CPU -Description "CPU is above 80% threshold" -TimeToLiveSec 120

PS C:\> Get-ServiceFabricNodeHealth -NodeName Node.1
NodeName              : Node.1
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='CPU', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 5
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : CPU
                        HealthState           : Warning
                        SequenceNumber        : 130741236814913394
                        SentAt                : 4/21/2015 9:01:21 PM
                        ReceivedAt            : 4/21/2015 9:01:21 PM
                        TTL                   : 00:02:00
                        Description           : CPU is above 80% threshold
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:01:21 PM
```

hello 下列範例會報告暫時性警告複本。 它會先取得 hello 分割區識別碼，並接著 hello 它感興趣的 hello 服務複本識別碼。 然後將傳送來自報表**PowershellWatcher** hello 屬性**ResourceDependency**。 hello 報表感興趣的兩分鐘，並自動移除從 hello 存放區。

```powershell
PS C:\> $partitionId = (Get-ServiceFabricPartition -ServiceName fabric:/WordCount/WordCount.Service).PartitionId

PS C:\> $replicaId = (Get-ServiceFabricReplica -PartitionId $partitionId | where {$_.ReplicaRole -eq "Primary"}).ReplicaId

PS C:\> Send-ServiceFabricReplicaHealthReport -PartitionId $partitionId -ReplicaId $replicaId -HealthState Warning -SourceId PowershellWatcher -HealthProperty ResourceDependency -Description "hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes." -TimeToLiveSec 120 -RemoveWhenExpired

PS C:\> Get-ServiceFabricReplicaHealth  -PartitionId $partitionId -ReplicaOrInstanceId $replicaId


PartitionId           : 8f82daff-eb68-4fd9-b631-7a37629e08c0
ReplicaId             : 130740415594605869
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='ResourceDependency', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130740768777734943
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : ResourceDependency
                        HealthState           : Warning
                        SequenceNumber        : 130741243777723555
                        SentAt                : 4/21/2015 9:12:57 PM
                        ReceivedAt            : 4/21/2015 9:12:57 PM
                        TTL                   : 00:02:00
                        Description           : hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:12:32 PM
```

### <a name="rest"></a>REST
傳送與 POST 要求到 toohello 預期實體和 hello 主體 hello 健全狀況報表描述中有使用 REST 的健康情況報告。 例如，請參閱如何 toosend REST[叢集健全狀況報表](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-cluster)或[服務健康情況報告](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)。 支援所有實體。

## <a name="next-steps"></a>後續步驟
根據 hello 健全狀況資料，服務寫入器和叢集/應用程式系統管理員可以將方式 tooconsume hello 資訊。 比方說，他們可以設定在引發中斷之前，根據健全狀況狀態 toocatch 嚴重問題的警示。 系統管理員也可以設定修復系統 toofix 問題自動。

[簡介 tooService 網狀架構健全狀況監視](service-fabric-health-introduction.md)

[檢視 Service Fabric 健康狀態報告](service-fabric-view-entities-aggregated-health.md)

[Tooreport 並檢查服務健全狀況](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[使用系統健康狀態報告進行疑難排解](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[在本機上監視及診斷服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Service Fabric 應用程式升級](service-fabric-application-upgrade.md)


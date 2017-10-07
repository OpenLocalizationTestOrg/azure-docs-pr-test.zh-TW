---
title: "在多租用戶 SaaS 應用程式中的許多 Azure SQL 資料庫的 aaaMonitor 效能 |Microsoft 文件"
description: "監視和管理的資料庫和 hello Azure SQL Database Wingtip SaaS 應用程式集區效能"
keywords: SQL Database Azure
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: f0d7ba456c485b7de249a56abac3cf4be3857285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-of-hello-wingtip-saas-application"></a>監視效能的 hello Wingtip SaaS 應用程式

本教學課程會探索 SaaS 應用程式中使用的數個關鍵效能管理案例。 使用負載產生器 toosimulate 活動跨越多個租用戶的所有資料庫，hello 內建的監視和警示功能的 SQL Database 和彈性集區會示範。

hello Wingtip SaaS 應用程式會使用單一租用戶資料模型，其中每個地點 （租用戶） 都有各自的資料庫。 許多 SaaS 應用程式，例如 hello 預期租用戶工作負載模式是無法預期且斷斷續續。 換句話說，票證銷售可能會在任何時間發生。 這個一般資料庫使用模式，租用戶資料庫部署至彈性資料庫集區的 tootake 優點。 彈性集區最佳化解決方案的 hello 成本跨多個資料庫共用資源。 這種模式，它為重要 toomonitor 資料庫，而載入的集區資源使用量 tooensure 合理的平衡跨集區。 您也需要 tooensure，個別的資料庫擁有足夠的資源和集區不會叫用其[eDTU](sql-database-what-is-a-dtu.md)限制。 本教學課程瀏覽方式 toomonitor 和管理資料庫和集區，以及如何在工作負載中的回應 toovariations tootake 矯正措施。

在本教學課程中，您了解如何：

> [!div class="checklist"]

> * Hello 租用戶資料庫上的使用量，以模擬的執行提供的負載產生器
> * 監視 hello 租用戶資料庫，如同這些回應 toohello 增加負載
> * 向上擴充 hello 回應 toohello 增加的資料庫負載中的彈性集區
> * 佈建第二個的彈性集區 tooload 平衡資料庫活動


toocomplete 完成本教學課程，請確定 hello 下列必要條件：

* hello Wingtip SaaS 應用程式部署。 toodeploy 在五分鐘內，請參閱[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)
* 已安裝 Azure PowerShell。 如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toosaas-performance-management-patterns"></a>簡介 tooSaaS 效能管理模式

資料庫效能管理包含編譯和分析效能資料，然後對回應 toothis 資料，藉由調整參數 toomaintain 應用程式接受的回應時間。 當裝載多個租用戶，彈性資料庫集區會符合成本效益的方式 tooprovide 和管理群組的資料庫無法預期的工作負載的資源。 使用特定工作負載模式，最少為兩個 S3 資料庫可以受惠於在集區中管理。

![媒體](./media/sql-database-saas-tutorial-performance-monitoring/app-diagram.png)

集區和集區中的 hello 資料庫應受監視的 tooensure 就會維持在可接受的效能範圍內。 微調 hello 集區組態 toomeet hello hello 彙總工作負載的需求 hello 的集區 edtu 數目皆適用於 hello 的所有資料庫的整體工作負載。 調整 hello 每個資料庫最小值和每個資料庫最大的 eDTU 值 tooappropriate 值的特定應用程式的需求。

### <a name="performance-management-strategies"></a>效能管理策略

* tooavoid 具有 toomanually 監視效能，是最有效率的太**設定警示，在資料庫或集區偏離超出正常範圍時觸發**。
* 集區，hello 彙總效能層級的 toorespond tooshort 詞彙波動 hello**集區 eDTU 層級可以向上或向下調整**。 如果此波動發生於定期或依照可預測的基礎，**調整 hello 集區可以是排程的 toooccur 自動**。 例如，當您知道夜間或者週末期間工作負載較輕時，就可以相應減少。
* toorespond toolonger 詞彙波動或變更 hello 的資料庫，數目**個別資料庫可能會移至其他集區**。
* toorespond tooshort 詞彙會增加在*個別*資料庫載入**可以超出集區和個別的效能等級指派給個別資料庫**。 一旦 hello 負載降低，hello 資料庫可以則傳回 toohello 集區。 當這事先已知道時，資料庫可以移動聯合國 tooensure hello 資料庫永遠都有其所需的 hello 資源和 tooavoid 影響 hello 集區中的其他資料庫上。 如果可預測，例如遇到的常見事件的票證銷售晚法院這項需求，此管理行為可以整合到 hello 應用程式。

hello [Azure 入口網站](https://portal.azure.com)提供內建的監視和警示最多資源。 針對 SQL Database，可使用資料庫和集區監視與警示功能。 此內建監視和警示是特定資源，因此它是方便 toouse 小的數字的資源，但不是很方便使用許多資源時。

在您處理許多資源的大量案例中，可以使用 [Log Analytics (OMS)](sql-database-saas-tutorial-log-analytics.md)。 這是個別的 Azure 服務，可針對發出的診斷記錄和記錄分析工作區中收集的遙測提供分析。 記錄分析可以從許多服務收集遙測和是使用的 tooquery，而且設定警示。

## <a name="get-hello-wingtip-application-source-code-and-scripts"></a>取得 hello Wingtip 應用程式原始碼和指令碼

hello Wingtip SaaS 指令碼和應用程式的原始程式碼中可用 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。 [步驟 toodownload hello Wingtip SaaS 指令碼](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。

## <a name="provision-additional-tenants"></a>佈建其他租用戶

雖然可以符合成本效益與兩個 S3 資料庫集區，而 hello 位於 hello 平均效果變得更符合成本效益的 hello 集區 hello 的多個資料庫。 為了深入了解效能監視與管理大規模運作的方式，本教學課程要求您至少部署 20 個資料庫。

如果在先前的教學課程已佈建了租用戶的批次，請略過 toohello[所有租用戶資料庫上的模擬使用量](#simulate-usage-on-all-tenant-databases)> 一節。

1. 開啟...\\學習模組\\效能監視與管理\\*示範 PerformanceMonitoringAndManagement.ps1*在 hello *PowerShell ISE*。 保持此指令碼開啟，因為您將在本教學課程期間執行數個案例。
1. 設定 **$DemoScenario** = **1**，**佈建批次的租用戶**
1. 按**F5** toorun hello 指令碼。

hello 指令碼將在五分鐘內部署 17 的租用戶。

hello*新增 TenantBatch*指令碼會使用巢狀或連結一[資源管理員](../azure-resource-manager/index.md)範本，建立批次的租用戶，其預設值會複製 hello 資料庫**basetenantdb** hello 類別目錄伺服器 toocreate hello 新租用戶的資料庫上，然後註冊這些 hello 類別目錄中，最後將其初始化 hello 租用戶名稱和地點類型。 這是與 hello 應用程式會提供給新的租用戶的 hello 方式一致。 所做過任何變更*basetenantdb*是套用的 tooany 佈建之後的新租用戶。 請參閱 hello[結構描述管理教學課程](sql-database-saas-tutorial-schema-management.md)toosee toomake 結構描述如何變更太*現有*租用戶資料庫 (包括 hello *basetenantdb*資料庫)。

## <a name="simulate-usage-on-all-tenant-databases"></a>模擬所有租用戶資料庫的使用情形

hello*示範 PerformanceMonitoringAndManagement.ps1*指令碼所提供的模擬所有租用戶資料庫上執行的工作負載。 hello 負載會產生使用其中一種 hello 可用的負載案例：

| 示範 | 案例 |
|:--|:--|
| 2 | 產生一般強度負載 (大約 40 個 DTU) |
| 3 | 每個資料庫產生時間更長、更頻繁高載的負載|
| 4 | 每個資料庫產生具有更高 DTU 高載的負載 (大約 80 個 DTU)|
| 5 | 在單一租用戶上產生一般負載加上高負載 (大約 95 個 DTU)|
| 6 | 產生跨多個集區的不對稱負載|

hello 負載產生器適用於*綜合*僅 CPU 負載 tooevery 租用戶資料庫。 hello 產生器啟動每一個呼叫的預存程序會定期產生 hello 負載的租用戶資料庫工作。 hello 負載層級 （Edtu)、 持續時間和間隔會改變所有資料庫，模擬預期租用戶活動。

1. 開啟...\\學習模組\\效能監視與管理\\*示範 PerformanceMonitoringAndManagement.ps1*在 hello *PowerShell ISE*。 保持此指令碼開啟，因為您將在本教學課程期間執行數個案例。
1. 設定 **$DemoScenario** = **2**，*產生一般強度負載*。
1. 按**F5** tooapply 負載 tooall 租用戶資料庫。

Wingtip 是 SaaS 應用程式，並 hello 真實世界負載 SaaS 應用程式通常是偶發和無法預期。 toosimulate 這 hello 負載產生器會產生隨機的負載分散到所有租用戶。 Hello 負載模式 tooemerge，因此執行 hello 負載產生器 3-5 分鐘，再嘗試 toomonitor hello 下列各節中的 hello 負載被需要幾分鐘的時間。

> [!IMPORTANT]
> hello 負載產生器以一系列的工作執行，本機 PowerShell 工作階段中。 保留 hello*示範 PerformanceMonitoringAndManagement.ps1*  索引標籤開啟 ！ 如果您關閉 [hello] 索引標籤，或暫止您的電腦時，就會停止 hello 負載產生器。 hello 負載產生器會保留在*作業叫用*狀態就會產生新的租用戶 hello 產生器啟動之後，會佈建的負載。 使用*CTRL-C* toostop 叫用新工作，並結束 hello 指令碼。 hello 負載產生器會繼續 toorun，但只能在現有的租用戶。

## <a name="monitor-resource-usage-using-hello-azure-portal"></a>使用 hello Azure 入口網站監視資源使用狀況

toomonitor hello 分派 hello 結果載入套用，開啟包含 hello 租用戶資料庫 hello 入口 toohello 集區：

1. 開啟 hello [Azure 入口網站](https://portal.azure.com)並瀏覽 toohello *tenants1-&lt;使用者&gt;*伺服器。
1. 向下捲動並找出彈性集區，然後按一下 [Pool1]。 此集區包含所有 hello 租用戶資料庫建立為止。

觀察 hello**彈性集區監視**和**彈性資料庫監視**圖表。

hello 集區的資源使用率是 hello hello 集區中所有資料庫的彙總資料庫使用量。 hello 資料庫圖表可顯示 hello 五個最熱的資料庫：

![](./media/sql-database-saas-tutorial-performance-monitoring/pool1.png)

由於超過 hello 集區中沒有其他資料庫 hello 前五個，hello 集區使用量會顯示不會反映在 hello 前五個資料庫圖表中的活動。 如需其他詳細資料，請按一下 [資料庫資源使用量]：

![](./media/sql-database-saas-tutorial-performance-monitoring/database-utilization.png)


## <a name="set-performance-alerts-on-hello-pool"></a>在 hello 集區上設定效能警示

在觸發程序的 hello 集區上設定警示\>75%使用率，如下所示：

1. 開啟*Pool1* (hello 上*tenants1-\<使用者\>*伺服器) 中 hello [Azure 入口網站](https://portal.azure.com)。
1. 按一下 警示規則，然後按一下+ 加入警示：

   ![加入警示](media/sql-database-saas-tutorial-performance-monitoring/add-alert.png)

1. 提供名稱，例如「高 DTU」，
1. 設定下列值的 hello:
   * **度量 = eDTU 百分比**
   * **條件 = 大於**。
   * **閾值 = 75**。
   * **週期 = hello 透過過去 30 分鐘內**。
1. 新增電子郵件地址 toohello*其他的系統管理員 email(s)*方塊，然後按一下**確定**。

   ![設定警示](media/sql-database-saas-tutorial-performance-monitoring/alert-rule.png)


## <a name="scale-up-a-busy-pool"></a>相應增加忙碌的集區

如果 hello 彙總負載層級增加集區 toohello 點，它 maxes 出 hello 集區，而且達到 100%的 eDTU 使用量，然後個別的資料庫效能受到影響，可能會拖慢 hello 集區中的所有資料庫的查詢回應時間。

**簡短詞彙**，請考慮向上擴充 hello 集區 tooprovide 其他資源，或從 hello 集區中移除資料庫 (將其移 tooother 集區，或移出 hello 集區 tooa 獨立服務層)。

**長期**，請考慮最佳化查詢或索引的使用方式 tooimprove 資料庫效能。 根據 hello 應用程式的敏感度 tooperformance 之前會發出其最佳作法 tooscale 向上的集區達到 100%的 eDTU 使用量。 使用警示的 toowarn 您事先。

您可以增加 hello 產生器所產生的 hello 負載模擬忙碌的集區。 造成 hello 資料庫 tooburst 更頻繁，以及較長，增加 hello 彙總負載 hello 集區上而不需要變更 hello 個別資料庫的 hello 需求。 輕鬆地進行向上擴充 hello 集區，在 hello 入口網站或從 PowerShell。 此練習使用 hello 入口網站。

1. 設定*$DemoScenario* = **3**，_產生負載，每個資料庫的長、 更頻繁暴增_hello 彙總負載 tooincrease hello 強度hello 集區，而不會變更每個資料庫所需的 hello 尖峰負載。
1. 按**F5** tooapply 負載 tooall 租用戶資料庫。

1. 跳過**Pool1** hello Azure 入口網站中。

監視 hello 增加集區 eDTU 使用量 hello 上方圖表上。 花幾分鐘，讓 hello 新高負載 tookick 中，您應該會快速看到 hello 集區啟動 toohit 最大使用量，但 hello 負載 steadies 變成 hello 新模式，因為它快速多載 hello 集區。

1. tooscale 向上 hello 集區中，按一下**設定集區**頂端的 hello hello **Pool1**頁面。
1. 調整 hello**集區 eDTU**太設定**100**。 變更 hello 集區 eDTU 不會變更 hello 每個資料庫設定 （這仍然是 50 eDTU 每個資料庫最大）。 您可以看到 hello 每個資料庫設定右側 hello hello**設定集區**頁面。
1. 按一下**儲存**toosubmit hello 要求 tooscale hello 集區。

請返回太**Pool1** > **概觀**tooview hello 監控圖表。 監視 hello 效果提供更多資源 hello 集區 （雖然幾個資料庫以及隨機的負載它不一定是簡單 toosee 做出段時間執行之前）。 時想要在 hello 圖表都帶有記住 100%上 hello 上方圖表現在代表 100 Edtu 時 hello 上較低的圖表 100%仍 50 Edtu hello 為每個資料庫最大值, 仍然是 50 的 Edtu。

資料庫會保持 online 和 hello 程序中完全可供使用。 Hello 在最後一刻才為每個資料庫都準備好 toobe hello 新集區 eDTU，以啟用任何使用中連接都會中斷。 應用程式程式碼應該一律寫入卸除 tooretry 連線，因此會重新 toohello hello 向上調整集區中的資料庫。

## <a name="load-balance-between-pools"></a>平衡集區之間的負載

因為替代 tooscaling 向上 hello 集區，建立第二個集區，並將資料庫移到其中 toobalance hello 載入 hello 之間兩個集區。 這個 hello 新集區必須在建立的 toodo 先 hello hello 與相同的伺服器。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，開啟 hello **tenants1-&lt;使用者&gt;**伺服器。
1. 按一下**+ 新集區**toocreate hello 目前伺服器上的集區。
1. 在 hello**彈性資料庫集區**範本：

    1. 設定**名稱**太*Pool2*。
    1. 保留 hello 定價層為**標準的集區**。
    1. 按一下 [設定集區]，
    1. 設定**集區 eDTU**太*50 eDTU*。
    1. 按一下**新增資料庫**toosee 太可加入 hello 伺服器上的資料庫清單*Pool2*。
    1. 選取所有 10 個資料庫 toomove 這些 toohello 新的集區，然後再按一下**選取**。 如果您已經執行 hello 負載產生器，hello 服務已經知道您的效能設定檔需要比 hello 預設 50 eDTU 大小較大的集區，並建議開頭為 100 的 eDTU 設定。

    ![建議](media/sql-database-saas-tutorial-performance-monitoring/configure-pool.png)

    1. 本教學課程，讓 hello 預設在 edtu 數 （50），然後按一下**選取**一次。
    1. 選取**確定**toocreate hello 新集區和 toomove hello 選取到其中的資料庫。

建立 hello 集區，而且移動 hello 資料庫需要幾分鐘。 移動它們之前 hello 非常最後一刻保持線上，而且完全可存取資料庫，因為此時任何開啟連接會關閉。 只要您有一些重試邏輯，用戶端會接著連接 toohello hello 新集區中的資料庫。

瀏覽過**Pool2** (hello 上*tenants1*伺服器) tooopen hello 集區，並監視其效能。 如果您沒有看到它，請等候佈建的新集區 toocomplete hello。

您現在可看到 Pool1 上的資源使用量已下降，而 Pool2 目前維持同樣的負載。

## <a name="manage-performance-of-a-single-database"></a>管理單一資料庫的效能

如果集區中的單一資料庫遇到持續高負載，則根據 hello 集區設定，它可能傾向 toodominate hello 集區中的 hello 資源，並會影響其他資料庫。 若是 hello 活動可能 toocontinue 段時間，hello 資料庫可以暫時移出 hello 集區。 這可讓 hello 資料庫 toohave hello 額外的資源，需要此項目，並隔離 hello 從其他資料庫。

這個練習會模擬 Contoso 搭配 Hall 當票證上銷售額熱門搭配遭遇高負載的 hello 的效果。

1. 開啟 hello...\\*示範 PerformanceMonitoringAndManagement.ps1*指令碼。
1. 設定 **$DemoScenario = 5，在單一租用戶上產生一般負載加上高負載 (大約 95 個 DTU)**。
1. 設定 **$SingleTenantDatabaseName = contosoconcerthall**
1. 執行指令碼 hello **F5**。


1. 在 hello [Azure 入口網站](https://portal.azure.com)開啟**Pool1**。
1. 檢查 hello**彈性集區監視**圖表，並尋找 hello 增加集區 eDTU 使用量。 一兩分鐘之後, hello 更高的負載應該啟動，tookick，而且您應該很快會看見 hello 集區達到 100%的使用率。
1. 檢查 hello**彈性資料庫監視**顯示過去一小時 hello 顯示 hello 最熱的資料庫。 hello *contosoconcerthall*資料庫應該很快就會顯示為其中一個 hello 五個最熱的資料庫。
1. **按一下 hello 彈性資料庫監視****圖表**開幕 hello 和**資料庫資源使用量**其中您可以監視任何 hello 資料庫頁面。 這可讓您找出 hello 顯示 hello *contosoconcerthall*資料庫。
1. 從資料庫 hello 清單，按一下  **contosoconcerthall**。
1. 按一下**定價層 （小數位數的 Dtu）** tooopen hello**設定效能**頁面，您可以設定 hello 資料庫獨立的效能層級。
1. 按一下 hello**標準**hello 標準層中的 tooopen hello 調整選項索引標籤上。
1. 投影片 hello **DTU 滑桿**tooright tooselect **100** Dtu。 請注意，這會對應 toohello 服務目標， **S3**。
1. 按一下**套用**toomove hello hello 集區之外的資料庫，並將其*標準 S3*資料庫。
1. 調整一旦完成，hello contosoconcerthall 資料庫上的監視 hello 生效且 Pool1 在 hello 彈性集區和資料庫刀鋒視窗上。

一旦 hello hello contosoconcerthall 資料庫上的高負載 subsides 您應該立即將其傳回 toohello 集區 tooreduce 它的成本。 如果不清楚時，會發生您可以設定警示 hello 資料庫上，將會觸發其 DTU 使用量低於 hello 每個資料庫時，max hello 集區上。 練習 5 中說明如何將資料庫移入集區。

## <a name="other-performance-management-patterns"></a>其他效能管理模式

**先佔式調整**在 hello 練習上述您探索如何 tooscale 隔離的資料庫，您就知道哪些資料庫 toolook，如。 如果 Contoso 搭配 Hall hello 管理具有通知的 hello 即將發生的票證銷售量 Wingtips，hello 資料庫可能已移出 hello 集區預先。 否則，它可能必須在 hello 集區或 hello 資料庫 toospot 警示發生什麼。 您不希望從 hello 有關此 toolearn hello 抱怨的效能降低的集區中的其他租用戶。 而且，如果 hello 租用戶可以預測需要額外的資源，您可以設定 hello 集區之外的 Azure 自動化 runbook toomove hello 資料庫並再重新上定義的排程時間長度。

**調整租用戶自助**因為調整是輕鬆地透過 hello 管理 API 呼叫的工作，輕鬆地建置 hello 能力 tooscale 租用戶資料庫到您的租用戶面向應用程式，並提供做為 SaaS 服務的功能。 例如，讓租用戶 self-administer 可能是直接連結向上和向下調整 tootheir 計費 ！

**排程 toomatch 習慣上向上及向下調整集區**

其中彙總租用戶的使用方式會遵循可預測的使用模式，您可以依排程向上和向下使用 Azure 自動化 tooscale 集區。 例如，當您知道資源需求會下降時，在工作日下午 6 點後相應減少集區，而在上午 6 點之前重新相應增加。



## <a name="next-steps"></a>後續步驟

在本教學課程中，您了解如何：

> [!div class="checklist"]
> * Hello 租用戶資料庫上的使用量，以模擬的執行提供的負載產生器
> * 監視 hello 租用戶資料庫，如同這些回應 toohello 增加負載
> * 向上擴充 hello 回應 toohello 增加的資料庫負載中的彈性集區
> * 佈建第二個彈性集區 tooload 平衡 hello 資料庫活動

[還原單一租用戶教學課程](sql-database-saas-tutorial-restore-single-tenant.md)


## <a name="additional-resources"></a>其他資源

* 其他[hello Wingtip SaaS 應用程式部署為基礎的教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [SQL 彈性集區](sql-database-elastic-pool.md)
* [Azure 自動化](../automation/automation-intro.md)
* [Log Analytics](sql-database-saas-tutorial-log-analytics.md) - 設定及使用 Log Analytics 教學課程

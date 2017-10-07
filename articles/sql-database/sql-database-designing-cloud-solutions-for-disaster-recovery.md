---
title: "使用 Azure SQL Database 的 aaaDesign 高可用性服務 |Microsoft 文件"
description: "了解使用 Azure SQL Database 對高可用性服務的應用程式設計。"
keywords: "cloud disaster recovery,disaster recovery solutions,app data backup,geo-replication,business continuity planning,雲端災害復原,災害復原方案,應用程式資料備份,異地複寫,商務持續性計劃"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: e8a346ac-dd08-41e7-9685-46cebca04582
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 04/21/2017
ms.author: sashan
ms.openlocfilehash: 815f754ba7014cd8a1108a2d84c2a8f71d7030a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-services-using-azure-sql-database"></a>使用 Azure SQL Database 設計高可用性服務

建置和部署 Azure SQL Database 上的高可用性服務，當您使用[容錯移轉群組和作用中地理複寫](sql-database-geo-replication-overview.md)tooprovide 恢復 tooregional 失敗及嚴重的中斷，並啟用快速復原toohello 次要資料庫。 本文著重於常見的應用程式模式，並討論 hello 優點和缺點 hello 應用程式部署需求，您的目標，hello 服務等級協定根據每個選項的流量延遲和成本。 如需主動式異地複寫與彈性集區的相關資訊，請參閱[彈性集區災害復原策略](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)。

## <a name="design-pattern-1-active-passive-deployment-for-cloud-disaster-recovery-with-a-co-located-database"></a>設計模式 1：雲端災害復原的主動-被動部署，使用共置資料庫
這個選項最適合用於應用程式具有下列特性的 hello:

* 單一 Azure 區域中的作用中執行個體
* 讀寫 (RW) 存取 toodata 強式相依性
* 跨地區 hello web 應用程式與資料庫之間連線 hello 不接受到期 toolatency 和流量成本    

在此情況下，hello 應用程式的部署拓撲最適合處理地區的災害，當所有應用程式元件會受到影響，因此需要 toofailover 做為一個單位。 如需地理備援，hello 應用程式邏輯和 hello 資料庫複寫的 tooanother 區域但不是用於 hello 在 hello 正常情況下的應用程式工作負載。 hello 次要區域中的 hello 應用程式應該設定的 toouse SQL 連接字串 toohello 次要資料庫。 流量管理員設定 toouse[容錯移轉路由方法](../traffic-manager/traffic-manager-configure-failover-routing-method.md)。  

> [!NOTE]
> 這整篇文章使用 [Azure 流量管理員](../traffic-manager/traffic-manager-overview.md)僅供說明用途。 您可以使用任何支援容錯移轉路由方法的負載平衡方案。    
>

hello 下列圖表顯示前中斷此設定。

![SQL Database 異地複寫組態。 雲端災害復原。](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-1.png)

發生中斷後 hello 主要區域中，hello SQL Database 服務會偵測該 hello 主要資料庫無法存取，因此觸發根據的 hello 自動容錯移轉原則 hello 參數是容錯移轉的 toohello 次要資料庫。 根據您應用程式的 SLA，您可以決定 tooconfigure 的寬限期內之間 hello 偵測 hello 中斷與本身 hello 容錯移轉。 設定寬限期內，可降低資料遺失 toohello 案例其中 hello 中斷是重大，而無法快速還原 hello 區域中的可用性 hello 風險。 如果 hello 端點容錯移轉會起始 hello 流量管理員 hello 容錯移轉群組觸發程序 hello hello 資料庫的容錯移轉之前，將 hello web 應用程式就不能 tooreconnect toohello 資料庫。 hello 資料庫容錯移轉完成時，會自動成功 hello 應用程式嘗試 tooreconnect。 

> [!NOTE]
> tooachieve 完全協調 hello 應用程式和 hello 資料庫的容錯移轉，您應該設計您自己的監視方法，並使用 hello web 應用程式端點和 hello 資料庫手動容錯移轉。
>

Hello hello 應用程式端點和 hello 資料庫的容錯移轉完成之後，hello 應用程式會重新開始處理 hello hello 區域 B 中的使用者要求，並就會維持與 hello 資料庫位於相同位置，因為 hello 主要資料庫目前處於區域 b。此案例中是以 hello 下列圖表所示。 在所有圖表中，實線表示作用中連線，虛線表示暫止的連線，停止標誌表示動作觸發。

![Toosecondary 地理複寫： 容錯移轉的資料庫。 應用程式資料備份。](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-2.png)

如果發生中斷情況發生 hello 次要區域中，hello hello 主要與 hello 次要資料庫之間的複寫連結會暫停，不過因為 hello 主要資料庫不受影響，不會觸發 hello 容錯移轉。 hello 應用程式的可用性不會變更在此情況下，但 hello 應用程式運作的公開，因此具有較高的風險，以防在兩個區域失敗連續。

> [!NOTE]
> 嚴重損壞修復建議 hello 組態與應用程式部署限制 tootwo 區域。 這是因為大部分的 hello Azure 地理位置具有只有兩個區域。 這些設定不會保護應用程式免於遭受兩個區域同時發生的重大失敗。  在這種罕見的失敗情況下，您可以使用[異地復原作業](sql-database-disaster-recovery.md#recover-using-geo-restore)，在第三個區域復原資料庫。
>

一旦降低 hello 中斷，hello 次要資料庫會自動重新同步處理以 hello 主要。 同步處理期間，主要 hello 的效能可能稍微影響視 hello 需要 toobe 同步處理的資料數量而定。 hello 下列圖表說明 hello 次要區域中的發生中斷。

![次要資料庫會與主要資料庫進行同步處理。 雲端災害復原。](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-3.png)

hello 金鑰**優點**此設計模式是：

* hello 相同 web 應用程式是部署的 tooboth 區域，而不需要任何特定地區設定和任何其他邏輯 tooreact toohello 容錯移轉。 
* hello 應用程式的效能不會受到為 hello web 應用程式的容錯移轉，而且 hello 資料庫永遠位於相同位置。

主要的 hello**權衡取捨**hello 多餘的應用程式是 hello 次要區域中的執行個體只用於災害復原。

## <a name="design-pattern-2-active-active-deployment-for-application-load-balancing"></a>設計模式 2：應用程式負載平衡的主動-主動部署
此雲端的災害復原選項最適合用於應用程式具有下列特性的 hello:

* 資料庫的比例過高讀取 toowrites
* 資料庫讀取延遲高於 hello 使用者體驗的 hello 寫入延遲 
* 使用不同的連接字串可以隔開唯讀邏輯和讀寫邏輯
* 唯讀邏輯並非取決於 hello 最新的更新與進行完整同步處理的資料  

如果您的應用程式具有下列特性，可大幅改善負載平衡不同區域中的多個應用程式執行個體中的 hello 使用者連線 hello 整體的使用者體驗。 Hello 區域的兩個應該當做 hello DR 配對和 hello 容錯移轉群組應該包含在這些區域中的 hello 資料庫。 tooimplement 負載平衡每個區域應該與 hello 讀寫 (RW) 連線的邏輯 toohello 讀取寫入接聽程式端點 hello 容錯移轉群組的作用中的 hello 應用程式執行個體。 它將會保證如果 hello 主要資料庫會受中斷影響自動起始 hello 容錯移轉。 hello 唯讀 (RO) 中邏輯 hello web 應用程式應該直接連接 toohello 資料庫在該區域中。 流量管理員應該設定 toouse[效能路由](../traffic-manager/traffic-manager-configure-performance-routing-method.md)與[端點監視](../traffic-manager/traffic-manager-monitoring.md)啟用每個應用程式執行個體。

如同模式 #1，您應該考慮部署類似的監視應用程式。 但是，有別於模式 #1，hello 監視應用程式不會負責觸發 hello 端點容錯移轉。

> [!NOTE]
> 此模式會使用多個次要資料庫，而只 hello 次要區域 B 中用於容錯移轉，而且應該 hello 容錯移轉群組的一部分。
>

流量管理員應該設定為效能路由 toodirect hello 使用者連線 toohello 應用程式執行個體最接近 toohello 使用者的地理位置。 hello 下列圖表說明前中斷此組態。

![沒有中斷： 路由 toonearest 應用程式的效能。 異地複寫。](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-1.png)

Hello 容錯移轉群組 hello 區域 A 中偵測到資料庫中斷時，會自動起始次要區域 b 中的區域 A toohello hello 主要資料庫的容錯移轉它也會自動將更新 hello 讀取寫入接聽程式端點 tooregion B 使 hello web 應用程式中的讀寫連接將不會受到影響。 hello traffic manager 會將排除 hello 路由表 hello 離線的端點，但仍會繼續路由 hello 使用者流量 toohello 剩餘線上的執行個體。 hello 唯讀 SQL 連接字串將不會影響，因為它們一律指向 hello toohello 資料庫相同的區域。 

hello 下列圖表說明 hello hello 容錯移轉之後的新組態。

![容錯移轉之後的組態。 雲端災害復原。](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-2.png)

發生在其中一個 hello 次要區域發生中斷，hello traffic manager 會自動移除 hello 離線的端點在該區域 hello 路由表。 將擱置 hello 複寫通道 toohello 次要資料庫在該區域中。 Hello 剩餘區域在此案例中取得額外的使用者流量，因為 hello 應用程式的效能會受到影響 hello 中斷期間。 一旦降低 hello 中斷，hello hello 受影響區域中的次要資料庫會立即同步處理以 hello 主要。 Hello 期間同步處理效能的主要 hello 可能稍微影響視 hello 需要 toobe 同步處理的資料數量而定。 hello 下列圖表說明區域 b 中斷

![次要地區中斷。 雲端災害復原 - 異地複寫。](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-3.png)

hello 金鑰**利用**這種設計模式是您可以跨多個次要資料庫 tooachieve hello 最佳的使用者效能調整 hello 應用程式工作負載。 hello**的權衡取捨完全**這個選項是：

* Hello 應用程式執行個體與資料庫之間的讀寫連接具有不同的延遲和成本
* Hello 中斷期間，會影響應用程式效能

> [!NOTE]
> 可以使用類似的方法 toooffload 特製化工作負載，例如報告作業、 商業智慧工具或備份。 一般而言，這些工作負載會耗用大量的資料庫資源因此建議您將指定 hello 的其中一個次要資料庫，與 hello 效能層級相符的 toohello 預期工作負載。
>

## <a name="design-pattern-3-active-passive-deployment-for-data-preservation"></a>設計模式 3：資料保留的主動-被動部署
這個選項最適合用於應用程式具有下列特性的 hello:

* 任何資料遺失都會帶來極高的商業風險。 hello 資料庫容錯移轉只能作為最後的方法如果 hello 中斷為重大。
* hello 應用程式支援唯讀和讀寫模式的作業，並可以在 「 唯讀模式 」 中運作的一段時間。

在這種模式 hello 應用程式時 hello 讀寫連接開始取得逾時錯誤切換 tooread 僅限模式。 hello Web 應用程式是部署的 tooboth 區域，包含連接 toohello 讀取寫入接聽程式端點和不同連線 toohello 唯讀接聽程式端點。 hello 流量管理員應該設定 toouse[容錯移轉路由](../traffic-manager/traffic-manager-configure-failover-routing-method.md)與[端點監視](../traffic-manager/traffic-manager-monitoring.md)hello 應用程式端點，每個區域中啟用。

hello 下列圖表說明前中斷此組態。

![容錯移轉之前的主動/被動部署。 雲端災害復原。](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-1.png)

當 hello traffic manager 偵測到的連線失敗 tooregion A 時，它會自動切換使用者流量 toohello 應用程式執行個體在區域 b。此模式中，很重要，您設定 hello 寬限期內使用的資料遺失 tooa 夠高的值，例如 24 小時。 它可確保，如果 hello 中斷降低該段時間內，避免資料遺失。 Hello hello 區域 B 中的 Web 應用程式啟動時 hello 讀取-寫入作業就會開始失敗。 此時，它應該切換 toohello 唯讀模式。 在此模式 hello 要求將會自動路由的 toohello 次要資料庫。 在 hello 案例中的重大錯誤 hello 中斷將不降低 hello 寬限期內，而且 hello 容錯移轉群組將會觸發 hello 容錯移轉。 該 hello 之後讀取寫入接聽程式會變成可用，而且 hello 呼叫 tooit 將會停止失敗。 Hello 下列圖表說明此用法。

![中斷：處於唯讀模式的應用程式。 雲端災害復原。](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-2.png)

如果 hello 主要區域中的 hello 中斷降低 hello 寬限期內，traffic manager 會連線 hello 還原偵測 hello 主要區域中，並切換使用者流量後 toohello 應用程式執行個體在區域 a會繼續該應用程式執行個體，並且在區域 a 使用 hello 主要資料庫的讀寫模式中運作

發生在 hello 區域 B 發生中斷，hello traffic manager 偵測 hello 失敗 hello 應用程式端點到區域 B 和 hello 容錯移轉群組交換器 hello 唯讀接聽程式 tooregion a。此中斷不會影響 hello 使用者體驗，但 hello 主要資料庫會公開在 hello 中斷期間。 Hello 下列圖表說明此用法。

![中斷：次要資料庫。 雲端災害復原。](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-3.png)

一旦降低 hello 中斷，hello 次要資料庫會立即同步處理主要 hello 和 hello 唯讀接聽程式是交換後 toohello 區域 b 中的次要資料庫同步處理期間 hello 主要的效能可能稍微影響視 hello 需要 toobe 同步處理的資料數量而定。

此設計模式有幾個 **優點**：

* 它可在 hello 暫時中斷期間避免資料遺失。
* 停機時間僅取決於流量管理員偵測 hello 連線失敗，您可設定的速度。

hello**權衡取捨**是：

* 應用程式必須能夠 toooperate 為唯讀模式。

> [!NOTE]
> Hello 區域中的永久性服務中斷，如果您手動啟動資料庫容錯移轉，並接受 hello 資料遺失。 hello 應用程式將能 hello 與讀寫存取 toohello 資料庫的次要區域中作用。
>

## <a name="business-continuity-planning-choose-an-application-design-for-cloud-disaster-recovery"></a>商務持續性計劃：針對雲端災害復原選擇應用程式設計
特定雲端災害復原策略可以合併或 toobest 符合 hello 需求的應用程式擴充這些設計模式。  如先前所述，您所選擇的 hello 策略根據 hello SLA toooffer tooyour 客戶並 hello 應用程式的部署拓撲。 toohelp 引導您決定，hello 下表比較 hello 選擇根據 hello 估計的資料遺失或復原點目標 (RPO) 和預估的復原時間 (ERT)。

| 模式 | RPO | ERT |
|:--- |:--- |:--- |
| 災害復原的主動-被動部署，使用共置資料庫存取 |讀寫存取 < 5 秒 |失敗偵測時間 + DNS TTL |
| 應用程式負載平衡的主動-主動部署 |讀寫存取 < 5 秒 |失敗偵測時間 + DNS TTL |
| 資料保留的主動-被動部署 |唯讀存取 < 5 秒 | 唯讀存取 = 0 |
||讀寫存取 = 0 | 讀寫存取 = 失敗偵測時間 + 遺失資料的寬限期 |
|||

## <a name="next-steps"></a>後續步驟
* toolearn 有關自動化 Azure SQL Database 備份，請參閱[SQL 資料庫自動備份](sql-database-automated-backups.md)
* 如需商務持續性概觀和案例，請參閱 [商務持續性概觀](sql-database-business-continuity.md)
* toolearn 有關使用自動的備份進行復原，請參閱[hello 服務起始的備份還原的資料庫](sql-database-recovery-using-backups.md)
* toolearn 有關更快速的復原選項，請參閱[作用中地理複寫](sql-database-geo-replication-overview.md)  
* toolearn 有關用於自動的備份封存，請參閱[資料庫複製](sql-database-copy.md)
* 如需主動式異地複寫與彈性集區的相關資訊，請參閱[彈性集區災害復原策略](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)。

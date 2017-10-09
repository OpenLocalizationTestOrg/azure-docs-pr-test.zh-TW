---
title: "aaaAzure SQL Database 的常見問題集 |Microsoft 文件"
description: "答案 toocommon 問題客戶詢問雲端資料庫和 Azure SQL Database、 Microsoft 的關聯式資料庫管理系統 (RDBMS)，以及資料庫為 hello 雲端中的服務。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 1da12abc-0646-43ba-b564-e3b049a6487f
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 02/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 04c02f96e6e91cf314221134ee0ef6d24217ef45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-faq"></a>SQL Database 常見問題集

## <a name="what-is-hello-current-version-of-sql-database"></a>什麼是 hello 最新版 SQL Database？
hello 最新版 SQL Database 是 V12。 版本 V11 已被淘汰。

## <a name="what-is-hello-sla-for-sql-database"></a>SQL Database 的 hello SLA 是什麼？
我們保證至少 99.99%的客戶 hello 其單一或彈性 Basic、 Standard 或 Premium Microsoft Azure SQL Database 與我們的網際網路閘道之間的連線。 如需詳細資訊，請參閱 [SLA](http://azure.microsoft.com/support/legal/sla/)。

## <a name="how-do-i-reset-hello-password-for-hello-server-admin"></a>如何重設 hello hello 伺服器系統管理員密碼？
在 hello [Azure 入口網站](https://portal.azure.com)按一下**SQL 伺服器**，從 [hello] 清單中，選取 hello 伺服器，然後按一下**重設密碼**。

## <a name="how-do-i-manage-databases-and-logins"></a>如何管理資料庫與登入？
請參閱[管理資料庫與登入](sql-database-manage-logins.md)。

## <a name="how-do-i-make-sure-only-authorized-ip-addresses-are-allowed-tooaccess-a-server"></a>如何確定只有獲得授權的 IP 位址都允許 tooaccess 伺服器？
請參閱 [如何：在 SQL Database 上進行防火牆設定](sql-database-configure-firewall-settings.md)。

## <a name="how-does-hello-usage-of-sql-database-show-up-on-my-bill"></a>如何確實 hello 的 SQL 資料庫的使用方式顯示在 我的帳單上？
SQL Database 帳單上可預測的時薪根據 hello 服務層 + 效能層級的單一資料庫或每個彈性集區 Edtu。 實際使用量會每小時依比例分配的方式計算，因此有可能會出現不滿一小時的帳單。 例如，如果資料庫在一個月內的存在時間是 12 個小時，則您的帳單會顯示 0.5 天的使用量。 此外，服務層 + 效能層級和每個集區 Edtu 都中斷 out hello bill toomake 中它更容易 toosee hello 數目您用於在單一月份內的每個資料庫使用天數。

## <a name="what-if-a-single-database-is-active-for-less-than-an-hour-or-uses-a-higher-service-tier-for-less-than-an-hour"></a>如果單一資料庫作用中的時間少於一小時，或使用更高服務層的時間少於一小時，會發生什麼情況？
您需要為每小時使用的資料庫已經存在 hello 最高服務層 + 效能層級，套用在該小時內，不論使用量或 hello 資料庫是否使用不超過一小時付費。 例如，假設您建立了單一資料庫並在五分鐘後刪除，您的帳單就會反映一個資料庫時數的費用。 

範例

* 如果您建立基本的資料庫，然後立即將它升級 tooStandard S1 時，您會收費 hello 標準 S1 hello 第一個小時。
* 如果您從基本 tooPremium 升級資料庫在下午 10:00 在隔天上午 1:35 完成升級， 在下列日期的 hello，您會收費 hello Premium 從上午 1:00 
* 如果您將資料庫從高階 tooBasic 降級上午 11:00 完成在下午 2:15，然後 hello 資料庫收費 hello Premium 直到下午 3:00 之後, 付費 hello 基本費率。

## <a name="how-does-elastic-pool-usage-show-up-on-my-bill-and-what-happens-when-i-change-edtus-per-pool"></a>彈性集區使用量如何在我的帳單上顯示，以及變更每個集區的 eDTU 時會發生什麼？
彈性集區費用顯示總在帳單上為彈性的 dtu 數 (Edtu) 上顯示每個集區 Edtu 下 hello 增量[hello 定價頁面](https://azure.microsoft.com/pricing/details/sql-database/)。 彈性集區沒有每一資料庫的費用。 您所要支付每小時的集區存在於 hello 最高的 eDTU，不論使用量或 hello 集區是否作用中少於一小時。 

範例

* 如果您建立標準的彈性集區 Edtu 200 上午 11:18，新增五個資料庫 toohello 集區，您將支付 200 Edtu hello 整個小時，從上午 11 透過 hello 一天的 hello 餘數。
* 上一天的 2、 上午 5:05，資料庫 1 開始耗用 50 的 Edtu，並擁有計算穩定透過 hello 天。 資料庫 2-5 會在 0 和 80 eDTU 之間波動。 Hello 一天，您可以加入五個使用不同的 Edtu hello 整天其他資料庫。 第 2 天是全天，以 200 eDTU 計費。 
* 在第 3 天上午 5:00， 您加入另外 15 個資料庫。 資料庫的使用量會增加整個 hello 天 toohello 點，您可以決定 tooincrease 從 200 too400 hello 集區的 Edtu 下午 8:05 Hello 200 eDTU 層級的費用是作用中直到下午 8，並增加 too400 Edtu hello 剩餘四小時。 

## <a name="elastic-pool-billing-and-pricing-information"></a>彈性集區的計費和定價資訊
彈性集區會計費每 hello 下列特性：

* 彈性集區是在其建立計費，即使 hello 集區中沒有任何資料庫。
* 彈性集區會以每小時計費。 這是 hello 相同計量與單一資料庫的效能層級的頻率。
* 彈性集區是否為新的調整大小的 tooa 的 Edtu，然後 hello 集區數目不會計費根據 toohello 新數量的 Edtu，直到 hello 調整大小作業完成為止。 這會遵循的 hello 相同模式為變更單一資料庫 hello 效能層級。
* 彈性集區的 hello 價格根據 hello hello 集區的 Edtu 數目。 彈性集區的 hello 價格無關 hello 數目和 hello 彈性資料庫內的使用率。
* 價格的計算方式為 (集區的 eDTU 數) x (每 eDTU 的單價)。

彈性集區的 hello 單位 eDTU 價格高於 hello DTU 單價 hello 在單一資料庫的相同服務層。 如需詳細資訊，請參閱 [SQL Database 定價](https://azure.microsoft.com/pricing/details/sql-database/)。 

toounderstand hello 的 edtu 數目及服務層，請參閱[SQL Database 選項及效能](sql-database-service-tiers.md)。

## <a name="how-does-hello-use-of-active-geo-replication-in-an-elastic-pool-show-up-on-my-bill"></a>Hello 如何使用我的帳單上彈性集區顯示中的作用中地理複寫的？
與單一資料庫不同，搭配彈性資料庫使用[作用中異地複寫](sql-database-geo-replication-overview.md)對計費並沒有直接的影響。  您僅支付 hello Edtu hello 集區 （主要集區和次要的集區） 的每個佈建

## <a name="how-does-hello-use-of-hello-auditing-feature-impact-my-bill"></a>如何 hello 使用稽核功能影響 hello 的我的帳單？
稽核建置到 hello SQL Database 服務不需額外成本，並是使用 tooBasic、 Standard、 Premium 和 Premium RS 資料庫。 不過，toostore hello 稽核記錄，hello 稽核功能使用 Azure 儲存體帳戶，與資料表和佇列在 Azure 儲存體費率適用於根據 hello 的稽核記錄的大小。

## <a name="how-do-i-find-hello-right-service-tier-and-performance-level-for-single-databases-and-elastic-pools"></a>如何針對單一資料庫和彈性集區中找到 hello 正確的服務層和效能層級？
有幾個工具可用 tooyou。 

* 在內部部署資料庫，請使用 hello [DTU 縮放 advisor](http://dtucalculator.azurewebsites.net/) toorecommend hello 資料庫和必要的 Dtu 和評估多個資料庫的彈性集區。
* 如果單一資料庫會因集區而受益，Azure 的智慧型引擎如果發現必要的歷程使用模式，就會建議彈性集區。 請參閱[監視和管理 hello Azure 入口網站的彈性集區](sql-database-elastic-pool-manage-portal.md)。 如需有關如何 toodo hello 數學自己的詳細資訊，請參閱[彈性集區的價格和效能考量](sql-database-elastic-pool.md)
* toosee 您是否需要 toodial 單一資料庫或當機，請參閱[單一資料庫的效能指引](sql-database-performance-guidance.md)。

## <a name="how-often-can-i-change-hello-service-tier-or-performance-level-of-a-single-database"></a>頻率可以變更 hello 服務層或效能層級的單一資料庫？
您可以變更 hello （之間 Basic、 Standard、 Premium 和 Premium RS） 的服務層或 hello 視您想要的服務層 (例如，S1 tooS2) 內的效能層級。 對於較早版本的資料庫，您可以變更 hello 服務層或效能層級四次，在 24 小時內的總計。

## <a name="how-often-can-i-adjust-hello-edtus-per-pool"></a>頻率可以調整每個集區 edtu 數 （hello）？
視您所需，不限次數。

## <a name="how-long-does-it-take-toochange-hello-service-tier-or-performance-level-of-a-single-database-or-move-a-database-in-and-out-of-an-elastic-pool"></a>多久它不會採取 toochange hello 服務層或效能層級的單一資料庫或將資料庫移入和移出彈性集區嗎？
變更資料庫的 hello 服務層，並移入和登出的集區需要 hello 資料庫 toobe 複製成背景操作 hello 平台上。 變更 hello 服務層可能需要幾分鐘的時間 tooseveral 數小時，視 hello hello 資料庫大小而定。 在這兩種情況下，hello 資料庫會保持上線而且可以使用在 hello 移動。 如需有關變更單一資料庫的詳細資訊，請參閱[變更 hello 服務層資料庫](sql-database-service-tiers.md)。 

## <a name="when-should-i-use-a-single-database-vs-elastic-databases"></a>何時應該使用單一資料庫與彈性資料庫？
一般而言，彈性集區是專為一般 [軟體即服務 (SaaS) 應用程式模式](sql-database-design-patterns-multi-tenancy-saas-applications.md)而設計，其中每一客戶或租用戶會有一個資料庫。 購買的個別資料庫過度佈建 toomeet hello 變數和尖峰要求的每個資料庫通常不成本效益。 使用集區，您管理 hello hello 集區的整體效能和 hello 資料庫擴充向上和向下自動。 Azure 的智慧型引擎如果發現必要的使用模式，就會對資料庫建議集區。 如需詳細資訊，請參閱[彈性集區指引](sql-database-elastic-pool.md)。

## <a name="what-does-it-mean-toohave-up-too200-of-your-maximum-provisioned-database-storage-for-backup-storage"></a>是什麼意思 toohave too200%您最大佈建的資料庫的儲存體的備份存放區？
備份儲存體是 hello 與自動化的資料庫備份所使用的相關聯的儲存體[點--時間-還原中](sql-database-recovery-using-backups.md#point-in-time-restore)和[異地還原](sql-database-recovery-using-backups.md#geo-restore)。 Microsoft Azure SQL Database 提供 too200%佈建的最大資料庫儲存體的備份儲存體不需要額外成本。 例如，如果您擁有可佈建 DB 大小為 250 GB 的標準 DB 執行個體，您就能免費獲得 500 GB 的備份儲存體。 如果您的資料庫超過 hello 提供備份儲存體，您可以選擇透過連絡 Azure 支援人員的 tooreduce hello 保留期限，或支付標準的讀取權限地理備援儲存體 (RA-GRS) 費率計費的 hello 額外備份儲存體。 如需 RA-GRS 計費的詳細資訊，請參閱儲存體價格詳細資料。

## <a name="im-moving-from-webbusiness-toohello-new-service-tiers-what-do-i-need-tooknow"></a>我正在移從 Web/Business toohello 新服務層，該怎麼我需要 tooknow 嗎？
Azure SQL Web 和 Business 資料庫現已淘汰。 hello Basic、 Standard、 Premium、 Premium RS 和彈性層取代淘汰 Web 和 Business 資料庫的 hello。 

## <a name="what-is-an-expected-replication-lag-when-geo-replicating-a-database-between-two-regions-within-hello-same-azure-geography"></a>什麼是預期的複寫延遲時資料庫內的兩個區域之間進行地理複寫 hello 相同 Azure 地理位置？
我們目前支援的五秒 RPO 和 hello 複寫延遲已少於 hello 地理次要 hello Azure 建議配對的區域中裝載時，而且在 hello 相同服務層。

## <a name="what-is-an-expected-replication-lag-when-geo-secondary-is-created-in-hello-same-region-as-hello-primary-database"></a>什麼是預期的複寫延遲地理次要資料庫中建立時 hello 相同 hello 主要資料庫與區域？
根據經驗的資料，沒有任何內部區域和區域間複寫延遲太多差異使用的 hello Azure 建議配對的區域時。 

## <a name="if-there-is-a-network-failure-between-two-regions-how-does-hello-retry-logic-work-when-geo-replication-is-set-up"></a>如果兩個區域之間沒有網路失敗，hello 重試邏輯的運作方式設定地理複寫時？
如果沒有中斷連接，我們會重試每隔 10 秒 toore-建立連線。

## <a name="what-can-i-do-tooguarantee-that-a-critical-change-on-hello-primary-database-is-replicated"></a>怎麼 tooguarantee hello 主要資料庫上的重大變更會複寫？
hello 地理次要是 async 複本，而我們不會嘗試 tookeep 在以主要 hello 完整同步處理。 但是，我們提供方法 tooforce 同步 tooensure hello 複寫的重大變更 （例如，密碼更新）。 強制同步處理會影響效能，因為它會封鎖 hello 呼叫執行緒直到所有認可的交易都會複寫。 如需詳細資訊，請參閱 [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx)。 

## <a name="what-tools-are-available-toomonitor-hello-replication-lag-between-hello-primary-database-and-geo-secondary"></a>哪些工具是 hello 主要資料庫和地理次要資料庫之間的可用 toomonitor hello 複寫延遲？
我們已公開 hello 主要資料庫和透過 DMV 地理次要資料庫之間的 hello 即時複寫延遲。 如需詳細資訊，請參閱 [sys.dm_geo_replication_link_status](https://msdn.microsoft.com/library/mt575504.aspx)。

## <a name="toomove-a-database-tooa-different-server-in-hello-same-subscription"></a>中的資料庫 tooa 不同伺服器 hello toomove 相同訂用帳戶
* 在 hello [Azure 入口網站](https://portal.azure.com)，按一下  **SQL 資料庫**hello] 清單中，從選取的資料庫，然後按**複製**。 如需詳細資訊，請參閱 [複製 Azure SQL Database](sql-database-copy.md) 。

## <a name="toomove-a-database-between-subscriptions"></a>toomove 訂用帳戶之間的資料庫
* 在 hello [Azure 入口網站](https://portal.azure.com)，按一下  **SQL 伺服器**，然後選取裝載您的資料庫從 hello 清單 hello 伺服器。 按一下**移動**，然後挑選 hello 資源 toomove 和 hello 訂用帳戶 toomove 至。

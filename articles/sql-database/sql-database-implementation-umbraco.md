---
title: "aaaAzure SQL 資料庫 Azure 案例研究-Umbraco |Microsoft 文件"
description: "深入了解 Umbraco 如何使用 SQL Database tooquickly 佈建和小數位數服務針對擁有成千上萬個租用戶 hello 雲端中"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5243d31e-3241-4cb0-9470-ad488ff28572
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 93e39e509831a5ff90f129d9537ece0b0dafef0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="umbraco-uses-azure-sql-database-tooquickly-provision-and-scale-services-for-thousands-of-tenants-in-hello-cloud"></a>Umbraco hello 雲端中使用 Azure SQL Database tooquickly 佈建和針對擁有成千上萬個租用戶的小數位數服務
![Umbraco 標誌](./media/sql-database-implementation-umbraco/umbracologo.png)

Umbraco 是熱門開放原始碼內容管理系統 (CMS)，可以執行的任何項目從小型的活動或冊站台 toocomplex 應用程式的全球 500 強公司和全域媒體網站。 

> 「 我們有相當大型的社群與 100,000 個以上開發人員在我們的論壇以及即時，超過 350000 個站台上執行 Umbraco 使用 hello 系統的開發人員 」。
> 
> — Morten Christensen，Umbraco 技術主管
> 
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-Umbraco/player]
> 
> 

toosimplify 客戶部署，Umbraco 加入 Umbraco 做為服務 (UaaS): 可以降低對內部部署的 hello 需求的軟體做為服務 (SaaS) 供應項目提供內建調整功能和額外負荷，進而移除管理開發人員 toofocus 創新，而不是解決方案管理的產品。 Umbraco 是無法 tooprovide 所依賴的所有這些優點 hello Microsoft Azure 所提供的彈性的平台做為服務 (PaaS) 模型。

UaaS 可讓 SaaS 客戶 toouse Umbraco CMS 功能，則先前超出其範圍。 針對這些客戶，會佈建一個包含生產環境資料庫的可運作 CMS 環境。 客戶可以加總 tootwo 進行開發和預備環境，根據其需求的其他資料庫。 發出新環境要求時，自動化程序會自動為該客戶指派一個資料庫。 hello 新的資料庫是以秒為單位，準備好，因為 hello 資料庫具有已預先佈建的 Umbraco 從 Azure 的彈性集區的可用資料庫 （請參閱圖 1）。

![Umbraco 佈建的生命週期](./media/sql-database-implementation-umbraco/figure1.png)

圖 1. Umbraco 即服務 (UaaS) 的佈建生命週期

## <a name="azure-elastic-pools-and-automation-simplify-deployments"></a>Azure 彈性集區和自動化可簡化部署
藉由使用 Azure SQL Database 和其他 Azure 服務，Umbraco 客戶可自行佈建其環境，而 Umbraco 則可以在直覺式工作流程中輕鬆地監視和管理資料庫︰

1. 佈建
   
   Umbraco 維持一個含有 200 個可用資料庫的容量，這些資料庫都是來自彈性集區的預先佈建資料庫。 當新客戶註冊 UaaS 時，Umbraco 提供與新的 CMS 環境幾近即時的 hello 客戶從 hello 可用性集區指派資料庫。
   
   當可用性集區達到其臨界值時，建立新的彈性集區時，與新的資料庫會視需要指派 toocustomers 預先佈建的 toobe。
   
   此實作是使用 C# 管理程式庫和「Azure 服務匯流排」佇列來完全自動化執行。
2. 利用
   
   客戶使用其中一個 toothree 環境 （適用於實際執行環境、 預備及/或開發），每個與它自己的資料庫。 客戶資料庫會處於彈性集區，可讓 Umbraco tooprovide 有效率地調整而不需要 tooover 佈建。
   
   ![Umbraco 專案概觀](./media/sql-database-implementation-umbraco/figure2.png)
   
   ![Umbraco 專案詳細資料](./media/sql-database-implementation-umbraco/figure3.png)
   
   圖 2. 顯示專案總覽和詳細資料的 Umbraco 即服務 (UaaS) 客戶網站
   
   Azure SQL Database 會使用資料庫交易單位 (Dtu) toorepresent hello 相對乘冪所需的實際資料庫交易。 UaaS 客戶資料庫通常會操作在大約 10 個 Dtu，但其中一個 hello 彈性 tooscale 依需求。 這意謂著 UaaS 可以確保客戶一律擁有必要的資源，甚至是在尖峰時間也一樣。 比方說，最近星期天運動事件期間，一位 UaaS 客戶會發生 hello 遊戲 hello 期間向上 too100 Dtu 資料庫尖峰。 Azure 的彈性集區變成可將 Umbraco toosupport 高而效能降低不需要。
3. 監視
   
   Umbraco 監視資料庫活動使用儀表板內 hello Azure 入口網站，以及自訂的電子郵件警示。
4. 災害復原
   
   Azure 提供兩種災害復原 (DR) 選項：作用中異地複寫和異地還原。 hello 應選取一家公司的 DR 選項取決於其[業務續航力目標](sql-database-business-continuity.md)。
   
   作用中地理複寫會提供最快 hello 回應 hello 的停機時間的事件層級。 使用作用中地理複寫，您可以建立 toofour 可讀取次要上不同的區域中的伺服器上，而且您接著可初始 hello hello 失敗事件中的次要資料庫的容錯移轉 tooany。
   
   Umbraco 不需要地理複寫，但它未充分利用 Azure 地理還原 toohelp 確認中斷的 hello 事件中的最少停機時間。 異地還原需倚賴異地備援 Azure 儲存體中的資料庫備份。 Hello 主要區域中發生中斷時，可讓使用者 toorestore 從備份副本。
5. 取消佈建
   
   刪除專案環境時，於「Azure 服務匯流排」佇列清除期間，將會移除所有關聯的資料庫 (開發、預備或即時)。 自動執行此程序還原 hello 未使用的資料庫 tooUmbraco 彈性資料庫可用性集區，讓它們可維持使用量上限未來佈建。

## <a name="elastic-pools-allow-uaas-tooscale-with-ease"></a>彈性集區允許 UaaS tooscale 就能輕鬆
利用 Azure 的彈性集區，Umbraco 可以最佳化其客戶的效能，而不需要 tooover 或置中佈建。 Umbraco 目前幾乎 3000 資料庫 19 彈性集區，與 hello 能力 tooeasily 比例調整成所需的 tooaccommodate 任何其現有 325,000 客戶或新客戶準備 toodeploy hello 雲端中的 CMS。

事實上，根據 tooMorten Christensen，技術會導致在 Umbraco、"UaaS 現在遇到大約 30 新客戶，每日的成長。 我們的客戶都很高興與 hello 便利性正在無法 tooprovision 新專案，以秒為單位，立即發行更新從開發環境中使用 '單鍵部署' tootheir 即時網站並進行變更一樣快速如果它們找出錯誤。 」

如果客戶不再需要第二個和/或第三個環境，可以直接將這些環境移除。 會釋放資源可以用於其他客戶 hello Umbraco 彈性資料庫可用性集區的一部分。

![Umbraco 部署架構](./media/sql-database-implementation-umbraco/figure4.png)

圖 3. Microsoft Azure 上的 UaaS 部署架構

## <a name="hello-path-from-datacenter-toocloud"></a>從資料中心 toocloud hello 路徑
Hello Umbraco 開發人員一開始進行 hello 決策 toomove tooa SaaS 模式，他們知道，客戶必須符合成本效益且可擴充的方式 toobuild 出 hello 服務。

> 「彈性集區是最適合我們 SaaS 方案的選項，因為我們可以視需要上下調整容量。 佈建相當簡單，再搭配上我們的設定，我們便可以做最充分的利用」。
> 
> — Morten Christensen，Umbraco 技術主管
> 
> 

「 我們 toospend 我們解決客戶的問題，無法管理基礎結構的時間。 我們想 toomake 讓我們的客戶 tooget 輕易 hello 大部分的值 」 指出 Niels Hartvig，創辦 Umbraco。 「 我們一開始會視為主控 hello 伺服器，但容量計劃已經惡夢 」。 碰巧的是，Umbraco 並未雇用任何資料庫系統管理員，而這強調了一個使用 UaaS 的主要價值主張。

Hello Umbraco 開發人員的一個重要的目標是 tooprovide UaaS 客戶 tooprovision 環境的方式，快速且不會受到容量限制。 但是，提供專屬的裝載的服務 Umbraco 資料中心內會有大量的多餘容量 toohandle 突發處理中。 這意謂著要新增大量一般不會充分利用的計算基礎結構。

此外，hello Umbraco 開發小組想要允許他們 tooreuse 一樣多的現有程式碼儘可能的解決方案。 Umbraco 開發人員為 Mikkel Madsen 所述，「 我們感到滿意 hello 我們已經熟悉，例如 Microsoft SQL Server、 Microsoft Azure SQL Database、 ASP.net 和 Internet Information Services (IIS) 的 Microsoft 開發工具。 之前投資 IaaS 或 PaaS 雲端解決方案中，我們想確定，就會支援我們的 Microsoft 工具和平台，因此我們不會有 toomake 大量變更 tooour 程式碼基底 toomake。 」

toomeet 所有的準則，Umbraco 尋找雲端合作夥伴以 hello 下列條件：

* 足夠的容量與可靠性
* 支援 Microsoft 開發工具，因此該 Umbraco 工程師不會強制 toocompletely 重建其開發環境
* 在所有 hello 地理市場 UaaS 競相 (他們可以快速地存取其資料和其資料儲存在符合其地區法規需求的位置就企業需要 tooensure) 所在的目前狀態

## <a name="why-umbraco-chose-azure-for-uaas"></a>為什麼 Umbraco 選擇將 Azure 用於 UaaS
根據 tooMorten Christensen 「 所有的選項後，我們選取 Azure 因為它符合所有我們準則，從 管理性和延展性 toofamiliarity 成本效益。 我們設定 hello Azure Vm 上的環境，且每個環境有它自己的 Azure SQL Database 執行個體，在彈性集區中的所有 hello 執行個體。 藉由分隔開發、 預備及實際環境之間的資料庫，我們可以我們的客戶提供強固的效能隔離相符 tooscale — 龐大 win。 」

Morten 持續發生，"之前，我們以手動方式在 tooprovision web 資料庫的伺服器。 現在，我們沒有 toothink 資訊，請參閱。 系統會自動執行的所有項目，從佈建 toocleanup。 」

以 hello 調整 Azure 所提供的功能，還有高興 Morten。 「彈性集區是最適合我們 SaaS 方案的選項，因為我們可以視需要上下調整容量。 佈建相當簡單，再搭配上我們的設定，我們便可以做最充分的利用」。 Morten 狀態，「 彈性集區，以及服務層基礎的 Dtu 保證 hello hello 簡化提供 hello 電源 tooprovision 新資源集區視。 其中一個較大客戶尖峰 too100 Dtu 其實際環境中。 使用 Azure 時，我們彈性集區提供了與它們所需而不需要 toopredict DTU 需求即時 hello 資源 hello 客戶的資料庫。 簡單地說，我們的客戶取得 hello 小時間，他們預期時，我們可以符合我們的效能層級的服務合約 」。

Mikkel Madsen 概括: 「 我們已經擁抱 hello 強大 Azure 演算法之上 hello 連接一般 SaaS 案例 （使用大規模的即時入門訓練新客戶） tooour 應用程式模式 （預先佈建資料庫，這兩種開發和即時）基礎技術 （Azure SQL Database 搭配使用 Azure 服務匯流排佇列）。 」

## <a name="with-azure-uaas-is-exceeding-customer-expectations"></a>透過 Azure，UaaS 的表現超出客戶期望
選擇 Azure 以做為其雲端協力電腦，因為 Umbraco 已能 tooprovide UaaS 客戶與內容管理最佳化的效能，不需要從自我裝載的解決方案所需的 hello IT 資源的投資。 Morten 指出，"歡迎您提供 hello 開發人員為了方便和 Azure 可讓我們的延展性，我們的客戶會滿意 hello 功能和可靠性。 整體而言，對我來說是一大勝利！」

## <a name="more-information"></a>詳細資訊
* toolearn 深入了解 Azure 的彈性集區，請參閱[彈性集區](sql-database-elastic-pool.md)。
* toolearn 深入了解 Azure 服務匯流排，請參閱[Azure 服務匯流排](https://azure.microsoft.com/services/service-bus/)。
* toolearn 深入了解 Web 角色和背景工作角色，請參閱[背景工作角色](../fundamentals-introduction-to-azure.md#compute)。    
* toolearn 進一步了解虛擬區域網路，請參閱[虛擬網路](https://azure.microsoft.com/documentation/services/virtual-network/)。    
* toolearn 進一步了解備份及復原，請參閱[業務續航力](sql-database-business-continuity.md)。    
* toolearn 進一步了解監視 ppols，請參閱[監視集區](sql-database-elastic-pool-manage-portal.md)。    
* toolearn 深入了解 Umbraco 為服務時，請參閱[Umbraco](https://umbraco.com/cloud)。


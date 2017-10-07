---
title: "多租用戶 SaaS 應用程式和 Azure SQL Database 的 aaaDesign 模式 |Microsoft 文件"
description: "這篇文章討論 hello 需求和雲端環境中執行的多租用戶資料庫應用程式的常見資料架構模式需要 tooconsider hello 與這些模式相關的各種權衡取捨。 其中也說明 Azure SQL Database 搭配其彈性集區和彈性工具，如何在無需妥協的情況下滿足這些需求。"
keywords: 
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 1dd20c6b-ddbb-40ef-ad34-609d398d008a
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-design
ms.date: 02/01/2017
ms.author: srinia
ms.openlocfilehash: a4b58935b08cb78792e65a675d680de708b709fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multi-tenant-saas-applications-and-azure-sql-database"></a>多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式
在本文中，您可以了解 hello 需求和常見資料架構模式的多租用戶軟體即服務 (SaaS) 的資料庫應用程式在雲端環境中執行。 它也會說明 hello 因素，您需要 tooconsider 並 hello 不同的設計模式的取捨。 Azure SQL Database 中的彈性集區和彈性工具可協助您符合特定需求，而不會影響其他目標。

開發人員有時候做出選擇，他們設計租用戶模型為多租用戶應用程式的 hello 資料層時，對其利益長期工作。 一開始，最少，開發人員可能會對看待簡化開發和降低雲端服務提供者為租用戶隔離或 hello 應用程式延展性比更重要成本。 這項選擇可能會導致 toocustomer 滿意度考量和成本高昂的課程更正更新版本。

多租用戶應用程式是裝載在雲端環境中的應用程式，以及提供的 hello 相同設定的服務 toohundreds 或數千個租用戶共用或檢視彼此的資料。 範例會提供在雲端裝載環境中的服務 tootenants 的 SaaS 應用程式。

## <a name="multi-tenant-applications"></a>多租用戶應用程式
在多租用戶應用程式中，可以輕鬆分割資料和工作負載。 您可以分割資料和工作負載，例如，沿著租用戶界限，因為租用戶 hello 範圍內發生的大部分要求。 該屬性是固有的 hello 資料和 hello 工作負載，以及它喜好本文所討論的 hello 應用程式模式。

開發人員會使用這種類型的應用程式 hello 整個重量級的跨雲端架構應用程式，包括：

* 夥伴的資料庫應用程式正在進行轉換的 toohello 雲端做為 SaaS 應用程式
* 建立的接地 hello hello 雲端 SaaS 應用程式
* 直接面向客戶的應用程式
* 面向員工的企業應用程式

為夥伴的資料庫應用程式通常都是多租用戶應用程式專為 hello 雲端以及與根目錄的 SaaS 應用程式。 這些 SaaS 應用程式提供服務 tootheir 租用戶特定的軟體應用程式。 租用戶可以存取 hello 應用程式服務，並具有完整的擁有權的相關聯的資料儲存成 hello 應用程式的一部分。 但 tootake 利用的 SaaS，租用戶 hello 優點必須投降一些控制自己的資料。 就會信任 hello SaaS 服務提供者 tookeep 安全且與其他租用戶資料隔離其資料。 這類多租用戶 SaaS 應用程式的範例包括 MYOB、SnelStart 和 Salesforce.com。每一個這些應用程式可以分割沿著租用戶界限和我們在本文中討論支援 hello 應用程式設計模式。

提供工作導向服務 toocustomers 或 tooemployees （通常參照的 tooas 使用者，而非租用戶） 在組織中的應用程式會在 hello 多租用戶應用程式範圍的另一個類別目錄。 客戶訂閱 toohello 服務，並不是擁有 hello 服務提供者的 hello 資料收集和儲存。 服務提供者可比較不嚴謹需求 tookeep 超出政府託管隱私權法規彼此隔離客戶資料。 這種客戶對應的多租用戶應用程式範例包括 Netflix、Spotify 和 Xbox LIVE 等媒體內容提供者。 還有其他可輕鬆分割的應用程式範例，包括面向客戶的網際網路等級應用程式或物聯網 (IoT) 應用程式，其中每個客戶或裝置都可能成為分割區。 分割區界限可以劃分不同的使用者和裝置。

並非所有應用程式都可輕易地沿著單一屬性來分割，例如租用戶、客戶、使用者或裝置。 例如，複雜企業資源規劃 (ERP) 應用程式具有產品、訂單和客戶。 其通常使用具有數千個緊密相互連結資料表的複雜結構描述。

任何單一資料分割策略可以套用 tooall 資料表，並跨應用程式的工作負載。 本文所著重的多租用戶應用程式，具有可輕鬆分割的資料和工作負載。

## <a name="multi-tenant-application-design-trade-offs"></a>多租用戶應用程式設計取捨
多租用戶應用程式開發人員通常會選擇的 hello 設計模式根據下列因素的 hello 考量：

* **隔離租用戶**。 hello 開發人員必須 tooensure 沒有租用戶都有未經授權的存取 tooother 租用戶的資料。 hello 隔離需求擴充 tooother 屬性，例如在含有雜訊的鄰近項目從提供的保護，正在無法 toorestore 租用戶的資料和實作租用戶專屬的自訂。
* **雲端資源成本**。 SaaS 應用程式需要 toobe 成本競爭力。 多租用戶應用程式開發人員可能會選擇成本較低的 toooptimize hello 使用雲端資源，例如儲存體中，並計算成本。
* **簡化 DevOps**。 多租用戶應用程式開發人員需要 tooincorporate 隔離保護、 維護和監視其應用程式和資料庫結構描述，hello 健全狀況和租用戶的問題進行疑難排解。 應用程式開發和作業的複雜度會將轉譯直接 tooincreased 成本並與租用戶滿意度面臨的挑戰。
* **延展性**。 hello 能力 tooincrementally 新增更多的租用戶和租用戶需要它是命令式 tooa 成功 SaaS 運算的容量。

這些因素有取捨比較 tooanother。 供應項目可能不會提供最方便的方式開發經驗 hello hello 成本最低的雲端。 是很重要的開發人員 toomake hello 應用程式的設計程序期間將選擇了解這些選項，以及其缺點。

款知名開發模式是 toopack 成一個或少數幾個資料庫的多個租用戶。 hello 這個方法的優點是更低的成本，因為您支付一些資料庫和 hello 相對而言較為簡單的處理有限數目的資料庫。 但經過一段時間，SaaS 多租用戶應用程式開發人員將會瞭解，這項選擇在租用戶隔離和延展性方面有些缺點。 如果租用戶隔離變得很重要的其他的投入時間是必要的 tooprotect 租用戶資料未經授權的存取或在含有雜訊的鄰近項目從共用存放裝置中。 這項額外的付出可能會大幅提升開發工作和隔離維護成本。 同樣地，如果需要加入租用戶，這種設計模式通常需要專門技術 tooredistribute 租用戶資料整個資料庫 tooproperly 標尺 hello 資料層應用程式。  

租用戶隔離通常是在 SaaS toobusinesses 和組織，符合的多租用戶應用程式的基本需求。 開發人員在簡單性和成本考量方面短視近利，而不重視隔離和延展性。 這個取捨可以證明複雜且昂貴 hello 服務成長以及租用戶隔離需求變得更重要且受管理的 hello 應用程式層級。 不過，在多租用戶應用程式提供直接的消費者導向服務 toocustomers 租用戶隔離可能會比最佳化雲端資源的成本較低的優先順序。

## <a name="multi-tenant-data-models"></a>多租用戶資料模型
放置租用戶資料的常見設計做法都遵循這三種不同的模型 (如圖 1 所示)。

![多租用戶應用程式資料模型](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-multi-tenant-data-models.png)

圖 1︰多租用戶資料模型的常見設計做法

* **租用戶各有資料庫**。 每個租用戶都有自己的資料庫。 所有租用戶特定的資料是局部的 toohello 租用戶的資料庫，並與其他租用戶和其資料隔離。
* **共用資料庫 - 分區化**。 多個租用戶會共用多個資料庫的其中一個。 一組不同的租用戶指派 tooeach 資料庫使用資料分割策略，例如雜湊、 範圍或清單資料分割。 此資料散發策略通常是參照的 tooas 分區化。
* **共用資料庫 - 單一**。 單一資料庫 (有時很大) 包含以租用戶識別碼資料行來區分的所有租用戶的資料。

> [!NOTE]
> 應用程式開發人員可能會在不同的資料庫結構描述中，選擇 tooplace 不同的租用戶，然後使用 hello 結構描述名稱 toodisambiguate hello 不同的租用戶。 我們不建議這種方法，因此通常需要 hello 使用動態 SQL，它便無法在計畫快取中有效。 在這篇文章 hello 其餘部分，我們會著重在 hello 共用資料表方法，這個分類的多租用戶應用程式。
> 
> 

## <a name="popular-multi-tenant-data-models"></a>熱門的多租用戶資料模型
重要 tooevaluate hello 不同類型的多租用戶資料模型，以 hello 應用程式設計的利弊得失我們已識別出它。 這些因素協助歸納 hello 三個稍早所述最常見多租用戶資料模型和其資料庫使用，如圖 2 所示。

* **隔離**。 hello 程度租用戶之間可以是隔離的資料模型會達到多少租用戶隔離的量值。
* **雲端資源成本**。 hello 租用戶之間共用的資源數量可以最佳化雲端資源的成本。 資源可以定義為 hello 運算和儲存體成本。
* **DevOps 成本**。 hello 輕鬆的應用程式開發、 部署和管理能力會減少整體 SaaS 作業成本。  

在圖 2 hello Y 軸會顯示 hello 租用戶隔離層級。 hello X 軸會顯示 hello 層級的資源共用。 hello 灰色 hello 中間的對角線箭號表示 hello DevOps 成本，降低 tooincrease 或減少的方向。

![熱門的多租用戶應用程式設計模式](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-popular-application-patterns.png)

圖 2︰熱門的多租用戶資料模型

hello 右下方，在圖 2 顯示使用可能很大的共用單一資料庫的應用程式模式和 hello 共用資料表 （或另一個結構描述） 的方法。 是良好的資源共用，因為所有租用戶使用的 hello 相同資料庫在單一資料庫中的資源 （CPU、 記憶體、 輸入/輸出）。 但租用戶隔離有限。 您可能需要 tootake 額外的步驟 tooprotect 租用戶彼此 hello 應用程式層級。 下列額外步驟可能會大幅增加 hello DevOps 成本的開發和管理 hello 應用程式。 延展性受限於 hello 小數位數 hello 硬體裝載 hello 資料庫。

在圖 2 中的 hello 左下方象限說明跨多個資料庫分區化的多個租用戶 （一般而言，不同的硬體延展單位）。 每個資料庫主控租用戶，的子集哪些位址 hello 延展性問題的其他模式。 如果需要更多租用戶適用的更多容量，所以您可以輕鬆地配置 toonew 硬體擴充單元的新資料庫上放置 hello 租用戶。 不過，減少的資源共用的 hello 數量。 只有租用戶上放置 hello 相同延展單位共用資源。 此方法會提供一些改進 tootenant 隔離，因為多個租用戶的仍共置，而不會自動受到保護從其他的動作。 應用程式複雜度仍然很高。

在圖 2 中的 hello 左上方象限為 hello 第三種方法。 它將每個租用戶的資料放在自己的資料庫中。 這種方法有良好的租用戶隔離特性，但是當每個資料庫提供自己專用的資源時，就會限制資源共用。 如果所有租用戶有可預測的工作負載，這會是個好方法。 如果租用戶工作負載變得更難預測，hello 提供者不能最佳化資源共用。 不可預測性是 SaaS 應用程式一般的特性。 hello 提供者必須是過度佈建 toomeet 要求或較低的資源。 任何一個動作都會導致成本提高或租用戶滿意度降低。 較高的資源在租用戶之間共用變得更符合成本效益的理想 toomake hello 方案。 Hello 日益增加的資料庫也會增加 DevOps 成本 toodeploy，並維護 hello 應用程式。 儘管這些考量，這個方法會提供租用戶的 hello 最佳且最簡單隔離。

這些因素也會影響客戶選擇 hello 設計模式：

* **租用戶資料的擁有權**。 租用戶保留的自己的資料擁有權的應用程式偏好 hello 模式，每個租用戶的單一資料庫。
* **規模**。 以數十萬或數百萬個租用戶為目標的應用程式，應該選擇資料庫共用方法，例如分區化。 但仍可能要解決隔離需求。
* **價值和商務模型**。 如果應用程式的個別租用戶營收很少 (少於一美元)，隔離需求會變得較不重要，而共用資料庫會較有意義。 如果每個租用戶的營收只有數美元或更多金額，則租用戶各有資料庫模型比較可行。 它可能有助於降低開發成本。

理想的多租用戶模型提供 hello 設計的利弊得失圖 2 所示，與在租用戶之間共用的最佳資源需要 tooincorporate 良好的租用戶隔離屬性。 此模型可完全置於 hello 類別 hello 右上方之圖 2 中所述。

## <a name="multi-tenancy-support-in-azure-sql-database"></a>Azure SQL Database 中的多租用戶支援
Azure SQL Database 支援圖 2 所示的所有多租用戶應用程式模式。 彈性集區，它也支援的應用程式模式，它結合了很好的資源共用與 hello hello 資料庫每位租用戶隔離優點方法 （請參閱圖 3 中的 hello 右上方象限）。 彈性資料庫工具和 SQL Database 中的功能可協助減少 hello 成本 toodevelop 和操作多個資料庫 （圖 3 中的 hello 陰影區域中顯示） 的應用程式。 這些工具可協助您建立和管理應用程式使用任何 hello 多重資料庫模式。

![Azure SQL Database 中的模式](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-patterns-sqldb.png)

圖 3：Azure SQL Database 中的多租用戶應用程式模式

## <a name="database-per-tenant-model-with-elastic-pools-and-tools"></a>租用戶各有資料庫模型與彈性集區和工具
SQL Database 中的彈性集區會結合租用戶隔離的租用戶資料庫 toobetter 支援 hello 資料庫每個租用戶方法之間共用的資源。 SQL Database 是資料層方案，可供建置多租用戶應用程式的 SaaS 提供者使用。 在租用戶之間共用之資源的 hello 負擔切換 hello 應用程式層 toohello 資料庫服務層。 管理和跨資料庫查詢大規模 hello 複雜度經過簡化的彈性作業、 彈性的查詢、 彈性的交易，與 hello 彈性資料庫用戶端程式庫。

| 應用程式需求 | SQL Database 功能 |
| --- | --- |
| 租用戶隔離與資源共用 |[彈性集區](sql-database-elastic-pool.md)： 配置的 SQL Database 資源集區，並跨各種資料庫共用 hello 資源。 此外，個別的資料庫可以繪製一樣多的資源從 hello 集區為所需的 tooaccommodate 容量增到期 toochanges 在租用戶工作負載。 本身的 hello 彈性集區可以調整向上或向下所需。 彈性集區也提供了易於管理和監視和疑難排解 hello 集區層級。 |
| 跨資料庫簡化 DevOps |[彈性集區](sql-database-elastic-pool.md)︰如先前所述。 |
| | [彈性查詢](sql-database-elastic-query-horizontal-partitioning.md)︰跨資料庫查詢以進行報告或跨租用戶分析。 |
| | [彈性作業](sql-database-elastic-jobs-overview.md)： 封裝及可靠地部署資料庫維護作業，或資料庫結構描述變更 toomultiple 資料庫。 |
| | [彈性交易](sql-database-elastic-transactions-overview.md): 不可部分完成及隔離的方式變更 tooseveral 資料庫的程序。 當應用程式在數個資料庫作業之間需要保證「全有或全無」時，就需要彈性交易。 |
| | [彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)： 管理資料分佈，以及對應的租用戶 toodatabases。 |

## <a name="shared-models"></a>共用的模型
如先前所述，大多數 SaaS 提供者的共用模型方法可能會引起租用戶隔離問題，以及應用程式開發和維護的複雜性。 不過，對於直接 tooconsumers，租用戶提供服務的多租用戶應用程式隔離需求可能不是做為最小化成本最高優先順序。 可能會無法 toopack 級較高的密度 tooreduce 成本的一或多個資料庫中的租用戶。 使用單一資料庫或多個分區化資料庫的共用資料庫模型，可以提高資源共用和整體成本的效率。 Azure SQL Database 提供一些功能，協助客戶建置提升的安全性和管理大規模 hello 資料層中的隔離。

| 應用程式需求 | SQL Database 功能 |
| --- | --- |
| 安全性隔離功能 |[資料列層級安全性](https://msdn.microsoft.com/library/dn765131.aspx) |
| [資料庫結構描述](https://msdn.microsoft.com/library/dd207005.aspx) | |
| 跨資料庫簡化 DevOps |[彈性查詢](sql-database-elastic-query-horizontal-partitioning.md) |
| | [彈性工作](sql-database-elastic-jobs-overview.md) |
| | [彈性交易](sql-database-elastic-transactions-overview.md) |
| | [彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md) |
| | [彈性資料庫分割和合併](sql-database-elastic-scale-overview-split-and-merge.md) |

## <a name="summary"></a>摘要
對於大多數 SaaS 多租用戶應用程式而言，租用戶隔離需求很重要。 hello 最佳選項 tooprovide 隔離大量 leans 朝 hello 資料庫每個租用戶的方法。 hello 其他兩種方法需要複雜的應用程式層級需要技術的開發人員 tooprovide 隔離，它會大幅增加成本和風險的投資。 如果隔離需求不計算在 hello 服務開發的早期，它們的更動而可能會更高 hello 前兩個模型中。 hello 與 hello 每個租用戶的資料庫模型相關聯的主要缺點是相關的 tooincreased 雲端資源成本，因為 tooreduced 共用、 維護和管理多個資料庫。 SaaS 應用程式開發人員經常掙扎於這些取捨之中。

雖然取捨可能與大部分的雲端資料庫服務提供者的重大障礙，Azure SQL Database 會消除 hello 障礙的彈性集區和彈性資料庫功能。 SaaS 開發人員可以結合 hello 隔離特性的每個租用戶的資料庫模型，並最佳化資源共用及 hello 管理性增強功能，許多資料庫的使用彈性集區和相關聯的工具。

沒有租用戶隔離需求，並能以高密度將租用戶封裝在資料庫中的多租用戶應用程式提供者，可能會發現共用資料模型可以提高資源共用的效率，並能降低整體成本。 Azure SQL Database 彈性資料庫工具、分區化程式庫和安全性功能，可協助 SaaS 提供者建置和管理多租用戶應用程式。

## <a name="next-steps"></a>後續步驟
[開始使用彈性資料庫工具](sql-database-elastic-scale-get-started.md)與範例應用程式，示範 hello 用戶端程式庫。

透過使用彈性集區的範例應用程式，建立 [SaaS 的彈性集區自訂儀表板](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools-custom-dashboard) ，以建置符合成本效益、可調整的資料庫解決方案。

也使用 hello Azure SQL Database 工具[移轉現有的資料庫 tooscale 出](sql-database-elastic-convert-to-use-elastic-tools.md)。

彈性集區使用 toocreate hello Azure 入口網站，請參閱[建立彈性集區](sql-database-elastic-pool-manage-portal.md)。  

了解如何太[監視和管理彈性集區](sql-database-elastic-pool-manage-portal.md)。

## <a name="additional-resources"></a>其他資源

* [部署及探索使用 Azure SQL Database 的多租用戶應用程式 - Wingtip SaaS](sql-database-saas-tutorial.md)
* [什麼是 Azure 彈性集區？](sql-database-elastic-pool.md)
* [使用 Azure SQL Database 相應放大](sql-database-elastic-scale-introduction.md)
* [使用彈性資料庫工具和資料列層級安全性的多租用戶應用程式](sql-database-elastic-tools-multi-tenant-row-level-security.md)
* [使用 Azure Active Directory 和 OpenID Connect 在多租用戶應用程式中進行驗證](../guidance/guidance-multitenant-identity-authenticate.md)
* [Tailspin Surveys 應用程式](../guidance/guidance-multitenant-identity-tailspin.md)


## <a name="questions-and-feature-requests"></a>問題和功能要求

如有問題，請造訪我們在 hello [SQL Database 論壇](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)。 在 hello 中加入功能要求[SQL Database 意見反應論壇](https://feedback.azure.com/forums/217321-sql-database/)。


---
title: "使用 Azure SQL Database 出 aaaScaling |Microsoft 文件"
description: "軟體即服務 (SaaS) 開發人員可以輕鬆地建立彈性、 可擴充的資料庫中 hello 雲端使用這些工具"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: d15a2e3f-5adf-41f0-95fa-4b945448e184
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 82a561e07389d8619727a540fa9424248c087eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-out-with-azure-sql-database"></a>使用 Azure SQL Database 相應放大
您可以輕鬆地向外擴充 Azure SQL database 使用 hello**彈性資料庫**工具。 這些工具和功能可讓您使用 hello 幾乎不受限制資料庫的資源**Azure SQL Database** toocreate 解決方案交易式工作負載，以及特別是軟體即服務 (SaaS) 應用程式。 彈性資料庫功能所組成 hello 下列：

* [彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md): hello 用戶端程式庫是一項功能，可讓您 toocreate 和維護分區化資料庫。  請參閱 [開始使用彈性資料庫工具](sql-database-elastic-scale-get-started.md)。
* [彈性資料庫分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md)︰在分區化資料庫之間移動資料。 這可用於將資料從多租用戶資料庫 tooa 單一租用戶資料庫 （或反之亦然）。 請參閱 [彈性資料庫分割合併工具教學課程](sql-database-elastic-scale-configure-deploy-split-and-merge.md)。
* [彈性資料庫工作](sql-database-elastic-jobs-overview.md)（預覽）： 使用工作 toomanage 大量的 Azure SQL 資料庫。 輕鬆執行系統管理作業，例如結構描述變更、認證管理、參考資料更新、效能資料收集，或使用工作的租用戶 (客戶) 遙測收集。
* [彈性資料庫查詢](sql-database-elastic-query-overview.md)（預覽）： 可讓您跨越多個資料庫的 toorun Transact SQL 查詢。 這可讓連線 tooreporting 工具，例如 Excel、 power Bi、 Tableau 等等。
* [彈性交易](sql-database-elastic-transactions-overview.md)： 這項功能可讓您跨越 Azure SQL Database 中的多個資料庫的 toorun 交易。 彈性資料庫交易適用於.NET 應用程式使用 ADO.NET 和整合與 hello 熟悉的程式設計體驗使用 hello [System.Transaction 類別](https://msdn.microsoft.com/library/system.transactions.aspx)。

hello 下圖顯示架構，其中包括 hello**彈性資料庫功能**關聯 tooa 集合的資料庫中。

此圖中的 hello 資料庫色彩表示結構描述。 資料庫與 hello 相同的色彩共用 hello 相同的結構描述。

1. 一組 **Azure SQL 資料庫** 使用分區化架構裝載於 Azure 中。
2. hello**彈性資料庫用戶端程式庫**設定使用的 toomanage 分區。
3. Hello 資料庫子集會放入**彈性集區**。 (請參閱 [何謂集區？](sql-database-elastic-pool.md))。
4. **彈性資料庫工作** 會針對所有資料庫執行排定的或 ad-hoc T-SQL 指令碼。
5. hello**分割合併工具**是從一個分區 tooanother 使用的 toomove 資料。
6. hello**彈性資料庫查詢**可讓您 toowrite 跨越 hello 分區集內的所有資料庫的查詢。
7. **彈性交易**可讓您跨越多個資料庫的 toorun 交易。 

![彈性資料庫工具][1]

## <a name="why-use-hello-tools"></a>為何要使用 hello 工具？
已簡單達成雲端應用程式在 VM和 Blob 儲存體方面的彈性和縮放 -- 增加或減少單位，或增加電源即可。 但對於關聯式資料庫中可設定狀態的資料處理，仍然是個挑戰。 在這些情況下出現的挑戰：

* 擴充和縮減容量 hello 關聯式資料庫工作負載的一部分。
* 管理可能會影響特定資料子集的作用區 - 例如特別忙碌的終端客戶 (租用戶)。

傳統上，這類案例已經解決的投資大規模的資料庫伺服器 toosupport hello 應用程式中。 不過，此選項會受到限制，其中的所有處理都發生在預先定義的商用硬體的 hello 雲端中。 相反地，將資料散發和程序跨越多個具有相同結構化的資料庫 （向外延展模式又稱為 「 分區化 」） 提供替代 tootraditional 成本和彈性方面的向上延展方法。

## <a name="horizontal-and-vertical-scaling"></a>水平和垂直縮放
hello 圖會顯示 hello 這種 hello 基本 hello 彈性資料庫可以調整水平和垂直維度的縮放比例。

![水平與垂直相應放大][2]

水平調整指的是 tooadding 或移除資料庫中順序 tooadjust 容量或整體效能。 這也稱為「相應放大」。 分區化中，資料分割之間的結構都完全相同的資料庫集合是常見的方式 tooimplement 水平縮放比例。  

垂直縮放比例是指 tooincreasing 或減少 hello 的個別資料庫的效能層級，這也稱為 「 向上擴充。 」

大部分雲端級別的資料庫應用程式都採用這些兩種策略的組合。 例如，軟體即服務應用程式可能使用水平縮放 tooprovision 新客戶] 和 [垂直調整 tooallow 每個結束-客戶資料庫 toogrow 或壓縮資源所 hello 工作負載。

* 水平延展使用 hello 管理[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)。
* 垂直縮放比例會藉由 Azure PowerShell cmdlet toochange hello 服務層，或將資料庫放在彈性集區。

## <a name="sharding"></a>分區化
*分區化*跨多個獨立的資料庫是技術 toodistribute 大量的相同結構化資料。 為一般客戶或企業建立軟體即服務 (SAAS) 供應項目的開發人員尤其愛用。 這些客戶通常會參考的 tooas 「 租用 」。 需要使用分區化可能有各種原因：  

* hello 的資料量總計是太大 toofit hello 條件約束的單一資料庫內
* hello 交易輸送量的 hello 整體工作負載超過單一資料庫的 hello 功能
* 租用戶可能需要彼此實際隔離，因此每個租用戶需要個別的資料庫
* 資料庫的各區段可能需要 tooreside 中不同的地理位置的相容性、 效能或地理政治的原因。

在其他案例，例如擷取的資料，並從分散式裝置分區化可能會使用的 toofill 一組會組織在暫時的資料庫。 例如，個別的資料庫可以專門 tooeach 天或週。 在此情況下，hello 分區化索引鍵可以是整數代表 hello 日期 （若出現在 hello 分區化資料表的所有資料列） 和擷取日期範圍內的資訊的查詢必須路由傳送的 hello 應用程式 toohello 涵蓋 hello 範圍中的資料庫子集問題。

分區化最適合應用程式中的每筆交易可以限制的 tooa 單一分區化索引鍵的值。 這可確保所有交易都可本機 tooa 特定資料庫。

## <a name="multi-tenant-and-single-tenant"></a>多租用戶和單一租用戶
有些應用程式會使用每個租用戶建立不同的資料庫中的 hello 最簡單的方式。 這是 hello**單一租用戶分區化模式**，提供隔離、 備份/還原功能與調整 hello hello 租用戶的資料粒度的資源。 單一租用戶分區化中，每個資料庫都與特定租用戶識別碼值 （或客戶的機碼值），但該金鑰需要不一定會出現在 hello 資料本身。 它是 hello 應用程式的責任 tooroute 每個要求 toohello 適當的資料庫-和 hello 用戶端程式庫可簡化這行。

![單一租用戶與多租用戶][4]

其他案例將多個租用戶一起放入資料庫中，而不是將它們隔離至個別的資料庫。 這是一般**多租用戶分區化模式**-和它可能會驅動應用程式管理大量的非常小的租用戶的 hello 事實。 在多租用戶分區化中，hello hello 資料庫資料表中的資料列會是所有設計 toocarry 找出 hello 租用戶識別碼或分區化索引鍵的索引鍵。 同樣地，hello 應用程式層會負責路由租用戶的要求 toohello 適當的資料庫，並支援此 hello 彈性資料庫用戶端程式庫。 此外，資料列層級安全性可以是資料列可以存取的每個租用戶-如需詳細資訊，請參閱 < 使用的 toofilter[多租用戶應用程式的彈性資料庫工具和資料列層級安全性](sql-database-elastic-tools-multi-tenant-row-level-security.md)。 轉散發資料庫之間的資料時可能需要與 hello 多租用戶分區化模式，而且這透過實現 hello 彈性資料庫分割合併工具。 toolearn 有關使用彈性集區，SaaS 應用程式的設計模式的詳細資訊請參閱[設計模式為多租用戶 SaaS 應用程式使用 Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md)。

### <a name="move-data-from-multiple-toosingle-tenancy-databases"></a>將資料從多個 toosingle 租用戶資料庫移動
在建立 SaaS 應用程式，最好是一般 toooffer 潛在客戶試用版的 hello 軟體。 在此情況下，它是符合成本效益 toouse hello 資料的多租用戶資料庫。 不過，當潛在客戶變成真正客戶時，單一租用戶資料庫就比較好，因為提供更好的效能。 如果 hello 客戶 hello 試用期間建立的資料，使用 hello[分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md)toomove hello 多租用戶 toohello 新單一租用戶資料庫中的 hello 資料。

## <a name="next-steps"></a>後續步驟
範例應用程式，示範 hello 用戶端程式庫，請參閱[彈性資料庫 tools 快速入門](sql-database-elastic-scale-get-started.md)。

tooconvert 現有資料庫 toouse hello 工具，請參閱[移轉現有的資料庫 tooscale 外](sql-database-elastic-convert-to-use-elastic-tools.md)。

toosee hello 細節 hello 彈性集區，請參閱[彈性集區的價格和效能考量](sql-database-elastic-pool.md)，或建立新的集區與[彈性集區](sql-database-elastic-pool-manage-portal.md)。  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-introduction/tools.png
[2]:./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]:./media/sql-database-elastic-scale-introduction/overview.png
[4]:./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png


---
title: "aaaManaging 向外延展雲端資料庫 |Microsoft 文件"
description: "說明 hello 彈性資料庫工作服務"
metakeywords: azure sql database elastic databases
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 6fa47cf2-1162-4534-a206-6e2d95b78580
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: b6d330cd712421b8cba781e835830772e6e5b77e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-scaled-out-cloud-databases"></a>管理相應放大的雲端資料庫
toomanage 向外延展分區化資料庫 hello**彈性資料庫工作**功能 （預覽） 可讓您 tooreliably 整個群組的資料庫，包括執行 TRANSACT-SQL (T-SQL) 指令碼：

* 自訂的資料庫集合 (如下所述)
* [彈性集區](sql-database-elastic-pool.md)中的所有資料庫
* 分區集 (使用 [彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)建立)。 

## <a name="documentation"></a>文件
* [安裝 hello 彈性資料庫工作元件](sql-database-elastic-jobs-service-installation.md)。 
* [開始使用彈性資料庫工作](sql-database-elastic-jobs-getting-started.md)。
* [使用 Powershell 建立和管理工作](sql-database-elastic-jobs-powershell.md)。
* [建立和管理相應放大的 Azure SQL Database](sql-database-elastic-jobs-getting-started.md)

**彈性資料庫工作**是目前的客戶裝載 Azure 雲端服務，可讓 hello 執行臨機操作方式與排程的管理工作，稱為**作業**。 工作進行，您可以輕易及可靠地管理大量的 Azure SQL Database 執行 TRANSACT-SQL 指令碼 tooperform 系統管理作業。 

![彈性資料庫工作服務][1]

## <a name="why-use-jobs"></a>為何要使用工作？
**管理**

輕鬆執行結構描述變更、認證管理、參考資料更新、效能資料收集，或租用戶 (客戶) 遙測收集。

**報告**

將 Azure SQL Database 集合中的資料彙總到單一目的地資料表中。

**減少額外負荷**

一般來說，您必須連接 tooeach 順序 toorun TRANSACT-SQL 陳述式中獨立的資料庫或執行其他管理工作。 作業會處理 hello tooeach hello 目標群組中的資料庫中記錄的工作。 也定義、 維護和持續的 Azure SQL Database 執行 TRANSACT-SQL 指令碼 toobe。

**資料記錄**

工作執行的每個資料庫執行的 hello 指令碼和記錄 hello 狀態。 失敗時也會自動重試。

**彈性**

定義 Azure SQL Database 的自訂群組，並定義排程以執行工作。

> [!NOTE]
> Hello Azure 入口網站，只會造成有限函式之一組經過簡化的 tooSQL Azure 彈性集區可供使用。 使用 hello PowerShell Api tooaccess hello 整組目前的功能。
> 
> 

## <a name="applications"></a>應用程式
* 執行管理工作，例如部署新的結構描述。
* 更新所有資料庫通用的產品資料參考資訊。 或排程每個工作日數小時後的自動更新。
* 重建索引 tooimprove 查詢效能。 hello 重建也有設定的 tooexecute 集合的資料庫重複執行，例如在離峰時間。
* 以持續執行的基礎從一組資料庫將查詢結果收集至中央資料表。 效能的查詢可以持續執行，而且設定 tootrigger 其他工作 toobe 執行。
* 跨資料庫的大型集合執行長時間執行的資料處理查詢，例如 hello 客戶遙測的集合。 結果會收集到單一目的地資料表做進一步的分析。

## <a name="elastic-database-jobs-end-to-end"></a>彈性資料庫工作：端對端
1. 安裝 hello**彈性資料庫工作**元件。 如需詳細資訊，請參閱 [安裝彈性資料庫工作](sql-database-elastic-jobs-service-installation.md)。 如果 hello 安裝失敗，請參閱[如何 toouninstall](sql-database-elastic-jobs-uninstall.md)。
2. 使用 PowerShell Api tooaccess hello 更多的功能，例如建立自訂的資料庫集合，新增排程和/或收集結果集。 使用 hello 入口網站進行簡單的安裝和建立/監視作業受限於針對 tooexecution**彈性集區**。 
3. 建立工作執行的加密的認證及[hello 群組中加入 hello tooeach 資料庫使用者 （或角色）](sql-database-security-overview.md)。
4. 建立具有等冪性能夠針對 hello 群組中每個資料庫來執行的 T-SQL 指令碼。 
5. 請遵循這些步驟 toocreate 作業使用 hello Azure 入口網站：[建立及管理彈性資料庫工作](sql-database-elastic-jobs-create-and-manage.md)。 
6. 或使用 PowerShell 指令碼： [使用 PowerShell 建立和管理 SQL Database 彈性資料庫工作 (預覽)](sql-database-elastic-jobs-powershell.md)。

## <a name="idempotent-scripts"></a>等冪指令碼
hello 指令碼必須是[等冪](https://en.wikipedia.org/wiki/Idempotence)。 簡單地說，「 具有等冪性 」 表示，如果 hello 指令碼成功，而且會再次執行，hello 發生相同的結果。 指令碼可能會 tootransient 網路問題而失敗。 在此情況下，hello 作業將自動重試執行 hello 指令碼之前 desisting 預設次數。 具有等冪性指令碼有結果即使已成功地執行兩次相同的 hello。 

簡單的策略是物件的 tootest hello 存在之前建立。  

    IF NOT EXIST (some_object)
    -- Create hello object 
    -- If it exists, drop hello object before recreating it.

同樣地，指令碼必須能夠 tooexecute 已成功由邏輯測試，指出任何條件找到。

## <a name="failures-and-logs"></a>失敗和記錄檔
如果指令碼失敗多次嘗試之後，hello 作業記錄 hello 錯誤並繼續。 工作結束之後 （表示針對 hello 群組中的所有資料庫的執行），您可以檢查其失敗次數的清單。 hello 記錄檔提供 toodebug 故障指令碼的詳細資料。 

## <a name="group-types-and-creation"></a>群組類型和建立
群組有兩種： 

1. 分區集
2. 自訂群組

分區集群組會建立使用 hello[彈性資料庫工具](sql-database-elastic-scale-introduction.md)。 當您建立的分區集群組時，資料庫會加入或自動從 hello 群組中移除。 例如，新的分區都會自動 hello 群組中時加入 toohello 分區對應。 然後可以針對 hello 群組執行作業。

自訂群組，hello 另一方面，嚴格定義。 您必須在自訂群組中明確地加入或移除資料庫。 如果 hello 群組中的資料庫已卸除，hello 作業將會嘗試針對最終的失敗所導致的 hello 資料庫 toorun hello 指令碼。 目前使用 hello Azure 入口網站所建立的群組是自訂的群組。 

## <a name="components-and-pricing"></a>元件和價格
hello 下列元件一起運作 toocreate Azure 雲端服務，可讓系統管理工作的特定執行。 hello 元件安裝和設定會自動在安裝期間，您的訂用帳戶中。 您可以識別 hello 服務，因為它們都有 hello 相同自動產生名稱。 hello 名稱會是唯一的並且包含 hello 前置詞"edj"後面接著隨機產生為 21 個字元。

* **Azure 雲端服務**： 彈性資料庫作業 （預覽） 提供的客戶裝載 Azure 雲端服務 hello tooperform 執行要求的工作。 Hello 入口網站中，從 hello 服務是部署，並裝載於 Microsoft Azure 訂用帳戶。 hello 預設部署服務會執行與 hello 的高可用性的兩個背景工作角色的最小值。 A0 執行個體上，執行每個工作者角色 (ElasticDatabaseJobWorker) hello 預設大小。 如需價格，請參閱 [雲端服務價格](https://azure.microsoft.com/pricing/details/cloud-services/)。 
* **Azure SQL Database**: hello 服務會使用稱為 hello Azure SQL Database**控制資料庫**toostore 所有 hello 工作中繼資料。 hello 預設服務層為 S0。 如需價格，請參閱 [SQL Database 價格](https://azure.microsoft.com/pricing/details/sql-database/)。
* **Azure 服務匯流排**: Azure 服務匯流排適用於協調的 hello hello Azure 雲端服務內的工作。 請參閱 [服務匯流排價格](https://azure.microsoft.com/pricing/details/service-bus/)。
* **Azure 儲存體**： 使用 Azure 儲存體帳戶 toostore 診斷輸出的登入問題需要進一步偵錯的 hello 事件 (請參閱[在 Azure 雲端服務和虛擬機器中啟用診斷](../cloud-services/cloud-services-dotnet-diagnostics.md))。 如需價格，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/)。

## <a name="how-elastic-database-jobs-work"></a>彈性資料庫工作的運作方式
1. Azure SQL Database 會指定 **控制資料庫** ，它會儲存所有中繼資料和狀態資料。
2. hello 控制資料庫存取 hello**工作服務**toolaunch 及追蹤工作 tooexecute。
3. 兩個不同的角色與 hello 控制資料庫通訊： 
   * 控制站： 判斷哪些作業需要工作 tooperform hello 要求藉由建立新的 「 作業 」 工作的作業，以及重試失敗的作業。
   * 工作執行作業： Hello 作業 」 工作執行。

### <a name="job-task-types"></a>工作作業類型
有多種類型的工作作業會執行工作：

* ShardMapRefresh： 查詢 hello 分區對應 toodetermine hello 的所有資料庫都做為分區
* ScriptSplit： 會 'GO' 陳述式批次分割 hello 指令碼
* ExpandJob：從以資料庫群組為目標的工作，針對每個資料庫建立子工作
* ScriptExecution：使用定義的認證針對特定資料庫執行指令碼
* Dacpac： 適用於 DACPAC tooa 特定資料庫使用特定的認證

## <a name="end-to-end-job-execution-work-flow"></a>端對端工作執行工作流程
1. 使用 hello 入口網站或 PowerShell API hello，作業會插入至 hello**控制資料庫**。 hello 作業會要求針對一組資料庫時使用特定認證的 TRANSACT-SQL 指令碼執行。
2. hello 控制器識別 hello 新工作。 作業 」 工作會建立並執行 toosplit hello 指令碼和 toorefresh hello 群組的資料庫。 最後，新的工作會建立和執行 tooexpand hello 作業，並建立新的子工作，其中每項子工作是指定的 tooexecute hello 針對個別資料庫 hello 群組中的 TRANSACT-SQL 指令碼。
3. hello 控制器識別 hello 建立子工作。 每個工作中，hello 控制站會建立，並觸發作業工作 tooexecute hello 指令碼，對資料庫。 
4. 完成所有作業 」 工作後，hello 控制器更新 hello 作業 tooa 都完成狀態。 
   在作業執行期間的任何時間點，hello PowerShell 應用程式開發介面可以是使用的 tooview hello 的作業執行的目前狀態。 所有時間都傳回的 hello PowerShell Api 以 UTC 表示。 如有需要，取消要求可以發出的 toostop 作業。 

## <a name="next-steps"></a>後續步驟
[安裝 hello 元件](sql-database-elastic-jobs-service-installation.md)，然後[建立並加入 tooeach hello 群組的資料庫中的資料庫中的記錄檔](sql-database-manage-logins.md)。 toofurther 了解作業的建立和管理，請參閱[建立及管理彈性資料庫工作](sql-database-elastic-jobs-create-and-manage.md)。 另請參閱 [開始使用彈性資料庫工作](sql-database-elastic-jobs-getting-started.md)。

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->



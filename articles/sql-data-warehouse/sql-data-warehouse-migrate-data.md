---
title: "aaaMigrate 您資料 tooSQL 資料倉儲 |Microsoft 文件"
description: "移轉您的資料 tooAzure SQL 資料倉儲來開發方案的提示。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a>移轉資料
資料可以藉由各種工具，從不同的來源移到您的「SQL 資料倉儲」中。  ADF 複製、 SSIS 和 bcp 因素都可使用的 tooachieve 此目標。 不過，hello 資料量增加時應考慮分解成步驟 hello 資料移轉程序。 這可以提供您 hello 機會 toooptimize 的效能與可靠度 tooensure smooth 資料移轉的每個步驟。

第一次這篇文章會討論 ADF 複製、 SSIS 和 bcp hello 簡單的移轉案例。 它然後看起來更到 hello 移轉可以最佳化的方式。

## <a name="azure-data-factory-adf-copy"></a>Azure Data Factory (ADF) 複製
[ADF 複製][ADF Copy]是 [Azure Data Factory][Azure Data Factory] 的一部分。 您可以使用 ADF 複製 tooexport 資料 tooflat 檔案位於本機儲存體，tooremote 一般檔案保留在 Azure blob 儲存體，或直接將 SQL 資料倉儲。

如果在一般檔案中，啟動您的資料，則您首先需要 tootransfer 它 tooAzure 儲存體 blob，才能起始載入到 SQL 資料倉儲。 一旦 hello 資料傳輸到 Azure blob 儲存體，您可以選擇 toouse [ADF 複製][ ADF Copy]再次 toopush hello 資料到 SQL 資料倉儲。

PolyBase 還提供高效能選項 hello 資料載入。 不過，這表示要使用兩種工具，而不止一種工具。 如果您需要 hello 達到最佳效能，請使用 PolyBase。 如果您想要的單一工具體驗 （和 hello 資料不是大量） ADF 是您的答案。


> 
> 

透過下列某些優越的文章 toohello 前端[ADF 範例][ADF samples]。

## <a name="integration-services"></a>Integration Services
Integration Services (SSIS) 是一個功能強大且靈活的擷取轉換和載入 (ETL) 工具，支援複雜的工作流程、資料轉換，以及數個資料載入選項。 使用 SSIS toosimply 傳輸資料 tooAzure 或是更廣泛的移轉的一部分。

> [!NOTE]
> SSIS 可以匯出 tooUTF-8 沒有 hello 檔案中的 hello 位元組順序標記。 您必須先使用 hello 這衍生資料行元件 tooconvert hello 中的字元資料的 tooconfigure hello 資料流程 toouse hello 65001 utf-8 字碼頁。 一旦已轉換 hello 資料行，將寫入 hello 資料 toohello 一般檔案目的地配接器確保 65001 為 hello hello 檔案的字碼頁中也已選取。
> 
> 

SSIS 連接 tooSQL 資料倉儲，就如同其所要連接 tooa SQL Server 部署。 不過，您的連線需要 toobe 使用 ADO.NET 連接管理員。 您應該也要負責 tooconfigure hello"的話就使用大量插入 」 設定 toomaximize 輸送量。 請參閱 toohello [ADO.NET 目的地配接器][ ADO.NET destination adapter]文章 toolearn 更多關於此屬性

> [!NOTE]
> 不支援使用 OLEDB 連接 tooAzure SQL 資料倉儲。
> 
> 

此外，總是會 hello 可能性封裝可能會失敗，因為 toothrottling 或網路問題。 設計封裝，讓他們可以繼續在 hello 失敗點，而不重做 hello 失敗前完成的工作。

如需詳細資訊，請參閱 hello [SSIS 文件][SSIS documentation]。

## <a name="bcp"></a>bcp
bcp 是專為一般檔案資料匯入和匯出所設計的命令列公用程式。 資料匯出期間可能進行某些轉換。 使用查詢 tooselect tooperform 簡單轉換，並轉換 hello 資料。 一旦匯出，然後可以載入 hello 一般檔案直接到 hello 目標 hello SQL 資料倉儲資料庫。

> [!NOTE]
> 它通常是個不錯的主意 tooencapsulate hello hello 來源系統上的檢視匯出資料期間所使用的轉換。 這可確保 hello 邏輯會保留，但 hello 程序可重複。
> 
> 

bcp 的優點包括：

* 簡單。 會簡單 toobuild bcp 命令，並執行
* 可重新啟動的載入程序。 一次匯出的 hello 負載可能會執行任何次數

bcp 的限制包括：

* bcp 只能使用列表式一般檔案。 無法使用 xml 或 JSON 之類的檔案
* 資料轉換功能只有有限的 toohello 匯出階段，而簡單的本質
* bcp 已調整的 toobe 強固時將資料載入透過 hello 網際網路。 任何網路不穩定狀況都可能造成載入錯誤。
* bcp 依賴出現在 hello 目標資料庫預先 toohello 負載中的 hello 結構描述

如需詳細資訊，請參閱[使用 bcp tooload 資料到 SQL 資料倉儲][Use bcp tooload data into SQL Data Warehouse]。

## <a name="optimizing-data-migration"></a>最佳化資料移轉
SQLDW 資料移轉程序可以有效地分成三個獨立的步驟：

1. 匯出來源資料
2. 傳輸的資料 tooAzure
3. 載入 hello 目標 SQLDW 資料庫

每個步驟可以是個別最佳化的 toocreate 達到最大效能，在每個步驟的強固、 重新啟動且有彈性的移轉程序。

## <a name="optimizing-data-load"></a>最佳化資料載入
查看這些以反向順序的時間。hello 最快方式 tooload 資料是透過 PolyBase。 PolyBase 載入程序最佳化放置於必要條件 hello 先前步驟是最佳 toounderstand 這前方。 如下：

1. 資料檔案的編碼
2. 資料檔案的格式
3. 資料檔案的位置

### <a name="encoding"></a>編碼
PolyBase 需要資料檔案 toobe utf-8 或 UTF-16 16FE。 



### <a name="format-of-data-files"></a>資料檔案的格式
PolyBase 規定要有固定的資料列結束字元 \n 或新行。 您的資料檔案都必須符合 toothis 標準。 字串或資料行結束字元沒有任何限制。

您必須 toodefine 每個資料行 hello 檔案中做為外部資料表中 PolyBase 的一部分。 請確定所有匯出的資料行所需，且 hello 類型符合所需的 toohello 標準。

請參閱上一步 toohello [移轉您的結構描述] 文件以取得有關支援的資料類型的詳細資料。

### <a name="location-of-data-files"></a>資料檔案的位置
SQL 資料倉儲以獨佔方式使用 PolyBase tooload 資料從 Azure Blob 儲存體。 因此，hello 資料必須已先傳送到 blob 儲存體。

## <a name="optimizing-data-transfer"></a>最佳化資料傳輸
Hello 傳送嗨資料 tooAzure hello 名最慢的部分資料移轉的其中一個。 不只網路頻寬可能是個問題，網路可靠性也可能嚴重阻礙進度。 預設情況下移轉資料 tooAzure 是透過 hello 網際網路因此 hello 發生可能相當的傳輸錯誤的機會。 不過，這些錯誤可能需要重新傳送整個或部分資料 toobe。

幸運的是您有數個選項 tooimprove hello 速度和恢復功能，此程序：

### <a name="expressrouteexpressroute"></a>[ExpressRoute][ExpressRoute]
您可以使用 tooconsider [ExpressRoute] [ ExpressRoute] toospeed hello 傳輸設定。 [ExpressRoute] [ ExpressRoute]提供您已建立私人連線 tooAzure 讓 hello 連接不會通過 hello 公用網際網路。 這絕不是必要的步驟。 不過，它將會改善輸送量時發送資料 tooAzure 從內部部署或共置設備。

hello 優點[ExpressRoute] [ ExpressRoute]是：

1. 更高的可靠性
2. 更快的網路速度
3. 更短的網路延遲
4. 更高的網路安全性

[ExpressRoute] [ ExpressRoute]很有幫助的案例數目，不只是 hello 移轉。

有興趣嗎？ 如需詳細資訊，請定價請瀏覽 hello [ExpressRoute 文件][ExpressRoute documentation]。

### <a name="azure-import-and-export-service"></a>Azure 匯入和匯出服務
hello Azure 匯入和匯出服務是針對大型 （GB + +） toomassive （TB + +） 的資料傳輸至 Azure 的資料傳輸程序。 它牽涉到撰寫資料 toodisks 和傳送它們 tooan Azure 資料中心。 然後會代替您到 Azure 儲存體 Blob 載入 hello 磁碟內容。

Hello 匯入匯出程序的高層級檢視如下所示：

1. 設定 Azure Blob 儲存體容器 tooreceive hello 資料
2. 匯出資料 toolocal 儲存體
3. 複製 hello 資料 too3.5 英吋 SATA II/III 硬碟機使用 hello [Azure 匯入/匯出工具]
4. 建立使用 hello Azure 匯入和匯出的服務提供 hello [Azure 匯入/匯出工具] 所產生的 hello 日誌檔案匯入工作
5. 寄送 hello 磁碟機指定 Azure 資料中心
6. 您的資料會傳送的 tooyour Azure Blob 儲存體容器
7. Hello 資料載入 SQLDW 使用 PolyBase

### <a name="azcopyazcopy-utility"></a>[AZCopy][AZCopy] 公用程式
hello [AZCopy][AZCopy]公用程式會取得您的資料傳輸至 Azure 儲存體 Blob 的絕佳工具。 它可供小型 （MB + +） toovery 大型 （GB + +） 資料傳輸。 [AZCopy]也已設計的 tooprovide 彈性輸送量時傳送資料 tooAzure，所以是不錯的選擇，hello 資料傳輸的步驟。 您可以使用 SQL 資料倉儲 PolyBase hello 資料載入一次傳送。 您也可以使用「執行程序」工作，將 AZCopy 納入 SSIS 封裝。

toouse AZCopy 您第一次將會需要 toodownload 並安裝它。 有[生產版本][production version]和[預覽版本][preview version]可用。

tooupload 檔案從檔案系統，您需要一個 hello 類似的命令如下：

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

高階程序摘要如下：

1. 設定 Azure 儲存體 blob 容器 tooreceive hello 資料
2. 匯出資料 toolocal 儲存體
3. AZCopy hello Azure Blob 儲存體容器中的資料
4. Hello 資料載入使用 PolyBase 的 SQL 資料倉儲

有完整的文件：[AZCopy][AZCopy]。

## <a name="optimizing-data-export"></a>最佳化資料匯出
此外 tooensuring hello 匯出符合 toohello 需求配置 PolyBase 您也可以搜尋 hello 資料 tooimprove hello 程序的進一步 toooptimize hello 匯出。



### <a name="data-compression"></a>資料壓縮
PolyBase 可以讀取 gzip 壓縮的資料。 如果您無法 toocompress 資料 toogzip 檔案，則會減少 hello 被推倒 hello 網路資料數量。

### <a name="multiple-files"></a>多個檔案
分割成數個檔案的大型資料表有助於 tooimprove 匯出速度，它也可協助使用傳輸 re-startability，和 hello hello 中的資料一次 hello Azure blob 儲存體的整體管理能力。 其中有許多不錯的 PolyBase 功能是它會讀取所有的 hello hello 資料夾內的檔案，並視為一個資料表。 因此，這是個不錯的主意 tooisolate hello 檔案的每個資料表至其自身的資料夾。

PolyBase 也支援一項稱為「遞迴資料夾周遊」的功能。 您可以使用這項功能 toofurther 增強的匯出的資料 tooimprove hello 組織您的資料管理。

toolearn 詳細資料載入資料，使用 PolyBase，請參閱[使用 PolyBase tooload 資料到 SQL 資料倉儲][Use PolyBase tooload data into SQL Data Warehouse]。

## <a name="next-steps"></a>後續步驟
如需有關移轉的詳細資訊，請參閱[移轉您的方案 tooSQL 資料倉儲][Migrate your solution tooSQL Data Warehouse]。
如需更多開發秘訣，請參閱[開發概觀][development overview]。

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx

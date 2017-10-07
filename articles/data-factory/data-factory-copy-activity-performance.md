---
title: "aaaCopy 活動效能及微調指南 |Microsoft 文件"
description: "深入了解當您使用複製活動時，會影響 Azure Data Factory 中的資料移動 hello 效能的關鍵因素。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 4b9a6a4f-8cf5-4e0a-a06f-8133a2b7bc58
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jingwang
ms.openlocfilehash: b0fb5a76c34752d07e8ddfffbb799a05fb5d6be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-activity-performance-and-tuning-guide"></a>複製活動的效能及微調指南
Azure Data Factory 複製活動會提供安全、可靠、高效能的頂級資料載入解決方案。 它可讓您 toocopy 數以萬計的 tb 的資料每天在各式各樣的雲端，並在內部部署資料存放區。 急速資料載入效能是您可以專注於 hello 核心"巨量資料 」 問題的索引鍵 tooensure： 建立進階的分析解決方案，並從所有資料取得的深入資訊。

Azure 提供企業等級的一組資料的儲存體和資料倉儲方案，並複製活動提供高度最佳化的資料載入輕鬆 tooconfigure 及設定的體驗。 只要使用單一的複製活動，您便可以達成下列目的︰

* 以 **1.2 GBps** 的速度將資料載入 **Azure SQL 資料倉儲**。 如需使用案例的逐步解說，請參閱[使用 Azure Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲](data-factory-load-sql-data-warehouse.md)。
* 以 **1.0 GBps** 的速度將資料載入 **Azure Blob 儲存體**
* 以 **1.0 GBps** 的速度將資料載入 **Azure Data Lake Store**

本文章說明：

* [效能參考編號](#performance-reference)針對支援的來源和接收資料存放區 toohelp 您計劃您的專案。
* 功能，可以提升 hello 不同的案例，包括複製輸送量[雲端資料移動的單位](#cloud-data-movement-units)，[平行複製](#parallel-copy)，和[分段複製](#staged-copy);
* [效能調整指引](#performance-tuning-steps)上 tootune hello 效能與 hello 關鍵因素會影響如何複製效能。

> [!NOTE]
> 如果您大致來說並不熟悉複製活動，請先參閱 [使用複製活動來移動資料](data-factory-data-movement-activities.md) 再閱讀本文。
>

## <a name="performance-reference"></a>效能參考

做為參考下表, 會顯示 hello 複製輸送量數字中 MBps hello 指定來源和接收組內部測試為基礎。 為了進行比較，該表格也會示範[雲端資料移動單位](#cloud-data-movement-units)或[資料管理閘道延展性](data-factory-data-management-gateway-high-availability-scalability.md) (多個閘道節點) 的不同設定如何協助複製效能。

![效能矩陣](./media/data-factory-copy-activity-performance/CopyPerfRef.png)


**點 toonote:**
* 輸送量使用 hello 下列公式來計算: [從來源讀取資料的大小] / [複製活動執行持續時間]。
* hello 資料表中的 hello 效能參考編號已測量使用[TPC H](http://www.tpc.org/tpch/)執行單一複製活動中的資料集。
* 在 Azure 的資料存放區，hello 來源和接收器是 hello 中相同的 Azure 區域。
* 在內部部署和雲端之間的混合式複製的資料存放區，已與 hello 在內部部署資料存放區下方規格不同的電腦上執行閘道的每個節點。 當單一活動執行閘道上時，hello 複製作業會取用一小部分的 hello 測試機器的 CPU、 記憶體或網路頻寬。 深入了解[資料管理閘道的考量](#considerations-for-data-management-gateway)。
    <table>
    <tr>
        <td>CPU</td>
        <td>32 核心 2.20 GHz Intel Xeon E5-2660 v2</td>
    </tr>
    <tr>
        <td>記憶體</td>
        <td>128 GB</td>
    </tr>
    <tr>
        <td>網路</td>
        <td>網際網路介面：10 Gbps；內部網路介面：40 Gbps</td>
    </tr>
    </table>


> [!TIP]
> 您可以利用更多資料移動的單位 (DMUs) 比 hello，以達到更高的輸送量預設最大 DMUs，即 32 雲端至雲端複製活動執行。 比方說，使用 100 DMU，您就可以用 **1.0GBps** 的速率將資料從 Azure Blob 複製到 Azure Data Lake Store。 請參閱 hello[雲端資料移動的單位](#cloud-data-movement-units)> 一節，如需詳細資訊，此功能和 hello 支援案例。 請連絡[Azure 支援](https://azure.microsoft.com/support/)toorequest 詳細 DMUs。

## <a name="parallel-copy"></a>平行複製
您可以閱讀 hello 從資料來源，或寫入資料 toohello 目的地**在複製活動中執行的平行**。 這項功能可加強 hello 的複製作業的輸送量並減少 hello toomove 資料所花費的時間。

這項設定是不同於 hello**並行**hello 活動定義中的屬性。 hello**並行**屬性決定 hello 數目**並行複製活動執行**tooprocess 資料從不同的活動視窗 (1 AM too2 AM，2 AM too3 AM，3 AM too4 等等)。 在執行歷程載入時，這個功能非常有用。 hello 平行複製功能適用於 tooa**單一活動執行**。

讓我們看一下範例案例。 在下列範例的 hello，從過去的 hello 的多個配量會需要 toobe 處理。 Data Factory 會對每個配量執行一個複製活動執行個體 (活動執行)：

* 從第一個活動視窗 hello hello 資料配量 （1 AM too2 是） = = > 活動執行 1
* 從第二個活動視窗 hello hello 資料配量 （2 AM too3 是） = = > 執行 2 活動。
* 從第二個活動視窗 hello hello 資料配量 （3 AM too4 是） = = > 執行的活動 3

依此類推。

在此範例中，當 hello**並行**設 too2，**活動執行 1**和**活動執行 2**資料複製兩個活動視窗**同時** tooimprove 資料移動的效能。 不過，如果多個檔案會與活動執行 1 相關聯，hello 資料移動服務將檔案複製從 hello 來源 toohello 目的地一個檔案一次。

### <a name="cloud-data-movement-units"></a>雲端資料移動單位
A**雲端資料移動單位 (DMU)**量值會呈現 hello 乘冪 （CPU、 記憶體和網路資源配置的組合） 的 Data Factory 中的單一單位。 DMU 可用於雲端到雲端的複製作業，但不可用於混合式複製。

根據預設，資料處理站會使用單一雲端 DMU tooperform 執行單一複製活動。 toooverride 此預設值，指定的值為 hello **cloudDataMovementUnits** ，如下所示的屬性。 相關之效能改善的 hello 層級的資訊可能會收到時設定特定的複製來源與接收器的多個單位，請參閱 hello[效能參考](#performance-reference)。

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "cloudDataMovementUnits": 32
        }
    }
]
```
hello**允許的值**hello **cloudDataMovementUnits**屬性是 1 （預設值）、 2、 4、 8、 16、 32。 hello**雲端 DMUs 的實際數目**hello 複製作業會使用在執行階段會等於 tooor 小於 hello 設定值，根據資料模式。

> [!NOTE]
> 如果您需要更多雲端 DMU 以提高輸送量，請連絡 [Azure 支援](https://azure.microsoft.com/support/)。 設定為 8 及更新版本的目前運作時，才您**複製多個檔案從 Blob 儲存體/Data Lake Store/Amazon S3/雲端 FTP/雲端 SFTP tooBlob 儲存體/Data Lake Store/Azure SQL Database**。
>

### <a name="parallelcopies"></a>parallelCopies
您可以使用 hello **parallelCopies**屬性 tooindicate hello 您想複製活動 toouse 的平行處理原則。 您可以將此屬性視為 hello 內可以從您的來源讀取或寫入 tooyour 接收資料存放區，以平行方式複製活動的執行緒數目上限。

對於每個複製活動時執行，Data Factory 會決定 hello 數目平行複製 toouse toocopy 資料從 hello 來源資料存放區和 toohello 目的地資料存放區。 它會使用的平行複本的 hello 預設數目取決於 hello 的來源和接收您所使用的型別。  

| 來源和接收 | 由服務決定的預設平行複製計數 |
| --- | --- |
| 在檔案型存放區 (Blob 儲存體、Data Lake Store、Amazon S3、內部部署檔案系統、內部部署 HDFS) 之間複製資料 |介於 1 到 32。 大小而定 hello hello 檔案和雲端資料移動單元 (DMUs) 的 hello 數目的兩個雲端資料存放區之間使用的 toocopy 資料或 hello 實體組態的 hello 閘道機器用於混合式複製 (toocopy 資料 tooor 從內部部署資料存放區). |
| 將資料從複製**tooAzure 資料表儲存體的任何來源資料存放區** |4 |
| 所有其他來源和接收組 |1 |

通常，hello 預設行為，應該能 hello 最佳輸送量。 不過，toocontrol hello 載入機器上裝載您的資料存放區或 tootune 複製的效能，您可能選擇 toooverride hello 預設值，然後指定一個值為 hello **parallelCopies**屬性。 hello 值必須介於 1 和 32 （兩者內含）。 在執行階段，hello 獲得最佳效能，複製活動會使用值小於或等於 toohello 您所設定的值。

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "parallelCopies": 8
        }
    }
]
```
點 toonote:

* 當您複製檔案為基礎的存放區之間的資料時，hello **parallelCopies**判斷 hello hello 檔案層級的平行處理原則。 單一檔案中的 hello 區塊處理時會發生情況之下自動且明確地，和其設計目的是 toouse hello 最佳適合區塊大小的指定的來源資料存放區中平行和正交 tooparallelCopies 輸入 tooload 資料。 hello 的平行複本 hello 資料移動服務會使用 hello 複製作業在執行階段是不超過您擁有的檔案的 hello 數目的實際數目。 如果 hello 複製行為**mergeFile**，複製活動無法充分利用檔案層級平行處理原則。
* 當您指定的值為 hello **parallelCopies**屬性，如果是混合式複製，請考慮在您的來源和接收的資料存放區和 toogateway hello 負載增加。 發生這種情況特別是當您有多個活動或 hello 並行執行相同的活動執行 hello 相同資料存放區。 如果您注意到 hello 資料存放區或閘道爆 hello 負載，減少 hello **parallelCopies**值 toorelieve hello 負載。
* 當您從存放區不是以檔案為基礎的檔案為基礎 toostores 複製資料時，hello 資料移動服務將會忽略 hello **parallelCopies**屬性。 即使已指定平行處理原則，也不會套用於此案例。

> [!NOTE]
> 您必須使用資料管理閘道器版本 1.11 或更新版本的 toouse hello **parallelCopies**功能，當您執行混合式複製。
>
>

toobetter 使用這些兩個屬性和 tooenhance 您資料移動的輸送量，請參閱 hello[範例使用案例](#case-study-use-parallel-copy)。 您不需要 tooconfigure **parallelCopies** tootake 優點 hello 預設行為。 如果您有設定且 **parallelCopies** 太小，將可能無法充分利用多個雲端 DMU。  

### <a name="billing-impact"></a>計費影響
它有**重要**向您收費的 tooremember 根據 hello hello 複製作業的時間總計。 如果複製作業 tootake 一小時搭配使用雲端的一個單位，現在只需要四個雲端單位 15 分鐘 hello 整體帳單會維持幾乎 hello 相同。 例如，您使用 4 個雲端單位。 第一個雲端單位 hello 花費在 10 分鐘，hello 第二個，10 分鐘，hello 第三個，5 分鐘，hello 第四個的其中一個，所有在執行一個複製活動中的 5 分鐘。 您必須支付 hello 總複製 （資料移動） 時間，也就是 10 + 10 + 5 + 5 = 30 分鐘。 是否使用 **parallelCopies** 對計費沒有任何影響。

## <a name="staged-copy"></a>分段複製
當您複製資料來源建立資料存放區 tooa 接收資料存放區時，您可能會選擇 toouse Blob 儲存體做為暫時的臨時存放區。 臨時區域是特別適用於下列情況下的 hello:

1. **您想從各種資料存放區 tooingest 資料到 SQL 資料倉儲 PolyBase 透過**。 SQL 資料倉儲會使用 PolyBase，作為到 SQL 資料倉儲的高輸送量機制 tooload 大量的資料。 不過，hello 來源資料必須在 Blob 儲存體，而且它必須符合其他準則。 當您從 Blob 儲存體以外的資料存放區載入資料時，您可以啟用透過過渡暫存 Blob 儲存體的資料複製。 在此情況下，Data Factory 執行所需的 hello 資料轉換 tooensure 確定它符合 PolyBase hello 需求。 然後它會使用 PolyBase tooload 資料到 SQL 資料倉儲。 如需詳細資訊，請參閱[使用 PolyBase tooload 資料到 Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse)。 如需使用案例的逐步解說，請參閱[使用 Azure Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲](data-factory-load-sql-data-warehouse.md)。
2. **有時它需要一些時間 tooperform 混合資料移動 (也就是在內部部署資料存放區與雲端資料存放區之間 toocopy) 透過低速網路連線**。 tooimprove 效能，您可以壓縮的 hello 內部資料，使其接受 toomove 資料 toohello 臨時資料存放區 hello 雲端中的時間。 然後您可以解壓縮 hello hello 執行之前載入 hello 目的地資料存放區的存放區中的資料。
3. **您不想 tooopen 連接埠以外的連接埠 80 和由於公司的 IT 原則的連接埠 443，在您的防火牆，**。 例如，當您從內部部署資料存放區 tooan Azure SQL Database 接收或 Azure SQL 資料倉儲接收複製資料，您需要 tooactivate 連出 TCP 通訊埠 1433年上的 hello Windows 防火牆和在公司防火牆。 在此案例中，利用 hello 閘道 toofirst 複製資料 tooa Blob 儲存體預備執行個體透過 HTTP 或 HTTPS 連接埠 443。 然後，hello 將資料載入 SQL Database 或 SQL 資料倉儲從 Blob 儲存體臨時區域。 在此流程，您不需要 tooenable 通訊埠 1433年。

### <a name="how-staged-copy-works"></a>分段複製的運作方式
當您啟用 hello 暫存功能時，第一個 hello 會資料從複製 hello 來源資料存放區 toohello 暫存資料存放區 （攜帶您自己）。 接下來，從 hello 暫存資料存放區 toohello 接收資料存放區複製 hello 資料。 Data Factory 自動管理您的 hello 兩階段流程。 Data Factory 也會清除從 hello hello 資料移動完成之後，暫存儲存體的暫存資料。

在 hello 雲端複製案例 （來源和接收的資料存放區是 hello 雲端中），不會使用閘道。 hello Data Factory 服務會執行 hello 複製作業。

![分段複製：雲端案例](media/data-factory-copy-activity-performance/staged-copy-cloud-scenario.png)

在 hello 混合式案例中複製 （來源是在內部部署和接收器是 hello 雲端中） hello 閘道才會移動 hello 來源資料中的資料存放區 tooa 暫存資料存放區。 資料處理站服務移從 hello 暫存資料的資料存放區 toohello 接收資料存放區。 資料複製到雲端資料儲存區 tooan 內部部署資料存放區透過臨時區域也支援 hello 反轉流程。

![分段複製：混合式案例](media/data-factory-copy-activity-performance/staged-copy-hybrid-scenario.png)

當您使用的暫存儲存區啟動資料移動時，您可以指定是否要讓 hello 資料 toobe 之前先將資料從 hello 來源資料儲存 tooan 暫時的或暫存資料存放區，然後再將資料從暫時移解壓縮壓縮或暫存資料存放區 toohello 接收資料存放區。

目前您還無法使用暫存存放區在兩個內部部署資料存放區之間複製資料。 我們希望能使用這個選項 toobe 推出。

### <a name="configuration"></a>組態
設定 hello **enableStaging**是否要先載入目的地資料存放區，暫置在 Blob 儲存體中的 hello 資料 toobe 在複製活動 toospecify 設定。 當您將**enableStaging** tooTRUE，指定 hello hello 下一個表格中列出的其他屬性。 如果您沒有帳戶，您也需要 toocreate Azure 儲存體或存放裝置共用存取簽章連結服務的預備環境。

| 屬性 | 說明 | 預設值 | 必要 |
| --- | --- | --- | --- |
| **enableStaging** |指定是否要透過暫存存放區暫時 toocopy 資料。 |False |否 |
| **linkedServiceName** |指定 hello 名稱[AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service)或[AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service)連結服務，它會參考您做為暫時的臨時存放區的儲存體 toohello 執行個體。 <br/><br/> 您無法使用共用的存取簽章 tooload 資料儲存到透過 PolyBase 的 SQL 資料倉儲。 您可以將它用於其他所有案例。 |N/A |是，當**enableStaging**設定 tooTRUE |
| **路徑** |指定您想要 toocontain hello 接移資料 hello Blob 儲存體路徑。 如果您未提供路徑，hello 服務會建立容器 toostore 暫存資料。 <br/><br/> 只有當您使用存放裝置使用共用的存取簽章，或您需要在特定位置的暫存資料 toobe 指定的路徑。 |N/A |否 |
| **enableCompression** |指定複製的 toohello 目的地之前，是否應該壓縮資料。 此設定可減少 hello 磁碟區所傳送的資料。 |False |否 |

以下是範例的定義複製活動與 hello 屬性 hello 前面表格中所述：

```json
"activities":[  
{
    "name": "Sample copy activity",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDBOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlSink"
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob",
            "path": "stagingcontainer/path",
            "enableCompression": true
        }
    }
}
]
```

### <a name="billing-impact"></a>計費影響
我們將會根據兩個步驟向您收費：複製持續時間和複製類型。

* 當您使用暫存期間雲端複製 （資料從雲端資料儲存區 tooanother 雲端資料存放區），您需要付費 hello [步驟 1 和步驟 2 複製的持續時間的加總] x [雲端複製單價]。
* 當您使用暫存期間混合式複製 （資料從內部部署資料存放區 tooa 雲端資料存放區），您將支付 [混合式複製持續時間] x [混合式複製單價] + [雲端複製持續時間] x [雲端複製單價]。

## <a name="performance-tuning-steps"></a>效能微調步驟
我們建議您採取下列步驟複製活動的 Data Factory 服務 tootune hello 效能：

1. **建立基準**。 Hello 開發階段，請針對代表性資料樣本使用複製活動以測試您的管線。 您可以使用 Data Factory hello[配量模型](data-factory-scheduling-and-execution.md)toolimit hello 您使用的資料量。

   收集執行時間和效能特性，使用 hello**監視及管理應用程式**。 在 Data Factory 首頁上選擇 [監視及管理]。 在 hello 樹狀結構檢視中，選擇 hello**輸出資料集**。 在 hello**活動 Windows**清單中，選擇 hello 複製活動執行。 **活動 Windows**列出 hello 複製活動持續時間和 hello hello 複製的資料大小。 hello 輸送量會列在**活動視窗總管**。 toolearn 進一步了解 hello 應用程式，請參閱[監視和管理 Azure Data Factory 管線使用 hello 監視及管理應用程式](data-factory-monitor-manage-app.md)。

   ![活動執行詳細資料](./media/data-factory-copy-activity-performance/mmapp-activity-run-details.png)

   稍後在 hello 文章中，您可以比較 hello 效能和設定您的案例 tooCopy 活動的[效能參考](#performance-reference)從我們的測試。
2. **效能診斷與最佳化**。 如果您觀察到的 hello 效能不符合您的預期，您會需要 tooidentify 效能瓶頸。 然後，最佳化效能 tooremove 或降低瓶頸的 hello 造成影響。 效能診斷的完整說明超出本文的 hello 範圍，但以下是一些常見的考量：

   * 效能功能︰
     * [平行複製](#parallel-copy)
     * [雲端資料移動單位](#cloud-data-movement-units)
     * [分段複製](#staged-copy)
     * [資料管理閘道延展性](data-factory-data-management-gateway-high-availability-scalability.md)
   * [資料管理閘道](#considerations-for-data-management-gateway)
   * [來源](#considerations-for-the-source)
   * [接收](#considerations-for-the-sink)
   * [序列化和還原序列化](#considerations-for-serialization-and-deserialization)
   * [壓縮](#considerations-for-compression)
   * [資料行對應](#considerations-for-column-mapping)
   * [其他考量](#other-considerations)
3. **展開 hello 組態 tooyour 整個資料集**。 當您滿意 hello 執行結果及效能時，您可以展開 hello 定義與管線使用中週期 toocover 您整個資料集。

## <a name="considerations-for-data-management-gateway"></a>資料管理閘道的考量
**閘道安裝**： 我們建議您使用專用的電腦 toohost 資料管理閘道器。 請參閱[使用資料管理閘道的考量](data-factory-data-management-gateway.md#considerations-for-using-gateway)。  

**監視閘道和向上/外**： 單一邏輯閘道與一或多個閘道節點可以提供多個複製活動就會在 hello 相同時間同時。 您可以檢視幾乎是即時的資源使用情況 (CPU、 記憶體、 network(in/out) 等) 的快照集，以及執行與 hello Azure 入口網站中限制的並行處理作業的 hello 數目看到在閘道機器上[hello 入口網站中的監視閘道](data-factory-data-management-gateway.md#monitor-gateway-in-the-portal). 如果在混合式資料移動使用大量的並行複製活動執行或大量的資料 toocopy 上有大量的需要，請考慮太[向上延展還是向外閘道延展](data-factory-data-management-gateway-high-availability-scalability.md#scale-considerations)，toobetter 以利用您的資源或tooprovision 更多資源 tooempower 複製。 

## <a name="considerations-for-hello-source"></a>Hello 來源的考量
### <a name="general"></a>一般
請務必的或對它執行其他工作負載不爆該 hello 基礎資料存放區。

Microsoft 資料存放區，請參閱[監視及調整主題](#performance-reference)屬於特定 toodata 存放區和幫助您了解資料存放區效能特性、 回應時間降到最低和最大化輸送量。

如果您將資料複製 Blob 儲存體 tooSQL 資料倉儲時，請考慮使用**PolyBase** tooboost 效能。 請參閱[使用 PolyBase tooload 資料到 Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse)如需詳細資訊。 如需使用案例的逐步解說，請參閱[使用 Azure Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲](data-factory-load-sql-data-warehouse.md)。

### <a name="file-based-data-stores"></a>以檔案為基礎的資料存放區
*(包括 Blob 儲存體、Data Lake Store、Amazon S3、內部部署檔案系統及內部部署 HDFS)*

* **平均檔案大小和檔案計數**：複製活動會一次傳送一個檔案的資料。 以相同數量的資料 toobe 移動的 hello，hello 整體輸送量較低 hello 資料若包含許多小檔案，而不是因為 toohello 啟動程序階段中的每個檔案的幾個大型檔案。 因此，可能的話，請將小型檔案合併較大檔案 toogain 較高的輸送量。
* **檔案格式與壓縮**： 更多方式 tooimprove 效能，請參閱 hello[序列化和還原序列化的考量](#considerations-for-serialization-and-deserialization)和[考量壓縮](#considerations-for-compression)區段。
* Hello**在內部部署檔案系統**案例中的，在其中**資料管理閘道器**是必要，請參閱 hello[資料管理閘道器的考量](#considerations-for-data-management-gateway)> 一節。

### <a name="relational-data-stores"></a>關聯式資料存放區
*(包括 SQL Database、SQL 資料倉儲、Amazon Redshift、SQL Server 資料庫，以及 Oracle、MySQL、DB2、Teradata、Sybase 和 PostgreSQL 資料庫等)*

* **資料模式**︰資料表結構描述對複製輸送量會有影響。 大型資料列大小可讓您更佳的效能比小型資料列大小，toocopy hello 相同的資料量。 hello 原因是該 hello 資料庫可以更有效率地擷取較少的批次包含較少的資料列的資料。
* **查詢或預存程序**： 最佳化 hello 查詢或預存程序更有效率地指定 hello 複製活動來源 toofetch 資料中的 hello 邏輯。
* 如**在內部部署關聯式資料庫**，例如 SQL Server 和 Oracle，需要使用 hello**資料管理閘道器**，請參閱 hello[資料管理閘道器的考量](#considerations-on-data-management-gateway) > 一節。

## <a name="considerations-for-hello-sink"></a>Hello 接收的考量
### <a name="general"></a>一般
請務必的或對它執行其他工作負載不爆該 hello 基礎資料存放區。

Microsoft 資料存放區，請參閱太[監視及調整主題](#performance-reference)屬於特定 toodata 存放區。 這些主題可協助您了解資料存放區效能特性，以及如何 toominimize 回應逾時和最大化輸送量。

如果您要複製的資料**Blob 儲存體**太**SQL 資料倉儲**，請考慮使用**PolyBase** tooboost 效能。 請參閱[使用 PolyBase tooload 資料到 Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse)如需詳細資訊。 如需使用案例的逐步解說，請參閱[使用 Azure Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲](data-factory-load-sql-data-warehouse.md)。

### <a name="file-based-data-stores"></a>以檔案為基礎的資料存放區
*(包括 Blob 儲存體、Data Lake Store、Amazon S3、內部部署檔案系統及內部部署 HDFS)*

* **複製行為**： 如果您從不同的檔案為基礎的資料存放區複製資料，複製活動有三個選項，透過 hello **copyBehavior**屬性。 它會保留階層、扁平化階層或合併檔案。 保留或是扁平化階層有少量或沒有效能額外負荷，但合併檔案會造成效能負擔 tooincrease。
* **檔案格式與壓縮**： 請參閱 hello[序列化和還原序列化的考量](#considerations-for-serialization-and-deserialization)和[壓縮的考量](#considerations-for-compression)更方式 tooimprove 高效能的章節.
* **Blob 儲存體**：Blob 儲存體目前只支援以區塊 Blob 來最佳化資料傳送和輸送量。
* 如**在內部部署檔案系統**需要 hello 使用案例**資料管理閘道器**，請參閱 hello[資料管理閘道器的考量](#considerations-for-data-management-gateway)> 一節。

### <a name="relational-data-stores"></a>關聯式資料存放區
*(包括 SQL Database、SQL 資料倉儲、SQL Server 資料庫及 Oracle 資料庫)*

* **複製行為**： 根據您所設定的 hello 屬性**sqlSink**，複製活動中不同的方式寫入資料 toohello 目的地資料庫。
  * 根據預設，hello 資料移動服務會使用中的 hello 大量複製 API tooinsert 資料附加模式中，可提供 hello 達到最佳效能。
  * 如果您在 hello 接收器設定預存程序，hello 資料庫就會套用 hello 資料的一個資料列一次而不是為大量載入。 因此效能會大幅降低。 如果您的資料集很大，如果適用的話，請考慮切換 toousing hello **sqlWriterCleanupScript**屬性。
  * 如果您設定 hello **sqlWriterCleanupScript**執行每個複製活動的屬性、 hello 服務觸發程序 hello 指令碼，並使用 hello 大量複製 API tooinsert hello 資料。 例如，toooverwrite hello 整個資料表 hello 最新的資料，您可以指定指令碼 toofirst hello 來源中刪除大量載入 hello 新資料之前的所有記錄。
* **資料模式和批次大小**：
  * 資料表結構描述對複製輸送量會有影響。 toocopy hello 相同的資料量，大型資料列大小可讓您更佳的效能比小型資料列大小因為 hello 資料庫可以更有效率地認可的資料較少的批次。
  * 複製活動會以一系列的批次插入資料。 您也可以使用 hello 批次中設定的資料列的 hello 數目**叫用 writeBatchSize**屬性。 如果您的資料有小型的資料列，您可以設定 hello**叫用 writeBatchSize**屬性與更高的值 toobenefit 從批次額外負荷較低 」 和 「 較高的輸送量。 如果 hello 資料列大小的資料很大，請小心增加**叫用 writeBatchSize**。 較高的值可能會導致多載 hello 資料庫所致 tooa 複製失敗。
* 如**在內部部署關聯式資料庫**，如 SQL Server 和 Oracle 需要 hello 使用**資料管理閘道器**，請參閱 hello[資料管理閘道器的考量](#considerations-for-data-management-gateway) > 一節。

### <a name="nosql-stores"></a>NoSQL 存放區
(包括表格儲存體和 Azure Cosmos DB)

* 針對 **表格儲存體**：
  * **資料分割**： 撰寫資料 toointerleaved 分割大幅降低效能。 資料分割索引鍵所排序您的來源資料，使得 hello 資料插入有效率地一個分割區之後，或調整 hello 邏輯 toowrite hello 資料 tooa 單一資料分割。
* 針對 **Azure Cosmos DB**：
  * **批次大小**: hello**叫用 writeBatchSize**屬性會設定平行要求的 hello 數目 toohello Azure Cosmos DB 服務 toocreate 文件。 您可以預期更佳的效能，當您增加**叫用 writeBatchSize**因為多個平行的要求會傳送 tooAzure Cosmos DB。 不過，當您撰寫 tooAzure Cosmos DB 節流監看 （hello 錯誤訊息為 「 要求率非常大 」）。 各種因素會造成節流設定，包括文件大小 hello 詞彙數目的 hello 文件，並且 hello 目標集合的編製索引原則。 tooachieve 較高的複製輸送量，請考慮使用較佳的集合，例如 S3。

## <a name="considerations-for-serialization-and-deserialization"></a>序列化和還原序列化的考量
如果您的輸入資料集或輸出資料集是檔案，就可能發生序列化和還原序列化。 請參閱[支援的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)，其中具有關於複製活動支援檔案格式的詳細資訊。

**複製行為**：

* 在以檔案為基礎的資料存放區之間複製檔案：
  * 當輸入和輸出資料集都有 hello 相同或任何檔案格式設定、 hello 資料移動服務執行的二進位的複本，而不需要任何序列化或還原序列化。 您會看到較高的輸送量比較 toohello 案例，哪些 hello 來源和接收的檔案格式設定都與彼此不同。
  * 當輸入和輸出的資料集這兩個是以文字格式只有 hello 編碼類型不同，hello 資料移動服務，才會執行編碼方式轉換。 它不會執行任何序列化和還原序列化時，會導致某些效能額外負荷比較 tooa 二進位複製。
  * 當輸入和輸出資料集這兩個具有不同的檔案格式或不同的組態，分隔符號，例如 hello 資料移動服務還原序列化的來源資料 toostream、 轉換，然後將它序列化成您所指定的 hello 輸出格式。 此作業會產生額外負荷更顯著的效能比較 tooother 案例。
* 當您複製檔案，從資料存放區不是以檔案為基礎 （例如，從檔案型存放區 tooa 關聯式存放區） 時，hello 序列化或還原序列化的步驟需要。 此步驟會導致很高的效能負荷。

**檔案格式**: hello 您選擇的檔案格式可能會影響複製效能。 例如，Avro 是一種壓縮二進位格式，可將中繼資料和資料儲存在一起。 它進行處理和查詢的 hello Hadoop 生態系統中有廣泛的支援。 不過，Avro 是更昂貴的序列化和還原序列化，而這會造成較低的複製輸送量比較 tootext 格式。 讓您選擇的整個 hello 而加以進行歷程處理流程的檔案格式。 以何種表單 hello 資料會儲存在開頭，而且來源資料存放區或 toobe 擷取自外部系統。儲存體、 分析的處理及查詢; hello 最佳格式並以何種格式 hello 資料應該匯出到資料超市報告和視覺化工具。 有時是次佳的檔案格式讀取和寫入效能可能會很好的選擇，當您考慮 hello 整體分析程序。

## <a name="considerations-for-compression"></a>壓縮的考量
當您輸入或輸出的資料集是一個檔案時，您可以設定複製活動 tooperform 壓縮或解壓縮，因為它會將資料 toohello 目的地。 當您選擇壓縮時，您必須在輸入/輸出 (I/O) 與 CPU 之間進行取捨。 壓縮 hello 資料中額外的成本計算資源。 但另一方面卻可降低網路 I/O 和儲存體用量。 根據您的資料，您可能會看到整體複製輸送量有所提升。

**轉碼器**︰複製活動支援 gzip、bzip2 和 Deflate 壓縮類型。 這三種類型都可供 Azure HDInsight 進行處理。 每種壓縮轉碼器各有優點。 例如，bzip2 hello 最低複製輸送量，但是因為您可以將它分割進行處理，取得 hello 最佳 Hive 查詢的效能與 bzip2。 Gzip 是最平衡 hello 選項，以及使用它最常 hello。 選擇最適合您的端對端案例的 hello 轉碼器。

**層級**：對於每個壓縮轉碼器，您可以從兩個選項中做選擇：最快速的壓縮和最佳化的壓縮。 hello 最快速的壓縮的選項 hello 資料壓縮儘快，即使未以最佳方式壓縮 hello 產生的檔案。 hello 以最佳方式壓縮的選項壓縮花更多時間，並會產生最少量的資料。 您可以測試這兩個選項 toosee 可提供更佳的整體效能，您的情況。

**要考量的事項**: toocopy 大量的內部存放區與 hello 雲端之間的資料，請考慮使用壓縮的過渡期的 blob 儲存體。 使用暫時儲存體時，很有幫助您的公司網路和您的 Azure 服務的 hello 頻寬 hello 限制因素，而且您想 hello 輸入資料集和輸出資料集這兩個 toobe 未壓縮的形式。 更具體來說，您可以將單一複製活動分成兩個複製活動。 hello 第一個複製活動會從複製 hello 來源 tooan 暫時的或壓縮格式中的暫存 blob。 第二個複製活動 hello hello 壓縮資料複製從臨時區域，，然後將解壓縮時就會將寫入 toohello 接收。

## <a name="considerations-for-column-mapping"></a>資料行對應的考量
您可以設定 hello **columnMappings**中所有的複製活動 toomap 或子集 hello 屬性輸入資料行 toohello 輸出資料行。 Hello 資料移動服務從 hello 來源讀取 hello 資料之後，它會將寫入 hello 資料 toohello 接收器之前需要 tooperform hello 資料的資料行對應。 這項額外處理會降低複製輸送量。

如果來源資料存放區可供查詢，比方說，如果是類似 SQL Database 或 SQL Server 關聯式存放區，或者它是 NoSQL 存放區，例如資料表儲存體或 Azure Cosmos DB，請考慮推送 hello 資料行篩選和邏輯 toohello 重新調整順序**查詢**屬性，而不要使用資料行對應。 如此一來，hello 來源資料中的資料存放區，會更有效率的 hello 資料移動服務讀取時，就會發生 hello 投影。

## <a name="other-considerations"></a>其他考量
如果 hello 大小想 toocopy 大，您可以調整的資料的商務邏輯 toofurther 分割 hello 資料使用 hello Data Factory 中切割機制。 然後，排程複製活動 toorun 更頻繁地執行每個複製活動 tooreduce hello 資料大小。

能謹慎 hello 數目的資料集和複製活動需要 Data Factory tooconnector toohello 相同的資料儲存在 hello 相同的時間。 許多並行的複製作業可能會進行節流資料存放區和導致 toodegraded 效能，複製作業內部重試次數，在某些情況下，執行失敗數目。

## <a name="sample-scenario-copy-from-an-on-premises-sql-server-tooblob-storage"></a>範例案例： 從內部部署 SQL Server 的 tooBlob 存放區的複本
**案例**： 在管線內建 toocopy 資料從內部部署 SQL Server 的 tooBlob 存放區以 CSV 格式。 toomake hello 複製作業更快、 hello CSV 檔案應該壓縮成 bzip2 格式。

**測試和分析**: hello 輸送量，複製活動是小於 2 MBps，也就是比 hello 效能基準測試變得很慢。

**效能分析和微調**: tootroubleshoot hello 效能問題，讓我們看看如何處理及移動 hello 資料。

1. **讀取資料**： 閘道會開啟連接 tooSQL 伺服器，並傳送 hello 查詢。 SQL Server 回應傳送嗨資料資料流 tooGateway 透過 hello 內部網路。
2. **序列化和壓縮資料**： 閘道序列化 hello 資料資料流 tooCSV 格式，並壓縮 hello 資料 tooa bzip2 資料流。
3. **將資料寫入**： 閘道上傳 hello bzip2 資料流 tooBlob 儲存體透過 hello 網際網路。

如您所見，hello 資料正在處理，而且移動資料流的循序方式： SQL Server > LAN > 閘道 > WAN > Blob 儲存體。 **hello 整體效能閘道 hello 輸送量最小值由整個 hello 管線**。

![資料流](./media/data-factory-copy-activity-performance/case-study-pic-1.png)

一或多個 hello 下列因素可能會導致 hello 效能瓶頸：

* **來源**：SQL Server 本身的輸送量偏低，因為負載過重。
* **資料管理閘道**：
  * **LAN**： 閘道遠 hello SQL Server 電腦，並且具有低頻寬連線。
  * **閘道**： 閘道已達到下列作業其負載限制 tooperform hello:
    * **序列化**： 序列化 hello 資料資料流 tooCSV 格式具有慢速的輸送量。
    * **壓縮**：您選擇了緩慢的壓縮轉碼器 (例如 bzip2，其採用 Core i7，速度為 2.8 MBps)。
  * **WAN**: hello hello 公司網路與您的 Azure 服務之間的頻寬太低 (例如，T1 = 1,544 kbps。T2 = 6,312 kbps)。
* **接收**：Blob 儲存體的輸送量低  (但不太可能發生，因為其 SLA 保證至少有 60 MBps)。

在此情況下，bzip2 資料壓縮可能會減緩 hello 整個管線使用。 切換 tooa gzip 壓縮轉碼器，可能會簡化此瓶頸。

## <a name="sample-scenarios-use-parallel-copy"></a>範例案例︰使用平行複本
**案例 i:** 1,000 1 MB 的檔案複製 hello 在內部部署檔案系統 tooBlob 儲存體。

**分析和效能調整**： 例如，如果您有四核心電腦上安裝閘道 Data Factory 會使用 hello 檔案系統 tooBlob 儲存體從 16 toomove 檔案平行複製同時。 此平行執行應該會導致高輸送量。 您也可以明確指定 hello 平行複本計數。 在複製許多小型檔案時，平行複製可藉由更有效率地使用資源，而對輸送量大有幫助。

![案例 1](./media/data-factory-copy-activity-performance/scenario-1.png)

**案例 II**: 20 的 500 MB 的 blob 複製 Blob 儲存體 tooData 湖存放區分析，並再調整效能。

**分析和效能調整**： 在此案例中，Data Factory hello 將資料複製從 Blob 儲存體 tooData 湖存放區使用單一複本 (**parallelCopies**設定 too1) 及單一雲端資料移動的單位。 hello 輸送量您觀察就會關閉 toothat 述 hello[效能參考章節](#performance-reference)。   

![案例 2](./media/data-factory-copy-activity-performance/scenario-2.png)

**案例 III**︰個別檔案大小大於數十 MB 且總數量很大。

**分析和效能微調**： 增加**parallelCopies**由於的單一雲端 DMU hello 資源限制並不會造成複製更好的效能。 相反地，您應該指定多個雲端 DMUs tooget 更多資源 tooperform hello 資料移動。 未指定的值為 hello **parallelCopies**屬性。 Data Factory 會為您處理 hello 平行處理原則。 在此情況下，如果您設定**cloudDataMovementUnits** too4，關於輸送量四次，就會發生。

![案例 3](./media/data-factory-copy-activity-performance/scenario-3.png)

## <a name="reference"></a>參考
以下是效能監視及微調參考某些 hello 支援資料存放區：

* Azure 儲存體 (包括 Blob 儲存體和表格儲存體)：[Azure 儲存體的擴充性目標](../storage/common/storage-scalability-targets.md)和 [Azure 儲存體效能和擴充性檢查清單](../storage/common/storage-performance-checklist.md)
* Azure SQL Database： 您可以[監視 hello 效能](../sql-database/sql-database-single-database-monitor.md)並檢查 hello 資料庫交易單位 (DTU) 百分比
* Azure SQL 資料倉儲：其能力會以資料倉儲單位 (DWU) 來測量；請參閱 [管理 Azure SQL 資料倉儲中的計算能力 (概觀)](../sql-data-warehouse/sql-data-warehouse-manage-compute-overview.md)
* Azure Cosmos DB：[Azure Cosmos DB 中的效能等級](../documentdb/documentdb-performance-levels.md)
* 內部部署 SQL Server： [效能的監視與微調](https://msdn.microsoft.com/library/ms189081.aspx)
* 內部部署檔案伺服器： [檔案伺服器的效能微調](https://msdn.microsoft.com/library/dn567661.aspx)

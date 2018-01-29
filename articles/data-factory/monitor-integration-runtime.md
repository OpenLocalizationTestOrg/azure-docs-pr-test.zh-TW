---
title: "在 Azure Data Factory 中監視整合執行階段 | Microsoft Docs"
description: "了解如何監視 Azure Data Factory 中不同類型的整合執行階段。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2017
ms.author: spelluru
ms.openlocfilehash: e1bfb7199ddf9f02297db9de529729ba3833cf8c
ms.sourcegitcommit: c50171c9f28881ed3ac33100c2ea82a17bfedbff
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2017
---
# <a name="monitor-an-integration-runtime-in-azure-data-factory"></a>在 Azure Data Factory 中監視整合執行階段  
**整合執行階段**是 Azure Data Factory 所使用的計算基礎結構，可提供跨不同網路環境的各種資料整合功能。 Data Factory 提供三種類型的整合執行階段：

- Azure 整合執行階段
- 自我裝載整合執行階段
- Azure SSIS 整合執行階段

> [!NOTE]
> 本文適用於第 2 版的 Data Fatory (目前為預覽版)。 如果您使用 Data Factory 服務的 1 版 (正式推出版本 (GA))，請參閱 [Data Factory 第 1 版文件](v1/data-factory-introduction.md)。

若要取得整合執行階段 (IR) 的執行個體狀態，請執行下列 PowerShell 命令： 

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName MyDataFactory -ResourceGroupName MyResourceGroup -Name MyAzureIR -Status
``` 

Cmdlet 會為不同類型的整合執行階段傳回不同的資訊。 本文說明每一種整合執行階段類型的屬性和狀態。  

## <a name="azure-integration-runtime"></a>Azure 整合執行階段
可在 Azure 中完整且靈活地管理 Azure 整合執行階段的計算資源。 下表提供 **Get-AzureRmDataFactoryV2IntegrationRuntime** 命令所傳回屬性說明：

### <a name="properties"></a>屬性
下表提供 Azure 整合執行階段的 Cmdlet 所傳回的屬性說明：

| 屬性 | 說明 |
-------- | ------------- | 
| 名稱 | Azure 整合執行階段的名稱。 |  
| State | Azure 整合執行階段的狀態。 | 
| 位置 | Azure 整合執行階段的位置。 如需 Azure 整合執行階段的位置詳細資訊，請參閱[整合執行階段簡介](concepts-integration-runtime.md)。 |
| DataFactoryName | Azure 整合執行階段所屬的資料處理站名稱。 | 
| resourceGroupName | 資料處理站所屬的資源群組名稱。  |
| 說明 | 整合執行階段的說明。  |

### <a name="status"></a>狀態
下表提供 Azure 整合執行階段的可能狀態：

| 狀態 | 註解/案例 | 
| ------ | ------------------ |
| 線上 | Azure 整合執行階段在線上且可供使用。 | 
| 離線 | Azure 整合執行階段因內部錯誤而離線。 |

## <a name="self-hosted-integration-runtime"></a>自我裝載整合執行階段
本節提供 Get-AzureRmDataFactoryV2IntegrationRuntime Cmdlet 所傳回的屬性說明。 

> [!NOTE] 
> 傳回的屬性和狀態包含整體的自我裝載整合執行階段，和執行階段中每個節點的相關資訊。  

### <a name="properties"></a>屬性

下表提供**每個節點**的監視屬性說明：

| 屬性 | 說明 | 
| -------- | ----------- | 
| 名稱 | 自我裝載整合執行階段及其關聯之節點的名稱。 節點是安裝了自我裝載整合執行階段的內部部署 Windows 電腦。 |  
| 狀態 | 整體自我裝載整合執行階段與每個節點的狀態。 範例：線上/離線/受限制/等等。如需這些狀態的相關資訊，請參閱下一節。 | 
| 版本 | 自我裝載整合執行階段與每個節點的版本。 自我裝載整合執行階段的版本取決於群組中大多數節點的版本。 如果自我裝載整合執行階段設定中有不同版本的節點，則只有版本號碼和邏輯自我裝載整合執行階段的節點會正常運作。 其他節點會進入受限制模式，並需要加以手動更新 (如果自動更新失敗才需要這麼做)。 | 
| 可用的記憶體 | 自我裝載整合執行階段節點上的可用記憶體。 這個值是近乎即時的快照集。 | 
| CPU 使用率 | 自我裝載整合執行階段節點的 CPU 使用率。 這個值是近乎即時的快照集。 |
| 網路功能 (輸入/輸出) | 自我裝載整合執行階段節點的網路使用率。 這個值是近乎即時的快照集。 | 
| 並行作業 (執行中/限制) | 每個節點上執行的作業或工作數目。 這個值是近乎即時的快照集。 限制表示每個節點的最大並行作業數。 這個值會根據機器大小來定義。 您可以提高限制以在進階案例 (CPU/記憶體/網路並未充分使用，但活動會逾時的案例) 中相應增加並行作業執行能力。這項功能也可與單一節點的自我裝載整合執行階段搭配使用。 |
| 角色 | 多節點的自我裝載整合執行階段中的角色有兩種 – 發送器和背景工作角色。 所有節點都是背景工作角色，這表示它們全都能用來執行作業。 發送器節點只有一個，可用來提取雲端服務中的工作/作業，並發送到不同的背景工作節點。 發送器節點也是背景工作角色節點。 |

當自我裝載整合執行階段中有兩個或多個節點 (相應放大情節) 時，屬性的某些設定會比較合理。 
  
### <a name="status-per-node"></a>狀態 (每個節點)
下表提供自我裝載整合執行階段節點的可能狀態：

| 狀態 | 說明 |
| ------ | ------------------ | 
| 線上 | 節點已連線至 Data Factory 服務。 |
| 離線 | 節點已離線。 |
| 升級中 | 節點正在自動更新。 |
| 限制 | 由於連線能力問題。 可能是因為 HTTP 連接埠 8050 問題、服務匯流排連線問題或認證同步問題。 |
| 非使用中 | 節點所在的組態不同於其他大多數節點的組態。 |

節點無法連線至其他節點時，便會處於非使用中狀態。

### <a name="status-overall-self-hosted-integration-runtime"></a>狀態 (整體自我裝載整合執行階段)
下表提供自我裝載整合執行階段的可能狀態。 此狀態取決於隸屬於執行階段的所有節點狀態。 

| 狀態 | 說明 |
| ------ | ----------- | 
| 需要註冊 | 尚未針對此自我裝載整合執行階段註冊節點。 |
| 線上 | 所有節點已連線。 |
| 離線 | 沒有節點在線上。 |
| 限制 | 在此自我裝載整合執行階段中，並非所有節點皆處於健康狀態。 這個狀態是某些節點可能會關閉的警告。 此狀態可能是發送器/背景工作角色節點的認證同步問題所引起。 |

使用 **Get-AzureRmDataFactoryV2IntegrationRuntimeMetric** Cmdlet 來擷取包含詳細的自我裝載整合執行階段屬性的 JSON 裝載，及其在執行 Cmdlet 期間的快照集值。

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntimeMetric -name $integrationRuntimeName -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName  | | ConvertTo-Json 
```

輸出範例 (假設此自我裝載整合執行階段有兩個相關節點)：

```json
{
    "IntegrationRuntimeName":  "<Name of your integration runtime>",
    "ResourceGroupName":  "<Resource Group Name>",
    "DataFactoryName":  "<Data Factory Name>",
    "Nodes":  [
        {
            "NodeName":  "<Node Name>",
            "AvailableMemoryInMB":  <Value>,
            "CpuUtilization":  <Value>,
            "ConcurrentJobsLimit":  <Value>,
            "ConcurrentJobsRunning":  <Value>,
            "MaxConcurrentJobs":  <Value>,
            "SentBytes":  <Value>,
            "ReceivedBytes":  <Value>
        },
        {
            "NodeName":  "<Node Name>",
            "AvailableMemoryInMB":  <Value>,
            "CpuUtilization":  <Value>,
            "ConcurrentJobsLimit":  <Value>,
            "ConcurrentJobsRunning":  <Value>,
            "MaxConcurrentJobs":  <Value>,
            "SentBytes":  <Value>,
            "ReceivedBytes":  <Value>
        }

    ]
} 
```


## <a name="azure-ssis-integration-runtime"></a>Azure SSIS 整合執行階段
Azure SSIS 整合執行階段是完全受管理的 Azure 虛擬機器 (或節點) 叢集，專門用來執行 SSIS 套件。 它不會執行 Azure Data Factory 的任何其他活動。 佈建之後，您可以查詢其屬性並監視其整體/節點的特定狀態。

### <a name="properties"></a>屬性

| 屬性/狀態 | 說明 |
| --------------- | ----------- |
| CreateTime | 您的 Azure SSIS 整合執行階段建立時的 UTC 時間。 |
| 節點 | 含特定節點狀態 (啟動中/可用/回收/無法使用中) 的 Azure SSIS 整合執行階段的配置/可用節點，及可採取動作的錯誤。 |
| OtherErrors | 您的 Azure SSIS 整合執行階段上非特定節點之可採取動作的錯誤。 |
| LastOperation | Azure SSIS 整合執行階段上最後一個啟動/停止作業的結果，含在失敗時可採取動作的錯誤。 |
| State | 您的 Azure SSIS 整合執行階段的整體狀態 (初始/啟動中/已啟動/停止中/已停止)。 |
| 位置 | Azure SSIS 整合執行階段的位置。 |
| NodeSize | Azure SSIS 整合執行階段之每個節點的大小。 |
| NodeCount | Azure SSIS 整合執行階段中的節點數目。 |
| MaxParallelExecutionsPerNode | Azure SSIS 整合執行階段中每個節點的平行執行數目。 |
| CatalogServerEndpoint | 至主機 SSISDB 的現有 Azure SQL Database/受管理執行個體伺服器的端點。 |
| CatalogAdminUserName | 現有 Azure SQL Database/受管理執行個體伺服器之管理者的使用者名稱。 Data Factory 服務會使用此資訊，代表您準備及管理 SSISDB。 |
| CatalogAdminPassword | 現有 Azure SQL Database/受管理執行個體伺服器之管理者密碼。 |
| CatalogPricingTier | 現有 Azure SQL Database 伺服器所裝載的 SSISDB 定價層。  不適用於 Azure SQL 受管理的執行個體裝載 SSISDB。 |
| VNetId | Azure SSIS 整合執行階段要加入的虛擬網路 (VNet) 資源識別碼。 |
| 子網路 | Azure SSIS 整合執行階段要加入的子網路名稱。 |
| ID | Azure SSIS 整合執行階段的資源識別碼。 |
| 類型 | Azure SSIS 整合執行階段的 (受管理/自我裝載) 類型。 |
| resourceGroupName | Azure 資源群組的名稱，其中已建立 Data Factory 和 Azure SSIS 整合執行階段。 |
| DataFactoryName | Azure 資料處理站的名稱。 |
| 名稱 | Azure SSIS 整合執行階段的名稱。 |
| 說明 | Azure SSIS 整合執行階段的說明。 |

  
### <a name="status-per-node"></a>狀態 (每個節點)

| 狀態 | 說明 |
| ------ | ----------- | 
| 啟動中 | 正在準備此節點。 |
| 可用 | 此節點已準備好部署/執行 SSIS 套件。 |
| 回收中 | 此節點正在修復/重新啟動。 |
| 無法使用 | 此節點未準備好部署/執行 SSIS 套件，而且具有可採取動作解決的錯誤/問題。 |

### <a name="status-overall-azure-ssis-integration-runtime"></a>狀態 (整體 Azure SSIS 整合執行階段)

| 整體狀態 | 說明 | 
| -------------- | ----------- | 
| Initial | 您的 Azure SSIS 整合執行階段的節點尚未配置/備妥。 | 
| 啟動中 | Azure SSIS 整合執行階段的節點正在配置/備妥，並已開始計費。 |
| 已啟動 | Azure SSIS 整合執行階段的節點已配置/備妥，而且它們已準備好部署/執行 SSIS 套件。 |
| 停止中  | Azure SSIS 整合執行階段的節點正在釋出。 |
| 已停止 | Azure SSIS 整合執行階段的節點已釋出並已停止計費。 |

請參閱下列文章以深入了解 Azure SSIS 整合執行階段：

- [Azure SSIS 整合執行階段](concepts-integration-runtime.md#azure-ssis-integration-runtime)。 本文提供整合執行階段的一般概念性資訊，包括 Azure-SSIS IR。 
- [教學課程：將 SSIS 套件部署至 Azure](tutorial-deploy-ssis-packages-azure.md)。 本文逐步說明如何建立 Azure-SSIS IR，並使用 Azure SQL Database 裝載 SSIS 目錄。 
- [如何：建立 Azure-SSIS 整合執行階段](create-azure-ssis-integration-runtime.md)。 這篇文章會展開教學課程，並提供使用 Azure SQL 的受管理執行個體 (私人預覽)，和將 IR 加入 VNet 的指示。 
- [管理 Azure SSIS IR](manage-azure-ssis-integration-runtime.md)。 本文示範如何停止、啟動或移除 Azure-SSIS IR。 它也會告訴您如何將更多節點新增至 IR，藉此相應放大 Azure SSIS IR。 
- [將 VNet 加入至 Azure SSIS IR](join-azure-ssis-integration-runtime-virtual-network.md)。 這篇文章提供將 Azure SSIS IR 加入至 Azure 虛擬網路 (VNet) 的概念資訊。 它也提供使用 Azure 入口網站來設定 VNet，好讓 Azure SSIS IR 可加入 VNet 的步驟。 

## <a name="next-steps"></a>後續步驟
請參閱以下文章，以不同的方式監視管線： 

- [快速入門：建立資料處理站](quickstart-create-data-factory-dot-net.md)。
- [使用 Azure 監視器監視 Data Factory 管線](monitor-using-azure-monitor.md)
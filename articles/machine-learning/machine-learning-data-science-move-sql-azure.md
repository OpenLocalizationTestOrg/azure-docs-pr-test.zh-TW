---
title: "aaaMove 資料 tooan Azure SQL Database 的 Azure Machine Learning |Microsoft 文件"
description: "建立 SQL 資料表並載入資料 tooSQL 資料表"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 50f8b862-4d32-44b2-a1e2-4fbc8024acaa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: b33ef836f42c17a56794baf763281e9998b16bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooan-azure-sql-database-for-azure-machine-learning"></a>移動資料 tooan Azure Machine Learning 的 Azure SQL Database
本主題概述 hello 選項移動資料，從一般檔案 （CSV 或 TSV 格式），或是從儲存在內部部署 SQL Server tooan Azure SQL database 中的資料。 移動資料 toohello 雲端這些工作是 hello 資料科學的小組流程的一部分。

主題會概述移動資料 tooan hello 選項在內部部署 SQL Server 機器學習，請參閱[移動 Azure 的虛擬機器上的資料 tooSQL 伺服器](machine-learning-data-science-move-sql-server-virtual-machine.md)。

hello 下列**功能表**連結 tootopics 描述 tooingest 資料可以儲存和處理期間 hello 資料的目標環境 hello 小組資料科學程序 (TDSP) 的方式。

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

hello 下表摘要列出 hello 選項移動資料 tooan Azure SQL Database。

| <b>來源</b> | <b>目的地：Azure SQL Database</b> |
| --- | --- |
| <b>一般檔案 (CSV 或 TSV 格式)</b> |<a href="#bulk-insert-sql-query">大量插入 SQL 查詢 |
| <b>內部部署 SQL Server</b> |1.<a href="#export-flat-file">匯出 tooFlat 檔案<br> 2.<a href="#insert-tables-bcp">SQL Database 移轉精靈<br> 3.<a href="#db-migration">資料庫備份和還原<br> 4.<a href="#adf">Azure Data Factory |

## <a name="prereqs"></a>必要條件
hello 此處概述的程序需要您具備：

* **Azure 訂用帳戶**。 如果您沒有訂用帳戶，可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure 儲存體帳戶**。 您可以使用 Azure 儲存體帳戶將 hello 資料儲存在本教學課程。 如果您沒有 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)發行項。 建立 hello 儲存體帳戶之後，您會需要 tooobtain hello 帳戶使用 tooaccess hello 儲存體金鑰。 請參閱 [管理儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)。
* 存取 tooan **Azure SQL Database**。 如果您必須設定 Azure SQL Database，[開始使用 Microsoft Azure SQL Database](../sql-database/sql-database-get-started.md)如何提供有關 tooprovision Azure SQL Database 的新執行個體。
* 已在本機上安裝和設定 **Azure PowerShell** 。 如需指示，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

**資料**: hello 移轉程序會示範使用 hello [NYC 計程車資料集](http://chriswhong.com/open-data/foil_nyc_taxi/)。 hello NYC 計程車資料集包含路線資料和 fairs 的相關資訊，並可以在 Azure blob 儲存體： [NYC 計程車資料](http://www.andresmh.com/nyctaxitrips/)。 這些檔案的範例和說明都會在 [NYC 計程車車程資料集說明](machine-learning-data-science-process-sql-walkthrough.md#dataset)中提供。

您可以調整 hello 程序所述的這裡 tooa 組自己的資料，或者遵循 hello 步驟所述使用 hello NYC 計程車資料集。 tooupload hello NYC 計程車資料集在內部部署 SQL Server 資料庫，請遵循 hello 程序中所述[大量匯入資料到 SQL Server 資料庫](machine-learning-data-science-process-sql-walkthrough.md#dbload)。 這些指示適用於 SQL Server 在 Azure 虛擬機器上，但是 hello 程序上傳內部部署 SQL Server 是的 toohello hello 相同。

## <a name="file-to-azure-sql-database"></a>將資料從一般檔案來源 tooan Azure SQL database
一般檔案 （CSV 或 TSV 格式） 中的資料可以是移動的 tooan Azure SQL database 使用大量插入 SQL 查詢。

### <a name="bulk-insert-sql-query"></a> 大量插入 SQL 查詢
hello 程序中使用 hello 大量插入的 SQL 查詢的 hello 步驟都類似 toothose hello Azure VM 上，從一般檔案來源 tooSQL 伺服器移動資料的各節涵蓋。 如需詳細資料，請參閱 [大量插入 SQL 查詢](machine-learning-data-science-move-sql-server-virtual-machine.md#insert-tables-bulkquery)。

## <a name="sql-on-prem-to-sazure-sql-database"></a>將資料從內部部署 SQL Server tooan Azure SQL database
如果 hello 來源資料儲存在內部部署 SQL Server 中，有移動 hello 資料 tooan Azure SQL database 的各種可能性：

1. [匯出 tooFlat 檔案](#export-flat-file)
2. [SQL Database 移轉精靈](#insert-tables-bcp)
3. [資料庫備份和還原](#db-migration)
4. [Azure Data Factory](#adf)

hello hello 前三個步驟是非常類似 toothose 區段中的[移動 Azure 的虛擬機器上的資料 tooSQL 伺服器](machine-learning-data-science-move-sql-server-virtual-machine.md)涵蓋這些相同的程序。 下列指示的 hello 提供的連結 toohello 適當章節的主題。

### <a name="export-flat-file"></a>匯出 tooFlat 檔案
此匯出的 tooa 一般檔案的 hello 步驟如下所述的類似 toothose[匯出 tooFlat 檔案](machine-learning-data-science-move-sql-server-virtual-machine.md#export-flat-file)。

### <a name="insert-tables-bcp"></a>SQL Database 移轉精靈
hello 使用 hello SQL Database 移轉精靈的步驟會在涵蓋的類似 toothose [SQL Database 移轉精靈](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-migration)。

### <a name="db-migration"></a>資料庫備份和還原
hello 步驟，使用資料庫備份和還原所涵蓋的類似 toothose[資料庫備份和還原](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-backup)。

### <a name="adf"></a>Azure Data Factory
hello 主題會提供移動資料 tooan Azure SQL database 與 Azure 資料處理站 (ADF) 中的 hello 程序[將資料從內部部署 SQL server tooSQL Azure 與 Azure Data Factory 移](machine-learning-data-science-move-sql-azure-adf.md)。 本主題說明如何 toomove 資料從內部部署 SQL Server 資料庫 tooan Azure SQL 資料庫透過 Azure Blob 儲存體使用 ADF。

請考慮使用 ADF 資料需求 toobe 持續移轉中存取這兩個內部部署混合式案例時，雲端資源，也 hello 資料會進行交易，或需要時 toobe 修改或商務邏輯加入 tooit 時移轉。 ADF 允許 hello 排程和監視使用簡單的 JSON 指令碼管理 hello 定期執行的資料移動作業。 ADF 也有其他功能，例如支援複雜作業。

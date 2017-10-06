---
title: "從 Azure Blob 儲存體使用 SSIS 連接器 aaaMove 資料 tooor |Microsoft 文件"
description: "移動資料 tooor 從 Azure Blob 儲存體使用 SSIS 連接器。"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 96a1b5fb-34d1-4b9b-8d99-2bb8289e0398
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 15068af1c69f11e74e109ee5ae2b9f1a674ea388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooor-from-azure-blob-storage-using-ssis-connectors"></a>移動資料 tooor 從 Azure Blob 儲存體使用 SSIS 連接器
hello [SQL Server Integration Services 功能套件 azure](https://msdn.microsoft.com/library/mt146770.aspx)提供元件 tooconnect tooAzure 之間傳輸資料 Azure 和內部部署資料來源，以及儲存在 Azure 中的處理序資料。

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

一旦客戶已將內部部署資料移到 hello 的雲端，就可以從任何 Azure 服務 tooleverage hello 的完整功能的 Azure 技術的 hello 套件來進行存取。 例如，可用在 Azure 機器學習服務或 HDInsight 叢集中。

這通常是 hello 第一個步驟是 hello [SQL](machine-learning-data-science-process-sql-walkthrough.md)和[HDInsight](machine-learning-data-science-process-hive-walkthrough.md)逐步解說。

使用 SSIS tooaccomplish 商務標準案例的討論必須在混合式資料整合案例一般，請參閱[這樣做更的 SQL Server Integration Services 功能套件 azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx)部落格。

> [!NOTE]
> 完成簡介 tooAzure blob 儲存體，請參閱太[Azure Blob 的基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和太[Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。
> 
> 

## <a name="prerequisites"></a>必要條件
在本文中說明 tooperform hello 工作您必須擁有 Azure 訂用帳戶和設定 Azure 儲存體帳戶。 您必須知道您 Azure 儲存體帳戶名稱和帳戶金鑰 tooupload 或下載資料。

* 向上 tooset **Azure 訂用帳戶**，請參閱[免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。
* 如需建立 **儲存體帳戶** 以及取得帳戶和金鑰資訊的指示，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。

toouse hello **SSIS 連接器**，您必須下載：

* **SQL Server 2014 或 2016 標準版 (或更新版本)**：安裝包含 SQL Server 整合服務。
* **Microsoft SQL Server 2014 或 azure 2016 Integration Services 功能套件**： 這些可以下載，分別從 hello [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366)和[SQL Server 2016 Integration服務](https://www.microsoft.com/download/details.aspx?id=49492)頁面。

> [!NOTE]
> SSIS 已安裝與 SQL Server，但未包含在 hello Express 版本。 如需 SQL Server 各種版本中包含哪些應用程式的相關資訊，請參閱 [SQL Server 版本](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)
> 
> 

如需 SSIS 的訓練教材，請參閱 [SSIS 實務訓練](http://www.microsoft.com/download/details.aspx?id=20766)

如需詳細資訊 tooget 向上運作使用 SISS toobuild 簡單擷取、 轉換和載入 (ETL) 封裝，請參閱[SSIS 教學課程： 建立簡易 ETL 封裝](https://msdn.microsoft.com/library/ms169917.aspx)。

## <a name="download-nyc-taxi-dataset"></a>下載紐約計程車資料集
hello 範例說明在此使用公開可用的資料集-hello [NYC 計程車往返](http://www.andresmh.com/nyctaxitrips/)資料集。 hello 資料集是由約 173 百萬計程車了 NYC 中 hello 年 2013年所組成。 資料有兩種：路線詳細資料及車費資料。 由於每個月都有一個檔案，因此總共有 24 個檔案，每個檔案未壓縮的大小約 2GB。

## <a name="upload-data-tooazure-blob-storage"></a>上傳資料 tooAzure blob 儲存體
使用 hello SSIS toomove 資料功能從內部部署 tooAzure blob 儲存體的套件，我們使用執行個體的 hello [ **Azure Blob 上傳工作**](https://msdn.microsoft.com/library/mt146776.aspx)，如下所示：

![configure-data-science-vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

hello 工作使用的 hello 參數為此處所述：

| 欄位 | 說明 |
| --- | --- |
| **AzureStorageConnection** |指定現有的 Azure 儲存體連線管理員，或建立新的參考點 toowhere hello blob 檔案的 tooan Azure 儲存體帳戶的其中一個裝載。 |
| **BlobContainer** |指定 hello hello 保存 hello 上傳檔案做為 blob 的 blob 容器名稱。 |
| **BlobDirectory** |指定 hello hello 上傳的檔案儲存為區塊 blob 的 blob 目錄。 hello blob 目錄是虛擬的階層式結構。 如果 hello blob 已經存在，it ia 取代。 |
| **LocalDirectory** |指定包含 hello 檔案 toobe 上傳的 hello 本機目錄。 |
| **FileName** |指定名稱篩選 tooselect 檔案 hello 指定的名稱模式。 例如，MySheet\*.xls\* 包括如 MySheet001.xls 與 MySheetABC.xlsx 等檔案 |
| **TimeRangeFrom/TimeRangeTo** |指定時間範圍篩選器。 會包含在 *TimeRangeFrom* 後和 *TimeRangeTo* 前修改的檔案。 |

> [!NOTE]
> hello **AzureStorageConnection**認證需要 toobe 正確和 hello **BlobContainer** hello 傳輸嘗試之前，必須存在。
> 
> 

## <a name="download-data-from-azure-blob-storage"></a>從 Azure Blob 儲存體下載資料
從 Azure blob 儲存體 tooon 內部儲存體與 SSIS，toodownload 資料使用 hello 的執行個體[Azure Blob 上傳工作](https://msdn.microsoft.com/library/mt146779.aspx)。

## <a name="more-advanced-ssis-azure-scenarios"></a>較進階的 SSIS-Azure 案例
hello SSIS 功能套件可讓您更複雜的流程 toobe 一起由封裝工作。 例如，hello blob 資料無法直接送入的 HDInsight 叢集，無法下載其輸出，回復 tooa blob，然後 tooon 內部儲存體。 SSIS 可使用其他 SSIS 連接器在 HDInsight 叢集上執行 Hive 與 Pig 工作：

* 使用 SSIS 中使用叢集上的 Azure HDInsight Hive 指令碼的 toorun [Azure HDInsight Hive 工作](https://msdn.microsoft.com/library/mt146771.aspx)。
* 使用 SSIS 中使用叢集上的 Azure HDInsight Pig 指令碼的 toorun [Azure HDInsight Pig 工作](https://msdn.microsoft.com/library/mt146781.aspx)。


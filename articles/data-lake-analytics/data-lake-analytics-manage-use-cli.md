---
title: "使用 Azure 命令列介面的 Azure Data Lake Analytics aaaManage |Microsoft 文件"
description: "了解如何 toomanage Data Lake Analytics 帳戶，資料來源、 工作和使用者使用 Azure CLI"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a>使用 Azure 命令列介面 (CLI) 管理 Azure Data Lake Analytics
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

了解 toomanage Azure Data Lake Analytics 帳戶、 資料來源、 使用者和工作使用 hello Azure CLI。 toosee 管理主題使用其他工具中，按一下 [hello] 索引標籤選取上述。


**必要條件**

開始本教學課程之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure CLI**。 請參閱 [安裝和設定 Azure CLI](../cli-install-nodejs.md)。
  * 下載並安裝 hello**發行前版本** [Azure CLI 工具](https://github.com/MicrosoftBigData/AzureDataLake/releases)中排序 toocomplete 此示範。
* **驗證**，並使用下列命令 hello:
  
        azure login
    如需有關如何使用工作或學校帳戶驗證的詳細資訊，請參閱[tooan Azure 訂用帳戶連線從 hello Azure CLI](../xplat-cli-connect.md)。
* **交換器 toohello Azure Resource Manager 模式**，並使用下列命令 hello:
  
        azure config mode arm

**toolist hello 資料湖存放區和 Data Lake Analytics 命令：**

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a>管理帳戶
您必須擁有 Data Lake Analytics 帳戶，才能執行任何 Data Lake Analytics 工作。 與 Azure HDInsight 不同的是，分析帳戶未執行工作時，您無需支付該帳戶的費用。  您只需支付 hello 時間執行作業時。  如需詳細資訊，請參閱 [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。  

### <a name="create-accounts"></a>建立帳戶
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a>更新帳戶
hello 下列命令會更新現有的資料湖分析帳戶 hello 屬性

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a>列出帳戶
列出 Data Lake Analytics 帳戶 

    azure datalake analytics account list

列出特定資源群組內的 Data Lake Analytics 帳戶

    azure datalake analytics account list -g "<Azure Resource Group Name>"

取得特定 Data Lake Analytics 帳戶的詳細資料

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a>刪除 Data Lake Analytics 帳戶
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a>管理帳戶資料來源
Data Lake Analytics 目前支援下列資料來源的 hello:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure 儲存體](../storage/common/storage-introduction.md)

當您建立 Analytics 帳戶時，您必須指定的 Azure 資料湖存放區帳戶 toobe hello 預設儲存體帳戶。 hello ADL 存放裝置會使用預設帳戶 toostore 工作中繼資料和作業的稽核記錄檔。 建立分析帳戶後，就可以新增其他 Azure Data Lake 儲存體帳戶和/或 Azure 儲存體帳戶。 

### <a name="find-hello-default-adl-storage-account"></a>找不到 hello 預設 ADL 儲存體帳戶
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

hello 值都會列在屬性： datalakeStoreAccount:name。

### <a name="add-additional-azure-blob-storage-accounts"></a>新增其他的 Azure Blob 儲存體帳戶
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> 僅支援 Blob 儲存體簡短名稱。  請勿使用 FQDN，例如 "myblob.blob.core.windows.net"。
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a>新增其他的 Data Lake Store 帳戶
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

[-d] 是選擇性參數 tooindicate hello 所加入的資料湖是否 hello 預設資料湖帳戶。 

### <a name="update-existing-data-source"></a>更新現有的資料來源
tooset 現有 Data Lake Store 帳戶 toobe hello 預設值：

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

tooupdate 現有的 Blob 儲存體帳戶金鑰：

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a>列出資料來源：
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Data Lake Analytics 會列出資料來源](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a>刪除資料來源：
toodelete Data Lake Store 帳戶：

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

toodelete Blob 儲存體帳戶：

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a>管理工作
您必須擁有 Data Lake Analytics 帳戶，才能建立工作。  如需詳細資訊，請參閱 [管理 Data Lake Analytics 帳戶](#manage-accounts)。

### <a name="list-jobs"></a>列出工作
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Data Lake Analytics 會列出資料來源](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a>取得工作詳細資料
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a>提交工作
> [!NOTE]
> 工作的 hello 預設優先權為 1000，和工作平行處理原則的 hello 預設程度為 1。
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a>取消工作
使用 hello 清單命令 toofind hello 作業識別碼，然後再使用 [取消] 5d; toocancel hello 作業。

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a>管理目錄
hello U-SQL 目錄會是使用的 toostructure 資料和程式碼，因此它們可以共用 U-SQL 指令碼。 hello 類別目錄可讓 hello Azure Data Lake 中的資料可能的最大效能。 如需詳細資訊，請參閱 [使用 U-SQL 目錄](data-lake-analytics-use-u-sql-catalog.md)。

### <a name="list-catalog-items"></a>列出目錄項目
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

hello 類型包括資料庫、 結構描述、 組件、 外部資料來源、 資料表、 資料表值函式或資料表統計資料。

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a>使用 ARM 群組
應用程式通常由許多元件組成，例如，Web 應用程式、資料庫、資料庫伺服器、儲存體和協力廠商服務。 Azure 資源管理員 (ARM) 可讓您與您的應用程式，為群組參照 tooas Azure 資源群組中的 hello 資源 toowork。 您可以部署、 更新、 監視或刪除所有 hello 資源應用程式在單一、 協調作業。 您會使用部署的範本，且該範本可以用於不同的環境，例如測試、預備和生產環境。 您可以藉由檢視 hello hello 整個群組的彙總成本，計費釐清為您的組織。 如需詳細資訊，請參閱 [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。 

資料湖分析服務可包含下列元件的 hello:

* Azure Data Lake Analytics 帳戶
* 必要的預設 Azure Data Lake 儲存體帳戶
* 其他 Azure Data Lake 儲存體帳戶
* 其他 Azure 儲存體帳戶

您可以建立一個 ARM 群組 toomake 底下的所有這些元件它們更容易 toomanage。

![Azure Data Lake Analytics 帳戶與儲存體](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

Data Lake Analytics 帳戶和 hello 相依的儲存體帳戶必須放置在 hello 相同 Azure 資料中心。
hello ARM 群組不過可以位於不同的資料中心。  

## <a name="see-also"></a>另請參閱
* [Microsoft Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)
* [使用 Azure 入口網站開始使用 Data Lake Analytics](data-lake-analytics-get-started-portal.md)
* [使用 Azure 入口網站管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-portal.md)
* [使用 Azure 入口網站監視和疑難排解 Azure Data Lake Analytics 工作](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)


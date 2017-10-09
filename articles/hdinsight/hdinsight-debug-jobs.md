---
title: "針對 HDInsight 上的 Hadoop 進行偵錯：檢視記錄與解譯錯誤訊息 - Azure | Microsoft Docs"
description: "深入了解管理 HDInsight PowerShell 及步驟可讓您 toorecover 使用時，您可能會收到 hello 錯誤訊息。"
services: hdinsight
tags: azure-portal
editor: cgronlun
manager: jhubbard
author: mumian
documentationcenter: 
ms.assetid: 7e6ceb0e-8be8-4911-bc80-20714030a3ad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 2f12a40e9dcac32ce2e11d66d60d8b3b212ecb53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-hdinsight-logs"></a>分析 HDInsight 記錄檔
Azure HDInsight 中的每個 Hadoop 叢集具有做為 hello 預設的檔案系統的 Azure 儲存體帳戶。 hello 儲存體帳戶會稱為 hello 預設儲存體帳戶。 叢集將使用 hello Azure 資料表儲存體和 hello Blob 儲存體 hello 預設儲存體帳戶 toostore 上其記錄檔。  toofind 出 hello 預設儲存體帳戶用於您的叢集，請參閱[在 HDInsight 中的管理 Hadoop 叢集](hdinsight-administer-use-management-portal.md#find-the-default-storage-account)。 hello 記錄檔會保留 hello 儲存體帳戶，即使 hello 叢集刪除。

## <a name="logs-written-tooazure-tables"></a>記錄寫入 tooAzure 資料表
hello 寫入 tooAzure 資料表的記錄檔提供一層的深入了解發生什麼事與 HDInsight 叢集。

當您建立的 HDInsight 叢集時，6 資料表會自動建立 linux 叢集 hello 預設資料表儲存體中：

* hdinsightagentlog
* syslog
* daemonlog
* hadoopservicelog
* ambariserverlog
* ambariagentlog

針對 Windows 型叢集建立 3 個資料表：

* setuplog：佈建/設定 HDInsight 叢集時發生的事件/例外狀況的記錄檔。
* hadoopinstalllog: hello 叢集上安裝 Hadoop 時發生的事件/例外狀況記錄。 此資料表可能有助於偵錯問題相關 tooclusters 建立使用自訂參數。
* hadoopservicelog：所有 Hadoop 服務記錄的事件/例外狀況的記錄檔。 此資料表可能有助於偵錯在 HDInsight 叢集上的問題相關的 toojob 失敗。

hello 資料表的檔案名稱會是**u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**。

這些資料表包含下列欄位的 hello:

* ClusterDnsName
* ComponentName
* EventTimestamp
* Host
* MALoggingHash
* 訊息
* N
* PreciseTimeStamp
* 角色
* RowIndex
* 租用戶
* 時間戳記
* TraceLevel

### <a name="tools-for-accessing-hello-logs"></a>適用於存取 hello 記錄工具
有許多工具可用來存取這些資料表中的資料：

* Visual Studio
* Azure 儲存體總管
* Power Query for Excel

#### <a name="use-power-query-for-excel"></a>使用 Power Query for Excel
您可以從 [www.microsoft.com/en-us/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379) 安裝 Power Query。 請參閱 hello hello 系統需求的下載頁面

**toouse Power Query tooopen 和分析 hello 服務記錄檔**

1. 開啟 **Microsoft Excel**。
2. 從 hello **Power Query**功能表上，按一下 **從 Azure**，然後按一下**從 Microsoft Azure 資料表儲存體**。
   
    ![HDInsight Hadoop Excel PowerQuery 開啟 Azure 資料表儲存體](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-open.png)
3. 輸入 hello 儲存體帳戶名稱。 這可以是 hello 簡短名稱或 hello FQDN。
4. 輸入 hello 儲存體帳戶金鑰。 您應該會看到一份資料表清單：
   
    ![儲存在 Azure 資料表儲存體中的 HDInsight Hadoop 記錄檔](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-table-names.png)
5. 以滑鼠右鍵按一下 hello hadoopservicelog 資料表在 hello**導覽**窗格，然後選取**編輯**。 您應該會看到 4 個資料行。 選擇性地刪除 hello**資料分割索引鍵**，**資料列索引鍵**，和**時間戳記**資料行，只要選取它們，然後按一下**移除資料行**從 hello 功能區中的 hello 選項。
6. 按一下 hello 展開圖示上 hello 內容要 tooimport hello Excel 試算表的資料行 toochoose hello 資料行。 在此示範中，我選擇 TraceLevel 和 ComponentName：它可以提供一些基本資訊讓我知道哪些元件有問題。
   
    ![HDInsight Hadoop 記錄檔選擇資料行](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-filter.png)
7. 按一下**確定**tooimport hello 資料。
8. 選取 hello **TraceLevel**，角色和**ComponentName**資料行，然後再按一下**Group By** hello 功能區中的控制項。
9. 按一下**確定**hello Group By 對話方塊中
10. 按一下 [套用並關閉]。

您現在可以視需要使用 Excel toofilter 和排序。 很明顯地，您可能想 tooinclude 中向下的順序 toodrill 其他資料行 （例如訊息） 問題發生，但選取並群組 hello 上面所述的資料行提供不錯圖片的 Hadoop 服務發生什麼事時。 hello 相同概念可以套用的 toohello setuplog 和 hadoopinstalllog 資料表。

#### <a name="use-visual-studio"></a>使用 Visual Studio
**toouse Visual Studio**

1. 開啟 Visual Studio。
2. 從 hello**檢視**功能表上，按一下  **Cloud Explorer**。 或直接按一下 **CTRL+\, CTRL+X**。
3. 從 [Cloud Explorer] 中，選取 [資源類型]。  hello 其他可用的選項是**資源群組**。
4. 展開**儲存體帳戶**，hello 叢集中的預設儲存體帳戶，然後**資料表**。
5. 按兩下 [hadoopservicelog]。
6. 新增篩選器。 例如：
   
        TraceLevel eq 'ERROR'
   
    ![HDInsight Hadoop 記錄檔選擇資料行](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-visual-studio-filter.png)
   
    如需建構篩選條件的詳細資訊，請參閱[hello 資料表設計工具建構篩選字串](../vs-azure-tools-table-designer-construct-filter-strings.md)。

## <a name="logs-written-tooazure-blob-storage"></a>記錄檔寫入 tooAzure Blob 儲存體
[hello 記錄寫入的 tooAzure 資料表](#log-written-to-azure-tables)提供一個層級的深入了解發生什麼事與 HDInsight 叢集。 不過，這些資料表並不會提供工作層級記錄檔，這些記錄檔有助於發生問題時進一步深入探索。 tooprovide 這個下一個層級的詳細資料，HDInsight 叢集會設定 toowrite 工作記錄檔 tooyour Blob 儲存體帳戶透過 Templeton 送出任何工作。 實際上，這表示使用 hello Microsoft Azure PowerShell cmdlet 或 hello.NET 作業提交應用程式開發介面，不透過 RDP/命令列存取 toohello 叢集提交的工作提交的工作。 

tooview hello 記錄，請參閱 <<c0> [ 存取 YARN 應用程式記錄檔以 Linux 為基礎的 HDInsight 上](hdinsight-hadoop-access-yarn-app-logs-linux.md)。

如需應用程式記錄檔的詳細資訊，請參閱 [簡化 YARN 的使用者記錄檔管理和存取](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/)。

## <a name="view-cluster-health-and-job-logs"></a>檢視叢集健康情況和工作記錄檔
### <a name="access-hadoop-ui"></a>存取 Hadoop UI
從 hello Azure 入口網站，按一下 HDInsight 叢集名稱 tooopen hello 叢集刀鋒視窗。 從 hello 叢集刀鋒視窗中，按一下 **儀表板**。

![啟動叢集儀表板](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard.png)

出現提示時，輸入 hello 叢集系統管理員認證。 在 hello 開啟的查詢主控台中，按一下  **Hadoop UI**。

![啟動 Hadoop UI](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard-hadoop-ui.png)

### <a name="access-hello-yarn-ui"></a>存取 hello Yarn UI
從 hello Azure 入口網站，按一下 HDInsight 叢集名稱 tooopen hello 叢集刀鋒視窗。 從 hello 叢集刀鋒視窗中，按一下 **儀表板**。 出現提示時，輸入 hello 叢集系統管理員認證。 在 hello 開啟的查詢主控台中，按一下  **YARN UI**。

您可以使用 hello YARN UI toodo hello 下列：

* **取得叢集狀態**。 從 hello 左窗格中，展開**叢集**，然後按一下**有關**。 此存在叢集狀態詳細資料，例如配置記憶體、 核心使用，總共 hello 叢集資源管理員的狀態時，叢集版本等等。
  
    ![啟動叢集儀表板](./media/hdinsight-debug-jobs/hdi-debug-yarn-cluster-state.png)
* **取得節點狀態**。 從 hello 左窗格中，展開**叢集**，然後按一下**節點**。 這會列示在 hello 叢集，每個節點、 資源配置的 tooeach 節點和其他內容的 HTTP 位址的所有 hello 節點。
* **監視工作狀態**。 從 hello 左窗格中，展開**叢集**，然後按一下**應用程式**toolist 所有 hello hello 叢集中的作業。 如果您想在特定的工作 toolook 狀態 （例如新送出，執行等），按一下 [hello] 下方的適當連結**應用程式**。 您可以進一步按一下 hello 作業名稱 toofind hello 工作這類包括 hello 輸出、 記錄檔等深入了解。

### <a name="access-hello-hbase-ui"></a>存取 hello HBase UI
從 hello Azure 入口網站，按一下 HDInsight HBase 叢集名稱 tooopen hello 叢集刀鋒視窗。 從 hello 叢集刀鋒視窗中，按一下 **儀表板**。 出現提示時，輸入 hello 叢集系統管理員認證。 在 hello 開啟的查詢主控台中，按一下  **HBase UI**。

## <a name="hdinsight-error-codes"></a>HDInsight 錯誤代碼
hello 分本節中的錯誤訊息所提供的 Azure HDInsight 中的 Hadoop toohelp hello 使用者了解可能的錯誤狀況，他們可以在管理使用 Azure PowerShell 及 tooadvise hello 服務時遇到在 hello 步驟這可以採取 toorecover hello 錯誤。

其中某些錯誤訊息可能也會出現在 hello Azure 入口網站時使用的 toomanage HDInsight 叢集。 但您可能會遇到其他錯誤訊息有較不精細到期 toohello hello 修復動作可能在此內容中的條件約束。 Hello 緩和所在明顯 hello 內容提供的其他錯誤訊息。 

### <a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided
* **描述**： 請提供 Azure SQL database 詳細資料至少一個元件中順序 toouse Hive 和 Oozie 中繼存放區的自訂設定。
* **風險降低**: hello 使用者需要 toosupply 為有效 SQL Azure 中繼存放區，然後重試 hello 的要求。  

### <a id="AzureRegionNotSupported"></a>AzureRegionNotSupported
* **描述**：無法在區域 *nameOfYourRegion*中建立叢集。 請使用有效的 HDInsight 區域，然後重試要求。
* **風險降低**： 客戶應該建立目前支援它們的 hello 叢區域： 東南亞、 西歐、 北歐、 美國東部、 或美國西部。  

### <a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound
* **描述**: hello 伺服器找不到 hello 要求叢集記錄。  
* **風險降低**: hello 作業重試一次。

### <a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord
* **描述**：叢集 DNS 名稱 *yourDnsName* 無效。 請確定名稱以英數字元開始和結束，且只包含 '-' 特殊字元  
* **風險降低**： 請確定您使用的是有效的 DNS 名稱為您的叢集，開頭和結尾是英數字元，並不包含任何特殊字元而不是 hello 虛線 '-'，然後重試 hello 作業。

### <a id="ClusterNameUnavailable"></a>ClusterNameUnavailable
* **描述**：叢集名稱 *yourClusterName* 無法使用。 請挑選其他名稱。  
* **風險降低**: hello 使用者應該指定唯一 clustername 並不存在，然後再試一次。 如果 hello 使用者正在使用 hello 入口網站，UI 會通知方式如果叢集名稱已在 hello 期間使用的 hello 建立步驟。

### <a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid
* **描述**：叢集密碼無效。 密碼必須至少 10 個字元，必須包含至少一個數字、 大寫字母、 小寫字母和不含空格的特殊字元，且不能包含 hello 做為其一部分的使用者名稱。  
* **風險降低**： 提供有效的叢集密碼，然後重試 hello 作業。

### <a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid
* **描述**：叢集使用者名稱無效。 請確定使用者名稱不含特殊字元或空格。  
* **風險降低**： 提供有效的叢集使用者名稱，然後重試 hello 作業。

### <a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord
* **描述**：叢集 DNS 名稱 *yourDnsClusterName* 無效。 請確定名稱以英數字元開始和結束，且只包含 '-' 特殊字元  
* **風險降低**： 提供有效的 DNS 叢集使用者名稱，然後重試 hello 作業。

### <a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName
* **描述**: URI 中的容器名稱*yourcontainerURI*和 DNS 名稱*yourDnsName*在要求主體必須是 hello 相同。  
* **風險降低**： 請確定您的容器名稱和您的 DNS 名稱 hello 相同，然後重試 hello 作業。

### <a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound
* **描述**：叢集組態無效。 無法 toofind 任何資料節點中的定義節點大小。  
* **風險降低**: hello 作業重試一次。

### <a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure
* **描述**: hello 叢集無法刪除部署  
* **風險降低**: hello 刪除作業重試一次。

### <a id="DnsMappingNotFound"></a>DnsMappingNotFound
* **描述**：服務組態錯誤。 找不到必要的 DNS 對應資訊。  
* **緩和**：刪除叢集，然後建立新的叢集。

### <a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest
* **描述**：嘗試建立重複的叢集容器。 已存在 *nameOfYourContainer* 的記錄，但 Etag 不符。
* **風險降低**: hello 容器和重試 hello 建立操作提供唯一的名稱。

### <a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService
* **描述**：代管服務 *nameOfYourHostedService* 已包含叢集。 代管服務不可包含多個叢集  
* **風險降低**： 主機 hello 叢集在另一個託管服務。

### <a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus
* **描述**: hello server 無法更新 hello 叢集部署的 hello 狀態。  
* **風險降低**: hello 作業重試一次。 如果此情況發生多次，請連絡 CSS。

### <a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered
* **描述**：維護時已刪除叢集 *yourClusterName* 。 請重新建立 hello 叢集。
* **風險降低**： 重新建立 hello 叢集。

### <a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound
* **描述**：叢集組態無效。 在節點大小中找不到必要的前端節點組態。
* **風險降低**: hello 作業重試一次。

### <a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure
* **描述**： 無法 toocreate 託管服務*nameOfYourHostedService*。 請重試要求。  
* **風險降低**: hello 的重試要求。

### <a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment
* **描述**：託管服務「nameOfYourHostedService」已有生產部署。 代管服務不可包含多個生產部署 重試 hello 要求以不同的叢集名稱。
* **風險降低**： 使用不同的叢集名稱，然後重試 hello 要求。

### <a id="HostedServiceNotFound"></a>HostedServiceNotFound
* **描述**： 託管服務*nameOfYourHostedService*找不到 hello 叢集。  
* **風險降低**: hello 叢集處於錯誤狀態時，如果刪除它，並再試一次。

### <a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment
* **描述**：代管服務 *nameOfYourHostedService* 沒有相關聯的部署。  
* **風險降低**: hello 叢集處於錯誤狀態時，如果刪除它，並再試一次。

### <a id="InsufficientResourcesCores"></a>InsufficientResourcesCores
* **描述**: hello SubscriptionId *yourSubscriptionId*沒有核心左的 toocreate 叢集*yourClusterName*。 必要：「resourcesRequired」、可用：「resourcesAvailable」。  
* **風險降低**： 釋放您的訂用帳戶中的資源或增加 hello 資源可用 toohello 訂用帳戶然後再試一次 toocreate hello 叢集。

### <a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices
* **描述**： 訂用帳戶 ID *yourSubscriptionId*沒有配額，以便為新的託管服務 toocreate 叢集*yourClusterName*。  
* **風險降低**： 釋放您的訂用帳戶中的資源或增加 hello 資源可用 toohello 訂用帳戶然後再試一次 toocreate hello 叢集。

### <a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest
* **描述**: hello 伺服器發生內部錯誤。 請重試要求。  
* **風險降低**: hello 的重試要求。

### <a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation
* **描述**：Azure 儲存體位置 *dataRegionName* 不是有效的位置。 請確定 hello 區域正確，然後重試要求。
* **風險降低**： 選取支援 HDInsight 的存放位置，請檢查您的叢集已共然後重試 hello 作業。

### <a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode
* **描述**：資源節點的 VM 大小無效。 所有資料節點僅支援 'Large VM' 大小。  
* **風險降低**： 指定支援的 hello 節點大小的 hello 資料節點，然後重試 hello 作業。

### <a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode
* **描述**：前端節點的 VM 大小無效。 前端節點僅支援 'ExtraLarge VM' 大小。  
* **風險降低**： 指定支援的 hello hello 前端節點的節點大小，然後重試 hello 作業

### <a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion
* **描述**： 訂用帳戶 ID *yourSubscriptionId*正在使用沒有叢集的足夠權限 tooexecute 刪除作業*yourClusterName*。  
* **風險降低**: hello 叢集處於錯誤狀態時，如果卸除它，並再試一次。  

### <a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName
* **描述**：外部儲存帳戶 Blob 容器名稱 *yourContainerName* 無效。 請確定名稱以字母開頭，且只包含小寫字母、數字和虛線。  
* **風險降低**： 指定有效的儲存體帳戶 blob 容器名稱，然後重試 hello 作業。

### <a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey
* **描述**： 外部儲存體帳戶的組態*yourStorageAccountName*祕密金鑰的詳細資料是必要的 toohave toobe 組。  
* **風險降低**： 指定有效的密碼金鑰 hello 儲存體帳戶，然後重試 hello 作業。

### <a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat
* **描述**：版本標頭 *yourVersionHeader* 不是有效格式 yyyy-mm-dd。  
* **風險降低**： 指定有效的格式為 hello 版本標頭，然後重試 hello 要求。

### <a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode
* **描述**：叢集組態無效。 發現多個前端節點組態。  
* **風險降低**： 編輯 hello 組態，使得只有一個前端節點指定。

### <a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest
* **描述**: hello 作業無法完成 hello 允許的時間內或 hello 最大重試嘗試盡量。 請重試要求。  
* **風險降低**: hello 的重試要求。

### <a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty
* **描述**：參數 *yourParameterName* 不可為 Null 或空白。  
* **風險降低**： 指定有效的值為 hello 參數。

### <a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure
* **描述**： 一或多個 hello 叢集建立要求輸入無效。 請確定 hello 輸入的值正確，然後重試要求。  
* **風險降低**： 請確定 hello 輸入的值是否正確，然後重試要求。

### <a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable
* **描述**：區域「yourRegionName」和訂用帳戶識別碼「yourSubscriptionId」無法使用區域功能。  
* **緩和**：請指定支援 HDInsight 叢集的區域。 公開支援 hello 區域是一種： 東南亞、 西歐、 北歐、 美國東部、 或美國西部。

### <a id="StorageAccountNotColocated"></a>StorageAccountNotColocated
* **描述**：儲存體帳戶「yourStorageAccountName」位於區域「currentRegionName」中。 它應該是相同 hello 叢區域*yourClusterRegionName*。  
* **風險降低**： 指定儲存體帳戶在 hello 叢集位於相同區域中，或如果您的資料已經 hello 儲存體帳戶中，建立新叢集 hello 與 hello 現有儲存體帳戶相同的區域。 如果您使用 hello 入口網站，hello UI 會事先通知他們這個問題。

### <a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive
* **描述**：並未使用指定的訂用帳戶識別碼 *yourSubscriptionId* 。  
* **緩和**：請重新啟用訂用帳戶，或取得新的有效訂用帳戶。

### <a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound
* **描述**：找不到訂用帳戶識別碼 *yourSubscriptionId* 。  
* **風險降低**： 請檢查您的訂用帳戶識別碼是否有效，然後重試 hello 作業。

### <a id="UnableToResolveDNS"></a>UnableToResolveDNS
* **描述**： 無法 tooresolve DNS *yourDnsUrl*。 請中提供 hello blob 端點，確定 hello 完整 URL。  
* **緩和**：提供有效的 Blob URL。 hello URL 必須是完整有效的包括開頭*http://*中和結束*.com*。

### <a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource
* **描述**： 資源無法 tooverify 位置*yourDnsUrl*。 請中提供 hello blob 端點，確定 hello 完整 URL。  
* **緩和**：提供有效的 Blob URL。 hello URL 必須是完整有效的包括開頭*http://*中和結束*.com*。

### <a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable
* **描述**：版本「specifiedVersion」和訂用帳戶識別碼「yourSubscriptionId」無法使用版本功能。  
* **風險降低**： 選擇可用的版本，然後重試 hello 作業。

### <a id="VersionNotSupported"></a>VersionNotSupported
* **描述**：不支援版本 *specifiedVersion* 。
* **風險降低**： 選擇支援的版本，然後重試 hello 作業。

### <a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion
* **描述**：Azure 區域「specifiedRegion」中無法使用版本「specifiedVersion」。  
* **風險降低**： 選擇支援指定的 hello 區域中的版本，然後重試 hello 作業。

### <a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound
* **描述**：叢集組態無效。 在外部帳戶中找不到必要的 WASB 帳戶組態。  
* **風險降低**： 確認 hello 帳戶存在，而且是正常作業中指定的組態，然後重試 hello。

## <a name="next-steps"></a>後續步驟
* [HDInsight 上使用 Ambari 檢視 toodebug Tez 作業](hdinsight-debug-ambari-tez-view.md)
* [在以 Linux 為基礎的 HDInsight 上啟用 Hadoop 服務的堆積傾印](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [使用 hello Ambari Web UI 來管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)


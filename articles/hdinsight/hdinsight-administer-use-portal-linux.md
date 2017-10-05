---
title: "使用 Azure 入口網站管理 HDInsight 中的 Hadoop 叢集 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站來監視和管理 HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c9cb631aef71f72457c3517d02566a56919f82bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-the-azure-portal"></a>使用 Azure 入口網站管理 HDInsight 上的 Hadoop 叢集
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

使用 [Azure 入口網站][azure-portal]，您可以管理 Azure HDInsight 中的 Hadoop 叢集。 使用索引標籤選取器，以取得使用其他工具管理 HDInsight 中 Hadoop 叢集的詳細資訊。

**必要條件**

開始閱讀本文之前，您必須有下列各項：

* **Azure 訂用帳戶**。 請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。

## <a name="open-the-portal"></a>開啟入口網站
1. 登入 [https://portal.azure.com](https://portal.azure.com)。
2. 開啟入口網站之後，您可以：

   * 按一下左功能表中的 [新增]  以建立新的叢集：

       ![新的 HDInsight 叢集按鈕](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * 按一下左側功能表中的 [HDInsight 叢集]  以列出現有的叢集

       ![Azure 入口網站 HDInsight 叢集按鈕](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       如果您沒有看見 HDInsight 叢集，請按一下位於清單底部的 [更多服務]，然後按一下位於 [智慧 + 分析] 區段底下的 [HDInsight 叢集]。


## <a name="create-clusters"></a>建立叢集
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

HDInsight 可以與很多 Hadoop 元件搭配使用。 如需已驗證和所支援元件的清單，請參閱 [Azure HDInsight 提供 Hadoop 的什麼版本？](hdinsight-component-versioning.md)(英文)。 如需一般叢集建立的資訊，請參閱 [在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

### <a name="access-control-requirements"></a>存取控制需求

當您建立 HDInsight 叢集時，必須指定 Azure 訂用帳戶。 這個叢集可在新的 Azure 資源群組中建立，或是在現有的資源群組中建立。 您可以使用下列步驟，確認您具有建立 HDInsight 叢集的權限：

- 使用現有的資源群組。

    1. 登入 [Azure 入口網站](https://portal.azure.com)。
    2. 按一下左側功能表的 [資源群組] 以列出資源群組。
    3. 按一下您要用來建立 HDInsight 叢集的資源群組。
    4. 按一下 [存取控制 (IAM)]，然後確認您 (或是您所屬的群組) 至少具有資源群組的「參與者」存取權限。

- 建立新的資源群組

    1. 登入 [Azure 入口網站](https://portal.azure.com)。
    2. 按一下左側功能表的 [訂用帳戶]。 它有黃色的鑰匙圖示。 您應該會看到訂用帳戶清單。
    3. 按一下您要用來建立叢集的訂用帳戶。 
    4. 按一下 [我的權限]。  它會顯示您在訂用帳戶上的[角色](../active-directory/role-based-access-control-what-is.md#built-in-roles)。 您至少需要「參與者」存取權限才能建立 HDInsight 叢集。

如果您收到 NoRegisteredProviderFound 錯誤或 MissingSubscriptionRegistration 錯誤，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](../azure-resource-manager/resource-manager-common-deployment-errors.md)。

## <a name="list-and-show-clusters"></a>列出和顯示叢集
1. 登入 [https://portal.azure.com](https://portal.azure.com)。
2. 按一下左側功能表中的 [HDInsight 叢集]  以列出現有的叢集。
3. 按一下叢集名稱。 如果叢集清單很長，您可以使用頁面頂端的篩選器。
4. 按一下清單中的叢集以顯示概觀頁面：

    ![Azure portal HDInsight cluster essentials](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * **儀表板**：開啟叢集儀表板，這是適用於以 Linux 為基礎之叢集的 Ambari Web。
    * **安全殼層**︰顯示使用安全殼層 (SSH) 連線連接到叢集的指示。
    * **調整叢集**：可讓您變更此叢集的背景工作節點數目。
    * **刪除**：刪除叢集。
    * **活動記錄檔**︰顯示和查詢活動記錄檔。
    * **存取控制 (IAM)**︰使用角色指派。  請參閱[使用角色指派來管理 Azure 訂用帳戶資源的存取權](../active-directory/role-based-access-control-configure.md)。
    * **標記**：可讓您設定索引鍵/值組，以定義自訂的雲端服務分類法。 例如，您可建立名為 **project**的索引鍵，然後使用與特定專案相關聯之所有服務的通用值。
    * **診斷並解決問題**︰顯示疑難排解資訊。
    * **鎖定**︰新增鎖定以防止叢集遭到修改或刪除。
    * **自動化指令碼**︰顯示和匯出叢集的 Azure Resource Manager 範本。 目前，您只能匯出相依的 Azure 儲存體帳戶。 請參閱[使用 Azure Resource Manager 範本在 HDInsight 中建立 Linux 型 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)。
    * **快速啟動**：顯示可協助您開始使用 HDInsight 的資訊。
    * **適用於 HDInsight 的工具**：HDInsight 相關工具的說明資訊。
    * **叢集登入**︰顯示叢集登入資訊。
    * **訂用帳戶核心使用量**︰顯示訂用帳戶的已使用和可用核心。
    * **調整叢集**：增加和減少叢集背景工作角色節點的數目。 請參閱[調整叢集](hdinsight-administer-use-management-portal.md#scale-clusters)。
    * **安全殼層**︰顯示使用安全殼層 (SSH) 連線連接到叢集的指示。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。
    * **HDInsight 合作夥伴**︰新增/移除目前的 HDInsight 合作夥伴。
    * **外部中繼存放區**：檢視 Hive 和 Oozie 中繼存放區。 中繼存放區只可以在叢集建立程序期間進行設定。 請參閱[使用 Hive/Oozie 中繼存放區](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore)。
    * **指令碼動作**︰在叢集上執行 Bash 指令碼。 請參閱 [使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。
    * **應用程式**：新增/移除 HDInsight 應用程式。  請參閱[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)。
    * **屬性**：檢視叢集屬性。
    * **儲存體帳戶**︰檢視儲存體帳戶和金鑰。 儲存體帳戶是在進行叢集建立程序時設定。
    * **叢集 AAD 身分識別**：
    * **新的支援要求**︰可讓您透過 Microsoft 支援服務建立支援票證。
    
6. 按一下 [屬性] ：

    屬性如下︰

   * **主機名稱**：叢集名稱。
   * **叢集 URL**。 Ambari Web 介面的 URL。
   * **狀態**：包括Aborted、Accepted、ClusterStorageProvisioned、AzureVMConfiguration、HDInsightConfiguration、Operational、Running、Error、Deleting、Deleted、Timedout、DeleteQueued、DeleteTimedout、DeleteError、PatchQueued、CertRolloverQueued、ResizeQueued、ClusterCustomization
   * **區域**：Azure 位置。 如需支援的 Azure 位置清單，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)上的 [區域] 下拉式清單方塊。
   * **建立日期**。
   * **作業系統**：**Windows** 或 **Linux**。
   * **類型**：Hadoop、HBase、Storm、Spark。
   * **版本**。 請參閱 [HDInsight 版本](hdinsight-component-versioning.md)
   * **訂用帳戶**︰訂用帳戶名稱。
   * **預設資料來源**︰預設叢集檔案系統。
   * **背景工作節點**。
   * **前端節點大小**。

## <a name="delete-clusters"></a>刪除叢集
刪除叢集時，並不會刪除預設的儲存體帳戶或任何連結的儲存體帳戶。 您可以使用相同的儲存體帳戶和相同的中繼存放區重新建立叢集。 建議您在重新建立叢集時使用新的預設 Blob 容器。

1. 登入[入口網站][azure-portal]。
2. 按一下左功能表中的 [HDInsight 叢集]  。 如果您沒有看到 [HDInsight 叢集]，可先按一下 [更多服務]。
3. 按一下您想要刪除的叢集。
4. 按一下頂端功能表中的 [刪除]  ，然後依照指示執行。

另請參閱 [暫停/關閉叢集](#pauseshut-down-clusters)。

## <a name="add-additional-storage-accounts"></a>新增其他儲存體帳戶

建立叢集之後，您可以新增其他 Azure 儲存體帳戶和 Azure Data Lake Store 帳戶。 如需詳細資訊，請參閱[將其他儲存體帳戶新增至 HDInsight](./hdinsight-hadoop-add-storage.md)。

## <a name="scale-clusters"></a>調整叢集
叢集調整功能可讓您變更在 Azure HDInsight 中執行的叢集所用的背景工作節點數目，而不需要重新建立叢集。

> [!NOTE]
> 只支援使用 HDInsight 3.1.3 版或更高版本的叢集。 如果不確定您的叢集版本，您可以檢查 [屬性] 頁面。  請參閱[列出和顯示叢集](#list-and-show-clusters)。
>
>

變更 HDInsight 支援的每一種叢集所用的資料節點數目會有何影響：

* Hadoop

    您可以順暢地增加正在執行的 Hadoop 叢集中背景工作節點數目，而不會影響任何擱置或執行中的工作。 您也可以在作業進行當中提交新工作。 系統會順暢處理失敗的調整作業，讓叢集永保正常運作狀態。

    減少資料節點數目以縮減 Hadoop 叢集時，系統會重新啟動叢集中的部分服務。 此行為會導致所有執行中和擱置的工作在調整作業完成時失敗。 但您可以在作業完成後重新提交這些工作。
* HBase

    您可以順暢地在 HBase 叢集運作時對其新增或移除資料節點。 區域伺服器會在完成調整作業的數分鐘之內自動取得平衡。 但是，您也可以手動平衡區域伺服器，方法是登入叢集的前端節點，然後從命令提示字元視窗執行下列命令：

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    如需使用 HBase 殼層的詳細資訊，請參閱 []
* Storm

    您可以順暢地在 Storm 叢集運作時對其新增或移除資料節點。 但在調整作業順利完成後，您需要重新平衡拓撲。

    您可以使用兩種方式來完成重新平衡作業：

  * Storm Web UI
  * 命令列介面 (CLI) 工具

    如需詳細資訊，請參閱 [Apache Storm 文件](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) 。

    HDInsight 叢集上有提供 Storm Web UI：

    ![HDInsight Storm 調整重新平衡](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    以下是如何使用 CLI 命令重新平衡 Storm 拓撲的範例：

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**調整叢集**

1. 登入[入口網站][azure-portal]。
2. 按一下左功能表中的 [HDInsight 叢集]  。
3. 按一下您想要調整的叢集。
3. 按一下 [調整叢集]。
4. 輸入 **背景工作節點的數目**。 叢集節點的數目限制會因 Azure 訂用帳戶而有所不同。 請連絡帳務支援提高限制。  成本資訊會反映您對節點數目所做的變更。

    ![HDInsight hadoop hbase storm spark scale](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a>暫停/關閉叢集

大部分 Hadoop 工作是只會偶爾執行的批次工作。 對於大部分的 Hadoop 叢集而言，叢集長時間並未用於處理。 利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。
您也需支付 HDInsight 叢集的費用 (即使未使用)。 由於叢集費用是儲存體費用的許多倍，所以刪除未使用的叢集符合經濟效益。

有許多方法可以設計程序：

* 使用 Azure Data Factory。 如需建立隨選 HDInsight 連結服務，請參閱 [使用 Azure Data Factory 在 HDInsight 中建立 Linux 型隨選 Handooop 叢集](hdinsight-hadoop-create-linux-clusters-adf.md) 。
* 使用 Azure PowerShell。  請參閱 [分析航班延誤資料](hdinsight-analyze-flight-delay-data.md)。
* 使用 Azure CLI。 請參閱 [使用 Azure CLI 管理 HDInsight 叢集](hdinsight-administer-use-command-line.md)。
* 使用 HDInsight .NET SDK。 請參閱 [提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)。

如需定價資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。 若要從入口網站刪除叢集，請參閱 [刪除叢集](#delete-clusters)


## <a name="upgrade-clusters"></a>升級叢集

請參閱[將 HDInsight 叢集升級為更新的版本](./hdinsight-upgrade-cluster.md)。

## <a name="change-passwords"></a>變更密碼
HDInsight 叢集可以有兩個使用者帳戶。 HDInsight 叢集使用者帳戶 (A.K.A. HTTP 使用者帳戶) 以及 SSH 使用者帳戶都會在建立程序期間建立。 您可以使用 Ambari Web UI 來變更叢集使用者帳戶的使用者名稱、密碼，以及用於變更 SSH 使用者帳戶的指令碼動作。

### <a name="change-the-cluster-user-password"></a>變更叢集使用者密碼
您可以使用 Ambari Web UI 來變更叢集使用者密碼。 若要登入 Ambari，您必須使用現有的叢集使用者名稱和密碼。

> [!NOTE]
> 變更叢集使用者 (管理員) 密碼可能會造成針對此叢集執行的指令碼動作失敗。 如果您有任何以背景工作節點為目標的持續性指令碼動作，當您透過調整大小作業新增節點到叢集，這些指令碼可能會失敗。 如需指令碼動作的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。
>
>

1. 使用 HDInsight 叢集使用者認證登入 Ambari Web UI。 預設的使用者名稱為 **admin**。URL 是 **https://&lt;HDInsight 叢集名稱>azurehdinsight.net**。
2. 按一下頂端功能表中的 [管理]  ，然後按一下 [管理 Ambari]。
3. 按一下左側功能表中的 [使用者] 。
4. 按一下 Admin 。
5. 按一下 [變更密碼] 。

Ambari 會變更叢集中所有節點上的密碼。

### <a name="change-the-ssh-user-password"></a>變更 SSH 使用者密碼
1. 使用文字編輯器，將下列文字儲存為檔案並命名為 **changepassword.sh**。

   > [!IMPORTANT]
   > 您必須使用行尾結束符號為 LF 的編輯器。 如果編輯器使用 CRLF，指令碼會無法運作。
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. 將檔案上傳至可以使用 HTTP 或 HTTPS 位址從 HDInsight 存取的儲存位置。 例如，OneDrive 或 Azure Blob 儲存體這類的公用檔案存放區。 將 URI (HTTP 或 HTTPS 位址) 儲存至檔案，在下一個步驟需用到此 URI。
3. 從 Azure 入口網站，按一下 [HDInsight 叢集]。
4. 按一下您的 HDInsight 叢集。
4. 按一下 [指令碼動作]。
4. 從 [指令碼動作] 刀鋒視窗中，選取 [提交新的]。 [提交指令碼動作] 刀鋒視窗出現後，輸入下列資訊：

   | 欄位 | 值 |
   | --- | --- |
   | Name |變更 SSH 密碼 |
   | Bash 指令碼 URI |changepassword.sh 檔案的 URI |
   | 節點 (前端、背景工作、Nimbus、監督員、Zookeeper 等) |✓ 針對列出的所有節點類型 |
   | 參數 |輸入 SSH 使用者名稱，然後輸入密碼。 使用者名稱和密碼之間應該有一個空格。 |
   | 保存這個指令碼動作... |不選取此欄位。 |
5. 按一下 [建立] 套用指令碼。 指令碼完成後，您可以使用 SSH 與新密碼連線到叢集。

## <a name="grantrevoke-access"></a>授與/撤銷存取權
HDInsight 叢集具有下列 HTTP Web 服務 (所有這些服務都有 RESTful 端點)：

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

預設會授與這些服務的存取權。 您可以使用 [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) 和 [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access) 撤銷/授與存取權。

## <a name="find-the-subscription-id"></a>尋找訂用帳戶識別碼

**尋找您的 Azure 訂用帳戶識別碼**

1. 登入[入口網站][azure-portal]。
2. 按一下 [訂用帳戶]。 每個訂用帳戶都有一個名稱和一個識別碼。

每個叢集都會繫結至一個 Azure 訂用帳戶。 訂用帳戶識別碼會顯示在叢集 [基本資料]  圖格上。 請參閱 [列出和顯示叢集](#list-and-show-clusters)。

## <a name="find-the-resource-group"></a>尋找資源群組
在 Azure Resource Manager 模式中，每個 HDInsight 叢集是隨著 Azure Resource Manager 群組一起建立。 叢集所屬的 Resource Manager 群組會出現於：

* 叢集清單含有 [資源群組]  資料行。
* 叢集 [基本資料]  磚。  

請參閱 [列出和顯示叢集](#list-and-show-clusters)。

## <a name="find-the-default-storage-account"></a>尋找預設的儲存體帳戶
每個 HDInsight 叢集都有預設的儲存體帳戶。 叢集的預設儲存體帳戶與其金鑰會顯示在 [儲存體帳戶] 之下。 請參閱 [列出和顯示叢集](#list-and-show-clusters)。

## <a name="run-hive-queries"></a>執行 Hive 查詢
您無法直接從 Azure 入口網站執行 Hive 作業，但您可以使用 Ambari Web UI 上的 Hive 檢視。

**使用 Ambari Hive 檢視執行 Hive 查詢**

1. 使用 HDInsight 叢集使用者認證登入 Ambari Web UI。 預設的使用者名稱為 **admin**。URL 是 **https://&lt;HDInsight 叢集名稱>azurehdinsight.net**。
2. 開啟 [Hive 檢視]，如下列螢幕擷取畫面所示：  

    ![HDInsight Hive 檢視](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. 按一下頂端功能表中的 [查詢]  。
4. 在 [查詢編輯器] 中輸入 Hive 查詢，然後按一下 [執行]。

## <a name="monitor-jobs"></a>監視工作
請參閱 [使用 Ambari Web UI 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md#monitoring)。

## <a name="browse-files"></a>瀏覽檔案
使用 Azure 入口網站時，您可以瀏覽預設容器的內容。

1. 登入 [https://portal.azure.com](https://portal.azure.com)。
2. 按一下左側功能表中的 [HDInsight 叢集]  以列出現有的叢集。
3. 按一下叢集名稱。 如果叢集清單很長，您可以使用頁面頂端的篩選器。
4. 按一下叢集左側功能表中的 [儲存體帳戶]。
5. 按一下 [儲存體帳戶]。
7. 按一下 [blob]  圖格。
8. 按一下預設容器名稱。

## <a name="monitor-cluster-usage"></a>監視叢集使用量
HDInsight 叢集刀鋒視窗的 [使用量] 區段會顯示以下資訊：訂用帳戶可搭配 HDInsight 使用的核心數目，以及配置給此叢集的核心數目和它們在此叢集中配置給節點的方式。 請參閱 [列出和顯示叢集](#list-and-show-clusters)。

> [!IMPORTANT]
> 若要監視 HDInsight 叢集所提供的服務，您必須使用 Ambari Web 或 Ambari REST API。 如需使用 Ambari 的詳細資訊，請參閱 [使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="connect-to-a-cluster"></a>連接到叢集

* [〈搭配 HDInsight 使用 Hivet〉](hdinsight-hadoop-use-hive-ambari-view.md)
* [搭配使用 SSH 與 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a>後續步驟
在本文中，您已了解一些基本的系統管理函式。 若要深入了解，請參閱下列文章：

* [使用 Azure PowerShell 管理 HDInsight](hdinsight-administer-use-powershell.md)
* [使用 Azure CLI 管理 HDInsight](hdinsight-administer-use-command-line.md)
* [建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)
* [在 HDInsight 中使用 Hive](hdinsight-use-hive.md)
* [在 HDInsight 中使用 Pig](hdinsight-use-pig.md)
* [在 HDInsight 中使用 Sqoop](hdinsight-use-sqoop.md)
* [開始使用 Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Azure HDInsight 提供 Hadoop 的什麼版本？](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Hadoop 命令列"

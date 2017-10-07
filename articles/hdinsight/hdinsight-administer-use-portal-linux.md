---
title: "使用 Azure 入口網站的 HDInsight 叢集 aaaManage Hadoop |Microsoft 文件"
description: "深入了解如何 toocreate 和管理 HDInsight 叢集使用 hello Azure 入口網站。"
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
ms.openlocfilehash: c242d43d4ccea7cf1e7be19c3f3d7ed3c4f50918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>透過 hello Azure 入口網站來管理 HDInsight 中的 Hadoop 叢集
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

使用 hello [Azure 入口網站][azure-portal]，您可以管理在 Azure HDInsight Hadoop 叢集。 如需有關管理中使用其他工具的 HDInsight Hadoop 叢集資訊使用 hello 索引標籤選取器。

**必要條件**

在開始這份文件之前，您必須擁有 hello 下列項目：

* **Azure 訂用帳戶**。 請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。

## <a name="open-hello-portal"></a>開啟 hello 入口網站
1. 登入太[https://portal.azure.com](https://portal.azure.com)。
2. 開啟 hello 入口網站之後，您可以：

   * 按一下**新增**從 hello 左側的功能表 toocreate 新叢集：

       ![新的 HDInsight 叢集按鈕](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * 按一下**HDInsight 叢集**hello 從左側的功能表 toolist hello 現有叢集

       ![Azure 入口網站 HDInsight 叢集按鈕](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       如果您沒有看到 HDInsight 叢集，按一下 **更多服務**在 hello hello 清單的底部，然後按一下 **HDInsight 叢集**下 hello**智慧 + 分析**一節。


## <a name="create-clusters"></a>建立叢集
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

HDInsight 可以與很多 Hadoop 元件搭配使用。 Hello 驗證以及支援 hello 元件清單，請參閱[的 Hadoop 版本是在 Azure HDInsight](hdinsight-component-versioning.md)。 建立 hello 一般叢集中的資訊，請參閱[在 HDInsight 中的建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

### <a name="access-control-requirements"></a>存取控制需求

當您建立 HDInsight 叢集時，必須指定 Azure 訂用帳戶。 這個叢集可在新的 Azure 資源群組中建立，或是在現有的資源群組中建立。 您可以使用下列步驟 tooverify hello 您的權限，來建立 HDInsight 叢集：

- toouse 現有的資源群組。

    1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
    2. 按一下**資源群組**從 hello 左側的功能表 toolist hello 資源群組。
    3. 按一下您要建立您的 HDInsight 叢集的 toouse hello 資源群組。
    4. 按一下**存取控制 (IAM)**，並確認您 （或您所屬的群組） 有至少 hello 參與者存取 toohello 資源群組。

- toocreate 新的資源群組

    1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
    2. 按一下**訂用帳戶**hello 左側功能表中。 它有黃色的鑰匙圖示。 您應該會看到訂用帳戶清單。
    3. 按一下您將 toocreate 叢集 hello 訂用帳戶。 
    4. 按一下 [我的權限]。  它會顯示您[角色](../active-directory/role-based-access-control-what-is.md#built-in-roles)hello 訂用帳戶。 您必須至少參與者存取 toocreate HDInsight 叢集。

如果您收到 hello NoRegisteredProviderFound 錯誤或 hello MissingSubscriptionRegistration 錯誤，請參閱[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](../azure-resource-manager/resource-manager-common-deployment-errors.md)。

## <a name="list-and-show-clusters"></a>列出和顯示叢集
1. 登入太[https://portal.azure.com](https://portal.azure.com)。
2. 按一下**HDInsight 叢集**hello 從左側的功能表 toolist hello 現有的叢集。
3. 按一下 hello 叢集名稱。 如果 hello 叢集清單很長，您可以使用篩選器上 hello hello 頁面的頂端。
4. 按一下從 hello 清單 toosee hello 概觀頁面上的叢集：

    ![Azure portal HDInsight cluster essentials](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * **儀表板**： 開啟 hello 叢集儀表板，也就是 Ambari Web 用於以 Linux 為基礎的叢集。
    * **安全殼層**： 顯示 hello 指示 tooconnect toohello 叢集使用安全殼層 (SSH) 連線。
    * **調整叢集**： 可讓您對此叢集的背景工作節點 toochange hello 數。
    * **刪除**： 刪除 hello 叢集。
    * **活動記錄檔**︰顯示和查詢活動記錄檔。
    * **存取控制 (IAM)**︰使用角色指派。  請參閱[使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](../active-directory/role-based-access-control-configure.md)。
    * **標記**： 可讓您 tooset 索引鍵/值組 toodefine 自訂您的雲端服務的分類。 例如，您可建立名為 **project**的索引鍵，然後使用與特定專案相關聯之所有服務的通用值。
    * **診斷並解決問題**︰顯示疑難排解資訊。
    * **鎖定**： 新增鎖定 tooprevent hello 叢集正在修改或刪除。
    * **自動化指令碼**: hello 叢集的顯示和匯出 hello Azure Resource Manager 範本。 目前，您可以只匯出 hello 相依的 Azure 儲存體帳戶。 請參閱[使用 Azure Resource Manager 範本在 HDInsight 中建立 Linux 型 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)。
    * **快速啟動**：顯示可協助您開始使用 HDInsight 的資訊。
    * **適用於 HDInsight 的工具**：HDInsight 相關工具的說明資訊。
    * **叢集登入**： 顯示 hello 叢集登入資訊。
    * **訂用帳戶核心使用量**： 顯示 hello 訂用帳戶的使用和可用的核心。
    * **調整叢集**： 增減 hello 叢集背景工作節點數。 請參閱[調整叢集](hdinsight-administer-use-management-portal.md#scale-clusters)。
    * **安全殼層**： 顯示 hello 指示 tooconnect toohello 叢集使用安全殼層 (SSH) 連線。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。
    * **HDInsight 合作夥伴**： 新增/移除 hello 目前的 HDInsight 合作夥伴。
    * **外部中繼存放區**： 檢視 hello Hive 和 Oozie 中繼存放區。 只能在 hello 叢集建立程序期間設定 hello 中繼存放區。 請參閱[使用 Hive/Oozie 中繼存放區](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore)。
    * **編寫指令碼動作**： 執行撞 hello 叢集上的指令碼。 請參閱 [使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。
    * **應用程式**：新增/移除 HDInsight 應用程式。  請參閱[安裝自訂 HDInsight 應用程式](hdinsight-apps-install-custom-applications.md)。
    * **屬性**： 檢視 hello 叢集內容。
    * **儲存體帳戶**： 檢視 hello 儲存體帳戶和 hello 機碼。 hello 叢集建立程序期間，會設定 hello 儲存體帳戶。
    * **叢集 AAD 身分識別**：
    * **新的支援要求**： 可讓您 toocreate 支援票證，向 Microsoft 支援。
    
6. 按一下 [屬性] ：

    hello 屬性如下：

   * **主機名稱**：叢集名稱。
   * **叢集 URL**。 hello hello Ambari web 介面的 URL。
   * **狀態**：包括Aborted、Accepted、ClusterStorageProvisioned、AzureVMConfiguration、HDInsightConfiguration、Operational、Running、Error、Deleting、Deleted、Timedout、DeleteQueued、DeleteTimedout、DeleteError、PatchQueued、CertRolloverQueued、ResizeQueued、ClusterCustomization
   * **區域**：Azure 位置。 如需支援的 Azure 位置的清單，請參閱 hello**區域**下拉式清單方塊上的[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。
   * **建立日期**。
   * **作業系統**：**Windows** 或 **Linux**。
   * **類型**：Hadoop、HBase、Storm、Spark。
   * **版本**。 請參閱 [HDInsight 版本](hdinsight-component-versioning.md)
   * **訂用帳戶**︰訂用帳戶名稱。
   * **預設的資料來源**: hello 預設叢集檔案系統。
   * **背景工作節點**。
   * **前端節點大小**。

## <a name="delete-clusters"></a>刪除叢集
正在刪除叢集不會刪除 hello 預設儲存體帳戶或任何連結儲存體帳戶。 您可以使用，以重新建立 hello 叢集 hello 相同的儲存體帳戶和 hello 相同中繼存放區。 它是您重新建立 hello 叢集的使用者 toouse 建議新的預設 Blob 容器。

1. 登入 toohello[入口網站][azure-portal]。
2. 按一下**HDInsight 叢集**hello 左側功能表中。 如果您沒有看到 [HDInsight 叢集]，可先按一下 [更多服務]。
3. 按一下您想 toodelete hello 叢集。
4. 按一下**刪除**從 hello 上方功能表中，然後再遵循 hello 的指示。

另請參閱 [暫停/關閉叢集](#pauseshut-down-clusters)。

## <a name="add-additional-storage-accounts"></a>新增其他儲存體帳戶

建立叢集之後，您可以新增其他 Azure 儲存體帳戶和 Azure Data Lake Store 帳戶。 如需詳細資訊，請參閱[新增額外的儲存體帳戶 tooHDInsight](./hdinsight-hadoop-add-storage.md)。

## <a name="scale-clusters"></a>調整叢集
hello 叢集擴充功能可讓您在 Azure HDInsight 中執行而不需要 toore 叢集所用的背景工作節點 toochange hello 數-建立 hello 叢集。

> [!NOTE]
> 只支援使用 HDInsight 3.1.3 版或更高版本的叢集。 如果您不確定您的叢集 hello 版本，您可以檢查 hello 屬性頁面。  請參閱[列出和顯示叢集](#list-and-show-clusters)。
>
>

hello 變更造成的影響 hello 支援 HDInsight 叢集的每種類型的資料節點數目：

* Hadoop

    您可以順暢地增加 hello Hadoop 叢集中執行而不會影響任何暫止或執行工作的背景工作節點數。 Hello 作業正在進行時，也可以提交新的作業。 使 hello 叢集一律會保持在運作狀態，是依正常程序處理中縮放作業失敗。

    當在 Hadoop 叢集縮小藉由減少 hello 資料節點數時，部分 hello hello 叢集中的服務會重新啟動。 所有執行和暫止的工作 toofail hello hello 調整大小作業完成時，會導致此行為。 您可以不過，再重新送出 hello 工作一旦 hello 作業已完成。
* HBase

    順暢地，您可以新增或移除節點 tooyour HBase 叢集正在執行時。 完成 hello 調整大小作業的幾分鐘內自動平衡地區的伺服器。 不過，您就可以手動平衡 hello 地區的伺服器登入以 toohello 叢集前端節點的叢集和執行 hello 的命令提示字元視窗中的下列命令：

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    如需有關使用 hello HBase 殼層的詳細資訊，請參閱]
* Storm

    順暢地，您可以新增或移除在執行時的資料節點 tooyour Storm 叢集。 但是 hello 調整大小作業順利完成之後, 您將需要 toorebalance hello 拓撲。

    您可以使用兩種方式來完成重新平衡作業：

  * Storm Web UI
  * 命令列介面 (CLI) 工具

    請參閱 toohello [Apache Storm 文件](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)如需詳細資訊。

    hello Storm web UI 是在 hello HDInsight 叢集上使用：

    ![HDInsight Storm 調整重新平衡](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    以下是範例如何 toouse hello CLI 命令 toorebalance hello Storm 拓撲：

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**tooscale 叢集**

1. 登入 toohello[入口網站][azure-portal]。
2. 按一下**HDInsight 叢集**hello 左側功能表中。
3. 按一下您想要 tooscale hello 叢集。
3. 按一下 [調整叢集]。
4. 輸入 **背景工作節點的數目**。 hello hello 叢集節點數目限制會因 Azure 訂用帳戶而異。 您可以連絡帳務支援 tooincrease hello 限制。  hello 成本資訊會反映您所做的節點 toohello 數目的 hello 變更。

    ![HDInsight hadoop hbase storm spark scale](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a>暫停/關閉叢集

大部分 Hadoop 工作是只會偶爾執行的批次工作。 對於大多數的 Hadoop 叢集有長時間的過 hello 叢集不正進行處理。 利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。
您也需支付 HDInsight 叢集的費用 (即使未使用)。 由於 hello 叢集 hello 費用的次數超過儲存體的 hello 費用，經濟效益 toodelete 叢集時未使用。

有許多方法，您可以程式設計 hello 程序：

* 使用 Azure Data Factory。 如需建立隨選 HDInsight 連結服務，請參閱 [使用 Azure Data Factory 在 HDInsight 中建立 Linux 型隨選 Handooop 叢集](hdinsight-hadoop-create-linux-clusters-adf.md) 。
* 使用 Azure PowerShell。  請參閱 [分析航班延誤資料](hdinsight-analyze-flight-delay-data.md)。
* 使用 Azure CLI。 請參閱 [使用 Azure CLI 管理 HDInsight 叢集](hdinsight-administer-use-command-line.md)。
* 使用 HDInsight .NET SDK。 請參閱 [提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)。

Hello 定價資訊，請參閱[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。 請參閱 toodelete hello 入口網站中，從叢集[刪除叢集](#delete-clusters)


## <a name="upgrade-clusters"></a>升級叢集

請參閱[升級 HDInsight 叢集 tooa 較新版本](./hdinsight-upgrade-cluster.md)。

## <a name="change-passwords"></a>變更密碼
HDInsight 叢集可以有兩個使用者帳戶。 （也稱為 hello HDInsight 叢集的使用者帳戶 HTTP 使用者帳戶） 以及 hello 建立程序期間建立 hello SSH 使用者帳戶。 您可以使用 hello Ambari web UI toochange hello 叢集使用者的帳戶使用者名稱和密碼，以及指令碼動作 toochange hello SSH 使用者帳戶

### <a name="change-hello-cluster-user-password"></a>變更 hello 叢集使用者密碼
您可以使用 hello Ambari Web UI toochange hello 叢集使用者密碼。 toolog tooAmbari 中的，您必須使用 hello 現有叢集使用者名稱和密碼。

> [!NOTE]
> 變更 hello 叢集使用者 (admin) 密碼可能會導致動作執行針對這個叢集 toofail 指令碼。 如果您有任何目標背景工作角色節點的保存的指令碼動作，這些指令碼可能會失敗，當您新增節點 toohello 叢集透過調整大小作業。 如需指令碼動作的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。
>
>

1. 登入 toohello Ambari Web UI 使用 hello HDInsight 叢集的使用者認證。 hello 預設使用者名稱是**admin**。 URL 是的 hello **https://&lt;HDInsight 叢集名稱 >.azurehdinsight.net**。
2. 按一下**Admin**從 hello 上方的功能表，然後按一下 「 管理 Ambari"。
3. 從 hello 左窗格中，按一下 **使用者**。
4. 按一下 Admin 。
5. 按一下 [變更密碼] 。

Ambari 然後變更 hello hello 叢集中所有節點上的密碼。

### <a name="change-hello-ssh-user-password"></a>變更 hello SSH 使用者密碼
1. 使用文字編輯器中，儲存為檔案命名為下列文字的 hello **changepassword.sh**。

   > [!IMPORTANT]
   > 您必須使用 LF 做 hello 行尾結束符號的編輯器。 如果 hello 編輯器使用 CRLF，然後 hello 指令碼無法運作。
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. 上傳 hello 檔案 tooa 存取儲存體位置可以是從 HDInsight 使用 HTTP 或 HTTPS 位址。 例如，OneDrive 或 Azure Blob 儲存體這類的公用檔案存放區。 儲存 hello URI （HTTP 或 HTTPS 位址） toohello 檔案，因為 hello 下一個步驟中需要此 URI。
3. 從 hello Azure 入口網站，按一下  **HDInsight 叢集**。
4. 按一下您的 HDInsight 叢集。
4. 按一下 [指令碼動作]。
4. 從 hello**指令碼動作**刀鋒視窗中，選取**提交新**。 當 hello**送出指令碼動作**刀鋒視窗中出現，請輸入下列資訊的 hello:

   | 欄位 | 值 |
   | --- | --- |
   | Name |變更 SSH 密碼 |
   | Bash 指令碼 URI |hello URI toohello changepassword.sh 檔案 |
   | 節點 (前端、背景工作、Nimbus、監督員、Zookeeper 等) |✓ 針對列出的所有節點類型 |
   | 參數 |輸入 hello SSH 使用者名稱，然後 hello 新密碼。 應該要有一個 hello 使用者名稱和密碼 hello 之間的空格。 |
   | 保存這個指令碼動作... |不選取此欄位。 |
5. 選取**建立**tooapply hello 指令碼。 一旦 hello 指令碼完成時，您就可以 tooconnect toohello 叢集使用 SSH 使用 hello 新密碼。

## <a name="grantrevoke-access"></a>授與/撤銷存取權
HDInsight 叢集都有下列 （所有這些服務有 RESTful 端點） 的 HTTP web 服務的 hello:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

預設會授與這些服務的存取權。 您可以撤銷/授與存取權來使用 hello [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster)和[Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access)。

## <a name="find-hello-subscription-id"></a>尋找 hello 訂用帳戶 ID

**toofind 您 Azure 訂用帳戶 Id**

1. 登入 toohello[入口網站][azure-portal]。
2. 按一下 [訂用帳戶]。 每個訂用帳戶都有一個名稱和一個識別碼。

每個叢集是繫結的 tooan Azure 訂用帳戶。 hello 訂用帳戶 ID 會顯示 hello 叢集**基本**磚。 請參閱[列出和顯示叢集](#list-and-show-clusters)。

## <a name="find-hello-resource-group"></a>找不到 hello 資源群組
在 hello Azure Resource Manager 模式中，每個 HDInsight 叢集建立 Azure 資源管理員群組。 叢集所屬 tooappears 中的 hello 資源管理員群組：

* hello 叢集清單有**資源群組**資料行。
* 叢集 [基本資料]  磚。  

請參閱[列出和顯示叢集](#list-and-show-clusters)。

## <a name="find-hello-default-storage-account"></a>找不到 hello 預設儲存體帳戶
每個 HDInsight 叢集都有預設的儲存體帳戶。 叢集會顯示在 hello 預設儲存體帳戶，而且其索引鍵**儲存體帳戶**。 請參閱[列出和顯示叢集](#list-and-show-clusters)。

## <a name="run-hive-queries"></a>執行 Hive 查詢
您無法直接從 hello Azure 入口網站執行 Hive 工作，但是您可以使用 hello Ambari Web UI 上的登錄區的檢視。

**使用 Ambari Hive 檢視 toorun Hive 查詢**

1. 登入 toohello Ambari Web UI 使用 hello HDInsight 叢集的使用者認證。 hello 預設使用者名稱是**admin**。 URL 是的 hello **https://&lt;HDInsight 叢集名稱 >.azurehdinsight.net**。
2. 開啟登錄區的檢視，hello 下列螢幕擷取畫面所示：  

    ![HDInsight Hive 檢視](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. 按一下**查詢**從 hello 上方的功能表。
4. 在 查詢編輯器 中輸入 Hive 查詢，然後按一下執行。

## <a name="monitor-jobs"></a>監視工作
請參閱[管理 HDInsight 叢集使用 hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md#monitoring)。

## <a name="browse-files"></a>瀏覽檔案
使用 hello Azure 入口網站，您可以瀏覽 hello 的 hello 預設容器的內容。

1. 登入太[https://portal.azure.com](https://portal.azure.com)。
2. 按一下**HDInsight 叢集**hello 從左側的功能表 toolist hello 現有的叢集。
3. 按一下 hello 叢集名稱。 如果 hello 叢集清單很長，您可以使用篩選器上 hello hello 頁面的頂端。
4. 按一下**儲存體帳戶**hello 叢集左側功能表中。
5. 按一下 [儲存體帳戶]。
7. 按一下 hello **Blob**磚。
8. 按一下 hello 預設容器名稱。

## <a name="monitor-cluster-usage"></a>監視叢集使用量
hello**使用量**hello HDInsight 叢集刀鋒視窗的區段會顯示 hello 核心可用 tooyour HDInsight，搭配使用的訂用帳戶數目，以及 hello toothis 叢集以及其同時配置的核心數目的相關資訊配置給 hello 此叢集中的節點。 請參閱[列出和顯示叢集](#list-and-show-clusters)。

> [!IMPORTANT]
> toomonitor hello 服務提供 hello HDInsight 叢集，您必須使用 Ambari Web 或 hello Ambari REST API。 如需使用 Ambari 的詳細資訊，請參閱 [使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="connect-tooa-cluster"></a>Tooa 叢集連線

* [搭配 HDInsight 使用 Hivet](hdinsight-hadoop-use-hive-ambari-view.md)
* [搭配使用 SSH 與 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a>後續步驟
在本文中，您已了解一些基本的系統管理函式。 toolearn 詳細資訊，請參閱下列文章 hello:

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

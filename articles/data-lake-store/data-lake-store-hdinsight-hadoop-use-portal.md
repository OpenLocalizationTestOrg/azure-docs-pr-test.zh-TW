---
title: "aaaUse hello Azure 入口網站 toocreate Azure HDInsight 叢集與資料湖存放區 |Microsoft 文件"
description: "使用 Azure 入口網站 toocreate hello 和使用 Azure Data Lake Store 的 HDInsight 叢集"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a>使用 Data Lake Store 的 HDInsight 叢集建立使用 hello Azure 入口網站
> [!div class="op_single_selector"]
> * [使用 hello Azure 入口網站](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [使用 PowerShell (針對預設儲存體)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [使用 PowerShell (針對額外儲存體)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [使用 Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

了解如何 toouse hello Azure 入口網站 toocreate HDInsight 叢集的 Azure Data Lake Store 帳戶做為 hello 預設儲存體或額外的存放裝置。 即使額外的儲存體是選擇性的 HDInsight 叢集，則建議 toostore hello 額外的儲存體帳戶中商務資料。

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，請確定您符合下列需求的 hello:

* **Azure 訂用帳戶**。 跳過[取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure Data Lake Store 帳戶**。 請依照下列指示 hello[使用 hello Azure 入口網站開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)。 您也必須建立根資料夾上 hello 帳戶。  在本教學課程中，會使用名為 __/clusters__ 的根資料夾。
* **Azure Active Directory 服務主體**。 本教學課程提供如何指示 toocreate Azure Active Directory (Azure AD) 中的服務主體。 不過，toocreate 服務主體，您必須是 Azure AD 系統管理員。 如果您是系統管理員，則可以略過這項必要條件，並繼續進行 hello 教學課程。

    >[!NOTE]
    >唯有您是 Azure AD 系統管理員，才可以建立服務主體。 您的 Azure AD 系統管理員必須先建立服務主體，您才能建立搭配 Data Lake Store 的 HDInsight 叢集。 此外，hello 服務主體必須以建立憑證時，依照[建立服務主體與憑證](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate)。
    >

## <a name="create-an-hdinsight-cluster"></a>建立 HDInsight 叢集

本節中，您可以建立 HDInsight 叢集與 hello 預設值為 hello 額外的存放裝置的 Data Lake Store 帳戶。 本文只著重 hello 一部分設定 Data Lake Store 帳戶。  Hello 一般叢集建立資訊和程序，請參閱[在 HDInsight 中的建立 Hadoop 叢集](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)。

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a>建立以 Data Lake Store 做為預設儲存體的叢集

**Data Lake Store toocreate HDInsight 叢集與 hello 預設儲存體帳戶**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 請遵循[建立叢集](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters)的 hello 建立 HDInsight 叢集的一般資訊。
3. 在 hello**儲存體**刀鋒視窗下**主要儲存體類型**，選取**Data Lake Store**，然後輸入下列資訊的 hello:

    ![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "新增服務主體 tooHDInsight 叢集")

    - **選取 Data Lake Store 帳戶**： 選取現有的 Data Lake Store 帳戶。 需要現有的 Data Lake Store 帳戶。  請參閱[必要條件](#prereuisites)。
    - **根路徑**： 輸入 hello 叢集特定檔案的 toobe 儲存的位置路徑。 在 hello 螢幕擷取畫面，這是__/叢集/myhdiadlcluster/__中的 hello __/叢集__資料夾必須存在，且 hello 入口網站建立*myhdicluster*資料夾。  hello *myhdicluster* hello 叢集名稱。
    - **資料湖存放區存取**: hello Data Lake Store 帳戶與 HDInsight 叢集之間的存取設定。 如需指示，請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。
    - **其他儲存體帳戶**: hello 叢集新增 Azure 儲存體帳戶做為額外的儲存體帳戶。 tooadd 額外資料湖存放區是由 Data Lake Store 帳戶設定為 hello 主要儲存體類型時，給予更多的 Data Lake Store 帳戶中的資料上的 hello 叢集權限。 請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。

4. 在 hello**資料湖存放區存取**，按一下 **選取**中, 所述，然後繼續建立叢集與[建立 Hadoop 叢集 HDInsight 中](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md)。


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a>建立以 Data Lake Store 做為額外儲存體的叢集

hello 下列指示建立 HDInsight 叢集的 Azure 儲存體帳戶為 hello 預設儲存體，與做為額外的存放裝置的 Data Lake Store 帳戶。
**Data Lake Store toocreate HDInsight 叢集與 hello 預設儲存體帳戶**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 請遵循[建立叢集](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters)的 hello 建立 HDInsight 叢集的一般資訊。
3. 在 hello**儲存體**刀鋒視窗底下**主要儲存體類型**，選取**Azure 儲存體**，然後輸入下列資訊的 hello:

    ![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "新增服務主體 tooHDInsight 叢集")

    - **選取方法**： 使用其中一種 hello 下列選項：

        * toospecify 屬於您 Azure 訂用帳戶的儲存體帳戶選取**我的訂閱**，然後選取 hello 儲存體帳戶。
        * toospecify 超出您的 Azure 訂閱，選取儲存體帳戶**便捷鍵**，然後提供 hello hello 外部儲存體帳戶的資訊。

    - **預設容器**： 使用任一個 hello 預設值或指定您自己的名稱。

    - 其他儲存體帳戶： 將多個 Azure 儲存體帳戶新增為 hello 額外的存放裝置。
    - 資料湖存放區存取： hello Data Lake Store 帳戶與 HDInsight 叢集之間的存取設定。 如需指示，請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。

## <a name="configure-data-lake-store-access"></a>設定 Data Lake Store 存取 

在本節中，您將會使用 Azure Active Directory 服務主體設定 Data Lake Store 與 HDInsight 叢集之間的存取。 

### <a name="specify-a-service-principal"></a>指定服務主體

從 hello Azure 入口網站，您可以使用現有的服務主體或另外新建一個。

**toocreate hello Azure 入口網站的服務主體**

1. 按一下**資料湖存放區存取**的 hello 存放區 刀鋒視窗。
2. 在 hello**資料湖存放區存取**刀鋒視窗中，按一下 **建立新**。
3. 按一下**服務主體**，然後依照 hello 指示 toocreate 服務主體。
4. 如果您決定 toouse 下載 hello 憑證一次在未來的 hello。 這是很有用，如果您想 toouse hello 相同服務主體時建立額外的 HDInsight 叢集下載 hello 憑證。

    ![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "新增服務主體 tooHDInsight 叢集")

4. 按一下**存取**tooconfigure hello 資料夾存取。  請參閱[設定檔案權限](#configure-file-permissions)。


**toouse 現有服務主體從 hello Azure 入口網站**

1. 按一下 [Data Lake Store 存取]。
1. 在 hello**資料湖存放區存取**刀鋒視窗中，按一下 **使用現有**。
2. 按一下 [服務主體]，然後選取一個服務主體。 
3. 上傳您的選取的服務主體相關聯的 hello 憑證 （.pfx 檔案），然後輸入 hello 憑證的密碼。

    ![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "新增服務主體 tooHDInsight 叢集")

4. 按一下**存取**tooconfigure hello 資料夾存取。  請參閱[設定檔案權限](#configure-file-permissions)。


### <a name="configure-file-permissions"></a>設定檔案權限

hello 設定會根據是否 hello 帳戶會當做 hello 預設儲存體或其他儲存體帳戶而不同：

- 作為預設儲存體

    - 在根層級 hello hello Data Lake Store 帳戶的權限
    - hello HDInsight 叢集存放裝置 hello 根層級的權限。 例如，hello __/叢集__hello 教學課程中先前使用的資料夾。
- 作為其他儲存體

    - 在您需要在此檔案存取的 hello 資料夾的權限。

**在 hello Data Lake Store 帳戶的根層級的 tooassign 權限**

1. 在 hello**資料湖存放區存取**刀鋒視窗中，按一下 **存取**。 hello**選取檔案的權限**開啟刀鋒視窗。 它會列出您的訂用帳戶中的所有 hello Data Lake Store 帳戶。
2. 將滑鼠停留 （請勿按一下） hello 的結束滑鼠停留 hello hello toomake hello 可見，核取方塊，然後選取 hello 核取方塊的 Data Lake Store 帳戶名稱。

    ![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "新增服務主體 tooHDInsight 叢集")

  根據預設，__READ__、__WRITE__ 和 __EXECUTE__ 會全部選取。

3. 按一下**選取**上 hello hello 頁面的底部。
4. 按一下**執行**tooassign 權限。
5. 按一下 [完成] 。

**在 hello HDInsight 叢集根層級的 tooassign 權限**

1. 在 hello**資料湖存放區存取**刀鋒視窗中，按一下 **存取**。 hello**選取檔案的權限**開啟刀鋒視窗。 它會列出您的訂用帳戶中的所有 hello Data Lake Store 帳戶。
1. 從 hello**選取檔案的權限**刀鋒視窗中，按一下 hello 資料湖存放區名稱 tooshow 其內容。
2. 選取左側的 hello 資料夾 hello hello 核取方塊來選取 hello HDInsight 叢集儲存區根目錄。 稍早根據 toohello 螢幕擷取畫面，hello 叢集儲存區根目錄是__/叢集__您選取為預設的存放裝置 hello 資料湖存放區時所指定的資料夾。
3. Hello 資料夾上設定 hello 權限。  根據預設，讀取、寫入和執行會全部選取。
4. 按一下**選取**上 hello hello 頁面的底部。
5. 按一下 **[執行]**。
6. 按一下 [完成] 。

如果您使用 Data Lake Store 作為額外的存放裝置，您必須指派只能用於 hello 資料夾的權限的 tooaccess 從 hello HDInsight 叢集。 例如，在 hello 以下螢幕擷取畫面，您提供存取只太**hdiaddonstorage** Data Lake Store 帳戶中的資料夾。

![指派服務主體的權限 toohello HDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "指派服務主體的權限 toohello HDInsight 叢集")


## <a name="verify-cluster-set-up"></a>確認叢集設定

Hello 叢集安裝程式完成之後，在 hello 叢集刀鋒視窗中，確認您的結果執行一個或兩個步驟的 hello:

* hello hello 叢集為您指定的 hello Data Lake Store 帳戶的相關聯的儲存體，請按一下 tooverify**儲存體帳戶**hello 左窗格中。

    ![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "新增服務主體 tooHDInsight 叢集")

* hello 服務主體的 tooverify 是正確與 hello HDInsight 叢集相關聯，請按一下**資料湖存放區存取**hello 左窗格中。

    ![新增服務主體 tooHDInsight 叢集](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "新增服務主體 tooHDInsight 叢集")


## <a name="examples"></a>範例

您已將設定 Data Lake Store 的 hello 叢集為您的儲存體之後，請參閱 toothese 範例 toouse HDInsight 叢集 tooanalyze hello 資料儲存在資料湖存放區中的方式。

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a>針對 Data Lake Store (做為主要儲存體) 中的資料執行 Hive 查詢

toorun Hive 查詢，使用 hello Ambari 入口網站中的 hello Hive 檢視介面。 如需有關如何檢視 toouse Ambari Hive 的指示，請參閱[使用 hello HDInsight 中的 Hadoop hive 控制檔的檢視](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md)。

當您使用資料湖存放區中的資料時，有幾個字串 toochange。

如果您使用，例如，資料湖存放區做為主要儲存體，以建立 hello 叢集 hello 路徑 toohello 資料是： *adl: / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*。 Hive 查詢 toocreate 會儲存在 hello Data Lake Store 帳戶的範例資料中的資料表看起來像 hello 後面的陳述式中：

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

說明：
* `adl://hdiadlstorage.azuredatalakestore.net/`是 hello 根 hello Data Lake Store 帳戶。
* `/clusters/myhdiadlcluster`是 hello 根 hello 建立 hello 叢集時，您指定的叢集資料。
* `/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`是您在 hello 查詢中使用的 hello 範例檔案的 hello 位置。

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a>針對 Data Lake Store (做為額外儲存體) 中的資料執行 Hive 查詢

如果您建立的 hello 叢集做為預設儲存體使用 Blob 儲存體，hello 範例資料不會包含在 hello Azure Data Lake Store 帳戶做為額外的存放裝置。 在這種情況下，第一次傳送 hello 資料從 Blob 儲存體 toohello 資料湖存放區，然後再執行 hello 查詢 hello 前面範例所示。

上如何 toocopy 從 Blob 儲存體 tooa 資料湖存放區資料的資訊，請參閱下列文章 hello:

* [使用 Azure 儲存體 blob 與資料湖存放區之間 Distcp toocopy 資料](data-lake-store-copy-data-wasb-distcp.md)
* [使用 AdlCopy toocopy 資料從 Azure 儲存體 blob tooData 湖存放區](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a>使用 Data Lake Store 搭配 Spark 叢集
您可以使用 Spark 叢集 toorun Spark 作業上儲存資料湖存放區中的資料。 如需詳細資訊，請參閱[資料湖存放區中的使用 HDInsight Spark 叢集 tooanalyze 資料](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md)。


### <a name="use-data-lake-store-in-a-storm-topology"></a>在 Storm 拓撲中使用 Data Lake Store
您可以使用 Storm 拓撲 hello Data Lake Store toowrite 資料。 如需有關指示 tooachieve 此案例中，請參閱[與 HDInsight Apache Storm 與使用 Azure Data Lake Store](../hdinsight/hdinsight-storm-write-data-lake-store.md)。

## <a name="see-also"></a>另請參閱
* [PowerShell： 建立 HDInsight 叢集 toouse 資料湖存放區](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx

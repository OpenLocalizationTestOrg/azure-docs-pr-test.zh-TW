---
title: "使用 linux 的 HDInsight 的 Azure 上的 Hadoop aaaTips |Microsoft 文件"
description: "取得實作的提示熟悉 hello Azure 雲端中執行的 Linux 環境上使用 linux 的 HDInsight (Hadoop) 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: a555622605079c9beae88ece872042e36d540c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a>在 Linux 上使用 HDInsight 的相關資訊

Azure HDInsight 叢集提供熟悉的 Linux 環境，在 hello Azure 雲端中執行的 Hadoop。 其操作大多與 Linux 安裝上的任何其他 Hadoop 相同。 本文件會指出其中應注意的特殊不同之處。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="prerequisites"></a>必要條件

許多 hello 本文件中的步驟會使用下列公用程式，可能需要安裝在您的系統上的 toobe hello。

* [cURL](https://curl.haxx.se/) -toocommunicate 搭配 web 服務
* [jq](https://stedolan.github.io/jq/) -使用 tooparse JSON 文件
* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (preview)-使用的 tooremotely 管理 Azure 服務

## <a name="users"></a>使用者

除非[已加入網域](hdinsight-domain-joined-introduction.md)，否則應將 HDInsight 視為**單一使用者**系統。 單一的 SSH 使用者帳戶會建立與 hello 叢集，以系統管理員層級權限。 您可以建立額外的 SSH 帳戶，但還具有系統管理員存取 toohello 叢集。

已加入網域的 HDInsight 可支援多個使用者和更細微的權限和角色設定。 如需詳細資訊，請參閱[管理已加入網域的 HDInsight 叢集](hdinsight-domain-joined-manage.md)。

## <a name="domain-names"></a>網域名稱

hello 完整網域名稱 (FQDN) toouse hello 網際網路是從連接 toohello 叢集時 **&lt;clustername >。.azurehdinsight.net**或 （適用於僅 SSH)  **&lt;clustername-ssh>。.azurehdinsight.net**。

就內部而言，hello 叢集中的每個節點都在叢集組態期間指派的名稱。 toofind hello 叢集名稱，請參閱 hello**主機**hello Ambari Web UI 上的頁面。 您也可以使用下列 tooreturn 從 hello Ambari REST API 主機清單的 hello:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

取代**密碼**與 hello hello 系統管理員，帳戶的密碼和**CLUSTERNAME**與 hello 叢集的名稱。 此命令會傳回 JSON 文件包含一份 hello hello 叢集中的主機。 Jq 為使用的 tooextract hello`host_name`每個主控件的項目值。

如果您需要 toofind hello hello 節點名稱為特定服務時，您可以查詢 Ambari 該元件。 比方說，toofind hello 主控件 hello HDFS 名稱節點，使用下列命令的 hello:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

此命令會傳回描述 hello 服務的 JSON 文件和 jq 然後提取出只 hello `host_name` hello 主機的值。

## <a name="remote-access-tooservices"></a>遠端存取 tooservices

* **Ambari (web)** - https://&lt;clustername>.azurehdinsight.net

    驗證使用 hello 叢集系統管理員使用者和密碼，並再登入 tooAmbari。

    驗證是純文字-一律使用 HTTPS toohelp 確保 hello 連線的安全。

    > [!IMPORTANT]
    > 一些 hello web Ui 可透過 Ambari 存取使用的內部網域名稱的節點。 內部網域名稱不是透過可公開存取 hello 網際網路。 嘗試 tooaccess hello 網際網路上的某些功能時，您可能會收到 「 找不到伺服器 」 錯誤。
    >
    > toouse hello 完整功能 hello Ambari web UI，使用 SSH 通道 tooproxy web 流量 toohello 叢集前端節點。 請參閱[使用 SSH 通道 tooaccess Ambari web UI、 ResourceManager、 JobHistory、 NameNode、 Oozie、 以及其他 web Ui](hdinsight-linux-ambari-ssh-tunnel.md)

* **Ambari (REST)** - https://&lt;clustername>.azurehdinsight.net/ambari

    > [!NOTE]
    > 使用 hello 叢集系統管理員使用者名稱和密碼進行驗證。
    >
    > 驗證是純文字-一律使用 HTTPS toohelp 確保 hello 連線的安全。

* **WebHCat (Templeton)** - https://&lt;clustername>.azurehdinsight.net/templeton

    > [!NOTE]
    > 使用 hello 叢集系統管理員使用者名稱和密碼進行驗證。
    >
    > 驗證是純文字-一律使用 HTTPS toohelp 確保 hello 連線的安全。

* **SSH** - 連接埠 22 或 23 上的 &lt;clustername>-ssh.azurehdinsight.net。 連接埠 22。 使用的 tooconnect toohello 主要叢集前端節點，23 時使用的 tooconnect toohello 次要 如需有關 hello 前端節點的詳細資訊，請參閱[HDInsight 中的可用性和可靠性的 Hadoop 叢集](hdinsight-high-availability-linux.md)。

    > [!NOTE]
    > 您只能從用戶端電腦透過 SSH 存取 hello 叢集前端節點。 一旦連接之後，您就可以從前端節點使用 SSH，然後存取 hello 背景工作節點。

## <a name="file-locations"></a>檔案位置

Hadoop 相關的檔案可以在 hello 叢集節點上找到`/usr/hdp`。 此目錄包含下列子目錄的 hello:

* **2.2.4.9-1**: hello 目錄名稱是 hello hello Hortonworks Data Platform 使用 HDInsight 版本。 在叢集上的 hello 數目可能不同於此處所列的其中一個 hello。
* **目前**： 此目錄包含 hello 底下的連結 toosubdirectories **2.2.4.9-1**目錄。 此目錄存在，所以您不需要 tooremember hello 版本號碼。

在 Hadoop 分散式檔案系統的 `/example` 和 `/HdiSamples` 可取得範例資料和 JAR 檔案。

## <a name="hdfs-azure-storage-and-data-lake-store"></a>HDFS、Azure 儲存體和 Data Lake Store

在大部分的 Hadoop 散發 HDFS hello hello 叢集中的電腦上本機儲存體所支援。 針對雲端解決方案使用本機儲存體的成本可能相當高，因為計算資源是以每小時或每分鐘為單位來計費。

HDInsight 使用 Azure 儲存體中的 blob 或 Azure Data Lake Store 做 hello 預設存放區。 這些服務會提供下列優點 hello:

* 長期儲存成本低廉
* 可從各種外部服務進行存取，例如網站、檔案上傳/下載公用程式、各種語言的 SDK 和網頁瀏覽器

> [!WARNING]
> HDInsight 僅支援__一般用途__的 Azure 儲存體帳戶。 它目前不支援 hello __Blob 儲存體__帳戶類型。

Azure 儲存體帳戶可以阻擋 too4.75 TB，雖然個別的 blob （或從 HDInsight 觀點來看的檔案） 可以只向上 too195 GB。 Azure 資料湖存放區可以動態地成長檔案，的 toohold trillions 大於 pb 的個別檔案。 如需詳細資訊，請參閱[了解 Blob](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) 和[Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)。

使用 Azure 儲存體或資料湖存放區時，您沒有 toodo 特殊從 HDInsight tooaccess hello 資料的任何項目。 例如，下列命令的 hello 列出限制清單中 hello`/example/data`不論其是否儲存在 Azure 儲存體或資料湖存放區的資料夾：

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a>URI 和配置

有些命令時，可能需要您 toospecify hello 配置 hello URI 的一部分存取檔案。 例如，hello Storm HDFS 元件需要您 toospecify hello 配置。 當使用非預設儲存體 （儲存體新增為 「 其他 」 的儲存體 toohello 叢集），您必須一律使用 hello 配置 hello URI 的一部分。

當使用__Azure 儲存體__，使用其中一種 hello 下列 URI 配置：

* `wasb:///`︰使用未加密通訊存取預設儲存體。

* `wasbs:///`︰使用加密通訊存取預設儲存體。  只能從 HDInsight 3.6 版及更新版本支援 hello wasbs 配置。

* `wasb://<container-name>@<account-name>.blob.core.windows.net/`︰以非預設儲存體帳戶進行通訊時使用。 例如，當您有其他儲存體帳戶，或在可公開存取的儲存體帳戶中存取儲存的資料時。

當使用__Data Lake Store__，使用其中一種 hello 下列 URI 配置：

* `adl:///`： 存取 hello 預設 Data Lake Store hello 叢集。

* `adl://<storage-name>.azuredatalakestore.net/`：用來與非預設 Data Lake Store 進行通訊。 也可以用您的 HDInsight 叢集的 hello 根目錄之外的 tooaccess 資料。

> [!IMPORTANT]
> 當使用資料湖存放區做為 hello HDInsight 的預設存放區，您必須指定 hello 存放區 toouse 內的路徑為 hello HDInsight 儲存區根目錄。 hello 預設路徑是`/clusters/<cluster-name>/`。
>
> 使用時`/`或`adl:///`tooaccess 資料，您只能存取儲存在 hello 根目錄中的資料 (例如， `/clusters/<cluster-name>/`) 的 hello 叢集。 tooaccess 資料 hello 存放區中的任何位置使用 hello`adl://<storage-name>.azuredatalakestore.net/`格式。

### <a name="what-storage-is-hello-cluster-using"></a>Hello 叢集正在使用何種儲存體

您可以使用 Ambari tooretrieve hello 預設儲存體設定 hello 叢集。 使用 hello 下列命令使用 curl，tooretrieve HDFS 組態資訊，並使用[jq](https://stedolan.github.io/jq/):

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> 這會傳回第一次套用設定 toohello 伺服器 hello (`service_config_version=1`)，其中包含這項資訊。 您可能需要 toolist toofind hello 最新版本的所有組態版本。

此命令會傳回值的類似 toohello，下列 Uri:

* `wasb://<container-name>@<account-name>.blob.core.windows.net`，若使用 Azure 儲存體帳戶。

    hello 帳戶名稱是 hello hello Azure 儲存體帳戶名稱、 hello blob 容器 hello 容器名稱時，會是 hello 根 hello 叢集存放區。

* `adl://home`，若使用 Azure Data Lake Store。 tooget hello 資料湖存放區名稱，使用下列 REST 呼叫的 hello:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    此命令會傳回下列主機名稱的 hello: `<data-lake-store-account-name>.azuredatalakestore.net`。

    是使用下列 REST 呼叫的 hello HDInsight 的 hello 根 hello 存放區內 tooget hello 目錄：

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    此命令會傳回下列路徑的路徑類似的 toohello: `/clusters/<hdinsight-cluster-name>/`。

您也可以找到使用 hello Azure 入口網站使用下列步驟的 hello hello 儲存體資訊：

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 HDInsight 叢集。

2. 從 hello**屬性**區段中，選取**儲存體帳戶**。 會顯示 hello hello 叢集的儲存體資訊。

### <a name="how-do-i-access-files-from-outside-hdinsight"></a>如何從 HDInsight 外部存取檔案

有各種方式從外部 hello HDInsight 叢集 tooaccess 資料。 hello 以下是一些連結 tooutilities 和 Sdk 可與您的資料使用的 toowork:

如果使用__Azure 儲存體__，請參閱下列連結查看的方式，您可以存取資料的 hello:

* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)：適用於 Azure 的命令列介面命令。 安裝之後，使用 hello`az storage`命令說明使用的存放裝置或`az storage blob`blob 特定的命令。
* [blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage)：python 指令碼，用於 Azure 儲存體中的 Blob。
* 各種 SDK：

    * [Java](https://github.com/Azure/azure-sdk-for-java)
    * [Node.js](https://github.com/Azure/azure-sdk-for-node)
    * [PHP](https://github.com/Azure/azure-sdk-for-php)
    * [Python](https://github.com/Azure/azure-sdk-for-python)
    * [Ruby](https://github.com/Azure/azure-sdk-for-ruby)
    * [.NET](https://github.com/Azure/azure-sdk-for-net)
    * [儲存體 REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx)

如果使用__Azure Data Lake Store__，請參閱下列連結查看的方式，您可以存取資料的 hello:

* [Web 瀏覽器](../data-lake-store/data-lake-store-get-started-portal.md)
* [PowerShell](../data-lake-store/data-lake-store-get-started-powershell.md)
* [Azure CLI 2.0](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [WebHDFS REST API](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [Visual Studio 適用的 Data Lake 工具](https://www.microsoft.com/download/details.aspx?id=49504)
* [.NET](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [Java](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [Python](../data-lake-store/data-lake-store-get-started-python.md)

## <a name="scaling"></a>調整您的叢集規模

hello 叢集調整功能可讓您 toodynamically 變更 hello 叢集所用的資料節點數。 正在叢集上執行其他工作或處理序時，您可以執行調整作業。

hello 不同的叢集類型會受到縮放比例，如下所示：

* **Hadoop**： 當規模 hello 叢集中的節點數目，某些 hello 叢集中的 hello 服務會重新啟動。 調整作業可能導致工作執行或暫止 toofail hello hello 調整大小作業完成時。 當 hello 操作完成之後，您可以重新提交 hello 作業。
* **對 HBase**: hello 調整大小作業完成之後的幾分鐘內自動平衡地區的伺服器。 toomanually 平衡地區伺服器，使用下列步驟的 hello:

    1. Toohello HDInsight 叢集使用 SSH 連線。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

    2. 使用下列 toostart hello HBase 殼層 hello:

            hbase shell

    3. Hello HBase 殼層已載入後，使用下列 toomanually 平衡 hello 地區伺服器 hello:

            balancer

* **Storm**︰執行調整作業之後，您應該重新平衡任何執行中的 Storm 拓撲。 重新平衡可讓 hello 新 hello 叢集中的節點數目為基礎的 hello 拓撲 tooreadjust 平行處理原則設定。 toorebalance 執行拓撲中，使用其中一個 hello 下列選項：

    * **SSH**: toohello 伺服器連接，並使用 hello 下列命令 toorebalance 拓撲：

            storm rebalance TOPOLOGYNAME

        您也可以指定參數 toooverride hello 平行處理原則提示原本提供的 hello 拓撲。 例如，`storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10`檔重新設定 hello 拓撲 too5 背景工作處理序、 3 hello 藍色 spout 元件，執行程式和 10 hello 黃色閃電元件執行程式。

    * **Storm UI**： 使用 hello 下列步驟 toorebalance 使用 hello Storm UI 的拓撲。

        1. 開啟**https://CLUSTERNAME.azurehdinsight.net/stormui**網頁瀏覽器，其中 CLUSTERNAME 是 hello Storm 叢集名稱。 如果出現提示，請輸入 hello HDInsight 叢集系統管理員 （管理員） 的名稱和密碼建立 hello 叢集時，您所指定。
        2. 選取您想 toorebalance，然後選擇 hello hello 拓撲**重新平衡** 按鈕。 執行 hello 重新平衡作業之前，請輸入 hello 延遲。

如需有關調整 HDInsight 叢集的特定資訊，請參閱：

* [透過 hello Azure 入口網站來管理 HDInsight 中的 Hadoop 叢集](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [使用 Azure PowerShell 管理 HDInsight 上的 Hadoop 叢集](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a>如何安裝 Hue (或其他 Hadoop 元件)？

HDInsight 是受管理的服務。 如果 Azure 偵測到問題與 hello 叢集時，它可能會刪除 hello 失敗節點，並建立節點 tooreplace 它。 如果您手動 hello 叢集上安裝項目，它們不會保存時就會發生這項作業。 請改用 [HDInsight 指令碼動作](hdinsight-hadoop-customize-cluster.md)。 指令碼動作可以是使用的 toomake hello 下列變更：

* 安裝及設定服務或網站，例如 Spark 或 Hue。
* 安裝和設定需要 hello 叢集中的多個節點上的組態變更的元件。 例如，必要的環境變數、建立記錄目錄或建立組態檔。

指令碼動作是 Bash 指令碼。 hello 指令碼執行期間佈建叢集時，可使用的 tooinstall 及 hello 叢集上設定其他元件。 範例指令碼可供安裝下列元件的 hello:

* [Hue](hdinsight-hadoop-hue-linux.md)
* [Giraph](hdinsight-hadoop-giraph-install-linux.md)
* [Solr](hdinsight-hadoop-solr-install-linux.md)

如需開發您自己的指令碼動作相關資訊，請參閱 [使用 HDInsight 開發指令碼動作](hdinsight-hadoop-script-actions-linux.md)。

### <a name="jar-files"></a>JAR 檔案

獨立的 jar 檔案中提供了一些 Hadoop 技術，其中包含可用來做為 MapReduce 工作一部分的函式，或者來自 Pig 或 Hive 內部的函式。 雖然這些都可以使用安裝指令碼動作，它們通常不需要任何設定和佈建之後可以上傳的 toohello 叢集，直接使用。 如果您想確定 hello 元件 toomake 未重新安裝映像的 hello 叢集，您可以為您的叢集 （WASB 或 ADL） hello jar 檔儲存在 hello 預設儲存體。

例如，如果您想要 toouse hello 最新版本的[DataFu](http://datafu.incubator.apache.org/)，您可以下載的 jar 包含 hello 專案，並將它上傳 toohello HDInsight 叢集。 如何依照 hello DataFu 文件 toouse 從 Pig 或登錄區。

> [!IMPORTANT]
> 獨立 jar 檔案的某些元件所提供的 HDInsight，但是不在 hello 路徑。 如果您要尋找特定元件，您可以使用它的 hello 後續 toosearch 在叢集上：
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> 此命令會傳回 hello 的任何相符的 jar 檔案的路徑。

toouse 不同版本的元件，請上傳 hello 版本，您需要並將它用於您的工作。

> [!WARNING]
> 完全支援隨附 hello HDInsight 叢集的元件，而且 Microsoft 支援服務可協助 tooisolate 並解決問題的相關的 toothese 元件。
>
> 自訂元件會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。 這可能會導致解決 hello 問題，或詢問您 tooengage hello 可用的頻道開啟原始碼技術找到深層的專業知識，針對該項技術。 例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如：[Hadoop](http://hadoop.apache.org/)、[Spark](http://spark.apache.org/)。

## <a name="next-steps"></a>後續步驟

* [從 Windows 為基礎的 HDInsight tooLinux 式移轉](hdinsight-migrate-from-windows-to-linux.md)
* [搭配 HDInsight 使用 Hivet](hdinsight-use-hive.md)
* [搭配 HDInsight 使用 Pig](hdinsight-use-pig.md)
* [搭配 HDInsight 使用 MapReduce 工作](hdinsight-use-mapreduce.md)

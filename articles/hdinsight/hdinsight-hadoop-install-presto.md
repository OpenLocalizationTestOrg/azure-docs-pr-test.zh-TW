---
title: "aaaInstall 照片 on Azure HDInsight Linux 叢集 |Microsoft 文件"
description: "了解如何 tooinstall 照片和 Airpal 上以 Linux 為基礎的 HDInsight Hadoop 叢集使用指令碼動作。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a>在 HDInsight Hadoop 叢集上安裝和使用 Presto

在本主題中，您學會如何 tooinstall 照片上 HDInsight Hadoop 叢集使用指令碼動作。 您也學到如何 tooinstall Airpal 對現有的 Presto HDInsight 叢集。

> [!IMPORTANT]
> hello 本文件中的步驟需要**HDInsight 3.5 Hadoop 叢集**使用 Linux。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [HDInsight 版本](hdinsight-component-versioning.md)。

## <a name="what-is-presto"></a>什麼是 Presto？
[Presto](https://prestodb.io/overview.html) 是巨量資料的快速分散式 SQL 查詢引擎。 Presto 適合數 PB 資料的互動式查詢。 照片和它們如何共同運作的 hello 元件詳細資訊，請參閱[馬上概念](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst)。

> [!WARNING]
> 完全支援隨附 hello HDInsight 叢集的元件，而且 Microsoft 支援服務將會說明 tooisolate 及解決問題的相關的 toothese 元件。
> 
> 自訂元件，例如照片，會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。 這可能會導致解決 hello 問題，或詢問您 tooengage hello 可用的頻道開啟原始碼技術找到深層的專業知識，針對該項技術。 例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。
> 
> 


## <a name="install-presto-using-script-action"></a>使用指令碼動作來安裝 Presto

本節提供如何 toouse hello 範例指令碼時建立新叢集使用 hello Azure 入口網站的指示。 

1. 開始使用中的 hello 步驟佈建叢集[佈建 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)。 請確定您建立使用 hello hello 叢集**自訂**叢集建立流程。 您必須確定您建立該 hello 叢集符合下列需求的 hello。

    a. 必須為隨附 HDInsight 3.5 版的 Hadoop 叢集。

    b. 它必須使用 Azure 儲存體與 hello 資料存放區。 尚未支援使用 Presto 做 hello 儲存選項使用 Azure Data Lake Store 的叢集上。 

    ![使用自訂選項建立 HDInsight 叢集](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. 在 hello**進階設定**刀鋒視窗中，選取**指令碼動作**，並提供下列 hello 資訊：
   
   * **名稱**： 輸入 hello 指令碼動作的易記名稱。
   * **Bash 指令碼 URI**：`https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`
   * **HEAD**：勾選此選項
   * **WORKER**：勾選此選項
   * **ZOOKEEPER**︰清除此核取方塊
   * **參數**：將此欄位保留空白


3. 在 hello 底部 hello**指令碼動作**刀鋒視窗中，按一下 hello**選取**按鈕 toosave hello 組態。 最後，按一下 hello**選取**在 hello hello 底部的按鈕**進階設定**刀鋒視窗 toosave hello 組態資訊。

4. 繼續中所述，佈建 hello 叢集[佈建 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)。

    > [!NOTE]
    > Azure PowerShell、 hello Azure CLI、 hello HDInsight.NET SDK 或 Azure 資源管理員範本也可以使用的 tooapply 指令碼動作。 您也可以套用指令碼動作 tooalready 執行中的叢集。 如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。
    > 
    > 

## <a name="use-presto-with-hdinsight"></a>使用 Presto 搭配 HDInsight

執行之後，您必須安裝它使用 hello 上面所述的步驟，請遵循步驟 toouse 照片 HDInsight 叢集中的 hello。

1. 連線使用 SSH toohello HDInsight 叢集：
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。
     

2. 啟動 hello 馬上 shell 會使用下列命令的 hello。
   
        presto --schema default

3. 在所有 HDInsight 叢集中預設可用的範例資料表 (**hivesampletable**) 上執行查詢。
   
        select count (*) from hivesampletable;
   
    依預設，已設定 Presto 的 [Hive](https://prestodb.io/docs/current/connector/hive.html) 和 [TPCH](https://prestodb.io/docs/current/connector/tpch.html) 連接器。 Hive 連接器是設定的 toouse hello 預設安裝 Hive 安裝，因此登錄區中的所有 hello 資料表都會自動顯示在照片。

    如需 Presto 使用方式的詳細說明，請參閱 [Presto 文件](https://prestodb.io/docs/current/index.html)。

## <a name="use-airpal-with-presto"></a>使用 Airpal 搭配 Presto

[Airpal](https://github.com/airbnb/airpal#airpal) 是 Presto 以 web 作為基礎的開放原始碼查詢介面。 如需有關 Airpal 的詳細資訊，請參閱 [Airpal 文件](https://github.com/airbnb/airpal#airpal)。

在本節中，我們查看 hello 步驟太**hello edgenode 上安裝 Airpal** HDInsight Hadoop 叢集中已有照片安裝。 這可確保該 hello Airpal web 查詢介面是透過網際網路 hello。

1. 使用 SSH，連線 toohello 的 hello Presto 已安裝的 HDInsight 叢集的前端節點：
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 一旦連線後，執行下列命令的 hello。

        sudo slider registry  --name presto1 --getexp presto 
   
    您應該會看到類似 hello 下列輸出：

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. 從 hello 輸出，請注意 hello hello 值**值**屬性。 您將需要此安裝 Airpal hello 叢集 edgenode 上時。 從 hello 上述輸出中，您將需要的 hello 值是**10.0.0.12:9090**。

4. 使用 hello 範本**[這裡](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** toocreate 在 HDInsight 叢集 edgenode 並提供 hello 值 hello 下列螢幕擷取畫面所示。

    ![HDInsight 在 Presto 叢集上安裝 Airpal](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. 按一下 [購買]。

6. Hello 變更套用的 toohello 叢集設定後，您可以使用下列步驟的 hello 存取 hello Airpal web 介面。

    a. 從 hello 叢集刀鋒視窗中，按一下 **應用程式**。

    ![HDInsight 在 Presto 叢集上啟動 Airpal](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    b. 從 hello**安裝應用程式**刀鋒視窗中，按一下 **入口網站**針對 airpal。

    ![HDInsight 在 Presto 叢集上啟動 Airpal](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    c. 出現提示時，輸入 hello 建立 hello HDInsight Hadoop 叢集時，您指定的系統管理員認證。

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a>在 HDInsight 叢集上自訂 Presto 安裝

HDInsight Hadoop 叢集上安裝多照片之後，您可以自訂 hello 安裝 toomake 變更，例如更新記憶體設定、 變更連接器等。執行下列步驟 toodo 因此 hello。

1. 使用 SSH，連線 toohello 的 hello Presto 已安裝的 HDInsight 叢集的前端節點：
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 在 hello 檔案進行組態變更`/var/lib/presto/presto-hdinsight-master/appConfig-default.json`。 如需 Presto 設定的詳細資訊，請參閱[以 YARN 作為基礎之叢集的 Presto 設定](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html)。

3. 停止和終止 hello 目前的執行個體照片。

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. 啟動與 hello 自訂的照片的新執行個體。

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. 等候 hello 新執行個體 toobe 就緒，並記下馬上協調器位址。


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a>產生執行 Presto 之 HDInsight 叢集的基準測試資料

TPC DS 是 hello 業界標準的測量 hello 的許多決策支援系統，包括巨量資料系統的效能。 您可以使用 Presto HDInsight 叢集 toogenerate 資料，並評估它與您的 HDInsight 基準資料會比較方式。 如需詳細資訊，請參閱[這裡](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md)。



## <a name="see-also"></a>另請參閱
* [在 HDInsight 叢集上安裝及使用 Hue](hdinsight-hadoop-hue-linux.md)。 色調是 web UI，讓您輕鬆 toocreate，執行並儲存 Pig 和 Hive 工作，以及做為瀏覽 hello HDInsight 叢集的預設儲存體。

* [在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install-linux.md)。 使用叢集自訂 tooinstall Giraph 上 HDInsight Hadoop 叢集。 Giraph 可讓您使用 Hadoop，處理 tooperform 圖形，並可以搭配 Azure HDInsight。

* [在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install-linux.md)。 使用叢集自訂 tooinstall Solr 上 HDInsight Hadoop 叢集。 Solr 可讓您儲存的資料 tooperform 功能強大的搜尋作業。

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md

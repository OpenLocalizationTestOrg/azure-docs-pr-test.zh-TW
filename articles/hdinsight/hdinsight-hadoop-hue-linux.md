---
title: "HDInsight linux 叢集-Azure 上的 Hadoop aaaHue |Microsoft 文件"
description: "了解 tooinstall 色調 HDInsight 上的叢集，並使用通道 tooroute hello 要求 tooHue。 使用 色調 toobrowse 儲存體，並執行 Hive 或 Pig。"
keywords: Hue hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: f086cbad2a90cc6903fbfccbf4a6be44f8999d07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a>在 HDInsight Hadoop 叢集上安裝和使用 Hue

了解 tooinstall 色調 HDInsight 上的叢集，並使用通道 tooroute hello 要求 tooHue。

> [!IMPORTANT]
> 本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="what-is-hue"></a>何謂 Hue？
色調是一組 Web 應用程式使用 toointeract 與 Hadoop 叢集。 您可以使用相關聯的 Hadoop 叢集 (在 HDInsight 叢集的案例中 hello WASB) 的色調 toobrowse hello 儲存體、 執行工作 Hive 和 Pig 指令碼，並以此類推。 hello 下列元件都可以使用 HDInsight Hadoop 叢集上的色調安裝。

* Beeswax Hive 編輯器
* Pig
* Metastore 管理員
* Oozie
* FileBrowser （其中交談 tooWASB 預設容器）
* 工作瀏覽器

> [!WARNING]
> 完全支援隨附 hello HDInsight 叢集的元件，而且 Microsoft 支援服務將會說明 tooisolate 及解決問題的相關的 toothese 元件。
>
> 自訂元件會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。 這可能會導致解決 hello 問題，或詢問您 tooengage hello 可用的頻道開啟原始碼技術找到深層的專業知識，針對該項技術。 例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。
>
>

## <a name="install-hue-using-script-actions"></a>使用指令碼動作安裝 Hue

hello 指令碼 tooinstall 色調以 Linux 為基礎的 HDInsight 叢集上將會位於 https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh。當做預設儲存體，您可以在與 Azure 儲存體 Blob (WASB) 或 Azure Data Lake Store 的叢集上使用此指令碼 tooinstall 色調。

本節提供有關如何 toouse hello 指令碼佈建 hello 叢集使用 hello Azure 入口網站時的指示。

> [!NOTE]
> Azure PowerShell、 hello Azure CLI、 hello HDInsight.NET SDK 或 Azure 資源管理員範本也可以使用的 tooapply 指令碼動作。 您也可以套用指令碼動作 tooalready 執行中的叢集。 如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。
>
>

1. 開始使用中的 hello 步驟佈建叢集[佈建 HDInsight 叢集在 Linux 上](hdinsight-hadoop-provision-linux-clusters.md)，但是不完成佈建。

   > [!NOTE]
   > tooinstall 色調 HDInsight 上的叢集、 hello 建議叢集前端節點大小至少為 A4 （8 核心，14 GB 記憶體）。
   >
   >
2. 在 hello**選擇性組態**刀鋒視窗中，選取**指令碼動作**，並提供 hello 資訊，如下所示：

    ![提供 Hue 的指令碼動作參數](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "提供 Hue 的指令碼動作參數")

   * **名稱**： 輸入 hello 指令碼動作的易記名稱。
   * **SCRIPT URI**：https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
   * **HEAD**：勾選此選項
   * **背景工作角色**：將此選項保留空白。
   * **ZOOKEEPER**：將此選項保留空白。
   * **參數**：將此選項保留空白。
3. 在 hello 底部 hello**指令碼動作**，使用 hello**選取**按鈕 toosave hello 組態。 最後，使用 hello**選取**在 hello hello 底部的按鈕**選擇性組態**刀鋒視窗 toosave hello 選擇性的組態資訊。
4. 繼續中所述，佈建 hello 叢集[佈建 HDInsight 叢集在 Linux 上](hdinsight-hadoop-provision-linux-clusters.md)。

## <a name="use-hue-with-hdinsight-clusters"></a>搭配使用 Hue 與 HDInsight 叢集

SSH 通道是 hello 唯一方式 tooaccess 色調 hello 叢集上的，一旦它正在執行。 透過 SSH 通道可讓 hello 流量 toogo 直接 toohello 叢集前端節點的 hello 叢集正在色調。 Hello 叢集佈建完成後，使用下列步驟 toouse 色調 HDInsight Linux 叢集上的 hello。

> [!NOTE]
> 我們建議使用 Firefox web 瀏覽器 toofollow hello 下列指示。
>
>

1. 使用中的 hello 資訊[使用 SSH 通道 tooaccess Ambari web UI、 ResourceManager、 JobHistory、 NameNode、 Oozie、 以及其他的 web UI](hdinsight-linux-ambari-ssh-tunnel.md) toocreate SSH 通道，從用戶端系統 toohello HDInsight 叢集，然後再設定您 Web 瀏覽器 toouse hello SSH 通道的 proxy。

2. 一旦您建立的 SSH 通道並設定您的瀏覽器 tooproxy 流量透過它，您必須尋找 hello 的 hello 的主要前端節點的主機名稱。 您可以連接 toohello 叢集使用 SSH 連接埠 22。 比方說，`ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`其中**USERNAME**是您的 SSH 使用者名稱和**CLUSTERNAME**是 hello 叢集的名稱。

    如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

3. 一旦連接之後，使用下列命令 tooobtain hello 的 hello 主要叢集前端節點的完整的網域名稱的 hello:

        hostname -f

    這會傳回名稱類似 toohello 下列：

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    這是 hello 色調網站所在的 hello 主要叢集前端節點的 hello 主機名稱。
4. 使用 http://HOSTNAME:8888 hello 瀏覽器 tooopen hello 色調入口網站。 主機名稱取代 hello hello 先前步驟中取得的名稱。

   > [!NOTE]
   > 當您登入 hello 第一次時，您將會提示的 toocreate toohello 色調入口網站中的帳戶 toolog。 您在此處指定的 hello 認證將會限制的 toohello 入口網站，並不相關的 toohello 管理員或佈建 hello 叢集時所指定的 SSH 使用者認證。
   >
   >

    ![登入 toohello 色調入口網站](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "指定認證色調入口網站")

### <a name="run-a-hive-query"></a>執行 HIVE 查詢
1. 從 hello 色調入口網站中，按一下 **查詢編輯器**，然後按一下 **Hive** tooopen hello 登錄區編輯器。

    ![使用 Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "使用 Hive")
2. 在 hello**協助**索引標籤，下方**資料庫**，您應該會看到**hivesampletable**。 這是 HDInsight 上的所有 Hadoop 叢集隨附的範例資料表。 輸入 hello 右窗格中的範例查詢和 hello 上看見 hello 輸出**結果**hello 螢幕擷取畫面所示，在下面 hello 窗格中索引標籤。

    ![執行 Hive 查詢](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "執行 Hive 查詢")

    您也可以使用 hello**圖表**索引標籤上 toosee hello 結果的視覺化表示法。

### <a name="browse-hello-cluster-storage"></a>瀏覽 hello 叢集存放裝置
1. 從 hello 色調入口網站中，按一下 **檔案瀏覽器**hello 右上角中的 hello 功能表列中。
2. 依預設 hello 檔案瀏覽器會開啟在 hello **/使用者/myuser**目錄。 按一下 前 hello hello toogo toohello 根路徑的 hello 與 hello 叢集相關聯的 Azure 儲存體容器中的使用者目錄的 hello 正斜線。

    ![使用檔案瀏覽器](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "使用檔案瀏覽器")
3. 以滑鼠右鍵按一下檔案或資料夾 toosee hello 可用的作業。 使用 hello**上傳**hello 右上角 tooupload 檔案 toohello 目前目錄中的按鈕。 使用 hello**新增**按鈕 toocreate 新檔案或目錄。

> [!NOTE]
> hello 色調檔案瀏覽器只會顯示 hello 的 hello 與 hello HDInsight 叢集相關聯的預設容器的內容。 任何額外的儲存體帳戶/容器，您可能有相關聯的 hello 叢集將無法存取使用 hello 檔案瀏覽器。 不過，hello 與 hello 叢集相關聯的其他容器永遠都可以存取 hello Hive 工作。 例如，如果您輸入 hello 命令`dfs -ls wasb://newcontainer@mystore.blob.core.windows.net`在 hello 登錄區編輯器 中，您可以看到 hello 內容以及其他容器。 這個命令中， **newcontainer**不 hello 與叢集相關聯的預設容器。
>
>

## <a name="important-considerations"></a>重要考量︰
1. hello 用指令碼 tooinstall 色調會安裝它只能在 hello hello 叢集的主要前端節點上。

2. 在安裝期間，會重新啟動來更新 hello 組態的多個 Hadoop 服務 （HDFS、 YARN、 MR2、 Oozie）。 安裝色調的 hello 指令碼完成之後，它最多可能需要一些時間，其他的 Hadoop 服務 toostart。 一開始可能會影響 Hue 的效能。 所有服務啟動之後，Hue 就可以完全正常運作。
3. 色調不了解 Tez 作業 hello 登錄區的目前預設值。 如果您想 toouse MapReduce hello Hive 執行引擎時，，更新下列命令指令碼中的 hello 指令碼 toouse hello:

        set hive.execution.engine=mr;

4. 使用 Linux 叢集時，您可以在您的服務正在執行的案例 hello 主要叢集前端節點上 hello 資源管理員無法執行 hello 次要上時。 Hello 叢集上使用的執行作業的色調 tooview 詳細資料時，這種狀況可能會導致錯誤 （如下所示）。 不過，您可以在 hello 作業完成時，檢視 hello 工作詳細資料。

   ![Hue 入口網站錯誤](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Hue 入口網站錯誤")

   這是因為 tooa 已知問題。 因應措施，修改 Ambari 使 hello 作用中的資源管理員也會執行 hello 主要叢集前端節點上。
5. 當 HDInsight 叢集使用 Azure 儲存體 (使用 `wasb://`) 時，色調能了解 WebHDFS。 因此，hello 與指令碼動作搭配使用的自訂指令碼會安裝 WebWasb，是指 tooWASB WebHDFS 相容服務。 因此，即使 hello 色調入口網站會指出 HDFS 位置中的 (例如當您將滑鼠移 hello**檔案瀏覽器**)，它應該解譯為 WASB。

## <a name="next-steps"></a>後續步驟
* [在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install-linux.md)。 使用叢集自訂 tooinstall Giraph 上 HDInsight Hadoop 叢集。 Giraph 可讓您處理使用 Hadoop，tooperform 圖形，並搭配 Azure HDInsight。
* [在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install-linux.md)。 使用叢集自訂 tooinstall Solr 上 HDInsight Hadoop 叢集。 Solr 可讓您儲存的資料 tooperform 功能強大的搜尋作業。
* [在 HDInsight 叢集上安裝 R](hdinsight-hadoop-r-scripts-linux.md)。 使用叢集自訂 tooinstall R HDInsight Hadoop 叢集上。 R 是一個用於統計計算的開放原始碼語言和環境。 它提供數百個內建的統計函式及它自己的程式設計語言，此語言結合了函式型和物件導向程式設計的層面。 它也提供廣泛的圖形功能。

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md

---
title: "aaaGet 開始使用 HDInsight 的 Azure 上的 R 伺服器 |Microsoft 文件"
description: "了解如何 toocreate Apache 二手包含 R Server 的 HDInsight 叢集上，並送出 hello 叢集上的 R 指令碼。"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a>開始使用 HDInsight 中的 R Server

HDInsight 包括 R Server 選項 toobe 整合到您的 HDInsight 叢集。 此選項可讓 R 指令碼 toouse Spark 和 MapReduce toorun 分散式計算。 在本文件中，您學會 toocreate R 伺服器 HDInsight 叢集，然後再執行 R 指令碼將示範如何使用 Spark 散發 R 運算的方式。


## <a name="prerequisites"></a>必要條件

* **Azure 訂用帳戶**：開始進行本教學課程之前，您必須擁有 Azure 訂用帳戶。 移 toohello 文章[取得 Microsoft Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)如需詳細資訊。
* **安全殼層 (SSH) 用戶端**: SSH 用戶端使用 tooremotely 連接 toohello HDInsight 叢集，並直接在 hello 叢集上執行命令。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。
* **SSH 金鑰 （選擇性）**： 您可以保護 hello SSH 使用帳戶 tooconnect toohello 叢集使用密碼或公開金鑰。 使用密碼更為簡單，並可讓您 tooget 啟動而不需要 toocreate 公開/私密金鑰組。 不過，使用金鑰更加安全。

> [!NOTE]
> 本文件中的 hello 步驟假設您使用的密碼。


## <a name="automated-cluster-creation"></a>自動化的叢集建立

您可以自動化 hello 建立 HDInsight R 伺服器使用 Azure Resource Manager 範本、 hello SDK，以及 PowerShell。

* toocreate R 伺服器使用 Azure 資源管理的範本，請參閱[部署 R 伺服器 HDInsight 叢集](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/)。
* toocreate 的 R 伺服器使用 hello.NET SDK，請參閱[HDInsight 使用 hello.NET SDK 中建立 linux 叢集。](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* toodeploy R 伺服器上使用 powershell，請參閱 hello 文章[具有 PowerShell HDInsight 上建立 R Server](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)。


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a>建立 hello 叢集使用 hello Azure 入口網站

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 依序選取 [新增] -> [情報 + 分析] -> [HDInsight]。

    ![建立新叢集的影像](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. 在 hello**快速建立**體驗，輸入 hello 叢集的名稱在 hello**叢集名稱**欄位。 如果您有多個 Azure 訂用帳戶，使用 hello**訂用帳戶**項目 tooselect hello 其中一個要 toouse。

    ![叢集名稱和訂用帳戶選取項目](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. 選取**叢集類型**tooopen hello**叢集設定**刀鋒視窗。 在 hello**叢集設定**刀鋒視窗中，選取下列選項的 hello:

    * **叢集類型**：R 伺服器
    * **版本**: hello 叢集上的 R 伺服器 tooinstall 選取 hello 版本。 目前可用的 hello 版本是***R 伺服器 9.1 (HDI 3.6)***。 Hello 可用版本的 R Server 的版本資訊可用[這裡](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)。
    * **R Studio community 版本的 R 伺服器**: hello 邊緣節點上的預設會安裝此瀏覽器為基礎的 IDE。 如果您想使用 toonot 進行安裝，然後取消核取 [hello] 核取方塊。 如果您選擇 toohave 它安裝，來存取的 hello RStudio 伺服器登入位於入口網站應用程式 刀鋒視窗，供您的叢集，一旦建立之後的 hello URL。
    * Hello 其他選項保留 hello 預設值，並使用 hello**選取**按鈕 toosave hello 叢集類型。

        ![叢集類型刀鋒視窗螢幕擷取畫面](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. 輸入 [叢集登入使用者名稱] 和 [叢集登入密碼]。

    指定 [SSH 使用者名稱]。 SSH 使用的 tooremotely toohello 叢集使用連接**安全殼層 (SSH)**用戶端。 在這個對話方塊中，或 （hello 組態 索引標籤中的 hello 叢集） 建立 hello 叢集後，您可以指定 hello SSH 使用者。 R 伺服器是設定的 tooexpect **SSH 使用者名稱**的"remoteuser"。  **如果您使用不同的使用者名稱，您必須在建立 hello 叢集後，執行額外的步驟。**

    檢查是否有保留 hello 方塊**使用與叢集登入相同的密碼**toouse**密碼**hello 驗證輸入除非您偏好使用公用金鑰。  您必須透過為，比方說，RTVS、 RStudio 或其他桌面 IDE 的遠端用戶端 hello 叢集上的公開/私密金鑰組 tooaccess R Server。 如果您安裝 hello RStudio Server community edition，您會需要 toochoose SSH 密碼。     

    toocreate 和使用公開/私密金鑰組，取消核取**使用與叢集登入相同的密碼**，然後選取 **公開金鑰**並繼續進行，如下所示。 這些指示會假設您已安裝 Cygwin 和 ssh-keygen 或具同等效力的命令。

    * 從您的膝上型電腦上的 hello 命令提示字元中產生公開/私密金鑰組：

        ssh-keygen -t rsa -b 2048

    * 遵循 hello 提示 tooname 金鑰檔案，然後輸入複雜密碼為增加安全性。 您的畫面看起來應該像下列映像的 hello:

        ![Windows 中的 SSH 命令列](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * 此命令會建立私用金鑰檔和 hello 名稱 < 私用金鑰的檔名 >.pub，例如 furiosa 和 furiosa.pub 底下的公用金鑰檔案。

        ![SSH dir](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * 然後指定 hello 公開金鑰檔案 (&#42;。pub) 時指派 HDI 叢集認證與最後確認您的資源群組和區域並選取**下一步**。

        ![認證刀鋒視窗](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * 變更您的膝上型電腦上的 hello 私用金鑰檔的權限：

        chmod 600 <private-key-filename>

   * 遠端登入使用 SSH hello 私用金鑰檔：

        ssh –i <private-key-filename> remoteuser@<hostname public ip>

      或者，您也可以做 Hadoop Spark 一部分 hello 定義計算內容的 R 伺服器 hello 用戶端上。 請參閱 hello**為 Hadoop 用戶端使用 Microsoft R Server**小節中[建立計算內容的 Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark)。

6. hello 快速建立您轉換 toohello**儲存體**hello hello 主要位置使用的設定 toobe HDFS 檔案系統 hello 叢集所用的刀鋒視窗 tooselect hello 儲存體帳戶。 選取新的或現有的 Azure 儲存體帳戶或現有的 Data Lake 儲存體帳戶。

    - 如果您選取的 Azure 儲存體帳戶時，會選取現有的儲存體帳戶選擇**選取儲存體帳戶**，然後選取 hello 相關帳戶。 建立新的帳戶使用 hello**新建**hello 中的連結**選取儲存體帳戶**> 一節。

      > [!NOTE]
      > 如果您選取**新增**您必須輸入 hello 新儲存體帳戶的名稱。 如果已接受 hello 名稱，則會出現綠色核取。

      hello**預設容器**預設 toohello hello 叢集名稱。 保留這個預設值為 hello 值。

      如果已選取新的儲存體帳戶選項，提示 tooselect**位置**是 tooselect 指定哪一個區域 toocreate hello 儲存體帳戶。  

         ![資料來源刀鋒視窗](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > 選擇 hello hello 預設的資料來源的位置時，也會設定 hello 位置 hello HDInsight 叢集。 hello 叢集和預設資料來源必須在 hello 相同的區域。

    - 如果您想 toouse 現有的資料湖存放區，然後選取 hello ADLS 儲存體帳戶 toouse 和新增 hello 叢集*新增*身分識別 tooyour 叢集 tooallow 存取 toohello 存放區。 如需此程序的詳細資訊，請參閱[使用 Azure 入口網站建立具有 Data Lake Store 的 HDInsight 叢集](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal)。

    使用 hello**選取**按鈕 toosave hello 資料來源組態。


7. hello**摘要**刀鋒視窗然後顯示 toovalidate 您的設定。 您可以在這裡變更您**叢集大小**toomodify hello 叢集中的伺服器數目和也指定任何**編寫指令碼動作**想 toorun。 除非您知道您需要較大的叢集，將背景工作節點數 hello 保留 hello 預設值是`4`。 hello 估計成本的 hello 叢集會顯示 hello 刀鋒視窗中。

    ![叢集摘要](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > 如有需要您可以調整您的叢集，稍後透過 hello 入口網站 (**叢集** -> **設定** -> **延展叢集**) tooincrease 或減少 hello 背景工作節點數。  此調整大小可能很有用的閒置到達便關閉 hello 叢集時不在使用中，或新增容量 toomeet hello 需求的較大型的工作。
   >
   >

   調整您的叢集、 hello 資料節點和 hello 邊緣節點記住的一些因素 tookeep 包括：  

   * hello 效能上的 Spark 的分散式 R Server 分析時，背景工作節點數成正比 toohello hello 資料很大。  

   * R 伺服器分析的 hello 效能中是線性 hello 所分析的資料大小。 例如：  

     * 小型 toomodest 資料效能最好分析 hello 邊緣節點上的本機計算內容中時。  如需有關在本機的 hello 與 Spark 計算內容的 hello 案例適合，請參閱 R Server 計算內容選項在 HDInsight 上。<br>
     * 如果您登入 toohello 邊緣節點，然後執行 R 指令碼，則所有但 hello ScaleR rx 函數執行<strong>本機</strong>hello 邊緣節點上。 因此 hello 記憶體及核心 hello 邊緣節點的數目應該要據以調整大小。 如果您使用 R Server HDI 上做為遠端計算內容從膝上型電腦套用 hello。

     ![節點定價層刀鋒視窗](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     使用 hello**選取**按鈕 toosave hello 節點定價組態。

   還有 [下載範本和參數] 的連結。 按一下此連結 toodisplay 指令碼可以使用的 tooautomate hello 建立 hello 選設定與叢集上。 一旦建立之後，您也可以從 hello Azure 入口網站的項目叢集中執行這些指令碼。

   > [!NOTE]
   > 花一些時間 hello 叢集 toobe 建立，通常是 20 分鐘的時間。 使用 hello 磚上 hello 開始面板，或 hello**通知**hello 建立程序上剩餘的 hello 頁面 toocheck 的 hello 上的項目。
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a>連接 tooRStudio 伺服器

如果您選擇 tooinclude RStudio Server community edition 安裝中，您就可以存取透過兩個不同方法的 hello RStudio 登入。

1. 移 toohello 下列 URL (其中**CLUSTERNAME**是您已建立 hello 叢集 hello 名稱):

    https://**CLUSTERNAME**.azurehdinsight.net/rstudio/

2. 在 hello Azure 入口網站中，選取 hello 中開啟您的叢集 hello 項目**R Server 儀表板**快速連結，然後選取 hello **R Studio 儀表板**:

     ![存取 hello R studio 儀表板](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![存取 hello R studio 儀表板](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > 使用 hello 方法，不論 hello 第一次登入您需要 tooauthenticate 兩次。  在 hello 第一次驗證，可讓 hello*叢集系統管理員使用者識別碼*和*密碼*。 在 hello 第二個提示字元中提供 hello *SSH userid*和*密碼*。 後續的記錄集只需要 hello *SSH 密碼*和*userid*。

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a>Toohello R Server 邊緣節點連接

連接導覽伺服器邊緣節點 hello 命令搭配使用 SSH hello HDInsight 叢集：

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> 您可以找到 hello`USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`中 hello Azure 入口網站，然後選取您的叢集位址**所有設定** -> **應用程式** -> **RServer**. 這會顯示 hello hello 邊緣節點的 SSH 端點資訊。
>
> ![Hello SSH 端點 hello 邊緣節點的影像](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

如果您使用密碼 toosecure SSH 使用者帳戶，則提示的 tooenter 它。 如果您使用公開金鑰，您可能必須 toouse hello`-i`參數 toospecify hello 相符的私密金鑰。 例如：

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

如需詳細資訊，請參閱[連接 tooHDInsight (Hadoop) 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

一旦連接之後，您會抵達提示的類似 toohello 下列：

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a>啟用多個並行使用者

您可以啟用多個並行使用者藉由新增更多使用者 hello 邊緣節點上的 hello RStudio 社群版本中執行。

當您建立 HDInsight 叢集時，您必須提供兩個使用者 (HTTP 使用者和 SSH 使用者)：

![並行使用者 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- **叢集登入使用者名稱**: 的 HTTP 使用者進行驗證，透過 hello HDInsight 閘道所使用的 tooprotect hello HDInsight 叢集，您所建立。 此 HTTP 使用者是使用的 tooaccess hello Ambari UI、 YARN UI，以及其他 UI 元件。
- **安全殼層 (SSH) 的使用者名稱**： 透過安全殼層的 SSH 使用者 tooaccess hello 叢集。 此使用者是 hello hello 前端節點、 背景工作節點和邊緣節點的 Linux 系統中的使用者。 因此您可以使用安全殼層 tooaccess hello 節點中的遠端叢集。

hello Microsoft R Server 類型的 HDInsight 叢集上所使用的 hello R Studio Server 社群版本只接受 Linux 使用者名稱與密碼做為登入機制。 但不支援傳遞權杖。 因此，如果您已建立新的叢集，並想 toouse R Studio tooaccess，您需要在 toolog 兩次。

- 第一次使用認證登入 hello HTTP 使用者透過 hello HDInsight 閘道： 

    ![並行使用者 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- 然後使用 hello SSH 使用者認證 toolog tooRStudio 中：
  
    ![並行使用者 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

目前，在佈建 HDInsight 叢集時，只可以建立一個 SSH 使用者帳戶。 因此 tooenable 多個使用者 tooaccess HDInsight 上的 Microsoft R Server 叢集，我們需要 toocreate hello Linux 系統中的其他使用者。

由於 RStudio Server 社群 hello 叢集邊緣節點上執行，但有以下幾個步驟：

1. 您可以使用建立 hello SSH 使用者 toolog toohello 邊緣節點中
2. 在邊緣節點中新增更多 Linux 使用者
3. 使用 RStudio 社群版本與 hello 所建立的使用者

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a>步驟 1： 使用 toohello 邊緣節點中建立的 hello SSH 使用者 toolog

下載任何 SSH 工具 （例如 Putty) 並使用 hello 現有 SSH 使用者 toolog 中。 然後遵循所提供的 hello 指示[連接 tooHDInsight (Hadoop) 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello 邊緣節點。 hello 邊緣節點位址 R Server 在 HDInsight 叢集上： *clustername-ed-ssh.azurehdinsight.net*


### <a name="step-2-add-more-linux-users-in-edge-node"></a>步驟 2：在邊緣節點中新增更多 Linux 使用者

tooadd 使用者 toohello 邊緣節點，執行 hello 命令：

    sudo useradd yournewusername -m
    sudo passwd yourusername

您應該會看到下列項目傳回 hello: 

![並行使用者 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

當系統提示您輸入"目前的 Kerberos 密碼: 」，請按**Enter** tooignore 它。 hello`-m`選項`useradd`命令表示 hello 系統將會建立 hello 使用者所需的 RStudio 社群版本的主資料夾。


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a>步驟 3： 使用 RStudio 社群版本與 hello 所建立的使用者

使用 hello 使用者建立 toolog tooRStudio 中：

![並行使用者 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

RStudio 表示使用 hello 新使用者的通知 (例如，這裡*sshuser6*) toolog hello 叢集中： 

![並行使用者 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

您也可以登入使用 hello 原始認證 (依預設，它是*sshuser*) 同時從另一個瀏覽器視窗。

您可以使用 scaleR 函式來提交作業。 以下是範例 hello 命令會使用 toorun 作業：

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


送出 hello 作業在 YARN UI 中的不同的使用者名稱 底下的注意事項：

![並行使用者 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

請注意，也該 hello 新加入的使用者不需要根權限在 Linux 系統中，但它們有 hello 相同存取 tooall hello hello 遠端 HDFS 與 WASB 儲存體中的檔案。


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a>使用 hello R 主控台

1. 從 hello SSH 工作階段，使用下列命令 toostart hello R 主控台 hello:  

        R

2. 您應該會看到類似 toohello 下列輸出：
    
    R 版本 3.2.2 (2015年-08-14)-"引發 Safety"Copyright (C) 2015 hello R Foundation 統計運算平台： x86_64-pc-linux-gnu （64 位元）

    R 是免費的軟體，且「絕對無瑕疵責任擔保」。
    您是  褖畫惎 tooredistribute 它在某些情況下。
    輸入 'license()' 或 'licence()' 可取得發佈詳細資料。

    支援自然語言，但是在英文地區設定中執行

    R 是共同作業專案，具有許多的參與者。
    如需詳細資訊和 'citation()' 的 'contributors()' 輸入上 toocite R 或 R 發行集內的封裝中。

    輸入一些示範、 線上說明，請 ' help()' 或 'help.start()' 的 HTML 瀏覽器介面 toohelp 'demo()'。
    輸入 'q()' tooquit。

    Microsoft R 伺服器 8.0 版：R 的增強發佈 Microsoft 套件 Copyright (C) 2016 Microsoft Corporation

    輸入 'readme()' 可取得版本資訊。
    >

3. 從 hello`>`提示字元，您可以輸入 R 程式碼。 R 伺服器包括 tooeasily 可讓您的封裝互動的 Hadoop 和執行分散式的計算。 例如，使用下列命令 tooview hello 根 hello hello HDInsight 叢集的預設檔案系統的 hello:

    rxHadoopListFiles("/")

4. 您也可以使用 hello WASB 樣式定址。

    rxHadoopListFiles("wasb:///")


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a>從 Microsoft R Server 或 Microsoft R Client 的遠端執行個體使用 HDI 上的 R Server

從 Microsoft R Server 或 Microsoft R 用戶端桌上型電腦或膝上型電腦上執行的遠端執行個體存取 toohello HDI Hadoop Spark 計算內容可能 tooset 它。 請參閱**為 Hadoop 用戶端使用 Microsoft R Server** hello 的小節[建立計算內容的 Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md)。 toodo 因此，您需要下列選項，您的膝上型電腦上定義 hello RxSpark 計算內容時的 toospecify hello: hdfsShareDir，shareDir，sshUsername，sshHostname，sshSwitches，和 sshProfileScript。 例如：


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a>使用計算內容

計算內容可讓您 toocontrol 計算是在本機執行 hello 邊緣節點上或分散在 hello hello HDInsight 叢集中的節點。

1. 從 RStudio 伺服器或 hello R 主控台 （中的 SSH 工作階段），使用下列程式碼 tooload 範例資料到 hello 預設儲存體，HDInsight 的 hello:

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. 接下來，讓我們來建立部分資料的資訊，並定義兩個資料來源，以便我們可以使用 hello 資料。

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. 讓我們使用 hello 本機計算內容的 hello 資料執行羅吉斯迴歸。

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    您應該看到的結尾行類似 toohello 下列輸出：

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. 接下來，我們先執行 hello 使用 hello Spark 內容的相同羅吉斯迴歸。 hello Spark 內容會發佈 hello 透過 hello HDInsight 叢集中的所有 hello 背景工作節點處理。

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > 您也可以使用 MapReduce toodistribute 計算叢集節點之間。 如需計算內容的詳細資訊，請參閱[適用於 HDInsight 中 R 伺服器的計算內容選項](hdinsight-hadoop-r-server-compute-contexts.md)。


## <a name="distribute-r-code-toomultiple-nodes"></a>將 R 程式碼 toomultiple 節點

使用 R Server 可以輕易地讓現有的 R 程式碼並執行它 hello 叢集中的多個節點之間使用`rxExec`。 執行參數掃掠或模擬時，這個函式非常有用。 hello 下列程式碼是如何的範例 toouse `rxExec`:

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

如果您仍在使用 hello Spark 或 MapReduce 內容，此命令會傳回 hello 背景工作角色節點的 hello nodename 值該 hello 程式碼`(Sys.info()["nodename"])`上執行。 例如，在四個節點叢集上，您預期 tooreceive 輸出類似 toohello 下列：

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a>存取 Hive 和 Parquet 中的資料

R 伺服器 9.1 提供的功能可允許使用 Hive 和 Parquet 中的直接存取 toodata ScaleR 函數 hello Spark 計算內容中。 這些功能都是透過新 ScaleR 資料來源運作的函式呼叫 RxHiveData 和 RxParquetData 藉由使用 Spark SQL tooload 資料直接將 ScaleR 以進行分析的 Spark 資料框架。  

下列程式碼的 hello 提供 hello 新函式的使用範例程式碼：

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


如需使用這些新的函式的詳細資訊，請參閱 hello 中的線上說明 R Server 藉由使用 hello`?RxHivedata`和`?RxParquetData`命令。  


## <a name="install-additional-r-packages-on-hello-edge-node"></a>Hello 邊緣節點上安裝其他的 R 封裝

如果您想要在 hello 邊緣節點 tooinstall 其他 R 封裝，您可以使用`install.packages()`直接從 hello R 主控台時連線的 toohello 邊緣透過 SSH 的節點。 不過，如果您需要將 R 封裝 tooinstall hello 工作者 hello 叢集中節點上的，您必須使用指令碼動作。

指令碼動作是使用的 toomake 組態變更 toohello HDInsight 叢集或 tooinstall 其他軟體，例如其他 R 封裝 Bash 指令碼。 tooinstall 其他封裝使用指令碼動作，使用下列步驟的 hello:

> [!IMPORTANT]
> 使用指令碼動作 tooinstall 其他 R 封裝只能在建立 hello 叢集之後。 Hello 指令碼是根據 R 伺服器完整地安裝和設定時，請勿在叢集建立期間使用這個程序。
>
>

1. 從 hello [Azure 入口網站](https://portal.azure.com)，選取您的 R 伺服器，在 HDInsight 叢集上。

2. 從 hello**設定**刀鋒視窗中，選取**指令碼動作**然後**提交新**toosubmit 新的指令碼動作。

   ![指令碼動作刀鋒視窗的影像](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. 從 hello**送出指令碼動作**刀鋒視窗中，提供下列資訊的 hello:

   * **名稱**: 易記名稱 tooidentify 此指令碼

   * **Bash 指令碼 URI**：`http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`

   * **前端**︰此項目應該是**未核取**狀態

   * **背景工作**︰此項目應該是**已核取**狀態

   * **邊緣節點**︰此項目應該是**未核取**狀態

   * **Zookeeper**︰此項目應該是**未核取**狀態

   * **參數**: hello R 封裝 toobe 安裝。 例如， `bitops stringr arules`

   * **保存此指令碼...**︰此項目應該是**已核取**狀態  

   > [!NOTE]
   > 1. 根據預設，所有的 R 封裝會安裝從 hello Microsoft MRAN 儲存機制已安裝的 R 伺服器 hello 版本與一致的快照集。 如果您想 tooinstall 較新版本的封裝，就不相容的某些風險。 不過這種安裝方法，就是指定`useCRAN`為 hello hello 封裝的第一個項目清單，例如`useCRAN bitops, stringr, arules`。  
   > 2. 有些 R 套件需要額外的 Linux 系統程式庫。 為了方便起見，我們已預先安裝 hello hello 前 100 最受歡迎的 R 封裝所需的相依性。 不過，如果您安裝的 hello R 封裝需要超出這些範圍的程式庫然後您必須下載 hello 這裡使用的基底指令碼並新增步驟 tooinstall hello 系統程式庫。 您必須上傳 hello 修改指令碼 tooa 公用 blob 在 Azure 儲存體容器，並使用 hello 修改指令碼 tooinstall hello 封裝。
   >    如需開發指令碼動作的詳細資訊，請參閱 [指令碼動作開發](hdinsight-hadoop-script-actions-linux.md)。  
   >
   >

   ![新增指令碼動作](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. 選取**建立**toorun hello 指令碼。 Hello 指令碼完成之後，就有一個 hello R 封裝可用背景工作的所有節點上。


## <a name="using-microsoft-r-server-operationalization"></a>使用 Microsoft R 伺服器實作

完成您的資料模型化時，您可以實施 hello 模型 toomake 預測。 Microsoft R Server 實施的 tooconfigure 執行 hello 下列步驟：

首先，ssh hello 邊緣節點。 例如， 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

在使用後 ssh，變更用於 hello 相關版本和 sudo hello dotnet dll 的目錄： 

- 對於 Microsoft R Server 9.1：

    cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll

- 對於 Microsoft R Server 9.0：

    cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

與一個方塊設定 tooconfigure Microsoft R Server 實施 hello 遵循：

1. 選取 [設定 R 伺服器來實施]
2. 選取 A. One-box (web + compute nodes)
3. 輸入密碼以 hello **admin**使用者

![one box op](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

您也可以選擇性地執行診斷測試來執行診斷檢查，如下所示：

1. 選取 6. Run diagnostic tests
2. 選取 A. Test configuration
3. 輸入上述設定步驟中的使用者名稱 = “admin” 和密碼
4. 確認整體健全狀況 = pass
5. 結束 hello 管理公用程式
6. 結束 SSH

![實作的診斷](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
>**在 Spark 上取用 Web 服務時長時間延遲**
>
>如果嘗試 tooconsume web 服務建立 mrsdeploy Spark 計算內容中的函式使用時，您會遇到冗長延遲，您可能需要 tooadd 部分遺失的資料夾。 hello Spark 應用程式所屬 tooa 使用者稱為 '*rserve2*' 時被叫用 web 服務使用 mrsdeploy 函式。 toowork 解決此問題：

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


在這個階段，hello 用於實施已完成設定。 現在您可以使用 hello 'mrsdeploy' 邊緣節點上您 RClient tooconnect toohello 實施上的套件，並開始使用它的功能類似[遠端執行](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution)和[web 服務](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette)。 根據是否叢集中設定虛擬網路上或不，您可能需要 tooset 設定連接埠轉送通道透過 SSH 登入。 hello 下列各節說明如何設定此通道 tooset。

### <a name="rserver-cluster-on-virtual-network"></a>虛擬網路上的 RServer 叢集

請確定您允許流量通過連接埠 12800 toohello 邊緣節點。 這樣一來，您可以使用 hello 邊緣節點 tooconnect toohello 實施功能。


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


如果 hello`remoteLogin()`不能連接 toohello 邊緣節點，但可以 SSH toohello 邊緣節點，然後您需要 tooverify 是否正確或沒有已設定連接埠 12800 hello 規則 tooallow 流量。 如果您繼續 tooface hello 問題，您可以藉由設定連接埠正透過的通道 SSH 暫時解決它。 如需指示，請參閱下列區段的 hello。

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a>RServer 叢集未設定於虛擬網路上

如果您的叢集未設定於 vnet 上，或如果您在透過 vnet 連線時遇到問題，可以使用 SSH 連接埠轉送通道︰

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

在 Putty 上，您也可以做此設定。

![putty ssh 連線](./media/hdinsight-hadoop-r-server-get-started/putty.png)

一旦您的 SSH 工作階段為作用中，從您電腦的連接埠 12800 hello 流量就會轉送 toohello 邊緣節點的連接埠 12800 透過 SSH 工作階段。 請務必在 `remoteLogin()` 方法中使用 `127.0.0.1:12800`。 這會記錄透過連接埠轉送 toohello 邊緣節點的實施。


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a>Microsoft R Server 實施 tooscale 如何計算 HDInsight 背景工作節點上的節點

### <a name="decommission-hello-worker-nodes"></a>解除委任 hello 背景工作節點

Microsoft R 伺服器目前無法透過 Yarn 管理。 如果 hello 背景工作節點不是已解除任務，hello Yarn 資源管理員將無法正常運作因為並不會察覺的 hello 伺服器所佔據的 hello 資源。 在順序 tooavoid 這種情況下，我們建議您相應 hello 計算節點之前解除委任 hello 背景工作節點。

步驟 toodecommissioning 背景工作節點：

* 登入 tooHDI 叢集 Ambari 主控台，然後按一下 [主機] 索引標籤上
* 選取 (解除委任 toobe) 的背景工作節點，請按一下 [動作] > [選取主機] > [主機]"> 按一下 「 開啟 ON 維護模式 」。 例如，在下列映像的 hello 我們已選取 wn3 和 wn4 toodecommission。  

   ![解除委任背景工作節點](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* 選取 [動作] > [選取的主機] > [DataNode] > 按一下 [解除委任]
* 選取 [動作] > [選取的主機] > [NodeManagers] > 按一下 [解除委任]
* 選取 [動作] > [選取的主機] > [DataNode] > 按一下 [停止]
* 選取 [動作] > [選取的主機] > [NodeManagers] > 按一下 [停止]
* 選取 [動作] > [選取的主機] > [主機] > 按一下 [停止所有元件]
* 取消選取 hello 背景工作節點，並選取 hello 前端節點
* 選取 [動作] > [選取的主機] > [主機] > [重新啟動所有元件]

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a>在每個已解除委任的背景工作節點上設定計算節點

1. 透過 SSH 連線到每個已解除委任的背景工作角色節點。
2. 使用 `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll` 執行系統管理公用程式。
3. 請輸入"1"tooselect 選項"設定 R 伺服器的實施"。
4. 請輸入"c"tooselect 選項 「 C. Compute node。 這會在 hello 背景工作節點上設定 hello 計算節點。
5. 結束 hello 管理公用程式。

### <a name="add-compute-nodes-details-on-web-node"></a>在 Web 節點上新增計算節點詳細資料

在設定已解除任務的背景工作的所有節點之後 toorun 計算節點、 hello 邊緣節點上回來 hello Microsoft R Server web 節點設定中新增已解除任務的背景工作角色節點的 IP 位址：

* SSH hello 邊緣節點。
* 執行 `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`。
* 尋找 hello"Uri"區段中，並新增背景工作節點的 IP 和連接埠詳細資料。

    ![解除委任背景工作節點 cmdline](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a>疑難排解

如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。


## <a name="next-steps"></a>後續步驟

現在，您應該了解如何 toocreate 新的 HDInsight 叢集，其中包含使用的 hello R 伺服器與 hello 基本概念 hello 的 SSH 工作階段從 R 主控台。 hello 下列主題說明管理和使用 HDInsight 上的 R 伺服器的其他方式：

* [新增 RStudio 伺服器 tooHDInsight （如果未安裝在叢集建立期間）](hdinsight-hadoop-r-server-install-r-studio.md)
* [適用於 HDInsight 中 R 伺服器的計算內容選項](hdinsight-hadoop-r-server-compute-contexts.md)
* [適用於 HDInsight R 伺服器的 Azure 儲存體選項](hdinsight-hadoop-r-server-storage.md)

---
title: "aaaGet 開始使用 HDInsight 的 Azure 上 HBase 範例 |Microsoft 文件"
description: "請遵循此 Apache HBase 範例 toostart HDInsight 上使用 hadoop。 從 hello HBase 殼層建立資料表，並加以查詢，使用登錄區。"
keywords: "hbasecommand,hbase 範例"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="f1103-105">開始使用 HDInsight 中的 Apache HBase 範例</span><span class="sxs-lookup"><span data-stu-id="f1103-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="f1103-106">了解如何建立 HBase 資料表 toocreate 在 HDInsight HBase 叢集，以及使用 Hive 查詢的資料表。</span><span class="sxs-lookup"><span data-stu-id="f1103-106">Learn how toocreate an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="f1103-107">如需一般 HBase 資訊，請參閱 [HDInsight HBase 概觀][hdinsight-hbase-overview]。</span><span class="sxs-lookup"><span data-stu-id="f1103-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="f1103-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="f1103-108">Prerequisites</span></span>
<span data-ttu-id="f1103-109">開始嘗試這個 HBase 範例之前，您必須具備下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="f1103-109">Before you begin trying this HBase example, you must have hello following items:</span></span>

* <span data-ttu-id="f1103-110">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f1103-110">**An Azure subscription**.</span></span> <span data-ttu-id="f1103-111">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="f1103-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="f1103-112">[安全殼層 (SSH)](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="f1103-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="f1103-113">[cURL](http://curl.haxx.se/download.html)。</span><span class="sxs-lookup"><span data-stu-id="f1103-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="f1103-114">建立 HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="f1103-114">Create HBase cluster</span></span>
<span data-ttu-id="f1103-115">hello 下列程序會使用 Azure Resource Manager 範本 toocreate 版本 3.4 linux HBase 叢集和 hello 相依的預設 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f1103-115">hello following procedure uses an Azure Resource Manager template toocreate a version 3.4 Linux-based HBase cluster and hello dependent default Azure Storage account.</span></span> <span data-ttu-id="f1103-116">toounderstand hello 參數用於 hello 程序和其他叢集建立方法，請參閱[HDInsight 叢集建立 Linux Hadoop](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="f1103-116">toounderstand hello parameters used in hello procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="f1103-117">按一下下列映像 tooopen hello 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="f1103-117">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="f1103-118">hello 範本位於 公用 blob 容器中。</span><span class="sxs-lookup"><span data-stu-id="f1103-118">hello template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="f1103-119">從 hello**自訂部署**刀鋒視窗中，輸入下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="f1103-119">From hello **Custom deployment** blade, enter hello following values:</span></span>
   
   * <span data-ttu-id="f1103-120">**訂用帳戶**： 選取您是使用的 toocreate hello 叢集的 Azure 訂閱。</span><span class="sxs-lookup"><span data-stu-id="f1103-120">**Subscription**: Select your Azure subscription that is used toocreate hello cluster.</span></span>
   * <span data-ttu-id="f1103-121">**資源群組**：建立 Azure 資源管理群組，或選取現有的資源管理群組。</span><span class="sxs-lookup"><span data-stu-id="f1103-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="f1103-122">**位置**： 指定 hello hello 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="f1103-122">**Location**: Specify hello location of hello resource group.</span></span> 
   * <span data-ttu-id="f1103-123">**ClusterName**： 輸入 hello HBase 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="f1103-123">**ClusterName**: Enter a name for hello HBase cluster.</span></span>
   * <span data-ttu-id="f1103-124">**叢集登入名稱和密碼**: hello 預設登入名稱是**admin**。</span><span class="sxs-lookup"><span data-stu-id="f1103-124">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="f1103-125">**SSH 使用者名稱和密碼**: hello 預設使用者名稱是**sshuser**。</span><span class="sxs-lookup"><span data-stu-id="f1103-125">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="f1103-126">您可以將它重新命名。</span><span class="sxs-lookup"><span data-stu-id="f1103-126">You can rename it.</span></span>
     
     <span data-ttu-id="f1103-127">其他參數都是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="f1103-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="f1103-128">每個叢集都具備 Azure 儲存體帳戶相依性。</span><span class="sxs-lookup"><span data-stu-id="f1103-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="f1103-129">刪除叢集之後，hello 資料會保留 hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="f1103-129">After you delete a cluster, hello data retains in hello storage account.</span></span> <span data-ttu-id="f1103-130">hello 叢集預設儲存體帳戶名稱是與 「 市集 」 附加 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f1103-130">hello cluster default storage account name is hello cluster name with "store" appended.</span></span> <span data-ttu-id="f1103-131">它是硬式編碼 hello 範本變數區段中。</span><span class="sxs-lookup"><span data-stu-id="f1103-131">It is hardcoded in hello template variables section.</span></span>
3. <span data-ttu-id="f1103-132">選取**toohello 條款和條件前面所述，即表示我同意**，然後按一下**購買**。</span><span class="sxs-lookup"><span data-stu-id="f1103-132">Select **I agree toohello terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="f1103-133">它會採用約 20 分鐘 toocreate 叢集。</span><span class="sxs-lookup"><span data-stu-id="f1103-133">It takes about 20 minutes toocreate a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="f1103-134">刪除 HBase 叢集之後，您可以使用 hello 來建立另一個 HBase 叢集相同的預設 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="f1103-134">After an HBase cluster is deleted, you can create another HBase cluster by using hello same default blob container.</span></span> <span data-ttu-id="f1103-135">hello 新叢集挑選您建立 hello 原始叢集中的 hello HBase 資料表。</span><span class="sxs-lookup"><span data-stu-id="f1103-135">hello new cluster picks up hello HBase tables you created in hello original cluster.</span></span> <span data-ttu-id="f1103-136">tooavoid 不一致，我們建議您刪除 hello 叢集之前，停用 hello HBase 資料表。</span><span class="sxs-lookup"><span data-stu-id="f1103-136">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="f1103-137">建立資料表和插入資料</span><span class="sxs-lookup"><span data-stu-id="f1103-137">Create tables and insert data</span></span>
<span data-ttu-id="f1103-138">您可以使用 SSH tooconnect tooHBase 叢集，然後使用 HBase 殼層 toocreate HBase 資料表插入資料及查詢資料。</span><span class="sxs-lookup"><span data-stu-id="f1103-138">You can use SSH tooconnect tooHBase clusters and then use HBase Shell toocreate HBase tables, insert data, and query data.</span></span> <span data-ttu-id="f1103-139">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="f1103-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="f1103-140">對大多數人來說，資料會出現在 hello 表格式格式：</span><span class="sxs-lookup"><span data-stu-id="f1103-140">For most people, data appears in hello tabular format:</span></span>

![HDInsight HBase 表格式資料][img-hbase-sample-data-tabular]

<span data-ttu-id="f1103-142">HBase （BigTable 的實作），在 hello 相同的資料如下所示：</span><span class="sxs-lookup"><span data-stu-id="f1103-142">In HBase (an implementation of BigTable), hello same data looks like:</span></span>

![HDInsight HBase BigTable 資料][img-hbase-sample-data-bigtable]


<span data-ttu-id="f1103-144">**toouse hello HBase 殼層**</span><span class="sxs-lookup"><span data-stu-id="f1103-144">**toouse hello HBase shell**</span></span>

1. <span data-ttu-id="f1103-145">Ssh，執行下列命令 HBase hello:</span><span class="sxs-lookup"><span data-stu-id="f1103-145">From SSH, run hello following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="f1103-146">使用兩個資料行系列建立 HBase：</span><span class="sxs-lookup"><span data-stu-id="f1103-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="f1103-147">插入一些資料：</span><span class="sxs-lookup"><span data-stu-id="f1103-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![HDInsight Hadoop HBase 殼層][img-hbase-shell]
4. <span data-ttu-id="f1103-149">取得單一資料列</span><span class="sxs-lookup"><span data-stu-id="f1103-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="f1103-150">您應該看到的 hello 相同的結果做為使用 hello 掃描命令，因為只有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="f1103-150">You shall see hello same results as using hello scan command because there is only one row.</span></span>
   
    <span data-ttu-id="f1103-151">如需 hello HBase 資料表的結構描述的詳細資訊，請參閱[簡介 tooHBase 結構描述設計][hbase-schema]。</span><span class="sxs-lookup"><span data-stu-id="f1103-151">For more information about hello HBase table schema, see [Introduction tooHBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="f1103-152">如需其他 HBase 命令，請參閱 [Apache HBase 參考指南][hbase-quick-start]。</span><span class="sxs-lookup"><span data-stu-id="f1103-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="f1103-153">結束 hello 殼層</span><span class="sxs-lookup"><span data-stu-id="f1103-153">Exit hello shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="f1103-154">**toobulk hello 連絡人 HBase 資料表將資料載入**</span><span class="sxs-lookup"><span data-stu-id="f1103-154">**toobulk load data into hello contacts HBase table**</span></span>

<span data-ttu-id="f1103-155">HBase 包含數個將資料載入資料表的方法。</span><span class="sxs-lookup"><span data-stu-id="f1103-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="f1103-156">如需詳細資訊，請參閱 [大量載入](http://hbase.apache.org/book.html#arch.bulk.load)。</span><span class="sxs-lookup"><span data-stu-id="f1103-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="f1103-157">您可以在公用 Blob 容器中找到資料檔案範例 (*wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*)。</span><span class="sxs-lookup"><span data-stu-id="f1103-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="f1103-158">hello hello 資料檔案內容為：</span><span class="sxs-lookup"><span data-stu-id="f1103-158">hello content of hello data file is:</span></span>

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

<span data-ttu-id="f1103-159">您可以選擇性地建立文字檔，並上傳 hello 檔案 tooyour 自己的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f1103-159">You can optionally create a text file and upload hello file tooyour own storage account.</span></span> <span data-ttu-id="f1103-160">Hello 指示，請參閱[HDInsight 中的 Hadoop 工作的資料上傳][hdinsight-upload-data]。</span><span class="sxs-lookup"><span data-stu-id="f1103-160">For hello instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="f1103-161">此程序會使用您已建立 hello 最後一個程序中的 hello 連絡人 HBase 資料表。</span><span class="sxs-lookup"><span data-stu-id="f1103-161">This procedure uses hello Contacts HBase table you have created in hello last procedure.</span></span>
> 

1. <span data-ttu-id="f1103-162">Ssh，執行下列命令 tootransform hello 資料檔案 tooStoreFiles，並儲存在 Dimporttsv.bulk.output 所指定的相對路徑的 hello。</span><span class="sxs-lookup"><span data-stu-id="f1103-162">From SSH, run hello following command tootransform hello data file tooStoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="f1103-163">如果您是在 HBase 殼層中，使用 hello 結束命令 tooexit。</span><span class="sxs-lookup"><span data-stu-id="f1103-163">If you are in HBase Shell, use hello exit command tooexit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="f1103-164">執行 hello /example/data/storeDataFileOutput toohello HBase 資料表中的下列命令 tooupload hello 資料：</span><span class="sxs-lookup"><span data-stu-id="f1103-164">Run hello following command tooupload hello data from  /example/data/storeDataFileOutput toohello HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="f1103-165">您可以開啟 hello HBase 殼層，並使用 hello 掃描命令 toolist hello 資料表內容。</span><span class="sxs-lookup"><span data-stu-id="f1103-165">You can open hello HBase shell, and use hello scan command toolist hello table content.</span></span>

## <a name="use-hive-tooquery-hbase"></a><span data-ttu-id="f1103-166">使用 Hive tooquery HBase</span><span class="sxs-lookup"><span data-stu-id="f1103-166">Use Hive tooquery HBase</span></span>

<span data-ttu-id="f1103-167">您可以使用 Hive 查詢 HBase 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="f1103-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="f1103-168">在本節中，您建立的 Hive 資料表的對應 toohello HBase 資料表，並使用它 tooquery hello 資料 HBase 資料表中。</span><span class="sxs-lookup"><span data-stu-id="f1103-168">In this section, you create a Hive table that maps toohello HBase table and uses it tooquery hello data in your HBase table.</span></span>

1. <span data-ttu-id="f1103-169">開啟**PuTTY**，並連接 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f1103-169">Open **PuTTY**, and connect toohello cluster.</span></span>  <span data-ttu-id="f1103-170">請參閱 hello hello 前程序中的指示。</span><span class="sxs-lookup"><span data-stu-id="f1103-170">See hello instructions in hello previous procedure.</span></span>
2. <span data-ttu-id="f1103-171">從 hello SSH 工作階段，使用下列命令 toostart Beeline hello:</span><span class="sxs-lookup"><span data-stu-id="f1103-171">From hello SSH session, use hello following command toostart Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="f1103-172">如需有關 Beeline 的詳細資訊，請參閱[利用 Beeline 搭配使用 Hive 與 HDInsight 中的 Hadoop](hdinsight-hadoop-use-hive-beeline.md)。</span><span class="sxs-lookup"><span data-stu-id="f1103-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="f1103-173">執行下列 HiveQL 指令碼 toocreate hello 對應 toohello HBase 資料表的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="f1103-173">Run hello following HiveQL script  toocreate a Hive table that maps toohello HBase table.</span></span> <span data-ttu-id="f1103-174">請確定您已建立使用 hello HBase 殼層，然後再執行此陳述式參考稍早在本教學課程中的 hello 範例資料表。</span><span class="sxs-lookup"><span data-stu-id="f1103-174">Make sure that you have created hello sample table referenced earlier in this tutorial by using hello HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="f1103-175">執行下列 HiveQL 指令碼 tooquery hello 資料 hello HBase 資料表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="f1103-175">Run hello following HiveQL script tooquery hello data in hello HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="f1103-176">使用 Curl 來使用 HBase REST API</span><span class="sxs-lookup"><span data-stu-id="f1103-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="f1103-177">hello REST API 會透過保護[基本驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)。</span><span class="sxs-lookup"><span data-stu-id="f1103-177">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="f1103-178">您永遠都應該使用安全 HTTP (HTTPS) toohelp 確保您的認證會安全地傳送 toohello 伺服器提出要求。</span><span class="sxs-lookup"><span data-stu-id="f1103-178">You shall always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>

2. <span data-ttu-id="f1103-179">使用下列命令 toolist hello 現有 HBase 資料表的 hello:</span><span class="sxs-lookup"><span data-stu-id="f1103-179">Use hello following command toolist hello existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="f1103-180">使用下列命令 toocreate 具有兩個資料行家族的新 HBase 資料表的 hello:</span><span class="sxs-lookup"><span data-stu-id="f1103-180">Use hello following command toocreate a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="f1103-181">hello 結構描述提供 hello JSon 格式。</span><span class="sxs-lookup"><span data-stu-id="f1103-181">hello schema is provided in hello JSon format.</span></span>
4. <span data-ttu-id="f1103-182">使用下列命令 tooinsert hello 某些資料：</span><span class="sxs-lookup"><span data-stu-id="f1103-182">Use hello following command tooinsert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="f1103-183">您必須 base64 編碼 hello hello-d 參數中指定的值。</span><span class="sxs-lookup"><span data-stu-id="f1103-183">You must base64 encode hello values specified in hello -d switch.</span></span> <span data-ttu-id="f1103-184">在 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="f1103-184">In hello example:</span></span>
   
   * <span data-ttu-id="f1103-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="f1103-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="f1103-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="f1103-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="f1103-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="f1103-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="f1103-188">[false-資料列索引鍵](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single)可讓您 tooinsert （批次） 的多個值。</span><span class="sxs-lookup"><span data-stu-id="f1103-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you tooinsert multiple (batched) values.</span></span>
5. <span data-ttu-id="f1103-189">使用下列命令 tooget 一個資料列的 hello:</span><span class="sxs-lookup"><span data-stu-id="f1103-189">Use hello following command tooget a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="f1103-190">如需 HBase Rest 的詳細資訊，請參閱 [Apache HBase 參考指南](https://hbase.apache.org/book.html#_rest)。</span><span class="sxs-lookup"><span data-stu-id="f1103-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="f1103-191">Thrift 不受 HDInsight 中的 HBase 所支援。</span><span class="sxs-lookup"><span data-stu-id="f1103-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="f1103-192">當使用 WebHCat Curl 或任何其他的 REST 通訊，您必須驗證 hello 要求藉由提供 hello 使用者名稱和 hello HDInsight 叢集系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="f1103-192">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="f1103-193">您也必須使用 hello 統一資源識別元 (URI) 的一部分使用 toosend hello 要求 toohello 伺服器 hello 叢集名稱：</span><span class="sxs-lookup"><span data-stu-id="f1103-193">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="f1103-194">您應該會收到回應類似 toohello 下列回應：</span><span class="sxs-lookup"><span data-stu-id="f1103-194">You should receive a response similar toohello following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="f1103-195">檢查叢集狀態</span><span class="sxs-lookup"><span data-stu-id="f1103-195">Check cluster status</span></span>
<span data-ttu-id="f1103-196">HDInsight 中的 HBase 隨附於 Web UI，以供監視叢集。</span><span class="sxs-lookup"><span data-stu-id="f1103-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="f1103-197">使用 hello Web UI，您可以要求統計資料或區域的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f1103-197">Using hello Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="f1103-198">**tooaccess hello HBase 主要 UI**</span><span class="sxs-lookup"><span data-stu-id="f1103-198">**tooaccess hello HBase Master UI**</span></span>

1. <span data-ttu-id="f1103-199">登入 hello https:// 在 hello Ambari Web UI&lt;Clustername >。.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="f1103-199">Sign into hello hello Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="f1103-200">按一下**HBase** hello 左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="f1103-200">Click **HBase** from hello left menu.</span></span>
3. <span data-ttu-id="f1103-201">按一下**快速連結**在 hello active 動物園管理員節點連結點 toohello，hello 頁面頂端，然後按一下 **HBase 主要 UI**。</span><span class="sxs-lookup"><span data-stu-id="f1103-201">Click **Quick links** on hello top of hello page, point toohello active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="f1103-202">在另一個瀏覽器索引標籤中開啟 hello UI:</span><span class="sxs-lookup"><span data-stu-id="f1103-202">hello UI is opened in another browser tab:</span></span>

  ![HDInsight HBase HMaster UI](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="f1103-204">hello HBase 主要 UI 包含下列各節的 hello:</span><span class="sxs-lookup"><span data-stu-id="f1103-204">hello HBase Master UI contains hello following sections:</span></span>

  - <span data-ttu-id="f1103-205">區域伺服器</span><span class="sxs-lookup"><span data-stu-id="f1103-205">region servers</span></span>
  - <span data-ttu-id="f1103-206">備份主機</span><span class="sxs-lookup"><span data-stu-id="f1103-206">backup masters</span></span>
  - <span data-ttu-id="f1103-207">tables</span><span class="sxs-lookup"><span data-stu-id="f1103-207">tables</span></span>
  - <span data-ttu-id="f1103-208">工作</span><span class="sxs-lookup"><span data-stu-id="f1103-208">tasks</span></span>
  - <span data-ttu-id="f1103-209">軟體屬性</span><span class="sxs-lookup"><span data-stu-id="f1103-209">software attributes</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="f1103-210">刪除 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="f1103-210">Delete hello cluster</span></span>
<span data-ttu-id="f1103-211">tooavoid 不一致，我們建議您刪除 hello 叢集之前，停用 hello HBase 資料表。</span><span class="sxs-lookup"><span data-stu-id="f1103-211">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="f1103-212">疑難排解</span><span class="sxs-lookup"><span data-stu-id="f1103-212">Troubleshoot</span></span>

<span data-ttu-id="f1103-213">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f1103-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1103-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1103-214">Next steps</span></span>
<span data-ttu-id="f1103-215">在本文中，您學會如何 toocreate HBase 叢集和 toocreate 資料表和檢視 hello 從這些資料表中的資料 hello HBase 殼層。</span><span class="sxs-lookup"><span data-stu-id="f1103-215">In this article, you learned how toocreate an HBase cluster and how toocreate tables and view hello data in those tables from hello HBase shell.</span></span> <span data-ttu-id="f1103-216">您也學到如何 toouse Hive HBase 資料表和如何 toouse hello toocreate HBase REST Api C# 中的資料 HBase 資料表的查詢，並從 hello 資料表擷取資料。</span><span class="sxs-lookup"><span data-stu-id="f1103-216">You also learned how toouse a Hive query on data in HBase tables and how toouse hello HBase C# REST APIs toocreate an HBase table and retrieve data from hello table.</span></span>

<span data-ttu-id="f1103-217">toolearn 詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f1103-217">toolearn more, see:</span></span>

* <span data-ttu-id="f1103-218">[HDInsight HBase 概觀][hdinsight-hbase-overview]：HBase 是建置於 Hadoop 上的 Apache 開放原始碼 NoSQL 資料庫，可針對大量非結構化及半結構化資料，提供隨機存取功能和強大一致性。</span><span class="sxs-lookup"><span data-stu-id="f1103-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png

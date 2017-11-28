---
title: "開始使用 HDInsight 上的 HBase 範例 - Azure | Microsoft Docs"
description: "遵循此 Apache HBase 範例開始在 HDInsight 上使用 Hadoop。 使用 Hive 從 HBase Shell 建立資料表並加以查詢。"
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
ms.openlocfilehash: bbd8a838062795ee03ae02dc5e3fd45d841a6e17
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="8c858-105">開始使用 HDInsight 中的 Apache HBase 範例</span><span class="sxs-lookup"><span data-stu-id="8c858-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="8c858-106">了解如何使用 Hive 在 HDInsight 中建立 HBase 叢集、建立 HBase 資料表，以及查詢資料表。</span><span class="sxs-lookup"><span data-stu-id="8c858-106">Learn how to create an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="8c858-107">如需一般 HBase 資訊，請參閱 [HDInsight HBase 概觀][hdinsight-hbase-overview]。</span><span class="sxs-lookup"><span data-stu-id="8c858-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="8c858-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="8c858-108">Prerequisites</span></span>
<span data-ttu-id="8c858-109">開始嘗試進行本 HBase 範例之前，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="8c858-109">Before you begin trying this HBase example, you must have the following items:</span></span>

* <span data-ttu-id="8c858-110">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8c858-110">**An Azure subscription**.</span></span> <span data-ttu-id="8c858-111">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="8c858-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="8c858-112">[安全殼層 (SSH)](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="8c858-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="8c858-113">[cURL](http://curl.haxx.se/download.html)。</span><span class="sxs-lookup"><span data-stu-id="8c858-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="8c858-114">建立 HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="8c858-114">Create HBase cluster</span></span>
<span data-ttu-id="8c858-115">下列程序會使用 Azure Resource Manager 範本建立 3.4 版以 Linux 為基礎的 HBase 叢集和相依的預設 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c858-115">The following procedure uses an Azure Resource Manager template to create a version 3.4 Linux-based HBase cluster and the dependent default Azure Storage account.</span></span> <span data-ttu-id="8c858-116">若要了解此程序與其他叢集建立方法中使用的參數，請參閱 [在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="8c858-116">To understand the parameters used in the procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="8c858-117">按一下以下影像，在 Azure 入口網站中開啟範本。</span><span class="sxs-lookup"><span data-stu-id="8c858-117">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="8c858-118">此範本位於公用 Blob 容器中。</span><span class="sxs-lookup"><span data-stu-id="8c858-118">The template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="8c858-119">從 [自訂部署] 刀鋒視窗，輸入下列值：</span><span class="sxs-lookup"><span data-stu-id="8c858-119">From the **Custom deployment** blade, enter the following values:</span></span>
   
   * <span data-ttu-id="8c858-120">**訂用帳戶**：選取用來建立叢集的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c858-120">**Subscription**: Select your Azure subscription that is used to create the cluster.</span></span>
   * <span data-ttu-id="8c858-121">**資源群組**：建立 Azure 資源管理群組，或選取現有的資源管理群組。</span><span class="sxs-lookup"><span data-stu-id="8c858-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="8c858-122">**位置**：指定資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="8c858-122">**Location**: Specify the location of the resource group.</span></span> 
   * <span data-ttu-id="8c858-123">**叢集名稱**：輸入 HBase 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="8c858-123">**ClusterName**: Enter a name for the HBase cluster.</span></span>
   * <span data-ttu-id="8c858-124">**叢集登入名稱和密碼**：預設登入名稱是 **admin**。</span><span class="sxs-lookup"><span data-stu-id="8c858-124">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="8c858-125">**SSH 使用者名稱和密碼**：預設使用者名稱是 **sshuser**。</span><span class="sxs-lookup"><span data-stu-id="8c858-125">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="8c858-126">您可以將它重新命名。</span><span class="sxs-lookup"><span data-stu-id="8c858-126">You can rename it.</span></span>
     
     <span data-ttu-id="8c858-127">其他參數都是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="8c858-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="8c858-128">每個叢集都具備 Azure 儲存體帳戶相依性。</span><span class="sxs-lookup"><span data-stu-id="8c858-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="8c858-129">刪除叢集之後，資料會保留在儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="8c858-129">After you delete a cluster, the data retains in the storage account.</span></span> <span data-ttu-id="8c858-130">叢集預設儲存體帳戶名稱是附加 "store" 的叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="8c858-130">The cluster default storage account name is the cluster name with "store" appended.</span></span> <span data-ttu-id="8c858-131">它會硬式編碼在範本變數區段中。</span><span class="sxs-lookup"><span data-stu-id="8c858-131">It is hardcoded in the template variables section.</span></span>
3. <span data-ttu-id="8c858-132">選取 [我同意上方所述的條款及條件]，然後按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="8c858-132">Select **I agree to the terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="8c858-133">大約需要 20 分鐘的時間來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="8c858-133">It takes about 20 minutes to create a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="8c858-134">刪除 HBase 叢集之後，您可以使用相同的預設 Blob 容器建立另一個 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="8c858-134">After an HBase cluster is deleted, you can create another HBase cluster by using the same default blob container.</span></span> <span data-ttu-id="8c858-135">這個新叢集會挑選您在原始叢集中建立的 HBase 資料表。</span><span class="sxs-lookup"><span data-stu-id="8c858-135">The new cluster picks up the HBase tables you created in the original cluster.</span></span> <span data-ttu-id="8c858-136">為了避免不一致，建議您在刪除叢集之前，先停用 HBase 資料表。</span><span class="sxs-lookup"><span data-stu-id="8c858-136">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="8c858-137">建立資料表和插入資料</span><span class="sxs-lookup"><span data-stu-id="8c858-137">Create tables and insert data</span></span>
<span data-ttu-id="8c858-138">您可以使用 SSH 來連線到 HBase 叢集，然後使用 HBase Shell 來建立 HBase 資料表、插入及查詢資料。</span><span class="sxs-lookup"><span data-stu-id="8c858-138">You can use SSH to connect to HBase clusters and then use HBase Shell to create HBase tables, insert data, and query data.</span></span> <span data-ttu-id="8c858-139">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="8c858-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="8c858-140">對大多數人而言，資料會以表格形式出現：</span><span class="sxs-lookup"><span data-stu-id="8c858-140">For most people, data appears in the tabular format:</span></span>

![HDInsight HBase 表格式資料][img-hbase-sample-data-tabular]

<span data-ttu-id="8c858-142">在 HBase (實作 BigTable) 中，相同的資料看起來如下：</span><span class="sxs-lookup"><span data-stu-id="8c858-142">In HBase (an implementation of BigTable), the same data looks like:</span></span>

![HDInsight HBase BigTable 資料][img-hbase-sample-data-bigtable]


<span data-ttu-id="8c858-144">**使用 HBase Shell**</span><span class="sxs-lookup"><span data-stu-id="8c858-144">**To use the HBase shell**</span></span>

1. <span data-ttu-id="8c858-145">從 SSH，執行下列 HBase 命令：</span><span class="sxs-lookup"><span data-stu-id="8c858-145">From SSH, run the following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="8c858-146">使用兩個資料行系列建立 HBase：</span><span class="sxs-lookup"><span data-stu-id="8c858-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="8c858-147">插入一些資料：</span><span class="sxs-lookup"><span data-stu-id="8c858-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![HDInsight Hadoop HBase 殼層][img-hbase-shell]
4. <span data-ttu-id="8c858-149">取得單一資料列</span><span class="sxs-lookup"><span data-stu-id="8c858-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="8c858-150">您會看到與使用掃描命令相同的結果，因為只有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="8c858-150">You shall see the same results as using the scan command because there is only one row.</span></span>
   
    <span data-ttu-id="8c858-151">如需 HBase 資料表結構描述的詳細資訊，請參閱 [HBase 結構描述設計簡介][hbase-schema]。</span><span class="sxs-lookup"><span data-stu-id="8c858-151">For more information about the HBase table schema, see [Introduction to HBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="8c858-152">如需其他 HBase 命令，請參閱 [Apache HBase 參考指南][hbase-quick-start]。</span><span class="sxs-lookup"><span data-stu-id="8c858-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="8c858-153">結束 Shell</span><span class="sxs-lookup"><span data-stu-id="8c858-153">Exit the shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="8c858-154">**將資料大量載入連絡人 HBase 資料表中**</span><span class="sxs-lookup"><span data-stu-id="8c858-154">**To bulk load data into the contacts HBase table**</span></span>

<span data-ttu-id="8c858-155">HBase 包含數個將資料載入資料表的方法。</span><span class="sxs-lookup"><span data-stu-id="8c858-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="8c858-156">如需詳細資訊，請參閱 [大量載入](http://hbase.apache.org/book.html#arch.bulk.load)。</span><span class="sxs-lookup"><span data-stu-id="8c858-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="8c858-157">您可以在公用 Blob 容器中找到資料檔案範例 (*wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*)。</span><span class="sxs-lookup"><span data-stu-id="8c858-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="8c858-158">資料檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="8c858-158">The content of the data file is:</span></span>

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

<span data-ttu-id="8c858-159">您可以選擇性地建立文字檔，並將檔案上載至自己的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c858-159">You can optionally create a text file and upload the file to your own storage account.</span></span> <span data-ttu-id="8c858-160">如需指示，請參閱[在 HDInsight 中將 Hadoop 工作的資料上傳][hdinsight-upload-data]。</span><span class="sxs-lookup"><span data-stu-id="8c858-160">For the instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="8c858-161">此程序會使用您在上一個程序中建立的連絡人 HBase 資料表。</span><span class="sxs-lookup"><span data-stu-id="8c858-161">This procedure uses the Contacts HBase table you have created in the last procedure.</span></span>
> 

1. <span data-ttu-id="8c858-162">從 SSH，執行下列命令，將資料檔案轉換成 StoreFiles 並存放在 Dimporttsv.bulk.output 所指定的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="8c858-162">From SSH, run the following command to transform the data file to StoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="8c858-163">如果您在 HBase Shell 中，請使用 exit 命令來結束。</span><span class="sxs-lookup"><span data-stu-id="8c858-163">If you are in HBase Shell, use the exit command to exit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="8c858-164">執行下列命令，將資料從 /example/data/storeDataFileOutput 上傳至 HBase 資料表：</span><span class="sxs-lookup"><span data-stu-id="8c858-164">Run the following command to upload the data from  /example/data/storeDataFileOutput to the HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="8c858-165">您可以開啟 HBase Shell，並使用掃描命令來列出資料表內容。</span><span class="sxs-lookup"><span data-stu-id="8c858-165">You can open the HBase shell, and use the scan command to list the table content.</span></span>

## <a name="use-hive-to-query-hbase"></a><span data-ttu-id="8c858-166">使用 Hive 查詢 HBase</span><span class="sxs-lookup"><span data-stu-id="8c858-166">Use Hive to query HBase</span></span>

<span data-ttu-id="8c858-167">您可以使用 Hive 查詢 HBase 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="8c858-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="8c858-168">在本節中，您會建立對應至 HBase 資料表的 Hive 資料表，並用以查詢您 HBase 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="8c858-168">In this section, you create a Hive table that maps to the HBase table and uses it to query the data in your HBase table.</span></span>

1. <span data-ttu-id="8c858-169">開啟 **PuTTY**，然後連線到叢集。</span><span class="sxs-lookup"><span data-stu-id="8c858-169">Open **PuTTY**, and connect to the cluster.</span></span>  <span data-ttu-id="8c858-170">請參閱先前程序中的指示。</span><span class="sxs-lookup"><span data-stu-id="8c858-170">See the instructions in the previous procedure.</span></span>
2. <span data-ttu-id="8c858-171">在 SSH 工作階段中，使用以下命令啟動 Beeline：</span><span class="sxs-lookup"><span data-stu-id="8c858-171">From the SSH session, use the following command to start Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="8c858-172">如需有關 Beeline 的詳細資訊，請參閱[利用 Beeline 搭配使用 Hive 與 HDInsight 中的 Hadoop](hdinsight-hadoop-use-hive-beeline.md)。</span><span class="sxs-lookup"><span data-stu-id="8c858-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="8c858-173">執行下列 HiveQL 指令碼以建立對應到 HBase 資料表的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="8c858-173">Run the following HiveQL script  to create a Hive table that maps to the HBase table.</span></span> <span data-ttu-id="8c858-174">在執行此陳述式前，請確定您已使用 HBase Shell 建立參考先前本教學課程的範例資料表。</span><span class="sxs-lookup"><span data-stu-id="8c858-174">Make sure that you have created the sample table referenced earlier in this tutorial by using the HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="8c858-175">執行下列 HiveQL 指令碼，以查詢 HBase 資料表中的資料：</span><span class="sxs-lookup"><span data-stu-id="8c858-175">Run the following HiveQL script to query the data in the HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="8c858-176">使用 Curl 來使用 HBase REST API</span><span class="sxs-lookup"><span data-stu-id="8c858-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="8c858-177">透過 [基本驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)來保護 REST API 的安全。</span><span class="sxs-lookup"><span data-stu-id="8c858-177">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="8c858-178">您應該一律使用安全 HTTP (HTTPS) 提出要求，確保認證安全地傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c858-178">You shall always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>

2. <span data-ttu-id="8c858-179">使用下列命令列出現有的 HBase 資料表：</span><span class="sxs-lookup"><span data-stu-id="8c858-179">Use the following command to list the existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="8c858-180">使用下列命令建立含兩個資料欄系列的新 HBase 資料表：</span><span class="sxs-lookup"><span data-stu-id="8c858-180">Use the following command to create a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="8c858-181">結構描述是以 JSON 格式提供。</span><span class="sxs-lookup"><span data-stu-id="8c858-181">The schema is provided in the JSon format.</span></span>
4. <span data-ttu-id="8c858-182">使用下列命令插入一些資料：</span><span class="sxs-lookup"><span data-stu-id="8c858-182">Use the following command to insert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="8c858-183">您必須使用 base64 編碼 -d 參數中指定的值。</span><span class="sxs-lookup"><span data-stu-id="8c858-183">You must base64 encode the values specified in the -d switch.</span></span> <span data-ttu-id="8c858-184">在範例中︰</span><span class="sxs-lookup"><span data-stu-id="8c858-184">In the example:</span></span>
   
   * <span data-ttu-id="8c858-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="8c858-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="8c858-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="8c858-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="8c858-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="8c858-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="8c858-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) 可讓您插入多個 (批次) 值。</span><span class="sxs-lookup"><span data-stu-id="8c858-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you to insert multiple (batched) values.</span></span>
5. <span data-ttu-id="8c858-189">使用下列命令取得資料列：</span><span class="sxs-lookup"><span data-stu-id="8c858-189">Use the following command to get a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="8c858-190">如需 HBase Rest 的詳細資訊，請參閱 [Apache HBase 參考指南](https://hbase.apache.org/book.html#_rest)。</span><span class="sxs-lookup"><span data-stu-id="8c858-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="8c858-191">Thrift 不受 HDInsight 中的 HBase 所支援。</span><span class="sxs-lookup"><span data-stu-id="8c858-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="8c858-192">在使用 Curl 或與 WebHCat 進行任何其他 REST 通訊時，您必須提供 HDInsight 叢集系統管理員的使用者名稱和密碼來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="8c858-192">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="8c858-193">您也必須在用來將要求傳送至伺服器的統一資源識別項 (URI) 中使用叢集名稱：</span><span class="sxs-lookup"><span data-stu-id="8c858-193">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="8c858-194">您應該會收到類似下列的回應：</span><span class="sxs-lookup"><span data-stu-id="8c858-194">You should receive a response similar to the following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="8c858-195">檢查叢集狀態</span><span class="sxs-lookup"><span data-stu-id="8c858-195">Check cluster status</span></span>
<span data-ttu-id="8c858-196">HDInsight 中的 HBase 隨附於 Web UI，以供監視叢集。</span><span class="sxs-lookup"><span data-stu-id="8c858-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="8c858-197">使用 Web UI，您可要求關於區域的統計資料或資訊。</span><span class="sxs-lookup"><span data-stu-id="8c858-197">Using the Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="8c858-198">**存取 HBase 主要 UI**</span><span class="sxs-lookup"><span data-stu-id="8c858-198">**To access the HBase Master UI**</span></span>

1. <span data-ttu-id="8c858-199">登入 Ambari Web UI (https://&lt;Clustername>.azurehdinsight.net)。</span><span class="sxs-lookup"><span data-stu-id="8c858-199">Sign into the the Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="8c858-200">按一下左側功能表的 [HBase]。</span><span class="sxs-lookup"><span data-stu-id="8c858-200">Click **HBase** from the left menu.</span></span>
3. <span data-ttu-id="8c858-201">按一下頁面頂端的 [快速連結]，指向使用中的 Zookeeper 節點連結，然後按一下 [HBase 主要 UI]。</span><span class="sxs-lookup"><span data-stu-id="8c858-201">Click **Quick links** on the top of the page, point to the active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="8c858-202">UI 會在另一個瀏覽器索引標籤中開啟：</span><span class="sxs-lookup"><span data-stu-id="8c858-202">The UI is opened in another browser tab:</span></span>

  ![HDInsight HBase HMaster UI](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="8c858-204">HBase 主要 UI 包含下列區段：</span><span class="sxs-lookup"><span data-stu-id="8c858-204">The HBase Master UI contains the following sections:</span></span>

  - <span data-ttu-id="8c858-205">區域伺服器</span><span class="sxs-lookup"><span data-stu-id="8c858-205">region servers</span></span>
  - <span data-ttu-id="8c858-206">備份主機</span><span class="sxs-lookup"><span data-stu-id="8c858-206">backup masters</span></span>
  - <span data-ttu-id="8c858-207">tables</span><span class="sxs-lookup"><span data-stu-id="8c858-207">tables</span></span>
  - <span data-ttu-id="8c858-208">工作</span><span class="sxs-lookup"><span data-stu-id="8c858-208">tasks</span></span>
  - <span data-ttu-id="8c858-209">軟體屬性</span><span class="sxs-lookup"><span data-stu-id="8c858-209">software attributes</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="8c858-210">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="8c858-210">Delete the cluster</span></span>
<span data-ttu-id="8c858-211">為了避免不一致，建議您在刪除叢集之前，先停用 HBase 資料表。</span><span class="sxs-lookup"><span data-stu-id="8c858-211">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="8c858-212">疑難排解</span><span class="sxs-lookup"><span data-stu-id="8c858-212">Troubleshoot</span></span>

<span data-ttu-id="8c858-213">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="8c858-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c858-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c858-214">Next steps</span></span>
<span data-ttu-id="8c858-215">在本文中，您已了解如何建立 HBase 叢集，以及如何建立資料表，並從 HBase Shell 檢視這些資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="8c858-215">In this article, you learned how to create an HBase cluster and how to create tables and view the data in those tables from the HBase shell.</span></span> <span data-ttu-id="8c858-216">您同時也了解到如何使用 Hive 查詢 HBase 資料表中的資料，以及如何使用 HBase C# REST API 建立 HBase 資料表，並擷取其資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="8c858-216">You also learned how to use a Hive query on data in HBase tables and how to use the HBase C# REST APIs to create an HBase table and retrieve data from the table.</span></span>

<span data-ttu-id="8c858-217">若要深入了解，請參閱：</span><span class="sxs-lookup"><span data-stu-id="8c858-217">To learn more, see:</span></span>

* <span data-ttu-id="8c858-218">[HDInsight HBase 概觀][hdinsight-hbase-overview]：HBase 是建置於 Hadoop 上的 Apache 開放原始碼 NoSQL 資料庫，可針對大量非結構化及半結構化資料，提供隨機存取功能和強大一致性。</span><span class="sxs-lookup"><span data-stu-id="8c858-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

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

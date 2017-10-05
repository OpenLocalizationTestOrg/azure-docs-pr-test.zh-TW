---
title: "建立 Hive 資料表，並從 Azure Blob 儲存體載入資料 | Microsoft Docs"
description: "建立 Hive 資料表，並將 Blob 中的資料載入 Hive 資料表"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: eca4ecd8f639bb9816903f4b1d1f999755da819c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="5a0d5-103">建立 Hive 資料表，並從 Azure Blob 儲存體載入資料</span><span class="sxs-lookup"><span data-stu-id="5a0d5-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="5a0d5-104">本主題會顯示泛型 Hive 查詢，這類查詢可建立 Hive 資料表，並從 Azure Blob 儲存體載入資料。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="5a0d5-105">同時也會提供一些關於資料分割 Hive 資料表，以及使用最佳化單欄式資料列 (ORC) 格式來提升查詢效能的指引。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-105">Some guidance is also provided on partitioning Hive tables and on using the Optimized Row Columnar (ORC) formatting to improve query performance.</span></span>

<span data-ttu-id="5a0d5-106">此 **功能表** 所連結的主題會說明如何將資料內嵌至目標環境，以在 Team Data Science Process (TDSP) 期間儲存和處理該資料。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-106">This **menu** links to topics that describe how to ingest data into target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="5a0d5-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="5a0d5-107">Prerequisites</span></span>
<span data-ttu-id="5a0d5-108">本文假設您已經：</span><span class="sxs-lookup"><span data-stu-id="5a0d5-108">This article assumes that you have:</span></span>

* <span data-ttu-id="5a0d5-109">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-109">Created an Azure storage account.</span></span> <span data-ttu-id="5a0d5-110">如需相關指示，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="5a0d5-111">佈建含有 HDInsight 服務的自訂 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-111">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="5a0d5-112">如需指示，請參閱 [自訂適用於進階分析的 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="5a0d5-113">啟用叢集的遠端存取、登入，然後開啟 Hadoop 命令列主控台。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-113">Enabled remote access to the cluster, logged in, and opened the Hadoop Command-Line console.</span></span> <span data-ttu-id="5a0d5-114">如需指示，請參閱 [存取 Hadoop 叢集的前端節點](machine-learning-data-science-customize-hadoop-cluster.md#headnode)。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-114">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="5a0d5-115">將資料上傳至 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="5a0d5-115">Upload data to Azure blob storage</span></span>
<span data-ttu-id="5a0d5-116">如果您遵循[設定適用於進階分析的 Azure 虛擬機器](machine-learning-data-science-setup-virtual-machine.md)中所提供的指示建立了 Azure 虛擬機器，應該已將這個指令碼檔案下載至虛擬機器上的 C:\\Users\\\<使用者名稱\>\\Documents\\Data Science Scripts 目錄中。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-116">If you created an Azure virtual machine by following the instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded to the *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on the virtual machine.</span></span> <span data-ttu-id="5a0d5-117">這些 Hive 查詢只要求您插入自己的資料結構描述，以及已準備好進行提交之適當欄位中的 Azure Blob 儲存體設定。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in the appropriate fields to be ready for submission.</span></span>

<span data-ttu-id="5a0d5-118">我們假設 Hive 資料表的資料為 **未壓縮的** 表格格式，而且資料已上傳至 Hadoop 叢集所使用之儲存體帳戶的預設 (或其他) 容器。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-118">We assume that the data for Hive tables is in an **uncompressed** tabular format, and that the data has been uploaded to the default (or to an additional) container of the storage account used by the Hadoop cluster.</span></span>

<span data-ttu-id="5a0d5-119">如果您想要使用 **NYC 計程車車程資料**進行練習，您需要︰</span><span class="sxs-lookup"><span data-stu-id="5a0d5-119">If you want to practice on the **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="5a0d5-120">**下載** 24 個 [NYC 計程車車程資料](http://www.andresmh.com/nyctaxitrips) 檔案 (12 個車程檔案和 12 個費用檔案)，</span><span class="sxs-lookup"><span data-stu-id="5a0d5-120">**download** the 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="5a0d5-121">**解壓縮** 為 .csv 檔案，然後</span><span class="sxs-lookup"><span data-stu-id="5a0d5-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="5a0d5-122">**上傳** 檔案到 [針對進階分析程序和技術自訂 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md) 主題所述之程序所建立的 Azure 儲存體帳戶預設值 (或適當容器)。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-122">**upload** them to the default (or appropriate container) of the Azure storage account that was created by the procedure outlined in the [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="5a0d5-123">請參閱此 [頁面](machine-learning-data-science-process-hive-walkthrough.md#upload)，以了解將 .csv 檔案上傳至儲存體帳戶上之預設容器的程序。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-123">The process to upload the .csv files to the default container on the storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="5a0d5-124"><a name="submit"></a>如何提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="5a0d5-124"><a name="submit"></a>How to submit Hive queries</span></span>
<span data-ttu-id="5a0d5-125">您可以使用下列方法來提交 Hive 查詢：</span><span class="sxs-lookup"><span data-stu-id="5a0d5-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="5a0d5-126">透過 Hadoop 叢集前端節點中的 Hadoop 命令列提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="5a0d5-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="5a0d5-127">利用 Hive 編輯器提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="5a0d5-127">Submit Hive queries with the Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="5a0d5-128">利用 Azure PowerShell 命令提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="5a0d5-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="5a0d5-129">Hive 查詢類似 SQL。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="5a0d5-130">如果您熟悉 SQL，您可能會發現 [Hive for SQL 使用者功能提要](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) 很有用。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-130">If you are familiar with SQL, you may find the [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="5a0d5-131">提交 Hive 查詢時，您也可以控制 Hive 查詢輸出的目的地，它是否會出現在螢幕上，或是輸出到前端節點上的本機檔案或 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-131">When submitting a Hive query, you can also control the destination of the output from Hive queries, whether it be on the screen or to a local file on the head node or to an Azure blob.</span></span>

### <span data-ttu-id="5a0d5-132"><a name="headnode"></a> 1.透過 Hadoop 叢集前端節點中的 Hadoop 命令列提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="5a0d5-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="5a0d5-133">如果 Hive 查詢相當複雜，在 Hadoop 叢集的前端節點中直接提交 Hive 查詢，通常會導致整備速度比使用 Hive 編輯器或 Azure PowerShell 指令碼進行提交還快。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-133">If the Hive query is complex, submitting it directly in the head node of the Hadoop cluster typically leads to faster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="5a0d5-134">登入 Hadoop 叢集的前端節點、在前端節點的桌面上開啟 Hadoop 命令列，然後輸入命令 `cd %hive_home%\bin`。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-134">Log in to the head node of the Hadoop cluster, open the Hadoop Command Line on the desktop of the head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="5a0d5-135">您有三種方式可在 Hadoop 命令列中提交 Hive 查詢：</span><span class="sxs-lookup"><span data-stu-id="5a0d5-135">You have three ways to submit Hive queries in the Hadoop Command Line:</span></span>

* <span data-ttu-id="5a0d5-136">直接</span><span class="sxs-lookup"><span data-stu-id="5a0d5-136">directly</span></span>
* <span data-ttu-id="5a0d5-137">使用 .hql 檔案</span><span class="sxs-lookup"><span data-stu-id="5a0d5-137">using .hql files</span></span>
* <span data-ttu-id="5a0d5-138">利用 Hive 命令主控台</span><span class="sxs-lookup"><span data-stu-id="5a0d5-138">with the Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="5a0d5-139">在 Hadoop 命令列中直接提交 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="5a0d5-140">您可以執行類似 `hive -e "<your hive query>;` 的命令，在 Hadoop 命令列中直接提交簡單的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-140">You can run command like `hive -e "<your hive query>;` to submit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="5a0d5-141">在下列範例中，紅色方塊框起來的是提交 Hive 查詢的命令，而綠色方塊框起來的則是 Hive 查詢的輸出。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-141">Here is an example, where the red box outlines the command that submits the Hive query, and the green box outlines the output from the Hive query.</span></span>

![建立工作區](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="5a0d5-143">提交 .hql 檔案中的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="5a0d5-144">若 Hive 查詢更複雜且有多行，則在命令列或 Hive 命令主控台中編輯查詢並不實際。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-144">When the Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="5a0d5-145">替代方法是在 Hadoop 叢集的前端節點中使用文字編輯器，將 Hive 查詢儲存於前端節點本機目錄上的 .hql 檔案中。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-145">An alternative is to use a text editor in the head node of the Hadoop cluster to save the Hive queries in a .hql file in a local directory of the head node.</span></span> <span data-ttu-id="5a0d5-146">然後可以使用 `-f` 引數提交 .hql 檔案中的 Hive 查詢，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5a0d5-146">Then the Hive query in the .hql file can be submitted by using the `-f` argument as follows:</span></span>

    hive -f "<path to the .hql file>"

![建立工作區](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="5a0d5-148">**隱藏 Hive 查詢的進度狀態畫面顯示**</span><span class="sxs-lookup"><span data-stu-id="5a0d5-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="5a0d5-149">根據預設，在 Hadoop 命令列中提交 Hive 查詢之後，Map/Reduce 作業的進度會顯示於螢幕上。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-149">By default, after Hive query is submitted in Hadoop Command Line, the progress of the Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="5a0d5-150">若要隱藏 Map/Reduce 工作進度的畫面顯示，您可以在命令列中使用引數 `-S` (大寫的 "S")，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5a0d5-150">To suppress the screen print of the Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in the command line as follows:</span></span>

    hive -S -f "<path to the .hql file>"
<span data-ttu-id="5a0d5-151">。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-151">.</span></span>    <span data-ttu-id="5a0d5-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="5a0d5-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="5a0d5-153">在 Hive 命令主控台中提交 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="5a0d5-154">您也可以在 Hadoop 命令列中執行 `hive` 命令，先進入 Hive 命令主控台，然後在 Hive 命令主控台中提交 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-154">You can also first enter the Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="5a0d5-155">範例如下。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-155">Here is an example.</span></span> <span data-ttu-id="5a0d5-156">在此範例中，這兩個紅色方塊反白顯示的命令分別是用來進入 Hive 命令主控台，以及在 Hive 命令主控台中提交 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-156">In this example, the two red boxes highlight the commands used to enter the Hive command console, and the Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="5a0d5-157">綠色方塊反白顯示的是 Hive 查詢的輸出。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-157">The green box highlights the output from the Hive query.</span></span>

![建立工作區](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="5a0d5-159">上述範例會在螢幕上直接輸出 Hive 查詢結果。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-159">The previous examples directly output the Hive query results on screen.</span></span> <span data-ttu-id="5a0d5-160">您也可以將輸出寫入前端節點上的本機檔案，或寫入 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-160">You can also write the output to a local file on the head node, or to an Azure blob.</span></span> <span data-ttu-id="5a0d5-161">接著，您可以使用其他工具，進一步分析 Hive 查詢的輸出。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-161">Then, you can use other tools to further analyze the output of Hive queries.</span></span>

<span data-ttu-id="5a0d5-162">**將 Hive 查詢結果輸出到本機檔案。**</span><span class="sxs-lookup"><span data-stu-id="5a0d5-162">**Output Hive query results to a local file.**</span></span>
<span data-ttu-id="5a0d5-163">若要將 Hive 查詢結果輸出到前端節點上的本機目錄，您必須在 Hadoop 命令列中提交 Hive 查詢，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5a0d5-163">To output Hive query results to a local directory on the head node, you have to submit the Hive query in the Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in the head node>

<span data-ttu-id="5a0d5-164">在下列範例中，Hive 查詢的輸出會寫入 `C:\apps\temp` 目錄中的 `hivequeryoutput.txt` 檔案。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-164">In the following example, the output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![建立工作區](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="5a0d5-166">**將 Hive 查詢結果輸出到 Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="5a0d5-166">**Output Hive query results to an Azure blob**</span></span>

<span data-ttu-id="5a0d5-167">您也可以將 Hive 查詢結果輸出到 Hadoop 叢集預設容器內的 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-167">You can also output the Hive query results to an Azure blob, within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="5a0d5-168">此作業的 Hive 查詢如下所示：</span><span class="sxs-lookup"><span data-stu-id="5a0d5-168">The Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within the default container> <select clause from ...>

<span data-ttu-id="5a0d5-169">在下列範例中，Hive 查詢的輸出會寫入 Hadoop 叢集預設容器內的 Blob 目錄 `queryoutputdir` 。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-169">In the following example, the output of Hive query is written to a blob directory `queryoutputdir` within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="5a0d5-170">在此處，您只需提供目錄名稱，而不需提供 Blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-170">Here, you only need to provide the directory name, without the blob name.</span></span> <span data-ttu-id="5a0d5-171">如果您同時提供目錄和 Blob 名稱 (例如 `wasb:///queryoutputdir/queryoutput.txt`)，則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![建立工作區](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="5a0d5-173">如果您使用 Azure 儲存體總管開啟 Hadoop 叢集的預設容器，則可以看到如下圖所示的 Hive 查詢輸出。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-173">If you open the default container of the Hadoop cluster using Azure Storage Explorer, you can see the output of the Hive query as shown in the following figure.</span></span> <span data-ttu-id="5a0d5-174">您可以套用篩選條件 (以紅色方塊反白顯示)，只擷取名稱中具有指定字母的 Blob。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-174">You can apply the filter (highlighted by red box) to only retrieve the blob with specified letters in names.</span></span>

![建立工作區](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="5a0d5-176"><a name="hive-editor"></a> 2.利用 Hive 編輯器提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="5a0d5-176"><a name="hive-editor"></a> 2. Submit Hive queries with the Hive Editor</span></span>
<span data-ttu-id="5a0d5-177">您也可以在網頁瀏覽器中輸入https://&#60;Hadoop 叢集名稱>.azurehdinsight.net/Home/HiveEditor 格式的 URL，以使用查詢主控台 (Hive 編輯器)。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-177">You can also use the Query Console (Hive Editor) by entering a URL of the form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="5a0d5-178">您必須登入才能看到此主控台，因此您在這裡需要 Hadoop 叢集認證。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-178">You must be logged in the see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="5a0d5-179"><a name="ps"></a> 3.利用 Azure PowerShell 命令提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="5a0d5-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="5a0d5-180">您也可以使用 PowerShell 提交 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-180">You can also use PowerShell to submit Hive queries.</span></span> <span data-ttu-id="5a0d5-181">如需指示，請參閱 [使用 PowerShell 提交 Hive 工作](../hdinsight/hdinsight-hadoop-use-hive-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="5a0d5-182"><a name="create-tables"></a>建立 Hive 資料庫和資料表</span><span class="sxs-lookup"><span data-stu-id="5a0d5-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="5a0d5-183">Hive 查詢會在 [GitHub 存放庫](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql)中共用，並且可從該處下載。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-183">The Hive queries are shared in the [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="5a0d5-184">以下是建立 Hive 資料表的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-184">Here is the Hive query that creates a Hive table.</span></span>

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

<span data-ttu-id="5a0d5-185">以下是您需要插入的欄位和其他設定的說明：</span><span class="sxs-lookup"><span data-stu-id="5a0d5-185">Here are the descriptions of the fields that you need to plug in and other configurations:</span></span>

* <span data-ttu-id="5a0d5-186">**&#60;資料庫名稱>**：您要建立之資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-186">**&#60;database name>**: the name of the database that you want to create.</span></span> <span data-ttu-id="5a0d5-187">如果您只想要使用預設資料庫，則可省略「create database...」  查詢。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-187">If you just want to use the default database, the query *create database...* can be omitted.</span></span>
* <span data-ttu-id="5a0d5-188">**&#60;資料表名稱>**：您想要在指定資料庫內建立之資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-188">**&#60;table name>**: the name of the table that you want to create within the specified database.</span></span> <span data-ttu-id="5a0d5-189">如果您想要使用預設資料庫，可透過 &#60;資料表名稱> 直接參考資料表，而不需要使用 &#60;資料庫名稱>。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-189">If you want to use the default database, the table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="5a0d5-190">**&#60;欄位分隔符號>**：上傳至 Hive 資料表的資料檔中分隔欄位的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-190">**&#60;field separator>**: the separator that delimits fields in the data file to be uploaded to the Hive table.</span></span>
* <span data-ttu-id="5a0d5-191">**&#60;資料行分隔符號>**：用來分隔資料檔中各行的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-191">**&#60;line separator>**: the separator that delimits lines in the data file.</span></span>
* <span data-ttu-id="5a0d5-192">**&#60;儲存體位置>**：用來儲存 Hive 資料表資料的 Azure 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-192">**&#60;storage location>**: the Azure storage location to save the data of Hive tables.</span></span> <span data-ttu-id="5a0d5-193">如果您未指定 LOCATION &#60;儲存體位置>，資料庫和資料表預設會儲存在 Hive 叢集之預設容器的 hive/warehouse/ 目錄中。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-193">If you do not specify *LOCATION &#60;storage location>*, the database and the tables are stored in *hive/warehouse/* directory in the default container of the Hive cluster by default.</span></span> <span data-ttu-id="5a0d5-194">如果您想要指定儲存體位置，儲存體位置必須位於資料庫和資料表的預設容器內。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-194">If you want to specify the storage location, the storage location has to be within the default container for the database and tables.</span></span> <span data-ttu-id="5a0d5-195">這個位置必須是叢集之預設容器的相對位置，其格式為 'wasb:///&#60;directory 1>/' 或 'wasb:///&#60;directory 1>/&#60;directory 2>/' 等。執行查詢之後，系統會在預設容器內建立相對目錄。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-195">This location has to be referred as location relative to the default container of the cluster in the format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After the query is executed, the relative directories are created within the default container.</span></span>
* <span data-ttu-id="5a0d5-196">**TBLPROPERTIES("skip.header.line.count"="1")**：如果資料檔有標頭行，您就必須在 create table 查詢的**結尾**處新增這個屬性。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If the data file has a header line, you have to add this property **at the end** of the *create table* query.</span></span> <span data-ttu-id="5a0d5-197">否則，載入的標頭行會做為資料表的記錄。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-197">Otherwise, the header line is loaded as a record to the table.</span></span> <span data-ttu-id="5a0d5-198">如果資料檔不含標頭行，則可在查詢中省略此設定。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-198">If the data file does not have a header line, this configuration can be omitted in the query.</span></span>

## <span data-ttu-id="5a0d5-199"><a name="load-data"></a>將資料載入至 Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="5a0d5-199"><a name="load-data"></a>Load data to Hive tables</span></span>
<span data-ttu-id="5a0d5-200">以下是將資料載入 Hive 資料表的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-200">Here is the Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path to blob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="5a0d5-201">**&#60;Blob 資料路徑>**：如果要上傳至 Hive 資料表的 Blob 檔案是在 HDInsight Hadoop 叢集的預設容器中，則 &#60;Blob 資料路徑> 的格式應該是 'wasb:///&#60;此容器中的目錄>/&#60;Blob 檔案名稱>'。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-201">**&#60;path to blob data>**: If the blob file to be uploaded to the Hive table is in the default container of the HDInsight Hadoop cluster, the *&#60;path to blob data>* should be in the format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="5a0d5-202">Blob 檔案也可以位於 HDInsight Hadoop 叢集的其他容器中。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-202">The blob file can also be in an additional container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="5a0d5-203">在此情況下， *&#60;blob 資料路徑>* 的格式應該是 *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-203">In this case, *&#60;path to blob data>* should be in the format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5a0d5-204">上傳至 Hive 資料表的 Blob 資料必須位於 Hadoop 叢集儲存體帳戶的預設或其他容器中。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-204">The blob data to be uploaded to Hive table has to be in the default or additional container of the storage account for the Hadoop cluster.</span></span> <span data-ttu-id="5a0d5-205">否則，「LOAD DATA」  查詢會失敗並提報它無法存取資料。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-205">Otherwise, the *LOAD DATA* query fails complaining that it cannot access the data.</span></span>
  >
  >

## <span data-ttu-id="5a0d5-206"><a name="partition-orc"></a>進階主題：資料分割資料表及使用 ORC 格式儲存 Hive 資料</span><span class="sxs-lookup"><span data-stu-id="5a0d5-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="5a0d5-207">如果資料量很大，對於只需掃描資料表中數個資料分割的查詢而言，分割資料表就很有助益。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-207">If the data is large, partitioning the table is beneficial for queries that only need to scan a few partitions of the table.</span></span> <span data-ttu-id="5a0d5-208">例如，依日期分割網站的記錄資料就很合理。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-208">For instance, it is reasonable to partition the log data of a web site by dates.</span></span>

<span data-ttu-id="5a0d5-209">除了資料分割 Hive 資料表之外，對於使用最佳化單欄式資料列 (ORC) 格式來儲存 Hive 資料也很有幫助。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-209">In addition to partitioning Hive tables, it is also beneficial to store the Hive data in the Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="5a0d5-210">如需 ORC 格式的詳細資訊，請參閱<a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">在 Hive 讀取、寫入及處理資料時使用 ORC 檔案提升效能</a>。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="5a0d5-211">資料分割資料表</span><span class="sxs-lookup"><span data-stu-id="5a0d5-211">Partitioned table</span></span>
<span data-ttu-id="5a0d5-212">以下是建立資料分割資料表和並將資料載入其中的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-212">Here is the Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="5a0d5-213">查詢資料分割資料表時，建議在** 子句的**開頭`where`新增資料分割條件，這樣就能大幅提升搜尋效率。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-213">When querying partitioned tables, it is recommended to add the partition condition in the **beginning** of the `where` clause as this improves the efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="5a0d5-214"><a name="orc"></a>使用 ORC 格式儲存 Hive 資料</span><span class="sxs-lookup"><span data-stu-id="5a0d5-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="5a0d5-215">您無法將資料從 Blob 儲存體直接載入以 ORC 格式儲存的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-215">You cannot directly load data from blob storage into Hive tables that is stored in the ORC format.</span></span> <span data-ttu-id="5a0d5-216">以下是您為了將資料從 Azure Blob 載入到以 ORC 格式儲存的 Hive 資料表所需採取的步驟。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-216">Here are the steps that the you need to take to load data from Azure blobs to Hive tables stored in ORC format.</span></span>

<span data-ttu-id="5a0d5-217">建立外部資料表 **STORED AS TEXTFILE** ，並將資料從 Blob 儲存體載入該資料表。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage to the table.</span></span>

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="5a0d5-218">建立和步驟 1 中建立的外部資料表具備相同結構描述及相同欄位分隔符號的內部資料表，並使用 ORC 格式儲存 Hive 資料。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-218">Create an internal table with the same schema as the external table in step 1, with the same field delimiter, and store the Hive data in the ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="5a0d5-219">從步驟 1 中的外部資料表選取資料，並插入 ORC 資料表</span><span class="sxs-lookup"><span data-stu-id="5a0d5-219">Select data from the external table in step 1 and insert into the ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="5a0d5-220">如果 TEXTFILE 資料表 &#60;資料庫名稱>.&#60;外部文字檔資料表名稱> 具有資料分割，則在步驟 3 中，`SELECT * FROM <database name>.<external textfile table name>` 命令會選取資料分割變數做為所傳回資料集中的欄位。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-220">If the TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, the `SELECT * FROM <database name>.<external textfile table name>` command selects the partition variable as a field in the returned data set.</span></span> <span data-ttu-id="5a0d5-221">將它插入 &#60;資料庫名稱>.&#60;ORC 資料表名稱> 會失敗，因為 &#60;資料庫名稱>.&#60;ORC 資料表名稱> 沒有資料分割參數可做為資料表結構描述中的欄位。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-221">Inserting it into the *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have the partition variable as a field in the table schema.</span></span> <span data-ttu-id="5a0d5-222">在此情況下，您需要明確選取要插入 &#60;資料庫名稱>.&#60;ORC 資料表名稱> 的欄位，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5a0d5-222">In this case, you need to specifically select the fields to be inserted to *&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="5a0d5-223">將所有資料插入 &#60;資料庫名稱>.&#60;ORC 資料表名稱> 之後，當您使用下列查詢時，即可安全捨棄 &#60;外部文字檔資料表名稱>：</span><span class="sxs-lookup"><span data-stu-id="5a0d5-223">It is safe to drop the *&#60;external textfile table name>* when using the following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="5a0d5-224">依照此程序執行之後，您應該會有含 ORC 格式之資料的資料表可供使用。</span><span class="sxs-lookup"><span data-stu-id="5a0d5-224">After following this procedure, you should have a table with data in the ORC format ready to use.</span></span>  

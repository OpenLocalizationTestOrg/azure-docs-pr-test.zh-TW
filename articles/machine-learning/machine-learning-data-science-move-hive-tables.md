---
title: "aaaCreate Hive 資料表和資料從 Azure Blob 儲存體載入 |Microsoft 文件"
description: "建立登錄區資料表，並載入 blob toohive 資料表中的資料"
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
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="e5a2d-103">建立 Hive 資料表，並從 Azure Blob 儲存體載入資料</span><span class="sxs-lookup"><span data-stu-id="e5a2d-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="e5a2d-104">本主題會顯示泛型 Hive 查詢，這類查詢可建立 Hive 資料表，並從 Azure Blob 儲存體載入資料。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="e5a2d-105">在分割區資料表，使用 hello 最佳化的資料列單欄式 (ORC) 格式化 tooimprove 查詢效能，也會提供一些指引。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-105">Some guidance is also provided on partitioning Hive tables and on using hello Optimized Row Columnar (ORC) formatting tooimprove query performance.</span></span>

<span data-ttu-id="e5a2d-106">這**功能表**連結 tootopics 描述 tooingest 資料可以儲存和處理期間 hello 資料的目標環境 hello 小組資料科學程序 (TDSP) 的方式。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-106">This **menu** links tootopics that describe how tooingest data into target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="e5a2d-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="e5a2d-107">Prerequisites</span></span>
<span data-ttu-id="e5a2d-108">本文假設您已經：</span><span class="sxs-lookup"><span data-stu-id="e5a2d-108">This article assumes that you have:</span></span>

* <span data-ttu-id="e5a2d-109">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-109">Created an Azure storage account.</span></span> <span data-ttu-id="e5a2d-110">如需相關指示，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="e5a2d-111">自訂的 Hadoop 叢集以 hello HDInsight 服務使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-111">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="e5a2d-112">如需指示，請參閱 [自訂適用於進階分析的 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="e5a2d-113">啟用遠端存取 toohello 叢集中，登入，並開啟 hello Hadoop 命令列主控台。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-113">Enabled remote access toohello cluster, logged in, and opened hello Hadoop Command-Line console.</span></span> <span data-ttu-id="e5a2d-114">如果您需要的指示，請參閱[存取 hello 的 Hadoop 叢集前端節點](machine-learning-data-science-customize-hadoop-cluster.md#headnode)。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-114">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="e5a2d-115">上傳資料 tooAzure blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e5a2d-115">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="e5a2d-116">如果您建立 Azure 虛擬機器中提供的 hello 指示[設定 Azure 虛擬機器執行進階分析](machine-learning-data-science-setup-virtual-machine.md)，此指令碼檔案應該已經下載的 toohello *c:\\使用者\\\<使用者名\>\\文件\\資料科學指令碼*hello 虛擬機器上的目錄。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-116">If you created an Azure virtual machine by following hello instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded toohello *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on hello virtual machine.</span></span> <span data-ttu-id="e5a2d-117">這些 Hive 查詢只需要您插入您自己的資料結構描述和準備送出 hello 適當欄位 toobe 中的 Azure blob 儲存體設定中。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in hello appropriate fields toobe ready for submission.</span></span>

<span data-ttu-id="e5a2d-118">我們假設 hello Hive 資料表的資料在**未壓縮**表格式格式和 hello 資料已經上傳 toohello 預設 （或其他 tooan） hello hello Hadoop 叢集所使用的儲存體帳戶的容器。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-118">We assume that hello data for Hive tables is in an **uncompressed** tabular format, and that hello data has been uploaded toohello default (or tooan additional) container of hello storage account used by hello Hadoop cluster.</span></span>

<span data-ttu-id="e5a2d-119">如果您想在 hello toopractice **NYC 計程車路線資料**，您需要：</span><span class="sxs-lookup"><span data-stu-id="e5a2d-119">If you want toopractice on hello **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="e5a2d-120">**下載**hello 24 [NYC 計程車路線資料](http://www.andresmh.com/nyctaxitrips)檔案 （12 個路線檔案和 12 個價位檔案）</span><span class="sxs-lookup"><span data-stu-id="e5a2d-120">**download** hello 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="e5a2d-121">**解壓縮** 為 .csv 檔案，然後</span><span class="sxs-lookup"><span data-stu-id="e5a2d-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="e5a2d-122">**上傳**它們 toohello 預設 （或適當的容器） 的 hello hello hello 中所述的程序所建立的 Azure 儲存體帳戶[自訂 Azure HDInsight Hadoop 叢集以提供進階分析程序和技術](machine-learning-data-science-customize-hadoop-cluster.md)主題。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-122">**upload** them toohello default (or appropriate container) of hello Azure storage account that was created by hello procedure outlined in hello [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="e5a2d-123">hello 程序 tooupload hello.csv 檔案 toohello 預設容器 hello 儲存體帳戶上的可以找到此[頁面](machine-learning-data-science-process-hive-walkthrough.md#upload)。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-123">hello process tooupload hello .csv files toohello default container on hello storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="e5a2d-124"><a name="submit"></a>如何 toosubmit Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="e5a2d-124"><a name="submit"></a>How toosubmit Hive queries</span></span>
<span data-ttu-id="e5a2d-125">您可以使用下列方法來提交 Hive 查詢：</span><span class="sxs-lookup"><span data-stu-id="e5a2d-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="e5a2d-126">透過 Hadoop 叢集前端節點中的 Hadoop 命令列提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="e5a2d-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="e5a2d-127">提交 Hive 查詢以 hello 登錄區編輯器</span><span class="sxs-lookup"><span data-stu-id="e5a2d-127">Submit Hive queries with hello Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="e5a2d-128">利用 Azure PowerShell 命令提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="e5a2d-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="e5a2d-129">Hive 查詢類似 SQL。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="e5a2d-130">如果您熟悉 SQL，您可能會發現 hello [SQL 使用者小工作表的 Hive](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf)很有用。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-130">If you are familiar with SQL, you may find hello [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="e5a2d-131">當提交 Hive 查詢，您也可以控制 hello 目的地的 Hive 查詢從 hello 輸出無論 hello 螢幕或 tooa 本機檔案上 hello 前端節點或 tooan Azure blob。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-131">When submitting a Hive query, you can also control hello destination of hello output from Hive queries, whether it be on hello screen or tooa local file on hello head node or tooan Azure blob.</span></span>

### <span data-ttu-id="e5a2d-132"><a name="headnode"></a> 1.透過 Hadoop 叢集前端節點中的 Hadoop 命令列提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="e5a2d-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="e5a2d-133">如果 hello Hive 查詢就會很複雜，提交直接在 hello hello Hadoop 叢集前端節點通常會導致 toofaster 返回比提交 hive 控制檔的編輯器或 Azure PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-133">If hello Hive query is complex, submitting it directly in hello head node of hello Hadoop cluster typically leads toofaster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="e5a2d-134">登入 toohello hello Hadoop 叢集前端節點，開啟 hello Hadoop 命令列桌面上 hello hello 前端節點，然後輸入命令`cd %hive_home%\bin`。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-134">Log in toohello head node of hello Hadoop cluster, open hello Hadoop Command Line on hello desktop of hello head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="e5a2d-135">Hello Hadoop 命令列中有三種方式 toosubmit Hive 查詢：</span><span class="sxs-lookup"><span data-stu-id="e5a2d-135">You have three ways toosubmit Hive queries in hello Hadoop Command Line:</span></span>

* <span data-ttu-id="e5a2d-136">直接</span><span class="sxs-lookup"><span data-stu-id="e5a2d-136">directly</span></span>
* <span data-ttu-id="e5a2d-137">使用 .hql 檔案</span><span class="sxs-lookup"><span data-stu-id="e5a2d-137">using .hql files</span></span>
* <span data-ttu-id="e5a2d-138">以 hello Hive 命令主控台</span><span class="sxs-lookup"><span data-stu-id="e5a2d-138">with hello Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="e5a2d-139">在 Hadoop 命令列中直接提交 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="e5a2d-140">您可以執行的命令，像`hive -e "<your hive query>;`toosubmit 簡單 Hive 查詢直接在 Hadoop 命令列。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-140">You can run command like `hive -e "<your hive query>;` toosubmit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="e5a2d-141">以下是的範例，其中 hello 紅色方塊外框 hello 命令送出 hello Hive 查詢，而 hello hello Hive 查詢的綠色方塊外框 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-141">Here is an example, where hello red box outlines hello command that submits hello Hive query, and hello green box outlines hello output from hello Hive query.</span></span>

![建立工作區](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="e5a2d-143">提交 .hql 檔案中的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="e5a2d-144">當 hello Hive 查詢較為複雜，而且擁有多行時，並不實用編輯命令列或 Hive 命令主控台中的查詢。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-144">When hello Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="e5a2d-145">替代方式是 toouse 文字編輯器中的 hello Hadoop 叢集 toosave hello Hive 查詢.hql 檔案中的 hello 前端節點的本機目錄中的 hello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-145">An alternative is toouse a text editor in hello head node of hello Hadoop cluster toosave hello Hive queries in a .hql file in a local directory of hello head node.</span></span> <span data-ttu-id="e5a2d-146">然後可以使用 hello 送出 hello.hql 檔案中的 hello Hive 查詢`-f`引數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e5a2d-146">Then hello Hive query in hello .hql file can be submitted by using hello `-f` argument as follows:</span></span>

    hive -f "<path toohello .hql file>"

![建立工作區](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="e5a2d-148">**隱藏 Hive 查詢的進度狀態畫面顯示**</span><span class="sxs-lookup"><span data-stu-id="e5a2d-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="e5a2d-149">根據預設，Hive 查詢提交的 Hadoop 命令列中之後, hello hello Map/Reduce 作業進度會列印螢幕上。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-149">By default, after Hive query is submitted in Hadoop Command Line, hello progress of hello Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="e5a2d-150">toosuppress hello hello Map/Reduce 作業進度的螢幕列印，您可以使用引數`-S`(大寫為"S") 中 hello 命令列，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e5a2d-150">toosuppress hello screen print of hello Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in hello command line as follows:</span></span>

    hive -S -f "<path toohello .hql file>"
<span data-ttu-id="e5a2d-151">.</span><span class="sxs-lookup"><span data-stu-id="e5a2d-151">.</span></span>    <span data-ttu-id="e5a2d-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="e5a2d-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="e5a2d-153">在 Hive 命令主控台中提交 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="e5a2d-154">您可以執行命令，以也先輸入 hello Hive 命令主控台`hive`在 Hadoop 命令列，然後提交 Hive 命令主控台中的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-154">You can also first enter hello Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="e5a2d-155">範例如下。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-155">Here is an example.</span></span> <span data-ttu-id="e5a2d-156">在此範例中，hello 兩個紅色方塊反白顯示 hello 命令會使用 tooenter hello Hive 命令主控台中，而且 hello Hive 查詢提交 Hive 命令主控台中，分別。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-156">In this example, hello two red boxes highlight hello commands used tooenter hello Hive command console, and hello Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="e5a2d-157">hello 綠色方塊反白顯示 hello hello Hive 查詢的輸出。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-157">hello green box highlights hello output from hello Hive query.</span></span>

![建立工作區](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="e5a2d-159">hello 前面的範例直接輸出畫面上 hello Hive 查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-159">hello previous examples directly output hello Hive query results on screen.</span></span> <span data-ttu-id="e5a2d-160">您也可以撰寫 hello 前端節點或 tooan Azure blob 上的 hello 輸出 tooa 本機檔案。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-160">You can also write hello output tooa local file on hello head node, or tooan Azure blob.</span></span> <span data-ttu-id="e5a2d-161">然後，您可以使用其他工具 toofurther 分析 hello 的 Hive 查詢的輸出。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-161">Then, you can use other tools toofurther analyze hello output of Hive queries.</span></span>

<span data-ttu-id="e5a2d-162">**輸出 Hive 查詢結果 tooa 本機檔案。**</span><span class="sxs-lookup"><span data-stu-id="e5a2d-162">**Output Hive query results tooa local file.**</span></span>
<span data-ttu-id="e5a2d-163">toooutput Hive 查詢結果 tooa 本機目錄 hello 前端節點上的，您有 toosubmit hello Hive 查詢 hello Hadoop 命令列中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e5a2d-163">toooutput Hive query results tooa local directory on hello head node, you have toosubmit hello Hive query in hello Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in hello head node>

<span data-ttu-id="e5a2d-164">在下列範例的 hello，Hive 查詢的 hello 輸出寫入檔案`hivequeryoutput.txt`目錄中`C:\apps\temp`。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-164">In hello following example, hello output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![建立工作區](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="e5a2d-166">**輸出 Hive 查詢的結果 tooan Azure blob**</span><span class="sxs-lookup"><span data-stu-id="e5a2d-166">**Output Hive query results tooan Azure blob**</span></span>

<span data-ttu-id="e5a2d-167">您也可以輸出 hello Hive 查詢的結果 tooan hello hello Hadoop 叢集的預設容器內的 Azure blob。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-167">You can also output hello Hive query results tooan Azure blob, within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="e5a2d-168">這個 hello Hive 查詢如下所示：</span><span class="sxs-lookup"><span data-stu-id="e5a2d-168">hello Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

<span data-ttu-id="e5a2d-169">在下列範例的 hello，Hive 查詢 hello 輸出寫入 tooa blob 目錄`queryoutputdir`hello hello Hadoop 叢集的預設容器內。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-169">In hello following example, hello output of Hive query is written tooa blob directory `queryoutputdir` within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="e5a2d-170">在這裡，您只需要 tooprovide hello 目錄名稱，不含 hello blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-170">Here, you only need tooprovide hello directory name, without hello blob name.</span></span> <span data-ttu-id="e5a2d-171">如果您同時提供目錄和 Blob 名稱 (例如 `wasb:///queryoutputdir/queryoutput.txt`)，則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![建立工作區](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="e5a2d-173">如果您開啟 hello 預設容器，使用 Azure 儲存體總管 hello Hadoop 叢集，您可以看到 hello Hive 查詢的 hello 的輸出 hello 遵循圖所示。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-173">If you open hello default container of hello Hadoop cluster using Azure Storage Explorer, you can see hello output of hello Hive query as shown in hello following figure.</span></span> <span data-ttu-id="e5a2d-174">您可以套用 hello 篩選器 （以紅色方塊反白顯示） tooonly 擷取 hello blob 名稱中指定的字元。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-174">You can apply hello filter (highlighted by red box) tooonly retrieve hello blob with specified letters in names.</span></span>

![建立工作區](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="e5a2d-176"><a name="hive-editor"></a> 2.提交 Hive 查詢以 hello 登錄區編輯器</span><span class="sxs-lookup"><span data-stu-id="e5a2d-176"><a name="hive-editor"></a> 2. Submit Hive queries with hello Hive Editor</span></span>
<span data-ttu-id="e5a2d-177">您也可以輸入 hello 表單的 URL，使用 hello 查詢主控台 （登錄區編輯器） *https://&#60;Hadoop 叢集名稱 >.azurehdinsight.net/Home/HiveEditor*在網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-177">You can also use hello Query Console (Hive Editor) by entering a URL of hello form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="e5a2d-178">您必須登入 hello，請參閱此主控台，因此您需要以下 Hadoop 叢集認證。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-178">You must be logged in hello see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="e5a2d-179"><a name="ps"></a> 3.利用 Azure PowerShell 命令提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="e5a2d-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="e5a2d-180">您也可以使用 PowerShell toosubmit Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-180">You can also use PowerShell toosubmit Hive queries.</span></span> <span data-ttu-id="e5a2d-181">如需指示，請參閱 [使用 PowerShell 提交 Hive 工作](../hdinsight/hdinsight-hadoop-use-hive-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="e5a2d-182"><a name="create-tables"></a>建立 Hive 資料庫和資料表</span><span class="sxs-lookup"><span data-stu-id="e5a2d-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="e5a2d-183">hello Hive 查詢中共用 hello [GitHub 儲存機制](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql)而且可以從該處下載。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-183">hello Hive queries are shared in hello [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="e5a2d-184">以下是建立的 Hive 資料表的 hello Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-184">Here is hello Hive query that creates a Hive table.</span></span>

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

<span data-ttu-id="e5a2d-185">以下是 hello 的描述，您需要在 tooplug hello 欄位以及其他組態：</span><span class="sxs-lookup"><span data-stu-id="e5a2d-185">Here are hello descriptions of hello fields that you need tooplug in and other configurations:</span></span>

* <span data-ttu-id="e5a2d-186">**&#60; 資料庫名稱 >**: hello 的 toocreate hello 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-186">**&#60;database name>**: hello name of hello database that you want toocreate.</span></span> <span data-ttu-id="e5a2d-187">如果您只想 toouse hello 預設資料庫，hello 查詢*建立資料庫...*可以省略。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-187">If you just want toouse hello default database, hello query *create database...* can be omitted.</span></span>
* <span data-ttu-id="e5a2d-188">**&#60; 資料表名稱 >**: hello 的 toocreate hello 指定資料庫中的 hello 資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-188">**&#60;table name>**: hello name of hello table that you want toocreate within hello specified database.</span></span> <span data-ttu-id="e5a2d-189">如果您想 toouse hello 預設資料庫，可以透過直接參考 hello 資料表*&#60; 資料表名稱 >*而不 &#60; 資料庫名稱 >。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-189">If you want toouse hello default database, hello table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="e5a2d-190">**&#60; 欄位的分隔符號 >**: hello 分隔符號分隔 hello 資料檔案 toobe 中的欄位，上傳 toohello Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-190">**&#60;field separator>**: hello separator that delimits fields in hello data file toobe uploaded toohello Hive table.</span></span>
* <span data-ttu-id="e5a2d-191">**&#60; 行分隔符號 >**: hello 分隔符號，用來分隔 hello 資料檔案中的行。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-191">**&#60;line separator>**: hello separator that delimits lines in hello data file.</span></span>
* <span data-ttu-id="e5a2d-192">**&#60; 儲存體位置 >**: hello Azure 儲存體位置 toosave hello 資料的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-192">**&#60;storage location>**: hello Azure storage location toosave hello data of Hive tables.</span></span> <span data-ttu-id="e5a2d-193">如果您未指定*位置 &#60; 儲存體位置 >*、 hello 資料庫和 hello 資料表會儲存在*hive/倉儲/*目錄中的 hello Hive 叢集預設 hello 預設容器。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-193">If you do not specify *LOCATION &#60;storage location>*, hello database and hello tables are stored in *hive/warehouse/* directory in hello default container of hello Hive cluster by default.</span></span> <span data-ttu-id="e5a2d-194">如果您想 toospecify hello 儲存位置，hello 儲存位置有 toobe hello hello 資料庫和資料表的預設容器內。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-194">If you want toospecify hello storage location, hello storage location has toobe within hello default container for hello database and tables.</span></span> <span data-ttu-id="e5a2d-195">這個位置已經 toobe 稱為 hello 格式中的 hello 叢集中的位置相對的 toohello 預設容器*'wasb: / / &#60; 目錄 1 > /'*或*' wasb: / / &#60; 目錄 1 > / &#60;目錄 2 > /'*等等。Hello 查詢執行之後，hello 相對目錄會建立 hello 預設容器內。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-195">This location has toobe referred as location relative toohello default container of hello cluster in hello format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After hello query is executed, hello relative directories are created within hello default container.</span></span>
* <span data-ttu-id="e5a2d-196">**TBLPROPERTIES("skip.header.line.count"="1")**: hello 資料檔案的標頭行，如果您有 tooadd 這個屬性**hello 結尾**的 hello*建立資料表*查詢。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If hello data file has a header line, you have tooadd this property **at hello end** of hello *create table* query.</span></span> <span data-ttu-id="e5a2d-197">否則，為記錄 toohello 資料表載入 hello 標頭行。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-197">Otherwise, hello header line is loaded as a record toohello table.</span></span> <span data-ttu-id="e5a2d-198">如果 hello 資料檔案沒有標頭行，此設定可省略 hello 查詢中。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-198">If hello data file does not have a header line, this configuration can be omitted in hello query.</span></span>

## <span data-ttu-id="e5a2d-199"><a name="load-data"></a>載入資料 tooHive 資料表</span><span class="sxs-lookup"><span data-stu-id="e5a2d-199"><a name="load-data"></a>Load data tooHive tables</span></span>
<span data-ttu-id="e5a2d-200">以下是將資料載入的 Hive 資料表的 hello Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-200">Here is hello Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="e5a2d-201">**&#60; 路徑 tooblob 資料 >**： 如果 hello blob 檔案上傳 toobe toohello Hive 資料表中的 hello HDInsight Hadoop 叢集中的 hello 預設容器，hello *（& s) #60; 路徑 tooblob 資料 >* hello 格式應該是*' wasb: / / &#60; 在此容器中的目錄 > / &#60; blob 檔案名稱 >'*。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-201">**&#60;path tooblob data>**: If hello blob file toobe uploaded toohello Hive table is in hello default container of hello HDInsight Hadoop cluster, hello *&#60;path tooblob data>* should be in hello format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="e5a2d-202">hello blob 檔案，也可以在 hello HDInsight Hadoop 叢集中的其他容器中。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-202">hello blob file can also be in an additional container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="e5a2d-203">在此情況下， *&#60; 路徑 tooblob 資料 >* hello 格式應該是*' wasb: / / （& s) #60; 容器名稱 > @ （& s) #60; 儲存體帳戶名稱 >.blob.core.windows.net/ &#60; blob 檔案名稱 >'*.</span><span class="sxs-lookup"><span data-stu-id="e5a2d-203">In this case, *&#60;path tooblob data>* should be in hello format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e5a2d-204">hello blob 資料上傳 toobe tooHive 資料表有 toobe hello 預設或 hello hello Hadoop 叢集的儲存體帳戶的其他容器中。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-204">hello blob data toobe uploaded tooHive table has toobe in hello default or additional container of hello storage account for hello Hadoop cluster.</span></span> <span data-ttu-id="e5a2d-205">否則，hello*將資料載入*抱怨無法存取 hello 資料的查詢失敗。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-205">Otherwise, hello *LOAD DATA* query fails complaining that it cannot access hello data.</span></span>
  >
  >

## <span data-ttu-id="e5a2d-206"><a name="partition-orc"></a>進階主題：資料分割資料表及使用 ORC 格式儲存 Hive 資料</span><span class="sxs-lookup"><span data-stu-id="e5a2d-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="e5a2d-207">Hello 資料很大，分割 hello 資料表是有幫助，只需要 tooscan hello 資料表的幾個資料分割的查詢。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-207">If hello data is large, partitioning hello table is beneficial for queries that only need tooscan a few partitions of hello table.</span></span> <span data-ttu-id="e5a2d-208">比方說，它是網站的日期合理 toopartition hello 記錄資料。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-208">For instance, it is reasonable toopartition hello log data of a web site by dates.</span></span>

<span data-ttu-id="e5a2d-209">在加法 toopartitioning Hive 資料表，也很有幫助 toostore hello Hive 資料 hello 最佳化的資料列單欄式 (ORC) 格式。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-209">In addition toopartitioning Hive tables, it is also beneficial toostore hello Hive data in hello Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="e5a2d-210">如需 ORC 格式的詳細資訊，請參閱<a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">在 Hive 讀取、寫入及處理資料時使用 ORC 檔案提升效能</a>。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="e5a2d-211">資料分割資料表</span><span class="sxs-lookup"><span data-stu-id="e5a2d-211">Partitioned table</span></span>
<span data-ttu-id="e5a2d-212">以下是建立資料分割的資料表和資料載入其中的 hello Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-212">Here is hello Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="e5a2d-213">查詢時資料分割的資料表，建議在 hello tooadd hello 分割區條件**開頭**的 hello`where`子句，因為這樣可改善 hello 的大幅搜尋的效率。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-213">When querying partitioned tables, it is recommended tooadd hello partition condition in hello **beginning** of hello `where` clause as this improves hello efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="e5a2d-214"><a name="orc"></a>使用 ORC 格式儲存 Hive 資料</span><span class="sxs-lookup"><span data-stu-id="e5a2d-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="e5a2d-215">您無法直接將資料載入從 blob 儲存體以 hello ORC 格式儲存的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-215">You cannot directly load data from blob storage into Hive tables that is stored in hello ORC format.</span></span> <span data-ttu-id="e5a2d-216">以下是 hello 步驟需要 tootake tooload 資料從 Azure 的 hello blob tooHive ORC 格式儲存的資料表。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-216">Here are hello steps that hello you need tootake tooload data from Azure blobs tooHive tables stored in ORC format.</span></span>

<span data-ttu-id="e5a2d-217">建立外部資料表**儲存成文字檔**並從 blob 儲存體 toohello 資料表載入資料。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage toohello table.</span></span>

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

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="e5a2d-218">建立內部資料表以 hello 相同結構描述以 hello 相同欄位分隔符號，並將儲存的步驟 1 中的 hello 外部資料表 hello hello ORC 格式的登錄區資料。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-218">Create an internal table with hello same schema as hello external table in step 1, with hello same field delimiter, and store hello Hive data in hello ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="e5a2d-219">在步驟 1 中的 hello 外部資料表選取資料和插入 hello ORC 資料表</span><span class="sxs-lookup"><span data-stu-id="e5a2d-219">Select data from hello external table in step 1 and insert into hello ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="e5a2d-220">如果 hello 文字檔資料表*&#60; 資料庫名稱 >。 （& s) #60; 外部文字檔資料表名稱 >*有資料分割，在步驟 3 中 hello`SELECT * FROM <database name>.<external textfile table name>`選取 hello 資料分割的變數，在 hello 欄位傳回的資料集的命令。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-220">If hello TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, hello `SELECT * FROM <database name>.<external textfile table name>` command selects hello partition variable as a field in hello returned data set.</span></span> <span data-ttu-id="e5a2d-221">插入 hello *（& s) #60; 資料庫名稱 >。 （& s) #60; ORC 資料表名稱 >*失敗後*（& s) #60; 資料庫名稱 >。 （& s) #60; ORC 資料表名稱 >*沒有 hello 分割變數hello 資料表結構描述中的欄位。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-221">Inserting it into hello *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have hello partition variable as a field in hello table schema.</span></span> <span data-ttu-id="e5a2d-222">在此情況下，您需要插入太 toospecifically 選取 hello 欄位 toobe*&#60; 資料庫名稱 >。 &#60; ORC 資料表名稱 >* ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e5a2d-222">In this case, you need toospecifically select hello fields toobe inserted too*&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="e5a2d-223">很安全 toodrop hello *&#60; 外部文字檔資料表名稱 >*時使用下列查詢，所有的資料之後 hello 已插入至*（& s) #60; 資料庫名稱 >。 （& s) #60; ORC 資料表名稱 >*:</span><span class="sxs-lookup"><span data-stu-id="e5a2d-223">It is safe toodrop hello *&#60;external textfile table name>* when using hello following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="e5a2d-224">完成此程序之後，您應該有資料表 hello ORC 格式準備 toouse 中的資料。</span><span class="sxs-lookup"><span data-stu-id="e5a2d-224">After following this procedure, you should have a table with data in hello ORC format ready toouse.</span></span>  

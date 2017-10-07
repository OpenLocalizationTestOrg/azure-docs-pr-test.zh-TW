---
title: "aaaRun Hadoop 作業使用 Azure Cosmos DB 和 HDInsight |Microsoft 文件"
description: "了解 toorun 簡單 Hive、 Pig 和 MapReduce 如何與 Azure Cosmos DB Azure HDInsight 工作。"
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="26490-103"><a name="Azure Cosmos DB-HDInsight"></a>使用 Azure Cosmos DB 和 HDInsight 執行 Apache Hive、Pig 或 Hadoop 作業</span><span class="sxs-lookup"><span data-stu-id="26490-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="26490-104">本教學課程示範如何 toorun [Apache Hive][apache-hive]， [Apache Pig][apache-pig]，和[Apache Hadoop] [apache-hadoop] Cosmos DB Hadoop 連接器與 Azure HDInsight 上的 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="26490-104">This tutorial shows you how toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="26490-105">Cosmos DB 的 Hadoop 連接器可讓您為來源和接收器 Hive、 Pig 和 MapReduce 工作的 Cosmos DB tooact。</span><span class="sxs-lookup"><span data-stu-id="26490-105">Cosmos DB's Hadoop connector allows Cosmos DB tooact as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="26490-106">本教學課程將使用 Cosmos DB 作為 hello 資料來源和目的地 Hadoop 工作。</span><span class="sxs-lookup"><span data-stu-id="26490-106">This tutorial will use Cosmos DB as both hello data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="26490-107">完成本教學課程之後，您會無法 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="26490-107">After completing this tutorial, you'll be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="26490-108">如何使用 Hive、Pig 或 MapReduce 作業從 Cosmos DB 載入資料？</span><span class="sxs-lookup"><span data-stu-id="26490-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="26490-109">如何使用 Hive、Pig 或 MapReduce 作業在 Cosmos DB 中儲存資料？</span><span class="sxs-lookup"><span data-stu-id="26490-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="26490-110">我們建議您藉由監看下列影片，我們透過使用 Cosmos DB 與 HDInsight Hive 工作執行所在的 hello 開始使用。</span><span class="sxs-lookup"><span data-stu-id="26490-110">We recommend getting started by watching hello following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="26490-111">然後，傳回 toothis 發行項，您會在此收到 hello 上如何的 Cosmos DB 資料執行分析工作的完整詳細資料。</span><span class="sxs-lookup"><span data-stu-id="26490-111">Then, return toothis article, where you'll receive hello full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="26490-112">本教學課程假設您先前已有使用 Apache Hadoop、Hive 和/或 Pig 的經驗。</span><span class="sxs-lookup"><span data-stu-id="26490-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="26490-113">如果您是新 tooApache Hadoop、 Hive 和 Pig，我們建議您造訪 hello [Apache Hadoop 文件][apache-hadoop-doc]。</span><span class="sxs-lookup"><span data-stu-id="26490-113">If you are new tooApache Hadoop, Hive, and Pig, we recommend visiting hello [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="26490-114">本教學課程也假設您先前已有使用 Cosmos DB 的經驗，且擁有 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="26490-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="26490-115">如果您是新 tooCosmos DB，或是您沒有 Cosmos DB 帳戶，請查看我們[入門][ getting-started]頁面。</span><span class="sxs-lookup"><span data-stu-id="26490-115">If you are new tooCosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="26490-116">沒有時間 toocomplete hello 教學課程和 Hive、 Pig 和 MapReduce 只要 tooget hello 完整的範例 PowerShell 指令碼嗎？</span><span class="sxs-lookup"><span data-stu-id="26490-116">Don't have time toocomplete hello tutorial and just want tooget hello full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="26490-117">沒問題，您可以在[這裡][hdinsight-samples]取得。</span><span class="sxs-lookup"><span data-stu-id="26490-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="26490-118">hello 下載也包含對這些範例的 hello hql、 pig 和 java 檔案。</span><span class="sxs-lookup"><span data-stu-id="26490-118">hello download also contains hello hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="26490-119"><a name="NewestVersion"></a>最新版本</span><span class="sxs-lookup"><span data-stu-id="26490-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="26490-120">Hadoop 連接器版本</span><span class="sxs-lookup"><span data-stu-id="26490-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="26490-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="26490-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="26490-122">指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="26490-122">Script Uri</span></span></th>
        <td><span data-ttu-id="26490-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="26490-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="26490-124">修改日期</span><span class="sxs-lookup"><span data-stu-id="26490-124">Date Modified</span></span></th>
        <td><span data-ttu-id="26490-125">2016 年 4 月 26 日</span><span class="sxs-lookup"><span data-stu-id="26490-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="26490-126">支援的 HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="26490-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="26490-127">3.1、3.2</span><span class="sxs-lookup"><span data-stu-id="26490-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="26490-128">變更記錄檔</span><span class="sxs-lookup"><span data-stu-id="26490-128">Change Log</span></span></th>
        <td><span data-ttu-id="26490-129">更新 Azure Cosmos DB Java SDK too1.6.0</span><span class="sxs-lookup"><span data-stu-id="26490-129">Updated Azure Cosmos DB Java SDK too1.6.0</span></span></br>
            <span data-ttu-id="26490-130">將已分割的集合支援同時加入為來源和接收</span><span class="sxs-lookup"><span data-stu-id="26490-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="26490-131"><a name="Prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="26490-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="26490-132">之前遵循 hello 指示在本教學課程，請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="26490-132">Before following hello instructions in this tutorial, ensure that you have hello following:</span></span>

* <span data-ttu-id="26490-133">Cosmos DB 帳戶、資料庫和包含文件的集合。</span><span class="sxs-lookup"><span data-stu-id="26490-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="26490-134">如需詳細資訊，請參閱[開始使用 Azure Cosmos DB][getting-started]。</span><span class="sxs-lookup"><span data-stu-id="26490-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="26490-135">範例資料匯入您的 Cosmos DB 帳戶以 hello [Cosmos DB 匯入工具][import-data]。</span><span class="sxs-lookup"><span data-stu-id="26490-135">Import sample data into your Cosmos DB account with hello [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="26490-136">輸送量。</span><span class="sxs-lookup"><span data-stu-id="26490-136">Throughput.</span></span> <span data-ttu-id="26490-137">從 HDInsight 讀取和寫入將會計入您的集合的配置要求單位。</span><span class="sxs-lookup"><span data-stu-id="26490-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="26490-138">每個輸出集合額內額外預存程序的容量。</span><span class="sxs-lookup"><span data-stu-id="26490-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="26490-139">hello 預存程序可用來傳送產生的文件。</span><span class="sxs-lookup"><span data-stu-id="26490-139">hello stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="26490-140">產生的文件 hello hello Hive、 Pig 或 MapReduce 工作的容量。</span><span class="sxs-lookup"><span data-stu-id="26490-140">Capacity for hello resulting documents from hello Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="26490-141">[*選擇性*] 額外集合的容量。</span><span class="sxs-lookup"><span data-stu-id="26490-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="26490-142">順序 tooavoid hello 建立新的集合，在任何 hello 工作期間，您可以列印 hello 結果 toostdout、 儲存 hello 輸出 tooyour WASB 容器，或指定現有的集合。</span><span class="sxs-lookup"><span data-stu-id="26490-142">In order tooavoid hello creation of a new collection during any of hello jobs, you can either print hello results toostdout, save hello output tooyour WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="26490-143">在指定的現有集合的 hello 情況下，會建立新文件 hello 集合內的與中的衝突時，只會影響現有的文件*識別碼*。</span><span class="sxs-lookup"><span data-stu-id="26490-143">In hello case of specifying an existing collection, new documents will be created inside hello collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="26490-144">**hello 連接器將會自動覆寫現有的文件識別碼衝突**。</span><span class="sxs-lookup"><span data-stu-id="26490-144">**hello connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="26490-145">您可以藉由設定 hello upsert 選項 toofalse 來關閉這項功能。</span><span class="sxs-lookup"><span data-stu-id="26490-145">You can turn off this feature by setting hello upsert option toofalse.</span></span> <span data-ttu-id="26490-146">如果 upsert 為 false，就會發生衝突，hello Hadoop 工作將會失敗。報告發生 id 衝突錯誤。</span><span class="sxs-lookup"><span data-stu-id="26490-146">If upsert is false and a conflict occurs, hello Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="26490-147"><a name="ProvisionHDInsight"></a>步驟 1︰建立新的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="26490-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="26490-148">本教學課程會使用指令碼動作 hello Azure 入口網站 toocustomize 從您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="26490-148">This tutorial uses Script Action from hello Azure Portal toocustomize your HDInsight cluster.</span></span> <span data-ttu-id="26490-149">在本教學課程中，我們將使用 hello Azure 入口網站 toocreate 您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="26490-149">In this tutorial, we will use hello Azure Portal toocreate your HDInsight cluster.</span></span> <span data-ttu-id="26490-150">如需有關如何 toouse PowerShell cmdlet 或 hello HDInsight.NET SDK，請參閱指示[自訂 HDInsight 叢集使用指令碼動作][ hdinsight-custom-provision]發行項。</span><span class="sxs-lookup"><span data-stu-id="26490-150">For instructions on how toouse PowerShell cmdlets or hello HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="26490-151">登入 toohello [Azure 入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="26490-151">Sign in toohello [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="26490-152">按一下**+ 新增**hello hello 左瀏覽頂端，在搜尋**HDInsight** hello 新刀鋒視窗上的 hello 頂端搜尋列中。</span><span class="sxs-lookup"><span data-stu-id="26490-152">Click **+ New** on hello top of hello left navigation, search for **HDInsight** in hello top search bar on hello New blade.</span></span>
3. <span data-ttu-id="26490-153">**HDInsight**所發行**Microsoft**頂端 hello hello 結果會出現。</span><span class="sxs-lookup"><span data-stu-id="26490-153">**HDInsight** published by **Microsoft** will appear at hello top of hello Results.</span></span> <span data-ttu-id="26490-154">對它按一下，然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="26490-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="26490-155">Hello 新的 HDInsight 叢集上建立刀鋒視窗中，輸入您**叢集名稱**和選取 hello**訂用帳戶**tooprovision 您想在此資源。</span><span class="sxs-lookup"><span data-stu-id="26490-155">On hello New HDInsight Cluster create blade, enter your **Cluster Name** and select hello **Subscription** you want tooprovision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="26490-156">叢集名稱</span><span class="sxs-lookup"><span data-stu-id="26490-156">Cluster name</span></span></td><td><span data-ttu-id="26490-157">名稱 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="26490-157">Name hello cluster.</span></span><br/>
<span data-ttu-id="26490-158">DNS 名稱的開頭與結尾都必須是英數字元，且可包含連字號。</span><span class="sxs-lookup"><span data-stu-id="26490-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="26490-159">hello 欄位必須是介於 3 到 63 個字元之間的字串。</span><span class="sxs-lookup"><span data-stu-id="26490-159">hello field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="26490-160">訂用帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="26490-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="26490-161">如果您有多個 Azure 訂用帳戶，請選取 hello 訂用帳戶裝載 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="26490-161">If you have more than one Azure Subscription, select hello subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="26490-162">
5.按一下**選取叢集類型**和下列屬性 toohello 組 hello 指定值。</span><span class="sxs-lookup"><span data-stu-id="26490-162">
5. Click **Select Cluster Type** and set hello following properties toohello specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="26490-163">叢集類型</span><span class="sxs-lookup"><span data-stu-id="26490-163">Cluster type</span></span></td><td><span data-ttu-id="26490-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="26490-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="26490-165">叢集層</span><span class="sxs-lookup"><span data-stu-id="26490-165">Cluster tier</span></span></td><td><span data-ttu-id="26490-166"><strong>標準</strong></span><span class="sxs-lookup"><span data-stu-id="26490-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="26490-167">作業系統</span><span class="sxs-lookup"><span data-stu-id="26490-167">Operating System</span></span></td><td><span data-ttu-id="26490-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="26490-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="26490-169">版本</span><span class="sxs-lookup"><span data-stu-id="26490-169">Version</span></span></td><td><span data-ttu-id="26490-170">最新版本</span><span class="sxs-lookup"><span data-stu-id="26490-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="26490-171">現在，按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="26490-171">Now, click **SELECT**.</span></span>

    ![提供 Hadoop HDInsight 初始叢集詳細資料][image-customprovision-page1]
6. <span data-ttu-id="26490-173">按一下**認證**tooset 您登入及遠端存取認證。</span><span class="sxs-lookup"><span data-stu-id="26490-173">Click on **Credentials** tooset your login and remote access credentials.</span></span> <span data-ttu-id="26490-174">選擇 [叢集登入使用者名稱] 和 [叢集登入密碼]。</span><span class="sxs-lookup"><span data-stu-id="26490-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="26490-175">如果您想 tooremote 到您的叢集，請選取*是*在 hello hello 刀鋒視窗的底部，並提供使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="26490-175">If you want tooremote into your cluster, select *yes* at hello bottom of hello blade and provide a username and password.</span></span>
7. <span data-ttu-id="26490-176">按一下**資料來源**tooset 您主要資料的位置存取。</span><span class="sxs-lookup"><span data-stu-id="26490-176">Click on **Data Source** tooset your primary location for data access.</span></span> <span data-ttu-id="26490-177">選擇 hello**選取方法**並指定現有的儲存體帳戶或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="26490-177">Choose hello **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="26490-178">在 hello 相同刀鋒視窗中，指定**預設容器**和**位置**。</span><span class="sxs-lookup"><span data-stu-id="26490-178">On hello same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="26490-179">然後，按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="26490-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="26490-180">選取位置關閉 tooyour Cosmos DB 帳戶區域，以提升效能</span><span class="sxs-lookup"><span data-stu-id="26490-180">Select a location close tooyour Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="26490-181">按一下**定價**tooselect hello 的節點數目和類型。</span><span class="sxs-lookup"><span data-stu-id="26490-181">Click on **Pricing** tooselect hello number and type of nodes.</span></span> <span data-ttu-id="26490-182">稍後可以保留 hello 預設組態及背景工作節點的小數位數 hello 數。</span><span class="sxs-lookup"><span data-stu-id="26490-182">You can keep hello default configuration and scale hello number of Worker nodes later on.</span></span>
10. <span data-ttu-id="26490-183">按一下**選擇性組態**，然後**指令碼動作**hello 選擇性組態刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="26490-183">Click **Optional Configuration**, then **Script Actions** in hello Optional Configuration Blade.</span></span>

     <span data-ttu-id="26490-184">在指令碼動作] 中，輸入下列資訊 toocustomize hello 您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="26490-184">In Script Actions, enter hello following information toocustomize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="26490-185">屬性</span><span class="sxs-lookup"><span data-stu-id="26490-185">Property</span></span></th><th><span data-ttu-id="26490-186">值</span><span class="sxs-lookup"><span data-stu-id="26490-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="26490-187">名稱</span><span class="sxs-lookup"><span data-stu-id="26490-187">Name</span></span></td>
             <td><span data-ttu-id="26490-188">指定 hello 指令碼動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="26490-188">Specify a name for hello script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="26490-189">指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="26490-189">Script URI</span></span></td>
             <td><span data-ttu-id="26490-190">指定 hello URI toohello 指令碼會叫用的 toocustomize hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="26490-190">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span></br></br>
<span data-ttu-id="26490-191">請輸入：</span><span class="sxs-lookup"><span data-stu-id="26490-191">Please enter:</span></span> </br> <span data-ttu-id="26490-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="26490-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="26490-193">前端</span><span class="sxs-lookup"><span data-stu-id="26490-193">Head</span></span></td>
             <td><span data-ttu-id="26490-194">按一下 [hello] 核取方塊 toorun hello hello 前端節點上的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="26490-194">Click hello checkbox toorun hello PowerShell script onto hello Head node.</span></span></br></br><span data-ttu-id="26490-195">
             <strong>勾選此核取方塊</strong>。</span><span class="sxs-lookup"><span data-stu-id="26490-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="26490-196">背景工作</span><span class="sxs-lookup"><span data-stu-id="26490-196">Worker</span></span></td>
             <td><span data-ttu-id="26490-197">按一下 [hello] 核取方塊 toorun hello PowerShell 指令碼到 hello 背景工作節點上。</span><span class="sxs-lookup"><span data-stu-id="26490-197">Click hello checkbox toorun hello PowerShell script onto hello Worker node.</span></span></br></br><span data-ttu-id="26490-198">
             <strong>勾選此核取方塊</strong>。</span><span class="sxs-lookup"><span data-stu-id="26490-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="26490-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="26490-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="26490-200">按一下 [hello] 核取方塊 toorun hello PowerShell 指令碼到 hello 動物園管理員。</span><span class="sxs-lookup"><span data-stu-id="26490-200">Click hello checkbox toorun hello PowerShell script onto hello Zookeeper.</span></span></br></br><span data-ttu-id="26490-201">
             <strong>不需要</strong>。</span><span class="sxs-lookup"><span data-stu-id="26490-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="26490-202">參數</span><span class="sxs-lookup"><span data-stu-id="26490-202">Parameters</span></span></td>
             <td><span data-ttu-id="26490-203">指定 hello 參數，如果 hello 指令碼所需。</span><span class="sxs-lookup"><span data-stu-id="26490-203">Specify hello parameters, if required by hello script.</span></span></br></br><span data-ttu-id="26490-204">
             <strong>不需要參數</strong>。</span><span class="sxs-lookup"><span data-stu-id="26490-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="26490-205">
11. 建立新的**資源群組**或使用 Azure 訂用帳戶下的現有資源群組。</span><span class="sxs-lookup"><span data-stu-id="26490-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="26490-206">12.</span><span class="sxs-lookup"><span data-stu-id="26490-206">12.</span></span> <span data-ttu-id="26490-207">現在，檢查**Pin toodashboard** tootrack 其部署和按一下**建立**！</span><span class="sxs-lookup"><span data-stu-id="26490-207">Now, check **Pin toodashboard** tootrack its deployment and click **Create**!</span></span>

## <span data-ttu-id="26490-208"><a name="InstallCmdlets"></a>步驟 2：安裝並設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="26490-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="26490-209">安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="26490-209">Install Azure PowerShell.</span></span> <span data-ttu-id="26490-210">您可以在[這裡][powershell-install-configure]找到指示。</span><span class="sxs-lookup"><span data-stu-id="26490-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="26490-211">或者，您可以使用 HDInsight 的線上 Hive 編輯器 (僅限 Hive 查詢)。</span><span class="sxs-lookup"><span data-stu-id="26490-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="26490-212">toodo，登入 toohello [Azure 入口網站][azure-portal]，按一下 [ **HDInsight**在 hello 左的窗格 tooview 一份您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="26490-212">toodo so, sign in toohello [Azure Portal][azure-portal], click **HDInsight** on hello left pane tooview a list of your HDInsight clusters.</span></span> <span data-ttu-id="26490-213">按一下您想 toorun Hive 查詢，然後再按一下 hello 叢集**查詢主控台**。</span><span class="sxs-lookup"><span data-stu-id="26490-213">Click hello cluster you want toorun Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="26490-214">開啟 Azure PowerShell 整合式指令碼環境的 hello:</span><span class="sxs-lookup"><span data-stu-id="26490-214">Open hello Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="26490-215">在執行 Windows 8 或 Windows Server 2012 或以上版本的電腦，您可以使用 hello 內建搜尋。</span><span class="sxs-lookup"><span data-stu-id="26490-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use hello built-in Search.</span></span> <span data-ttu-id="26490-216">從 hello [開始] 畫面，輸入**powershell ise**按一下**Enter**。</span><span class="sxs-lookup"><span data-stu-id="26490-216">From hello Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="26490-217">在執行版本早於 Windows 8 或 Windows Server 2012 的電腦，使用 hello [開始] 功能表。</span><span class="sxs-lookup"><span data-stu-id="26490-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use hello Start menu.</span></span> <span data-ttu-id="26490-218">從 hello [開始] 功能表中，輸入**命令提示字元**hello 搜尋方塊中，然後在 [hello 結果清單中，按一下**命令提示字元**。</span><span class="sxs-lookup"><span data-stu-id="26490-218">From hello Start menu, type **Command Prompt** in hello search box, then in hello list of results, click **Command Prompt**.</span></span> <span data-ttu-id="26490-219">在 [hello 命令提示字元，輸入**powershell_ise**按一下**Enter**。</span><span class="sxs-lookup"><span data-stu-id="26490-219">In hello Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="26490-220">新增您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="26490-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="26490-221">在 [hello 主控台窗格中，輸入**Add-azureaccount**按一下**Enter**。</span><span class="sxs-lookup"><span data-stu-id="26490-221">In hello Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="26490-222">輸入您 Azure 訂用帳戶相關聯的 hello 電子郵件地址，然後按一下**繼續**。</span><span class="sxs-lookup"><span data-stu-id="26490-222">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="26490-223">輸入 hello Azure 訂用帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="26490-223">Type in hello password for your Azure subscription.</span></span>
   4. <span data-ttu-id="26490-224">按一下 [ **登入**]。</span><span class="sxs-lookup"><span data-stu-id="26490-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="26490-225">下列圖表中的 hello 識別您的 Azure PowerShell 指令碼環境的 hello 重要部分。</span><span class="sxs-lookup"><span data-stu-id="26490-225">hello following diagram identifies hello important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Azure PowerShell 的圖表][azure-powershell-diagram]

## <span data-ttu-id="26490-227"><a name="RunHive"></a>步驟 3：使用 Cosmos DB 和 HDInsight 執行 Hive 作業</span><span class="sxs-lookup"><span data-stu-id="26490-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="26490-228">以 < > 表示的所有變數都必須使用組態設定進行填寫。</span><span class="sxs-lookup"><span data-stu-id="26490-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="26490-229">下列 PowerShell 指令碼窗格中的變數集 hello。</span><span class="sxs-lookup"><span data-stu-id="26490-229">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="26490-230">首先我們要建構查詢字串。</span><span class="sxs-lookup"><span data-stu-id="26490-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="26490-231">我們會撰寫 Hive 查詢會接受所有文件產生的系統時間戳記 (_ts) 和 Azure Cosmos DB 集合中的唯一識別碼 (_rid)、 計算所有文件以 hello 分鐘，然後儲存 hello 結果回新的 Azure Cosmos DB 集合。</span><span class="sxs-lookup"><span data-stu-id="26490-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="26490-232">首先，我們要在 Azure Cosmos DB 集合中建立 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="26490-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="26490-233">新增下列程式碼片段 toohello PowerShell 指令碼窗格中的 hello<strong>之後</strong>hello # 1 的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="26490-233">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="26490-234">請確定您包含 hello 選擇性 DocumentDB.query 參數 t 修剪我們的文件 toojust _ts 和 _rid。</span><span class="sxs-lookup"><span data-stu-id="26490-234">Make sure you include hello optional DocumentDB.query parameter t trim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="26490-235">**命名 DocumentDB.inputCollections 是正確的選擇。**</span><span class="sxs-lookup"><span data-stu-id="26490-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="26490-236">沒錯，我們允許在一筆輸入中加入多個集合：</span><span class="sxs-lookup"><span data-stu-id="26490-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="26490-237">接下來，讓我們來建立 hello 輸出集合的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="26490-237">Next, let's create a Hive table for hello output collection.</span></span> <span data-ttu-id="26490-238">hello 輸出文件屬性將 hello 月、 日、 時、 分、 hello 總次數。</span><span class="sxs-lookup"><span data-stu-id="26490-238">hello output document properties will be hello month, day, hour, minute, and hello total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="26490-239">**再重申一次，命名 DocumentDB.outputCollections 是正確的選擇。**</span><span class="sxs-lookup"><span data-stu-id="26490-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="26490-240">沒錯，我們允許在一筆輸出中加入多個集合：</span><span class="sxs-lookup"><span data-stu-id="26490-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="26490-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB 輸出集合名稱 1\>*,*\<DocumentDB 輸出集合名稱 2\>*'</span><span class="sxs-lookup"><span data-stu-id="26490-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="26490-242">hello 集合名稱不含空格，使用單一逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="26490-242">hello collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="26490-243">文件將會是跨多個集合的分散式循環配置資源。</span><span class="sxs-lookup"><span data-stu-id="26490-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="26490-244">批次的文件會儲存在一個集合，然後第二個批次的文件會儲存在 hello 下一次回收，依此類推。</span><span class="sxs-lookup"><span data-stu-id="26490-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="26490-245">最後，讓我們依月、 日、 小時和分鐘，而且插入 hello 結果回 hello 票數 hello 文件輸出 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="26490-245">Finally, let's tally hello documents by month, day, hour, and minute and insert hello results back into hello output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="26490-246">新增 hello hello 上一個查詢中的下列指令碼程式碼片段 toocreate Hive 工作定義。</span><span class="sxs-lookup"><span data-stu-id="26490-246">Add hello following script snippet toocreate a Hive job definition from hello previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="26490-247">您也可以使用 hello-檔案切換 toospecify HDFS 上的下列 HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="26490-247">You can also use hello -File switch toospecify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="26490-248">新增下列程式碼片段 toosave hello 開始時間的 hello 和送出 hello Hive 工作。</span><span class="sxs-lookup"><span data-stu-id="26490-248">Add hello following snippet toosave hello start time and submit hello Hive job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="26490-249">新增下列 hello Hive 工作 toocomplete 的 toowait hello。</span><span class="sxs-lookup"><span data-stu-id="26490-249">Add hello following toowait for hello Hive job toocomplete.</span></span>

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="26490-250">新增 hello 遵循 tooprint hello 標準輸出和 hello 開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="26490-250">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="26490-251">**執行** 新的指令碼！</span><span class="sxs-lookup"><span data-stu-id="26490-251">**Run** your new script!</span></span> <span data-ttu-id="26490-252">**按一下**hello 綠色執行] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="26490-252">**Click** hello green execute button.</span></span>
8. <span data-ttu-id="26490-253">檢查 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="26490-253">Check hello results.</span></span> <span data-ttu-id="26490-254">登入 hello [Azure 入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="26490-254">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="26490-255">按一下<strong>瀏覽</strong>hello 左側面板上。</span><span class="sxs-lookup"><span data-stu-id="26490-255">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
   2. <span data-ttu-id="26490-256">按一下<strong>一切</strong>在 hello 的右上方 hello 瀏覽面板。</span><span class="sxs-lookup"><span data-stu-id="26490-256">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
   3. <span data-ttu-id="26490-257">尋找並按一下 [Azure Cosmos DB 帳戶]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="26490-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="26490-258">接下來，尋找您<strong>Azure Cosmos DB 帳戶</strong>，然後<strong>Azure Cosmos DB Database</strong>和您<strong>Azure Cosmos DB 集合</strong>hello 輸出集合中指定相關聯Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="26490-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="26490-259">最後，按一下 [<strong>開發人員工具</strong>] 底下的 <strong>Document Explorer</strong>。</span><span class="sxs-lookup"><span data-stu-id="26490-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="26490-260">您會看到 hello 的 Hive 查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="26490-260">You will see hello results of your Hive query.</span></span>

   ![Hive 查詢結果][image-hive-query-results]

## <span data-ttu-id="26490-262"><a name="RunPig"></a>步驟 4：使用 Cosmos DB 和 HDInsight 執行 Pig 作業</span><span class="sxs-lookup"><span data-stu-id="26490-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="26490-263">以 < > 表示的所有變數都必須使用組態設定進行填寫。</span><span class="sxs-lookup"><span data-stu-id="26490-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="26490-264">下列 PowerShell 指令碼窗格中的變數集 hello。</span><span class="sxs-lookup"><span data-stu-id="26490-264">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="26490-265">首先我們要建構查詢字串。</span><span class="sxs-lookup"><span data-stu-id="26490-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="26490-266">我們會撰寫 Pig 查詢會接受所有文件產生的系統時間戳記 (_ts) 和 Azure Cosmos DB 集合中的唯一識別碼 (_rid)、 計算所有文件以 hello 分鐘，然後儲存 hello 結果回新的 Azure Cosmos DB 集合。</span><span class="sxs-lookup"><span data-stu-id="26490-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="26490-267">首先，將文件從 Cosmos DB 載入 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="26490-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="26490-268">新增下列程式碼片段 toohello PowerShell 指令碼窗格中的 hello<strong>之後</strong>hello # 1 的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="26490-268">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="26490-269">請確定 tooadd DocumentDB 查詢 toohello 選擇性 DocumentDB 查詢參數 tootrim，我們的文件 toojust _ts 和 _rid。</span><span class="sxs-lookup"><span data-stu-id="26490-269">Make sure tooadd a DocumentDB query toohello optional DocumentDB query parameter tootrim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="26490-270">沒錯，我們允許在一筆輸入中加入多個集合：</span><span class="sxs-lookup"><span data-stu-id="26490-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="26490-271">'*\<DocumentDB 輸入集合名稱 1\>*,*\<DocumentDB 輸入集合名稱 2\>*'</span><span class="sxs-lookup"><span data-stu-id="26490-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="26490-272">hello 集合名稱不含空格，使用單一逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="26490-272">hello collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="26490-273">文件將會是跨多個集合的分散式循環配置資源。</span><span class="sxs-lookup"><span data-stu-id="26490-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="26490-274">批次的文件會儲存在一個集合，然後第二個批次的文件會儲存在 hello 下一次回收，依此類推。</span><span class="sxs-lookup"><span data-stu-id="26490-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="26490-275">接下來，讓我們清點 hello 文件的 hello 月、 日、 時、 分、 hello 總次數。</span><span class="sxs-lookup"><span data-stu-id="26490-275">Next, let's tally hello documents by hello month, day, hour, minute, and hello total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="26490-276">最後，讓我們 hello 結果儲存至新輸出集合。</span><span class="sxs-lookup"><span data-stu-id="26490-276">Finally, let's store hello results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="26490-277">沒錯，我們允許在一筆輸出中加入多個集合：</span><span class="sxs-lookup"><span data-stu-id="26490-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="26490-278">'\<DocumentDB 輸出集合名稱 1\>,\<DocumentDB 輸出集合名稱 2\>'</span><span class="sxs-lookup"><span data-stu-id="26490-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="26490-279">hello 集合名稱不含空格，使用單一逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="26490-279">hello collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="26490-280">文件將會是分散式的循環配置資源的 hello 多個集合。</span><span class="sxs-lookup"><span data-stu-id="26490-280">Documents will be distributed round-robin across hello multiple collections.</span></span> <span data-ttu-id="26490-281">批次的文件會儲存在一個集合，然後第二個批次的文件會儲存在 hello 下一次回收，依此類推。</span><span class="sxs-lookup"><span data-stu-id="26490-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="26490-282">新增 hello hello 上一個查詢中的下列指令碼程式碼片段 toocreate Pig 工作定義。</span><span class="sxs-lookup"><span data-stu-id="26490-282">Add hello following script snippet toocreate a Pig job definition from hello previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="26490-283">您也可以使用 hello-檔案切換 toospecify HDFS 上的 Pig 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="26490-283">You can also use hello -File switch toospecify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="26490-284">新增下列程式碼片段 toosave hello 開始時間的 hello 和送出 hello Pig 工作。</span><span class="sxs-lookup"><span data-stu-id="26490-284">Add hello following snippet toosave hello start time and submit hello Pig job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="26490-285">新增下列 hello Pig 工作 toocomplete 的 toowait hello。</span><span class="sxs-lookup"><span data-stu-id="26490-285">Add hello following toowait for hello Pig job toocomplete.</span></span>

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="26490-286">新增 hello 遵循 tooprint hello 標準輸出和 hello 開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="26490-286">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="26490-287">**執行** 新的指令碼！</span><span class="sxs-lookup"><span data-stu-id="26490-287">**Run** your new script!</span></span> <span data-ttu-id="26490-288">**按一下**hello 綠色執行] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="26490-288">**Click** hello green execute button.</span></span>
10. <span data-ttu-id="26490-289">檢查 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="26490-289">Check hello results.</span></span> <span data-ttu-id="26490-290">登入 hello [Azure 入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="26490-290">Sign into hello [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="26490-291">按一下<strong>瀏覽</strong>hello 左側面板上。</span><span class="sxs-lookup"><span data-stu-id="26490-291">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
    2. <span data-ttu-id="26490-292">按一下<strong>一切</strong>在 hello 的右上方 hello 瀏覽面板。</span><span class="sxs-lookup"><span data-stu-id="26490-292">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
    3. <span data-ttu-id="26490-293">尋找並按一下 [Azure Cosmos DB 帳戶]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="26490-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="26490-294">接下來，尋找您<strong>Azure Cosmos DB 帳戶</strong>，然後<strong>Azure Cosmos DB Database</strong>和您<strong>Azure Cosmos DB 集合</strong>hello 輸出集合中指定相關聯Pig 查詢。</span><span class="sxs-lookup"><span data-stu-id="26490-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="26490-295">最後，按一下 [<strong>開發人員工具</strong>] 底下的 <strong>Document Explorer</strong>。</span><span class="sxs-lookup"><span data-stu-id="26490-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="26490-296">您會看到 hello Pig 查詢結果。</span><span class="sxs-lookup"><span data-stu-id="26490-296">You will see hello results of your Pig query.</span></span>

    ![Pig 查詢結果][image-pig-query-results]

## <span data-ttu-id="26490-298"><a name="RunMapReduce"></a>步驟 5：使用 Azure Cosmos DB 和 HDInsight 執行 MapReduce 作業</span><span class="sxs-lookup"><span data-stu-id="26490-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="26490-299">下列 PowerShell 指令碼窗格中的變數集 hello。</span><span class="sxs-lookup"><span data-stu-id="26490-299">Set hello following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="26490-300">我們會執行 MapReduce 工作，計算 hello Azure Cosmos DB 集合中每個文件屬性的項目數目。</span><span class="sxs-lookup"><span data-stu-id="26490-300">We'll execute a MapReduce job that tallies hello number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="26490-301">新增此指令碼程式碼片段**之後**hello 程式碼片段上方。</span><span class="sxs-lookup"><span data-stu-id="26490-301">Add this script snippet **after** hello snippet above.</span></span>

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="26490-302">TallyProperties v01.jar 隨附的 hello Cosmos DB Hadoop 連接器 hello 自訂安裝。</span><span class="sxs-lookup"><span data-stu-id="26490-302">TallyProperties-v01.jar comes with hello custom installation of hello Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="26490-303">新增下列命令 toosubmit hello MapReduce 工作的 hello。</span><span class="sxs-lookup"><span data-stu-id="26490-303">Add hello following command toosubmit hello MapReduce job.</span></span>

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="26490-304">此外 toohello MapReduce 工作定義，您也提供您想 toorun hello MapReduce 工作，以及 hello 認證 hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="26490-304">In addition toohello MapReduce job definition, you also provide hello HDInsight cluster name where you want toorun hello MapReduce job, and hello credentials.</span></span> <span data-ttu-id="26490-305">hello Start-azurehdinsightjob 是非同步的呼叫。</span><span class="sxs-lookup"><span data-stu-id="26490-305">hello Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="26490-306">hello 作業，使用 hello toocheck hello 完成*Wait-azurehdinsightjob* cmdlet。</span><span class="sxs-lookup"><span data-stu-id="26490-306">toocheck hello completion of hello job, use hello *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="26490-307">加入下列命令 toocheck hello 執行 hello MapReduce 工作的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="26490-307">Add hello following command toocheck any errors with running hello MapReduce job.</span></span>

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="26490-308">**執行** 新的指令碼！</span><span class="sxs-lookup"><span data-stu-id="26490-308">**Run** your new script!</span></span> <span data-ttu-id="26490-309">**按一下**hello 綠色執行] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="26490-309">**Click** hello green execute button.</span></span>
6. <span data-ttu-id="26490-310">檢查 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="26490-310">Check hello results.</span></span> <span data-ttu-id="26490-311">登入 hello [Azure 入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="26490-311">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="26490-312">按一下<strong>瀏覽</strong>hello 左側面板上。</span><span class="sxs-lookup"><span data-stu-id="26490-312">Click <strong>Browse</strong> on hello left-side panel.</span></span>
   2. <span data-ttu-id="26490-313">按一下<strong>一切</strong>在 hello 的右上方 hello 瀏覽面板。</span><span class="sxs-lookup"><span data-stu-id="26490-313">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span>
   3. <span data-ttu-id="26490-314">尋找並按一下 [Azure Cosmos DB 帳戶]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="26490-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="26490-315">接下來，尋找您<strong>Azure Cosmos DB 帳戶</strong>，然後<strong>Azure Cosmos DB Database</strong>和您<strong>Azure Cosmos DB 集合</strong>hello 輸出集合中指定相關聯MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="26490-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="26490-316">最後，按一下 [<strong>開發人員工具</strong>] 底下的 <strong>Document Explorer</strong>。</span><span class="sxs-lookup"><span data-stu-id="26490-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="26490-317">您會看到 hello 的 MapReduce 工作的結果。</span><span class="sxs-lookup"><span data-stu-id="26490-317">You will see hello results of your MapReduce job.</span></span>

      ![MapReduce 查詢結果][image-mapreduce-query-results]

## <span data-ttu-id="26490-319"><a name="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="26490-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="26490-320">恭喜！</span><span class="sxs-lookup"><span data-stu-id="26490-320">Congratulations!</span></span> <span data-ttu-id="26490-321">您剛剛使用 Azure Cosmos DB 和 HDInsight 執行您的第一個 Hive、Pig 和 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="26490-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="26490-322">我們已開放 Hadoop 連接器的原始碼。</span><span class="sxs-lookup"><span data-stu-id="26490-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="26490-323">如果您有興趣，您可以在 [GitHub][github] 上發表意見。</span><span class="sxs-lookup"><span data-stu-id="26490-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="26490-324">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="26490-324">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="26490-325">[使用 Documentdb 開發 Java 應用程式][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="26490-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="26490-326">[在 HDInsight 上開發 Hadoop 的 Java MapReduce 程式][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="26490-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="26490-327">[開始使用登錄區中的 Hadoop，HDInsight tooanalyze 行動話筒使用中][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="26490-327">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="26490-328">[搭配 HDInsight 使用 MapReduce][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="26490-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="26490-329">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="26490-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="26490-330">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="26490-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="26490-331">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="26490-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0

---
title: "經過一段時間 Storm 與 HDInsight 上的 HBase aaaCorrelate 事件"
description: "深入了解如何在不同的時間到達 HDInsight 上使用 Storm 和 HBase toocorrelate 事件。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="d74db-103">在不同時間使用 Storm 和 HBase 抵達的事件相互關聯</span><span class="sxs-lookup"><span data-stu-id="d74db-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="d74db-104">搭配 Apache Store 使用永續性資料存放區，可以讓在不同時間抵達的資料項目相互關聯。</span><span class="sxs-lookup"><span data-stu-id="d74db-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="d74db-105">例如，持續時間 hello 工作階段如何連結登入和登出使用者工作階段 toocalculate 事件。</span><span class="sxs-lookup"><span data-stu-id="d74db-105">For example, linking login and logout events for a user session toocalculate how long hello session lasted.</span></span>

<span data-ttu-id="d74db-106">在本文件中，您將學習如何 toocreate 基本的 C# Storm 拓撲可為使用者工作階段，追蹤登入和登出事件，並計算 hello hello 工作階段持續時間。</span><span class="sxs-lookup"><span data-stu-id="d74db-106">In this document, you learn how toocreate a basic C# Storm topology that tracks login and logout events for user sessions, and calculates hello duration of hello session.</span></span> <span data-ttu-id="d74db-107">hello 拓撲使用 HBase 做為永續性資料存放區。</span><span class="sxs-lookup"><span data-stu-id="d74db-107">hello topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="d74db-108">HBase 也允許您 tooperform 批次的查詢 hello 歷程記錄資料 tooproduce 額外的見解。</span><span class="sxs-lookup"><span data-stu-id="d74db-108">HBase also allows you tooperform batch queries on hello historical data tooproduce additional insights.</span></span> <span data-ttu-id="d74db-109">例如，在特定時間週期內已開始或結束多少個使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="d74db-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d74db-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d74db-110">Prerequisites</span></span>

* <span data-ttu-id="d74db-111">Visual Studio 和 hello HDInsight tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d74db-111">Visual Studio and hello HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="d74db-112">如需詳細資訊，請參閱[開始使用 hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="d74db-112">For more information, see [Get started using hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="d74db-113">Apache Storm on HDInsight 叢集 (Windows)。</span><span class="sxs-lookup"><span data-stu-id="d74db-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="d74db-114">在 2016 年 10 月 28 之後建立的 linux Storm 叢集上支援 SCP.NET 拓撲，而.NET 套件總 2016 年 10 月 28 可 hello HBase SDK 不上無法正常運作以 Linux 為基礎的 HDInsight</span><span class="sxs-lookup"><span data-stu-id="d74db-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, hello HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="d74db-115">Apache HBase on HDInsight 叢集 (Linux 或 Windows 型)。</span><span class="sxs-lookup"><span data-stu-id="d74db-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d74db-116">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="d74db-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d74db-117">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="d74db-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d74db-118">開發環境為 [Java](https://java.com) 1.7 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d74db-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="d74db-119">Java 是使用的 toopackage hello 拓撲時送出的 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d74db-119">Java is used toopackage hello topology when it is submitted toohello HDInsight cluster.</span></span>

  * <span data-ttu-id="d74db-120">hello **JAVA_HOME**包含 Java 的環境變數必須點 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="d74db-120">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="d74db-121">hello **%JAVA_HOME%/bin**目錄必須位於 hello 路徑</span><span class="sxs-lookup"><span data-stu-id="d74db-121">hello **%JAVA_HOME%/bin** directory must be in hello path</span></span>

## <a name="architecture"></a><span data-ttu-id="d74db-122">架構</span><span class="sxs-lookup"><span data-stu-id="d74db-122">Architecture</span></span>

![透過 hello 拓撲 hello 資料流程的圖表](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="d74db-124">相互關聯事件需要通用識別碼 hello 事件來源。</span><span class="sxs-lookup"><span data-stu-id="d74db-124">Correlating events requires a common identifier for hello event source.</span></span> <span data-ttu-id="d74db-125">例如，使用者識別碼、 工作階段識別碼或其他的資料，是） 唯一且 b） 中包含所有的資料傳送 tooStorm。</span><span class="sxs-lookup"><span data-stu-id="d74db-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent tooStorm.</span></span> <span data-ttu-id="d74db-126">這個範例會使用 GUID 值 toorepresent 工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="d74db-126">This example uses a GUID value toorepresent a session ID.</span></span>

<span data-ttu-id="d74db-127">此範例包含兩個 HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="d74db-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="d74db-128">HBase：歷程記錄資料的持續性資料存放區</span><span class="sxs-lookup"><span data-stu-id="d74db-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="d74db-129">Storm： 使用 tooingest 內送資料</span><span class="sxs-lookup"><span data-stu-id="d74db-129">Storm: used tooingest incoming data</span></span>

<span data-ttu-id="d74db-130">hello 資料 hello Storm 拓樸，隨機產生，而且包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="d74db-130">hello data is randomly generated by hello Storm topology, and consists of hello following items:</span></span>

* <span data-ttu-id="d74db-131">工作階段識別碼：可唯一識別每個工作階段的 GUID</span><span class="sxs-lookup"><span data-stu-id="d74db-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="d74db-132">事件：START 或 END 事件。</span><span class="sxs-lookup"><span data-stu-id="d74db-132">Event: a START or END event.</span></span> <span data-ttu-id="d74db-133">在此範例中，START 一律發生於 END 之前</span><span class="sxs-lookup"><span data-stu-id="d74db-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="d74db-134">Hello 事件時間： hello 時間。</span><span class="sxs-lookup"><span data-stu-id="d74db-134">Time: hello time of hello event.</span></span>

<span data-ttu-id="d74db-135">此資料已處理並儲存在 HBase 中。</span><span class="sxs-lookup"><span data-stu-id="d74db-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="d74db-136">Storm 拓撲</span><span class="sxs-lookup"><span data-stu-id="d74db-136">Storm topology</span></span>

<span data-ttu-id="d74db-137">當工作階段啟動時，**啟動**事件收到 hello 拓樸和記錄 tooHBase。</span><span class="sxs-lookup"><span data-stu-id="d74db-137">When a session starts, a **START** event is received by hello topology and logged tooHBase.</span></span> <span data-ttu-id="d74db-138">當**結束**收到事件時，會擷取 hello 拓撲 hello**啟動**事件並計算 hello hello 兩個事件之間的時間。</span><span class="sxs-lookup"><span data-stu-id="d74db-138">When an **END** event is received, hello topology retrieves hello **START** event and calculates hello time between hello two events.</span></span> <span data-ttu-id="d74db-139">這**持續時間**值接著會儲存在 HBase 以及 hello**結束**事件資訊。</span><span class="sxs-lookup"><span data-stu-id="d74db-139">This **Duration** value is then stored in HBase along with hello **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d74db-140">雖然此拓撲會示範 hello 基本模式，生產環境方案需要 tootake 設計 hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="d74db-140">While this topology demonstrates hello basic pattern, a production solution would need tootake design for hello following scenarios:</span></span>
>
> * <span data-ttu-id="d74db-141">未按順序抵達的事件</span><span class="sxs-lookup"><span data-stu-id="d74db-141">Events arriving out of order</span></span>
> * <span data-ttu-id="d74db-142">重複的事件</span><span class="sxs-lookup"><span data-stu-id="d74db-142">Duplicate events</span></span>
> * <span data-ttu-id="d74db-143">卸除的事件</span><span class="sxs-lookup"><span data-stu-id="d74db-143">Dropped events</span></span>

<span data-ttu-id="d74db-144">hello 範例拓撲是由 hello 下列元件組成：</span><span class="sxs-lookup"><span data-stu-id="d74db-144">hello sample topology is composed of hello following components:</span></span>

* <span data-ttu-id="d74db-145">Session.cs： 建立隨機的工作階段識別碼，開始時間，以及多久 hello 工作階段的持續時間來模擬使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="d74db-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long hello session lasts.</span></span>

* <span data-ttu-id="d74db-146">Spout.cs： 建立 100 個工作階段、 發出的開始事件、 hello 隨機逾時等候每個工作階段，並接著發出結束事件。</span><span class="sxs-lookup"><span data-stu-id="d74db-146">Spout.cs: creates 100 sessions, emits a START event, waits hello random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="d74db-147">然後回收結束工作階段 toogenerate 新的。</span><span class="sxs-lookup"><span data-stu-id="d74db-147">Then recycles ended sessions toogenerate new ones.</span></span>

* <span data-ttu-id="d74db-148">HBaseLookupBolt.cs： 使用 hello 工作階段識別碼 toolook HBase 從工作階段資訊。</span><span class="sxs-lookup"><span data-stu-id="d74db-148">HBaseLookupBolt.cs: uses hello session ID toolook up session information from HBase.</span></span> <span data-ttu-id="d74db-149">當處理結束事件時，它會尋找 hello 對應的開始事件，並計算 hello hello 工作階段持續時間。</span><span class="sxs-lookup"><span data-stu-id="d74db-149">When an END event is processed, it finds hello corresponding START event and calculates hello duration of hello session.</span></span>

* <span data-ttu-id="d74db-150">HBaseBolt.cs：將資訊儲存在 HBase 中。</span><span class="sxs-lookup"><span data-stu-id="d74db-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="d74db-151">類型轉換時讀取 / 寫入 tooHBase TypeHelper.cs： 幫助。</span><span class="sxs-lookup"><span data-stu-id="d74db-151">TypeHelper.cs: Helps with type conversion when reading from/writing tooHBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="d74db-152">HBase 結構描述</span><span class="sxs-lookup"><span data-stu-id="d74db-152">HBase schema</span></span>

<span data-ttu-id="d74db-153">Hbase，hello 資料會儲存在資料表具有下列結構描述/設定 hello:</span><span class="sxs-lookup"><span data-stu-id="d74db-153">In HBase, hello data is stored in a table with hello following schema/settings:</span></span>

* <span data-ttu-id="d74db-154">資料列索引鍵： 做為此資料表中的資料列的 hello 索引鍵使用識別碼 hello 工作階段。</span><span class="sxs-lookup"><span data-stu-id="d74db-154">Row key: hello session ID is used as hello key for rows in this table.</span></span>

* <span data-ttu-id="d74db-155">資料欄系列： hello 系列名稱為 'cf'。</span><span class="sxs-lookup"><span data-stu-id="d74db-155">Column family: hello family name is 'cf'.</span></span> <span data-ttu-id="d74db-156">儲存在此系列中的資料行如下：</span><span class="sxs-lookup"><span data-stu-id="d74db-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="d74db-157">事件：START 或 END。</span><span class="sxs-lookup"><span data-stu-id="d74db-157">event: START or END.</span></span>

  * <span data-ttu-id="d74db-158">時間： hello 時間，以毫秒為單位的 hello 事件發生。</span><span class="sxs-lookup"><span data-stu-id="d74db-158">time: hello time in milliseconds that hello event occurred.</span></span>

  * <span data-ttu-id="d74db-159">持續時間： hello 開始和結束事件之間的長度。</span><span class="sxs-lookup"><span data-stu-id="d74db-159">duration: hello length between START and END event.</span></span>

* <span data-ttu-id="d74db-160">版本： hello 'cf' 家族設定 tooretain 5 每個資料列版本。</span><span class="sxs-lookup"><span data-stu-id="d74db-160">VERSIONS: hello 'cf' family is set tooretain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d74db-161">版本是針對特定資料列索引鍵儲存的先前值的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d74db-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="d74db-162">根據預設，HBase 只會傳回 hello hello 最新版本資料列的值。</span><span class="sxs-lookup"><span data-stu-id="d74db-162">By default, HBase only returns hello value for hello most recent version of a row.</span></span> <span data-ttu-id="d74db-163">在此情況下，hello 相同的資料列用於所有事件 （啟動，end） 資料列的每個版本由 hello 時間戳記值。</span><span class="sxs-lookup"><span data-stu-id="d74db-163">In this case, hello same row is used for all events (START, END.) each version of a row is identified by hello timestamp value.</span></span> <span data-ttu-id="d74db-164">版本可提供針對特定識別碼記錄之事件的歷程記錄檢視。</span><span class="sxs-lookup"><span data-stu-id="d74db-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="d74db-165">下載 hello 專案</span><span class="sxs-lookup"><span data-stu-id="d74db-165">Download hello project</span></span>

<span data-ttu-id="d74db-166">您可以從下載 hello 範例專案[https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation)。</span><span class="sxs-lookup"><span data-stu-id="d74db-166">hello sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="d74db-167">此下載項目包含下列 C# 專案中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d74db-167">This download contains hello following C# projects:</span></span>

* <span data-ttu-id="d74db-168">CorrelationTopology：針對使用者工作階段隨機發出開始與結束事件的 C# Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="d74db-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="d74db-169">每個工作階段持續 1 到 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="d74db-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="d74db-170">SessionInfo: C# 主控台應用程式建立 hello HBase 資料表，並提供範例查詢 tooreturn 儲存的工作階段資料的資訊。</span><span class="sxs-lookup"><span data-stu-id="d74db-170">SessionInfo: C# console application that creates hello HBase table, and provides example queries tooreturn information about stored session data.</span></span>

## <a name="create-hello-table"></a><span data-ttu-id="d74db-171">建立 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="d74db-171">Create hello table</span></span>

1. <span data-ttu-id="d74db-172">開啟 hello **SessionInfo** Visual Studio 專案中的。</span><span class="sxs-lookup"><span data-stu-id="d74db-172">Open hello **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="d74db-173">在**方案總管 中**，以滑鼠右鍵按一下 hello **SessionInfo**專案，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="d74db-173">In **Solution Explorer**, right-click hello **SessionInfo** project and select **Properties**.</span></span>

    ![已選取屬性的功能表螢幕擷取畫面](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="d74db-175">選取**設定**，然後設定 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="d74db-175">Select **Settings**, then set hello following values:</span></span>

   * <span data-ttu-id="d74db-176">HBaseClusterURL: hello URL tooyour HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="d74db-176">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="d74db-177">例如，https://myhbasecluster.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="d74db-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="d74db-178">針對您的叢集 HBaseClusterUserName: hello admin/HTTP 使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="d74db-178">HBaseClusterUserName: hello admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="d74db-179">HBaseClusterPassword: hello hello admin/HTTP 使用者帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="d74db-179">HBaseClusterPassword: hello password for hello admin/HTTP user account</span></span>

   * <span data-ttu-id="d74db-180">HBaseTableName: hello 名稱的這個範例與 hello 資料表 toouse</span><span class="sxs-lookup"><span data-stu-id="d74db-180">HBaseTableName: hello name of hello table toouse with this example</span></span>

   * <span data-ttu-id="d74db-181">HBaseTableColumnFamily: hello 欄系列名稱</span><span class="sxs-lookup"><span data-stu-id="d74db-181">HBaseTableColumnFamily: hello column family name</span></span>

     ![設定對話方塊的影像](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="d74db-183">執行 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="d74db-183">Run hello solution.</span></span> <span data-ttu-id="d74db-184">出現提示時，選取 hello 'c' 索引鍵 toocreate hello 資料表 HBase 叢集上。</span><span class="sxs-lookup"><span data-stu-id="d74db-184">When prompted, select hello 'c' key toocreate hello table on your HBase cluster.</span></span>

## <a name="build-and-deploy-hello-storm-topology"></a><span data-ttu-id="d74db-185">建置和部署 hello Storm 拓樸</span><span class="sxs-lookup"><span data-stu-id="d74db-185">Build and deploy hello Storm topology</span></span>

1. <span data-ttu-id="d74db-186">開啟 hello **CorrelationTopology** Visual Studio 中的方案。</span><span class="sxs-lookup"><span data-stu-id="d74db-186">Open hello **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="d74db-187">在**方案總管 中**，以滑鼠右鍵按一下 hello **CorrelationTopology**專案，然後選取內容。</span><span class="sxs-lookup"><span data-stu-id="d74db-187">In **Solution Explorer**, right-click hello **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="d74db-188">在 [hello 屬性] 視窗中選取**設定**，然後輸入 hello 組態值，這個專案。</span><span class="sxs-lookup"><span data-stu-id="d74db-188">In hello properties window, select **Settings** and enter hello configuration values for this project.</span></span> <span data-ttu-id="d74db-189">hello 前 5 是的 hello 使用相同的值由 hello **SessionInfo**專案：</span><span class="sxs-lookup"><span data-stu-id="d74db-189">hello first 5 are hello same values used by hello **SessionInfo** project:</span></span>

   * <span data-ttu-id="d74db-190">HBaseClusterURL: hello URL tooyour HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="d74db-190">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="d74db-191">例如，https://myhbasecluster.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="d74db-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="d74db-192">HBaseClusterUserName: hello admin/HTTP 使用者帳戶用於您的叢集。</span><span class="sxs-lookup"><span data-stu-id="d74db-192">HBaseClusterUserName: hello admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="d74db-193">HBaseClusterPassword: hello hello admin/HTTP 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="d74db-193">HBaseClusterPassword: hello password for hello admin/HTTP user account.</span></span>

   * <span data-ttu-id="d74db-194">此範例與 hello 資料表 toouse HBaseTableName: hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="d74db-194">HBaseTableName: hello name of hello table toouse with this example.</span></span> <span data-ttu-id="d74db-195">此值為 hello 相同 hello SessionInfo 專案中所使用的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="d74db-195">This value is hello same table name as used in hello SessionInfo project.</span></span>

   * <span data-ttu-id="d74db-196">HBaseTableColumnFamily: hello 欄系列名稱。</span><span class="sxs-lookup"><span data-stu-id="d74db-196">HBaseTableColumnFamily: hello column family name.</span></span> <span data-ttu-id="d74db-197">此值為 hello 相同 hello SessionInfo 專案中所使用的資料行的系列名稱。</span><span class="sxs-lookup"><span data-stu-id="d74db-197">This value is hello same column family name as used in hello SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d74db-198">請勿變更 hello HBaseTableColumnNames，因為 hello 預設值是所使用的 hello 名稱**SessionInfo** tooretrieve 資料。</span><span class="sxs-lookup"><span data-stu-id="d74db-198">Do not change hello HBaseTableColumnNames, as hello defaults are hello names used by **SessionInfo** tooretrieve data.</span></span>

4. <span data-ttu-id="d74db-199">儲存 hello 屬性，然後建置 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="d74db-199">Save hello properties, then build hello project.</span></span>

5. <span data-ttu-id="d74db-200">在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**提交 HDInsight 上的 tooStorm**。</span><span class="sxs-lookup"><span data-stu-id="d74db-200">In **Solution Explorer**, right-click hello project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="d74db-201">如果出現提示，請輸入您的 Azure 訂閱 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="d74db-201">If prompted, enter hello credentials for your Azure subscription.</span></span>

   ![映像的 hello 提交 toostorm 功能表項目](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="d74db-203">在 hello**提交拓撲**對話方塊中，您想要此拓撲 toodeploy 選取 hello Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="d74db-203">In hello **Submit Topology** dialog, select hello Storm cluster you want toodeploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d74db-204">hello 第一次提交拓撲，可能需要幾秒鐘的時間 tooretrieve hello 您的 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="d74db-204">hello first time you submit a topology, it may take a few seconds tooretrieve hello name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="d74db-205">一旦 hello 拓撲已上傳和提交 toohello 叢集，hello **Storm 拓撲檢視**會開啟並顯示 hello 執行拓樸。</span><span class="sxs-lookup"><span data-stu-id="d74db-205">Once hello topology has been uploaded and submitted toohello cluster, hello **Storm Topology View** opens and displays hello running topology.</span></span> <span data-ttu-id="d74db-206">toorefresh hello 資料選取 hello **CorrelationTopology**並用 hello 重新整理 按鈕在 hello hello 頁面的右上方。</span><span class="sxs-lookup"><span data-stu-id="d74db-206">toorefresh hello data, select hello **CorrelationTopology** and use hello refresh button at hello top right of hello page.</span></span>

   ![映像的 hello 拓撲檢視](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="d74db-208">當 hello 拓樸開始產生資料時，hello 中 hello 值**Emitted**資料行遞增。</span><span class="sxs-lookup"><span data-stu-id="d74db-208">When hello topology begins generating data, hello value in hello **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d74db-209">如果 hello **Storm 拓撲檢視**不會自動開啟，請使用它 hello 步驟 tooopen 下列：</span><span class="sxs-lookup"><span data-stu-id="d74db-209">If hello **Storm Topology View** does not open automatically, use hello following steps tooopen it:</span></span>
   >
   > 1. <span data-ttu-id="d74db-210">在 [方案總管] 中，展開 **Azure**，然後展開 **HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="d74db-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="d74db-211">Hello 拓撲以滑鼠右鍵按一下 hello Storm 叢集會在上執行，然後選取**檢視 Storm 拓撲**</span><span class="sxs-lookup"><span data-stu-id="d74db-211">Right-click hello Storm cluster that hello topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-hello-data"></a><span data-ttu-id="d74db-212">查詢 hello 資料</span><span class="sxs-lookup"><span data-stu-id="d74db-212">Query hello data</span></span>

<span data-ttu-id="d74db-213">一旦已發出資料，使用下列步驟 tooquery hello 資料 hello。</span><span class="sxs-lookup"><span data-stu-id="d74db-213">Once data has been emitted, use hello following steps tooquery hello data.</span></span>

1. <span data-ttu-id="d74db-214">傳回 toohello **SessionInfo**專案。</span><span class="sxs-lookup"><span data-stu-id="d74db-214">Return toohello **SessionInfo** project.</span></span> <span data-ttu-id="d74db-215">如果不在執行中，請啟動它的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="d74db-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="d74db-216">出現提示時，選取**s** toosearch 開始事件。</span><span class="sxs-lookup"><span data-stu-id="d74db-216">When prompted, select **s** toosearch for START event.</span></span> <span data-ttu-id="d74db-217">您會提示的 tooenter 開始和結束時間 toodefine 時間範圍-會傳回這兩個時間之間的唯一事件。</span><span class="sxs-lookup"><span data-stu-id="d74db-217">You are prompted tooenter a start and end time toodefine a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="d74db-218">使用 hello 下列格式輸入 hello 開始和結束時間： hh: mm 和 'm' 或 'pm'。</span><span class="sxs-lookup"><span data-stu-id="d74db-218">Use hello following format when entering hello start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="d74db-219">例如，11:20pm。</span><span class="sxs-lookup"><span data-stu-id="d74db-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="d74db-220">tooreturn 記錄事件，會使用 hello Storm 部署拓撲之前, 從開始時間和結束時間為現在。</span><span class="sxs-lookup"><span data-stu-id="d74db-220">tooreturn logged events, use a start time from before hello Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="d74db-221">hello 傳回的資料包含下列文字的項目類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="d74db-221">hello return data contains entries similar toohello following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="d74db-222">正在搜尋的結束事件 works hello 相同做為開始事件。</span><span class="sxs-lookup"><span data-stu-id="d74db-222">Searching for END events works hello same as START events.</span></span> <span data-ttu-id="d74db-223">不過，結束事件是隨機產生的 hello 開始事件之後的 1 到 5 分鐘之間。</span><span class="sxs-lookup"><span data-stu-id="d74db-223">However, END events are generated randomly between 1 and 5 minutes after hello START event.</span></span> <span data-ttu-id="d74db-224">您可能需要一些時間範圍 toofind hello 結束事件 tootry。</span><span class="sxs-lookup"><span data-stu-id="d74db-224">You may have tootry a few time ranges toofind hello END events.</span></span> <span data-ttu-id="d74db-225">結束事件也包含 hello 持續時間的 hello 工作階段-hello hello 開始事件時間和結束事件時間之間的差異。</span><span class="sxs-lookup"><span data-stu-id="d74db-225">END events also contain hello duration of hello session - hello difference between hello START event time and END event time.</span></span> <span data-ttu-id="d74db-226">以下是 END 事件的資料範例：</span><span class="sxs-lookup"><span data-stu-id="d74db-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="d74db-227">雖然您輸入的 hello 時間值以本地時間，從 hello 查詢傳回的 hello 時間是使用 utc 格式。</span><span class="sxs-lookup"><span data-stu-id="d74db-227">While hello time values you enter are in local time, hello time returned from hello query is in UTC.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="d74db-228">停止 hello 拓樸</span><span class="sxs-lookup"><span data-stu-id="d74db-228">Stop hello topology</span></span>

<span data-ttu-id="d74db-229">當您準備好 toostop hello 拓撲時，傳回 toohello **CorrelationTopology** Visual Studio 專案中的。</span><span class="sxs-lookup"><span data-stu-id="d74db-229">When you are ready toostop hello topology, return toohello **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="d74db-230">在 hello **Storm 拓撲檢視**選取 hello 拓樸，然後使用 hello **Kill**在 hello hello 拓撲檢視頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d74db-230">In hello **Storm Topology View**, select hello topology and then use hello **Kill** button at hello top of hello topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="d74db-231">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="d74db-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="d74db-232">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d74db-232">Next steps</span></span>

<span data-ttu-id="d74db-233">如需更多 Storm 範例，請參閱 [Storm on HDInsight 上的範例拓撲](hdinsight-storm-example-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="d74db-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

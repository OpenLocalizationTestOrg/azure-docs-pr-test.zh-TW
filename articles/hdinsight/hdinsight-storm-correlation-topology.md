---
title: "使用 HDInsight 上的 Storm 和 HBase 讓事件隨著時間而相互關聯"
description: "了解如何使用 HDInsight 上的 Storm 和 HBase 讓在不同的時間抵達的事件相互關聯。"
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
ms.openlocfilehash: 06630096383601e48e8f69f8553314cee42f5f3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="279bf-103">在不同時間使用 Storm 和 HBase 抵達的事件相互關聯</span><span class="sxs-lookup"><span data-stu-id="279bf-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="279bf-104">搭配 Apache Store 使用永續性資料存放區，可以讓在不同時間抵達的資料項目相互關聯。</span><span class="sxs-lookup"><span data-stu-id="279bf-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="279bf-105">例如，連結使用者工作階段的登入和登出事件，可計算工作階段的持續時間長度。</span><span class="sxs-lookup"><span data-stu-id="279bf-105">For example, linking login and logout events for a user session to calculate how long the session lasted.</span></span>

<span data-ttu-id="279bf-106">在本文件中，您會學習如何建立基本的 C# Storm 拓撲，以便追蹤使用者工作階段的登入和登出事件，並計算工作階段的持續時間。</span><span class="sxs-lookup"><span data-stu-id="279bf-106">In this document, you learn how to create a basic C# Storm topology that tracks login and logout events for user sessions, and calculates the duration of the session.</span></span> <span data-ttu-id="279bf-107">此拓撲會使用 HBase 做為永續性資料存放區。</span><span class="sxs-lookup"><span data-stu-id="279bf-107">The topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="279bf-108">HBase 也可讓您對歷程記錄資料執行批次查詢來產生額外的見解。</span><span class="sxs-lookup"><span data-stu-id="279bf-108">HBase also allows you to perform batch queries on the historical data to produce additional insights.</span></span> <span data-ttu-id="279bf-109">例如，在特定時間週期內已開始或結束多少個使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="279bf-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="279bf-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="279bf-110">Prerequisites</span></span>

* <span data-ttu-id="279bf-111">Visual Studio 和 HDInsight tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="279bf-111">Visual Studio and the HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="279bf-112">如需詳細資訊，請參閱[開始使用 HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="279bf-112">For more information, see [Get started using the HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="279bf-113">Apache Storm on HDInsight 叢集 (Windows)。</span><span class="sxs-lookup"><span data-stu-id="279bf-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="279bf-114">雖然在 2016/10/28 之後建立的 Linux 架構 Storm 叢集可支援 SCP.NET 拓撲，但 2016/10/28 起提供的 HBase SDK for .NET 套件無法在 Linux 上的 HDInsight 中正確運作</span><span class="sxs-lookup"><span data-stu-id="279bf-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, the HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="279bf-115">Apache HBase on HDInsight 叢集 (Linux 或 Windows 型)。</span><span class="sxs-lookup"><span data-stu-id="279bf-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="279bf-116">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="279bf-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="279bf-117">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="279bf-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="279bf-118">開發環境為 [Java](https://java.com) 1.7 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="279bf-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="279bf-119">當拓撲提交到 HDInsight 叢集時，會使用 Java 來封裝它。</span><span class="sxs-lookup"><span data-stu-id="279bf-119">Java is used to package the topology when it is submitted to the HDInsight cluster.</span></span>

  * <span data-ttu-id="279bf-120">**JAVA_HOME** 環境變數必須指向包含 Java 的目錄。</span><span class="sxs-lookup"><span data-stu-id="279bf-120">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="279bf-121">**%JAVA_HOME%/bin** 目錄必須在路徑中</span><span class="sxs-lookup"><span data-stu-id="279bf-121">The **%JAVA_HOME%/bin** directory must be in the path</span></span>

## <a name="architecture"></a><span data-ttu-id="279bf-122">架構</span><span class="sxs-lookup"><span data-stu-id="279bf-122">Architecture</span></span>

![透過拓撲的資料流程圖表](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="279bf-124">需要有事件來源的通用識別碼，才能讓事件相互關聯。</span><span class="sxs-lookup"><span data-stu-id="279bf-124">Correlating events requires a common identifier for the event source.</span></span> <span data-ttu-id="279bf-125">例如，使用者識別碼、工作階段識別碼，或其他資料：a) 唯一的資料，b) 包含在所有傳送至 Storm 的資料。</span><span class="sxs-lookup"><span data-stu-id="279bf-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent to Storm.</span></span> <span data-ttu-id="279bf-126">此範例使用 GUID 值代表工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="279bf-126">This example uses a GUID value to represent a session ID.</span></span>

<span data-ttu-id="279bf-127">此範例包含兩個 HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="279bf-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="279bf-128">HBase：歷程記錄資料的持續性資料存放區</span><span class="sxs-lookup"><span data-stu-id="279bf-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="279bf-129">Storm：用來擷取傳入的資料</span><span class="sxs-lookup"><span data-stu-id="279bf-129">Storm: used to ingest incoming data</span></span>

<span data-ttu-id="279bf-130">資料是由 Storm 拓撲隨機產生，並包括下列項目：</span><span class="sxs-lookup"><span data-stu-id="279bf-130">The data is randomly generated by the Storm topology, and consists of the following items:</span></span>

* <span data-ttu-id="279bf-131">工作階段識別碼：可唯一識別每個工作階段的 GUID</span><span class="sxs-lookup"><span data-stu-id="279bf-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="279bf-132">事件：START 或 END 事件。</span><span class="sxs-lookup"><span data-stu-id="279bf-132">Event: a START or END event.</span></span> <span data-ttu-id="279bf-133">在此範例中，START 一律發生於 END 之前</span><span class="sxs-lookup"><span data-stu-id="279bf-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="279bf-134">時間：事件的時間。</span><span class="sxs-lookup"><span data-stu-id="279bf-134">Time: the time of the event.</span></span>

<span data-ttu-id="279bf-135">此資料已處理並儲存在 HBase 中。</span><span class="sxs-lookup"><span data-stu-id="279bf-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="279bf-136">Storm 拓撲</span><span class="sxs-lookup"><span data-stu-id="279bf-136">Storm topology</span></span>

<span data-ttu-id="279bf-137">當工作階段開始時， **START** 事件會由拓撲接收並記錄至 HBase。</span><span class="sxs-lookup"><span data-stu-id="279bf-137">When a session starts, a **START** event is received by the topology and logged to HBase.</span></span> <span data-ttu-id="279bf-138">收到 **END** 事件時，拓撲會擷取 **START** 事件並計算兩個事件之間的時間。</span><span class="sxs-lookup"><span data-stu-id="279bf-138">When an **END** event is received, the topology retrieves the **START** event and calculates the time between the two events.</span></span> <span data-ttu-id="279bf-139">此 [持續時間] 值接著會連同 **END** 事件資訊儲存在 HBase 中。</span><span class="sxs-lookup"><span data-stu-id="279bf-139">This **Duration** value is then stored in HBase along with the **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="279bf-140">雖然此拓撲示範基本模式，但生產方案必須採用下列案例的設計：</span><span class="sxs-lookup"><span data-stu-id="279bf-140">While this topology demonstrates the basic pattern, a production solution would need to take design for the following scenarios:</span></span>
>
> * <span data-ttu-id="279bf-141">未按順序抵達的事件</span><span class="sxs-lookup"><span data-stu-id="279bf-141">Events arriving out of order</span></span>
> * <span data-ttu-id="279bf-142">重複的事件</span><span class="sxs-lookup"><span data-stu-id="279bf-142">Duplicate events</span></span>
> * <span data-ttu-id="279bf-143">卸除的事件</span><span class="sxs-lookup"><span data-stu-id="279bf-143">Dropped events</span></span>

<span data-ttu-id="279bf-144">本範例拓撲包含下列元件：</span><span class="sxs-lookup"><span data-stu-id="279bf-144">The sample topology is composed of the following components:</span></span>

* <span data-ttu-id="279bf-145">Session.cs：藉由建立隨機工作階段識別碼、開始時間，以及工作階段的持續時間長度，模擬使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="279bf-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long the session lasts.</span></span>

* <span data-ttu-id="279bf-146">Spout.cs：建立 100 個工作階段、發出 START 事件、等候每個工作階段隨機逾時，然後發出 END 事件。</span><span class="sxs-lookup"><span data-stu-id="279bf-146">Spout.cs: creates 100 sessions, emits a START event, waits the random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="279bf-147">然後回收結束的工作階段，以產生新的工作階段。</span><span class="sxs-lookup"><span data-stu-id="279bf-147">Then recycles ended sessions to generate new ones.</span></span>

* <span data-ttu-id="279bf-148">HBaseLookupBolt.cs：使用工作階段識別碼來查閱 HBase 中的工作階段資訊。</span><span class="sxs-lookup"><span data-stu-id="279bf-148">HBaseLookupBolt.cs: uses the session ID to look up session information from HBase.</span></span> <span data-ttu-id="279bf-149">處理 END 事件時，它會尋找對應的 START 事件並計算工作階段的持續時間。</span><span class="sxs-lookup"><span data-stu-id="279bf-149">When an END event is processed, it finds the corresponding START event and calculates the duration of the session.</span></span>

* <span data-ttu-id="279bf-150">HBaseBolt.cs：將資訊儲存在 HBase 中。</span><span class="sxs-lookup"><span data-stu-id="279bf-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="279bf-151">TypeHelper.cs：有助於讀取/寫入 HBase 時的類型轉換。</span><span class="sxs-lookup"><span data-stu-id="279bf-151">TypeHelper.cs: Helps with type conversion when reading from/writing to HBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="279bf-152">HBase 結構描述</span><span class="sxs-lookup"><span data-stu-id="279bf-152">HBase schema</span></span>

<span data-ttu-id="279bf-153">在 HBase 中，資料會儲存在具有下列結構描述/設定的資料表中：</span><span class="sxs-lookup"><span data-stu-id="279bf-153">In HBase, the data is stored in a table with the following schema/settings:</span></span>

* <span data-ttu-id="279bf-154">資料列索引鍵：工作階段識別碼做為此資料表中資料列的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="279bf-154">Row key: the session ID is used as the key for rows in this table.</span></span>

* <span data-ttu-id="279bf-155">資料行系列：系列名稱為 'cf'。</span><span class="sxs-lookup"><span data-stu-id="279bf-155">Column family: the family name is 'cf'.</span></span> <span data-ttu-id="279bf-156">儲存在此系列中的資料行如下：</span><span class="sxs-lookup"><span data-stu-id="279bf-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="279bf-157">事件：START 或 END。</span><span class="sxs-lookup"><span data-stu-id="279bf-157">event: START or END.</span></span>

  * <span data-ttu-id="279bf-158">時間：事件發生的時間 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="279bf-158">time: the time in milliseconds that the event occurred.</span></span>

  * <span data-ttu-id="279bf-159">持續時間：START 和 END 事件之間的長度。</span><span class="sxs-lookup"><span data-stu-id="279bf-159">duration: the length between START and END event.</span></span>

* <span data-ttu-id="279bf-160">版本：'cf' 系列會設定為每個資料列保留 5 個版本。</span><span class="sxs-lookup"><span data-stu-id="279bf-160">VERSIONS: the 'cf' family is set to retain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="279bf-161">版本是針對特定資料列索引鍵儲存的先前值的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="279bf-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="279bf-162">根據預設，HBase 只會針對資料列的最新版本傳回此值。</span><span class="sxs-lookup"><span data-stu-id="279bf-162">By default, HBase only returns the value for the most recent version of a row.</span></span> <span data-ttu-id="279bf-163">在此情況下，相同的資料列使用於所有事件 (START、END)，而資料列的每個版本都是以時間戳記值識別。</span><span class="sxs-lookup"><span data-stu-id="279bf-163">In this case, the same row is used for all events (START, END.) each version of a row is identified by the timestamp value.</span></span> <span data-ttu-id="279bf-164">版本可提供針對特定識別碼記錄之事件的歷程記錄檢視。</span><span class="sxs-lookup"><span data-stu-id="279bf-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-the-project"></a><span data-ttu-id="279bf-165">下載專案</span><span class="sxs-lookup"><span data-stu-id="279bf-165">Download the project</span></span>

<span data-ttu-id="279bf-166">您可以從 [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation)下載範例專案。</span><span class="sxs-lookup"><span data-stu-id="279bf-166">The sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="279bf-167">此下載包含下列 C# 專案：</span><span class="sxs-lookup"><span data-stu-id="279bf-167">This download contains the following C# projects:</span></span>

* <span data-ttu-id="279bf-168">CorrelationTopology：針對使用者工作階段隨機發出開始與結束事件的 C# Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="279bf-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="279bf-169">每個工作階段持續 1 到 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="279bf-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="279bf-170">SessionInfo：C# 主控台應用程式，用以建立 HBase 資料表，以及提供範例查詢來傳回儲存的工作階段資料相關資訊。</span><span class="sxs-lookup"><span data-stu-id="279bf-170">SessionInfo: C# console application that creates the HBase table, and provides example queries to return information about stored session data.</span></span>

## <a name="create-the-table"></a><span data-ttu-id="279bf-171">建立資料表</span><span class="sxs-lookup"><span data-stu-id="279bf-171">Create the table</span></span>

1. <span data-ttu-id="279bf-172">在 Visual Studio 中開啟 **SessionInfo** 專案。</span><span class="sxs-lookup"><span data-stu-id="279bf-172">Open the **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="279bf-173">在 [方案總管] 中，於 **SessionInfo** 專案上按一下滑鼠右鍵，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="279bf-173">In **Solution Explorer**, right-click the **SessionInfo** project and select **Properties**.</span></span>

    ![已選取屬性的功能表螢幕擷取畫面](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="279bf-175">選取 [ **設定**]，然後設定下列值：</span><span class="sxs-lookup"><span data-stu-id="279bf-175">Select **Settings**, then set the following values:</span></span>

   * <span data-ttu-id="279bf-176">HBaseClusterURL：HBase 叢集的 URL。</span><span class="sxs-lookup"><span data-stu-id="279bf-176">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="279bf-177">例如，https://myhbasecluster.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="279bf-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="279bf-178">HBaseClusterUserName：您的叢集的 admin/HTTP 使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="279bf-178">HBaseClusterUserName: the admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="279bf-179">HBaseClusterPassword：admin/HTTP 使用者帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="279bf-179">HBaseClusterPassword: the password for the admin/HTTP user account</span></span>

   * <span data-ttu-id="279bf-180">HBaseTableName：要用於此範例的資料表名稱</span><span class="sxs-lookup"><span data-stu-id="279bf-180">HBaseTableName: the name of the table to use with this example</span></span>

   * <span data-ttu-id="279bf-181">HBaseTableColumnFamily：資料行系列名稱</span><span class="sxs-lookup"><span data-stu-id="279bf-181">HBaseTableColumnFamily: The column family name</span></span>

     ![設定對話方塊的影像](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="279bf-183">執行方案。</span><span class="sxs-lookup"><span data-stu-id="279bf-183">Run the solution.</span></span> <span data-ttu-id="279bf-184">出現提示時，選取用以在 HBase 叢集上建立資料表的 'c' 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="279bf-184">When prompted, select the 'c' key to create the table on your HBase cluster.</span></span>

## <a name="build-and-deploy-the-storm-topology"></a><span data-ttu-id="279bf-185">建立和部署 Storm 拓撲</span><span class="sxs-lookup"><span data-stu-id="279bf-185">Build and deploy the Storm topology</span></span>

1. <span data-ttu-id="279bf-186">在 Visual Studio 中開啟 [ **CorrelationTopology** ] 方案。</span><span class="sxs-lookup"><span data-stu-id="279bf-186">Open the **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="279bf-187">在 [方案總管] 中，於 **CorrelationTopology** 專案上按一下滑鼠右鍵，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="279bf-187">In **Solution Explorer**, right-click the **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="279bf-188">在 [屬性] 視窗中，選取 [設定] 並輸入此專案的組態值。</span><span class="sxs-lookup"><span data-stu-id="279bf-188">In the properties window, select **Settings** and enter the configuration values for this project.</span></span> <span data-ttu-id="279bf-189">前 5 項是 **SessionInfo** 專案使用的相同值：</span><span class="sxs-lookup"><span data-stu-id="279bf-189">The first 5 are the same values used by the **SessionInfo** project:</span></span>

   * <span data-ttu-id="279bf-190">HBaseClusterURL：HBase 叢集的 URL。</span><span class="sxs-lookup"><span data-stu-id="279bf-190">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="279bf-191">例如，https://myhbasecluster.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="279bf-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="279bf-192">HBaseClusterUserName：您的叢集的 admin/HTTP 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="279bf-192">HBaseClusterUserName: the admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="279bf-193">HBaseClusterPassword：admin/HTTP 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="279bf-193">HBaseClusterPassword: the password for the admin/HTTP user account.</span></span>

   * <span data-ttu-id="279bf-194">HBaseTableName：要用於此範例的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="279bf-194">HBaseTableName: the name of the table to use with this example.</span></span> <span data-ttu-id="279bf-195">這個值與 SessionInfo 專案中使用的資料表名稱相同。</span><span class="sxs-lookup"><span data-stu-id="279bf-195">This value is the same table name as used in the SessionInfo project.</span></span>

   * <span data-ttu-id="279bf-196">HBaseTableColumnFamily：資料行系列名稱。</span><span class="sxs-lookup"><span data-stu-id="279bf-196">HBaseTableColumnFamily: The column family name.</span></span> <span data-ttu-id="279bf-197">這個值與 SessionInfo 專案中使用的資料行系列名稱相同。</span><span class="sxs-lookup"><span data-stu-id="279bf-197">This value is the same column family name as used in the SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="279bf-198">請勿變更 HBaseTableColumnNames，因為預設值是 **SessionInfo** 用來擷取資料的名稱。</span><span class="sxs-lookup"><span data-stu-id="279bf-198">Do not change the HBaseTableColumnNames, as the defaults are the names used by **SessionInfo** to retrieve data.</span></span>

4. <span data-ttu-id="279bf-199">儲存屬性，然後建置專案。</span><span class="sxs-lookup"><span data-stu-id="279bf-199">Save the properties, then build the project.</span></span>

5. <span data-ttu-id="279bf-200">在 [方案總管] 中，於專案上按一下滑鼠右鍵，然後選取 [提交至 Storm on HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="279bf-200">In **Solution Explorer**, right-click the project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="279bf-201">如果出現提示，請輸入您 Azure 訂用帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="279bf-201">If prompted, enter the credentials for your Azure subscription.</span></span>

   ![提交至 Storm 功能表項目的影像](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="279bf-203">在 [提交拓撲] 對話方塊中，選取要將此拓撲部署到的 Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="279bf-203">In the **Submit Topology** dialog, select the Storm cluster you want to deploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="279bf-204">第一次提交拓撲時，可能需要幾秒鐘的時間來擷取您的 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="279bf-204">The first time you submit a topology, it may take a few seconds to retrieve the name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="279bf-205">拓撲上傳並提交至叢集後，[Storm 拓撲檢視] 會開啟並顯示執行中的拓撲。</span><span class="sxs-lookup"><span data-stu-id="279bf-205">Once the topology has been uploaded and submitted to the cluster, the **Storm Topology View** opens and displays the running topology.</span></span> <span data-ttu-id="279bf-206">若要重新整理資料，請選取 **CorrelationTopology**，並使用頁面右上方的 [重新整理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="279bf-206">To refresh the data, select the **CorrelationTopology** and use the refresh button at the top right of the page.</span></span>

   ![拓撲檢視的影像](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="279bf-208">拓撲開始產生資料時，[已發出] 中的值會遞增。</span><span class="sxs-lookup"><span data-stu-id="279bf-208">When the topology begins generating data, the value in the **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="279bf-209">如果 [ **Storm 拓撲檢視** ] 並未自動開啟，請使用下列步驟來開啟：</span><span class="sxs-lookup"><span data-stu-id="279bf-209">If the **Storm Topology View** does not open automatically, use the following steps to open it:</span></span>
   >
   > 1. <span data-ttu-id="279bf-210">在 [方案總管] 中，展開 **Azure**，然後展開 **HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="279bf-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="279bf-211">以滑鼠右鍵按一下正在執行拓撲的 Storm 叢集，然後選取 [檢視 Storm 拓撲]</span><span class="sxs-lookup"><span data-stu-id="279bf-211">Right-click the Storm cluster that the topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-the-data"></a><span data-ttu-id="279bf-212">查詢資料</span><span class="sxs-lookup"><span data-stu-id="279bf-212">Query the data</span></span>

<span data-ttu-id="279bf-213">發出資料後，使用下列步驟來查詢資料。</span><span class="sxs-lookup"><span data-stu-id="279bf-213">Once data has been emitted, use the following steps to query the data.</span></span>

1. <span data-ttu-id="279bf-214">回到 **SessionInfo** 專案。</span><span class="sxs-lookup"><span data-stu-id="279bf-214">Return to the **SessionInfo** project.</span></span> <span data-ttu-id="279bf-215">如果不在執行中，請啟動它的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="279bf-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="279bf-216">出現提示時，選取 **s** 以搜尋 START 事件。</span><span class="sxs-lookup"><span data-stu-id="279bf-216">When prompted, select **s** to search for START event.</span></span> <span data-ttu-id="279bf-217">系統會提示您輸入開始和結束時間來定義時間範圍，發生於這兩個時間之間的事件才會傳回。</span><span class="sxs-lookup"><span data-stu-id="279bf-217">You are prompted to enter a start and end time to define a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="279bf-218">輸入開始和結束時間時，請使用下列格式：HH:MM 和 'am' 或 'pm'。</span><span class="sxs-lookup"><span data-stu-id="279bf-218">Use the following format when entering the start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="279bf-219">例如，11:20pm。</span><span class="sxs-lookup"><span data-stu-id="279bf-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="279bf-220">若要傳回記錄的事件，請使用早於 Storm 拓撲部署的開始時間，以及現在的結束時間。</span><span class="sxs-lookup"><span data-stu-id="279bf-220">To return logged events, use a start time from before the Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="279bf-221">傳回的資料包含類似下列文字的項目︰</span><span class="sxs-lookup"><span data-stu-id="279bf-221">The return data contains entries similar to the following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="279bf-222">搜尋 END 事件和 START 事件的方式相同。</span><span class="sxs-lookup"><span data-stu-id="279bf-222">Searching for END events works the same as START events.</span></span> <span data-ttu-id="279bf-223">不過，END 事件會在 START 事件之後的 1 到 5 分鐘之間隨機產生。</span><span class="sxs-lookup"><span data-stu-id="279bf-223">However, END events are generated randomly between 1 and 5 minutes after the START event.</span></span> <span data-ttu-id="279bf-224">您可能必須嘗試幾個時間範圍，以便找出 END 事件。</span><span class="sxs-lookup"><span data-stu-id="279bf-224">You may have to try a few time ranges to find the END events.</span></span> <span data-ttu-id="279bf-225">END 事件也會包含工作階段的持續時間，也就是 START 事件時間和 END 事件時間之間的差異。</span><span class="sxs-lookup"><span data-stu-id="279bf-225">END events also contain the duration of the session - the difference between the START event time and END event time.</span></span> <span data-ttu-id="279bf-226">以下是 END 事件的資料範例：</span><span class="sxs-lookup"><span data-stu-id="279bf-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="279bf-227">雖然您輸入的時間值都是當地時間，但查詢所傳回的時間會是 UTC。</span><span class="sxs-lookup"><span data-stu-id="279bf-227">While the time values you enter are in local time, the time returned from the query is in UTC.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="279bf-228">停止拓撲</span><span class="sxs-lookup"><span data-stu-id="279bf-228">Stop the topology</span></span>

<span data-ttu-id="279bf-229">當您準備要停止拓撲時，請回到 Visual Studio 中的 **CorrelationTopology** 專案。</span><span class="sxs-lookup"><span data-stu-id="279bf-229">When you are ready to stop the topology, return to the **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="279bf-230">在 [Storm 拓撲檢視] 中，選取拓撲，然後使用拓撲檢視頂端的 [刪除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="279bf-230">In the **Storm Topology View**, select the topology and then use the **Kill** button at the top of the topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="279bf-231">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="279bf-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="279bf-232">後續步驟</span><span class="sxs-lookup"><span data-stu-id="279bf-232">Next steps</span></span>

<span data-ttu-id="279bf-233">如需更多 Storm 範例，請參閱 [Storm on HDInsight 上的範例拓撲](hdinsight-storm-example-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="279bf-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

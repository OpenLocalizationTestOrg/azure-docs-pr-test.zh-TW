---
title: "搭配使用 Apache Storm 與 Power BI - Azure HDInsight | Microsoft Docs"
description: "使用來自 HDInsight 中的 Apache Storm 叢集上執行的 C# 拓撲的資料建立 Power BI。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="76f1b-103">使用 Power BI 視覺化 Apache Storm 拓撲的資料</span><span class="sxs-lookup"><span data-stu-id="76f1b-103">Use Power BI to visualize data from an Apache Storm topology</span></span>

<span data-ttu-id="76f1b-104">Power BI 可讓您以視覺化的方式將資料顯示為報告。</span><span class="sxs-lookup"><span data-stu-id="76f1b-104">Power BI allows you to visually display data as reports.</span></span> <span data-ttu-id="76f1b-105">本文件提供如何使用 Apache Storm on HDInsight 為 Power BI 產生資料的範例。</span><span class="sxs-lookup"><span data-stu-id="76f1b-105">This document provides an example of how to use Apache Storm on HDInsight to generate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="76f1b-106">本文件中的步驟仰賴於含有 Visual Studio 的 Windows 開發環境。</span><span class="sxs-lookup"><span data-stu-id="76f1b-106">The steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="76f1b-107">已編譯的專案可以提交到以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="76f1b-107">The compiled project can be submitted to a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="76f1b-108">只有在 2016/10/28 之後建立的以 Linux 為基礎的叢集可支援 SCP.NET 拓撲。</span><span class="sxs-lookup"><span data-stu-id="76f1b-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="76f1b-109">若要搭配使用 C# 拓撲與以 Linux 為基礎的叢集，請將專案使用的 Microsoft.SCP.Net.SDK NuGet 套件，更新為 0.10.0.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="76f1b-109">To use a C# topology with a Linux-based cluster, update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span></span> <span data-ttu-id="76f1b-110">套件版本也必須符合 HDInsight 上安裝的 Storm 主要版本。</span><span class="sxs-lookup"><span data-stu-id="76f1b-110">The version of the package must also match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="76f1b-111">例如，Storm on HDInsight 3.3 和 3.4 版使用 Storm 0.10.x 版，而 HDInsight 3.5 使用 Storm 1.0.x。</span><span class="sxs-lookup"><span data-stu-id="76f1b-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="76f1b-112">在以 Linux 為基礎之叢集上的 C# 拓撲必須使用 .NET 4.5，並使用 Mono 以在 HDInsight 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="76f1b-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="76f1b-113">大多能正常運作。</span><span class="sxs-lookup"><span data-stu-id="76f1b-113">Most things work.</span></span> <span data-ttu-id="76f1b-114">不過您應該查看 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/)文件，以了解是否可能有不相容之處。</span><span class="sxs-lookup"><span data-stu-id="76f1b-114">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="76f1b-115">如需此專案的 Java 版本 (可在以 Linux 或 Windows 為基礎的 HDInsight 上運作)，請參閱[使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)](hdinsight-storm-develop-java-event-hub-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="76f1b-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76f1b-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="76f1b-116">Prerequisites</span></span>

* <span data-ttu-id="76f1b-117">具備 [Power BI](https://powerbi.com) 存取權的 Azure Active Directory 使用者。</span><span class="sxs-lookup"><span data-stu-id="76f1b-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="76f1b-118">HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="76f1b-118">An HDInsight cluster.</span></span> <span data-ttu-id="76f1b-119">如需詳細資訊，請參閱[開始使用 Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="76f1b-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="76f1b-120">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="76f1b-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="76f1b-121">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="76f1b-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="76f1b-122">Visual Studio (下列其中一個版本)</span><span class="sxs-lookup"><span data-stu-id="76f1b-122">Visual Studio (one of the following versions)</span></span>

  * <span data-ttu-id="76f1b-123">[Visual Studio 2012](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="76f1b-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="76f1b-124">Visual Studio 2013 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=44921) 或 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="76f1b-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="76f1b-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="76f1b-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="76f1b-126">Visual Studio 2017 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="76f1b-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="76f1b-127">HDInsight Tools for Visual Studio：如需安裝的相關資訊，請參閱 [開始使用 HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) 。</span><span class="sxs-lookup"><span data-stu-id="76f1b-127">The HDInsight Tools for Visual Studio: See [Get started using the HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="76f1b-128">運作方式</span><span class="sxs-lookup"><span data-stu-id="76f1b-128">How it works</span></span>

<span data-ttu-id="76f1b-129">此範例包含 C# Storm 拓撲，會隨機產生網際網路資訊服務 (IIS) 記錄資料。</span><span class="sxs-lookup"><span data-stu-id="76f1b-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="76f1b-130">然後此資料會寫入至 SQL Database，並且從該處用來在 Power BI 中產生報告。</span><span class="sxs-lookup"><span data-stu-id="76f1b-130">This data is then written to a SQL Database, and from there it is used to generate reports in Power BI.</span></span>

<span data-ttu-id="76f1b-131">下列檔案會實作此範例的主要功能︰</span><span class="sxs-lookup"><span data-stu-id="76f1b-131">The following files implement the main functionality of this example:</span></span>

* <span data-ttu-id="76f1b-132">**SqlAzureBolt.cs**︰將 Storm 拓撲中產生的資訊寫入 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="76f1b-132">**SqlAzureBolt.cs**: Writes information produced in the Storm topology to SQL Database.</span></span>
* <span data-ttu-id="76f1b-133">**IISLogsTable.sql**︰用來產生儲存資料所在的資料庫的 Transact-SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="76f1b-133">**IISLogsTable.sql**: The Transact-SQL statements used to generate the database that the data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="76f1b-134">在 HDInsight 叢集上啟動拓撲之前，先於 SQL Database 中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="76f1b-134">Create the table in SQL Database before starting the topology on your HDInsight cluster.</span></span>

## <a name="download-the-example"></a><span data-ttu-id="76f1b-135">下載範例</span><span class="sxs-lookup"><span data-stu-id="76f1b-135">Download the example</span></span>

<span data-ttu-id="76f1b-136">下載 [HDInsight C# Storm Power BI 範例](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi)。</span><span class="sxs-lookup"><span data-stu-id="76f1b-136">Download the [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="76f1b-137">若要下載它，請使用 [git](http://git-scm.com/)分岔/複製它，或使用 **下載** 連結下載封存的 .zip。</span><span class="sxs-lookup"><span data-stu-id="76f1b-137">To download it, either fork/clone it using [git](http://git-scm.com/), or use the **Download** link to download a .zip of the archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="76f1b-138">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="76f1b-138">Create a database</span></span>

1. <span data-ttu-id="76f1b-139">若要建立 SQL Database，請使用 [SQL Database 教學課程](../sql-database/sql-database-get-started.md)文件中的步驟。</span><span class="sxs-lookup"><span data-stu-id="76f1b-139">To create a database, use the steps in the [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="76f1b-140">遵循[使用 Visual Studio 連線至 SQL Database](../sql-database/sql-database-connect-query.md)文件中的步驟，連線至資料庫。</span><span class="sxs-lookup"><span data-stu-id="76f1b-140">Connect to the database by following the steps in the [Connect to a SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="76f1b-141">在 [物件總管] 中，以滑鼠右鍵按一下資料庫，然後選取 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="76f1b-141">In Object Explorer, right-click the database and select  **New Query**.</span></span> <span data-ttu-id="76f1b-142">將下載的專案中包含的 **IISLogsTable.sql** 檔案的內容，貼上至查詢視窗中，然後使用 Ctrl + Shift + E 來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="76f1b-142">Paste the contents of the **IISLogsTable.sql** file included in the downloaded project into the query window, and then use Ctrl + Shift + E to execute the query.</span></span> <span data-ttu-id="76f1b-143">您應該會收到已成功完成命令的訊息。</span><span class="sxs-lookup"><span data-stu-id="76f1b-143">You should receive a message that the commands completed successfully.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="76f1b-144">設定範例</span><span class="sxs-lookup"><span data-stu-id="76f1b-144">Configure the sample</span></span>

1. <span data-ttu-id="76f1b-145">從 [Azure 入口網站](https://portal.azure.com)中，選取您的 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="76f1b-145">From the [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="76f1b-146">從 [SQL Database] 刀鋒視窗的 [基本功能] 區段中，選取 [顯示資料庫連接字串]。</span><span class="sxs-lookup"><span data-stu-id="76f1b-146">From the **Essentials** section of the SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="76f1b-147">從顯示的清單中，複製 **ADO.NET (SQL 驗證)** 資訊。</span><span class="sxs-lookup"><span data-stu-id="76f1b-147">From the list that appears, copy the **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="76f1b-148">在 Visual Studio 中開啟範例。</span><span class="sxs-lookup"><span data-stu-id="76f1b-148">Open the sample in Visual Studio.</span></span> <span data-ttu-id="76f1b-149">從 [方案總管] 開啟 **App.config** 檔案，然後尋找下列項目：</span><span class="sxs-lookup"><span data-stu-id="76f1b-149">From **Solution Explorer**, open the **App.config** file, and then find the following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="76f1b-150">將 **##TOBEFILLED##** 值取代為上一個步驟中複製的資料庫連接字串。</span><span class="sxs-lookup"><span data-stu-id="76f1b-150">Replace the **##TOBEFILLED##** value with the database connection string copied in the previous step.</span></span> <span data-ttu-id="76f1b-151">將 **{your\_username}** 和 **{your\_password}** 取代為資料庫的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="76f1b-151">Replace **{your\_username}** and **{your\_password}** with the username and password for the database.</span></span>

3. <span data-ttu-id="76f1b-152">儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="76f1b-152">Save and close the files.</span></span>

## <a name="deploy-the-sample"></a><span data-ttu-id="76f1b-153">部署範例</span><span class="sxs-lookup"><span data-stu-id="76f1b-153">Deploy the sample</span></span>

1. <span data-ttu-id="76f1b-154">從 [方案總管]，以滑鼠右鍵按一下 **StormToSQL** 專案，然後選取 [提交至 Storm on HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="76f1b-154">From **Solution Explorer**, right-click the **StormToSQL** project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="76f1b-155">從 [Storm 叢集] 下拉式清單對話方塊選取 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="76f1b-155">Select the HDInsight cluster from the **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="76f1b-156">[ **Storm 叢集** ] 下拉式清單可能需要幾秒鐘的時間來填入伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="76f1b-156">It may take a few seconds for the **Storm Cluster** dropdown to populate with server names.</span></span>
   >
   > <span data-ttu-id="76f1b-157">如果出現提示，請輸入您 Azure 訂閱的登入認證。</span><span class="sxs-lookup"><span data-stu-id="76f1b-157">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="76f1b-158">如果您有多個訂用帳戶，請登入包含 Storm on HDInsight 叢集的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="76f1b-158">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="76f1b-159">提交拓撲之後，[拓撲檢視器] 便會隨即出現。</span><span class="sxs-lookup"><span data-stu-id="76f1b-159">When the topology has been submitted, the __Topology Viewer__ appears.</span></span> <span data-ttu-id="76f1b-160">若要檢視此拓撲，請從清單中選取 SqlAzureWriterTopology 項目。</span><span class="sxs-lookup"><span data-stu-id="76f1b-160">To view this topology, select the SqlAzureWriterTopology entry from the list.</span></span>

    ![已選取拓撲的拓撲](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="76f1b-162">您可以使用此檢視在拓撲中查看資訊，或按兩下項目 (例如 SqlAzureBolt)，以查看拓撲中元件的特定資訊。</span><span class="sxs-lookup"><span data-stu-id="76f1b-162">You can use this view to see information on the topology, or double-click an entry (such as the SqlAzureBolt) to see information specific to a component in the topology.</span></span>

3. <span data-ttu-id="76f1b-163">在拓撲執行幾分鐘之後，返回您用來建立資料庫的 SQL 查詢視窗。</span><span class="sxs-lookup"><span data-stu-id="76f1b-163">After the topology has ran for a few minutes, return to the SQL query window you used to create the database.</span></span> <span data-ttu-id="76f1b-164">以下列查詢取代現有陳述式：</span><span class="sxs-lookup"><span data-stu-id="76f1b-164">Replace the existing statements with the following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="76f1b-165">使用 Ctrl + Shift + E 來執行查詢，您應該會收到類似下列資料的結果：</span><span class="sxs-lookup"><span data-stu-id="76f1b-165">Use Ctrl + Shift + E to execute the query, and you should receive results similar to the following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="76f1b-166">這是從 Storm 拓撲寫入的資料。</span><span class="sxs-lookup"><span data-stu-id="76f1b-166">This data has been written from the Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="76f1b-167">建立報表</span><span class="sxs-lookup"><span data-stu-id="76f1b-167">Create a report</span></span>

1. <span data-ttu-id="76f1b-168">連接到適用於 Power BI 的 [Azure SQL Database 連接器](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) 。</span><span class="sxs-lookup"><span data-stu-id="76f1b-168">Connect to the [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="76f1b-169">在 [資料庫] 內，選取 [Get]。</span><span class="sxs-lookup"><span data-stu-id="76f1b-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="76f1b-170">選取 [Azure SQL Database]，然後選取 [連接]。</span><span class="sxs-lookup"><span data-stu-id="76f1b-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="76f1b-171">系統可能會要求您下載 Power BI Desktop 以繼續執行。</span><span class="sxs-lookup"><span data-stu-id="76f1b-171">You may be asked to download the Power BI Desktop to continue.</span></span> <span data-ttu-id="76f1b-172">若是如此，請使用下列步驟來連接：</span><span class="sxs-lookup"><span data-stu-id="76f1b-172">If so, use the following steps to connect:</span></span>
    >
    > 1. <span data-ttu-id="76f1b-173">開啟 Power BI Desktop 並選取 [取得資料]。</span><span class="sxs-lookup"><span data-stu-id="76f1b-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="76f1b-174">2  選取 __Azure__，然後選取 __Azure SQL Database__。</span><span class="sxs-lookup"><span data-stu-id="76f1b-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="76f1b-175">輸入資訊以連接到您的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="76f1b-175">Enter the information to connect to your Azure SQL Database.</span></span> <span data-ttu-id="76f1b-176">您可以造訪 [Azure 入口網站](https://portal.azure.com)，並且選取您的 SQL Database，以找到此資訊。</span><span class="sxs-lookup"><span data-stu-id="76f1b-176">You can find this information by visiting the [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="76f1b-177">您也可以從連接對話方塊使用 [啟用進階選項]，設定重新整理間隔和自訂篩選器。</span><span class="sxs-lookup"><span data-stu-id="76f1b-177">You can also set the refresh interval and custom filters by using **Enable Advanced Options** from the connect dialog.</span></span>

5. <span data-ttu-id="76f1b-178">連接之後，您會看到新的資料集具有與您連接的資料庫相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="76f1b-178">After you've connected, you will see a new dataset with the same name as the database you connected to.</span></span> <span data-ttu-id="76f1b-179">選取要開始設計報告的資料集。</span><span class="sxs-lookup"><span data-stu-id="76f1b-179">Select the dataset to begin designing a report.</span></span>

6. <span data-ttu-id="76f1b-180">從 [欄位] 展開 [IISLOGS] 項目。</span><span class="sxs-lookup"><span data-stu-id="76f1b-180">From **Fields**, expand the **IISLOGS** entry.</span></span> <span data-ttu-id="76f1b-181">若要建立列出 URI 主體的報告，請選取 **URISTEM** 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="76f1b-181">To create a report that lists the URI stems, select the checkbox for **URISTEM**.</span></span>

    ![建立報告](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="76f1b-183">接著，將 **方法** 拖曳至報告。</span><span class="sxs-lookup"><span data-stu-id="76f1b-183">Next, drag **METHOD** to the report.</span></span> <span data-ttu-id="76f1b-184">報告將會更新以列出主體和用於 HTTP 要求的對應 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="76f1b-184">The report updates to list the stems and the corresponding HTTP method used for the HTTP request.</span></span>

    ![新增方法資料](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="76f1b-186">從 [視覺效果] 資料行中，選取 [欄位] 圖示，然後選取 [值] 區段中 [方法] 旁的向下箭號。</span><span class="sxs-lookup"><span data-stu-id="76f1b-186">From the **Visualizations** column, select the **Fields** icon, and then select the down arrow next to **METHOD** in the **Values** section.</span></span> <span data-ttu-id="76f1b-187">若要顯示存取 URI 的次數，請選取 [計數]。</span><span class="sxs-lookup"><span data-stu-id="76f1b-187">To display a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![變更為方法的計數](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="76f1b-189">接下來，選取 [堆疊直條圖]  以變更資訊的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="76f1b-189">Next, select the **Stacked column chart** to change how the information is displayed.</span></span>

    ![變更堆疊圖表](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="76f1b-191">若要儲存報告，請選取 [儲存] 並輸入報告的名稱。</span><span class="sxs-lookup"><span data-stu-id="76f1b-191">To save the report, select **Save** and enter a name for the report.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="76f1b-192">停止拓撲</span><span class="sxs-lookup"><span data-stu-id="76f1b-192">Stop the topology</span></span>

<span data-ttu-id="76f1b-193">拓撲會繼續執行，直到您將它停止，或刪除 Storm on HDInsight 叢集為止。</span><span class="sxs-lookup"><span data-stu-id="76f1b-193">The topology continues to run until you stop it or delete the Storm on HDInsight cluster.</span></span> <span data-ttu-id="76f1b-194">若要停止拓撲，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="76f1b-194">To stop the topology, perform the following steps:</span></span>

1. <span data-ttu-id="76f1b-195">在 Visual Studio 中，返回拓撲檢視器並選取拓撲。</span><span class="sxs-lookup"><span data-stu-id="76f1b-195">In Visual Studio, return to the topology viewer and select the topology.</span></span>

2. <span data-ttu-id="76f1b-196">選取 [刪除]  按鈕以停止拓撲。</span><span class="sxs-lookup"><span data-stu-id="76f1b-196">Select the **Kill** button to stop the topology.</span></span>

    ![拓撲摘要上的刪除按鈕](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="76f1b-198">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="76f1b-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="76f1b-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="76f1b-199">Next steps</span></span>

<span data-ttu-id="76f1b-200">在本文件中，您已學會如何將資料從 Storm 拓撲傳送到 SQL Database，然後使用 Power BI 視覺化資料。</span><span class="sxs-lookup"><span data-stu-id="76f1b-200">In this document, you learned how to send data from a Storm topology to SQL Database, then visualize the data using Power BI.</span></span> <span data-ttu-id="76f1b-201">如需如何使用 Storm on HDInsight 以利用其他 Azure 技術的資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="76f1b-201">For information on how to work with other Azure technologies using Storm on HDInsight, see the following document:</span></span>

* [<span data-ttu-id="76f1b-202">Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="76f1b-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

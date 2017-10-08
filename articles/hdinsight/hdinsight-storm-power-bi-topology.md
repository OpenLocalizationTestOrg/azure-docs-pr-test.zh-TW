---
title: "使用 Power BI 的 Azure HDInsight Apache Storm aaaUse |Microsoft 文件"
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
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="53859-103">使用 Power BI toovisualize 資料從 Apache Storm 拓樸</span><span class="sxs-lookup"><span data-stu-id="53859-103">Use Power BI toovisualize data from an Apache Storm topology</span></span>

<span data-ttu-id="53859-104">Power BI 可讓您 toovisually 顯示的資料與報表。</span><span class="sxs-lookup"><span data-stu-id="53859-104">Power BI allows you toovisually display data as reports.</span></span> <span data-ttu-id="53859-105">本文件提供的範例 toouse Apache Storm 的 Power BI 的 HDInsight toogenerate 資料。</span><span class="sxs-lookup"><span data-stu-id="53859-105">This document provides an example of how toouse Apache Storm on HDInsight toogenerate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="53859-106">hello 本文件中的步驟會仰賴 Windows 與 Visual Studio 開發環境。</span><span class="sxs-lookup"><span data-stu-id="53859-106">hello steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="53859-107">hello 已編譯的專案可以提交的 tooa 以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="53859-107">hello compiled project can be submitted tooa Linux-based HDInsight cluster.</span></span> <span data-ttu-id="53859-108">只有在 2016/10/28 之後建立的以 Linux 為基礎的叢集可支援 SCP.NET 拓撲。</span><span class="sxs-lookup"><span data-stu-id="53859-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="53859-109">toouse 以 Linux 為基礎的叢集，而更新 hello Microsoft.SCP.Net.SDK NuGet 封裝使用您的專案 tooversion 0.10.0.6 或更高版本的 C# 拓撲。</span><span class="sxs-lookup"><span data-stu-id="53859-109">toouse a C# topology with a Linux-based cluster, update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or higher.</span></span> <span data-ttu-id="53859-110">hello hello 封裝版本也必須符合安裝在 HDInsight 上的 Storm hello 主要版本。</span><span class="sxs-lookup"><span data-stu-id="53859-110">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="53859-111">例如，Storm on HDInsight 3.3 和 3.4 版使用 Storm 0.10.x 版，而 HDInsight 3.5 使用 Storm 1.0.x。</span><span class="sxs-lookup"><span data-stu-id="53859-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="53859-112">C# 拓撲以 Linux 為基礎的叢集上必須使用.NET 4.5，並使用單聲道 toorun hello HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="53859-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="53859-113">大多能正常運作。</span><span class="sxs-lookup"><span data-stu-id="53859-113">Most things work.</span></span> <span data-ttu-id="53859-114">不過，您應該檢查 hello [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/)潛在的不相容的文件。</span><span class="sxs-lookup"><span data-stu-id="53859-114">However you should check hello [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="53859-115">如需此專案的 Java 版本 (可在以 Linux 或 Windows 為基礎的 HDInsight 上運作)，請參閱[使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)](hdinsight-storm-develop-java-event-hub-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="53859-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53859-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="53859-116">Prerequisites</span></span>

* <span data-ttu-id="53859-117">具備 [Power BI](https://powerbi.com) 存取權的 Azure Active Directory 使用者。</span><span class="sxs-lookup"><span data-stu-id="53859-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="53859-118">HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="53859-118">An HDInsight cluster.</span></span> <span data-ttu-id="53859-119">如需詳細資訊，請參閱[開始使用 Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="53859-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="53859-120">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="53859-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="53859-121">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="53859-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="53859-122">Visual Studio （其中 hello 之後版本）</span><span class="sxs-lookup"><span data-stu-id="53859-122">Visual Studio (one of hello following versions)</span></span>

  * <span data-ttu-id="53859-123">[Visual Studio 2012](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="53859-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="53859-124">Visual Studio 2013 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=44921) 或 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="53859-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="53859-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="53859-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="53859-126">Visual Studio 2017 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="53859-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="53859-127">hello HDInsight Tools for Visual Studio： 請參閱[開始使用 hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)如需安裝資訊。</span><span class="sxs-lookup"><span data-stu-id="53859-127">hello HDInsight Tools for Visual Studio: See [Get started using hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="53859-128">運作方式</span><span class="sxs-lookup"><span data-stu-id="53859-128">How it works</span></span>

<span data-ttu-id="53859-129">此範例包含 C# Storm 拓撲，會隨機產生網際網路資訊服務 (IIS) 記錄資料。</span><span class="sxs-lookup"><span data-stu-id="53859-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="53859-130">接著會將這項資料寫入 tooa SQL 資料庫，而且從該處使用的 toogenerate Power BI 中的報表。</span><span class="sxs-lookup"><span data-stu-id="53859-130">This data is then written tooa SQL Database, and from there it is used toogenerate reports in Power BI.</span></span>

<span data-ttu-id="53859-131">hello 遵循此範例的檔案實作 hello 主要功能：</span><span class="sxs-lookup"><span data-stu-id="53859-131">hello following files implement hello main functionality of this example:</span></span>

* <span data-ttu-id="53859-132">**SqlAzureBolt.cs**： 寫入 hello Storm 拓撲 tooSQL 資料庫中產生的資訊。</span><span class="sxs-lookup"><span data-stu-id="53859-132">**SqlAzureBolt.cs**: Writes information produced in hello Storm topology tooSQL Database.</span></span>
* <span data-ttu-id="53859-133">**IISLogsTable.sql**: hello TRANSACT-SQL 陳述式使用 toogenerate hello 儲存資料庫的 hello 資料中。</span><span class="sxs-lookup"><span data-stu-id="53859-133">**IISLogsTable.sql**: hello Transact-SQL statements used toogenerate hello database that hello data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="53859-134">建立 SQL Database 中的 hello 資料表，才可以開始您的 HDInsight 叢集 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="53859-134">Create hello table in SQL Database before starting hello topology on your HDInsight cluster.</span></span>

## <a name="download-hello-example"></a><span data-ttu-id="53859-135">下載 hello 範例</span><span class="sxs-lookup"><span data-stu-id="53859-135">Download hello example</span></span>

<span data-ttu-id="53859-136">下載 hello [HDInsight C# Storm Power BI 範例](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi)。</span><span class="sxs-lookup"><span data-stu-id="53859-136">Download hello [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="53859-137">toodownload，是分叉/複製使用[git](http://git-scm.com/)，或使用 hello**下載**連結 toodownload hello 封存的.zip。</span><span class="sxs-lookup"><span data-stu-id="53859-137">toodownload it, either fork/clone it using [git](http://git-scm.com/), or use hello **Download** link toodownload a .zip of hello archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="53859-138">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="53859-138">Create a database</span></span>

1. <span data-ttu-id="53859-139">toocreate 資料庫中，使用 hello hello 步驟[SQL Database 教學課程](../sql-database/sql-database-get-started.md)文件。</span><span class="sxs-lookup"><span data-stu-id="53859-139">toocreate a database, use hello steps in hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="53859-140">下列 hello 連接 toohello 資料庫步驟 hello [tooa SQL 資料庫連接使用 Visual Studio](../sql-database/sql-database-connect-query.md)文件。</span><span class="sxs-lookup"><span data-stu-id="53859-140">Connect toohello database by following hello steps in hello [Connect tooa SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="53859-141">在 [物件總管] 中，以滑鼠右鍵按一下 hello 資料庫，然後選取**新查詢**。</span><span class="sxs-lookup"><span data-stu-id="53859-141">In Object Explorer, right-click hello database and select  **New Query**.</span></span> <span data-ttu-id="53859-142">貼上 hello hello 內容**IISLogsTable.sql**檔案包含在 hello hello 查詢視窗中，下載專案，然後使用 Ctrl + Shift + E tooexecute hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="53859-142">Paste hello contents of hello **IISLogsTable.sql** file included in hello downloaded project into hello query window, and then use Ctrl + Shift + E tooexecute hello query.</span></span> <span data-ttu-id="53859-143">您應該會收到 hello 命令已順利完成的訊息。</span><span class="sxs-lookup"><span data-stu-id="53859-143">You should receive a message that hello commands completed successfully.</span></span>

## <a name="configure-hello-sample"></a><span data-ttu-id="53859-144">設定 hello 範例</span><span class="sxs-lookup"><span data-stu-id="53859-144">Configure hello sample</span></span>

1. <span data-ttu-id="53859-145">從 hello [Azure 入口網站](https://portal.azure.com)，選取您的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="53859-145">From hello [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="53859-146">從 hello **Essentials** hello SQL 資料庫刀鋒視窗中，選取部分**顯示資料庫的連接字串**。</span><span class="sxs-lookup"><span data-stu-id="53859-146">From hello **Essentials** section of hello SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="53859-147">從出現的 hello 清單，複製 hello **ADO.NET （SQL 驗證）**資訊。</span><span class="sxs-lookup"><span data-stu-id="53859-147">From hello list that appears, copy hello **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="53859-148">開啟 Visual Studio 中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="53859-148">Open hello sample in Visual Studio.</span></span> <span data-ttu-id="53859-149">從**方案總管 中**，開啟 hello **App.config**檔案，然後再尋找下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="53859-149">From **Solution Explorer**, open hello **App.config** file, and then find hello following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="53859-150">取代 hello **# # TOBEFILLED # #** hello 上一個步驟中複製的值與 hello 資料庫連接字串。</span><span class="sxs-lookup"><span data-stu-id="53859-150">Replace hello **##TOBEFILLED##** value with hello database connection string copied in hello previous step.</span></span> <span data-ttu-id="53859-151">取代**{您\_使用者名稱}**和**{您\_密碼}** hello 使用者名稱和密碼 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="53859-151">Replace **{your\_username}** and **{your\_password}** with hello username and password for hello database.</span></span>

3. <span data-ttu-id="53859-152">儲存並關閉 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="53859-152">Save and close hello files.</span></span>

## <a name="deploy-hello-sample"></a><span data-ttu-id="53859-153">部署 hello 範例</span><span class="sxs-lookup"><span data-stu-id="53859-153">Deploy hello sample</span></span>

1. <span data-ttu-id="53859-154">從**方案總管 中**，以滑鼠右鍵按一下 hello **StormToSQL**專案，然後選取**提交 HDInsight 上的 tooStorm**。</span><span class="sxs-lookup"><span data-stu-id="53859-154">From **Solution Explorer**, right-click hello **StormToSQL** project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="53859-155">選取 hello HDInsight 叢集的 hello **Storm 叢集**下拉式清單中的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="53859-155">Select hello HDInsight cluster from hello **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="53859-156">可能需要數秒鐘，讓 hello **Storm 叢集**下拉式 toopopulate 使用伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="53859-156">It may take a few seconds for hello **Storm Cluster** dropdown toopopulate with server names.</span></span>
   >
   > <span data-ttu-id="53859-157">如果出現提示，請輸入您的 Azure 訂閱 hello 登入認證。</span><span class="sxs-lookup"><span data-stu-id="53859-157">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="53859-158">如果您有多個訂用帳戶，登入另一個則包含您在 HDInsight 叢集的 Storm toohello。</span><span class="sxs-lookup"><span data-stu-id="53859-158">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="53859-159">當已送出 hello 拓樸時，hello__拓撲檢視器__隨即出現。</span><span class="sxs-lookup"><span data-stu-id="53859-159">When hello topology has been submitted, hello __Topology Viewer__ appears.</span></span> <span data-ttu-id="53859-160">tooview 此拓撲，從 [hello] 清單選取 hello SqlAzureWriterTopology 項目。</span><span class="sxs-lookup"><span data-stu-id="53859-160">tooview this topology, select hello SqlAzureWriterTopology entry from hello list.</span></span>

    ![hello 拓撲中，使用選取的 hello 拓撲](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="53859-162">您可以使用此檢視 toosee 資訊在 hello 拓撲中，或按兩下 hello 拓撲中的項目 （例如 hello SqlAzureBolt) toosee 資訊特定 tooa 元件。</span><span class="sxs-lookup"><span data-stu-id="53859-162">You can use this view toosee information on hello topology, or double-click an entry (such as hello SqlAzureBolt) toosee information specific tooa component in hello topology.</span></span>

3. <span data-ttu-id="53859-163">之後 hello 拓撲已執行幾分鐘的時間，傳回 toohello 用 toocreate hello 資料庫的 SQL 查詢視窗。</span><span class="sxs-lookup"><span data-stu-id="53859-163">After hello topology has ran for a few minutes, return toohello SQL query window you used toocreate hello database.</span></span> <span data-ttu-id="53859-164">取代下列查詢的 hello hello 現有陳述式：</span><span class="sxs-lookup"><span data-stu-id="53859-164">Replace hello existing statements with hello following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="53859-165">使用 Ctrl + Shift + E tooexecute hello 查詢，而且您應該會收到下列資料的結果類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="53859-165">Use Ctrl + Shift + E tooexecute hello query, and you should receive results similar toohello following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="53859-166">此資料已寫入 hello Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="53859-166">This data has been written from hello Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="53859-167">建立報表</span><span class="sxs-lookup"><span data-stu-id="53859-167">Create a report</span></span>

1. <span data-ttu-id="53859-168">連接 toohello [Azure SQL Database 連接器](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect)Power bi。</span><span class="sxs-lookup"><span data-stu-id="53859-168">Connect toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="53859-169">在 [資料庫] 內，選取 [Get]。</span><span class="sxs-lookup"><span data-stu-id="53859-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="53859-170">選取 [Azure SQL Database]，然後選取 [連接]。</span><span class="sxs-lookup"><span data-stu-id="53859-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="53859-171">您可能會要求 toodownload hello Power BI Desktop toocontinue。</span><span class="sxs-lookup"><span data-stu-id="53859-171">You may be asked toodownload hello Power BI Desktop toocontinue.</span></span> <span data-ttu-id="53859-172">若是如此，請使用下列步驟 tooconnect hello:</span><span class="sxs-lookup"><span data-stu-id="53859-172">If so, use hello following steps tooconnect:</span></span>
    >
    > 1. <span data-ttu-id="53859-173">開啟 Power BI Desktop 並選取 [取得資料]。</span><span class="sxs-lookup"><span data-stu-id="53859-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="53859-174">2  選取 __Azure__，然後選取 __Azure SQL Database__。</span><span class="sxs-lookup"><span data-stu-id="53859-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="53859-175">輸入 hello 資訊 tooconnect tooyour Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="53859-175">Enter hello information tooconnect tooyour Azure SQL Database.</span></span> <span data-ttu-id="53859-176">您可以找到此資訊，請瀏覽 hello [Azure 入口網站](https://portal.azure.com)，然後選取您的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="53859-176">You can find this information by visiting hello [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="53859-177">您也可以透過設定 hello 重新整理間隔，自訂篩選器**啟用進階選項**hello 從連接對話方塊。</span><span class="sxs-lookup"><span data-stu-id="53859-177">You can also set hello refresh interval and custom filters by using **Enable Advanced Options** from hello connect dialog.</span></span>

5. <span data-ttu-id="53859-178">您已連接之後，您會看到新的資料集，以相同的名稱，做為 hello 資料庫連接到您的 hello。</span><span class="sxs-lookup"><span data-stu-id="53859-178">After you've connected, you will see a new dataset with hello same name as hello database you connected to.</span></span> <span data-ttu-id="53859-179">選取 hello 資料集 toobegin 設計報表。</span><span class="sxs-lookup"><span data-stu-id="53859-179">Select hello dataset toobegin designing a report.</span></span>

6. <span data-ttu-id="53859-180">從**欄位**，依序展開 hello **IISLOGS**項目。</span><span class="sxs-lookup"><span data-stu-id="53859-180">From **Fields**, expand hello **IISLOGS** entry.</span></span> <span data-ttu-id="53859-181">toocreate 源自報表清單 hello URI，選取 hello 核取方塊**URISTEM**。</span><span class="sxs-lookup"><span data-stu-id="53859-181">toocreate a report that lists hello URI stems, select hello checkbox for **URISTEM**.</span></span>

    ![建立報告](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="53859-183">下一步，拖曳**方法**toohello 報表。</span><span class="sxs-lookup"><span data-stu-id="53859-183">Next, drag **METHOD** toohello report.</span></span> <span data-ttu-id="53859-184">源自 hello 報表更新 toolist hello 與 hello 對應的 HTTP 方法使用 hello HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="53859-184">hello report updates toolist hello stems and hello corresponding HTTP method used for hello HTTP request.</span></span>

    ![將資料加入 hello 方法](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="53859-186">從 hello**視覺效果**資料行中，選取 hello**欄位**圖示，然後選取 hello 向下箭號旁太**方法**在 hello**值**> 一節。</span><span class="sxs-lookup"><span data-stu-id="53859-186">From hello **Visualizations** column, select hello **Fields** icon, and then select hello down arrow next too**METHOD** in hello **Values** section.</span></span> <span data-ttu-id="53859-187">toodisplay 存取的多少次 URI 計數後，選取**計數**。</span><span class="sxs-lookup"><span data-stu-id="53859-187">toodisplay a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![變更 tooa 計數的方法](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="53859-189">接下來，選取 hello**堆疊直條圖**toochange hello 資訊的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="53859-189">Next, select hello **Stacked column chart** toochange how hello information is displayed.</span></span>

    ![變更 tooa 堆疊的圖表](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="53859-191">toosave hello 報表中，選取**儲存**，然後輸入 hello 報表的名稱。</span><span class="sxs-lookup"><span data-stu-id="53859-191">toosave hello report, select **Save** and enter a name for hello report.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="53859-192">停止 hello 拓樸</span><span class="sxs-lookup"><span data-stu-id="53859-192">Stop hello topology</span></span>

<span data-ttu-id="53859-193">hello 拓撲會繼續執行 toorun，直到您將它停止或刪除 hello Storm HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="53859-193">hello topology continues toorun until you stop it or delete hello Storm on HDInsight cluster.</span></span> <span data-ttu-id="53859-194">toostop hello 拓撲中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="53859-194">toostop hello topology, perform hello following steps:</span></span>

1. <span data-ttu-id="53859-195">在 Visual Studio 中，傳回 toohello 拓撲檢視器，然後選取 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="53859-195">In Visual Studio, return toohello topology viewer and select hello topology.</span></span>

2. <span data-ttu-id="53859-196">選取 hello **Kill**按鈕 toostop hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="53859-196">Select hello **Kill** button toostop hello topology.</span></span>

    ![Kill hello 拓樸摘要 按鈕](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="53859-198">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="53859-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="53859-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53859-199">Next steps</span></span>

<span data-ttu-id="53859-200">在本文件中，您學到如何 toosend 資料從 Storm 拓撲 tooSQL 資料庫，然後視覺效果顯示 hello 使用 Power BI 的資料。</span><span class="sxs-lookup"><span data-stu-id="53859-200">In this document, you learned how toosend data from a Storm topology tooSQL Database, then visualize hello data using Power BI.</span></span> <span data-ttu-id="53859-201">如需詳細資訊與其他 Azure 技術在 HDInsight 上使用 Storm toowork，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="53859-201">For information on how toowork with other Azure technologies using Storm on HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="53859-202">Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="53859-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

---
title: "使用 Windows PC 搭配 Hadoop on HDInsight - Azure | Microsoft Docs"
description: "從 Hadoop on HDInsight 中的 Windows PC 作業。 使用 PowerShell、Visual Studio 和 Linux 工具來管理和查詢叢集。 使用 .NET 開發巨量資料解決方案。"
services: hdinsight
keywords: "windows 上的 hadoop,適用於 windows 的 hadoop"
author: cjgronlund
manager: jhubbard
ms.author: cgronlun
ms.date: 05/17/2017
ms.topic: article
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.openlocfilehash: e4f231c1f9b903d6cc7f2b062b30d2a072be8493
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="work-in-the-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a><span data-ttu-id="aaaba-106">從 Windows PC 在 HDInsight 上的 Hadoop 生態系統中作業</span><span class="sxs-lookup"><span data-stu-id="aaaba-106">Work in the Hadoop ecosystem on HDInsight from a Windows PC</span></span>

<span data-ttu-id="aaaba-107">深入了解 Windows 電腦上的開發和管理選項，以便在 HDInsight 上的 Hadoop 生態系統中作業。</span><span class="sxs-lookup"><span data-stu-id="aaaba-107">Learn about development and management options on the Windows PC for working in the Hadoop ecosystem on HDInsight.</span></span> 

<span data-ttu-id="aaaba-108">HDInsight 是以 Apache Hadoop 和 Hadoop 元件為基礎，採用在 Linux 上開發的開放原始碼技術。</span><span class="sxs-lookup"><span data-stu-id="aaaba-108">HDInsight is based on Apache Hadoop and Hadoop components, open-source technologies developed on Linux.</span></span> <span data-ttu-id="aaaba-109">HDInsight 3.4 版及更新版本會使用 Ubuntu Linux 發行版本作為叢集的基礎作業系統。</span><span class="sxs-lookup"><span data-stu-id="aaaba-109">HDInsight version 3.4 and higher uses the Ubuntu Linux distribution as the underlying OS for the cluster.</span></span> <span data-ttu-id="aaaba-110">不過，您可以從 Windows 用戶端或 Windows 開發環境使用 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="aaaba-110">However, you can work with HDInsight from a Windows client or Windows development environment.</span></span>

## <a name="use-powershell-for-deployment-and-management-tasks"></a><span data-ttu-id="aaaba-111">使用 PowerShell 進行部署和管理工作</span><span class="sxs-lookup"><span data-stu-id="aaaba-111">Use PowerShell for deployment and management tasks</span></span>
<span data-ttu-id="aaaba-112">Azure PowerShell 是一種指令碼環境，可讓您從 Windows 在 HDInsight 中用來控制及自動執行部署和管理工作。</span><span class="sxs-lookup"><span data-stu-id="aaaba-112">Azure PowerShell is a scripting environment that you can use to control and automate deployment and management tasks in HDInsight from Windows.</span></span>

<span data-ttu-id="aaaba-113">您可以使用 PowerShell 執行的工作範例︰</span><span class="sxs-lookup"><span data-stu-id="aaaba-113">Examples of tasks you can do with PowerShell:</span></span>

* [<span data-ttu-id="aaaba-114">使用 PowerShell 建立叢集</span><span class="sxs-lookup"><span data-stu-id="aaaba-114">Create clusters using PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="aaaba-115">使用 PowerShell 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="aaaba-115">Run Hive queries using PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="aaaba-116">使用 PowerShell 管理叢集</span><span class="sxs-lookup"><span data-stu-id="aaaba-116">Manage clusters with PowerShell</span></span>](hdinsight-administer-use-powershell.md)

<span data-ttu-id="aaaba-117">請遵循步驟來[安裝和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) 以取得最新的版本。</span><span class="sxs-lookup"><span data-stu-id="aaaba-117">Follow steps to [install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to get the latest version.</span></span> <span data-ttu-id="aaaba-118">如果您需要修改指令碼才能使用適用於 Azure Resource Manager 的新 Cmdlet，請參閱[移轉至以 Azure Resource Manager 為基礎的開發工具 (適用於 HDInsight 叢集)](hdinsight-hadoop-development-using-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="aaaba-118">If you have scripts that need to be modified to use the new cmdlets for Azure Resource Manager, see [Migrate to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md).</span></span>

## <a name="utilities-you-can-run-in-a-browser"></a><span data-ttu-id="aaaba-119">您可以在瀏覽器中執行的公用程式</span><span class="sxs-lookup"><span data-stu-id="aaaba-119">Utilities you can run in a browser</span></span>
<span data-ttu-id="aaaba-120">下列公用程式具有可在瀏覽器中執行的 Web UI：</span><span class="sxs-lookup"><span data-stu-id="aaaba-120">The following utilities have a web UI that runs in a browser:</span></span>
* <span data-ttu-id="aaaba-121">**[Azure Cloud Shell (預覽)](https://docs.microsoft.com/azure/cloud-shell/quickstart)** 是可在瀏覽器中以及從 Azure 入口網站執行的互動式、命令列殼層。</span><span class="sxs-lookup"><span data-stu-id="aaaba-121">**[Azure Cloud Shell (preview)](https://docs.microsoft.com/azure/cloud-shell/quickstart)** is an interactive, command-line shell that runs in your browser and from within the Azure portal.</span></span>
* <span data-ttu-id="aaaba-122">**[Ambari Web UI](hdinsight-hadoop-manage-ambari.md)** 是 Azure 入口網站中可用的管理和監視公用程式，可用來管理不同種類的工作，例如︰</span><span class="sxs-lookup"><span data-stu-id="aaaba-122">**[Ambari Web UI](hdinsight-hadoop-manage-ambari.md)** is a management and monitoring utility available in the Azure portal that can be used to manage different kinds of jobs, such as:</span></span>
    * [<span data-ttu-id="aaaba-123">使用 Ambari 搭配 REST API</span><span class="sxs-lookup"><span data-stu-id="aaaba-123">Use Ambari with the REST API</span></span>](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [<span data-ttu-id="aaaba-124">Ambari 中的 Hive 檢視</span><span class="sxs-lookup"><span data-stu-id="aaaba-124">Hive View in Ambari</span></span>](hdinsight-hadoop-use-hive-ambari-view.md)
    * [<span data-ttu-id="aaaba-125">Ambari 中的 Tez 檢視</span><span class="sxs-lookup"><span data-stu-id="aaaba-125">Tez View in Ambari</span></span>](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a><span data-ttu-id="aaaba-126">Data Lake (Hadoop) Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aaaba-126">Data Lake (Hadoop) Tools for Visual Studio</span></span>
<span data-ttu-id="aaaba-127">使用 Data Lake Tools for Visual Studio 來部署和管理 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="aaaba-127">Use Data Lake Tools for Visual Studio to deploy and manage Storm topologies.</span></span> <span data-ttu-id="aaaba-128">Data Lake Tools 也會安裝 SCP.NET SDK，其可讓您使用 Visual Studio 開發 C# Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="aaaba-128">Data Lake Tools also installs the SCP.NET SDK, which allows you to develop C# Storm topologies with Visual Studio.</span></span>

<span data-ttu-id="aaaba-129">在您進行下列範例之前，請[安裝並嘗試 Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="aaaba-129">Before you go to the following examples, [install and try Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span> 

<span data-ttu-id="aaaba-130">您可以使用 Visual Studio 和 Data Lake Tools for Visual Studio 執行的工作範例︰</span><span class="sxs-lookup"><span data-stu-id="aaaba-130">Examples of tasks you can do with Visual Studio and Data Lake Tools for Visual Studio:</span></span>
* [<span data-ttu-id="aaaba-131">從 Visual Studio 部署和管理 Storm 拓撲</span><span class="sxs-lookup"><span data-stu-id="aaaba-131">Deploy and manage Storm topologies from Visual Studio</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
* <span data-ttu-id="aaaba-132">[使用 Visual Studio 開發 Storm 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="aaaba-132">[Develop C# topologies for Storm using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span> <span data-ttu-id="aaaba-133">其中包含您可以連接到資料庫 (例如 Azure Cosmos DB 和 SQL Database) 之 Storm 拓撲的範例範本。</span><span class="sxs-lookup"><span data-stu-id="aaaba-133">The bits include example templates for Storm topologies you can connect to databases, such as Azure Cosmos DB and SQL Database.</span></span>

## <a name="visual-studio-and-the-net-sdk"></a><span data-ttu-id="aaaba-134">Visual Studio 和 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="aaaba-134">Visual Studio and the .NET SDK</span></span> 

<span data-ttu-id="aaaba-135">您可以使用 Visual Studio 搭配 .NET SDK 來管理叢集和開發巨量資料應用程式。</span><span class="sxs-lookup"><span data-stu-id="aaaba-135">You can use Visual Studio with the .NET SDK to manage clusters and develop big data applications.</span></span> <span data-ttu-id="aaaba-136">您可以將其他 IDE 用於下列工作，但範例顯示在 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="aaaba-136">You can use other IDEs for the following tasks, but examples are shown in Visual Studio.</span></span>

<span data-ttu-id="aaaba-137">您可以在 Visual Studio 中使用 .NET SDK 執行的工作範例︰</span><span class="sxs-lookup"><span data-stu-id="aaaba-137">Examples of tasks you can do with the .NET SDK in Visual Studio:</span></span>
* [<span data-ttu-id="aaaba-138">從 .NET Framework 應用程式在 HDInsight 中建立和使用叢集</span><span class="sxs-lookup"><span data-stu-id="aaaba-138">Create clusters and work in HDInsight from a .NET Framework application</span></span>](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [<span data-ttu-id="aaaba-139">使用 .NET SDK 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="aaaba-139">Run Hive queries using the .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [<span data-ttu-id="aaaba-140">使用 C# 使用者定義的函式搭配 Hadoop 上的 Hive 和 Pig 串流</span><span class="sxs-lookup"><span data-stu-id="aaaba-140">Use C# user-defined functions with Hive and Pig streaming on Hadoop</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> <span data-ttu-id="aaaba-141">提示：如果您執行的 .NET 方案具有以 Windows 為基礎的 HDInsight 叢集，現在是規劃移轉至以 Linux 為基礎的叢集的好時機。</span><span class="sxs-lookup"><span data-stu-id="aaaba-141">TIP If you're running .NET solutions with Windows-based HDInsight clusters, it's a good time to plan a migration to Linux-based clusters.</span></span> <span data-ttu-id="aaaba-142">如需詳細資訊，請參閱[將以 Windows 為基礎的 HDInsight 適用的 .NET 方案移轉至以 Linux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="aaaba-142">For more information, see [Migrate .NET solution for Windows-based HDInsight to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span></span>

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a><span data-ttu-id="aaaba-143">適用於 Spark 叢集的 Intellij IDEA 和 Eclipse IDE</span><span class="sxs-lookup"><span data-stu-id="aaaba-143">Intellij IDEA and Eclipse IDE for Spark clusters</span></span>
<span data-ttu-id="aaaba-144">[Intellij IDEA](https://www.jetbrains.com/idea/download) 和 [Eclipse IDE](https://www.eclipse.org/downloads/) 都可以用來︰</span><span class="sxs-lookup"><span data-stu-id="aaaba-144">Both [Intellij IDEA](https://www.jetbrains.com/idea/download) and the [Eclipse IDE](https://www.eclipse.org/downloads/) can be used to:</span></span>
* <span data-ttu-id="aaaba-145">在 HDInsight Spark 叢集上開發並提交 Scala Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aaaba-145">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="aaaba-146">存取 Spark 叢集資源。</span><span class="sxs-lookup"><span data-stu-id="aaaba-146">Access Spark cluster resources.</span></span>
* <span data-ttu-id="aaaba-147">在本機開發並執行 Scala Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aaaba-147">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="aaaba-148">這些文章顯示如何︰</span><span class="sxs-lookup"><span data-stu-id="aaaba-148">These articles show how:</span></span> 
* <span data-ttu-id="aaaba-149">Intellij IDEA︰[使用 Azure Toolkit for Intellij 外掛程式和 Scala SDK 建立 Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)。</span><span class="sxs-lookup"><span data-stu-id="aaaba-149">Intellij IDEA: [Create Spark applications using the Azure Toolkit for Intellij plug-in and the Scala SDK.](hdinsight-apache-spark-intellij-tool-plugin.md)</span></span>
* <span data-ttu-id="aaaba-150">Eclipse IDE 或 Scala IDE for Eclipse：[建立 Spark 應用程式和 Azure Toolkit for Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="aaaba-150">Eclipse IDE or Scala IDE for Eclipse: [Create Spark applications and the Azure Toolkit for Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)</span></span> 


## <a name="notebooks-on-spark-for-data-scientists"></a><span data-ttu-id="aaaba-151">適用於資料科學家的 Spark Notebook</span><span class="sxs-lookup"><span data-stu-id="aaaba-151">Notebooks on Spark for data scientists</span></span> 
<span data-ttu-id="aaaba-152">HDInsight 中的 Apache Spark 叢集包含可搭配 Jupyter Notebook 使用的 Zeppelin Notebook 和核心。</span><span class="sxs-lookup"><span data-stu-id="aaaba-152">Apache Spark clusters in HDInsight include Zeppelin notebooks and kernels that can be used with Jupyter notebooks.</span></span> 

* [<span data-ttu-id="aaaba-153">了解如何使用 Spark 叢集上的核心搭配 Jupyter Notebook 來測試 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="aaaba-153">Learn how to use kernels on Spark clusters with Jupyter notebooks to test Spark applications</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="aaaba-154">了解如何使用 Spark 叢集上的 Zeppelin Notebook 來執行 Spark 作業</span><span class="sxs-lookup"><span data-stu-id="aaaba-154">Learn how to use Zeppelin notebooks on Spark clusters to run Spark jobs</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a><span data-ttu-id="aaaba-155">在 Windows 上執行以 Linux 為基礎的工具和技術</span><span class="sxs-lookup"><span data-stu-id="aaaba-155">Run Linux-based tools and technologies on Windows</span></span>

<span data-ttu-id="aaaba-156">如果您遇到必須使用只適用於 Linux 之工具或技術的情況，請考慮下列選項︰</span><span class="sxs-lookup"><span data-stu-id="aaaba-156">If you encounter a situation where you must use a tool or technology that is only available on Linux, consider the following options:</span></span>

* <span data-ttu-id="aaaba-157">**Windows 10 上的 Bash (Beta 版)** 在 Windows 上提供 Linux 子系統。</span><span class="sxs-lookup"><span data-stu-id="aaaba-157">**Bash (beta) on Windows 10** provides a Linux subsystem on Windows.</span></span> <span data-ttu-id="aaaba-158">Bash 可讓您直接執行 Linux 公用程式，而不必維護專用的 Linux 安裝。</span><span class="sxs-lookup"><span data-stu-id="aaaba-158">Bash allows you to directly run Linux utilities without having to maintain a dedicated Linux installation.</span></span> [<span data-ttu-id="aaaba-159">在 Windows 10 上安裝和執行 Bash Beta 版</span><span class="sxs-lookup"><span data-stu-id="aaaba-159">Install and run the Bash beta on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/install_guide)
* <span data-ttu-id="aaaba-160">**Docker for Windows** 可供存取許多以 Linux 為基礎的工具，並可以直接從 Windows 執行。</span><span class="sxs-lookup"><span data-stu-id="aaaba-160">**Docker for Windows** provides access to many Linux-based tools, and can be run directly from Windows.</span></span> <span data-ttu-id="aaaba-161">例如，您可以使用 Docker 直接從 Windows 執行 Hive 適用的 Beeline 用戶端。</span><span class="sxs-lookup"><span data-stu-id="aaaba-161">For example, you can use Docker to run the Beeline client for Hive directly from Windows.</span></span> <span data-ttu-id="aaaba-162">您也可以使用 Docker 來執行本機 Jupyter Notebook，並從遠端連線到 HDInsight 上的 Spark。</span><span class="sxs-lookup"><span data-stu-id="aaaba-162">You can also use Docker to run a local Jupyter notebook and remotely connect to Spark on HDInsight.</span></span> [<span data-ttu-id="aaaba-163">開始使用 Docker for Windows</span><span class="sxs-lookup"><span data-stu-id="aaaba-163">Get started with Docker for Windows</span></span>](https://docs.docker.com/docker-for-windows/)
* <span data-ttu-id="aaaba-164">**[MobaXTerm](http://mobaxterm.mobatek.net/)** 可讓您透過 SSH 連線，以圖形方式瀏覽叢集檔案系統。</span><span class="sxs-lookup"><span data-stu-id="aaaba-164">**[MobaXTerm](http://mobaxterm.mobatek.net/)** allows you to graphically browse the cluster file system over an SSH connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaaba-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aaaba-165">Next steps</span></span>
<span data-ttu-id="aaaba-166">如果您不熟悉使用以 Linux 為基礎的叢集，請參閱下列文章︰</span><span class="sxs-lookup"><span data-stu-id="aaaba-166">If you're new to working in Linux-based clusters, see the follow articles:</span></span>
* [<span data-ttu-id="aaaba-167">設定 Hadoop、Kafka、Spark 或其他叢集</span><span class="sxs-lookup"><span data-stu-id="aaaba-167">Set up Hadoop, Kafka, Spark, or other clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="aaaba-168">Linux 上的 HDInsight 叢集祕訣</span><span class="sxs-lookup"><span data-stu-id="aaaba-168">Tips for HDInsight clusters on Linux</span></span>](hdinsight-hadoop-linux-information.md)
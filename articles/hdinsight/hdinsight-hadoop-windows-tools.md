---
title: "aaaUse Windows PC 的 Hadoop HDInsight 的 Azure 上 |Microsoft 文件"
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
ms.openlocfilehash: 7c93f16e93349c0b8fb1abd55320c2c172b93aa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="work-in-hello-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a><span data-ttu-id="acaf0-106">在 hello HDInsight 的 Windows pc 的 Hadoop 生態系統</span><span class="sxs-lookup"><span data-stu-id="acaf0-106">Work in hello Hadoop ecosystem on HDInsight from a Windows PC</span></span>

<span data-ttu-id="acaf0-107">深入了解開發和管理 hello Windows 電腦上的選項，在 HDInsight 上的 hello Hadoop 生態系統中使用。</span><span class="sxs-lookup"><span data-stu-id="acaf0-107">Learn about development and management options on hello Windows PC for working in hello Hadoop ecosystem on HDInsight.</span></span> 

<span data-ttu-id="acaf0-108">HDInsight 是以 Apache Hadoop 和 Hadoop 元件為基礎，採用在 Linux 上開發的開放原始碼技術。</span><span class="sxs-lookup"><span data-stu-id="acaf0-108">HDInsight is based on Apache Hadoop and Hadoop components, open-source technologies developed on Linux.</span></span> <span data-ttu-id="acaf0-109">HDInsight 版本 3.4 及更新版本為 hello 基礎 OS hello 叢集使用 hello Ubuntu Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="acaf0-109">HDInsight version 3.4 and higher uses hello Ubuntu Linux distribution as hello underlying OS for hello cluster.</span></span> <span data-ttu-id="acaf0-110">不過，您可以從 Windows 用戶端或 Windows 開發環境使用 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="acaf0-110">However, you can work with HDInsight from a Windows client or Windows development environment.</span></span>

## <a name="use-powershell-for-deployment-and-management-tasks"></a><span data-ttu-id="acaf0-111">使用 PowerShell 進行部署和管理工作</span><span class="sxs-lookup"><span data-stu-id="acaf0-111">Use PowerShell for deployment and management tasks</span></span>
<span data-ttu-id="acaf0-112">Azure PowerShell 是指令碼環境，您可以使用 toocontrol，並從 Windows 的 HDInsight 中的部署和管理工作自動化。</span><span class="sxs-lookup"><span data-stu-id="acaf0-112">Azure PowerShell is a scripting environment that you can use toocontrol and automate deployment and management tasks in HDInsight from Windows.</span></span>

<span data-ttu-id="acaf0-113">您可以使用 PowerShell 執行的工作範例︰</span><span class="sxs-lookup"><span data-stu-id="acaf0-113">Examples of tasks you can do with PowerShell:</span></span>

* [<span data-ttu-id="acaf0-114">使用 PowerShell 建立叢集</span><span class="sxs-lookup"><span data-stu-id="acaf0-114">Create clusters using PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="acaf0-115">使用 PowerShell 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="acaf0-115">Run Hive queries using PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="acaf0-116">使用 PowerShell 管理叢集</span><span class="sxs-lookup"><span data-stu-id="acaf0-116">Manage clusters with PowerShell</span></span>](hdinsight-administer-use-powershell.md)

<span data-ttu-id="acaf0-117">請依照下列步驟太[安裝和設定 Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooget hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="acaf0-117">Follow steps too[install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooget hello latest version.</span></span> <span data-ttu-id="acaf0-118">如果您有 Azure 資源管理員的需要修改 toobe toouse hello 新 cmdlet 的指令碼，請參閱[移轉 tooAzure HDInsight 叢集的資源管理員為基礎的開發工具](hdinsight-hadoop-development-using-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="acaf0-118">If you have scripts that need toobe modified toouse hello new cmdlets for Azure Resource Manager, see [Migrate tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md).</span></span>

## <a name="utilities-you-can-run-in-a-browser"></a><span data-ttu-id="acaf0-119">您可以在瀏覽器中執行的公用程式</span><span class="sxs-lookup"><span data-stu-id="acaf0-119">Utilities you can run in a browser</span></span>
<span data-ttu-id="acaf0-120">hello 下列公用程式有 web 瀏覽器中執行的 UI:</span><span class="sxs-lookup"><span data-stu-id="acaf0-120">hello following utilities have a web UI that runs in a browser:</span></span>
* <span data-ttu-id="acaf0-121">**[Azure 雲端殼層 （預覽）](https://docs.microsoft.com/azure/cloud-shell/quickstart)** 是在您的瀏覽器中執行互動式的命令列殼層和從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="acaf0-121">**[Azure Cloud Shell (preview)](https://docs.microsoft.com/azure/cloud-shell/quickstart)** is an interactive, command-line shell that runs in your browser and from within hello Azure portal.</span></span>
* <span data-ttu-id="acaf0-122">**[Ambari Web UI](hdinsight-hadoop-manage-ambari.md)** 是管理與監視公用程式，可在 hello Azure 入口網站，可以是使用的 toomanage 不同種類的工作，例如：</span><span class="sxs-lookup"><span data-stu-id="acaf0-122">**[Ambari Web UI](hdinsight-hadoop-manage-ambari.md)** is a management and monitoring utility available in hello Azure portal that can be used toomanage different kinds of jobs, such as:</span></span>
    * [<span data-ttu-id="acaf0-123">使用 Ambari 以 hello REST API</span><span class="sxs-lookup"><span data-stu-id="acaf0-123">Use Ambari with hello REST API</span></span>](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [<span data-ttu-id="acaf0-124">Ambari 中的 Hive 檢視</span><span class="sxs-lookup"><span data-stu-id="acaf0-124">Hive View in Ambari</span></span>](hdinsight-hadoop-use-hive-ambari-view.md)
    * [<span data-ttu-id="acaf0-125">Ambari 中的 Tez 檢視</span><span class="sxs-lookup"><span data-stu-id="acaf0-125">Tez View in Ambari</span></span>](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a><span data-ttu-id="acaf0-126">Data Lake (Hadoop) Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="acaf0-126">Data Lake (Hadoop) Tools for Visual Studio</span></span>
<span data-ttu-id="acaf0-127">使用 Data Lake Tools for Visual Studio toodeploy 及管理 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="acaf0-127">Use Data Lake Tools for Visual Studio toodeploy and manage Storm topologies.</span></span> <span data-ttu-id="acaf0-128">資料湖工具也會安裝 hello SCP.NET SDK，可讓您使用 Visual Studio toodevelop C# Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="acaf0-128">Data Lake Tools also installs hello SCP.NET SDK, which allows you toodevelop C# Storm topologies with Visual Studio.</span></span>

<span data-ttu-id="acaf0-129">繼續遵循範例，toohello 之前[安裝，然後嘗試 Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="acaf0-129">Before you go toohello following examples, [install and try Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span> 

<span data-ttu-id="acaf0-130">您可以使用 Visual Studio 和 Data Lake Tools for Visual Studio 執行的工作範例︰</span><span class="sxs-lookup"><span data-stu-id="acaf0-130">Examples of tasks you can do with Visual Studio and Data Lake Tools for Visual Studio:</span></span>
* [<span data-ttu-id="acaf0-131">從 Visual Studio 部署和管理 Storm 拓撲</span><span class="sxs-lookup"><span data-stu-id="acaf0-131">Deploy and manage Storm topologies from Visual Studio</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
* <span data-ttu-id="acaf0-132">[使用 Visual Studio 開發 Storm 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="acaf0-132">[Develop C# topologies for Storm using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span> <span data-ttu-id="acaf0-133">hello 位元包含範例範本 Storm 拓撲中，您可以連接 toodatabases，例如 Azure Cosmos DB 和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="acaf0-133">hello bits include example templates for Storm topologies you can connect toodatabases, such as Azure Cosmos DB and SQL Database.</span></span>

## <a name="visual-studio-and-hello-net-sdk"></a><span data-ttu-id="acaf0-134">Visual Studio 和 hello.NET SDK</span><span class="sxs-lookup"><span data-stu-id="acaf0-134">Visual Studio and hello .NET SDK</span></span> 

<span data-ttu-id="acaf0-135">您可以使用 Visual Studio 與 hello.NET SDK toomanage 叢集，並開發巨量資料的應用程式。</span><span class="sxs-lookup"><span data-stu-id="acaf0-135">You can use Visual Studio with hello .NET SDK toomanage clusters and develop big data applications.</span></span> <span data-ttu-id="acaf0-136">您可以使用其他 Ide hello 下列工作，但在 Visual Studio 中顯示的範例。</span><span class="sxs-lookup"><span data-stu-id="acaf0-136">You can use other IDEs for hello following tasks, but examples are shown in Visual Studio.</span></span>

<span data-ttu-id="acaf0-137">您可以使用 Visual Studio 中的.NET SDK hello 執行的工作的範例包括：</span><span class="sxs-lookup"><span data-stu-id="acaf0-137">Examples of tasks you can do with hello .NET SDK in Visual Studio:</span></span>
* [<span data-ttu-id="acaf0-138">從 .NET Framework 應用程式在 HDInsight 中建立和使用叢集</span><span class="sxs-lookup"><span data-stu-id="acaf0-138">Create clusters and work in HDInsight from a .NET Framework application</span></span>](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [<span data-ttu-id="acaf0-139">執行 Hive 查詢使用 hello.NET SDK</span><span class="sxs-lookup"><span data-stu-id="acaf0-139">Run Hive queries using hello .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [<span data-ttu-id="acaf0-140">使用 C# 使用者定義的函式搭配 Hadoop 上的 Hive 和 Pig 串流</span><span class="sxs-lookup"><span data-stu-id="acaf0-140">Use C# user-defined functions with Hive and Pig streaming on Hadoop</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> <span data-ttu-id="acaf0-141">提示您執行.NET 方案與 Windows 為基礎的 HDInsight 叢集，它是否適合 tooplan 移轉 tooLinux 為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="acaf0-141">TIP If you're running .NET solutions with Windows-based HDInsight clusters, it's a good time tooplan a migration tooLinux-based clusters.</span></span> <span data-ttu-id="acaf0-142">如需詳細資訊，請參閱[Windows 為基礎的 HDInsight 的移轉.NET 方案 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="acaf0-142">For more information, see [Migrate .NET solution for Windows-based HDInsight tooLinux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span></span>

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a><span data-ttu-id="acaf0-143">適用於 Spark 叢集的 Intellij IDEA 和 Eclipse IDE</span><span class="sxs-lookup"><span data-stu-id="acaf0-143">Intellij IDEA and Eclipse IDE for Spark clusters</span></span>
<span data-ttu-id="acaf0-144">同時[Intellij 概念](https://www.jetbrains.com/idea/download)和 hello [Eclipse IDE](https://www.eclipse.org/downloads/)可以用來：</span><span class="sxs-lookup"><span data-stu-id="acaf0-144">Both [Intellij IDEA](https://www.jetbrains.com/idea/download) and hello [Eclipse IDE](https://www.eclipse.org/downloads/) can be used to:</span></span>
* <span data-ttu-id="acaf0-145">在 HDInsight Spark 叢集上開發並提交 Scala Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="acaf0-145">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="acaf0-146">存取 Spark 叢集資源。</span><span class="sxs-lookup"><span data-stu-id="acaf0-146">Access Spark cluster resources.</span></span>
* <span data-ttu-id="acaf0-147">在本機開發並執行 Scala Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="acaf0-147">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="acaf0-148">這些文章顯示如何︰</span><span class="sxs-lookup"><span data-stu-id="acaf0-148">These articles show how:</span></span> 
* <span data-ttu-id="acaf0-149">Intellij 概念：[建立 Spark 使用 hello Azure Toolkit for Intellij 外掛程式和 hello Scala SDK 的應用程式。](hdinsight-apache-spark-intellij-tool-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="acaf0-149">Intellij IDEA: [Create Spark applications using hello Azure Toolkit for Intellij plug-in and hello Scala SDK.](hdinsight-apache-spark-intellij-tool-plugin.md)</span></span>
* <span data-ttu-id="acaf0-150">Eclipse IDE 或 Scala Eclipse IDE:[建立 Spark 應用程式和 hello Azure Toolkit for Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="acaf0-150">Eclipse IDE or Scala IDE for Eclipse: [Create Spark applications and hello Azure Toolkit for Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)</span></span> 


## <a name="notebooks-on-spark-for-data-scientists"></a><span data-ttu-id="acaf0-151">適用於資料科學家的 Spark Notebook</span><span class="sxs-lookup"><span data-stu-id="acaf0-151">Notebooks on Spark for data scientists</span></span> 
<span data-ttu-id="acaf0-152">HDInsight 中的 Apache Spark 叢集包含可搭配 Jupyter Notebook 使用的 Zeppelin Notebook 和核心。</span><span class="sxs-lookup"><span data-stu-id="acaf0-152">Apache Spark clusters in HDInsight include Zeppelin notebooks and kernels that can be used with Jupyter notebooks.</span></span> 

* [<span data-ttu-id="acaf0-153">了解如何 toouse 核心上的 Spark 叢集與 Jupyter 筆記本 tootest Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="acaf0-153">Learn how toouse kernels on Spark clusters with Jupyter notebooks tootest Spark applications</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="acaf0-154">了解如何 toouse 運貨用飛艇筆記型電腦上的 Spark 叢集 toorun Spark 工作</span><span class="sxs-lookup"><span data-stu-id="acaf0-154">Learn how toouse Zeppelin notebooks on Spark clusters toorun Spark jobs</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a><span data-ttu-id="acaf0-155">在 Windows 上執行以 Linux 為基礎的工具和技術</span><span class="sxs-lookup"><span data-stu-id="acaf0-155">Run Linux-based tools and technologies on Windows</span></span>

<span data-ttu-id="acaf0-156">如果您遇到的情況下，您必須使用工具或只適用於 Linux 的技術，請考慮下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="acaf0-156">If you encounter a situation where you must use a tool or technology that is only available on Linux, consider hello following options:</span></span>

* <span data-ttu-id="acaf0-157">**Windows 10 上的 Bash (Beta 版)** 在 Windows 上提供 Linux 子系統。</span><span class="sxs-lookup"><span data-stu-id="acaf0-157">**Bash (beta) on Windows 10** provides a Linux subsystem on Windows.</span></span> <span data-ttu-id="acaf0-158">Bash 可讓您執行 Linux 公用程式，而不需要專用的 Linux 安裝 toomaintain toodirectly。</span><span class="sxs-lookup"><span data-stu-id="acaf0-158">Bash allows you toodirectly run Linux utilities without having toomaintain a dedicated Linux installation.</span></span> [<span data-ttu-id="acaf0-159">安裝並執行 Windows 10 上的 hello Bash beta</span><span class="sxs-lookup"><span data-stu-id="acaf0-159">Install and run hello Bash beta on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/install_guide)
* <span data-ttu-id="acaf0-160">**Docker for Windows** toomany Linux 為基礎的工具，提供存取，並可以直接從 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="acaf0-160">**Docker for Windows** provides access toomany Linux-based tools, and can be run directly from Windows.</span></span> <span data-ttu-id="acaf0-161">例如，您可以使用 Docker toorun hello Beeline 用戶端用於直接從 Windows 登錄區。</span><span class="sxs-lookup"><span data-stu-id="acaf0-161">For example, you can use Docker toorun hello Beeline client for Hive directly from Windows.</span></span> <span data-ttu-id="acaf0-162">您可以也使用 Docker toorun 本機 Jupyter 筆記本，並從遠端連接 tooSpark HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="acaf0-162">You can also use Docker toorun a local Jupyter notebook and remotely connect tooSpark on HDInsight.</span></span> [<span data-ttu-id="acaf0-163">開始使用 Docker for Windows</span><span class="sxs-lookup"><span data-stu-id="acaf0-163">Get started with Docker for Windows</span></span>](https://docs.docker.com/docker-for-windows/)
* <span data-ttu-id="acaf0-164">**[MobaXTerm](http://mobaxterm.mobatek.net/)** 可讓您透過 SSH 連線的 toographically 瀏覽 hello 叢集檔案系統。</span><span class="sxs-lookup"><span data-stu-id="acaf0-164">**[MobaXTerm](http://mobaxterm.mobatek.net/)** allows you toographically browse hello cluster file system over an SSH connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="acaf0-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="acaf0-165">Next steps</span></span>
<span data-ttu-id="acaf0-166">如果您是新 tooworking 以 Linux 為基礎的叢集，請參閱 hello，請依照下列文章：</span><span class="sxs-lookup"><span data-stu-id="acaf0-166">If you're new tooworking in Linux-based clusters, see hello follow articles:</span></span>
* [<span data-ttu-id="acaf0-167">設定 Hadoop、Kafka、Spark 或其他叢集</span><span class="sxs-lookup"><span data-stu-id="acaf0-167">Set up Hadoop, Kafka, Spark, or other clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="acaf0-168">Linux 上的 HDInsight 叢集祕訣</span><span class="sxs-lookup"><span data-stu-id="acaf0-168">Tips for HDInsight clusters on Linux</span></span>](hdinsight-hadoop-linux-information.md)
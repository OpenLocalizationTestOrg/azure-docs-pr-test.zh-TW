---
title: "使用 Visual Studio 和 C#-Azure HDInsight aaaApache Storm 拓撲 |Microsoft 文件"
description: "深入了解如何在 C# toocreate Storm 拓撲。 Visual Studio 中建立簡單的單字計數拓撲使用 hello Hadoop tools for Visual Studio。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="26826-104">使用 hello Data Lake tools for Visual Studio 開發 Apache Storm 的 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="26826-104">Develop C# topologies for Apache Storm by using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="26826-105">了解如何 toocreate 使用 hello Azure 資料湖 (Hadoop) 的 C# Storm 拓樸 tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="26826-105">Learn how toocreate a C# Storm topology by using hello Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="26826-106">本文件逐步 hello Visual Studio 中建立 Storm 專案、 在本機測試和部署程序它 tooan Apache Storm Azure HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="26826-106">This document walks through hello process of creating a Storm project in Visual Studio, testing it locally, and deploying it tooan Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="26826-107">您也學到如何 toocreate 混合式拓撲中，使用 C# 和 Java 的元件。</span><span class="sxs-lookup"><span data-stu-id="26826-107">You also learn how toocreate hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="26826-108">本文件中的 hello 步驟依賴 Windows 與 Visual Studio 開發環境，雖然 hello 已編譯的專案可以提交的 tooeither Linux 或 Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="26826-108">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooeither a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="26826-109">只有在 2016 年 10 月 28 日之後所建立之以 Linux 為基礎的叢集可支援 SCP.NET 拓撲。</span><span class="sxs-lookup"><span data-stu-id="26826-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="26826-110">toouse C# 拓撲中使用以 Linux 為基礎的叢集，您必須更新 hello Microsoft.SCP.Net.SDK NuGet 封裝使用您的專案 tooversion 0.10.0.6 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="26826-110">toouse a C# topology with a Linux-based cluster, you must update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or later.</span></span> <span data-ttu-id="26826-111">hello hello 封裝版本也必須符合安裝在 HDInsight 上的 Storm hello 主要版本。</span><span class="sxs-lookup"><span data-stu-id="26826-111">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="26826-112">HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="26826-112">HDInsight version</span></span> | <span data-ttu-id="26826-113">Storm 版本</span><span class="sxs-lookup"><span data-stu-id="26826-113">Storm version</span></span> | <span data-ttu-id="26826-114">SCP.NET 版本</span><span class="sxs-lookup"><span data-stu-id="26826-114">SCP.NET version</span></span> | <span data-ttu-id="26826-115">預設 Mono 版本</span><span class="sxs-lookup"><span data-stu-id="26826-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="26826-116">3.3</span><span class="sxs-lookup"><span data-stu-id="26826-116">3.3</span></span> |<span data-ttu-id="26826-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="26826-117">0.10.x</span></span> |<span data-ttu-id="26826-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="26826-118">0.10.x.x</span></span></br><span data-ttu-id="26826-119">(僅限以 Windows 為基礎的 HDInsight)</span><span class="sxs-lookup"><span data-stu-id="26826-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="26826-120">NA</span><span class="sxs-lookup"><span data-stu-id="26826-120">NA</span></span> |
| <span data-ttu-id="26826-121">3.4</span><span class="sxs-lookup"><span data-stu-id="26826-121">3.4</span></span> | <span data-ttu-id="26826-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="26826-122">0.10.0.x</span></span> | <span data-ttu-id="26826-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="26826-123">0.10.0.x</span></span> | <span data-ttu-id="26826-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="26826-124">3.2.8</span></span> |
| <span data-ttu-id="26826-125">3.5</span><span class="sxs-lookup"><span data-stu-id="26826-125">3.5</span></span> | <span data-ttu-id="26826-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="26826-126">1.0.2.x</span></span> | <span data-ttu-id="26826-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="26826-127">1.0.0.x</span></span> | <span data-ttu-id="26826-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="26826-128">4.2.1</span></span> |
| <span data-ttu-id="26826-129">3.6</span><span class="sxs-lookup"><span data-stu-id="26826-129">3.6</span></span> | <span data-ttu-id="26826-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="26826-130">1.1.0.x</span></span> | <span data-ttu-id="26826-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="26826-131">1.0.0.x</span></span> | <span data-ttu-id="26826-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="26826-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="26826-133">C# 拓撲以 Linux 為基礎的叢集上必須使用.NET 4.5，並使用單聲道 toorun hello HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="26826-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="26826-134">查看 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/) \(英文\) 以了解可能的不相容情形。</span><span class="sxs-lookup"><span data-stu-id="26826-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="26826-135">安裝 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="26826-135">Install Visual Studio</span></span>

<span data-ttu-id="26826-136">您可以使用其中一種 hello 下列版本的 Visual Studio 開發 SCP.NET 與 C# 拓撲：</span><span class="sxs-lookup"><span data-stu-id="26826-136">You can develop C# topologies with SCP.NET by using one of hello following versions of Visual Studio:</span></span>

* <span data-ttu-id="26826-137">Visual Studio 2012 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="26826-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="26826-138">Visual Studio 2013 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=44921) 或 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="26826-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="26826-139">Visual Studio 2015 或 [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="26826-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="26826-140">Visual Studio 2017 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="26826-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="26826-141">安裝 Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="26826-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="26826-142">tooinstall Data Lake tools for Visual Studio，請依照下列中的 hello 步驟[開始使用 Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="26826-142">tooinstall Data Lake tools for Visual Studio, follow hello steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="26826-143">安裝 Java</span><span class="sxs-lookup"><span data-stu-id="26826-143">Install Java</span></span>

<span data-ttu-id="26826-144">當您提交從 Visual Studio 的 Storm 拓樸時，SCP.NET 會產生包含 hello 拓樸和相依性的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="26826-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains hello topology and dependencies.</span></span> <span data-ttu-id="26826-145">Java 是使用的 toocreate 這些 zip 檔案，因為它會使用與 Linux 型叢集更相容的格式。</span><span class="sxs-lookup"><span data-stu-id="26826-145">Java is used toocreate these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="26826-146">安裝 hello Java Developer Kit (JDK) 7 或更新版本在您的開發環境。</span><span class="sxs-lookup"><span data-stu-id="26826-146">Install hello Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="26826-147">您可以取得 hello 從 Oracle JDK [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。</span><span class="sxs-lookup"><span data-stu-id="26826-147">You can get hello Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="26826-148">您也可以使用[其他 Java 發佈](http://openjdk.java.net/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="26826-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="26826-149">hello`JAVA_HOME`包含 Java 的環境變數必須點 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="26826-149">hello `JAVA_HOME` environment variable must point toohello directory that contains Java.</span></span>

3. <span data-ttu-id="26826-150">hello`PATH`環境變數必須包含 hello`%JAVA_HOME%\bin`目錄。</span><span class="sxs-lookup"><span data-stu-id="26826-150">hello `PATH` environment variable must include hello `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="26826-151">您可以使用下列 C# 主控台應用程式 tooverify Java 和 hello JDK 已正確安裝 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-151">You can use hello following C# console application tooverify that Java and hello JDK are correctly installed:</span></span>

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a><span data-ttu-id="26826-152">Storm 範本</span><span class="sxs-lookup"><span data-stu-id="26826-152">Storm templates</span></span>

<span data-ttu-id="26826-153">hello Data Lake tools for Visual Studio 提供下列範本的 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-153">hello Data Lake tools for Visual Studio provide hello following templates:</span></span>

| <span data-ttu-id="26826-154">專案類型</span><span class="sxs-lookup"><span data-stu-id="26826-154">Project type</span></span> | <span data-ttu-id="26826-155">示範</span><span class="sxs-lookup"><span data-stu-id="26826-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="26826-156">Storm 應用程式</span><span class="sxs-lookup"><span data-stu-id="26826-156">Storm Application</span></span> |<span data-ttu-id="26826-157">空白 Storm 拓撲專案。</span><span class="sxs-lookup"><span data-stu-id="26826-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="26826-158">Storm Azure SQL 寫入器範例</span><span class="sxs-lookup"><span data-stu-id="26826-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="26826-159">如何 toowrite tooAzure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="26826-159">How toowrite tooAzure SQL Database.</span></span> |
| <span data-ttu-id="26826-160">Storm Azure Cosmos DB 讀取器範例</span><span class="sxs-lookup"><span data-stu-id="26826-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="26826-161">如何從 Azure Cosmos DB tooread。</span><span class="sxs-lookup"><span data-stu-id="26826-161">How tooread from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="26826-162">Storm Azure Cosmos DB 寫入器範例</span><span class="sxs-lookup"><span data-stu-id="26826-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="26826-163">如何 toowrite tooAzure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="26826-163">How toowrite tooAzure Cosmos DB.</span></span> |
| <span data-ttu-id="26826-164">Storm EventHub 讀取器範例</span><span class="sxs-lookup"><span data-stu-id="26826-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="26826-165">如何從 Azure 事件中樞 tooread。</span><span class="sxs-lookup"><span data-stu-id="26826-165">How tooread from Azure Event Hubs.</span></span> |
| <span data-ttu-id="26826-166">Storm EventHub 寫入器範例</span><span class="sxs-lookup"><span data-stu-id="26826-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="26826-167">如何 toowrite tooAzure 事件中心。</span><span class="sxs-lookup"><span data-stu-id="26826-167">How toowrite tooAzure Event Hubs.</span></span> |
| <span data-ttu-id="26826-168">Storm HBase 讀取器範例</span><span class="sxs-lookup"><span data-stu-id="26826-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="26826-169">如何 tooread 從上 HDInsight HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="26826-169">How tooread from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="26826-170">Storm HBase 寫入器範例</span><span class="sxs-lookup"><span data-stu-id="26826-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="26826-171">Toowrite tooHBase HDInsight 上的叢集。</span><span class="sxs-lookup"><span data-stu-id="26826-171">How toowrite tooHBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="26826-172">Storm 混合式範例</span><span class="sxs-lookup"><span data-stu-id="26826-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="26826-173">如何 toouse Java 元件。</span><span class="sxs-lookup"><span data-stu-id="26826-173">How toouse a Java component.</span></span> |
| <span data-ttu-id="26826-174">Storm 範例</span><span class="sxs-lookup"><span data-stu-id="26826-174">Storm Sample</span></span> |<span data-ttu-id="26826-175">基本的字數統計拓撲。</span><span class="sxs-lookup"><span data-stu-id="26826-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="26826-176">並非所有範本都能與 Linux 架構的 HDInsight 搭配運作。</span><span class="sxs-lookup"><span data-stu-id="26826-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="26826-177">可能不相容的 Mono hello 範本所使用的 Nuget 套件。</span><span class="sxs-lookup"><span data-stu-id="26826-177">Nuget packages used by hello templates may not be compatible with Mono.</span></span> <span data-ttu-id="26826-178">檢查 hello[單聲道的相容性](http://www.mono-project.com/docs/about-mono/compatibility/)文件，並使用 hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify 潛在問題。</span><span class="sxs-lookup"><span data-stu-id="26826-178">Check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potential problems.</span></span>

<span data-ttu-id="26826-179">在本文件中的 hello 步驟，您可以使用 hello 基本 Storm 應用程式專案類型 toocreate 拓撲。</span><span class="sxs-lookup"><span data-stu-id="26826-179">In hello steps in this document, you use hello basic Storm Application project type toocreate a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="26826-180">HBase 範本注意事項</span><span class="sxs-lookup"><span data-stu-id="26826-180">HBase templates notes</span></span>

<span data-ttu-id="26826-181">hello HBase 讀取器和寫入器範本使用 hello HBase REST API，不 hello HBase Java 應用程式開發介面，toocommunicate HBase HDInsight 叢集上使用。</span><span class="sxs-lookup"><span data-stu-id="26826-181">hello HBase reader and writer templates use hello HBase REST API, not hello HBase Java API, toocommunicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="26826-182">EventHub 範本注意事項</span><span class="sxs-lookup"><span data-stu-id="26826-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26826-183">hello Java 為基礎的 EventHub spout 隨附的 hello EventHub 讀取器範本可能不適用於 HDInsight 版本 3.5 或更新版本上出現的元件。</span><span class="sxs-lookup"><span data-stu-id="26826-183">hello Java-based EventHub spout component included with hello EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="26826-184">此元件的更新版本可在 [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib) \(英文\) 取得。</span><span class="sxs-lookup"><span data-stu-id="26826-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="26826-185">如需使用此元件和搭配 Storm on HDInsight 3.5 使用的範例拓撲，請參閱 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="26826-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="26826-186">建立 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="26826-186">Create a C# topology</span></span>

1. <span data-ttu-id="26826-187">開啟 Visual Studio，選取 [檔案] > [新增]，然後選取 [專案]。</span><span class="sxs-lookup"><span data-stu-id="26826-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="26826-188">從 hello**新專案**視窗中，展開 **已安裝** > **範本**，然後選取**Azure 資料湖**。</span><span class="sxs-lookup"><span data-stu-id="26826-188">From hello **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="26826-189">從範本 hello 清單，選取**Storm 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="26826-189">From hello list of templates, select **Storm Application**.</span></span> <span data-ttu-id="26826-190">在 hello 囉 」 畫面下方，輸入**WordCount**做 hello hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="26826-190">At hello bottom of hello screen, enter **WordCount** as hello name of hello application.</span></span>

    ![[新增專案] 視窗的螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="26826-192">建立 hello 專案之後，您應該有下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-192">After you have created hello project, you should have hello following files:</span></span>

   * <span data-ttu-id="26826-193">**Program.cs**： 此檔案會定義您的專案的 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="26826-193">**Program.cs**: This file defines hello topology for your project.</span></span> <span data-ttu-id="26826-194">預設會建立含有一個 Spout 和一個 Bolt 的預設拓撲。</span><span class="sxs-lookup"><span data-stu-id="26826-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="26826-195">**Spout.cs**：發出亂數的範例 Spout。</span><span class="sxs-lookup"><span data-stu-id="26826-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="26826-196">**Bolt.cs**： 會保留 hello spout 所發出的數字計數範例閃電。</span><span class="sxs-lookup"><span data-stu-id="26826-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by hello spout.</span></span>

     <span data-ttu-id="26826-197">當您建立 hello 專案時，NuGet 下載最新 hello [SCP.NET 封裝](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/)。</span><span class="sxs-lookup"><span data-stu-id="26826-197">When you create hello project, NuGet downloads hello latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a><span data-ttu-id="26826-198">實作 hello spout</span><span class="sxs-lookup"><span data-stu-id="26826-198">Implement hello spout</span></span>

1. <span data-ttu-id="26826-199">開啟 **Spout.cs**。</span><span class="sxs-lookup"><span data-stu-id="26826-199">Open **Spout.cs**.</span></span> <span data-ttu-id="26826-200">Spouts 是使用的 tooread 拓撲從外部來源中的資料。</span><span class="sxs-lookup"><span data-stu-id="26826-200">Spouts are used tooread data in a topology from an external source.</span></span> <span data-ttu-id="26826-201">hello spout 主要元件為：</span><span class="sxs-lookup"><span data-stu-id="26826-201">hello main components for a spout are:</span></span>

   * <span data-ttu-id="26826-202">**NextTuple**: hello spout 允許 tooemit 新 tuple 時，由 Storm 呼叫。</span><span class="sxs-lookup"><span data-stu-id="26826-202">**NextTuple**: Called by Storm when hello spout is allowed tooemit new tuples.</span></span>

   * <span data-ttu-id="26826-203">**Ack** （只有交易式拓撲）： 處理通知寄件者 hello spout tuple 的 hello 拓撲中的其他元件所起始。</span><span class="sxs-lookup"><span data-stu-id="26826-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in hello topology for tuples sent from hello spout.</span></span> <span data-ttu-id="26826-204">認可 tuple，可讓 hello spout 知道它已順利處理的下游元件。</span><span class="sxs-lookup"><span data-stu-id="26826-204">Acknowledging a tuple lets hello spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="26826-205">**失敗**（只有交易式拓撲）： 處理會失敗-處理 hello 拓撲中的其他元件的 tuple。</span><span class="sxs-lookup"><span data-stu-id="26826-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in hello topology.</span></span> <span data-ttu-id="26826-206">實作 Fail 方法可讓您 toore-發出 hello tuple，以便再次處理。</span><span class="sxs-lookup"><span data-stu-id="26826-206">Implementing a Fail method allows you toore-emit hello tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="26826-207">取代 hello hello 內容**Spout** hello 文字之後使用的類別。</span><span class="sxs-lookup"><span data-stu-id="26826-207">Replace hello contents of hello **Spout** class with hello following text.</span></span> <span data-ttu-id="26826-208">此 spout 隨機會發出到 hello 拓撲的句子。</span><span class="sxs-lookup"><span data-stu-id="26826-208">This spout randomly emits a sentence into hello topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a><span data-ttu-id="26826-209">實作 hello 攻擊</span><span class="sxs-lookup"><span data-stu-id="26826-209">Implement hello bolts</span></span>

1. <span data-ttu-id="26826-210">刪除現有的 hello **Bolt.cs** hello 專案檔案。</span><span class="sxs-lookup"><span data-stu-id="26826-210">Delete hello existing **Bolt.cs** file from hello project.</span></span>

2. <span data-ttu-id="26826-211">在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**新增** > **新項目**。</span><span class="sxs-lookup"><span data-stu-id="26826-211">In **Solution Explorer**, right-click hello project, and select **Add** > **New item**.</span></span> <span data-ttu-id="26826-212">從 hello 清單中，選取 **出現閃電**，並輸入**Splitter.cs**做為 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="26826-212">From hello list, select **Storm Bolt**, and enter **Splitter.cs** as hello name.</span></span> <span data-ttu-id="26826-213">重複第二個閃電名為此程序 toocreate **Counter.cs**。</span><span class="sxs-lookup"><span data-stu-id="26826-213">Repeat this process toocreate a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="26826-214">**Splitter.cs**：實作會將句子分成個別單字，並發出一串新文字的 Bolt。</span><span class="sxs-lookup"><span data-stu-id="26826-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="26826-215">**Counter.cs**： 實作閃電，計算每個字，並發出新的資料流字詞與每個單字的 hello 計數。</span><span class="sxs-lookup"><span data-stu-id="26826-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and hello count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="26826-216">這些攻擊讀取和寫入 toostreams，但您也可以使用閃電 toocommunicate 來源，例如資料庫或服務。</span><span class="sxs-lookup"><span data-stu-id="26826-216">These bolts read and write toostreams, but you can also use a bolt toocommunicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="26826-217">開啟 **Splitter.cs**。</span><span class="sxs-lookup"><span data-stu-id="26826-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="26826-218">它預設只有一個方法：**Execute**。</span><span class="sxs-lookup"><span data-stu-id="26826-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="26826-219">hello 閃電收到 tuple，以進行處理時，會呼叫 hello Execute 方法。</span><span class="sxs-lookup"><span data-stu-id="26826-219">hello Execute method is called when hello bolt receives a tuple for processing.</span></span> <span data-ttu-id="26826-220">此時，您可以讀取和處理內送 Tuple，以及發出輸出 Tuple。</span><span class="sxs-lookup"><span data-stu-id="26826-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="26826-221">取代 hello hello 內容**分隔器**類別以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-221">Replace hello contents of hello **Splitter** class with hello following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. <span data-ttu-id="26826-222">開啟**Counter.cs**，並取代 hello 下列中的 hello 類別內容：</span><span class="sxs-lookup"><span data-stu-id="26826-222">Open **Counter.cs**, and replace hello class contents with hello following:</span></span>

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a><span data-ttu-id="26826-223">定義 hello 拓撲</span><span class="sxs-lookup"><span data-stu-id="26826-223">Define hello topology</span></span>

<span data-ttu-id="26826-224">在圖形中，它會定義元件之間流動 hello 資料的方式排列 spouts 和攻擊。</span><span class="sxs-lookup"><span data-stu-id="26826-224">Spouts and bolts are arranged in a graph, which defines how hello data flows between components.</span></span> <span data-ttu-id="26826-225">針對此拓撲，hello 圖形如下所示：</span><span class="sxs-lookup"><span data-stu-id="26826-225">For this topology, hello graph is as follows:</span></span>

![元件排列方式的圖表](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="26826-227">句子從 hello spout 會發出，因此是分散式的 hello 分隔器閃電 tooinstances。</span><span class="sxs-lookup"><span data-stu-id="26826-227">Sentences are emitted from hello spout, and are distributed tooinstances of hello Splitter bolt.</span></span> <span data-ttu-id="26826-228">hello 分隔器閃電成文字，也就是分散式的 toohello 計數器閃電中斷 hello 句子。</span><span class="sxs-lookup"><span data-stu-id="26826-228">hello Splitter bolt breaks hello sentences into words, which are distributed toohello Counter bolt.</span></span>

<span data-ttu-id="26826-229">字數統計會在本機保留 hello 計數器執行個體，因為我們想確定特定單字流程 toohello toomake 相同計數器閃電執行個體。</span><span class="sxs-lookup"><span data-stu-id="26826-229">Because word count is held locally in hello Counter instance, we want toomake sure that specific words flow toohello same Counter bolt instance.</span></span> <span data-ttu-id="26826-230">每個執行個體會保持追蹤特定文字。</span><span class="sxs-lookup"><span data-stu-id="26826-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="26826-231">Hello 分隔器閃電維護無狀態，因為它實際上並不重要 hello 分隔器的執行個體收到的句子。</span><span class="sxs-lookup"><span data-stu-id="26826-231">Since hello Splitter bolt maintains no state, it really doesn't matter which instance of hello splitter receives which sentence.</span></span>

<span data-ttu-id="26826-232">開啟 **Program.cs**。</span><span class="sxs-lookup"><span data-stu-id="26826-232">Open **Program.cs**.</span></span> <span data-ttu-id="26826-233">hello 重要的方法是**GetTopologyBuilder**，即是使用的 toodefine hello 拓樸提交 tooStorm。</span><span class="sxs-lookup"><span data-stu-id="26826-233">hello important method is **GetTopologyBuilder**, which is used toodefine hello topology that is submitted tooStorm.</span></span> <span data-ttu-id="26826-234">取代 hello 內容**GetTopologyBuilder**以下列程式碼 tooimplement hello 拓樸先前所述的 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-234">Replace hello contents of **GetTopologyBuilder** with hello following code tooimplement hello topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a><span data-ttu-id="26826-235">送出 hello 拓樸</span><span class="sxs-lookup"><span data-stu-id="26826-235">Submit hello topology</span></span>

1. <span data-ttu-id="26826-236">在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**提交 HDInsight 上的 tooStorm**。</span><span class="sxs-lookup"><span data-stu-id="26826-236">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="26826-237">如果出現提示，請輸入您的 Azure 訂閱 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="26826-237">If prompted, enter hello credentials for your Azure subscription.</span></span> <span data-ttu-id="26826-238">如果您有多個訂用帳戶，登入另一個則包含您在 HDInsight 叢集的 Storm toohello。</span><span class="sxs-lookup"><span data-stu-id="26826-238">If you have more than one subscription, sign in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="26826-239">選取您在 HDInsight 叢集的 Storm 從 hello **Storm 叢集**下拉式清單，然後選取**送出**。</span><span class="sxs-lookup"><span data-stu-id="26826-239">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="26826-240">如果使用 hello hello 提交成功，您可以監視**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="26826-240">You can monitor if hello submission is successful by using hello **Output** window.</span></span>

3. <span data-ttu-id="26826-241">已成功送出 hello 拓樸，當 hello **Storm 拓撲**hello 叢集應該會出現。</span><span class="sxs-lookup"><span data-stu-id="26826-241">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="26826-242">選取 hello **WordCount**拓撲從 hello 列出 tooview hello 執行拓撲的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="26826-242">Select hello **WordCount** topology from hello list tooview information about hello running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="26826-243">您也可以從 [伺服器總管] 檢視 [Storm 拓撲]。</span><span class="sxs-lookup"><span data-stu-id="26826-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="26826-244">展開 [Azure] > [HDInsight]，以滑鼠右鍵按一下 Storm on HDInsight 叢集，然後選取 [檢視 Storm 拓撲]。</span><span class="sxs-lookup"><span data-stu-id="26826-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="26826-245">tooview 資訊 hello 元件在 hello 拓撲中，按兩下 hello 圖中的 hello 元件。</span><span class="sxs-lookup"><span data-stu-id="26826-245">tooview information about hello components in hello topology, double-click hello component in hello diagram.</span></span>

4. <span data-ttu-id="26826-246">從 hello**拓撲摘要**檢視中，按一下**Kill** toostop hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="26826-246">From hello **Topology Summary** view, click **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="26826-247">Storm 拓撲繼續 toorun 直到都已停用，或刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="26826-247">Storm topologies continue toorun until they are deactivated, or hello cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="26826-248">交易式拓撲</span><span class="sxs-lookup"><span data-stu-id="26826-248">Transactional topology</span></span>

<span data-ttu-id="26826-249">hello 先前拓樸為非交易式。</span><span class="sxs-lookup"><span data-stu-id="26826-249">hello previous topology is non-transactional.</span></span> <span data-ttu-id="26826-250">hello 拓撲中的 hello 元件不會實作功能 tooreplaying 訊息。</span><span class="sxs-lookup"><span data-stu-id="26826-250">hello components in hello topology do not implement functionality tooreplaying messages.</span></span> <span data-ttu-id="26826-251">如需交易式拓撲的範例，建立專案並選取**Storm 範例**hello 專案類型。</span><span class="sxs-lookup"><span data-stu-id="26826-251">For an example of a transactional topology, create a project and select **Storm Sample** as hello project type.</span></span>

<span data-ttu-id="26826-252">交易式拓撲實作 hello 遵循 toosupport 重新執行的資料：</span><span class="sxs-lookup"><span data-stu-id="26826-252">Transactional topologies implement hello following toosupport replay of data:</span></span>

* <span data-ttu-id="26826-253">**中繼資料快取**: hello spout 必須儲存 hello 資料發出，以便可以擷取與發出一次，如果發生失敗的 hello 資料的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="26826-253">**Metadata caching**: hello spout must store metadata about hello data emitted, so that hello data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="26826-254">由於 hello 範例所發出的 hello 資料很小，每個 tuple 的 hello 未經處理資料都會儲存在重新執行的字典。</span><span class="sxs-lookup"><span data-stu-id="26826-254">Because hello data emitted by hello sample is small, hello raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="26826-255">**Ack**: hello 拓撲中的每個閃電可以呼叫`this.ctx.Ack(tuple)`tooacknowledge 已成功處理 tuple。</span><span class="sxs-lookup"><span data-stu-id="26826-255">**Ack**: Each bolt in hello topology can call `this.ctx.Ack(tuple)` tooacknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="26826-256">當所有發射 acked hello tuple，hello `Ack` hello spout 方法會叫用。</span><span class="sxs-lookup"><span data-stu-id="26826-256">When all bolts have acked hello tuple, hello `Ack` method of hello spout is invoked.</span></span> <span data-ttu-id="26826-257">hello`Ack`方法可讓重新執行快取的 hello spout tooremove 資料。</span><span class="sxs-lookup"><span data-stu-id="26826-257">hello `Ack` method allows hello spout tooremove data that was cached for replay.</span></span>

* <span data-ttu-id="26826-258">**失敗**： 可以在呼叫每個閃電`this.ctx.Fail(tuple)`tooindicate 該處理失敗的 tuple。</span><span class="sxs-lookup"><span data-stu-id="26826-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` tooindicate that processing has failed for a tuple.</span></span> <span data-ttu-id="26826-259">hello 失敗傳播 toohello`Fail`方法 hello spout，其中 hello tuple 可以重新執行所使用的快取中繼資料。</span><span class="sxs-lookup"><span data-stu-id="26826-259">hello failure propagates toohello `Fail` method of hello spout, where hello tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="26826-260">**序列識別碼**：發出 Tuple 時，可以指定唯一的序列識別碼。</span><span class="sxs-lookup"><span data-stu-id="26826-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="26826-261">這個值識別 （「 通知 」 和 「 失敗 」） 重新執行處理的 hello tuple。</span><span class="sxs-lookup"><span data-stu-id="26826-261">This value identifies hello tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="26826-262">比方說，hello 在 hello spout **Storm 範例**發出資料時，專案會使用 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="26826-262">For example, hello spout in hello **Storm Sample** project uses hello following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="26826-263">此程式碼會發出包含句子 toohello 預設資料流中包含的 hello 順序識別碼值與 tuple **lastSeqId**。</span><span class="sxs-lookup"><span data-stu-id="26826-263">This code emits a tuple that contains a sentence toohello default stream, with hello sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="26826-264">在此範例中，會遞增每個發出 Tuple 的 **lastSeqId**。</span><span class="sxs-lookup"><span data-stu-id="26826-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="26826-265">示 hello **Storm 範例**專案中，交易式元件是否可以在執行階段，根據組態設定。</span><span class="sxs-lookup"><span data-stu-id="26826-265">As demonstrated in hello **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="26826-266">採用 C# 和 Java 的混合式拓撲</span><span class="sxs-lookup"><span data-stu-id="26826-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="26826-267">您也可以使用 Data Lake 工具，如需 Visual Studio toocreate 混合拓撲，其中有些元件是 C#，而其他則 Java。</span><span class="sxs-lookup"><span data-stu-id="26826-267">You can also use Data Lake tools for Visual Studio toocreate hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="26826-268">針對混合式拓撲範例，請建立專案，然後選取 [Storm 混合式範例]。</span><span class="sxs-lookup"><span data-stu-id="26826-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="26826-269">此範例類型示範 hello 下列概念：</span><span class="sxs-lookup"><span data-stu-id="26826-269">This sample type demonstrates hello following concepts:</span></span>

* <span data-ttu-id="26826-270">**Java Spout** 和 **C# Bolt**：定義於 **HybridTopology_javaSpout_csharpBolt**。</span><span class="sxs-lookup"><span data-stu-id="26826-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="26826-271">交易式版本定義於 **HybridTopologyTx_javaSpout_csharpBolt**。</span><span class="sxs-lookup"><span data-stu-id="26826-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="26826-272">**C# Spout** 和 **Java Bolt**：定義於 **HybridTopology_csharpSpout_javaBolt**。</span><span class="sxs-lookup"><span data-stu-id="26826-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="26826-273">交易式版本定義於 **HybridTopologyTx_csharpSpout_javaBolt**。</span><span class="sxs-lookup"><span data-stu-id="26826-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="26826-274">此版本也會示範 toouse Clojure 從文字檔案做為 Java 元件的程式碼。</span><span class="sxs-lookup"><span data-stu-id="26826-274">This version also demonstrates how toouse Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="26826-275">tooswitch hello 拓撲時送出 hello 專案，只要移動 hello`[Active(true)]`想 toouse，送出 toohello 叢集之前的陳述式 toohello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="26826-275">tooswitch hello topology that is used when hello project is submitted, simply move hello `[Active(true)]` statement toohello topology you want toouse, before submitting it toohello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="26826-276">在 hello 這個專案的一部分提供所需的所有 hello Java 檔案**JavaDependency**資料夾。</span><span class="sxs-lookup"><span data-stu-id="26826-276">All hello Java files that are required are provided as part of this project in hello **JavaDependency** folder.</span></span>

<span data-ttu-id="26826-277">當您建立並提交混合式拓撲，請考慮下列 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-277">Consider hello following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="26826-278">您必須使用**JavaComponentConstructor** toocreate hello spout 或閃電的 Java 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="26826-278">You must use **JavaComponentConstructor** toocreate an instance of hello Java class for a spout or bolt.</span></span>

* <span data-ttu-id="26826-279">您應該使用**microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize 資料傳入或傳出 Java 元件從 Java 物件 tooJSON。</span><span class="sxs-lookup"><span data-stu-id="26826-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize data into or out of Java components from Java objects tooJSON.</span></span>

* <span data-ttu-id="26826-280">當送出 hello 拓撲 toohello 伺服器，您必須使用 hello**額外的組態**選項 toospecify hello **Java 檔案路徑**。</span><span class="sxs-lookup"><span data-stu-id="26826-280">When submitting hello topology toohello server, you must use hello **Additional configurations** option toospecify hello **Java File paths**.</span></span> <span data-ttu-id="26826-281">指定的 hello 路徑應該是包含 hello JAR 檔案，其中包含您的 Java 類別的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="26826-281">hello path specified should be hello directory that contains hello JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="26826-282">Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="26826-282">Azure Event Hubs</span></span>

<span data-ttu-id="26826-283">SCP.NET 版本 0.9.4.203 引入新類別，以及特別為 hello 事件中心 spout (從事件中心讀取 Java spout) 所使用的方法。</span><span class="sxs-lookup"><span data-stu-id="26826-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with hello Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="26826-284">當您建立使用事件中心 spout 拓撲時，使用下列方法 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-284">When you create a topology that uses an Event Hub spout, use hello following methods:</span></span>

* <span data-ttu-id="26826-285">**EventHubSpoutConfig**類別： 建立物件，其中包含 hello hello spout 元件的設定。</span><span class="sxs-lookup"><span data-stu-id="26826-285">**EventHubSpoutConfig** class: Creates an object that contains hello configuration for hello spout component.</span></span>

* <span data-ttu-id="26826-286">**TopologyBuilder.SetEventHubSpout**方法： 新增 hello 事件中心 spout 元件 toohello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="26826-286">**TopologyBuilder.SetEventHubSpout** method: Adds hello Event Hub spout component toohello topology.</span></span>

> [!NOTE]
> <span data-ttu-id="26826-287">您仍然必須使用 hello **CustomizedInteropJSONSerializer** hello spout 所產生的 tooserialize 資料。</span><span class="sxs-lookup"><span data-stu-id="26826-287">You must still use hello **CustomizedInteropJSONSerializer** tooserialize data produced by hello spout.</span></span>

## <span data-ttu-id="26826-288"><a id="configurationmanager"></a>使用 ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="26826-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="26826-289">請勿使用**ConfigurationManager** tooretrieve 組態中的值閃電和 spout 元件。</span><span class="sxs-lookup"><span data-stu-id="26826-289">Don't use **ConfigurationManager** tooretrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="26826-290">這麼做會導致 Null 指標例外狀況。</span><span class="sxs-lookup"><span data-stu-id="26826-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="26826-291">相反地，hello 專案組態傳入 hello Storm 拓樸為 hello 拓撲內容中的索引鍵和值組。</span><span class="sxs-lookup"><span data-stu-id="26826-291">Instead, hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="26826-292">每個元件所使用的設定值必須擷取它們 hello 內容初始化期間。</span><span class="sxs-lookup"><span data-stu-id="26826-292">Each component that relies on configuration values must retrieve them from hello context during initialization.</span></span>

<span data-ttu-id="26826-293">hello 下列程式碼示範如何 tooretrieve 這些值：</span><span class="sxs-lookup"><span data-stu-id="26826-293">hello following code demonstrates how tooretrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="26826-294">如果您使用`Get`方法 tooreturn 您元件的執行個體，您必須確定它會傳遞兩個 hello`Context`和`Dictionary<string, Object>`參數 toohello 建構函式。</span><span class="sxs-lookup"><span data-stu-id="26826-294">If you use a `Get` method tooreturn an instance of your component, you must ensure that it passes both hello `Context` and `Dictionary<string, Object>` parameters toohello constructor.</span></span> <span data-ttu-id="26826-295">hello 下列範例是基本`Get`正確傳遞這些值的方法：</span><span class="sxs-lookup"><span data-stu-id="26826-295">hello following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a><span data-ttu-id="26826-296">如何 tooupdate SCP.NET</span><span class="sxs-lookup"><span data-stu-id="26826-296">How tooupdate SCP.NET</span></span>

<span data-ttu-id="26826-297">最新版 SCP.NET 支援透過 NuGet 進行封裝升級。</span><span class="sxs-lookup"><span data-stu-id="26826-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="26826-298">當新的更新可用時，您會收到升級通知。</span><span class="sxs-lookup"><span data-stu-id="26826-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="26826-299">toomanually 核取進行升級時，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="26826-299">toomanually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="26826-300">在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="26826-300">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="26826-301">從 hello 封裝管理員 中，選取**更新**。</span><span class="sxs-lookup"><span data-stu-id="26826-301">From hello package manager, select **Updates**.</span></span> <span data-ttu-id="26826-302">如果有可用的更新，它會列出。</span><span class="sxs-lookup"><span data-stu-id="26826-302">If an update is available, it is listed.</span></span> <span data-ttu-id="26826-303">按一下**更新**的 hello 封裝 tooinstall 它。</span><span class="sxs-lookup"><span data-stu-id="26826-303">Click **Update** for hello package tooinstall it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26826-304">如果您的專案建立的舊版 SCP.NET 未使用 NuGet，您必須執行下列步驟 tooupdate tooa 較新版本的 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform hello following steps tooupdate tooa newer version:</span></span>
>
> 1. <span data-ttu-id="26826-305">在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="26826-305">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="26826-306">使用 hello**搜尋**欄位中搜尋，然後再新增， **Microsoft.SCP.Net.SDK** toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="26826-306">Using hello **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** toohello project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="26826-307">針對拓撲常見問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="26826-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="26826-308">Null 指標例外狀況</span><span class="sxs-lookup"><span data-stu-id="26826-308">Null pointer exceptions</span></span>

<span data-ttu-id="26826-309">當您使用 C# 拓撲與 linux 的 HDInsight 叢集時，閃電和 spout 使用的元件**ConfigurationManager** tooread 組態設定，在執行階段可能會傳回 null 指標例外狀況。</span><span class="sxs-lookup"><span data-stu-id="26826-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** tooread configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="26826-310">hello 專案組態傳入 hello Storm 拓撲中，為 hello 拓撲內容中的索引鍵和值組。</span><span class="sxs-lookup"><span data-stu-id="26826-310">hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="26826-311">它可以擷取從它們初始化時，傳遞 tooyour 元件 hello 字典物件。</span><span class="sxs-lookup"><span data-stu-id="26826-311">It can be retrieved from hello dictionary object that is passed tooyour components when they are initialized.</span></span>

<span data-ttu-id="26826-312">如需詳細資訊，請參閱 hello [ConfigurationManager](#configurationmanager)本文件一節。</span><span class="sxs-lookup"><span data-stu-id="26826-312">For more information, see hello [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="26826-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="26826-313">System.TypeLoadException</span></span>

<span data-ttu-id="26826-314">當您使用 C# 拓撲與 linux 的 HDInsight 叢集時，您可能會遇到下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter hello following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="26826-315">當您使用與.NET 的 Mono 支援 hello 版本不相容的二進位檔時，就會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="26826-315">This error occurs when you use a binary that is not compatible with hello version of .NET that Mono supports.</span></span>

<span data-ttu-id="26826-316">對於以 Linux 為基礎的 HDInsight 叢集，請確定專案使用針對 .NET 4.5 編譯的二進位檔。</span><span class="sxs-lookup"><span data-stu-id="26826-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="26826-317">在本機測試拓撲</span><span class="sxs-lookup"><span data-stu-id="26826-317">Test a topology locally</span></span>

<span data-ttu-id="26826-318">雖然它是簡單 toodeploy 拓撲 tooa 叢集，在某些情況下，您可能需要 tootest 在本機的拓撲。</span><span class="sxs-lookup"><span data-stu-id="26826-318">Although it is easy toodeploy a topology tooa cluster, in some cases, you may need tootest a topology locally.</span></span> <span data-ttu-id="26826-319">使用下列步驟 toorun hello 和測試 hello 範例拓撲在本教學課程，在本機開發環境中。</span><span class="sxs-lookup"><span data-stu-id="26826-319">Use hello following steps toorun and test hello example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="26826-320">本機測試只適用於僅限 C# 的基本拓撲。</span><span class="sxs-lookup"><span data-stu-id="26826-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="26826-321">您不得將本機測試使用於混合式拓撲或使用多個資料流的拓撲。</span><span class="sxs-lookup"><span data-stu-id="26826-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="26826-322">在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="26826-322">In **Solution Explorer**, right-click hello project, and select **Properties**.</span></span> <span data-ttu-id="26826-323">在 hello 專案屬性中，變更 hello**輸出類型**太**主控台應用程式**。</span><span class="sxs-lookup"><span data-stu-id="26826-323">In hello project properties, change hello **Output type** too**Console Application**.</span></span>

    ![醒目提示 [輸出] 類型的專案屬性螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="26826-325">請記住 toochange hello**輸出類型**太回**類別庫**hello 拓撲 tooa 叢集部署之前。</span><span class="sxs-lookup"><span data-stu-id="26826-325">Remember toochange hello **Output type** back too**Class Library** before you deploy hello topology tooa cluster.</span></span>

2. <span data-ttu-id="26826-326">在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**新增** > **新項目**。</span><span class="sxs-lookup"><span data-stu-id="26826-326">In **Solution Explorer**, right-click hello project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="26826-327">選取**類別**，並輸入**LocalTest.cs**與 hello 類別名稱。</span><span class="sxs-lookup"><span data-stu-id="26826-327">Select **Class**, and enter **LocalTest.cs** as hello class name.</span></span> <span data-ttu-id="26826-328">最後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="26826-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="26826-329">開啟**LocalTest.cs**，並加入下列 hello**使用**hello 上方的陳述式：</span><span class="sxs-lookup"><span data-stu-id="26826-329">Open **LocalTest.cs**, and add hello following **using** statement at hello top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="26826-330">使用 hello 下列程式碼做為 hello 內容的 hello **LocalTest**類別：</span><span class="sxs-lookup"><span data-stu-id="26826-330">Use hello following code as hello contents of hello **LocalTest** class:</span></span>

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="26826-331">需要一點時間 tooread 透過 hello 程式碼註解。</span><span class="sxs-lookup"><span data-stu-id="26826-331">Take a moment tooread through hello code comments.</span></span> <span data-ttu-id="26826-332">此程式碼使用**LocalContext** toorun hello 元件 hello 開發環境，並持續發生 hello hello 本機磁碟機上的元件 tootext 檔案之間的資料流。</span><span class="sxs-lookup"><span data-stu-id="26826-332">This code uses **LocalContext** toorun hello components in hello development environment, and it persists hello data stream between components tootext files on hello local drive.</span></span>

1. <span data-ttu-id="26826-333">開啟**Program.cs**，並加入下列 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="26826-333">Open **Program.cs**, and add hello following toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. <span data-ttu-id="26826-334">儲存 hello 變更，然後再按一下**F5**或選取**偵錯** > **開始偵錯**toostart hello 專案。</span><span class="sxs-lookup"><span data-stu-id="26826-334">Save hello changes, and then click **F5** or select **Debug** > **Start Debugging** toostart hello project.</span></span> <span data-ttu-id="26826-335">主控台視窗應該會出現，並身分 hello 測試進度的記錄狀態。</span><span class="sxs-lookup"><span data-stu-id="26826-335">A console window should appear, and log status as hello tests progress.</span></span> <span data-ttu-id="26826-336">當**測試完成**隨即出現，請按任何鍵 tooclose hello 視窗。</span><span class="sxs-lookup"><span data-stu-id="26826-336">When **Tests finished** appears, press any key tooclose hello window.</span></span>

3. <span data-ttu-id="26826-337">使用**Windows 檔案總管**toolocate hello 目錄，其中包含您的專案。</span><span class="sxs-lookup"><span data-stu-id="26826-337">Use **Windows Explorer** toolocate hello directory that contains your project.</span></span> <span data-ttu-id="26826-338">例如：**C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**。</span><span class="sxs-lookup"><span data-stu-id="26826-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="26826-339">在此目錄中，開啟 Bin，然後按一下偵錯。</span><span class="sxs-lookup"><span data-stu-id="26826-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="26826-340">您應該會看到 hello 測試執行時所產生的 hello 文字檔案： sentences.txt、 counter.txt 和 splitter.txt。</span><span class="sxs-lookup"><span data-stu-id="26826-340">You should see hello text files that were produced when hello tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="26826-341">開啟每個文字檔案，並檢查 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="26826-341">Open each text file and inspect hello data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="26826-342">字串資料會在這些檔案中保存為十進位值的陣列。</span><span class="sxs-lookup"><span data-stu-id="26826-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="26826-343">例如， \[[97,103,111]] 在 hello **splitter.txt**檔案是 hello 字*和*。</span><span class="sxs-lookup"><span data-stu-id="26826-343">For example, \[[97,103,111]] in hello **splitter.txt** file is hello word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="26826-344">要確定 tooset hello**專案類型**太回**類別庫**之前部署 tooa Storm HDInsight 叢集上的。</span><span class="sxs-lookup"><span data-stu-id="26826-344">Be sure tooset hello **Project type** back too**Class Library** before deploying tooa Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="26826-345">記錄資訊</span><span class="sxs-lookup"><span data-stu-id="26826-345">Log information</span></span>

<span data-ttu-id="26826-346">您可以使用 `Context.Logger`，輕鬆地記錄拓撲元件中的資訊。</span><span class="sxs-lookup"><span data-stu-id="26826-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="26826-347">例如，hello 下列範例會建立資訊的記錄項目：</span><span class="sxs-lookup"><span data-stu-id="26826-347">For example, hello following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="26826-348">可以檢視記錄的資訊從 hello **Hadoop 服務記錄檔**，找到**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="26826-348">Logged information can be viewed from hello **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="26826-349">展開您的 HDInsight 叢集的 Storm 的 hello 項目，然後展開**Hadoop 服務記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="26826-349">Expand hello entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="26826-350">最後，選取 hello 記錄檔案 tooview。</span><span class="sxs-lookup"><span data-stu-id="26826-350">Finally, select hello log file tooview.</span></span>

> [!NOTE]
> <span data-ttu-id="26826-351">hello 記錄檔會儲存在 hello Azure 儲存體帳戶，以供您的叢集。</span><span class="sxs-lookup"><span data-stu-id="26826-351">hello logs are stored in hello Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="26826-352">tooview hello 記錄檔，Visual Studio 中的，您必須登入 toohello 擁有 hello 儲存體帳戶的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="26826-352">tooview hello logs in Visual Studio, you must sign in toohello Azure subscription that owns hello storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="26826-353">檢視錯誤資訊</span><span class="sxs-lookup"><span data-stu-id="26826-353">View error information</span></span>

<span data-ttu-id="26826-354">tooview 錯誤發生在執行的拓撲中，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-354">tooview errors that have occurred in a running topology, use hello following steps:</span></span>

1. <span data-ttu-id="26826-355">從**伺服器總管**，hello Storm HDInsight 叢集上的按一下滑鼠右鍵，然後選取**檢視 Storm 拓撲**。</span><span class="sxs-lookup"><span data-stu-id="26826-355">From **Server Explorer**, right-click hello Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="26826-356">Hello **Spout**和**釘**，hello**最後一個錯誤**資料行包含 hello 最後一個錯誤的資訊。</span><span class="sxs-lookup"><span data-stu-id="26826-356">For hello **Spout** and **Bolts**, hello **Last Error** column contains information on hello last error.</span></span>

3. <span data-ttu-id="26826-357">選取 hello **Spout 識別碼**或**閃電識別碼**hello 元件列出發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="26826-357">Select hello **Spout Id** or **Bolt Id** for hello component that has an error listed.</span></span> <span data-ttu-id="26826-358">Hello 是顯示的其他錯誤的詳細資料頁面上列出資訊在 hello**錯誤**在 hello hello 頁面底部的區段。</span><span class="sxs-lookup"><span data-stu-id="26826-358">On hello details page that is displayed, additional error information is listed in hello **Errors** section at hello bottom of hello page.</span></span>

4. <span data-ttu-id="26826-359">tooobtain 的詳細資訊，選取**連接埠**從 hello**執行程式**hello 頁面區段、 toosee hello Storm 背景工作記錄檔中的 hello 最後幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="26826-359">tooobtain more information, select a **Port** from hello **Executors** section of hello page, toosee hello Storm worker log for hello last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="26826-360">提交拓撲的錯誤</span><span class="sxs-lookup"><span data-stu-id="26826-360">Errors submitting topologies</span></span>

<span data-ttu-id="26826-361">如果您遇到錯誤拓撲 tooHDInsight 送出時，您可以尋找記錄 hello 處理拓撲提交您的 HDInsight 叢集上的伺服器端元件。</span><span class="sxs-lookup"><span data-stu-id="26826-361">If you encounter errors submitting a topology tooHDInsight, you can find logs for hello server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="26826-362">tooretrieve 這些記錄檔時，下列命令，從命令列使用 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-362">tooretrieve these logs, use hello following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="26826-363">取代__sshuser__以 hello hello 叢集的 SSH 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="26826-363">Replace __sshuser__ with hello SSH user account for hello cluster.</span></span> <span data-ttu-id="26826-364">取代__clustername__ hello hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="26826-364">Replace __clustername__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="26826-365">如需搭配 HDInsight 使用 `scp` 和 `ssh` 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="26826-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="26826-366">提交失敗有多種原因：</span><span class="sxs-lookup"><span data-stu-id="26826-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="26826-367">JDK 未安裝或不在 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="26826-367">JDK is not installed or is not in hello path.</span></span>
* <span data-ttu-id="26826-368">必要的 Java 相依性不會包含在 hello 送出。</span><span class="sxs-lookup"><span data-stu-id="26826-368">Required Java dependencies are not included in hello submission.</span></span>
* <span data-ttu-id="26826-369">不相容的相依性。</span><span class="sxs-lookup"><span data-stu-id="26826-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="26826-370">重複的拓撲名稱。</span><span class="sxs-lookup"><span data-stu-id="26826-370">Duplicate topology names.</span></span>

<span data-ttu-id="26826-371">如果 hello`hdinsight-scpwebapi.out`記錄檔包含`FileNotFoundException`，這可能會因下列條件的 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-371">If hello `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by hello following conditions:</span></span>

* <span data-ttu-id="26826-372">hello JDK 不上 hello 開發環境的 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="26826-372">hello JDK is not in hello path on hello development environment.</span></span> <span data-ttu-id="26826-373">請確認該 hello hello 開發環境中，而且已安裝的 JDK `%JAVA_HOME%/bin` hello 路徑中。</span><span class="sxs-lookup"><span data-stu-id="26826-373">Verify that hello JDK is installed in hello development environment, and that `%JAVA_HOME%/bin` is in hello path.</span></span>
* <span data-ttu-id="26826-374">遺漏 Java 相依性。</span><span class="sxs-lookup"><span data-stu-id="26826-374">You are missing a Java dependency.</span></span> <span data-ttu-id="26826-375">請確定您同時納入任何必要的 d 檔案做為 hello 送出的一部分。</span><span class="sxs-lookup"><span data-stu-id="26826-375">Make sure you are including any required .jar files as part of hello submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26826-376">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26826-376">Next steps</span></span>

<span data-ttu-id="26826-377">如需從事件中樞處理資料的範例，請參閱[利用 Storm on HDInsight 處理 Azure 事件中樞的事件](hdinsight-storm-develop-csharp-event-hub-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="26826-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="26826-378">如需將資料流的資料分成多個資料流的 C# 拓撲範例，請參閱 [C# Storm 範例](https://github.com/Blackmist/csharp-storm-example)。</span><span class="sxs-lookup"><span data-stu-id="26826-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="26826-379">toodiscover 建立 C# 拓撲的相關詳細資訊，請參閱[GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md)。</span><span class="sxs-lookup"><span data-stu-id="26826-379">toodiscover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="26826-380">與 HDInsight 的更多方式 toowork 及多個出現之 HDInsight 範例，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="26826-380">For more ways toowork with HDInsight and more Storm on HDInsight samples, see hello following documents:</span></span>

<span data-ttu-id="26826-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="26826-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="26826-382">SCP 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="26826-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="26826-383">**Apache Storm on HDInsight**</span><span class="sxs-lookup"><span data-stu-id="26826-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="26826-384">使用 Apache Storm on HDInsight 部署和監視拓撲</span><span class="sxs-lookup"><span data-stu-id="26826-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="26826-385">Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="26826-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="26826-386">**Apache Hadoop on HDInsight**</span><span class="sxs-lookup"><span data-stu-id="26826-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="26826-387">搭配 HDInsight 上的 Hadoop 使用 Hive</span><span class="sxs-lookup"><span data-stu-id="26826-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="26826-388">搭配 HDInsight 上的 Hadoop 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="26826-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="26826-389">搭配 HDInsight 上的 Hadoop 使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="26826-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="26826-390">**Apache HBase on HDInsight**</span><span class="sxs-lookup"><span data-stu-id="26826-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="26826-391">開始使用 HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="26826-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)

---
title: "採用 Visual Studio 和 C# 的 Apache Storm 拓撲 - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 C# 建立 Storm 拓撲。 使用適用於 Visual Studio 的 Hadoop 工具在 Visual Studio 中建立簡單的字數統計拓撲。"
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
ms.openlocfilehash: 3ee89b6644ba395e0a6c28ecc2c082c2f7393ac8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="7ed82-104">使用 Data Lake Tools for Visual Studio 開發 Apache Storm 的 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="7ed82-104">Develop C# topologies for Apache Storm by using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="7ed82-105">了解如何使用 Azure Data Lake (Hadoop) Tools for Visual Studio 來建立 C# Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-105">Learn how to create a C# Storm topology by using the Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="7ed82-106">這份文件逐步解說如何在 Visual Studio 中建立 Storm 專案，在本機測試該專案，並將它部署至 Azure HDInsight 叢集上的 Apache Storm。</span><span class="sxs-lookup"><span data-stu-id="7ed82-106">This document walks through the process of creating a Storm project in Visual Studio, testing it locally, and deploying it to an Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="7ed82-107">您也會學習如何建立使用 C# 和 Java 元件的混合式拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-107">You also learn how to create hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="7ed82-108">雖然本文件中的步驟依賴 Windows 開發環境與 Visual Studio，但已編譯的專案可以提交到以 Linux 或 Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="7ed82-108">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="7ed82-109">只有在 2016 年 10 月 28 日之後所建立之以 Linux 為基礎的叢集可支援 SCP.NET 拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="7ed82-110">若要搭配使用 C# 拓撲與以 Linux 為基礎的叢集，您必須將專案使用的 Microsoft.SCP.Net.SDK NuGet 套件更新為 0.10.0.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="7ed82-110">To use a C# topology with a Linux-based cluster, you must update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or later.</span></span> <span data-ttu-id="7ed82-111">套件版本也必須符合 HDInsight 上安裝的 Storm 主要版本。</span><span class="sxs-lookup"><span data-stu-id="7ed82-111">The version of the package must also match the major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="7ed82-112">HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="7ed82-112">HDInsight version</span></span> | <span data-ttu-id="7ed82-113">Storm 版本</span><span class="sxs-lookup"><span data-stu-id="7ed82-113">Storm version</span></span> | <span data-ttu-id="7ed82-114">SCP.NET 版本</span><span class="sxs-lookup"><span data-stu-id="7ed82-114">SCP.NET version</span></span> | <span data-ttu-id="7ed82-115">預設 Mono 版本</span><span class="sxs-lookup"><span data-stu-id="7ed82-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="7ed82-116">3.3</span><span class="sxs-lookup"><span data-stu-id="7ed82-116">3.3</span></span> |<span data-ttu-id="7ed82-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="7ed82-117">0.10.x</span></span> |<span data-ttu-id="7ed82-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="7ed82-118">0.10.x.x</span></span></br><span data-ttu-id="7ed82-119">(僅限以 Windows 為基礎的 HDInsight)</span><span class="sxs-lookup"><span data-stu-id="7ed82-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="7ed82-120">NA</span><span class="sxs-lookup"><span data-stu-id="7ed82-120">NA</span></span> |
| <span data-ttu-id="7ed82-121">3.4</span><span class="sxs-lookup"><span data-stu-id="7ed82-121">3.4</span></span> | <span data-ttu-id="7ed82-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="7ed82-122">0.10.0.x</span></span> | <span data-ttu-id="7ed82-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="7ed82-123">0.10.0.x</span></span> | <span data-ttu-id="7ed82-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="7ed82-124">3.2.8</span></span> |
| <span data-ttu-id="7ed82-125">3.5</span><span class="sxs-lookup"><span data-stu-id="7ed82-125">3.5</span></span> | <span data-ttu-id="7ed82-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="7ed82-126">1.0.2.x</span></span> | <span data-ttu-id="7ed82-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="7ed82-127">1.0.0.x</span></span> | <span data-ttu-id="7ed82-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="7ed82-128">4.2.1</span></span> |
| <span data-ttu-id="7ed82-129">3.6</span><span class="sxs-lookup"><span data-stu-id="7ed82-129">3.6</span></span> | <span data-ttu-id="7ed82-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="7ed82-130">1.1.0.x</span></span> | <span data-ttu-id="7ed82-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="7ed82-131">1.0.0.x</span></span> | <span data-ttu-id="7ed82-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="7ed82-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="7ed82-133">在以 Linux 為基礎之叢集上的 C# 拓撲必須使用 .NET 4.5，並使用 Mono 以在 HDInsight 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="7ed82-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="7ed82-134">查看 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/) \(英文\) 以了解可能的不相容情形。</span><span class="sxs-lookup"><span data-stu-id="7ed82-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="7ed82-135">安裝 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7ed82-135">Install Visual Studio</span></span>

<span data-ttu-id="7ed82-136">您可以使用下列其中一種 Visual Studio 版本來搭配 SCP.NET 開發 C# 拓撲：</span><span class="sxs-lookup"><span data-stu-id="7ed82-136">You can develop C# topologies with SCP.NET by using one of the following versions of Visual Studio:</span></span>

* <span data-ttu-id="7ed82-137">Visual Studio 2012 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="7ed82-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="7ed82-138">Visual Studio 2013 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=44921) 或 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="7ed82-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="7ed82-139">Visual Studio 2015 或 [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="7ed82-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="7ed82-140">Visual Studio 2017 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="7ed82-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="7ed82-141">安裝 Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7ed82-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="7ed82-142">若要安裝 Data Lake Tools for Visual Studio，請遵循[開始使用 Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="7ed82-142">To install Data Lake tools for Visual Studio, follow the steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="7ed82-143">安裝 Java</span><span class="sxs-lookup"><span data-stu-id="7ed82-143">Install Java</span></span>

<span data-ttu-id="7ed82-144">當您從 Visual Studio 提交 Storm 拓撲時，SCP.NET 會產生包含拓撲及相依性的 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="7ed82-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains the topology and dependencies.</span></span> <span data-ttu-id="7ed82-145">系統會使用 Java 來建立這些 ZIP 檔案，因為它所使用的格式和以 Linux 為基礎的叢集更具相容性。</span><span class="sxs-lookup"><span data-stu-id="7ed82-145">Java is used to create these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="7ed82-146">在您的開發環境上安裝 Java Developer Kit (JDK) 7 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="7ed82-146">Install the Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="7ed82-147">您可以從 [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html) \(英文\) 取得 Oracle JDK。</span><span class="sxs-lookup"><span data-stu-id="7ed82-147">You can get the Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="7ed82-148">您也可以使用[其他 Java 發佈](http://openjdk.java.net/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7ed82-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="7ed82-149">`JAVA_HOME` 環境變數必須指向包含 Java 的目錄。</span><span class="sxs-lookup"><span data-stu-id="7ed82-149">The `JAVA_HOME` environment variable must point to the directory that contains Java.</span></span>

3. <span data-ttu-id="7ed82-150">`PATH` 環境變數必須包括 `%JAVA_HOME%\bin` 目錄。</span><span class="sxs-lookup"><span data-stu-id="7ed82-150">The `PATH` environment variable must include the `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="7ed82-151">您可以使用下列的 C# 主控台應用程式來確認 Java 和 JDK 是否已正確安裝：</span><span class="sxs-lookup"><span data-stu-id="7ed82-151">You can use the following C# console application to verify that Java and the JDK are correctly installed:</span></span>

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

## <a name="storm-templates"></a><span data-ttu-id="7ed82-152">Storm 範本</span><span class="sxs-lookup"><span data-stu-id="7ed82-152">Storm templates</span></span>

<span data-ttu-id="7ed82-153">Data Lake Tools for Visual Studio 提供下列範本：</span><span class="sxs-lookup"><span data-stu-id="7ed82-153">The Data Lake tools for Visual Studio provide the following templates:</span></span>

| <span data-ttu-id="7ed82-154">專案類型</span><span class="sxs-lookup"><span data-stu-id="7ed82-154">Project type</span></span> | <span data-ttu-id="7ed82-155">示範</span><span class="sxs-lookup"><span data-stu-id="7ed82-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="7ed82-156">Storm 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ed82-156">Storm Application</span></span> |<span data-ttu-id="7ed82-157">空白 Storm 拓撲專案。</span><span class="sxs-lookup"><span data-stu-id="7ed82-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="7ed82-158">Storm Azure SQL 寫入器範例</span><span class="sxs-lookup"><span data-stu-id="7ed82-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="7ed82-159">如何寫入至 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="7ed82-159">How to write to Azure SQL Database.</span></span> |
| <span data-ttu-id="7ed82-160">Storm Azure Cosmos DB 讀取器範例</span><span class="sxs-lookup"><span data-stu-id="7ed82-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="7ed82-161">如何從 Azure Cosmos DB 讀取。</span><span class="sxs-lookup"><span data-stu-id="7ed82-161">How to read from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="7ed82-162">Storm Azure Cosmos DB 寫入器範例</span><span class="sxs-lookup"><span data-stu-id="7ed82-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="7ed82-163">如何寫入至 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="7ed82-163">How to write to Azure Cosmos DB.</span></span> |
| <span data-ttu-id="7ed82-164">Storm EventHub 讀取器範例</span><span class="sxs-lookup"><span data-stu-id="7ed82-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="7ed82-165">如何從 Azure 事件中樞讀取。</span><span class="sxs-lookup"><span data-stu-id="7ed82-165">How to read from Azure Event Hubs.</span></span> |
| <span data-ttu-id="7ed82-166">Storm EventHub 寫入器範例</span><span class="sxs-lookup"><span data-stu-id="7ed82-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="7ed82-167">如何寫入至 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="7ed82-167">How to write to Azure Event Hubs.</span></span> |
| <span data-ttu-id="7ed82-168">Storm HBase 讀取器範例</span><span class="sxs-lookup"><span data-stu-id="7ed82-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="7ed82-169">如何從 HDInsight 叢集上的 HBase 讀取。</span><span class="sxs-lookup"><span data-stu-id="7ed82-169">How to read from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="7ed82-170">Storm HBase 寫入器範例</span><span class="sxs-lookup"><span data-stu-id="7ed82-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="7ed82-171">如何寫入至 HDInsight 叢集上的 HBase。</span><span class="sxs-lookup"><span data-stu-id="7ed82-171">How to write to HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="7ed82-172">Storm 混合式範例</span><span class="sxs-lookup"><span data-stu-id="7ed82-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="7ed82-173">如何使用 Java 元件。</span><span class="sxs-lookup"><span data-stu-id="7ed82-173">How to use a Java component.</span></span> |
| <span data-ttu-id="7ed82-174">Storm 範例</span><span class="sxs-lookup"><span data-stu-id="7ed82-174">Storm Sample</span></span> |<span data-ttu-id="7ed82-175">基本的字數統計拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="7ed82-176">並非所有範本都能與 Linux 架構的 HDInsight 搭配運作。</span><span class="sxs-lookup"><span data-stu-id="7ed82-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="7ed82-177">範本所使用的 Nuget 套件可能無法與 Mono 相容。</span><span class="sxs-lookup"><span data-stu-id="7ed82-177">Nuget packages used by the templates may not be compatible with Mono.</span></span> <span data-ttu-id="7ed82-178">請查看 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/)文件，並使用 [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) 來找出潛在問題。</span><span class="sxs-lookup"><span data-stu-id="7ed82-178">Check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use the [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) to identify potential problems.</span></span>

<span data-ttu-id="7ed82-179">在這份文件的步驟中，您會使用基本 Storm 應用程式專案類型來建立拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-179">In the steps in this document, you use the basic Storm Application project type to create a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="7ed82-180">HBase 範本注意事項</span><span class="sxs-lookup"><span data-stu-id="7ed82-180">HBase templates notes</span></span>

<span data-ttu-id="7ed82-181">HBase 讀取器和寫入器範本會使用 HBase REST API (而不是 HBase Java API) 來與 HDInsight 叢集上的 HBase 通訊。</span><span class="sxs-lookup"><span data-stu-id="7ed82-181">The HBase reader and writer templates use the HBase REST API, not the HBase Java API, to communicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="7ed82-182">EventHub 範本注意事項</span><span class="sxs-lookup"><span data-stu-id="7ed82-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ed82-183">包含在 EventHub Reader 讀取器範本中，以 Java 為基礎的 EventHub Spout 元件可能無法與 Storm on HDInsight 3.5 版或更新版本搭配使用。</span><span class="sxs-lookup"><span data-stu-id="7ed82-183">The Java-based EventHub spout component included with the EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="7ed82-184">此元件的更新版本可在 [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib) \(英文\) 取得。</span><span class="sxs-lookup"><span data-stu-id="7ed82-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="7ed82-185">如需使用此元件和搭配 Storm on HDInsight 3.5 使用的範例拓撲，請參閱 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7ed82-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="7ed82-186">建立 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="7ed82-186">Create a C# topology</span></span>

1. <span data-ttu-id="7ed82-187">開啟 Visual Studio，選取 [檔案] > [新增]，然後選取 [專案]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="7ed82-188">從 [新增專案] 視窗，展開 [已安裝] > [範本]，然後選取 [Azure Data Lake]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-188">From the **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="7ed82-189">從範本清單中，選取 [Storm 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-189">From the list of templates, select **Storm Application**.</span></span> <span data-ttu-id="7ed82-190">在畫面底部，輸入 **WordCount** 做為應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="7ed82-190">At the bottom of the screen, enter **WordCount** as the name of the application.</span></span>

    ![[新增專案] 視窗的螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="7ed82-192">建立專案之後，您應該會有下列檔案：</span><span class="sxs-lookup"><span data-stu-id="7ed82-192">After you have created the project, you should have the following files:</span></span>

   * <span data-ttu-id="7ed82-193">**Program.cs**：此檔案會定義您專案的拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-193">**Program.cs**: This file defines the topology for your project.</span></span> <span data-ttu-id="7ed82-194">預設會建立含有一個 Spout 和一個 Bolt 的預設拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="7ed82-195">**Spout.cs**：發出亂數的範例 Spout。</span><span class="sxs-lookup"><span data-stu-id="7ed82-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="7ed82-196">**Bolt.cs**：保留 Spout 所發出數字之計數的範例 Bolt。</span><span class="sxs-lookup"><span data-stu-id="7ed82-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by the spout.</span></span>

     <span data-ttu-id="7ed82-197">當您建立專案時，NuGet 會下載最新的 [SCP.NET 套件](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7ed82-197">When you create the project, NuGet downloads the latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-the-spout"></a><span data-ttu-id="7ed82-198">實作 Spout</span><span class="sxs-lookup"><span data-stu-id="7ed82-198">Implement the spout</span></span>

1. <span data-ttu-id="7ed82-199">開啟 **Spout.cs**。</span><span class="sxs-lookup"><span data-stu-id="7ed82-199">Open **Spout.cs**.</span></span> <span data-ttu-id="7ed82-200">Spout 是用來讀取來自外部來源之拓撲中的資料。</span><span class="sxs-lookup"><span data-stu-id="7ed82-200">Spouts are used to read data in a topology from an external source.</span></span> <span data-ttu-id="7ed82-201">Spout 的主要元件如下：</span><span class="sxs-lookup"><span data-stu-id="7ed82-201">The main components for a spout are:</span></span>

   * <span data-ttu-id="7ed82-202">**NextTuple**：允許 Spout 發出新的 Tuple 時，由 Storm 所呼叫。</span><span class="sxs-lookup"><span data-stu-id="7ed82-202">**NextTuple**: Called by Storm when the spout is allowed to emit new tuples.</span></span>

   * <span data-ttu-id="7ed82-203">**Ack** (僅限交易式拓撲)：針對從 Spout 傳送的 Tuple，處理拓撲中其他元件所起始的認可。</span><span class="sxs-lookup"><span data-stu-id="7ed82-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in the topology for tuples sent from the spout.</span></span> <span data-ttu-id="7ed82-204">認可 Tuple 可讓 Spout 知道下游元件已順利處理 Tuple。</span><span class="sxs-lookup"><span data-stu-id="7ed82-204">Acknowledging a tuple lets the spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="7ed82-205">**Fail** (僅限交易式拓撲)：處理無法處理拓撲中之其他元件的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="7ed82-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in the topology.</span></span> <span data-ttu-id="7ed82-206">實作 Fail 方法可讓您重新發出 Tuple，以便再次處理它。</span><span class="sxs-lookup"><span data-stu-id="7ed82-206">Implementing a Fail method allows you to re-emit the tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="7ed82-207">將 **Spout** 類別的內容取代為下文字。</span><span class="sxs-lookup"><span data-stu-id="7ed82-207">Replace the contents of the **Spout** class with the following text.</span></span> <span data-ttu-id="7ed82-208">此 spout 會將句子隨機發出至拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-208">This spout randomly emits a sentence into the topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "the cow jumped over the moon",
        "an apple a day keeps the doctor away",
        "four score and seven years ago",
        "snow white and the seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set the instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // The schema for the default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of the spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // The sentence to be emitted
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

### <a name="implement-the-bolts"></a><span data-ttu-id="7ed82-209">實作 Bolt</span><span class="sxs-lookup"><span data-stu-id="7ed82-209">Implement the bolts</span></span>

1. <span data-ttu-id="7ed82-210">刪除專案中的現有 **Bolt.cs** 檔。</span><span class="sxs-lookup"><span data-stu-id="7ed82-210">Delete the existing **Bolt.cs** file from the project.</span></span>

2. <span data-ttu-id="7ed82-211">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取 [新增] > [新項目]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-211">In **Solution Explorer**, right-click the project, and select **Add** > **New item**.</span></span> <span data-ttu-id="7ed82-212">從清單中，選取 [Storm Bolt]，並輸入 **Splitter.cs** 做為名稱。</span><span class="sxs-lookup"><span data-stu-id="7ed82-212">From the list, select **Storm Bolt**, and enter **Splitter.cs** as the name.</span></span> <span data-ttu-id="7ed82-213">重複此程序，以建立名為 **Counter.cs** 的第二個 Bolt。</span><span class="sxs-lookup"><span data-stu-id="7ed82-213">Repeat this process to create a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="7ed82-214">**Splitter.cs**：實作會將句子分成個別單字，並發出一串新文字的 Bolt。</span><span class="sxs-lookup"><span data-stu-id="7ed82-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="7ed82-215">**Counter.cs**：實作會計算每個單字的數目，並發出一串新文字和每個單字計數的 Bolt。</span><span class="sxs-lookup"><span data-stu-id="7ed82-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and the count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7ed82-216">這些 Bolt 會讀取和寫入資料流，但是您也可以使用 Bolt 與資料庫或服務等來源進行通訊。</span><span class="sxs-lookup"><span data-stu-id="7ed82-216">These bolts read and write to streams, but you can also use a bolt to communicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="7ed82-217">開啟 **Splitter.cs**。</span><span class="sxs-lookup"><span data-stu-id="7ed82-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="7ed82-218">它預設只有一個方法：**Execute**。</span><span class="sxs-lookup"><span data-stu-id="7ed82-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="7ed82-219">這是在 Bolt 收到要處理的 Tuple 時所呼叫的執行方法。</span><span class="sxs-lookup"><span data-stu-id="7ed82-219">The Execute method is called when the bolt receives a tuple for processing.</span></span> <span data-ttu-id="7ed82-220">此時，您可以讀取和處理內送 Tuple，以及發出輸出 Tuple。</span><span class="sxs-lookup"><span data-stu-id="7ed82-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="7ed82-221">將 **Splitter** 類別的內容取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="7ed82-221">Replace the contents of the **Splitter** class with the following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (the sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (the word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of the bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get the sentence from the tuple
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

5. <span data-ttu-id="7ed82-222">開啟 **Counter.cs**，並將類別內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="7ed82-222">Open **Counter.cs**, and replace the class contents with the following:</span></span>

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
        // A tuple containing a string field - the word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - the word and the word count
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

        // Get the word from the tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for the word in the dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment the count
        count++;
        // Update the count in the dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit the word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-the-topology"></a><span data-ttu-id="7ed82-223">定義拓撲</span><span class="sxs-lookup"><span data-stu-id="7ed82-223">Define the topology</span></span>

<span data-ttu-id="7ed82-224">Spout 和 Bolt 是以圖形方式排列，用以定義資料在元件之間的流動方式。</span><span class="sxs-lookup"><span data-stu-id="7ed82-224">Spouts and bolts are arranged in a graph, which defines how the data flows between components.</span></span> <span data-ttu-id="7ed82-225">此拓撲的圖形如下：</span><span class="sxs-lookup"><span data-stu-id="7ed82-225">For this topology, the graph is as follows:</span></span>

![元件排列方式的圖表](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="7ed82-227">句子是從 Spout 發出，並分散到 Splitter Bolt 執行個體。</span><span class="sxs-lookup"><span data-stu-id="7ed82-227">Sentences are emitted from the spout, and are distributed to instances of the Splitter bolt.</span></span> <span data-ttu-id="7ed82-228">Splitter Bolt 會將句子分成多個單字，並將這些單字分散到 Counter Bolt。</span><span class="sxs-lookup"><span data-stu-id="7ed82-228">The Splitter bolt breaks the sentences into words, which are distributed to the Counter bolt.</span></span>

<span data-ttu-id="7ed82-229">因為字數會本機保留在 Counter 執行個體中，所以我們想要確保特定單字流向相同的 Counter Bolt 執行個體。</span><span class="sxs-lookup"><span data-stu-id="7ed82-229">Because word count is held locally in the Counter instance, we want to make sure that specific words flow to the same Counter bolt instance.</span></span> <span data-ttu-id="7ed82-230">每個執行個體會保持追蹤特定文字。</span><span class="sxs-lookup"><span data-stu-id="7ed82-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="7ed82-231">分割器 Bolt 會維持無狀態，因為分割器的哪個執行個體收到哪個句子並不重要。</span><span class="sxs-lookup"><span data-stu-id="7ed82-231">Since the Splitter bolt maintains no state, it really doesn't matter which instance of the splitter receives which sentence.</span></span>

<span data-ttu-id="7ed82-232">開啟 **Program.cs**。</span><span class="sxs-lookup"><span data-stu-id="7ed82-232">Open **Program.cs**.</span></span> <span data-ttu-id="7ed82-233">重要的方法是 **GetTopologyBuilder**，其用來定義提交至 Storm 的拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-233">The important method is **GetTopologyBuilder**, which is used to define the topology that is submitted to Storm.</span></span> <span data-ttu-id="7ed82-234">將 **GetTopologyBuilder** 的內容取代為下列程式碼，以實作先前所述的拓撲：</span><span class="sxs-lookup"><span data-stu-id="7ed82-234">Replace the contents of **GetTopologyBuilder** with the following code to implement the topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add the spout to the topology.
// Name the component 'sentences'
// Name the field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add the splitter bolt to the topology.
// Name the component 'splitter'
// Name the field that is emitted 'word'
// Use suffleGrouping to distribute incoming tuples
//   from the 'sentences' spout across instances
//   of the splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add the counter bolt to the topology.
// Name the component 'counter'
// Name the fields that are emitted 'word' and 'count'
// Use fieldsGrouping to ensure that tuples are routed
//   to counter instances based on the contents of field
//   position 0 (the word). This could also have been
//   List<string>(){"word"}.
//   This ensures that the word 'jumped', for example, will always
//   go to the same instance
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

## <a name="submit-the-topology"></a><span data-ttu-id="7ed82-235">提交拓撲</span><span class="sxs-lookup"><span data-stu-id="7ed82-235">Submit the topology</span></span>

1. <span data-ttu-id="7ed82-236">在 [方案總管] 中，於專案上按一下滑鼠右鍵，然後選取 [提交至 Storm on HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-236">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7ed82-237">如果出現提示，請輸入您 Azure 訂用帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="7ed82-237">If prompted, enter the credentials for your Azure subscription.</span></span> <span data-ttu-id="7ed82-238">如果您有多個訂用帳戶，請登入包含 Storm on HDInsight 叢集的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ed82-238">If you have more than one subscription, sign in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="7ed82-239">從 [Storm 叢集] 下拉式清單中選取 Storm on HDInsight 叢集，然後選取 [提交]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-239">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="7ed82-240">您可以使用 [輸出]  視窗監視提交是否成功。</span><span class="sxs-lookup"><span data-stu-id="7ed82-240">You can monitor if the submission is successful by using the **Output** window.</span></span>

3. <span data-ttu-id="7ed82-241">順利提交拓撲時，應該會出現叢集的 [Storm 拓撲]  。</span><span class="sxs-lookup"><span data-stu-id="7ed82-241">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="7ed82-242">從清單中選取 [WordCount]  拓撲，以檢視執行中拓撲的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7ed82-242">Select the **WordCount** topology from the list to view information about the running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7ed82-243">您也可以從 [伺服器總管] 檢視 [Storm 拓撲]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="7ed82-244">展開 [Azure] > [HDInsight]，以滑鼠右鍵按一下 Storm on HDInsight 叢集，然後選取 [檢視 Storm 拓撲]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="7ed82-245">若要檢視拓撲中元件的相關資訊，請按兩下圖表中的元件。</span><span class="sxs-lookup"><span data-stu-id="7ed82-245">To view information about the components in the topology, double-click the component in the diagram.</span></span>

4. <span data-ttu-id="7ed82-246">從 [拓撲摘要] 檢視中，按一下 [終止] 停止拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-246">From the **Topology Summary** view, click **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7ed82-247">除非停用 Storm 拓撲或刪除叢集，否則 Storm 拓撲會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="7ed82-247">Storm topologies continue to run until they are deactivated, or the cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="7ed82-248">交易式拓撲</span><span class="sxs-lookup"><span data-stu-id="7ed82-248">Transactional topology</span></span>

<span data-ttu-id="7ed82-249">先前的拓撲為非交易式。</span><span class="sxs-lookup"><span data-stu-id="7ed82-249">The previous topology is non-transactional.</span></span> <span data-ttu-id="7ed82-250">拓撲中的元件不會實作功能來重新執行訊息。</span><span class="sxs-lookup"><span data-stu-id="7ed82-250">The components in the topology do not implement functionality to replaying messages.</span></span> <span data-ttu-id="7ed82-251">針對交易式拓撲範例，請建立專案，然後選取 [Storm 範例] 做為專案類型。</span><span class="sxs-lookup"><span data-stu-id="7ed82-251">For an example of a transactional topology, create a project and select **Storm Sample** as the project type.</span></span>

<span data-ttu-id="7ed82-252">交易式拓撲會實作下列項目來支援重新執行資料：</span><span class="sxs-lookup"><span data-stu-id="7ed82-252">Transactional topologies implement the following to support replay of data:</span></span>

* <span data-ttu-id="7ed82-253">**中繼資料快取**：Spout 必須儲存所發出資料的中繼資料，這樣一來，於失敗時就可以重新擷取和發出資料。</span><span class="sxs-lookup"><span data-stu-id="7ed82-253">**Metadata caching**: The spout must store metadata about the data emitted, so that the data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="7ed82-254">此範例所發出的資料太少，因此為了重新執行，每個 Tuple 的原始資料都會儲存在字典中。</span><span class="sxs-lookup"><span data-stu-id="7ed82-254">Because the data emitted by the sample is small, the raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="7ed82-255">**Ack**：拓撲中的每個 Bolt 都可以呼叫 `this.ctx.Ack(tuple)` 來認可它已順利處理 Tuple。</span><span class="sxs-lookup"><span data-stu-id="7ed82-255">**Ack**: Each bolt in the topology can call `this.ctx.Ack(tuple)` to acknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="7ed82-256">所有 Bolt 都已認可 Tuple 之後，即會叫用 Spout 的 `Ack` 方法。</span><span class="sxs-lookup"><span data-stu-id="7ed82-256">When all bolts have acked the tuple, the `Ack` method of the spout is invoked.</span></span> <span data-ttu-id="7ed82-257">`Ack` 方法可讓 Spout 移除快取以重新執行的資料。</span><span class="sxs-lookup"><span data-stu-id="7ed82-257">The `Ack` method allows the spout to remove data that was cached for replay.</span></span>

* <span data-ttu-id="7ed82-258">**Fail**：每個 Bolt 都可以呼叫 `this.ctx.Fail(tuple)`，以指出 Tuple 的處理失敗。</span><span class="sxs-lookup"><span data-stu-id="7ed82-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` to indicate that processing has failed for a tuple.</span></span> <span data-ttu-id="7ed82-259">這項失敗會傳播至 Spout 的 `Fail` 方法，在其中，可以使用快取的中繼資料來重新執行 Tuple。</span><span class="sxs-lookup"><span data-stu-id="7ed82-259">The failure propagates to the `Fail` method of the spout, where the tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="7ed82-260">**序列識別碼**：發出 Tuple 時，可以指定唯一的序列識別碼。</span><span class="sxs-lookup"><span data-stu-id="7ed82-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="7ed82-261">這個值可識別用於重新執行 (Ack 和 Fail) 處理的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="7ed82-261">This value identifies the tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="7ed82-262">例如，發出資料時，[Storm 範例]  專案中的 Spout 會使用下列項目：</span><span class="sxs-lookup"><span data-stu-id="7ed82-262">For example, the spout in the **Storm Sample** project uses the following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="7ed82-263">此程式碼會發出含有預設資料流之句子的 Tuple，以及 **lastSeqId** 中所含的序列識別碼值。</span><span class="sxs-lookup"><span data-stu-id="7ed82-263">This code emits a tuple that contains a sentence to the default stream, with the sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="7ed82-264">在此範例中，會遞增每個發出 Tuple 的 **lastSeqId**。</span><span class="sxs-lookup"><span data-stu-id="7ed82-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="7ed82-265">如 [Storm 範例] 專案中所示，在執行階段可以根據組態來設定元件是否為交易式。</span><span class="sxs-lookup"><span data-stu-id="7ed82-265">As demonstrated in the **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="7ed82-266">採用 C# 和 Java 的混合式拓撲</span><span class="sxs-lookup"><span data-stu-id="7ed82-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="7ed82-267">您也可以使用 Data Lake Tools for Visual Studio 來建立混合式拓撲，其中有些元件是 C#，有些則是 Java。</span><span class="sxs-lookup"><span data-stu-id="7ed82-267">You can also use Data Lake tools for Visual Studio to create hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="7ed82-268">針對混合式拓撲範例，請建立專案，然後選取 [Storm 混合式範例]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="7ed82-269">此範例類型將示範下列概念︰</span><span class="sxs-lookup"><span data-stu-id="7ed82-269">This sample type demonstrates the following concepts:</span></span>

* <span data-ttu-id="7ed82-270">**Java Spout** 和 **C# Bolt**：定義於 **HybridTopology_javaSpout_csharpBolt**。</span><span class="sxs-lookup"><span data-stu-id="7ed82-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="7ed82-271">交易式版本定義於 **HybridTopologyTx_javaSpout_csharpBolt**。</span><span class="sxs-lookup"><span data-stu-id="7ed82-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="7ed82-272">**C# Spout** 和 **Java Bolt**：定義於 **HybridTopology_csharpSpout_javaBolt**。</span><span class="sxs-lookup"><span data-stu-id="7ed82-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="7ed82-273">交易式版本定義於 **HybridTopologyTx_csharpSpout_javaBolt**。</span><span class="sxs-lookup"><span data-stu-id="7ed82-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7ed82-274">這個版本也會示範如何使用文字檔中的 Clojure 程式碼做為 Java 元件。</span><span class="sxs-lookup"><span data-stu-id="7ed82-274">This version also demonstrates how to use Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="7ed82-275">若要切換為提交專案時所使用的拓撲，只要在提交至叢集之前將 `[Active(true)]` 陳述式移至您要使用的拓撲即可。</span><span class="sxs-lookup"><span data-stu-id="7ed82-275">To switch the topology that is used when the project is submitted, simply move the `[Active(true)]` statement to the topology you want to use, before submitting it to the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="7ed82-276">在 **JavaDependency** 資料夾中，所需的所有 Java 檔案都會提供為此專案的一部分。</span><span class="sxs-lookup"><span data-stu-id="7ed82-276">All the Java files that are required are provided as part of this project in the **JavaDependency** folder.</span></span>

<span data-ttu-id="7ed82-277">當您建立和提交混合式拓撲時，請考慮下列項目：</span><span class="sxs-lookup"><span data-stu-id="7ed82-277">Consider the following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="7ed82-278">您必須使用 **JavaComponentConstructor** 來建立 Spout 或 Bolt 之 Java 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="7ed82-278">You must use **JavaComponentConstructor** to create an instance of the Java class for a spout or bolt.</span></span>

* <span data-ttu-id="7ed82-279">您應該使用 **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** 來將進入或離開 Java 元件的資料從 Java 物件序列化至 JSON。</span><span class="sxs-lookup"><span data-stu-id="7ed82-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** to serialize data into or out of Java components from Java objects to JSON.</span></span>

* <span data-ttu-id="7ed82-280">提交拓撲至伺服器時，您必須使用 [其他組態] 選項指定 [Java 檔案路徑]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-280">When submitting the topology to the server, you must use the **Additional configurations** option to specify the **Java File paths**.</span></span> <span data-ttu-id="7ed82-281">指定的路徑應該是含有 JAR 檔案的目錄，而 JAR 檔案包含您的 Java 類別。</span><span class="sxs-lookup"><span data-stu-id="7ed82-281">The path specified should be the directory that contains the JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="7ed82-282">Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="7ed82-282">Azure Event Hubs</span></span>

<span data-ttu-id="7ed82-283">SCP.NET 0.9.4.203 版引進了專用於事件中樞 Spout (從事件中樞讀取的 Java Spout) 的新類別和方法。</span><span class="sxs-lookup"><span data-stu-id="7ed82-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with the Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="7ed82-284">當您建立採用事件中樞 Spout 的拓撲時，請使用下列方法：</span><span class="sxs-lookup"><span data-stu-id="7ed82-284">When you create a topology that uses an Event Hub spout, use the following methods:</span></span>

* <span data-ttu-id="7ed82-285">**EventHubSpoutConfig** 類別：建立一個物件，其中包含 Spout 元件的設定。</span><span class="sxs-lookup"><span data-stu-id="7ed82-285">**EventHubSpoutConfig** class: Creates an object that contains the configuration for the spout component.</span></span>

* <span data-ttu-id="7ed82-286">**TopologyBuilder.SetEventHubSpout** 方法：將事件中樞 Spout 元件加入至拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-286">**TopologyBuilder.SetEventHubSpout** method: Adds the Event Hub spout component to the topology.</span></span>

> [!NOTE]
> <span data-ttu-id="7ed82-287">您仍然必須使用 **CustomizedInteropJSONSerializer** 來序列化 Spout 所產生的資料。</span><span class="sxs-lookup"><span data-stu-id="7ed82-287">You must still use the **CustomizedInteropJSONSerializer** to serialize data produced by the spout.</span></span>

## <span data-ttu-id="7ed82-288"><a id="configurationmanager"></a>使用 ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="7ed82-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="7ed82-289">請勿使用 **ConfigurationManager** 從 Bolt 和 Spout 元件擷取設定值。</span><span class="sxs-lookup"><span data-stu-id="7ed82-289">Don't use **ConfigurationManager** to retrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="7ed82-290">這麼做會導致 Null 指標例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7ed82-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="7ed82-291">相反地，專案設定會以拓撲內容中金鑰和值組的形式傳遞至 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-291">Instead, the configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="7ed82-292">仰賴組態值的每個元件則必須在初始化期間從內容擷取這些組態值。</span><span class="sxs-lookup"><span data-stu-id="7ed82-292">Each component that relies on configuration values must retrieve them from the context during initialization.</span></span>

<span data-ttu-id="7ed82-293">下列程式碼示範如何擷取這些值︰</span><span class="sxs-lookup"><span data-stu-id="7ed82-293">The following code demonstrates how to retrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // To hold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of the context for this component instance
        this.ctx = ctx;
        // If it exists, load the configuration for the component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve the value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="7ed82-294">如果您使用 `Get` 方法傳回元件的執行個體，您必須確定它會將 `Context` 和 `Dictionary<string, Object>` 參數同時傳遞至建構函式。</span><span class="sxs-lookup"><span data-stu-id="7ed82-294">If you use a `Get` method to return an instance of your component, you must ensure that it passes both the `Context` and `Dictionary<string, Object>` parameters to the constructor.</span></span> <span data-ttu-id="7ed82-295">下列範例是會正確傳遞這些值的基本 `Get` 方法︰</span><span class="sxs-lookup"><span data-stu-id="7ed82-295">The following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-to-update-scpnet"></a><span data-ttu-id="7ed82-296">如何更新 SCP.NET</span><span class="sxs-lookup"><span data-stu-id="7ed82-296">How to update SCP.NET</span></span>

<span data-ttu-id="7ed82-297">最新版 SCP.NET 支援透過 NuGet 進行封裝升級。</span><span class="sxs-lookup"><span data-stu-id="7ed82-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="7ed82-298">當新的更新可用時，您會收到升級通知。</span><span class="sxs-lookup"><span data-stu-id="7ed82-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="7ed82-299">若要手動檢查升級，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7ed82-299">To manually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="7ed82-300">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-300">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="7ed82-301">從封裝管理員，選取 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="7ed82-301">From the package manager, select **Updates**.</span></span> <span data-ttu-id="7ed82-302">如果有可用的更新，它會列出。</span><span class="sxs-lookup"><span data-stu-id="7ed82-302">If an update is available, it is listed.</span></span> <span data-ttu-id="7ed82-303">按一下套件的 [更新] 來安裝它。</span><span class="sxs-lookup"><span data-stu-id="7ed82-303">Click **Update** for the package to install it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ed82-304">如果您的專案是利用未使用 NuGet 的舊版 SCP.NET 建立，您必須執行下列步驟更新為新的版本：</span><span class="sxs-lookup"><span data-stu-id="7ed82-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform the following steps to update to a newer version:</span></span>
>
> 1. <span data-ttu-id="7ed82-305">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-305">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="7ed82-306">使用 [搜尋] 欄位，搜尋 **Microsoft.SCP.Net.SDK** 然後將其加入專案。</span><span class="sxs-lookup"><span data-stu-id="7ed82-306">Using the **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** to the project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="7ed82-307">針對拓撲常見問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="7ed82-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="7ed82-308">Null 指標例外狀況</span><span class="sxs-lookup"><span data-stu-id="7ed82-308">Null pointer exceptions</span></span>

<span data-ttu-id="7ed82-309">當您搭配使用 C# 拓撲與以 Linux 為基礎的 HDInsight 叢集時，在執行階段使用 **ConfigurationManager** 讀取組態設定的 Bolt 與 Spout 元件，可能會傳回 Null 指標例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7ed82-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** to read configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="7ed82-310">專案的設定會以拓撲內容中金鑰和值組的形式傳遞至 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-310">The configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="7ed82-311">可以從初始化時傳遞至您的元件的字典物件中擷取組態。</span><span class="sxs-lookup"><span data-stu-id="7ed82-311">It can be retrieved from the dictionary object that is passed to your components when they are initialized.</span></span>

<span data-ttu-id="7ed82-312">如需詳細資訊，請參閱本文件的 [ConfigurationManager](#configurationmanager) 小節。</span><span class="sxs-lookup"><span data-stu-id="7ed82-312">For more information, see the [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="7ed82-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="7ed82-313">System.TypeLoadException</span></span>

<span data-ttu-id="7ed82-314">當您搭配使用 C# 拓撲與以 Linux 為基礎的 HDInsight 叢集時，可能會遇到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="7ed82-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter the following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="7ed82-315">當您使用的二進位檔與 Mono 支援的 .NET 版本不相容時，會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ed82-315">This error occurs when you use a binary that is not compatible with the version of .NET that Mono supports.</span></span>

<span data-ttu-id="7ed82-316">對於以 Linux 為基礎的 HDInsight 叢集，請確定專案使用針對 .NET 4.5 編譯的二進位檔。</span><span class="sxs-lookup"><span data-stu-id="7ed82-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="7ed82-317">在本機測試拓撲</span><span class="sxs-lookup"><span data-stu-id="7ed82-317">Test a topology locally</span></span>

<span data-ttu-id="7ed82-318">雖然很容易就可以將拓撲部署至叢集，但是在某些情況下，您可能需要在本機測試拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-318">Although it is easy to deploy a topology to a cluster, in some cases, you may need to test a topology locally.</span></span> <span data-ttu-id="7ed82-319">使用下列步驟，在開發環境上以本機執行和測試本教學課程中的範例拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-319">Use the following steps to run and test the example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="7ed82-320">本機測試只適用於僅限 C# 的基本拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="7ed82-321">您不得將本機測試使用於混合式拓撲或使用多個資料流的拓撲。</span><span class="sxs-lookup"><span data-stu-id="7ed82-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="7ed82-322">在**方案總管**中，於專案上按一下滑鼠右鍵，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-322">In **Solution Explorer**, right-click the project, and select **Properties**.</span></span> <span data-ttu-id="7ed82-323">在專案屬性中，將 [輸出類型] 變更為 [主控台應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-323">In the project properties, change the **Output type** to **Console Application**.</span></span>

    ![醒目提示 [輸出] 類型的專案屬性螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="7ed82-325">請記得先將 [輸出類型] 變更回 [類別庫]，再將拓撲部署至叢集。</span><span class="sxs-lookup"><span data-stu-id="7ed82-325">Remember to change the **Output type** back to **Class Library** before you deploy the topology to a cluster.</span></span>

2. <span data-ttu-id="7ed82-326">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取 [新增] > [新項目]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-326">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="7ed82-327">選取 [類別]，並輸入 **LocalTest.cs** 做為類別名稱。</span><span class="sxs-lookup"><span data-stu-id="7ed82-327">Select **Class**, and enter **LocalTest.cs** as the class name.</span></span> <span data-ttu-id="7ed82-328">最後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="7ed82-329">開啟 **LocalTest.cs**，並在頂端加入下列 **using** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="7ed82-329">Open **LocalTest.cs**, and add the following **using** statement at the top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="7ed82-330">使用下列程式碼做為 **LocalTest** 類別的內容：</span><span class="sxs-lookup"><span data-stu-id="7ed82-330">Use the following code as the contents of the **LocalTest** class:</span></span>

    ```csharp
    // Drives the topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test the spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of the spout, using the local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext to persist the data stream to file
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test the splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set the data stream to the data created by the spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test the counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set the data stream to the data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="7ed82-331">請用一些時間閱讀程式碼註解。</span><span class="sxs-lookup"><span data-stu-id="7ed82-331">Take a moment to read through the code comments.</span></span> <span data-ttu-id="7ed82-332">此程式碼會使用 **LocalContext** ，在開發環境中執行元件，並將元件之間的資料流保存至本機磁碟機上的文字檔。</span><span class="sxs-lookup"><span data-stu-id="7ed82-332">This code uses **LocalContext** to run the components in the development environment, and it persists the data stream between components to text files on the local drive.</span></span>

1. <span data-ttu-id="7ed82-333">開啟 **Program.cs**，並將下列程式碼加入 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="7ed82-333">Open **Program.cs**, and add the following to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize the runtime
    SCPRuntime.Initialize();

    //If we are not running under the local context, throw an error
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

2. <span data-ttu-id="7ed82-334">儲存變更，然後按一下 **F5** 或選取 [偵錯] > [開始偵錯] 來啟動專案。</span><span class="sxs-lookup"><span data-stu-id="7ed82-334">Save the changes, and then click **F5** or select **Debug** > **Start Debugging** to start the project.</span></span> <span data-ttu-id="7ed82-335">應該會出現主控台視窗，並記錄測試進行的狀態。</span><span class="sxs-lookup"><span data-stu-id="7ed82-335">A console window should appear, and log status as the tests progress.</span></span> <span data-ttu-id="7ed82-336">出現 [測試已完成]  時，請按任意鍵關閉視窗。</span><span class="sxs-lookup"><span data-stu-id="7ed82-336">When **Tests finished** appears, press any key to close the window.</span></span>

3. <span data-ttu-id="7ed82-337">使用 [Windows 檔案總管] 找出包含您專案的目錄。</span><span class="sxs-lookup"><span data-stu-id="7ed82-337">Use **Windows Explorer** to locate the directory that contains your project.</span></span> <span data-ttu-id="7ed82-338">例如：**C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**。</span><span class="sxs-lookup"><span data-stu-id="7ed82-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="7ed82-339">在此目錄中，開啟 [Bin]，然後按一下 [偵錯]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="7ed82-340">您應該會看到執行測試時所產生的文字檔：sentences.txt、counter.txt 和 splitter.txt。</span><span class="sxs-lookup"><span data-stu-id="7ed82-340">You should see the text files that were produced when the tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="7ed82-341">開啟每個文字檔，並檢查資料。</span><span class="sxs-lookup"><span data-stu-id="7ed82-341">Open each text file and inspect the data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7ed82-342">字串資料會在這些檔案中保存為十進位值的陣列。</span><span class="sxs-lookup"><span data-stu-id="7ed82-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="7ed82-343">例如，**splitter.txt** 檔案中的 \[[97,103,111]] 是 *and* 這個單字。</span><span class="sxs-lookup"><span data-stu-id="7ed82-343">For example, \[[97,103,111]] in the **splitter.txt** file is the word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="7ed82-344">請一定要先將 [專案類型] 設回 [類別庫]，再部署至 Storm on HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="7ed82-344">Be sure to set the **Project type** back to **Class Library** before deploying to a Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="7ed82-345">記錄資訊</span><span class="sxs-lookup"><span data-stu-id="7ed82-345">Log information</span></span>

<span data-ttu-id="7ed82-346">您可以使用 `Context.Logger`，輕鬆地記錄拓撲元件中的資訊。</span><span class="sxs-lookup"><span data-stu-id="7ed82-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="7ed82-347">例如，以下會建立一個參考性記錄項目：</span><span class="sxs-lookup"><span data-stu-id="7ed82-347">For example, the following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="7ed82-348">您可以從 **[Hadoop 服務記錄]** \(位於**伺服器總管中**) 檢視記錄的資訊。</span><span class="sxs-lookup"><span data-stu-id="7ed82-348">Logged information can be viewed from the **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="7ed82-349">展開 Storm on HDInsight 叢集的項目，然後展開 [Hadoop 服務記錄]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-349">Expand the entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="7ed82-350">最後，選取要檢視的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7ed82-350">Finally, select the log file to view.</span></span>

> [!NOTE]
> <span data-ttu-id="7ed82-351">記錄會儲存在您叢集所使用的 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="7ed82-351">The logs are stored in the Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="7ed82-352">若要在 Visual Studio 中檢視記錄檔，您必須登入至擁有儲存體帳戶的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ed82-352">To view the logs in Visual Studio, you must sign in to the Azure subscription that owns the storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="7ed82-353">檢視錯誤資訊</span><span class="sxs-lookup"><span data-stu-id="7ed82-353">View error information</span></span>

<span data-ttu-id="7ed82-354">若要檢視執行中拓撲中所發生的錯誤，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7ed82-354">To view errors that have occurred in a running topology, use the following steps:</span></span>

1. <span data-ttu-id="7ed82-355">從**伺服器總管**中，於 Storm on HDInsight 叢集上按一下滑鼠右鍵，然後選取 [檢視 Storm 拓撲]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-355">From **Server Explorer**, right-click the Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="7ed82-356">針對 **Spout** 和 **Bolt**，[最後一個錯誤] 資料行會含有最後一個錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7ed82-356">For the **Spout** and **Bolts**, the **Last Error** column contains information on the last error.</span></span>

3. <span data-ttu-id="7ed82-357">選取發生錯誤之元件的 [Spout ID] 或 [Bolt ID]。</span><span class="sxs-lookup"><span data-stu-id="7ed82-357">Select the **Spout Id** or **Bolt Id** for the component that has an error listed.</span></span> <span data-ttu-id="7ed82-358">在顯示的詳細資料頁面上，其他錯誤資訊會列在頁面底部的 [錯誤] 區段中。</span><span class="sxs-lookup"><span data-stu-id="7ed82-358">On the details page that is displayed, additional error information is listed in the **Errors** section at the bottom of the page.</span></span>

4. <span data-ttu-id="7ed82-359">若要取得詳細資訊，請從頁面的 [執行程式] 區段中選取 [連接埠]，以查看最後幾分鐘的 Storm 背景工作記錄。</span><span class="sxs-lookup"><span data-stu-id="7ed82-359">To obtain more information, select a **Port** from the **Executors** section of the page, to see the Storm worker log for the last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="7ed82-360">提交拓撲的錯誤</span><span class="sxs-lookup"><span data-stu-id="7ed82-360">Errors submitting topologies</span></span>

<span data-ttu-id="7ed82-361">如果將拓撲提交到 HDInsight 時發生錯誤，您可以尋找在 HDInsight 叢集上處理拓撲提交之伺服器端元件的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7ed82-361">If you encounter errors submitting a topology to HDInsight, you can find logs for the server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="7ed82-362">若要擷取這些記錄檔，請在命令列使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="7ed82-362">To retrieve these logs, use the following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="7ed82-363">以叢集的 SSH 使用者帳戶取代 __sshuser__。</span><span class="sxs-lookup"><span data-stu-id="7ed82-363">Replace __sshuser__ with the SSH user account for the cluster.</span></span> <span data-ttu-id="7ed82-364">以 HDInsight 叢集的名稱取代 __clustername__。</span><span class="sxs-lookup"><span data-stu-id="7ed82-364">Replace __clustername__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="7ed82-365">如需搭配 HDInsight 使用 `scp` 和 `ssh` 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="7ed82-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="7ed82-366">提交失敗有多種原因：</span><span class="sxs-lookup"><span data-stu-id="7ed82-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="7ed82-367">JDK 未安裝或並未在路徑中。</span><span class="sxs-lookup"><span data-stu-id="7ed82-367">JDK is not installed or is not in the path.</span></span>
* <span data-ttu-id="7ed82-368">提交並未包括必要的 Java 相依性。</span><span class="sxs-lookup"><span data-stu-id="7ed82-368">Required Java dependencies are not included in the submission.</span></span>
* <span data-ttu-id="7ed82-369">不相容的相依性。</span><span class="sxs-lookup"><span data-stu-id="7ed82-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="7ed82-370">重複的拓撲名稱。</span><span class="sxs-lookup"><span data-stu-id="7ed82-370">Duplicate topology names.</span></span>

<span data-ttu-id="7ed82-371">如果 `hdinsight-scpwebapi.out` 記錄包含 `FileNotFoundException`，則可能是因為下列狀況造成：</span><span class="sxs-lookup"><span data-stu-id="7ed82-371">If the `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by the following conditions:</span></span>

* <span data-ttu-id="7ed82-372">JDK 沒有在開發環境的路徑中。</span><span class="sxs-lookup"><span data-stu-id="7ed82-372">The JDK is not in the path on the development environment.</span></span> <span data-ttu-id="7ed82-373">確認已在開發環境中安裝 JDK，且 `%JAVA_HOME%/bin` 在路徑中。</span><span class="sxs-lookup"><span data-stu-id="7ed82-373">Verify that the JDK is installed in the development environment, and that `%JAVA_HOME%/bin` is in the path.</span></span>
* <span data-ttu-id="7ed82-374">遺漏 Java 相依性。</span><span class="sxs-lookup"><span data-stu-id="7ed82-374">You are missing a Java dependency.</span></span> <span data-ttu-id="7ed82-375">確定您在提交內容中包含任何必要的 .jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="7ed82-375">Make sure you are including any required .jar files as part of the submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ed82-376">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ed82-376">Next steps</span></span>

<span data-ttu-id="7ed82-377">如需從事件中樞處理資料的範例，請參閱[利用 Storm on HDInsight 處理 Azure 事件中樞的事件](hdinsight-storm-develop-csharp-event-hub-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="7ed82-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="7ed82-378">如需將資料流的資料分成多個資料流的 C# 拓撲範例，請參閱 [C# Storm 範例](https://github.com/Blackmist/csharp-storm-example)。</span><span class="sxs-lookup"><span data-stu-id="7ed82-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="7ed82-379">若要探索建立 C# 拓撲的詳細資訊，請參閱 [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7ed82-379">To discover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="7ed82-380">如需更多使用 HDInsight 的方式，或更多 Storm on HDInsight 範例，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="7ed82-380">For more ways to work with HDInsight and more Storm on HDInsight samples, see the following documents:</span></span>

<span data-ttu-id="7ed82-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="7ed82-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="7ed82-382">SCP 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="7ed82-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="7ed82-383">**Apache Storm on HDInsight**</span><span class="sxs-lookup"><span data-stu-id="7ed82-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="7ed82-384">使用 Apache Storm on HDInsight 部署和監視拓撲</span><span class="sxs-lookup"><span data-stu-id="7ed82-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="7ed82-385">Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="7ed82-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="7ed82-386">**Apache Hadoop on HDInsight**</span><span class="sxs-lookup"><span data-stu-id="7ed82-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="7ed82-387">搭配 HDInsight 上的 Hadoop 使用 Hive</span><span class="sxs-lookup"><span data-stu-id="7ed82-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7ed82-388">搭配 HDInsight 上的 Hadoop 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="7ed82-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7ed82-389">搭配 HDInsight 上的 Hadoop 使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="7ed82-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="7ed82-390">**Apache HBase on HDInsight**</span><span class="sxs-lookup"><span data-stu-id="7ed82-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="7ed82-391">開始使用 HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ed82-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)

---
title: "在以 Linux 為基礎的 HDInsight - Azure 上搭配 Hadoop MapReduce 使用 .NET | Microsoft Docs"
description: "了解如何在以 Linux 為基礎的 HDInsight 上使用 .NET 應用程式串流處理 MapReduce。"
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 6ad188fb752474ff5c7d8a3fb9d609eefe8c7a9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-to-linux-based-hdinsight"></a><span data-ttu-id="fa848-103">將以 Windows 為基礎的 HDInsight 適用的 .NET 方案移轉至以 Linux 為基礎的 HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa848-103">Migrate .NET solutions for Windows-based HDInsight to Linux-based HDInsight</span></span>

<span data-ttu-id="fa848-104">以 Linux 為基礎的 HDInsight 叢集使用 [Mono (https://mono-project.com)](https://mono-project.com) 來執行 .NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa848-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="fa848-105">Mono 可讓您搭配以 Linux 為基礎的 HDInsight 使用 .NET 元件 (例如 MapReduce 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="fa848-105">Mono allows you to use .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="fa848-106">在本文件中，了解如何移轉為以 Windows 為基礎的 HDInsight 建立的 .NET 方案，以在以 Linux 為基礎的 HDInsight 上搭配 Mono 使用。</span><span class="sxs-lookup"><span data-stu-id="fa848-106">In this document, learn how to migrate .NET solutions created for Windows-based HDInsight clusters to work with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="fa848-107">Mono 與 .NET 的相容性</span><span class="sxs-lookup"><span data-stu-id="fa848-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="fa848-108">4.2.1 版的 Mono 隨附於 3.5 版的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="fa848-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="fa848-109">如需 HDInsight 包含之 Mono 版本的詳細資訊，請參閱 [HDInsight 元件版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="fa848-109">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="fa848-110">若要安裝特定版本的 Mono，請參閱[安裝或更新 Mono](hdinsight-hadoop-install-mono.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="fa848-110">To install a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="fa848-111">如需 Mono 與 .NET 之間的相容性詳細資訊，請參閱 [Mono 相容性 (英文) (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) 文件。</span><span class="sxs-lookup"><span data-stu-id="fa848-111">For detailed information on compatibility between Mono and .NET, see the [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa848-112">SCP.NET 架構與 Mono 相容。</span><span class="sxs-lookup"><span data-stu-id="fa848-112">The SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="fa848-113">如需搭配 Mono 使用 SCP.NET 的詳細資訊，請參閱[使用 Visual Studio 開發適用於 Apache Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="fa848-113">For more information on using SCP.NET with Mono, see [Use Visual Studio to develop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="fa848-114">自動化的可攜性分析</span><span class="sxs-lookup"><span data-stu-id="fa848-114">Automated portability analysis</span></span>

<span data-ttu-id="fa848-115">[.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) 可用來產生一份您的應用程式和 Mono 之間的不相容性報告。</span><span class="sxs-lookup"><span data-stu-id="fa848-115">The [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used to generate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="fa848-116">使用下列步驟設定分析器，以檢查您的應用程式是否具備 Mono 可攜性︰</span><span class="sxs-lookup"><span data-stu-id="fa848-116">Use the following steps to configure the analyzer to check your application for Mono portability:</span></span>

1. <span data-ttu-id="fa848-117">安裝 [.NET Portability Analyzer (英文)](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)。</span><span class="sxs-lookup"><span data-stu-id="fa848-117">Install the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="fa848-118">在安裝期間，選取要使用的 Visual Studio 版本。</span><span class="sxs-lookup"><span data-stu-id="fa848-118">During installation, select the version of Visual Studio to use.</span></span>

2. <span data-ttu-id="fa848-119">從 Visual Studio 2015，選取 [分析] >  [Portability Analyzer 設定]，並確定已選取 [Mono] 區段中的 __4.5__。</span><span class="sxs-lookup"><span data-stu-id="fa848-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in the __Mono__ section.</span></span>

    ![分析器設定的 [Mono] 區段中已選取 4.5](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="fa848-121">選取 [確定] 以儲存組態。</span><span class="sxs-lookup"><span data-stu-id="fa848-121">Select __OK__ to save the configuration.</span></span>

3. <span data-ttu-id="fa848-122">選取 [分析] > [分析組件可攜性]。</span><span class="sxs-lookup"><span data-stu-id="fa848-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="fa848-123">選取包含您的方案的組件，然後選取 [開啟] 以開始分析。</span><span class="sxs-lookup"><span data-stu-id="fa848-123">Select the assembly that contains your solution, and then select __Open__ to begin analysis.</span></span>

4. <span data-ttu-id="fa848-124">分析完成之後，請選取 [分析] > [檢視分析報告]。</span><span class="sxs-lookup"><span data-stu-id="fa848-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="fa848-125">在 [可攜性分析結果] 中，選取 [開啟報告] 以開啟報告。</span><span class="sxs-lookup"><span data-stu-id="fa848-125">In __Portability Analysis Results__, select __Open report__ to open a report.</span></span>

    ![Portability Analyzer 結果對話方塊](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="fa848-127">分析器無法找出您方案的每個問題。</span><span class="sxs-lookup"><span data-stu-id="fa848-127">The analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="fa848-128">例如，檔案路徑 `c:\temp\file.txt` 會視為有效，因為 Mono 可在 Windows 上執行，因此該路徑在該內容中有效。</span><span class="sxs-lookup"><span data-stu-id="fa848-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and the path is valid in that context.</span></span> <span data-ttu-id="fa848-129">不過，此路徑在 Linux 平台上無效。</span><span class="sxs-lookup"><span data-stu-id="fa848-129">However, the path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="fa848-130">手動的可攜性分析</span><span class="sxs-lookup"><span data-stu-id="fa848-130">Manual portability analysis</span></span>

<span data-ttu-id="fa848-131">使用[應用程式可攜性 (英文) (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) 文件中的資訊，執行程式碼的手動稽核。</span><span class="sxs-lookup"><span data-stu-id="fa848-131">Perform a manual audit of your code using the information in the [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="fa848-132">修改和建置</span><span class="sxs-lookup"><span data-stu-id="fa848-132">Modify and build</span></span>

<span data-ttu-id="fa848-133">您可以繼續使用 Visual Studio 建置適用於 HDInsight 的 .NET 方案。</span><span class="sxs-lookup"><span data-stu-id="fa848-133">You can continue to use Visual Studio to build your .NET solutions for HDInsight.</span></span> <span data-ttu-id="fa848-134">不過，您必須確定專案已設定為使用 .NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="fa848-134">However, you must ensure that the project is configured to use .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="fa848-135">部署和測試</span><span class="sxs-lookup"><span data-stu-id="fa848-135">Deploy and test</span></span>

<span data-ttu-id="fa848-136">使用 .NET Portability Analyzer 或手動分析的建議修改您的方案後，您必須使用 HDInsight 進行測試。</span><span class="sxs-lookup"><span data-stu-id="fa848-136">Once you have modified your solution using the recommendations from the .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="fa848-137">在以 Linux 為基礎的 HDInsight 叢集上測試方案，可能會揭露需要更正的細微問題。</span><span class="sxs-lookup"><span data-stu-id="fa848-137">Testing the solution on a Linux-based HDInsight cluster may reveal subtle problems that need to be corrected.</span></span> <span data-ttu-id="fa848-138">建議您在測試時啟用應用程式中的其他記錄。</span><span class="sxs-lookup"><span data-stu-id="fa848-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="fa848-139">如需存取記錄的詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="fa848-139">For more information on accessing logs, see the following documents:</span></span>

* [<span data-ttu-id="fa848-140">存取以 Linux 為基礎之 HDInsight 上的 YARN 應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="fa848-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="fa848-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa848-141">Next steps</span></span>

* [<span data-ttu-id="fa848-142">在 HDInsight 上搭配 MapReduce 使用 C#</span><span class="sxs-lookup"><span data-stu-id="fa848-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="fa848-143">搭配 Hive 和 Pig 使用 C# 使用者定義函數</span><span class="sxs-lookup"><span data-stu-id="fa848-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="fa848-144">開發適用於 Storm on HDInsight 的 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="fa848-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
---
title: "aaaUse 與 Hadoop MapReduce 以 Linux 為基礎的 HDInsight 的 Azure 上的.NET |Microsoft 文件"
description: "深入了解如何 toouse 串流 MapReduce 以 Linux 為基礎的 HDInsight 上的.NET 應用程式。"
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
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a><span data-ttu-id="d1cdc-103">移轉 Windows 為基礎的 hdinsight.NET 方案 tooLinux 為基礎的 HDInsight</span><span class="sxs-lookup"><span data-stu-id="d1cdc-103">Migrate .NET solutions for Windows-based HDInsight tooLinux-based HDInsight</span></span>

<span data-ttu-id="d1cdc-104">以 Linux 為基礎的 HDInsight 叢集使用[單聲道 (https://mono-project.com)](https://mono-project.com) toorun.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="d1cdc-105">單聲道可讓您 toouse.NET 元件，例如與 linux 的 HDInsight MapReduce 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-105">Mono allows you toouse .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="d1cdc-106">在這份文件，了解 toomigrate.NET 方案建立 Windows 為基礎的 HDInsight 叢集 toowork Mono 以 Linux 為基礎的 HDInsight 上使用的方式。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-106">In this document, learn how toomigrate .NET solutions created for Windows-based HDInsight clusters toowork with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="d1cdc-107">Mono 與 .NET 的相容性</span><span class="sxs-lookup"><span data-stu-id="d1cdc-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="d1cdc-108">4.2.1 版的 Mono 隨附於 3.5 版的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="d1cdc-109">多個 hello Mono 隨附 HDInsight 版本的詳細資訊，請參閱[HDInsight 元件版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-109">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="d1cdc-110">tooinstall 特定版本的 Mono，請參閱 hello[安裝或更新 Mono](hdinsight-hadoop-install-mono.md)文件。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-110">tooinstall a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="d1cdc-111">如需 Mono 和.NET 之間的相容性的詳細資訊，請參閱 hello[單聲道相容性 (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/)文件。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-111">For detailed information on compatibility between Mono and .NET, see hello [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1cdc-112">與單聲道相容 hello SCP.NET framework。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-112">hello SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="d1cdc-113">多個使用 Mono SCP.NET 的詳細資訊，請參閱[Apache Storm HDInsight 上使用 Visual Studio toodevelop C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-113">For more information on using SCP.NET with Mono, see [Use Visual Studio toodevelop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="d1cdc-114">自動化的可攜性分析</span><span class="sxs-lookup"><span data-stu-id="d1cdc-114">Automated portability analysis</span></span>

<span data-ttu-id="d1cdc-115">hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)可以是使用的 toogenerate 應用程式和單聲道之間的不相容的報表。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-115">hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used toogenerate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="d1cdc-116">使用您的應用程式遵循步驟 tooconfigure hello 分析器 toocheck hello 單聲道的可攜性：</span><span class="sxs-lookup"><span data-stu-id="d1cdc-116">Use hello following steps tooconfigure hello analyzer toocheck your application for Mono portability:</span></span>

1. <span data-ttu-id="d1cdc-117">安裝 hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-117">Install hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="d1cdc-118">在安裝期間，選取 Visual Studio toouse hello 版本。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-118">During installation, select hello version of Visual Studio toouse.</span></span>

2. <span data-ttu-id="d1cdc-119">從 Visual Studio 2015 中，選取__分析__ > __可攜性分析器設定__，並確定__4.5__簽入 hello__單聲道__ > 一節。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in hello __Mono__ section.</span></span>

    ![單聲道 hello 分析器設定區段中的 4.5 檢查](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="d1cdc-121">選取__確定__toosave hello 組態。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-121">Select __OK__ toosave hello configuration.</span></span>

3. <span data-ttu-id="d1cdc-122">選取 [分析] > [分析組件可攜性]。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="d1cdc-123">選取包含您的方案，hello 組件，然後選取__開啟__toobegin 分析。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-123">Select hello assembly that contains your solution, and then select __Open__ toobegin analysis.</span></span>

4. <span data-ttu-id="d1cdc-124">分析完成之後，請選取 [分析] > [檢視分析報告]。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="d1cdc-125">在__可攜性分析結果__，選取__開啟報表__tooopen 報表。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-125">In __Portability Analysis Results__, select __Open report__ tooopen a report.</span></span>

    ![Portability Analyzer 結果對話方塊](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="d1cdc-127">hello 分析器無法攔截與您的方案的每個問題。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-127">hello analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="d1cdc-128">例如，檔案的檔案路徑`c:\temp\file.txt`Mono 執行於 Windows 上及在該內容中的 hello 路徑無效，因此視為 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and hello path is valid in that context.</span></span> <span data-ttu-id="d1cdc-129">不過，hello 路徑不是有效的 Linux 平台上。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-129">However, hello path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="d1cdc-130">手動的可攜性分析</span><span class="sxs-lookup"><span data-stu-id="d1cdc-130">Manual portability analysis</span></span>

<span data-ttu-id="d1cdc-131">執行您的程式碼使用 hello hello 資訊手動稽核[應用程式可攜性 (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/)文件。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-131">Perform a manual audit of your code using hello information in hello [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="d1cdc-132">修改和建置</span><span class="sxs-lookup"><span data-stu-id="d1cdc-132">Modify and build</span></span>

<span data-ttu-id="d1cdc-133">您可以針對 HDInsight 繼續 toouse Visual Studio toobuild.NET 方案。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-133">You can continue toouse Visual Studio toobuild your .NET solutions for HDInsight.</span></span> <span data-ttu-id="d1cdc-134">不過，您必須確定該 hello 專案設定的 toouse.NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-134">However, you must ensure that hello project is configured toouse .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="d1cdc-135">部署和測試</span><span class="sxs-lookup"><span data-stu-id="d1cdc-135">Deploy and test</span></span>

<span data-ttu-id="d1cdc-136">一旦您修改您的方案使用 hello 建議從 hello.NET Portability Analyzer 或手動分析，您必須與 HDInsight 來進行測試。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-136">Once you have modified your solution using hello recommendations from hello .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="d1cdc-137">測試以 Linux 為基礎的 HDInsight 叢集上的 hello 解決方案，可能會顯示需要更正 toobe 的細部問題。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-137">Testing hello solution on a Linux-based HDInsight cluster may reveal subtle problems that need toobe corrected.</span></span> <span data-ttu-id="d1cdc-138">建議您在測試時啟用應用程式中的其他記錄。</span><span class="sxs-lookup"><span data-stu-id="d1cdc-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="d1cdc-139">如需有關存取記錄檔的詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="d1cdc-139">For more information on accessing logs, see hello following documents:</span></span>

* [<span data-ttu-id="d1cdc-140">存取以 Linux 為基礎之 HDInsight 上的 YARN 應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="d1cdc-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="d1cdc-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1cdc-141">Next steps</span></span>

* [<span data-ttu-id="d1cdc-142">在 HDInsight 上搭配 MapReduce 使用 C#</span><span class="sxs-lookup"><span data-stu-id="d1cdc-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="d1cdc-143">搭配 Hive 和 Pig 使用 C# 使用者定義函數</span><span class="sxs-lookup"><span data-stu-id="d1cdc-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="d1cdc-144">開發適用於 Storm on HDInsight 的 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="d1cdc-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
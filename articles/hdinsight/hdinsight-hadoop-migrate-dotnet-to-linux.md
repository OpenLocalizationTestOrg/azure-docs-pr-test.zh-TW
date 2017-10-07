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
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a>移轉 Windows 為基礎的 hdinsight.NET 方案 tooLinux 為基礎的 HDInsight

以 Linux 為基礎的 HDInsight 叢集使用[單聲道 (https://mono-project.com)](https://mono-project.com) toorun.NET 應用程式。 單聲道可讓您 toouse.NET 元件，例如與 linux 的 HDInsight MapReduce 應用程式。 在這份文件，了解 toomigrate.NET 方案建立 Windows 為基礎的 HDInsight 叢集 toowork Mono 以 Linux 為基礎的 HDInsight 上使用的方式。

## <a name="mono-compatibility-with-net"></a>Mono 與 .NET 的相容性

4.2.1 版的 Mono 隨附於 3.5 版的 HDInsight。 多個 hello Mono 隨附 HDInsight 版本的詳細資訊，請參閱[HDInsight 元件版本](hdinsight-component-versioning.md)。 tooinstall 特定版本的 Mono，請參閱 hello[安裝或更新 Mono](hdinsight-hadoop-install-mono.md)文件。

如需 Mono 和.NET 之間的相容性的詳細資訊，請參閱 hello[單聲道相容性 (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/)文件。

> [!IMPORTANT]
> 與單聲道相容 hello SCP.NET framework。 多個使用 Mono SCP.NET 的詳細資訊，請參閱[Apache Storm HDInsight 上使用 Visual Studio toodevelop C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。

## <a name="automated-portability-analysis"></a>自動化的可攜性分析

hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)可以是使用的 toogenerate 應用程式和單聲道之間的不相容的報表。 使用您的應用程式遵循步驟 tooconfigure hello 分析器 toocheck hello 單聲道的可攜性：

1. 安裝 hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)。 在安裝期間，選取 Visual Studio toouse hello 版本。

2. 從 Visual Studio 2015 中，選取__分析__ > __可攜性分析器設定__，並確定__4.5__簽入 hello__單聲道__ > 一節。

    ![單聲道 hello 分析器設定區段中的 4.5 檢查](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    選取__確定__toosave hello 組態。

3. 選取 [分析] > [分析組件可攜性]。 選取包含您的方案，hello 組件，然後選取__開啟__toobegin 分析。

4. 分析完成之後，請選取 [分析] > [檢視分析報告]。 在__可攜性分析結果__，選取__開啟報表__tooopen 報表。

    ![Portability Analyzer 結果對話方塊](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> hello 分析器無法攔截與您的方案的每個問題。 例如，檔案的檔案路徑`c:\temp\file.txt`Mono 執行於 Windows 上及在該內容中的 hello 路徑無效，因此視為 [確定]。 不過，hello 路徑不是有效的 Linux 平台上。

## <a name="manual-portability-analysis"></a>手動的可攜性分析

執行您的程式碼使用 hello hello 資訊手動稽核[應用程式可攜性 (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/)文件。

## <a name="modify-and-build"></a>修改和建置

您可以針對 HDInsight 繼續 toouse Visual Studio toobuild.NET 方案。 不過，您必須確定該 hello 專案設定的 toouse.NET Framework 4.5。

## <a name="deploy-and-test"></a>部署和測試

一旦您修改您的方案使用 hello 建議從 hello.NET Portability Analyzer 或手動分析，您必須與 HDInsight 來進行測試。 測試以 Linux 為基礎的 HDInsight 叢集上的 hello 解決方案，可能會顯示需要更正 toobe 的細部問題。 建議您在測試時啟用應用程式中的其他記錄。

如需有關存取記錄檔的詳細資訊，請參閱下列文件的 hello:

* [存取以 Linux 為基礎之 HDInsight 上的 YARN 應用程式記錄](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a>後續步驟

* [在 HDInsight 上搭配 MapReduce 使用 C#](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [搭配 Hive 和 Pig 使用 C# 使用者定義函數](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [開發適用於 Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)
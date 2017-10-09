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
# <a name="work-in-hello-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a>在 hello HDInsight 的 Windows pc 的 Hadoop 生態系統

深入了解開發和管理 hello Windows 電腦上的選項，在 HDInsight 上的 hello Hadoop 生態系統中使用。 

HDInsight 是以 Apache Hadoop 和 Hadoop 元件為基礎，採用在 Linux 上開發的開放原始碼技術。 HDInsight 版本 3.4 及更新版本為 hello 基礎 OS hello 叢集使用 hello Ubuntu Linux 散發套件。 不過，您可以從 Windows 用戶端或 Windows 開發環境使用 HDInsight。

## <a name="use-powershell-for-deployment-and-management-tasks"></a>使用 PowerShell 進行部署和管理工作
Azure PowerShell 是指令碼環境，您可以使用 toocontrol，並從 Windows 的 HDInsight 中的部署和管理工作自動化。

您可以使用 PowerShell 執行的工作範例︰

* [使用 PowerShell 建立叢集](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [使用 PowerShell 執行 Hive 查詢](hdinsight-hadoop-use-hive-powershell.md)
* [使用 PowerShell 管理叢集](hdinsight-administer-use-powershell.md)

請依照下列步驟太[安裝和設定 Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooget hello 最新版本。 如果您有 Azure 資源管理員的需要修改 toobe toouse hello 新 cmdlet 的指令碼，請參閱[移轉 tooAzure HDInsight 叢集的資源管理員為基礎的開發工具](hdinsight-hadoop-development-using-azure-resource-manager.md)。

## <a name="utilities-you-can-run-in-a-browser"></a>您可以在瀏覽器中執行的公用程式
hello 下列公用程式有 web 瀏覽器中執行的 UI:
* **[Azure 雲端殼層 （預覽）](https://docs.microsoft.com/azure/cloud-shell/quickstart)** 是在您的瀏覽器中執行互動式的命令列殼層和從 hello Azure 入口網站。
* **[Ambari Web UI](hdinsight-hadoop-manage-ambari.md)** 是管理與監視公用程式，可在 hello Azure 入口網站，可以是使用的 toomanage 不同種類的工作，例如：
    * [使用 Ambari 以 hello REST API](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [Ambari 中的 Hive 檢視](hdinsight-hadoop-use-hive-ambari-view.md)
    * [Ambari 中的 Tez 檢視](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a>Data Lake (Hadoop) Tools for Visual Studio
使用 Data Lake Tools for Visual Studio toodeploy 及管理 Storm 拓撲。 資料湖工具也會安裝 hello SCP.NET SDK，可讓您使用 Visual Studio toodevelop C# Storm 拓撲。

繼續遵循範例，toohello 之前[安裝，然後嘗試 Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。 

您可以使用 Visual Studio 和 Data Lake Tools for Visual Studio 執行的工作範例︰
* [從 Visual Studio 部署和管理 Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)
* [使用 Visual Studio 開發 Storm 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。 hello 位元包含範例範本 Storm 拓撲中，您可以連接 toodatabases，例如 Azure Cosmos DB 和 SQL Database。

## <a name="visual-studio-and-hello-net-sdk"></a>Visual Studio 和 hello.NET SDK 

您可以使用 Visual Studio 與 hello.NET SDK toomanage 叢集，並開發巨量資料的應用程式。 您可以使用其他 Ide hello 下列工作，但在 Visual Studio 中顯示的範例。

您可以使用 Visual Studio 中的.NET SDK hello 執行的工作的範例包括：
* [從 .NET Framework 應用程式在 HDInsight 中建立和使用叢集](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [執行 Hive 查詢使用 hello.NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [使用 C# 使用者定義的函式搭配 Hadoop 上的 Hive 和 Pig 串流](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> 提示您執行.NET 方案與 Windows 為基礎的 HDInsight 叢集，它是否適合 tooplan 移轉 tooLinux 為基礎的叢集。 如需詳細資訊，請參閱[Windows 為基礎的 HDInsight 的移轉.NET 方案 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)。

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a>適用於 Spark 叢集的 Intellij IDEA 和 Eclipse IDE
同時[Intellij 概念](https://www.jetbrains.com/idea/download)和 hello [Eclipse IDE](https://www.eclipse.org/downloads/)可以用來：
* 在 HDInsight Spark 叢集上開發並提交 Scala Spark 應用程式。
* 存取 Spark 叢集資源。
* 在本機開發並執行 Scala Spark 應用程式。

這些文章顯示如何︰ 
* Intellij 概念：[建立 Spark 使用 hello Azure Toolkit for Intellij 外掛程式和 hello Scala SDK 的應用程式。](hdinsight-apache-spark-intellij-tool-plugin.md)
* Eclipse IDE 或 Scala Eclipse IDE:[建立 Spark 應用程式和 hello Azure Toolkit for Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) 


## <a name="notebooks-on-spark-for-data-scientists"></a>適用於資料科學家的 Spark Notebook 
HDInsight 中的 Apache Spark 叢集包含可搭配 Jupyter Notebook 使用的 Zeppelin Notebook 和核心。 

* [了解如何 toouse 核心上的 Spark 叢集與 Jupyter 筆記本 tootest Spark 應用程式](hdinsight-apache-spark-zeppelin-notebook.md)
* [了解如何 toouse 運貨用飛艇筆記型電腦上的 Spark 叢集 toorun Spark 工作](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a>在 Windows 上執行以 Linux 為基礎的工具和技術

如果您遇到的情況下，您必須使用工具或只適用於 Linux 的技術，請考慮下列選項的 hello:

* **Windows 10 上的 Bash (Beta 版)** 在 Windows 上提供 Linux 子系統。 Bash 可讓您執行 Linux 公用程式，而不需要專用的 Linux 安裝 toomaintain toodirectly。 [安裝並執行 Windows 10 上的 hello Bash beta](https://msdn.microsoft.com/commandline/wsl/install_guide)
* **Docker for Windows** toomany Linux 為基礎的工具，提供存取，並可以直接從 Windows 上執行。 例如，您可以使用 Docker toorun hello Beeline 用戶端用於直接從 Windows 登錄區。 您可以也使用 Docker toorun 本機 Jupyter 筆記本，並從遠端連接 tooSpark HDInsight 上。 [開始使用 Docker for Windows](https://docs.docker.com/docker-for-windows/)
* **[MobaXTerm](http://mobaxterm.mobatek.net/)** 可讓您透過 SSH 連線的 toographically 瀏覽 hello 叢集檔案系統。

## <a name="next-steps"></a>後續步驟
如果您是新 tooworking 以 Linux 為基礎的叢集，請參閱 hello，請依照下列文章：
* [設定 Hadoop、Kafka、Spark 或其他叢集](hdinsight-hadoop-provision-linux-clusters.md)
* [Linux 上的 HDInsight 叢集祕訣](hdinsight-hadoop-linux-information.md)
---
title: "aaaRun Apache Pig 工作 Hadoop-Azure HDInsight.NET sdk |Microsoft 文件"
description: "了解如何 toouse hello.NET SDK 上 HDInsight Hadoop toosubmit Pig 工作 tooHadoop。"
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 1d4ceebd7c168372d23fe29a088f04676686de30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a>執行 hello.NET SDK 用於 HDInsight 中的 Hadoop Pig 工作

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

了解 toouse hello.NET SDK 的 Hadoop toosubmit Apache Pig 工作 tooHadoop Azure HDInsight 上的方式。

hello HDInsight.NET SDK 提供可讓您更輕鬆 toowork 與 HDInsight 叢集與.NET 的.NET 用戶端程式庫。 Pig 可讓您 toocreate MapReduce 作業依照模型化一系列的資料轉換。 在本文件中，您學會如何 toouse 基本 C# 應用程式 toosubmit Pig 工作 tooan HDInsight 叢集。

## <a name="prerequisites"></a>必要條件

toocomplete hello 本文中的步驟，您需要下列 hello。

* Azure HDInsight (HDInsight 上的 Hadoop) 叢集 (Windows 或 Linux 型)。

  > [!IMPORTANT]
  > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* Visual Studio 2012、2013、2015 或 2017。

## <a name="create-hello-application"></a>建立 hello 應用程式

hello HDInsight.NET SDK 提供.NET 用戶端程式庫，使其更容易 toowork 與.net 的 HDInsight 叢集。

1. 從 hello**檔案**在 Visual Studio 中，選取功能表**新增**，然後選取 **專案**。

2. Hello 新專案中，類型或選取 hello 下列值：

   | 屬性 | 值 |
   | ------ | ------ |
   | 類別 | 範本/Visual C#/Windows |
   | 範本 | 主控台應用程式 |
   | 名稱 | SubmitPigJob |

3. 按一下**確定**toocreate hello 專案。

4. 從 hello**工具**功能表上，選取**程式庫套件管理員**或**Nuget 套件管理員**，然後選取**Package Manager Console**。

5. tooinstall hello.NET SDK 封裝，請使用下列命令的 hello:

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. 從 方案總管 中，按兩下  **Program.cs** tooopen 它。 取代 hello 下列 hello 現有程式碼。

    ```csharp
    using Microsoft.Azure.Management.HDInsight.Job;
    using Microsoft.Azure.Management.HDInsight.Job.Models;
    using Hyak.Common;

    namespace SubmitHDInsightJobDotNet
    {
        class Program
        {
            private static HDInsightJobManagementClient _hdiJobManagementClient;

            private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
            private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
            private const string ExistingClusterUsername = "<Cluster Username>";
            private const string ExistingClusterPassword = "<Cluster User Password>";

            static void Main(string[] args)
            {
                System.Console.WriteLine("hello application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER toocontinue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting hello Pig job toohello cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that hello response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating hello response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. toostart hello 應用程式，請按**F5**。

8. tooexit hello 應用程式，請按**ENTER**。

## <a name="summary"></a>摘要

如您所見，hello Hadoop 的.NET SDK 可讓您 toocreate.NET 應用程式，提交 Pig 工作 tooan HDInsight 叢集，並監控 hello 工作狀態。

## <a name="next-steps"></a>後續步驟

如需 HDInsight 中 Pig 的詳細資訊，請參閱[搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)。

如需有關使用 HDInsight Hadoop 的詳細資訊，請參閱下列文件的 hello:

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/

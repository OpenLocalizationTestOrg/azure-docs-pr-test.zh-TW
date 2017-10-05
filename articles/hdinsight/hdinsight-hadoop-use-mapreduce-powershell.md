---
title: "搭配使用 MapReduce 和 PowerShell 與 Hadoop - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 PowerShell 從遠端搭配執行 MapReduce 工作與 HDInsight 上的 Hadoop。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: c3801573808709f29cb1e563ac803f225a28cafc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a>使用 PowerShell 搭配執行 MapReduce 工作與 HDInsight 上的 Hadoop

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

本文件提供使用 Azure PowerShell 在 HDInsight 叢集的 Hadoop 中執行 MapReduce 工作的範例。

## <a id="prereq"></a>必要條件

* **Azure HDInsight (HDInsight 上的 Hadoop) 叢集**

  > [!IMPORTANT]
  > Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* **具有 Azure PowerShell 的工作站**。

## <a id="powershell"></a>使用 Azure PowerShell 執行 MapReduce 工作

Azure PowerShell 提供 *Cmdlet* ，可讓您從遠端在 HDInsight 上執行 MapReduce 工作。 在內部，您可以使用在 HDInsight 叢集上執行的 [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (先前稱為 Templeton) 的 REST 呼叫來達到此目的。

在遠端 HDInsight 叢集中執行 MapReduce 工作時，會使用下列 Cmdlet。

* **Login-AzureRmAccount**：向您的 Azure 訂用帳戶驗證 Azure PowerShell。

* **New-AzureRmHDInsightMapReduceJobDefinition**：使用指定的 MapReduce 資訊建立新的「工作定義」。

* **Start-AzureRmHDInsightJob**：將工作定義傳送至 HDInsight、啟動工作，然後傳回可用來檢查工作狀態的「工作」物件。

* **Wait-AzureRmHDInsightJob**：使用工作物件來檢查工作的狀態。 它會等到工作完成，或等到等候時間超過。

* **Get-AzureRmHDInsightJobOutput**：用來擷取工作的輸出。

下列步驟示範如何使用這些 Cmdlet，在您的 HDInsight 叢集中執行工作。

1. 使用編輯器，將下列程式碼儲存為 **mapreducejob.ps1**。

    [!code-powershell[主要](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. 開啟新的 **Azure PowerShell** 命令提示字元。 將目錄變更至 **mapreducejob.ps1** 檔案的位置，然後使用下列命令來執行指令碼：

        .\mapreducejob.ps1

    當您執行指令碼時，系統會提示您的 HDInsight 叢集名稱和 HTTPS/管理帳戶名稱以及叢集的密碼。 系統可能也會提示您驗證 Azure 訂用帳戶。

3. 在作業完成時，您會收到類似下列文字的輸出：

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    此輸出表示工作已順利完成。

    > [!NOTE]
    > 如果 **ExitCode** 的值不是 0，請參閱 [疑難排解](#troubleshooting)。

    此範例也會將下載的檔案儲存到您執行指令碼所在目錄中的 **output.txt** 檔案。

### <a name="view-output"></a>檢視輸出

使用文字編輯器開啟 **output.txt** 檔案，以查看作業所產生的單字和計數。

> [!NOTE]
> MapReduce 工作的輸出檔是固定不變的。 因此，如果您重新執行此範例，則需要變更輸出檔的名稱。

## <a id="troubleshooting"></a>疑難排解

如果在工作完成時未傳回任何資訊，則可能是處理期間發生錯誤。 若要檢視這項工作的錯誤資訊，請將下列命令新增至 **mapreducejob.ps1** 檔案的結尾，並儲存它，然後重新予以執行。

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

這個 Cmdlet 會傳回執行作業時寫入至伺服器上之 STDERR 的資訊，而且可能有助於判斷作業的失敗原因。

## <a id="summary"></a>摘要

如您所見，Azure PowerShell 提供簡單的方法，在 HDInsight 叢集上執行 MapReduce 工作、監視工作狀態，以及擷取輸出。

## <a id="nextsteps"></a>接續步驟

如需 HDInsight 中 MapReduce 工作的一般資訊：

* [在 HDInsight Hadoop 上使用 MapReduce](hdinsight-use-mapreduce.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)
* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)

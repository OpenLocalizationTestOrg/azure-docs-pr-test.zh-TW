---
title: "使用 PowerShell HDInsight 的 Azure 中的 Hadoop Pig aaaUse |Microsoft 文件"
description: "了解使用 Azure PowerShell HDInsight 上 toosubmit Pig 工作 tooa Hadoop 叢集的方式。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a>使用 HDInsight 的 Azure PowerShell toorun Pig 工作

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

本文件提供使用 Azure PowerShell toosubmit Pig 工作 tooa Hadoop HDInsight 叢集上的範例。 Pig 可讓您使用資料轉換為模型語言 （Pig 拉丁） 的 toowrite MapReduce 工作，而非對應並減少函式。

> [!NOTE]
> 這份文件不提供 hello 範例中使用的 hello Pig 拉丁陳述式所執行的工作詳細的的描述。 Hello Pig 拉丁此範例中使用的相關資訊，請參閱[的 Hadoop HDInsight 上搭配使用 Pig](hdinsight-use-pig.md)。

## <a id="prereq"></a>必要條件

* **Azure HDInsight 叢集**

  > [!IMPORTANT]
  > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* **具有 Azure PowerShell 的工作站**。

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a id="powershell"></a>使用 PowerShell 執行 Pig 工作

Azure PowerShell 提供*cmdlet* ，可讓您執行 tooremotely Pig 工作在 HDInsight 上。 就內部而言，PowerShell 會使用 REST 呼叫太[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) hello HDInsight 叢集上執行。

hello 下列指令程式可用時在遠端的 HDInsight 叢集上執行 Pig 工作：

* **登入 AzureRmAccount**： 驗證 Azure PowerShell tooyour Azure 訂用帳戶
* **新 AzureRmHDInsightPigJobDefinition**： 建立*作業定義*使用 hello 指定 Pig 拉丁陳述式
* **開始 AzureRmHDInsightJob**： 傳送 hello 工作定義 tooHDInsight、 啟動 hello 工作，並傳回*作業*可以是使用的 toocheck hello hello 工作狀態的物件
* **等候 AzureRmHDInsightJob**： 使用 hello 工作物件 toocheck hello hello 工作狀態。 它會等候 hello 作業已完成，或已超過 hello 等待時間。
* **Get AzureRmHDInsightJobOutput**： 使用 tooretrieve hello hello 工作輸出

hello 下列步驟示範如何 toouse 這些 cmdlet toorun 您的 HDInsight 叢集上的工作。

1. 使用編輯器中，儲存下列程式碼做為 hello **pigjob.ps1**。

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. 開啟新的 Windows PowerShell 命令提示字元。 變更目錄 toohello 位置 hello **pigjob.ps1**檔案，然後使用下列命令 toorun hello 指令碼的 hello:

        .\pigjob.ps1

    您必須提示的 toolog tooyour Azure 訂用帳戶中。 然後，系統會詢問 hello HTTPs/系統管理員帳戶名稱和密碼 hello HDInsight 叢集。

2. Hello 作業完成時，它應該傳回資訊的類似 toohello 下列文字：

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="troubleshooting"></a>疑難排解

如果 hello 作業完成時，會不傳回任何資訊，可能會在處理期間發生錯誤。 tooview 錯誤資訊，為這個工作中，加入下列命令 toohello 結尾 hello hello **pigjob.ps1**檔、 加以儲存，然後再執行一次。

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

這會傳回 hello 資訊寫入 tooSTDERR hello 伺服器上執行 hello 作業時，它可以幫助判斷 hello 作業失敗的原因。

## <a id="summary"></a>摘要
如您所見，Azure PowerShell 提供簡單的方式 toorun Pig 工作 HDInsight 叢集，監視 hello 工作狀態和擷取 hello 輸出。

## <a id="nextsteps"></a>接續步驟
如需 HDInsight 中 Pig 的一般資訊：

* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)

---
title: "使用 PowerShell HDInsight 的 Azure 中的 Hadoop Hive aaaUse |Microsoft 文件"
description: "在 HDInsight 上的 Hadoop 使用 PowerShell toorun Hive 查詢。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a>使用 PowerShell 執行 Hive 查詢
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

本文件提供使用 Azure PowerShell hello Azure 資源群組模式 toorun Hive 查詢中 HDInsight 叢集上的 Hadoop 中的範例。

> [!NOTE]
> 這份文件不提供 hello 範例中所用的 hello HiveQL 陳述式所執行的工作詳細的的描述。 在 hello HiveQL 這個範例中所使用的資訊，請參閱[的 HDInsight 上的 Hadoop Hive 使用](hdinsight-use-hive.md)。

**必要條件**

* **Azure HDInsight 叢集**： 不論是否 hello 叢集是 Windows 或 Linux。

  > [!IMPORTANT]
  > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* **具有 Azure PowerShell 的工作站**。

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a>使用 Azure PowerShell 執行 Hive 查詢

Azure PowerShell 提供*cmdlet* ，HDInsight 上允許您 tooremotely 執行 Hive 查詢。 就內部而言，hello cmdlet 進行 REST 呼叫太[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) hello HDInsight 叢集上。

hello 下列指令程式會使用遠端的 HDInsight 叢集中執行 Hive 查詢時：

* **新增 AzureRmAccount**： 驗證 Azure PowerShell tooyour Azure 訂用帳戶
* **新 AzureRmHDInsightHiveJobDefinition**： 建立*作業定義*使用 hello 指定 HiveQL 陳述式
* **開始 AzureRmHDInsightJob**： 傳送 hello 工作定義 tooHDInsight、 啟動 hello 工作，並傳回*作業*可以是使用的 toocheck hello hello 工作狀態的物件
* **等候 AzureRmHDInsightJob**： 使用 hello 工作物件 toocheck hello hello 工作狀態。 它會等候 hello 作業完成，或超出 hello 等待時間。
* **Get AzureRmHDInsightJobOutput**： 使用 tooretrieve hello hello 工作輸出
* **叫用 AzureRmHDInsightHiveJob**： 使用 toorun HiveQL 陳述式。 此 cmdlet 區塊 hello 查詢完成時，則會傳回 hello 結果
* **使用 AzureRmHDInsightCluster**： 集 hello hello 目前叢集 toouse **Invoke AzureRmHDInsightHiveJob**命令

hello 下列步驟示範如何 toouse 這些 cmdlet toorun 中您的 HDInsight 叢集的工作：

1. 使用編輯器中，儲存下列程式碼做為 hello **hivejob.ps1**。

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. 開啟新的 **Azure PowerShell** 命令提示字元。 變更目錄 toohello 位置 hello **hivejob.ps1**檔案，然後使用下列命令 toorun hello 指令碼的 hello:

        .\hivejob.ps1

    Hello 指令碼執行時，您將會提示的 tooenter hello 叢集名稱和 hello HTTPS/系統管理帳戶認證 hello 叢集。 您也可能提示的 toolog tooyour Azure 訂用帳戶中。

3. Hello 作業完成時，它會傳回資訊的類似 toohello 遵循 thext:

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. 如先前所述， **Invoke-hive**可以是使用的 toorun 查詢，並等候 hello 回應。 使用下列方式叫用 Hive 指令碼 toosee hello:

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    hello 輸出看起來類似下列文字的 hello:

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > 對於較長的 HiveQL 查詢，您可以使用 hello Azure PowerShell **Here-string** cmdlet 或下列 HiveQL 指令碼檔案。 下列程式碼片段說明如何 hello toouse hello **Invoke-hive** cmdlet toorun 下列 HiveQL 指令碼檔案。 hello HiveQL 指令碼檔案必須上傳 toowasb: / /。
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > 如需 **Here-Strings** 的詳細資訊，請參閱<a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">使用 Windows PowerShell Here-Strings</a>。

## <a name="troubleshooting"></a>疑難排解

如果 hello 作業完成時，會不傳回任何資訊，可能會在處理期間發生錯誤。 tooview 錯誤資訊，為這個工作中，加入下列 toohello 結尾 hello hello **hivejob.ps1**檔、 加以儲存，然後再執行一次。

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

此 cmdlet 會傳回執行 hello 作業時，會寫入 tooSTDERR hello 伺服器的 hello 資訊。

## <a name="summary"></a>摘要

如您所見，Azure PowerShell 提供簡單的方式 toorun HDInsight 叢集中的 Hive 查詢、 監視器 hello 工作的狀態，和擷取 hello 輸出。

## <a name="next-steps"></a>後續步驟

如需 HDInsight 中 Hive 的一般資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)

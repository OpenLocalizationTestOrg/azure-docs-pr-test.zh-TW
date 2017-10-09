---
title: "使用 Apache Hive 和 Pig-Azure HDInsight UDF aaaPython |Microsoft 文件"
description: "了解如何 toouse Python 使用者定義函數 (UDF) 從 Hive 和 Pig 在 HDInsight Hadoop 技術 hello 堆疊在 Azure 上。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a>在 HDInsight 上使用 Python 使用者定義函數 (UDF) 與 Hive 和 Pig

了解如何 toouse Python 使用者定義函數 (UDF) 與 Apache Hive 和 Pig Azure HDInsight 上的 Hadoop 中。

## <a name="python"></a>HDInsight 上的 Python

HDInsight 3.0 和更新版本上預設已安裝 Python2.7。 Apache Hive 可以與此版本的 Python 搭配使用，以進行資料流處理。 資料流處理會使用 Hive 和 hello UDF 之間 STDOUT 和 STDIN toopass 資料。

HDInsight 也包含 Jython (以 Java 撰寫的 Python 實作)。 Jython 直接在 hello Java 虛擬機器上執行，並不使用資料流。 Jython 是 hello Pig 搭配使用 Python 時建議使用 Python 解譯器。

> [!WARNING]
> 本文件中的 hello 步驟進行下列假設 hello: 
>
> * 您建立 hello Python 指令碼的本機開發環境上。
> * 您上傳使用任一 hello hello 指令碼 tooHDInsight`scp`從本機 Bash 工作階段或 hello 提供 PowerShell 指令碼命令。
>
> 如果您想 toouse hello [Azure 雲端殼層 (bash)](https://docs.microsoft.com/azure/cloud-shell/overview)預覽 toowork 與 HDInsight，則必須：
>
> * 建立 hello hello 雲端殼層環境內的指令碼。
> * 使用`scp`tooupload hello 檔案從 hello 雲端殼層 tooHDInsight。
> * 使用`ssh`從 hello 雲端殼層 tooconnect tooHDInsight 和執行的 hello 範例。

## <a name="hivepython"></a>Hive UDF

Python 可用來當作 UDF 從 Hive 透過 hello HiveQL`TRANSFORM`陳述式。 例如，下列 HiveQL hello 叫用 hello `hiveudf.py` hello hello 叢集的預設 Azure 儲存體帳戶中儲存檔案。

**以 Linux 為基礎的 HDInsight**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

**以 Windows 為基礎的 HDInsight**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> 在 Windows 為基礎的 HDInsight 叢集上 hello`USING`子句必須指定 hello 完整路徑 toopython.exe。

以下是此範例所執行的動作：

1. hello `add file` hello 檔案的 hello 開頭的陳述式會將 hello`hiveudf.py`檔案 toohello 分散式快取，，所以 hello 叢集中所有節點存取。
2. hello`SELECT TRANSFORM ... USING`陳述式從 hello 選取資料`hivesampletable`。 它也會傳遞 hello clientid、 devicemake 和 devicemodel 值 toohello`hiveudf.py`指令碼。
3. hello`AS`子句描述從傳回的 hello 欄位`hiveudf.py`。

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a>建立 hello hiveudf.py 檔案


在開發環境中，建立名為 `hiveudf.py` 的文字檔。 使用下列程式碼為 hello hello 檔案內容的 hello:

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

此指令碼會執行下列動作的 hello:

1. 從 STDIN 中讀取資料行。
2. 使用移除尾端新行字元的 hello `string.strip(line, "\n ")`。
3. 當進行資料流處理時，單行包含定位字元，每個值之間的所有 hello 值。 因此`string.split(line, "\t")`可以是使用的 toosplit hello 輸入每個索引標籤，傳回只 hello 欄位。
4. 處理序完成時，hello 輸出必須寫 tooSTDOUT 成單一行中的每個欄位的索引標籤。 例如： `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`。
5. hello`while`迴圈會重複，直到沒有`line`讀取。

hello 指令碼輸出是 hello 的輸入值的串連`devicemake`和`devicemodel`，和雜湊 hello 的串連值。

請參閱[執行 hello 範例](#running)如何 toorun HDInsight 叢集上的這個範例。

## <a name="pigpython"></a>Pig UDF

Python 指令碼可用來當做從 Pig UDF 透過 hello`GENERATE`陳述式。 您可以執行使用 Jython 或 C Python hello 指令碼。

* Jython hello JVM 上, 執行，並且從 Pig 可原生。
* C Python 是外部處理序，以便將資料從 Pig hello 上 hello JVM 送出 toohello Python 處理序中執行的指令碼。 hello 的 hello Python 指令碼的輸出會傳送回 Pig。

toospecify hello Python 解釋器，使用`register`參考 hello Python 指令碼時。 hello 下列範例指令碼使用註冊為 Pig `myfuncs`:

* **toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`
* **toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`

> [!IMPORTANT]
> 當使用 Jython，hello 路徑 toohello pig_jython 檔案可以是本機路徑或 WASB: / / 路徑。 不過，使用 C Python，您必須參考 hello 節點使用 toosubmit hello Pig 工作 hello 本機檔案系統上的檔案。

一旦註冊，超過此範例中的 hello Pig 拉丁 hello 相同兩個：

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

以下是此範例所執行的動作：

1. hello 第一行會載入 hello 範例資料檔`sample.log`到`LOGS`。 它也會將每一筆記錄定義為 `chararray`。
2. hello 下一行會篩選出 null 值，儲存的 hello 作業插入的 hello 結果`LOG`。
3. 接下來，它會逐一中的 hello 記錄`LOG`並用`GENERATE`tooinvoke hello `create_structure` hello Python/Jython 指令碼中所包含的方法以載入`myfuncs`。 `LINE`是使用的 toopass hello 目前記錄 toohello 函式。
4. 最後，hello 輸出都是使用 hello 傾印的 tooSTDOUT`DUMP`命令。 Hello 作業完成之後，此命令會顯示 hello 結果。

### <a name="create-hello-pigudfpy-file"></a>建立 hello pigudf.py 檔案

在開發環境中，建立名為 `pigudf.py` 的文字檔。 使用下列程式碼為 hello hello 檔案內容的 hello:

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

在 hello Pig 拉丁範例中，我們定義 hello `LINE` chararray 為輸入，因為沒有 hello 輸入沒有一致的結構描述。 hello Python 指令碼會將 hello 資料轉換成一致的結構描述的輸出。

1. hello`@outputSchema`陳述式定義 hello 傳回 tooPig hello 資料格式。 在此案例中，這是一個 **data bag**(一種 Pig 資料類型)。 hello 包包含下列的欄位，都是 chararray （字串） 的 hello:

   * 日期-hello 日期 hello 記錄項目已建立
   * 時間-hello hello 記錄項目建立的時間
   * 類別名稱-已建立 hello 類別名稱 hello 項目
   * 層級-hello 記錄層級
   * 詳細資料： hello 的詳細資訊詳細資料記錄項目

2. 接下來，hello`def create_structure(input)`定義 Pig 會傳遞至明細項目的 hello 函式。

3. hello 範例資料， `sample.log`、 大部分符合 toohello 日期、 時間、 classname，層級，而且我們想 tooreturn 結構描述的詳細說明。 不過，它包含開頭為 `*java.lang.Exception*` 的數行。 這些行數必須是已修改的 toomatch hello 結構描述。 hello`if`陳述式會檢查，然後 massages hello 輸入的資料 toomove hello`*java.lang.Exception*`字串 toohello 結束時，將 hello 資料內嵌我們預期的輸出結構描述。

4. 接下來，hello`split`命令是使用的 toosplit hello hello 前四個空格字元的資料。 hello 輸出會指派到`date`， `time`， `classname`， `level`，和`detail`。

5. 最後，會傳回 hello 值 tooPig。

Hello 資料傳回時 tooPig，它有一致的結構描述定義在 hello`@outputSchema`陳述式。

## <a name="running"></a>上傳及執行 hello 範例

> [!IMPORTANT]
> hello **SSH**步驟只適用於以 Linux 為基礎的 HDInsight 叢集。 hello **PowerShell**使用 Linux 或 Windows 為基礎的 HDInsight 叢集的步驟，但需要 Windows 用戶端。

### <a name="ssh"></a>SSH

如需使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

1. 使用`scp`toocopy hello 檔案 tooyour HDInsight 叢集。 比方說，下列命令複製 hello 名為的檔案 tooa 叢集來 hello **mycluster**。

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. 使用 SSH tooconnect toohello 叢集。

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. Hello SSH 工作階段中，加入 hello python 上傳檔案之前 hello 叢集 toohello WASB 存放裝置。

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

上傳 hello 檔案之後, 使用 hello 下列步驟會 toorun hello Hive 和 Pig 工作。

#### <a name="use-hello-hive-udf"></a>使用 Hive UDF hello

1. 使用 hello`hive`命令 toostart hello hive 殼層。 您應該會看到`hive>`當載入 hello 殼層提示。

2. 輸入下列查詢在 hello hello`hive>`提示：

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. 輸入 hello 最後一行之後, 應該啟動 hello 作業。 一旦 hello 作業完成時，它會傳回下列範例的輸出類似 toohello:

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a>使用 Pig UDF hello

1. 使用 hello`pig`命令 toostart hello 殼層。 您會看到`grunt>`當載入 hello 殼層提示。

2. 輸入下列陳述式在 hello hello`grunt>`提示：

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. 在輸入後 hello 行下，應該啟動 hello 作業。 一旦 hello 作業完成時，它會傳回下列資料的輸出類似 toohello:

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. 使用`quit`tooexit hello Grunt 殼層，然後再使用下列 tooedit hello pigudf.py 檔 hello 本機檔案系統上的 hello:

    ```bash
    nano pigudf.py
    ```

5. 一次在 hello 編輯器中，請取消註解 hello 行下藉由移除 hello `#` hello 一行的 hello 開頭的字元：

    ```bash
    #from pig_util import outputSchema
    ```

    一旦 hello 已變更，使用 Ctrl + X tooexit hello 編輯器。 選取 Y、，然後輸入 toosave hello 變更。

6. 使用 hello`pig`命令 toostart hello 殼層一次。 一旦您是在 hello`grunt>`提示，請使用下列 toorun hello Python 指令碼使用 hello C Python 解譯器的 hello。

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    這項作業完成之後，您應該看到的 hello 相同的輸出做為您先前執行使用 Jython hello 指令碼時。

### <a name="powershell-upload-hello-files"></a>PowerShell： 上傳 hello 檔案

您可以使用 PowerShell tooupload hello 檔案 toohello HDInsight 伺服器。 使用下列指令碼 tooupload hello Python 檔案 hello:

> [!IMPORTANT] 
> 本節中的 hello 步驟使用 Azure PowerShell。 如需有關使用 Azure PowerShell 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> 變更 hello `C:\path\to` toohello 路徑 toohello 檔案，在開發環境上的值。

此指令碼會擷取您的 HDInsight 叢集的資訊，然後擷取 hello 帳戶和金鑰 hello 預設儲存體帳戶，並上傳 hello hello 容器的檔案 toohello 根。

> [!NOTE]
> 如需有關上傳檔案的詳細資訊，請參閱 hello [HDInsight 中的 Hadoop 工作的資料上傳](hdinsight-upload-data.md)文件。

#### <a name="powershell-use-hello-hive-udf"></a>PowerShell： 使用 hello Hive UDF

PowerShell 也可以使用的 tooremotely 執行 Hive 查詢。 使用下列 PowerShell 指令碼 toorun 使用 Hive 查詢的 hello **hiveudf.py**指令碼：

> [!IMPORTANT]
> 再執行，hello 指令碼會提示您輸入 hello HTTPs/管理您的 HDInsight 叢集的帳戶資訊。

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

hello 輸出 hello **Hive**作業應該會出現類似下列範例的 toohello:

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a>Pig (Jython)

PowerShell 也可以使用的 toorun Pig 拉丁作業。 toorun Pig 拉丁作業使用 hello **pigudf.py**編寫指令碼，請使用下列 PowerShell 指令碼的 hello:

> [!NOTE]
> 當從遠端提交工作，使用 PowerShell，它是不可能 toouse C Python hello 直譯器。

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

hello 輸出 hello **Pig**作業應該會出現類似 toohello 下列資料：

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <a name="troubleshooting"></a>疑難排解

### <a name="errors-when-running-jobs"></a>執行工作時發生錯誤

當執行 hello hive 工作，您可能會遇到錯誤類似 toohello 下列文字：

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

這個問題可能被因 hello hello Python 檔案中的行尾結束符號。 許多 Windows 編輯器預設 toousing CRLF 為 hello 行尾結束符號，但 Linux 應用程式通常會預期 LF。

您可以使用下列 PowerShell 陳述式 tooremove hello CR 字元之前上傳 hello 檔案 tooHDInsight hello:

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a>PowerShell 指令碼

這兩個 hello 範例使用 toorun hello 範例 PowerShell 指令碼包含加上註解的線條顯示 hello 之工作的錯誤輸出。 如果您沒有看到預期的 hello hello 之工作的輸出，請取消註解 hello 下列行，並查看 hello 錯誤資訊如果表示有問題。

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

hello 長期資訊時發生錯誤 (STDERR) 與 hello 工作 (STDOUT) hello 結果也是記錄的 tooyour HDInsight 儲存體。

| 關於此工作... | 查看這些 hello blob 容器中的檔案 |
| --- | --- |
| Hive |/HivePython/stderr<p>/HivePython/stdout |
| Pig |/PigPython/stderr<p>/PigPython/stdout |

## <a name="next"></a>接續步驟

如果您需要預設未提供的 tooload Python 模組，請參閱[如何 toodeploy 模組 tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx)。

其他的方式 toouse Pig、 Hive 和有關使用 MapReduce toolearn，請參閱下列文件的 hello:

* [搭配 HDInsight 使用 Hivet](hdinsight-use-hive.md)
* [搭配 HDInsight 使用 Pig](hdinsight-use-pig.md)
* [〈搭配 HDInsight 使用 MapReduce〉](hdinsight-use-mapreduce.md)

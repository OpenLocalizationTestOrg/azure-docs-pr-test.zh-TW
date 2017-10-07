---
title: "aaaUse C# 使用 Hive 和 Pig HDInsight 的 Azure 中的 Hadoop 上 |Microsoft 文件"
description: "了解如何 toouse C# 使用者定義函數 (UDF) 用於 Hive 和 Pig Azure HDInsight 中的資料流。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a>搭配使用 C# 使用者定義函數與 HDInsight 的 Hadoop 上的 Hive 和 Pig 串流處理。

了解 toouse C# 使用者定義函數 (UDF) 與 Apache Hive 和 Pig HDInsight 上的方式。

> [!IMPORTANT]
> 本文件中的 hello 步驟使用 linux 和 Windows 為基礎的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md)。

兩者的 Hive 和 Pig 可以將資料 tooexternal 應用程式進行處理傳遞。 這個程序稱為_串流處理_。 Hello 資料時使用.NET 應用程式，會傳遞 toohello 應用程式上 STDIN、 並 hello 應用程式傳回 hello 結果 STDOUT 上。 tooread 以及來自 STDIN 和 STDOUT 寫入，您可以使用`Console.ReadLine()`和`Console.WriteLine()`從主控台應用程式。

## <a name="prerequisites"></a>必要條件

* 熟悉如何撰寫和建置以 .NET Framework 4.5 為目標的 C# 程式碼。

    * 使用您想要的任何 IDE。 建議您使用 [Visual Studio](https://www.visualstudio.com/vs) 2015、2017 或 [Visual Studio Code](https://code.visualstudio.com/)。 此文件使用 Visual Studio 2017 hello 步驟。

* 方式 tooupload.exe 檔案 toohello 叢集並執行的 Pig 和 Hive 工作。 我們建議 Visual Studio、 Azure PowerShell 和 Azure CLI hello 資料湖工具。 hello 本文件中的步驟使用 hello 資料湖 Tools for Visual Studio tooupload hello 檔案並執行 hello 範例 Hive 查詢。

    其他方式 toorun Hive 查詢和 Pig 工作上的資訊，請參閱下列文件的 hello:

    * [搭配 HDInsight 使用 Apache Hive](hdinsight-use-hive.md)

    * [搭配 HDInsight 使用 Apache Pig](hdinsight-use-pig.md)

* HDInsight 叢集上的 Hadoop。 如需有關建立叢集的詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-provision-clusters.md)。

## <a name="net-on-hdinsight"></a>HDInsight 上的 .NET

* __以 Linux 為基礎的 HDInsight__使用叢集[單聲道 (https://mono-project.com)](https://mono-project.com) toorun.NET 應用程式。 4.2.1 版的 Mono 隨附於 3.5 版的 HDInsight。

    如需 Mono 與 .NET Framework 版本之相容性的詳細資訊，請參閱 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/) \(英文\)。

    toouse 特定版本的 Mono，請參閱 hello[安裝或更新 Mono](hdinsight-hadoop-install-mono.md)文件。

* __Windows 為基礎的 HDInsight__叢集使用 hello Microsoft.NET CLR toorun.NET 應用程式。

如需有關 hello hello.NET framework 版本和 Mono HDInsight 版本所隨附的詳細資訊，請參閱[HDInsight 元件版本](hdinsight-component-versioning.md)。

## <a name="create-hello-c-projects"></a>建立 hello C\#專案

### <a name="hive-udf"></a>Hive UDF

1. 開啟 Visual Studio 並建立方案。 Hello 專案類型 選取**主控台應用程式 (.NET Framework)**，和名稱 hello 新專案**HiveCSharp**。

    > [!IMPORTANT]
    > 如果您使用以 Linux 為基礎的 HDInsight 叢集，請選取 __.NET Framework 4.5__。 如需 Mono 與 .NET Framework 版本之相容性的詳細資訊，請參閱 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/) \(英文\)。

2. 取代 hello 內容**Program.cs** hello 下列：

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. 建置 hello 專案。

### <a name="pig-udf"></a>Pig UDF

1. 開啟 Visual Studio 並建立方案。 Hello 專案類型 選取**主控台應用程式**，和名稱 hello 新專案**PigUDF**。

2. 取代 hello hello 內容**Program.cs**檔案以下列程式碼的 hello:

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    此應用程式剖析 Pig，從傳送 hello 線條和重新格式化線條的開頭`java.lang.Exception`。

3. 儲存**Program.cs**，然後建置 hello 專案。

## <a name="upload-toostorage"></a>上傳 toostorage

1. 在 Visual Studio 中，開啟 [伺服器總管] 。

2. 展開 [Azure]，然後展開 [HDInsight]。

3. 如果出現提示，請輸入您的 Azure 訂用帳戶認證，然後按一下登入。

4. 展開您想 toodeploy 此應用程式的 hello HDInsight 叢集。 具有 hello 文字的項目__（預設儲存體帳戶）__列。

    ![顯示 hello hello 叢集的儲存體帳戶的伺服器總管](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * 您可以展開此項目，如果使用__Azure 儲存體帳戶__為 hello 叢集的預設儲存位置。 tooview hello 上的檔案 hello 預設儲存體 hello 叢集展開 hello 項目，然後按兩下 hello __（預設容器）__。

    * 無法展開此項目時，如果您使用__Azure Data Lake Store__為 hello hello 叢集的預設存放裝置。 tooview hello hello 預設儲存體上 hello 叢集檔案，按兩下 hello __（預設儲存體帳戶）__項目。

6. tooupload hello.exe 檔，使用其中一種 hello 下列方法：

    * 如果使用__Azure 儲存體帳戶__、 按一下 hello 上傳 圖示，然後瀏覽 toohello **bin\debug**資料夾 hello **HiveCSharp**專案。 最後，選取 hello **HiveCSharp.exe**檔案，然後按一下 **確定**。

        ![上傳圖示](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * 如果使用__Azure Data Lake Store__，hello 檔案清單中中的空白區域上按一下滑鼠右鍵，然後選取__上傳__。 最後，選取 hello **HiveCSharp.exe**檔案，然後按一下 **開啟**。

    一次 hello __HiveCSharp.exe__上傳完成時，重複 hello 上傳程序 hello __PigUDF.exe__檔案。

## <a name="run-a-hive-query"></a>執行 HIVE 查詢

1. 在 Visual Studio 中，開啟 [伺服器總管]。

2. 展開 [Azure]，然後展開 [HDInsight]。

3. 以滑鼠右鍵按一下您所部署的 hello 的 hello 叢集**HiveCSharp** ，應用程式，然後選取**撰寫 Hive 查詢**。

4. 使用下列 hello Hive 查詢的文字的 hello:

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > 請取消註解 hello`add file`用於您叢集的預設儲存體 hello 型別對應的陳述式。

    此查詢會選取 hello `clientid`， `devicemake`，和`devicemodel`欄位從`hivesampletable`，並傳遞 hello 欄位 toohello HiveCSharp.exe 應用程式。 hello 查詢必須要有 hello 應用程式 tooreturn 三個欄位，它儲存為`clientid`， `phoneLabel`，和`phoneHash`。 hello 查詢也必須要有 toofind HiveCSharp.exe hello hello 預設儲存體容器的根目錄中。

5. 按一下**送出**toosubmit hello 作業 toohello HDInsight 叢集。 hello **Hive 工作摘要**視窗隨即開啟。

6. 按一下**重新整理**toorefresh hello 摘要直到**作業狀態**變更太**已完成**。 tooview hello 作業輸出，按一下**作業輸出**。

## <a name="run-a-pig-job"></a>執行 Pig 作業

1. 請使用下列方法 tooconnect tooyour HDInsight 叢集的 hello:

    * 如果您使用__以 Linux 為基礎的__ HDInsight 叢集，請使用 SSH。 例如，`ssh sshuser@mycluster-ssh.azurehdinsight.net`。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)
    
    * 如果您使用__windows__ HDInsight 叢集[使用遠端桌面連線 toohello 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)

2. 使用下列命令 toostart hello Pig 命令列的一個 hello:

        pig

    > [!IMPORTANT]
    > 如果您使用 Windows 叢集，請使用 hello 改用下列命令：
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    `grunt>` 提示隨即顯示。

3. 輸入 hello 遵循 toorun hello.NET Framework 應用程式會使用 Pig 工作：

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    hello`DEFINE`陳述式會建立別名`streamer`hello pigudf.exe 應用程式，以及`CACHE`載入從 hello 叢集的預設儲存體。 稍後，`streamer`搭配 hello`STREAM`運算子 tooprocess hello 為一系列的資料行包含在記錄檔和傳回 hello 資料的單一線條。

    > [!NOTE]
    > 用在資料流的 hello 應用程式名稱必須以 hello 括住\`（單引號） 字元時別名，以及 ' （單引號） 搭配使用時`SHIP`。

4. 輸入 hello 最後一行之後, 應該啟動 hello 作業。 它會傳回輸出類似 toohello 下列文字：

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a>後續步驟

在本文件中，您已經學會如何 toouse 從 Hive 和 Pig HDInsight 上的.NET Framework 應用程式。 如果您想要如何 toouse Python 用於 Hive 和 Pig，請參閱的 toolearn[將 Python 用於 Hive 和 Pig HDInsight 中的](hdinsight-python.md)。

其他的方式 toouse Pig 和 Hive 和有關使用 MapReduce toolearn，請參閱下列文件的 hello:

* [搭配 HDInsight 使用 Hivet](hdinsight-use-hive.md)
* [搭配 HDInsight 使用 Pig](hdinsight-use-pig.md)
* [〈搭配 HDInsight 使用 MapReduce〉](hdinsight-use-mapreduce.md)

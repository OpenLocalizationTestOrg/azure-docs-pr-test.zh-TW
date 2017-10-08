---
title: "aaaUse MapReduce HDInsight 的 Azure 中的 Hadoop 上搭配使用 C# |Microsoft 文件"
description: "深入了解如何使用 Azure HDInsight 中的 Hadoop toouse C# toocreate MapReduce 解決方案。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a>搭配 HDInsight 的 Hadoop 上的 MapReduce 串流使用 C#

深入了解如何 toouse C# toocreate HDInsight MapReduce 解決方案。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md)。

Hadoop 串流處理是可讓您使用指令碼或可執行檔 toorun MapReduce 工作的公用程式。 在此範例中，.NET 是使用的 tooimplement hello 對應工具和減壓器 word 計數解決方案。

## <a name="net-on-hdinsight"></a>HDInsight 上的 .NET

__以 Linux 為基礎的 HDInsight__叢集使用[單聲道 (https://mono-project.com)](https://mono-project.com) toorun.NET 應用程式。 4.2.1 版的 Mono 隨附於 3.5 版的 HDInsight。 多個 hello Mono 隨附 HDInsight 版本的詳細資訊，請參閱[HDInsight 元件版本](hdinsight-component-versioning.md)。 toouse 特定版本的 Mono，請參閱 hello[安裝或更新 Mono](hdinsight-hadoop-install-mono.md)文件。

如需 Mono 與 .NET Framework 版本之相容性的詳細資訊，請參閱 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/) \(英文\)。

## <a name="how-hadoop-streaming-works"></a>Hadoop 串流的運作方式

用於資料流處理本文件中的 hello 基本程序如下所示：

1. Hadoop，傳遞 STDIN 資料 toohello 對應程式 (在此範例中 mapper.exe)。
2. hello 對應工具處理 hello 資料，並發出 tab 鍵分隔的索引鍵/值組 tooSTDOUT。
3. hello 輸出是由 Hadoop，讀取，然後傳遞 STDIN toohello 減壓器 (reducer.exe 在此範例中)。
4. hello 減壓器讀取 hello tab 鍵分隔的索引鍵/值組、 處理 hello 資料，並再發出 hello 結果為 STDOUT 上以 tab 分隔的索引鍵/值組。
5. hello 輸出是由 Hadoop 讀取和寫入 toohello 輸出目錄。

如需串流的詳細資訊，請參閱 [Hadoop 串流 (英文) (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)。

## <a name="prerequisites"></a>必要條件

* 熟悉如何撰寫和建置以 .NET Framework 4.5 為目標的 C# 程式碼。 此文件使用 Visual Studio 2017 hello 步驟。

* 方式 tooupload.exe 檔案 toohello 叢集。 hello 本文件中的步驟使用 hello 資料湖 Tools for Visual Studio tooupload hello 檔案 tooprimary 叢集的存放裝置 hello。

* Azure PowerShell 或 SSH 用戶端。

* HDInsight 叢集上的 Hadoop。 如需有關建立叢集的詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-provision-clusters.md)。

## <a name="create-hello-mapper"></a>建立 hello 對應程式

在 Visual Studio 中，建立名為 __mapper__ 的新__主控台應用程式__。 使用下列 hello 應用程式程式碼的 hello:

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

在建立之後 hello 應用程式，建立該 tooproduce hello `/bin/Debug/mapper.exe` hello 專案目錄中的檔案。

## <a name="create-hello-reducer"></a>建立 hello 減壓器

在 Visual Studio 中，建立名為 __reducer__ 的新__主控台應用程式__。 使用下列 hello 應用程式程式碼的 hello:

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

在建立之後 hello 應用程式，建立該 tooproduce hello `/bin/Debug/reducer.exe` hello 專案目錄中的檔案。

## <a name="upload-toostorage"></a>上傳 toostorage

1. 在 Visual Studio 中，開啟 [伺服器總管] 。

2. 展開 [Azure]，然後展開 [HDInsight]。

3. 如果出現提示，請輸入您的 Azure 訂用帳戶認證，然後按一下登入。

4. 展開您想 toodeploy 此應用程式的 hello HDInsight 叢集。 具有 hello 文字的項目__（預設儲存體帳戶）__列。

    ![顯示 hello hello 叢集的儲存體帳戶的伺服器總管](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * 您可以展開此項目，如果使用__Azure 儲存體帳戶__為 hello 叢集的預設儲存位置。 tooview hello 上的檔案 hello 預設儲存體 hello 叢集展開 hello 項目，然後按兩下 hello __（預設容器）__。

    * 無法展開此項目時，如果您使用__Azure Data Lake Store__為 hello hello 叢集的預設存放裝置。 tooview hello hello 預設儲存體上 hello 叢集檔案，按兩下 hello __（預設儲存體帳戶）__項目。

5. tooupload hello.exe 檔，使用其中一種 hello 下列方法：

    * 如果使用__Azure 儲存體帳戶__、 按一下 hello 上傳 圖示，然後瀏覽 toohello **bin\debug**資料夾 hello**對應工具**專案。 最後，選取 hello **mapper.exe**檔案，然後按一下 **確定**。

        ![上傳圖示](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * 如果使用__Azure Data Lake Store__，hello 檔案清單中中的空白區域上按一下滑鼠右鍵，然後選取__上傳__。 最後，選取 hello **mapper.exe**檔案，然後按一下 **開啟**。

    一次 hello __mapper.exe__上傳完成時，重複 hello 上傳程序 hello __reducer.exe__檔案。

## <a name="run-a-job-using-an-ssh-session"></a>執行工作︰使用 SSH 工作階段

1. 使用 SSH tooconnect toohello HDInsight 叢集。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 使用下列命令 toostart hello MapReduce 工作的 hello 的其中一個：

    * 如果使用 __Data Lake Store__ 作為預設儲存體：

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * 如果使用 __Azure 儲存體__作為預設儲存體：

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    hello 下列清單說明每個參數的用途：

    * `hadoop-streaming.jar`: hello jar 檔案，其中包含 hello 串流 MapReduce 功能。
    * `-files`： 另加入 hello`mapper.exe`和`reducer.exe`檔案 toothis 作業。 hello`adl:///`或`wasb:///`每個檔案是 hello 路徑 toohello 根 hello 叢集的預設儲存體之前。
    * `-mapper`： 指定哪些檔案會實作 hello 對應工具。
    * `-reducer`： 指定哪些檔案會實作 hello 減壓器。
    * `-input`: hello 輸入資料。
    * `-output`: hello 輸出目錄。

3. Hello MapReduce 工作完成之後，請使用下列 tooview hello 結果 hello:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    hello 下列文字是這個命令所傳回的 hello 資料的範例：

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a>執行作業：使用 PowerShell

使用下列 PowerShell 指令碼 toorun MapReduce 工作的 hello 和下載 hello 結果。

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

此指令碼會提示您輸入 hello 叢集登入帳戶名稱和密碼，以及 hello HDInsight 叢集名稱。 Hello 輸出 hello 作業完成之後，會下載的 toohello `output.txt` hello 目錄 hello 指令碼中的檔案從執行。 hello 下列文字是在 hello hello 資料的範例`output.txt`檔案：

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a>後續步驟

如需搭配 HDInsight 使用 MapReduce 的詳細資訊，請參閱[搭配 HDInsight 使用 MapReduce](hdinsight-use-mapreduce.md)。

如需搭配 Hive 與 Pig 使用 C# 的詳細資訊，請參閱[搭配 Hive 與 Pig 使用 C# 使用者定義函式](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)。

如需搭配 HDInsight 上的 Storm 使用 C# 的詳細資訊，請參閱[開發適用於 Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。
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
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="a7ada-103">搭配 HDInsight 的 Hadoop 上的 MapReduce 串流使用 C#</span><span class="sxs-lookup"><span data-stu-id="a7ada-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="a7ada-104">深入了解如何 toouse C# toocreate HDInsight MapReduce 解決方案。</span><span class="sxs-lookup"><span data-stu-id="a7ada-104">Learn how toouse C# toocreate a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7ada-105">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="a7ada-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a7ada-106">如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="a7ada-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="a7ada-107">Hadoop 串流處理是可讓您使用指令碼或可執行檔 toorun MapReduce 工作的公用程式。</span><span class="sxs-lookup"><span data-stu-id="a7ada-107">Hadoop streaming is a utility that allows you toorun MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="a7ada-108">在此範例中，.NET 是使用的 tooimplement hello 對應工具和減壓器 word 計數解決方案。</span><span class="sxs-lookup"><span data-stu-id="a7ada-108">In this example, .NET is used tooimplement hello mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="a7ada-109">HDInsight 上的 .NET</span><span class="sxs-lookup"><span data-stu-id="a7ada-109">.NET on HDInsight</span></span>

<span data-ttu-id="a7ada-110">__以 Linux 為基礎的 HDInsight__叢集使用[單聲道 (https://mono-project.com)](https://mono-project.com) toorun.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7ada-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="a7ada-111">4.2.1 版的 Mono 隨附於 3.5 版的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="a7ada-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="a7ada-112">多個 hello Mono 隨附 HDInsight 版本的詳細資訊，請參閱[HDInsight 元件版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="a7ada-112">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="a7ada-113">toouse 特定版本的 Mono，請參閱 hello[安裝或更新 Mono](hdinsight-hadoop-install-mono.md)文件。</span><span class="sxs-lookup"><span data-stu-id="a7ada-113">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="a7ada-114">如需 Mono 與 .NET Framework 版本之相容性的詳細資訊，請參閱 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="a7ada-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="a7ada-115">Hadoop 串流的運作方式</span><span class="sxs-lookup"><span data-stu-id="a7ada-115">How Hadoop streaming works</span></span>

<span data-ttu-id="a7ada-116">用於資料流處理本文件中的 hello 基本程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7ada-116">hello basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="a7ada-117">Hadoop，傳遞 STDIN 資料 toohello 對應程式 (在此範例中 mapper.exe)。</span><span class="sxs-lookup"><span data-stu-id="a7ada-117">Hadoop passes data toohello mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="a7ada-118">hello 對應工具處理 hello 資料，並發出 tab 鍵分隔的索引鍵/值組 tooSTDOUT。</span><span class="sxs-lookup"><span data-stu-id="a7ada-118">hello mapper processes hello data, and emits tab-delimited key/value pairs tooSTDOUT.</span></span>
3. <span data-ttu-id="a7ada-119">hello 輸出是由 Hadoop，讀取，然後傳遞 STDIN toohello 減壓器 (reducer.exe 在此範例中)。</span><span class="sxs-lookup"><span data-stu-id="a7ada-119">hello output is read by Hadoop, and then passed toohello reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="a7ada-120">hello 減壓器讀取 hello tab 鍵分隔的索引鍵/值組、 處理 hello 資料，並再發出 hello 結果為 STDOUT 上以 tab 分隔的索引鍵/值組。</span><span class="sxs-lookup"><span data-stu-id="a7ada-120">hello reducer reads hello tab-delimited key/value pairs, processes hello data, and then emits hello result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="a7ada-121">hello 輸出是由 Hadoop 讀取和寫入 toohello 輸出目錄。</span><span class="sxs-lookup"><span data-stu-id="a7ada-121">hello output is read by Hadoop and written toohello output directory.</span></span>

<span data-ttu-id="a7ada-122">如需串流的詳細資訊，請參閱 [Hadoop 串流 (英文) (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)。</span><span class="sxs-lookup"><span data-stu-id="a7ada-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7ada-123">必要條件</span><span class="sxs-lookup"><span data-stu-id="a7ada-123">Prerequisites</span></span>

* <span data-ttu-id="a7ada-124">熟悉如何撰寫和建置以 .NET Framework 4.5 為目標的 C# 程式碼。</span><span class="sxs-lookup"><span data-stu-id="a7ada-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="a7ada-125">此文件使用 Visual Studio 2017 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="a7ada-125">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="a7ada-126">方式 tooupload.exe 檔案 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="a7ada-126">A way tooupload .exe files toohello cluster.</span></span> <span data-ttu-id="a7ada-127">hello 本文件中的步驟使用 hello 資料湖 Tools for Visual Studio tooupload hello 檔案 tooprimary 叢集的存放裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="a7ada-127">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files tooprimary storage for hello cluster.</span></span>

* <span data-ttu-id="a7ada-128">Azure PowerShell 或 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="a7ada-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="a7ada-129">HDInsight 叢集上的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="a7ada-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="a7ada-130">如需有關建立叢集的詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-provision-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="a7ada-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-hello-mapper"></a><span data-ttu-id="a7ada-131">建立 hello 對應程式</span><span class="sxs-lookup"><span data-stu-id="a7ada-131">Create hello mapper</span></span>

<span data-ttu-id="a7ada-132">在 Visual Studio 中，建立名為 __mapper__ 的新__主控台應用程式__。</span><span class="sxs-lookup"><span data-stu-id="a7ada-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="a7ada-133">使用下列 hello 應用程式程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="a7ada-133">Use hello following code for hello application:</span></span>

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

<span data-ttu-id="a7ada-134">在建立之後 hello 應用程式，建立該 tooproduce hello `/bin/Debug/mapper.exe` hello 專案目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="a7ada-134">After creating hello application, build it tooproduce hello `/bin/Debug/mapper.exe` file in hello project directory.</span></span>

## <a name="create-hello-reducer"></a><span data-ttu-id="a7ada-135">建立 hello 減壓器</span><span class="sxs-lookup"><span data-stu-id="a7ada-135">Create hello reducer</span></span>

<span data-ttu-id="a7ada-136">在 Visual Studio 中，建立名為 __reducer__ 的新__主控台應用程式__。</span><span class="sxs-lookup"><span data-stu-id="a7ada-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="a7ada-137">使用下列 hello 應用程式程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="a7ada-137">Use hello following code for hello application:</span></span>

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

<span data-ttu-id="a7ada-138">在建立之後 hello 應用程式，建立該 tooproduce hello `/bin/Debug/reducer.exe` hello 專案目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="a7ada-138">After creating hello application, build it tooproduce hello `/bin/Debug/reducer.exe` file in hello project directory.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="a7ada-139">上傳 toostorage</span><span class="sxs-lookup"><span data-stu-id="a7ada-139">Upload toostorage</span></span>

1. <span data-ttu-id="a7ada-140">在 Visual Studio 中，開啟 [伺服器總管] 。</span><span class="sxs-lookup"><span data-stu-id="a7ada-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="a7ada-141">展開 [Azure]，然後展開 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="a7ada-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="a7ada-142">如果出現提示，請輸入您的 Azure 訂用帳戶認證，然後按一下登入。</span><span class="sxs-lookup"><span data-stu-id="a7ada-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="a7ada-143">展開您想 toodeploy 此應用程式的 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a7ada-143">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="a7ada-144">具有 hello 文字的項目__（預設儲存體帳戶）__列。</span><span class="sxs-lookup"><span data-stu-id="a7ada-144">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![顯示 hello hello 叢集的儲存體帳戶的伺服器總管](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="a7ada-146">您可以展開此項目，如果使用__Azure 儲存體帳戶__為 hello 叢集的預設儲存位置。</span><span class="sxs-lookup"><span data-stu-id="a7ada-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="a7ada-147">tooview hello 上的檔案 hello 預設儲存體 hello 叢集展開 hello 項目，然後按兩下 hello __（預設容器）__。</span><span class="sxs-lookup"><span data-stu-id="a7ada-147">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="a7ada-148">無法展開此項目時，如果您使用__Azure Data Lake Store__為 hello hello 叢集的預設存放裝置。</span><span class="sxs-lookup"><span data-stu-id="a7ada-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="a7ada-149">tooview hello hello 預設儲存體上 hello 叢集檔案，按兩下 hello __（預設儲存體帳戶）__項目。</span><span class="sxs-lookup"><span data-stu-id="a7ada-149">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="a7ada-150">tooupload hello.exe 檔，使用其中一種 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="a7ada-150">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="a7ada-151">如果使用__Azure 儲存體帳戶__、 按一下 hello 上傳 圖示，然後瀏覽 toohello **bin\debug**資料夾 hello**對應工具**專案。</span><span class="sxs-lookup"><span data-stu-id="a7ada-151">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **mapper** project.</span></span> <span data-ttu-id="a7ada-152">最後，選取 hello **mapper.exe**檔案，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="a7ada-152">Finally, select hello **mapper.exe** file and click **Ok**.</span></span>

        ![上傳圖示](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="a7ada-154">如果使用__Azure Data Lake Store__，hello 檔案清單中中的空白區域上按一下滑鼠右鍵，然後選取__上傳__。</span><span class="sxs-lookup"><span data-stu-id="a7ada-154">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="a7ada-155">最後，選取 hello **mapper.exe**檔案，然後按一下 **開啟**。</span><span class="sxs-lookup"><span data-stu-id="a7ada-155">Finally, select hello **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="a7ada-156">一次 hello __mapper.exe__上傳完成時，重複 hello 上傳程序 hello __reducer.exe__檔案。</span><span class="sxs-lookup"><span data-stu-id="a7ada-156">Once hello __mapper.exe__ upload has finished, repeat hello upload process for hello __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="a7ada-157">執行工作︰使用 SSH 工作階段</span><span class="sxs-lookup"><span data-stu-id="a7ada-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="a7ada-158">使用 SSH tooconnect toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a7ada-158">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="a7ada-159">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="a7ada-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="a7ada-160">使用下列命令 toostart hello MapReduce 工作的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="a7ada-160">Use one of hello following command toostart hello MapReduce job:</span></span>

    * <span data-ttu-id="a7ada-161">如果使用 __Data Lake Store__ 作為預設儲存體：</span><span class="sxs-lookup"><span data-stu-id="a7ada-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="a7ada-162">如果使用 __Azure 儲存體__作為預設儲存體：</span><span class="sxs-lookup"><span data-stu-id="a7ada-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="a7ada-163">hello 下列清單說明每個參數的用途：</span><span class="sxs-lookup"><span data-stu-id="a7ada-163">hello following list describes what each parameter does:</span></span>

    * <span data-ttu-id="a7ada-164">`hadoop-streaming.jar`: hello jar 檔案，其中包含 hello 串流 MapReduce 功能。</span><span class="sxs-lookup"><span data-stu-id="a7ada-164">`hadoop-streaming.jar`: hello jar file that contains hello streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="a7ada-165">`-files`： 另加入 hello`mapper.exe`和`reducer.exe`檔案 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="a7ada-165">`-files`: Adds hello `mapper.exe` and `reducer.exe` files toothis job.</span></span> <span data-ttu-id="a7ada-166">hello`adl:///`或`wasb:///`每個檔案是 hello 路徑 toohello 根 hello 叢集的預設儲存體之前。</span><span class="sxs-lookup"><span data-stu-id="a7ada-166">hello `adl:///` or `wasb:///` before each file is hello path toohello root of default storage for hello cluster.</span></span>
    * <span data-ttu-id="a7ada-167">`-mapper`： 指定哪些檔案會實作 hello 對應工具。</span><span class="sxs-lookup"><span data-stu-id="a7ada-167">`-mapper`: Specifies which file implements hello mapper.</span></span>
    * <span data-ttu-id="a7ada-168">`-reducer`： 指定哪些檔案會實作 hello 減壓器。</span><span class="sxs-lookup"><span data-stu-id="a7ada-168">`-reducer`: Specifies which file implements hello reducer.</span></span>
    * <span data-ttu-id="a7ada-169">`-input`: hello 輸入資料。</span><span class="sxs-lookup"><span data-stu-id="a7ada-169">`-input`: hello input data.</span></span>
    * <span data-ttu-id="a7ada-170">`-output`: hello 輸出目錄。</span><span class="sxs-lookup"><span data-stu-id="a7ada-170">`-output`: hello output directory.</span></span>

3. <span data-ttu-id="a7ada-171">Hello MapReduce 工作完成之後，請使用下列 tooview hello 結果 hello:</span><span class="sxs-lookup"><span data-stu-id="a7ada-171">Once hello MapReduce job completes, use hello following tooview hello results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="a7ada-172">hello 下列文字是這個命令所傳回的 hello 資料的範例：</span><span class="sxs-lookup"><span data-stu-id="a7ada-172">hello following text is an example of hello data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="a7ada-173">執行作業：使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7ada-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="a7ada-174">使用下列 PowerShell 指令碼 toorun MapReduce 工作的 hello 和下載 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="a7ada-174">Use hello following PowerShell script toorun a MapReduce job and download hello results.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

<span data-ttu-id="a7ada-175">此指令碼會提示您輸入 hello 叢集登入帳戶名稱和密碼，以及 hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="a7ada-175">This script prompts you for hello cluster login account name and password, along with hello HDInsight cluster name.</span></span> <span data-ttu-id="a7ada-176">Hello 輸出 hello 作業完成之後，會下載的 toohello `output.txt` hello 目錄 hello 指令碼中的檔案從執行。</span><span class="sxs-lookup"><span data-stu-id="a7ada-176">Once hello job completes, hello output is downloaded toohello `output.txt` file in hello directory hello script is ran from.</span></span> <span data-ttu-id="a7ada-177">hello 下列文字是在 hello hello 資料的範例`output.txt`檔案：</span><span class="sxs-lookup"><span data-stu-id="a7ada-177">hello following text is an example of hello data in hello `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="a7ada-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7ada-178">Next steps</span></span>

<span data-ttu-id="a7ada-179">如需搭配 HDInsight 使用 MapReduce 的詳細資訊，請參閱[搭配 HDInsight 使用 MapReduce](hdinsight-use-mapreduce.md)。</span><span class="sxs-lookup"><span data-stu-id="a7ada-179">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="a7ada-180">如需搭配 Hive 與 Pig 使用 C# 的詳細資訊，請參閱[搭配 Hive 與 Pig 使用 C# 使用者定義函式](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="a7ada-180">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="a7ada-181">如需搭配 HDInsight 上的 Storm 使用 C# 的詳細資訊，請參閱[開發適用於 Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="a7ada-181">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>
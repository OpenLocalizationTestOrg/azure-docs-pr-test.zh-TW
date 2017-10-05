---
title: "搭配 HDInsight 的 Hadoop 上的 MapReduce 使用 C# - Azure | Microsoft Docs"
description: "了解如何搭配 Azure HDInsight 的 Hadoop 使用 C# 以建立 MapReduce 方案。"
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
ms.openlocfilehash: adb454e56378a800c671614735aec78b6851aeb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="0e445-103">搭配 HDInsight 的 Hadoop 上的 MapReduce 串流使用 C#</span><span class="sxs-lookup"><span data-stu-id="0e445-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="0e445-104">了解如何使用 C# 在 HDInsight 上建立 MapReduce 方案。</span><span class="sxs-lookup"><span data-stu-id="0e445-104">Learn how to use C# to create a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e445-105">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="0e445-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0e445-106">如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="0e445-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="0e445-107">Hadoop 串流是一個公用程式，可讓您使用指令碼或可執行檔執行 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="0e445-107">Hadoop streaming is a utility that allows you to run MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="0e445-108">在此範例中，.NET 用來實作字數統計方案的對應工具和歸納器。</span><span class="sxs-lookup"><span data-stu-id="0e445-108">In this example, .NET is used to implement the mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="0e445-109">HDInsight 上的 .NET</span><span class="sxs-lookup"><span data-stu-id="0e445-109">.NET on HDInsight</span></span>

<span data-ttu-id="0e445-110">__以 Linux 為基礎的 HDInsight__ 叢集使用 [Mono (https://mono-project.com)](https://mono-project.com) 來執行 .NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e445-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="0e445-111">4.2.1 版的 Mono 隨附於 3.5 版的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="0e445-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="0e445-112">如需 HDInsight 包含之 Mono 版本的詳細資訊，請參閱 [HDInsight 元件版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="0e445-112">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="0e445-113">若要使用特定版本的 Mono，請參閱[安裝或更新 Mono](hdinsight-hadoop-install-mono.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="0e445-113">To use a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="0e445-114">如需 Mono 與 .NET Framework 版本之相容性的詳細資訊，請參閱 [Mono 相容性 (英文)](http://www.mono-project.com/docs/about-mono/compatibility/)。</span><span class="sxs-lookup"><span data-stu-id="0e445-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="0e445-115">Hadoop 串流的運作方式</span><span class="sxs-lookup"><span data-stu-id="0e445-115">How Hadoop streaming works</span></span>

<span data-ttu-id="0e445-116">本文件中使用於串流的基本程序如下︰</span><span class="sxs-lookup"><span data-stu-id="0e445-116">The basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="0e445-117">Hadoop 在 STDIN 上將資料傳遞至對應工具 (在此範例中是 mapper.exe)。</span><span class="sxs-lookup"><span data-stu-id="0e445-117">Hadoop passes data to the mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="0e445-118">對應工具會處理資料，然後發出以 Tab 分隔的機碼值組到 STDOUT。</span><span class="sxs-lookup"><span data-stu-id="0e445-118">The mapper processes the data, and emits tab-delimited key/value pairs to STDOUT.</span></span>
3. <span data-ttu-id="0e445-119">Hadoop 會讀取輸出，接著輸出會在 STDIN 上傳遞至歸納器 (在此範例中是 reducer.exe)。</span><span class="sxs-lookup"><span data-stu-id="0e445-119">The output is read by Hadoop, and then passed to the reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="0e445-120">歸納器會讀取以 Tab 分隔的機碼值組、處理資料，然後在 STDOUT 發出以 Tab 分隔的機碼值組格式結果。</span><span class="sxs-lookup"><span data-stu-id="0e445-120">The reducer reads the tab-delimited key/value pairs, processes the data, and then emits the result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="0e445-121">Hadoop 會讀取輸出，接著輸出會寫入至輸出目錄。</span><span class="sxs-lookup"><span data-stu-id="0e445-121">The output is read by Hadoop and written to the output directory.</span></span>

<span data-ttu-id="0e445-122">如需串流的詳細資訊，請參閱 [Hadoop 串流 (英文) (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)。</span><span class="sxs-lookup"><span data-stu-id="0e445-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e445-123">必要條件</span><span class="sxs-lookup"><span data-stu-id="0e445-123">Prerequisites</span></span>

* <span data-ttu-id="0e445-124">熟悉如何撰寫和建置以 .NET Framework 4.5 為目標的 C# 程式碼。</span><span class="sxs-lookup"><span data-stu-id="0e445-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="0e445-125">本文件中的步驟使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="0e445-125">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="0e445-126">將 .exe 檔案上傳至叢集的方式。</span><span class="sxs-lookup"><span data-stu-id="0e445-126">A way to upload .exe files to the cluster.</span></span> <span data-ttu-id="0e445-127">本文件中的步驟使用 Data Lake Tools for Visual Studio 將檔案上傳至叢集的主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="0e445-127">The steps in this document use the Data Lake Tools for Visual Studio to upload the files to primary storage for the cluster.</span></span>

* <span data-ttu-id="0e445-128">Azure PowerShell 或 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="0e445-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="0e445-129">HDInsight 叢集上的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="0e445-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="0e445-130">如需有關建立叢集的詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-provision-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="0e445-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-the-mapper"></a><span data-ttu-id="0e445-131">建立對應工具</span><span class="sxs-lookup"><span data-stu-id="0e445-131">Create the mapper</span></span>

<span data-ttu-id="0e445-132">在 Visual Studio 中，建立名為 __mapper__ 的新__主控台應用程式__。</span><span class="sxs-lookup"><span data-stu-id="0e445-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="0e445-133">針對此應用程式使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="0e445-133">Use the following code for the application:</span></span>

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
            //Hadoop passes data to the mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over the words
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

<span data-ttu-id="0e445-134">建立應用程式之後，建置它以在專案目錄中產生 `/bin/Debug/mapper.exe` 檔案。</span><span class="sxs-lookup"><span data-stu-id="0e445-134">After creating the application, build it to produce the `/bin/Debug/mapper.exe` file in the project directory.</span></span>

## <a name="create-the-reducer"></a><span data-ttu-id="0e445-135">建立歸納器</span><span class="sxs-lookup"><span data-stu-id="0e445-135">Create the reducer</span></span>

<span data-ttu-id="0e445-136">在 Visual Studio 中，建立名為 __reducer__ 的新__主控台應用程式__。</span><span class="sxs-lookup"><span data-stu-id="0e445-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="0e445-137">針對此應用程式使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="0e445-137">Use the following code for the application:</span></span>

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
                // Get the word
                string word = sArr[0];
                // Get the count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for the word?
                if(words.ContainsKey(word))
                {
                    //If so, increment the count
                    words[word] += count;
                } else
                {
                    //Add the key to the collection
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

<span data-ttu-id="0e445-138">建立應用程式之後，建置它以在專案目錄中產生 `/bin/Debug/reducer.exe` 檔案。</span><span class="sxs-lookup"><span data-stu-id="0e445-138">After creating the application, build it to produce the `/bin/Debug/reducer.exe` file in the project directory.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="0e445-139">上傳至儲存體</span><span class="sxs-lookup"><span data-stu-id="0e445-139">Upload to storage</span></span>

1. <span data-ttu-id="0e445-140">在 Visual Studio 中，開啟 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="0e445-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="0e445-141">展開 [Azure]，然後展開 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="0e445-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="0e445-142">如果出現提示，請輸入您的 Azure 訂用帳戶認證，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="0e445-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="0e445-143">展開您要部署此應用程式的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0e445-143">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="0e445-144">就會列出含有文字 __(預設儲存體帳戶)__ 的項目。</span><span class="sxs-lookup"><span data-stu-id="0e445-144">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![顯示叢集之儲存體帳戶的 [伺服器總管]](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="0e445-146">如果此項目可以展開，表示您是使用 __Azure 儲存體帳戶__作為叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="0e445-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="0e445-147">若要檢視叢集之預設儲存體上的檔案，請展開項目，然後按兩下 [(預設容器)]。</span><span class="sxs-lookup"><span data-stu-id="0e445-147">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="0e445-148">如果此項目無法展開，表示您是使用 __Azure Data Lake Store__ 作為叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="0e445-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="0e445-149">若要檢視叢集之預設儲存體上的檔案，請按兩下 [(預設儲存體帳戶)] 項目。</span><span class="sxs-lookup"><span data-stu-id="0e445-149">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="0e445-150">若要上傳 .exe 檔案，請使用下列其中一種方法：</span><span class="sxs-lookup"><span data-stu-id="0e445-150">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="0e445-151">如果使用 __Azure 儲存體帳戶__，請按一下上傳圖示，然後瀏覽至 **mapper** 專案的 **bin\debug** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0e445-151">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **mapper** project.</span></span> <span data-ttu-id="0e445-152">最後，選取 **mapper.exe** 檔案，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0e445-152">Finally, select the **mapper.exe** file and click **Ok**.</span></span>

        ![上傳圖示](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="0e445-154">如果使用 __Azure Data Lake Store__，請以滑鼠右鍵按一下檔案清單中的空白區域，然後選取 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="0e445-154">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="0e445-155">最後，選取 **mapper.exe** 檔案，然後按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="0e445-155">Finally, select the **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="0e445-156">__mapper.exe__ 上傳完成後，請針對 __reducer.exe__ 檔案重複上傳程序。</span><span class="sxs-lookup"><span data-stu-id="0e445-156">Once the __mapper.exe__ upload has finished, repeat the upload process for the __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="0e445-157">執行工作︰使用 SSH 工作階段</span><span class="sxs-lookup"><span data-stu-id="0e445-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="0e445-158">使用 SSH 連接到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0e445-158">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="0e445-159">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="0e445-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="0e445-160">使用下列其中一個命令來啟動 MapReduce 作業：</span><span class="sxs-lookup"><span data-stu-id="0e445-160">Use one of the following command to start the MapReduce job:</span></span>

    * <span data-ttu-id="0e445-161">如果使用 __Data Lake Store__ 作為預設儲存體：</span><span class="sxs-lookup"><span data-stu-id="0e445-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="0e445-162">如果使用 __Azure 儲存體__作為預設儲存體：</span><span class="sxs-lookup"><span data-stu-id="0e445-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="0e445-163">下列清單描述每個參數的用途︰</span><span class="sxs-lookup"><span data-stu-id="0e445-163">The following list describes what each parameter does:</span></span>

    * <span data-ttu-id="0e445-164">`hadoop-streaming.jar`︰包含串流處理 MapReduce 功能的 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="0e445-164">`hadoop-streaming.jar`: The jar file that contains the streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="0e445-165">`-files`︰將 `mapper.exe` 和 `reducer.exe` 檔案加入至此作業。</span><span class="sxs-lookup"><span data-stu-id="0e445-165">`-files`: Adds the `mapper.exe` and `reducer.exe` files to this job.</span></span> <span data-ttu-id="0e445-166">每個檔案前面的 `adl:///` 或 `wasb:///` 是叢集的預設儲存體根目錄路徑。</span><span class="sxs-lookup"><span data-stu-id="0e445-166">The `adl:///` or `wasb:///` before each file is the path to the root of default storage for the cluster.</span></span>
    * <span data-ttu-id="0e445-167">`-mapper`︰指定哪個檔案實作對應工具。</span><span class="sxs-lookup"><span data-stu-id="0e445-167">`-mapper`: Specifies which file implements the mapper.</span></span>
    * <span data-ttu-id="0e445-168">`-reducer`︰指定哪個檔案實作歸納器。</span><span class="sxs-lookup"><span data-stu-id="0e445-168">`-reducer`: Specifies which file implements the reducer.</span></span>
    * <span data-ttu-id="0e445-169">`-input`：輸入資料。</span><span class="sxs-lookup"><span data-stu-id="0e445-169">`-input`: The input data.</span></span>
    * <span data-ttu-id="0e445-170">`-output`︰輸出目錄。</span><span class="sxs-lookup"><span data-stu-id="0e445-170">`-output`: The output directory.</span></span>

3. <span data-ttu-id="0e445-171">在 MapReduce 作業完成後，使用下列命令來檢視結果：</span><span class="sxs-lookup"><span data-stu-id="0e445-171">Once the MapReduce job completes, use the following to view the results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="0e445-172">下列文字是此命令所傳回資料的範例︰</span><span class="sxs-lookup"><span data-stu-id="0e445-172">The following text is an example of the data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="0e445-173">執行作業：使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e445-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="0e445-174">使用下列 PowerShell 指令碼來執行 MapReduce 作業並下載結果。</span><span class="sxs-lookup"><span data-stu-id="0e445-174">Use the following PowerShell script to run a MapReduce job and download the results.</span></span>

<span data-ttu-id="0e445-175">[!code-powershell[主要](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span><span class="sxs-lookup"><span data-stu-id="0e445-175">[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span></span>

<span data-ttu-id="0e445-176">此指令碼會提示您輸入叢集登入帳戶名稱和密碼，以及 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="0e445-176">This script prompts you for the cluster login account name and password, along with the HDInsight cluster name.</span></span> <span data-ttu-id="0e445-177">完成工作時，會將輸出下載到此指令碼執行所在目錄中的 `output.txt` 檔案。</span><span class="sxs-lookup"><span data-stu-id="0e445-177">Once the job completes, the output is downloaded to the `output.txt` file in the directory the script is ran from.</span></span> <span data-ttu-id="0e445-178">以下文字是 `output.txt` 檔案中的資料範例：</span><span class="sxs-lookup"><span data-stu-id="0e445-178">The following text is an example of the data in the `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="0e445-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e445-179">Next steps</span></span>

<span data-ttu-id="0e445-180">如需搭配 HDInsight 使用 MapReduce 的詳細資訊，請參閱[搭配 HDInsight 使用 MapReduce](hdinsight-use-mapreduce.md)。</span><span class="sxs-lookup"><span data-stu-id="0e445-180">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="0e445-181">如需搭配 Hive 與 Pig 使用 C# 的詳細資訊，請參閱[搭配 Hive 與 Pig 使用 C# 使用者定義函式](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="0e445-181">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="0e445-182">如需搭配 HDInsight 上的 Storm 使用 C# 的詳細資訊，請參閱[開發適用於 Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="0e445-182">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>
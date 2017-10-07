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
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="a26e8-103">搭配使用 C# 使用者定義函數與 HDInsight 的 Hadoop 上的 Hive 和 Pig 串流處理。</span><span class="sxs-lookup"><span data-stu-id="a26e8-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="a26e8-104">了解 toouse C# 使用者定義函數 (UDF) 與 Apache Hive 和 Pig HDInsight 上的方式。</span><span class="sxs-lookup"><span data-stu-id="a26e8-104">Learn how toouse C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a26e8-105">本文件中的 hello 步驟使用 linux 和 Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a26e8-105">hello steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="a26e8-106">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="a26e8-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a26e8-107">如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="a26e8-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="a26e8-108">兩者的 Hive 和 Pig 可以將資料 tooexternal 應用程式進行處理傳遞。</span><span class="sxs-lookup"><span data-stu-id="a26e8-108">Both Hive and Pig can pass data tooexternal applications for processing.</span></span> <span data-ttu-id="a26e8-109">這個程序稱為_串流處理_。</span><span class="sxs-lookup"><span data-stu-id="a26e8-109">This process is known as _streaming_.</span></span> <span data-ttu-id="a26e8-110">Hello 資料時使用.NET 應用程式，會傳遞 toohello 應用程式上 STDIN、 並 hello 應用程式傳回 hello 結果 STDOUT 上。</span><span class="sxs-lookup"><span data-stu-id="a26e8-110">When using a .NET applciation, hello data is passed toohello application on STDIN, and hello application returns hello results on STDOUT.</span></span> <span data-ttu-id="a26e8-111">tooread 以及來自 STDIN 和 STDOUT 寫入，您可以使用`Console.ReadLine()`和`Console.WriteLine()`從主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a26e8-111">tooread and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a26e8-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="a26e8-112">Prerequisites</span></span>

* <span data-ttu-id="a26e8-113">熟悉如何撰寫和建置以 .NET Framework 4.5 為目標的 C# 程式碼。</span><span class="sxs-lookup"><span data-stu-id="a26e8-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="a26e8-114">使用您想要的任何 IDE。</span><span class="sxs-lookup"><span data-stu-id="a26e8-114">Use whatever IDE you want.</span></span> <span data-ttu-id="a26e8-115">建議您使用 [Visual Studio](https://www.visualstudio.com/vs) 2015、2017 或 [Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="a26e8-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="a26e8-116">此文件使用 Visual Studio 2017 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="a26e8-116">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="a26e8-117">方式 tooupload.exe 檔案 toohello 叢集並執行的 Pig 和 Hive 工作。</span><span class="sxs-lookup"><span data-stu-id="a26e8-117">A way tooupload .exe files toohello cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="a26e8-118">我們建議 Visual Studio、 Azure PowerShell 和 Azure CLI hello 資料湖工具。</span><span class="sxs-lookup"><span data-stu-id="a26e8-118">We recommend hello Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="a26e8-119">hello 本文件中的步驟使用 hello 資料湖 Tools for Visual Studio tooupload hello 檔案並執行 hello 範例 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="a26e8-119">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files and run hello example Hive query.</span></span>

    <span data-ttu-id="a26e8-120">其他方式 toorun Hive 查詢和 Pig 工作上的資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="a26e8-120">For information on other ways toorun Hive queries and Pig jobs, see hello following documents:</span></span>

    * [<span data-ttu-id="a26e8-121">搭配 HDInsight 使用 Apache Hive</span><span class="sxs-lookup"><span data-stu-id="a26e8-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="a26e8-122">搭配 HDInsight 使用 Apache Pig</span><span class="sxs-lookup"><span data-stu-id="a26e8-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="a26e8-123">HDInsight 叢集上的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="a26e8-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="a26e8-124">如需有關建立叢集的詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-provision-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="a26e8-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="a26e8-125">HDInsight 上的 .NET</span><span class="sxs-lookup"><span data-stu-id="a26e8-125">.NET on HDInsight</span></span>

* <span data-ttu-id="a26e8-126">__以 Linux 為基礎的 HDInsight__使用叢集[單聲道 (https://mono-project.com)](https://mono-project.com) toorun.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a26e8-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="a26e8-127">4.2.1 版的 Mono 隨附於 3.5 版的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="a26e8-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="a26e8-128">如需 Mono 與 .NET Framework 版本之相容性的詳細資訊，請參閱 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="a26e8-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="a26e8-129">toouse 特定版本的 Mono，請參閱 hello[安裝或更新 Mono](hdinsight-hadoop-install-mono.md)文件。</span><span class="sxs-lookup"><span data-stu-id="a26e8-129">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="a26e8-130">__Windows 為基礎的 HDInsight__叢集使用 hello Microsoft.NET CLR toorun.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a26e8-130">__Windows-based HDInsight__ clusters use hello Microsoft .NET CLR toorun .NET applications.</span></span>

<span data-ttu-id="a26e8-131">如需有關 hello hello.NET framework 版本和 Mono HDInsight 版本所隨附的詳細資訊，請參閱[HDInsight 元件版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="a26e8-131">For more information on hello version of hello .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-hello-c-projects"></a><span data-ttu-id="a26e8-132">建立 hello C\#專案</span><span class="sxs-lookup"><span data-stu-id="a26e8-132">Create hello C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="a26e8-133">Hive UDF</span><span class="sxs-lookup"><span data-stu-id="a26e8-133">Hive UDF</span></span>

1. <span data-ttu-id="a26e8-134">開啟 Visual Studio 並建立方案。</span><span class="sxs-lookup"><span data-stu-id="a26e8-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="a26e8-135">Hello 專案類型 選取**主控台應用程式 (.NET Framework)**，和名稱 hello 新專案**HiveCSharp**。</span><span class="sxs-lookup"><span data-stu-id="a26e8-135">For hello project type, select **Console App (.NET Framework)**, and name hello new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a26e8-136">如果您使用以 Linux 為基礎的 HDInsight 叢集，請選取 __.NET Framework 4.5__。</span><span class="sxs-lookup"><span data-stu-id="a26e8-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a26e8-137">如需 Mono 與 .NET Framework 版本之相容性的詳細資訊，請參閱 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="a26e8-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="a26e8-138">取代 hello 內容**Program.cs** hello 下列：</span><span class="sxs-lookup"><span data-stu-id="a26e8-138">Replace hello contents of **Program.cs** with hello following:</span></span>

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

3. <span data-ttu-id="a26e8-139">建置 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="a26e8-139">Build hello project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="a26e8-140">Pig UDF</span><span class="sxs-lookup"><span data-stu-id="a26e8-140">Pig UDF</span></span>

1. <span data-ttu-id="a26e8-141">開啟 Visual Studio 並建立方案。</span><span class="sxs-lookup"><span data-stu-id="a26e8-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="a26e8-142">Hello 專案類型 選取**主控台應用程式**，和名稱 hello 新專案**PigUDF**。</span><span class="sxs-lookup"><span data-stu-id="a26e8-142">For hello project type, select **Console Application**, and name hello new project **PigUDF**.</span></span>

2. <span data-ttu-id="a26e8-143">取代 hello hello 內容**Program.cs**檔案以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="a26e8-143">Replace hello contents of hello **Program.cs** file with hello following code:</span></span>

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

    <span data-ttu-id="a26e8-144">此應用程式剖析 Pig，從傳送 hello 線條和重新格式化線條的開頭`java.lang.Exception`。</span><span class="sxs-lookup"><span data-stu-id="a26e8-144">This application parses hello lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="a26e8-145">儲存**Program.cs**，然後建置 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="a26e8-145">Save **Program.cs**, and then build hello project.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="a26e8-146">上傳 toostorage</span><span class="sxs-lookup"><span data-stu-id="a26e8-146">Upload toostorage</span></span>

1. <span data-ttu-id="a26e8-147">在 Visual Studio 中，開啟 [伺服器總管] 。</span><span class="sxs-lookup"><span data-stu-id="a26e8-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="a26e8-148">展開 [Azure]，然後展開 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="a26e8-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="a26e8-149">如果出現提示，請輸入您的 Azure 訂用帳戶認證，然後按一下登入。</span><span class="sxs-lookup"><span data-stu-id="a26e8-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="a26e8-150">展開您想 toodeploy 此應用程式的 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a26e8-150">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="a26e8-151">具有 hello 文字的項目__（預設儲存體帳戶）__列。</span><span class="sxs-lookup"><span data-stu-id="a26e8-151">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![顯示 hello hello 叢集的儲存體帳戶的伺服器總管](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="a26e8-153">您可以展開此項目，如果使用__Azure 儲存體帳戶__為 hello 叢集的預設儲存位置。</span><span class="sxs-lookup"><span data-stu-id="a26e8-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="a26e8-154">tooview hello 上的檔案 hello 預設儲存體 hello 叢集展開 hello 項目，然後按兩下 hello __（預設容器）__。</span><span class="sxs-lookup"><span data-stu-id="a26e8-154">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="a26e8-155">無法展開此項目時，如果您使用__Azure Data Lake Store__為 hello hello 叢集的預設存放裝置。</span><span class="sxs-lookup"><span data-stu-id="a26e8-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="a26e8-156">tooview hello hello 預設儲存體上 hello 叢集檔案，按兩下 hello __（預設儲存體帳戶）__項目。</span><span class="sxs-lookup"><span data-stu-id="a26e8-156">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="a26e8-157">tooupload hello.exe 檔，使用其中一種 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="a26e8-157">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="a26e8-158">如果使用__Azure 儲存體帳戶__、 按一下 hello 上傳 圖示，然後瀏覽 toohello **bin\debug**資料夾 hello **HiveCSharp**專案。</span><span class="sxs-lookup"><span data-stu-id="a26e8-158">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **HiveCSharp** project.</span></span> <span data-ttu-id="a26e8-159">最後，選取 hello **HiveCSharp.exe**檔案，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="a26e8-159">Finally, select hello **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![上傳圖示](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="a26e8-161">如果使用__Azure Data Lake Store__，hello 檔案清單中中的空白區域上按一下滑鼠右鍵，然後選取__上傳__。</span><span class="sxs-lookup"><span data-stu-id="a26e8-161">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="a26e8-162">最後，選取 hello **HiveCSharp.exe**檔案，然後按一下 **開啟**。</span><span class="sxs-lookup"><span data-stu-id="a26e8-162">Finally, select hello **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="a26e8-163">一次 hello __HiveCSharp.exe__上傳完成時，重複 hello 上傳程序 hello __PigUDF.exe__檔案。</span><span class="sxs-lookup"><span data-stu-id="a26e8-163">Once hello __HiveCSharp.exe__ upload has finished, repeat hello upload process for hello __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="a26e8-164">執行 HIVE 查詢</span><span class="sxs-lookup"><span data-stu-id="a26e8-164">Run a Hive query</span></span>

1. <span data-ttu-id="a26e8-165">在 Visual Studio 中，開啟 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="a26e8-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="a26e8-166">展開 [Azure]，然後展開 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="a26e8-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="a26e8-167">以滑鼠右鍵按一下您所部署的 hello 的 hello 叢集**HiveCSharp** ，應用程式，然後選取**撰寫 Hive 查詢**。</span><span class="sxs-lookup"><span data-stu-id="a26e8-167">Right-click hello cluster that you deployed hello **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="a26e8-168">使用下列 hello Hive 查詢的文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="a26e8-168">Use hello following text for hello Hive query:</span></span>

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
    > <span data-ttu-id="a26e8-169">請取消註解 hello`add file`用於您叢集的預設儲存體 hello 型別對應的陳述式。</span><span class="sxs-lookup"><span data-stu-id="a26e8-169">Uncomment hello `add file` statement that matches hello type of default storage used for your cluster.</span></span>

    <span data-ttu-id="a26e8-170">此查詢會選取 hello `clientid`， `devicemake`，和`devicemodel`欄位從`hivesampletable`，並傳遞 hello 欄位 toohello HiveCSharp.exe 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a26e8-170">This query selects hello `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes hello fields toohello HiveCSharp.exe application.</span></span> <span data-ttu-id="a26e8-171">hello 查詢必須要有 hello 應用程式 tooreturn 三個欄位，它儲存為`clientid`， `phoneLabel`，和`phoneHash`。</span><span class="sxs-lookup"><span data-stu-id="a26e8-171">hello query expects hello application tooreturn three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="a26e8-172">hello 查詢也必須要有 toofind HiveCSharp.exe hello hello 預設儲存體容器的根目錄中。</span><span class="sxs-lookup"><span data-stu-id="a26e8-172">hello query also expects toofind HiveCSharp.exe in hello root of hello default storage container.</span></span>

5. <span data-ttu-id="a26e8-173">按一下**送出**toosubmit hello 作業 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a26e8-173">Click **Submit** toosubmit hello job toohello HDInsight cluster.</span></span> <span data-ttu-id="a26e8-174">hello **Hive 工作摘要**視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="a26e8-174">hello **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="a26e8-175">按一下**重新整理**toorefresh hello 摘要直到**作業狀態**變更太**已完成**。</span><span class="sxs-lookup"><span data-stu-id="a26e8-175">Click **Refresh** toorefresh hello summary until **Job Status** changes too**Completed**.</span></span> <span data-ttu-id="a26e8-176">tooview hello 作業輸出，按一下**作業輸出**。</span><span class="sxs-lookup"><span data-stu-id="a26e8-176">tooview hello job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="a26e8-177">執行 Pig 作業</span><span class="sxs-lookup"><span data-stu-id="a26e8-177">Run a Pig job</span></span>

1. <span data-ttu-id="a26e8-178">請使用下列方法 tooconnect tooyour HDInsight 叢集的 hello:</span><span class="sxs-lookup"><span data-stu-id="a26e8-178">Use one of hello following methods tooconnect tooyour HDInsight cluster:</span></span>

    * <span data-ttu-id="a26e8-179">如果您使用__以 Linux 為基礎的__ HDInsight 叢集，請使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="a26e8-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="a26e8-180">例如，`ssh sshuser@mycluster-ssh.azurehdinsight.net`。</span><span class="sxs-lookup"><span data-stu-id="a26e8-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="a26e8-181">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="a26e8-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="a26e8-182">如果您使用__windows__ HDInsight 叢集[使用遠端桌面連線 toohello 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="a26e8-182">If you are using a __Windows-based__ HDInsight cluster, [Connect toohello cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="a26e8-183">使用下列命令 toostart hello Pig 命令列的一個 hello:</span><span class="sxs-lookup"><span data-stu-id="a26e8-183">Use one hello following command toostart hello Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="a26e8-184">如果您使用 Windows 叢集，請使用 hello 改用下列命令：</span><span class="sxs-lookup"><span data-stu-id="a26e8-184">If you are using a Windows-based cluster, use hello following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="a26e8-185">`grunt>` 提示隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="a26e8-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="a26e8-186">輸入 hello 遵循 toorun hello.NET Framework 應用程式會使用 Pig 工作：</span><span class="sxs-lookup"><span data-stu-id="a26e8-186">Enter hello following toorun a Pig job that uses hello .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="a26e8-187">hello`DEFINE`陳述式會建立別名`streamer`hello pigudf.exe 應用程式，以及`CACHE`載入從 hello 叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="a26e8-187">hello `DEFINE` statement creates an alias of `streamer` for hello pigudf.exe applications, and `CACHE` loads it from default storage for hello cluster.</span></span> <span data-ttu-id="a26e8-188">稍後，`streamer`搭配 hello`STREAM`運算子 tooprocess hello 為一系列的資料行包含在記錄檔和傳回 hello 資料的單一線條。</span><span class="sxs-lookup"><span data-stu-id="a26e8-188">Later, `streamer` is used with hello `STREAM` operator tooprocess hello single lines contained in LOG and return hello data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a26e8-189">用在資料流的 hello 應用程式名稱必須以 hello 括住\`（單引號） 字元時別名，以及 ' （單引號） 搭配使用時`SHIP\`。</span><span class="sxs-lookup"><span data-stu-id="a26e8-189">hello application name that is used for streaming must be surrounded by hello \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="a26e8-190">輸入 hello 最後一行之後, 應該啟動 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="a26e8-190">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="a26e8-191">它會傳回輸出類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="a26e8-191">It returns output similar toohello following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="a26e8-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a26e8-192">Next steps</span></span>

<span data-ttu-id="a26e8-193">在本文件中，您已經學會如何 toouse 從 Hive 和 Pig HDInsight 上的.NET Framework 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a26e8-193">In this document, you have learned how toouse a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="a26e8-194">如果您想要如何 toouse Python 用於 Hive 和 Pig，請參閱的 toolearn[將 Python 用於 Hive 和 Pig HDInsight 中的](hdinsight-python.md)。</span><span class="sxs-lookup"><span data-stu-id="a26e8-194">If you would like toolearn how toouse Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="a26e8-195">其他的方式 toouse Pig 和 Hive 和有關使用 MapReduce toolearn，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="a26e8-195">For other ways toouse Pig and Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="a26e8-196">搭配 HDInsight 使用 Hivet</span><span class="sxs-lookup"><span data-stu-id="a26e8-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a26e8-197">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="a26e8-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="a26e8-198">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="a26e8-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

---
title: "搭配使用 C# 與 HDInsight 的 Hadoop 上的 Hive 和 Pig - Azure | Microsoft Docs"
description: "了解如何搭配使用 C# 使用者定義函數 (UDF) 與 Azure HDInsight 中的 Hive 和 Pig 串流處理。"
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
ms.openlocfilehash: 58e7af47be71c3e0389e5fb4641e124eb648494e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="03196-103">搭配使用 C# 使用者定義函數與 HDInsight 的 Hadoop 上的 Hive 和 Pig 串流處理。</span><span class="sxs-lookup"><span data-stu-id="03196-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="03196-104">了解如何搭配使用 C# 使用者定義函數 (UDF) 與 HDInsight 上的 Apache Hive 和 Pig。</span><span class="sxs-lookup"><span data-stu-id="03196-104">Learn how to use C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="03196-105">本文件中的步驟適用於以 Linux 為基礎和以 Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="03196-105">The steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="03196-106">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="03196-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="03196-107">如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="03196-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="03196-108">Hive 和 Pig 都可以將資料傳遞至外部應用程式進行處理。</span><span class="sxs-lookup"><span data-stu-id="03196-108">Both Hive and Pig can pass data to external applications for processing.</span></span> <span data-ttu-id="03196-109">這個程序稱為_串流處理_。</span><span class="sxs-lookup"><span data-stu-id="03196-109">This process is known as _streaming_.</span></span> <span data-ttu-id="03196-110">使用 .NET 應用程式時，資料會在 STDIN 上傳遞至應用程式，而應用程式會在 STDOUT 上傳回結果。</span><span class="sxs-lookup"><span data-stu-id="03196-110">When using a .NET applciation, the data is passed to the application on STDIN, and the application returns the results on STDOUT.</span></span> <span data-ttu-id="03196-111">為了在 STDIN 和 STDOUT 讀取和寫入，您可以從主控台應用程式使用 `Console.ReadLine()` 和 `Console.WriteLine()`。</span><span class="sxs-lookup"><span data-stu-id="03196-111">To read and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03196-112">先決條件</span><span class="sxs-lookup"><span data-stu-id="03196-112">Prerequisites</span></span>

* <span data-ttu-id="03196-113">熟悉如何撰寫和建置以 .NET Framework 4.5 為目標的 C# 程式碼。</span><span class="sxs-lookup"><span data-stu-id="03196-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="03196-114">使用您想要的任何 IDE。</span><span class="sxs-lookup"><span data-stu-id="03196-114">Use whatever IDE you want.</span></span> <span data-ttu-id="03196-115">建議您使用 [Visual Studio](https://www.visualstudio.com/vs) 2015、2017 或 [Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="03196-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="03196-116">本文件中的步驟使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="03196-116">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="03196-117">將 .exe 檔案上傳至叢集並執行 Pig 和 Hive 作業所採取的方式。</span><span class="sxs-lookup"><span data-stu-id="03196-117">A way to upload .exe files to the cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="03196-118">建議使用 Data Lake Tools for Visual Studio、Azure PowerShell 和 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="03196-118">We recommend the Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="03196-119">本文件中的步驟使用 Data Lake Tools for Visual Studio 上傳檔案並執行範例 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="03196-119">The steps in this document use the Data Lake Tools for Visual Studio to upload the files and run the example Hive query.</span></span>

    <span data-ttu-id="03196-120">如需執行 Hive 查詢和 Pig 作業之其他方式的詳細資訊，請參閱下列文件︰</span><span class="sxs-lookup"><span data-stu-id="03196-120">For information on other ways to run Hive queries and Pig jobs, see the following documents:</span></span>

    * [<span data-ttu-id="03196-121">搭配 HDInsight 使用 Apache Hive</span><span class="sxs-lookup"><span data-stu-id="03196-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="03196-122">搭配 HDInsight 使用 Apache Pig</span><span class="sxs-lookup"><span data-stu-id="03196-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="03196-123">HDInsight 叢集上的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="03196-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="03196-124">如需有關建立叢集的詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-provision-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="03196-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="03196-125">HDInsight 上的 .NET</span><span class="sxs-lookup"><span data-stu-id="03196-125">.NET on HDInsight</span></span>

* <span data-ttu-id="03196-126">__以 Linux 為基礎的 HDInsight__ 叢集使用 [Mono (https://mono-project.com)](https://mono-project.com) 來執行 .NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="03196-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="03196-127">4.2.1 版的 Mono 隨附於 3.5 版的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="03196-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="03196-128">如需 Mono 與 .NET Framework 版本之相容性的詳細資訊，請參閱 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="03196-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="03196-129">若要使用特定版本的 Mono，請參閱[安裝或更新 Mono](hdinsight-hadoop-install-mono.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="03196-129">To use a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="03196-130">__以 Windows 為基礎的 HDInsight__ 叢集使用 Microsoft.NET CLR 來執行.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="03196-130">__Windows-based HDInsight__ clusters use the Microsoft .NET CLR to run .NET applications.</span></span>

<span data-ttu-id="03196-131">如需 HDInsight 版本包含之 .NET Framework 和 Mono 版本的詳細資訊，請參閱 [HDInsight 元件版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="03196-131">For more information on the version of the .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-the-c-projects"></a><span data-ttu-id="03196-132">建立 C\# 專案</span><span class="sxs-lookup"><span data-stu-id="03196-132">Create the C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="03196-133">Hive UDF</span><span class="sxs-lookup"><span data-stu-id="03196-133">Hive UDF</span></span>

1. <span data-ttu-id="03196-134">開啟 Visual Studio 並建立方案。</span><span class="sxs-lookup"><span data-stu-id="03196-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="03196-135">在專案類型中選取 [主控台應用程式 (.NET Framework)]，然後將新專案命名為 **HiveCSharp**。</span><span class="sxs-lookup"><span data-stu-id="03196-135">For the project type, select **Console App (.NET Framework)**, and name the new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="03196-136">如果您使用以 Linux 為基礎的 HDInsight 叢集，請選取 __.NET Framework 4.5__。</span><span class="sxs-lookup"><span data-stu-id="03196-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="03196-137">如需 Mono 與 .NET Framework 版本之相容性的詳細資訊，請參閱 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="03196-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="03196-138">使用下列程式碼取代 **Program.cs** 的內容：</span><span class="sxs-lookup"><span data-stu-id="03196-138">Replace the contents of **Program.cs** with the following:</span></span>

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
                    // Parse the string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data to stdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for the given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array to hex string
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

3. <span data-ttu-id="03196-139">建置專案。</span><span class="sxs-lookup"><span data-stu-id="03196-139">Build the project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="03196-140">Pig UDF</span><span class="sxs-lookup"><span data-stu-id="03196-140">Pig UDF</span></span>

1. <span data-ttu-id="03196-141">開啟 Visual Studio 並建立方案。</span><span class="sxs-lookup"><span data-stu-id="03196-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="03196-142">在專案類型中選取 [主控台應用程式]，然後將新專案命名為 **PigUDF**。</span><span class="sxs-lookup"><span data-stu-id="03196-142">For the project type, select **Console Application**, and name the new project **PigUDF**.</span></span>

2. <span data-ttu-id="03196-143">使用下列程式碼取代 **Program.cs** 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="03196-143">Replace the contents of the **Program.cs** file with the following code:</span></span>

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
                        // Trim the error info off the beginning and add a note to the end of the line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split the fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    <span data-ttu-id="03196-144">此應用程式將剖析 Pig 送出的程式碼行，並將其重新格式化為以 `java.lang.Exception` 開頭的程式碼行。</span><span class="sxs-lookup"><span data-stu-id="03196-144">This application parses the lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="03196-145">儲存 **Program.cs**，然後建置專案。</span><span class="sxs-lookup"><span data-stu-id="03196-145">Save **Program.cs**, and then build the project.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="03196-146">上傳至儲存體</span><span class="sxs-lookup"><span data-stu-id="03196-146">Upload to storage</span></span>

1. <span data-ttu-id="03196-147">在 Visual Studio 中，開啟 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="03196-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="03196-148">展開 [Azure]，然後展開 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="03196-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="03196-149">如果出現提示，請輸入您的 Azure 訂用帳戶認證，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="03196-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="03196-150">展開您要部署此應用程式的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="03196-150">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="03196-151">就會列出含有文字 __(預設儲存體帳戶)__ 的項目。</span><span class="sxs-lookup"><span data-stu-id="03196-151">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![顯示叢集之儲存體帳戶的 [伺服器總管]](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="03196-153">如果此項目可以展開，表示您是使用 __Azure 儲存體帳戶__作為叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="03196-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="03196-154">若要檢視叢集之預設儲存體上的檔案，請展開項目，然後按兩下 [(預設容器)]。</span><span class="sxs-lookup"><span data-stu-id="03196-154">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="03196-155">如果此項目無法展開，表示您是使用 __Azure Data Lake Store__ 作為叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="03196-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="03196-156">若要檢視叢集之預設儲存體上的檔案，請按兩下 [(預設儲存體帳戶)] 項目。</span><span class="sxs-lookup"><span data-stu-id="03196-156">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="03196-157">若要上傳 .exe 檔案，請使用下列其中一種方法：</span><span class="sxs-lookup"><span data-stu-id="03196-157">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="03196-158">如果使用 __Azure 儲存體帳戶__，請按一下上傳圖示，然後瀏覽至 **HiveCSharp** 專案的 **bin\debug** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="03196-158">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **HiveCSharp** project.</span></span> <span data-ttu-id="03196-159">最後，選取 **HiveCSharp.exe** 檔案並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="03196-159">Finally, select the **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![上傳圖示](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="03196-161">如果使用 __Azure Data Lake Store__，請以滑鼠右鍵按一下檔案清單中的空白區域，然後選取 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="03196-161">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="03196-162">最後，選取 **HiveCSharp.exe** 檔案並按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="03196-162">Finally, select the **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="03196-163">__HiveCSharp.exe__ 上傳完成後，請針對 __PigUDF.exe__ 檔案重複上傳程序。</span><span class="sxs-lookup"><span data-stu-id="03196-163">Once the __HiveCSharp.exe__ upload has finished, repeat the upload process for the __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="03196-164">執行 HIVE 查詢</span><span class="sxs-lookup"><span data-stu-id="03196-164">Run a Hive query</span></span>

1. <span data-ttu-id="03196-165">在 Visual Studio 中，開啟 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="03196-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="03196-166">展開 [Azure]，然後展開 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="03196-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="03196-167">以滑鼠右鍵按一下部署 **HiveCSharp** 應用程式的叢集，然後選取 [撰寫 Hive 查詢]。</span><span class="sxs-lookup"><span data-stu-id="03196-167">Right-click the cluster that you deployed the **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="03196-168">在 Hive 查詢中使用下列文字：</span><span class="sxs-lookup"><span data-stu-id="03196-168">Use the following text for the Hive query:</span></span>

    ```hiveql
    -- Uncomment the following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment the following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="03196-169">將和使用於您叢集之預設儲存體類型相符的 `add file` 陳述式取消註解。</span><span class="sxs-lookup"><span data-stu-id="03196-169">Uncomment the `add file` statement that matches the type of default storage used for your cluster.</span></span>

    <span data-ttu-id="03196-170">此查詢會從 `hivesampletable` 中選取 `clientid`、`devicemake` 和 `devicemodel` 欄位，然後將這些欄位傳遞給 HiveCSharp.exe 應用程式。</span><span class="sxs-lookup"><span data-stu-id="03196-170">This query selects the `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes the fields to the HiveCSharp.exe application.</span></span> <span data-ttu-id="03196-171">此查詢預期應用程式會傳回儲存為 `clientid`、`phoneLabel` 和 `phoneHash` 的三個欄位。</span><span class="sxs-lookup"><span data-stu-id="03196-171">The query expects the application to return three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="03196-172">此查詢也預期會在預設儲存體容器的根目錄中找到 HiveCSharp.exe。</span><span class="sxs-lookup"><span data-stu-id="03196-172">The query also expects to find HiveCSharp.exe in the root of the default storage container.</span></span>

5. <span data-ttu-id="03196-173">按一下 [提交]，將工作提交至 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="03196-173">Click **Submit** to submit the job to the HDInsight cluster.</span></span> <span data-ttu-id="03196-174">[Hive 作業摘要] 視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="03196-174">The **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="03196-175">按一下 [重新整理] 以重新整理摘要，直到 [作業狀態] 變更為 [已完成] 為止。</span><span class="sxs-lookup"><span data-stu-id="03196-175">Click **Refresh** to refresh the summary until **Job Status** changes to **Completed**.</span></span> <span data-ttu-id="03196-176">若要檢視作業輸出，請按一下 [作業輸出]。</span><span class="sxs-lookup"><span data-stu-id="03196-176">To view the job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="03196-177">執行 Pig 作業</span><span class="sxs-lookup"><span data-stu-id="03196-177">Run a Pig job</span></span>

1. <span data-ttu-id="03196-178">使用下列其中一種方法來連線到您的 HDInsight 叢集︰</span><span class="sxs-lookup"><span data-stu-id="03196-178">Use one of the following methods to connect to your HDInsight cluster:</span></span>

    * <span data-ttu-id="03196-179">如果您使用__以 Linux 為基礎的__ HDInsight 叢集，請使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="03196-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="03196-180">例如，`ssh sshuser@mycluster-ssh.azurehdinsight.net`。</span><span class="sxs-lookup"><span data-stu-id="03196-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="03196-181">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="03196-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="03196-182">如果您使用__以 Windows 為基礎的__ HDInsight 叢集，請[使用遠端桌面連線到叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="03196-182">If you are using a __Windows-based__ HDInsight cluster, [Connect to the cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="03196-183">使用下列其中一個命令來啟動 Pig 命令列：</span><span class="sxs-lookup"><span data-stu-id="03196-183">Use one the following command to start the Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="03196-184">如果您使用以 Windows 為基礎的叢集，請改為使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="03196-184">If you are using a Windows-based cluster, use the following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="03196-185">`grunt>` 提示隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="03196-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="03196-186">輸入下列命令，以執行使用 .NET Framework 應用程式的 Pig 作業：</span><span class="sxs-lookup"><span data-stu-id="03196-186">Enter the following to run a Pig job that uses the .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="03196-187">`DEFINE` 陳述式會為 pigudf.exe 應用程式建立別名 `streamer`，然後 `CACHE` 會從叢集的預設儲存體載入它。</span><span class="sxs-lookup"><span data-stu-id="03196-187">The `DEFINE` statement creates an alias of `streamer` for the pigudf.exe applications, and `CACHE` loads it from default storage for the cluster.</span></span> <span data-ttu-id="03196-188">稍後，`streamer` 會與 `STREAM` 運算子搭配使用，進而處理 LOG 中所包含的單行，並以一連串資料行的方式傳回資料。</span><span class="sxs-lookup"><span data-stu-id="03196-188">Later, `streamer` is used with the `STREAM` operator to process the single lines contained in LOG and return the data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="03196-189">建立別名時，用於串流處理的應用程式名稱的兩邊必須加上 \` (倒引號) 字元，與 `SHIP\` 搭配使用時，必須加上 ' (單引號) 字元。</span><span class="sxs-lookup"><span data-stu-id="03196-189">The application name that is used for streaming must be surrounded by the \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="03196-190">輸入最後一行後，作業應該就會開始。</span><span class="sxs-lookup"><span data-stu-id="03196-190">After entering the last line, the job should start.</span></span> <span data-ttu-id="03196-191">它會傳回類似下列文字的輸出：</span><span class="sxs-lookup"><span data-stu-id="03196-191">It returns output similar to the following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="03196-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03196-192">Next steps</span></span>

<span data-ttu-id="03196-193">在本文中，您已學會如何從 HDInsight 上的 Hive 和 Pig 使用 .NET Framework 應用程式。</span><span class="sxs-lookup"><span data-stu-id="03196-193">In this document, you have learned how to use a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="03196-194">如果您想要了解如何搭配使用 Python 與 Hive 和 Pig，請參閱[搭配使用 Python 與 HDInsight 中的 Hive 和 Pig](hdinsight-python.md)。</span><span class="sxs-lookup"><span data-stu-id="03196-194">If you would like to learn how to use Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="03196-195">若要了解Pig 和 Hive 的其他使用方式，以及了解使用 MapReduce 的方式，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="03196-195">For other ways to use Pig and Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="03196-196">搭配 HDInsight 使用 Hivet</span><span class="sxs-lookup"><span data-stu-id="03196-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="03196-197">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="03196-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="03196-198">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="03196-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

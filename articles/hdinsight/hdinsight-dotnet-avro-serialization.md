---
title: "序列化 Hadoop 中的資料 - Microsoft Avro Library - Azure | Microsoft Docs"
description: "了解如何使用 Microsoft Avro Library 序列化和還原序列化 HDInsight 上 Hadoop 中的資料來保存到記憶體、資料庫或檔案中。"
keywords: avro, hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: d06bf8ff4a21e4f4b29593bac32bfa2b32601fc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="serialize-data-in-hadoop-with-the-microsoft-avro-library"></a><span data-ttu-id="b66fb-104">使用 Microsoft Avro Library 將 Hadoop 中的資料序列化</span><span class="sxs-lookup"><span data-stu-id="b66fb-104">Serialize data in Hadoop with the Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="b66fb-105">Microsoft 不再支援 Avro SDK。</span><span class="sxs-lookup"><span data-stu-id="b66fb-105">The Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="b66fb-106">該程式庫由開放原始碼社群來支援。</span><span class="sxs-lookup"><span data-stu-id="b66fb-106">The library is open source community supported.</span></span> <span data-ttu-id="b66fb-107">該程式庫的來源位於 [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro)。</span><span class="sxs-lookup"><span data-stu-id="b66fb-107">The sources for the library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="b66fb-108">本主題示範如何使用 [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) 將物件與其他資料結構序列化為串流，以將它們保存到記憶體、 資料庫或檔案中。</span><span class="sxs-lookup"><span data-stu-id="b66fb-108">This topic shows how to use the [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) to serialize objects and other data structures into streams to persist them to memory, a database, or a file.</span></span> <span data-ttu-id="b66fb-109">它也會示範如何將它們還原序列化，以復原原始物件。</span><span class="sxs-lookup"><span data-stu-id="b66fb-109">It also shows how to deserialize them to recover the original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="b66fb-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="b66fb-110">Apache Avro</span></span>
<span data-ttu-id="b66fb-111"><a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> 可在 Microsoft.NET 環境中實作 Apache Avro 資料序列化系統。</span><span class="sxs-lookup"><span data-stu-id="b66fb-111">The <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements the Apache Avro data serialization system for the Microsoft.NET environment.</span></span> <span data-ttu-id="b66fb-112">Apache Avro 提供一個可用於序列化的壓縮二進位資料交換格式。</span><span class="sxs-lookup"><span data-stu-id="b66fb-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="b66fb-113">它會使用 <a href="http://www.json.org" target="_blank">JSON</a> 來定義不限語言的結構描述，以負責提供語言互通性。</span><span class="sxs-lookup"><span data-stu-id="b66fb-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> to define a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="b66fb-114">以某個語言序列化的資料可以使用另一個語言讀取。</span><span class="sxs-lookup"><span data-stu-id="b66fb-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="b66fb-115">目前支援 C、C++、C#、Java、PHP、Python 和 Ruby。</span><span class="sxs-lookup"><span data-stu-id="b66fb-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="b66fb-116">如需此格式的詳細資訊，請參閱 <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro 規格</a>。</span><span class="sxs-lookup"><span data-stu-id="b66fb-116">Detailed information on the format can be found in the <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="b66fb-117">Microsoft Avro Library 不支援此規格的遠端程序呼叫 (RPC) 部分。</span><span class="sxs-lookup"><span data-stu-id="b66fb-117">The Microsoft Avro Library does not support the remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="b66fb-118">在 Avro 系統中，物件的序列化表示包含兩個部分：結構描述和實際值。</span><span class="sxs-lookup"><span data-stu-id="b66fb-118">The serialized representation of an object in the Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="b66fb-119">Avro 結構描述說明使用 JSON 序列化資料的語言獨立資料模型。</span><span class="sxs-lookup"><span data-stu-id="b66fb-119">The Avro schema describes the language-independent data model of the serialized data with JSON.</span></span> <span data-ttu-id="b66fb-120">它會與資料的二進位表示並存。</span><span class="sxs-lookup"><span data-stu-id="b66fb-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="b66fb-121">分開結構描述與二進位表示可允許在沒有個別值額外負荷的情況下寫入每個物件，以快速進行序列化並縮小表示。</span><span class="sxs-lookup"><span data-stu-id="b66fb-121">Having the schema separate from the binary representation permits each object to be written with no per-value overheads, making serialization fast, and the representation small.</span></span>

## <a name="the-hadoop-scenario"></a><span data-ttu-id="b66fb-122">Hadoop 案例</span><span class="sxs-lookup"><span data-stu-id="b66fb-122">The Hadoop scenario</span></span>
<span data-ttu-id="b66fb-123">Azure HDInsight 和其他 Apache Hadoop 環境中廣泛採用了 Apache Avro 序列化格式。</span><span class="sxs-lookup"><span data-stu-id="b66fb-123">The Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="b66fb-124">Avro 提供一個便利方式來呈現 Hadoop MapReduce 工作的複雜資料結構。</span><span class="sxs-lookup"><span data-stu-id="b66fb-124">Avro provides a convenient way to represent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="b66fb-125">Avro 檔案格式 (Avro 物件容器檔案) 已針對支援分散式 MapReduce 程式設計模型進行設計。</span><span class="sxs-lookup"><span data-stu-id="b66fb-125">The format of Avro files (Avro object container file) has been designed to support the distributed MapReduce programming model.</span></span> <span data-ttu-id="b66fb-126">啟用配送的主要功能是指檔案「可分割」，因此使用者可搜尋檔案中的任何位置，並從特定區塊開始讀取。</span><span class="sxs-lookup"><span data-stu-id="b66fb-126">The key feature that enables the distribution is that the files are “splittable” in the sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="b66fb-127">Avro Library 中的序列化</span><span class="sxs-lookup"><span data-stu-id="b66fb-127">Serialization in Avro Library</span></span>
<span data-ttu-id="b66fb-128">.NET Library for Avro 支援兩個序列化物件方式：</span><span class="sxs-lookup"><span data-stu-id="b66fb-128">The .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="b66fb-129">**反映** - 類型的 JSON 結構描述會根據要序列化的 .NET 類型資料合約屬性自動建置。</span><span class="sxs-lookup"><span data-stu-id="b66fb-129">**reflection** - The JSON schema for the types is automatically built from the data contract attributes of the .NET types to be serialized.</span></span>
* <span data-ttu-id="b66fb-130">**一般記錄**：當沒有 .NET 類型存在以說明要序列化資料的結構描述時，以 [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) 類別表示的記錄中會明確指定 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="b66fb-130">**generic record** - A JSON schema is explicitly specified in a record represented by the [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present to describe the schema for the data to be serialized.</span></span>

<span data-ttu-id="b66fb-131">當資料流的寫入器和讀取器可識別資料結構描述時，便可以在沒有其結構描述的情況下傳送資料。</span><span class="sxs-lookup"><span data-stu-id="b66fb-131">When the data schema is known to both the writer and reader of the stream, the data can be sent without its schema.</span></span> <span data-ttu-id="b66fb-132">在未使用 Avro 物件容器檔案的情況下，會將結構描述儲存在檔案內。</span><span class="sxs-lookup"><span data-stu-id="b66fb-132">In cases when an Avro object container file is used, the schema is stored within the file.</span></span> <span data-ttu-id="b66fb-133">您可以指定其他參數 (例如用於資料壓縮的轉碼器)。</span><span class="sxs-lookup"><span data-stu-id="b66fb-133">Other parameters, such as the codec used for data compression, can be specified.</span></span> <span data-ttu-id="b66fb-134">這些案例會在以下程式碼範例中詳加說明與圖解：</span><span class="sxs-lookup"><span data-stu-id="b66fb-134">These scenarios are outlined in more detail and illustrated in the following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="b66fb-135">安裝 Avro Library</span><span class="sxs-lookup"><span data-stu-id="b66fb-135">Install Avro Library</span></span>
<span data-ttu-id="b66fb-136">以下是安裝此程式庫前必備的條件：</span><span class="sxs-lookup"><span data-stu-id="b66fb-136">The following are required before you install the library:</span></span>

* <span data-ttu-id="b66fb-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="b66fb-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="b66fb-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="b66fb-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="b66fb-139">請注意，Newtonsoft.Json.dll 相依性也會隨著安裝 Microsoft Avro Library 自動下載。</span><span class="sxs-lookup"><span data-stu-id="b66fb-139">Note that the Newtonsoft.Json.dll dependency is downloaded automatically with the installation of the Microsoft Avro Library.</span></span> <span data-ttu-id="b66fb-140">此程序會在下一節中提供：</span><span class="sxs-lookup"><span data-stu-id="b66fb-140">The procedure is provided in the following section:</span></span>

<span data-ttu-id="b66fb-141">Microsoft Avro 程式庫會以 NuGet 封裝發行，您可以透過下列程序在 Visual Studio 中安裝 NuGet 封裝：</span><span class="sxs-lookup"><span data-stu-id="b66fb-141">The Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via the following procedure:</span></span>

1. <span data-ttu-id="b66fb-142">依序選取 [專案] 索引標籤 -> [管理 NuGet 封裝]</span><span class="sxs-lookup"><span data-stu-id="b66fb-142">Select the **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="b66fb-143">在 [ **線上搜尋** ] 方塊中搜尋 "Microsoft.Hadoop.Avro"。</span><span class="sxs-lookup"><span data-stu-id="b66fb-143">Search for "Microsoft.Hadoop.Avro" in the **Search Online** box.</span></span>
3. <span data-ttu-id="b66fb-144">按一下 [Microsoft Azure HDInsight Avro Library] 旁的 [安裝] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b66fb-144">Click the **Install** button next to **Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="b66fb-145">請注意，Newtonsoft.Json.dll (>=6.0.4) 相依性也會隨著 Microsoft Avro Library 自動下載。</span><span class="sxs-lookup"><span data-stu-id="b66fb-145">Note that the Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with the Microsoft Avro Library.</span></span>

<span data-ttu-id="b66fb-146">Microsoft Avro Library 原始程式碼可在 [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) 取得。</span><span class="sxs-lookup"><span data-stu-id="b66fb-146">The Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="b66fb-147">使用 Avro Library 來編譯結構描述</span><span class="sxs-lookup"><span data-stu-id="b66fb-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="b66fb-148">Microsoft Avro Library 包含程式碼產生公用程式，可允許自動依據先前定義的 JSON 結構描述來建立 C# 類型。</span><span class="sxs-lookup"><span data-stu-id="b66fb-148">The Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on the previously defined JSON schema.</span></span> <span data-ttu-id="b66fb-149">程式碼產生公用程式未以二進位執行檔的形式散佈，但可透過下列程序輕鬆建置：</span><span class="sxs-lookup"><span data-stu-id="b66fb-149">The code generation utility is not distributed as a binary executable, but can be easily built via the following procedure:</span></span>

1. <span data-ttu-id="b66fb-150">從 <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a> 下載具有最新版 HDInsight SDK 原始程式碼的 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="b66fb-150">Download the .zip file with the latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="b66fb-151">(按一下 [下載] 圖示，而不是 [下載] 索引標籤。)</span><span class="sxs-lookup"><span data-stu-id="b66fb-151">(Click the **Download** icon, not the **Downloads** tab.)</span></span>
2. <span data-ttu-id="b66fb-152">將 HDInsight SDK 解壓縮至已安裝 .NET Framework 4 並連接至網際網路的電腦上的目錄，以下載必要的相依性 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="b66fb-152">Extract the HDInsight SDK to a directory on the machine with .NET Framework 4 installed and connected to the Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="b66fb-153">以下我們假設原始程式碼會解壓縮至 C:\SDK。</span><span class="sxs-lookup"><span data-stu-id="b66fb-153">Below, we assume that the source code is extracted to C:\SDK.</span></span>
3. <span data-ttu-id="b66fb-154">前往資料夾 C:\SDK\src\Microsoft.Hadoop.Avro.Tools 並執行 build.bat</span><span class="sxs-lookup"><span data-stu-id="b66fb-154">Go to the folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="b66fb-155">(此檔案會呼叫 .NET Framework 32 位元發行版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="b66fb-155">(The file calls MSBuild from the 32-bit distribution of the .NET Framework.</span></span> <span data-ttu-id="b66fb-156">如果您想要使用 64 位元版本，請依照 build.bat 檔案中的註解編輯該檔案)。確保建置成功。</span><span class="sxs-lookup"><span data-stu-id="b66fb-156">If you would like to use the 64-bit version, edit build.bat, following the comments inside the file.) Ensure that the build is successful.</span></span> <span data-ttu-id="b66fb-157">(在某些系統上，MSBuild 可能會產生警告。</span><span class="sxs-lookup"><span data-stu-id="b66fb-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="b66fb-158">(只要沒有建置錯誤，就不會影響公用程式。)</span><span class="sxs-lookup"><span data-stu-id="b66fb-158">These warnings do not affect the utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="b66fb-159">編譯的公用程式位於 C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools。</span><span class="sxs-lookup"><span data-stu-id="b66fb-159">The compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="b66fb-160">若要熟悉命令列語法，請從程式碼產生公用程式所在的資料夾執行下列命令：`Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="b66fb-160">To get familiar with the command-line syntax, execute the following command from the folder where the code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="b66fb-161">若要測試公用程式，您可以從隨著原始程式碼提供的範例 JSON 結構描述檔案產生 C# 類別。</span><span class="sxs-lookup"><span data-stu-id="b66fb-161">To test the utility, you can generate C# classes from the sample JSON schema file provided with the source code.</span></span> <span data-ttu-id="b66fb-162">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="b66fb-162">Execute the following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="b66fb-163">這應該會在目前的目錄產生兩個 C# 檔案：SensorData.cs 和 Location.cs。</span><span class="sxs-lookup"><span data-stu-id="b66fb-163">This is supposed to produce two C# files in the current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="b66fb-164">若要了解程式碼產生公用程式在轉換 JSON 結構描述為 C# 類型時使用的邏輯，請參閱位於 C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc 的 GenerationVerification.feature 檔案。</span><span class="sxs-lookup"><span data-stu-id="b66fb-164">To understand the logic that the code generation utility is using while converting the JSON schema to C# types, see the file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="b66fb-165">命名空間是從 JSON 結構描述中擷取，所用的邏輯詳述於先前段落所提及的檔案中。</span><span class="sxs-lookup"><span data-stu-id="b66fb-165">Namespaces are extracted from the JSON schema, using the logic described in the file mentioned in the previous paragraph.</span></span> <span data-ttu-id="b66fb-166">從結構描述擷取的命名空間，將比公用程式命令列中使用 /n 參數提供的設定具有優先權。</span><span class="sxs-lookup"><span data-stu-id="b66fb-166">Namespaces extracted from the schema take precedence over whatever is provided with the /n parameter in the utility command line.</span></span> <span data-ttu-id="b66fb-167">如果您想要覆寫結構描述中內含的命名空間，請使用 /nf 參數。</span><span class="sxs-lookup"><span data-stu-id="b66fb-167">If you want to override the namespaces contained within the schema, use the /nf parameter.</span></span> <span data-ttu-id="b66fb-168">例如，若要將所有命名空間從 SampleJSONSchema.avsc 變更為 my.own.nspace，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b66fb-168">For example, to change all namespaces from the SampleJSONSchema.avsc to my.own.nspace, execute the following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-the-samples"></a><span data-ttu-id="b66fb-169">關於範例</span><span class="sxs-lookup"><span data-stu-id="b66fb-169">About the samples</span></span>
<span data-ttu-id="b66fb-170">本主題中提供了六個範例，每個範例說明 Microsoft Avro Library 所支援的不同案例。</span><span class="sxs-lookup"><span data-stu-id="b66fb-170">Six examples provided in this topic illustrate different scenarios supported by the Microsoft Avro Library.</span></span> <span data-ttu-id="b66fb-171">Microsoft Avro Library 是專門為了使用任何資料流所設計的。</span><span class="sxs-lookup"><span data-stu-id="b66fb-171">The Microsoft Avro Library is designed to work with any stream.</span></span> <span data-ttu-id="b66fb-172">為了方便一致起見，這些範例會透過記憶體資料流，而不是檔案資料流或資料庫。</span><span class="sxs-lookup"><span data-stu-id="b66fb-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="b66fb-173">生產環境中要採用的方法視確切的案例需求、資料來源和資料數量、效能限制及其他因素而定。</span><span class="sxs-lookup"><span data-stu-id="b66fb-173">The approach taken in a production environment depends on the exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="b66fb-174">前兩個範例說明如何使用反映和一般記錄，將資料序列化與還原序列化為記憶體資料流緩衝區。</span><span class="sxs-lookup"><span data-stu-id="b66fb-174">The first two examples show how to serialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="b66fb-175">在這兩個案例中假設讀取器和寫入器之間會共用結構描述。</span><span class="sxs-lookup"><span data-stu-id="b66fb-175">The schema in these two cases is assumed to be shared between the readers and writers out-of-band.</span></span>

<span data-ttu-id="b66fb-176">第三和第四個範例說明如何使用 Avro 物件容器檔案，將資料序列化與還原序列化。</span><span class="sxs-lookup"><span data-stu-id="b66fb-176">The third and fourth examples show how to serialize and deserialize data by using the Avro object container files.</span></span> <span data-ttu-id="b66fb-177">因為還原序列化必須共用結構描述，所以在 Avro 容器檔案中儲存資料時，一定會一起儲存資料的結構描述。</span><span class="sxs-lookup"><span data-stu-id="b66fb-177">When data is stored in an Avro container file, its schema is always stored with it because the schema must be shared for deserialization.</span></span>

<span data-ttu-id="b66fb-178">您可以從 <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure 程式碼範例</a>網站 (英文) 下載包含前四個案例的範例。</span><span class="sxs-lookup"><span data-stu-id="b66fb-178">The sample containing the first four examples can be downloaded from the <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="b66fb-179">第五個範例說明如何使用自訂壓縮轉碼器來處理 Avro 物件容器檔案。</span><span class="sxs-lookup"><span data-stu-id="b66fb-179">The fifth example shows how to use a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="b66fb-180">您可以從 <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure 程式碼範例</a> 網站 (英文) 下載包含此案例程式碼的範例。</span><span class="sxs-lookup"><span data-stu-id="b66fb-180">A sample containing the code for this example can be downloaded from the <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="b66fb-181">第六個範例顯示如何使用 Avro 序列化來上傳資料至 Azure Blob 儲存體，然後使用具有 HDInsight (Hadoop) 叢集的 Hive 加以分析。</span><span class="sxs-lookup"><span data-stu-id="b66fb-181">The sixth sample shows how to use Avro serialization to upload data to Azure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="b66fb-182">您可以從 <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure 程式碼範例</a> 網站 (英文) 下載包含前四個案例的範例。</span><span class="sxs-lookup"><span data-stu-id="b66fb-182">It can be downloaded from the <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="b66fb-183">以下是本主題所討論六個範例的連結：</span><span class="sxs-lookup"><span data-stu-id="b66fb-183">Here are links to the six samples discussed in the topic:</span></span>

* <span data-ttu-id="b66fb-184"><a href="#Scenario1">**使用反映進行序列化**</a> - 要序列化之類型的 JSON 結構描述會根據資料合約屬性自動建置。</span><span class="sxs-lookup"><span data-stu-id="b66fb-184"><a href="#Scenario1">**Serialization with reflection**</a> - The JSON schema for types to be serialized is automatically built from the data contract attributes.</span></span>
* <span data-ttu-id="b66fb-185"><a href="#Scenario2">**使用一般記錄進行序列化**</a> - 當沒有可用於反映的 .NET 類型時，會在記錄中明確指定 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="b66fb-185"><a href="#Scenario2">**Serialization with generic record**</a> - The JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="b66fb-186"><a href="#Scenario3">**使用物件容器檔案與反映進行序列化**</a> - JSON 結構描述會自動建置並透過 Avro 物件容器檔案隨著序列化的資料共用。</span><span class="sxs-lookup"><span data-stu-id="b66fb-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - The JSON schema is automatically built and shared together with the serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="b66fb-187"><a href="#Scenario4">**使用物件容器檔案與一般記錄進行序列化**</a> - JSON 結構描述會自動建置並透過 Avro 物件容器檔案隨著序列化的資料共用。</span><span class="sxs-lookup"><span data-stu-id="b66fb-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - The JSON schema is explicitly specified before the serialization and shared together with the data via an Avro object container file.</span></span>
* <span data-ttu-id="b66fb-188"><a href="#Scenario5">**使用物件容器檔案和自訂壓縮轉碼器進行序列化**</a> - 此範例顯示如何使用 Deflate 資料壓縮轉碼器的自訂 .NET 實作，來建立 Avro 物件容器檔案。</span><span class="sxs-lookup"><span data-stu-id="b66fb-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - The example shows how to create an Avro object container file with a customized .NET implementation of the Deflate data compression codec.</span></span>
* <span data-ttu-id="b66fb-189"><a href="#Scenario6">**使用 Avro 來上傳 Microsoft Azure HDInsight 服務的資料**</a> - 此範例說明 Avro 序列化如何與 HDInsight 服務互動。</span><span class="sxs-lookup"><span data-stu-id="b66fb-189"><a href="#Scenario6">**Using Avro to upload data for the Microsoft Azure HDInsight service**</a> - The example illustrates how Avro serialization interacts with the HDInsight service.</span></span> <span data-ttu-id="b66fb-190">使用中 Azure 訂用帳戶，並且可存取 Azure HDInsight 叢集為執行此範例的必要條件。</span><span class="sxs-lookup"><span data-stu-id="b66fb-190">An active Azure subscription and access to an Azure HDInsight cluster are required to run this example.</span></span>

## <span data-ttu-id="b66fb-191"><a name="Scenario1"></a>範例 1：使用反映進行序列化</span><span class="sxs-lookup"><span data-stu-id="b66fb-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="b66fb-192">Microsoft Avro 程式庫可透過反映、根據要序列化的 C# 物件資料合約屬性自動建置類型的 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="b66fb-192">The JSON schema for the types can be automatically built by the Microsoft Avro Library via reflection from the data contract attributes of the C# objects to be serialized.</span></span> <span data-ttu-id="b66fb-193">Microsoft Avro Library 會建立一個可識別要序列化欄位的 [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b66fb-193">The Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) to identify the fields to be serialized.</span></span>

<span data-ttu-id="b66fb-194">在此範例中，物件 (包含成員 [位置] 結構的 **SensorData** 類別) 會被序列化為記憶體資料流，後續再將此資料流還原序列化。</span><span class="sxs-lookup"><span data-stu-id="b66fb-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized to a memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="b66fb-195">最後將結果與初始執行個體相比較，以確認復原的 **SensorData** 物件會與原始物件相同。</span><span class="sxs-lookup"><span data-stu-id="b66fb-195">The result is then compared to the initial instance to confirm that the **SensorData** object recovered is identical to the original.</span></span>

<span data-ttu-id="b66fb-196">此範例假設讀取器和寫入器之間會共用結構描述，因此無需 Avro 物件容器格式。</span><span class="sxs-lookup"><span data-stu-id="b66fb-196">The schema in this example is assumed to be shared between the readers and writers, so the Avro object container format is not required.</span></span> <span data-ttu-id="b66fb-197">當必須使用資料來共用結構描述時，如需如何使用反映和物件容器格式將資料序列化和還原序列化為記憶體緩衝區的範例，請參閱<a href="#Scenario3">使用物件容器檔案與反映進行序列化</a>。</span><span class="sxs-lookup"><span data-stu-id="b66fb-197">For an example of how to serialize and deserialize data into memory buffers by using reflection with the object container format when the schema must be shared with the data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize the data to the specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from the stream and cast it to the same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches the original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization to memory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="b66fb-198">範例 2：使用一般記錄進行序列化</span><span class="sxs-lookup"><span data-stu-id="b66fb-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="b66fb-199">因為資料無法透過包含資料合約的 .NET 類別呈現，而無法使用反映時，您可以在一般記錄中明確指定 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="b66fb-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because the data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="b66fb-200">此方法較使用反映來得慢。</span><span class="sxs-lookup"><span data-stu-id="b66fb-200">This method is slower than using reflection.</span></span> <span data-ttu-id="b66fb-201">在此情況下，資料的結構描述也有可能是動態的，亦即在編譯階段開始之前無法得知資料的結構描述。</span><span class="sxs-lookup"><span data-stu-id="b66fb-201">In such cases, the schema for the data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="b66fb-202">此類動態案例的其中一個範例是以逗號分隔值 (CSV) 檔案表示的資料，在執行階段將它轉換為 Avro 格式之前不會知道檔案的結構描述。</span><span class="sxs-lookup"><span data-stu-id="b66fb-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed to the Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="b66fb-203">本範例說明如何建立與使用 [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) 來明確指定 JSON 結構描述、如何填入資料，然後如何將它序列化與還原序列化。</span><span class="sxs-lookup"><span data-stu-id="b66fb-203">This example shows how to create and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) to explicitly specify a JSON schema, how to populate it with the data, and then how to serialize and deserialize it.</span></span> <span data-ttu-id="b66fb-204">最後將結果與初始執行個體相比較，以確認復原的記錄會與原始記錄相同。</span><span class="sxs-lookup"><span data-stu-id="b66fb-204">The result is then compared to the initial instance to confirm that the record recovered is identical to the original.</span></span>

<span data-ttu-id="b66fb-205">此範例假設讀取器和寫入器之間會共用結構描述，因此無需 Avro 物件容器格式。</span><span class="sxs-lookup"><span data-stu-id="b66fb-205">The schema in this example is assumed to be shared between the readers and writers, so the Avro object container format is not required.</span></span> <span data-ttu-id="b66fb-206">當序列化資料中必須包含結構描述時，如需如何使用一般記錄和物件容器格式將資料序列化和還原序列化為記憶體緩衝區的範例，請參閱<a href="#Scenario4">使用物件容器檔案與一般記錄進行序列化</a>範例。</span><span class="sxs-lookup"><span data-stu-id="b66fb-206">For an example of how to serialize and deserialize data into memory buffers by using a generic record with the object container format when the schema must be included with the serialized data, see the <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //the usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with the schema explicitly defined in JSON.
        //All serialized data should be mapped to the fields of the generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining the Schema and creating Sample Data Set...");

            //Define the schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on the schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record to represent the data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize the data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize the data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify the results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization to memory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key to exit.");
            Console.Read();
        }
    }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining the Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="b66fb-207">範例 3：使用物件容器檔案進行序列化和使用反映進行序列化</span><span class="sxs-lookup"><span data-stu-id="b66fb-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="b66fb-208">本範例與<a href="#Scenario1">第一個範例</a> (使用反映暗中指定結構描述) 中的案例類似。</span><span class="sxs-lookup"><span data-stu-id="b66fb-208">This example is similar to the scenario in the <a href="#Scenario1"> first example</a>, where the schema is implicitly specified with reflection.</span></span> <span data-ttu-id="b66fb-209">差別在於本範例假設要將結構描述還原序列化的讀取器不知道結構描述。</span><span class="sxs-lookup"><span data-stu-id="b66fb-209">The difference is that here, the schema is not assumed to be known to the reader that deserializes it.</span></span> <span data-ttu-id="b66fb-210">要序列化的 **SensorData** 物件及其隱含指定的結構描述，會儲存在以 [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) 類別表示的 Avro 物件容器檔案中。</span><span class="sxs-lookup"><span data-stu-id="b66fb-210">The **SensorData** objects to be serialized and their implicitly specified schema are stored in an Avro object container file represented by the [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="b66fb-211">本範例會使用 [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) 序列化資料，並使用 [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) 還原序列化資料。</span><span class="sxs-lookup"><span data-stu-id="b66fb-211">The data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="b66fb-212">最後與初始執行個體相比較，以確認身分識別。</span><span class="sxs-lookup"><span data-stu-id="b66fb-212">The result then is compared to the initial instances to ensure identity.</span></span>

<span data-ttu-id="b66fb-213">物件容器檔案中的資料會透過 .NET Framework 4 預設的 [**Deflate**][deflate-100] 壓縮轉碼器進行壓縮。</span><span class="sxs-lookup"><span data-stu-id="b66fb-213">The data in the object container file is compressed via the default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="b66fb-214">請參閱本主題中的<a href="#Scenario5">第五個範例</a>，以了解如何使用 .NET Framework 4.5 中所提供更新的及更優異的 [**Deflate**][deflate-110] 壓縮轉碼器版本。</span><span class="sxs-lookup"><span data-stu-id="b66fb-214">See the <a href="#Scenario5"> fifth example</a> in this topic to learn how to use a more recent and superior version of the [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes the sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with the Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data to file.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Data is compressed using the Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize the data to stream by using the sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream to file
                    Console.WriteLine("Saving serialized data to file...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches the original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete the file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream to a new file with the given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using the given path to a memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection to Avro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="b66fb-215">範例 4：使用物件容器檔案進行序列化和使用一般記錄進行序列化</span><span class="sxs-lookup"><span data-stu-id="b66fb-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="b66fb-216">本範例與<a href="#Scenario2">第二個範例</a> (使用 JSON 明確指定結構描述) 中的案例類似。</span><span class="sxs-lookup"><span data-stu-id="b66fb-216">This example is similar to the scenario in the <a href="#Scenario2"> second example</a>, where the schema is explicitly specified with JSON.</span></span> <span data-ttu-id="b66fb-217">差別在於本範例假設要將結構描述還原序列化的讀取器不知道結構描述。</span><span class="sxs-lookup"><span data-stu-id="b66fb-217">The difference is that here, the schema is not assumed to be known to the reader that deserializes it.</span></span>

<span data-ttu-id="b66fb-218">您可以透過明確定義的 JSON 結構描述將測試資料集收集到 [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) 物件的清單，然後儲存在以 [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) 類別表示的物件容器檔案中。</span><span class="sxs-lookup"><span data-stu-id="b66fb-218">The test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by the [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="b66fb-219">這個容器檔案會建立一個寫入器，以未壓縮的方式將資料序列化為記憶體資料流，然後儲存到檔案。</span><span class="sxs-lookup"><span data-stu-id="b66fb-219">This container file creates a writer that is used to serialize the data, uncompressed, to a memory stream that is then saved to a file.</span></span> <span data-ttu-id="b66fb-220">用於建立讀取器的 [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) 參數會指定不要壓縮此資料。</span><span class="sxs-lookup"><span data-stu-id="b66fb-220">The [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating the reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="b66fb-221">最後，從檔案讀取資料並還原序列化為物件集合。</span><span class="sxs-lookup"><span data-stu-id="b66fb-221">The data is then read from the file and deserialized into a collection of objects.</span></span> <span data-ttu-id="b66fb-222">將此集合與 Avro 初始記錄清單相比較，以確認他們完全相同。</span><span class="sxs-lookup"><span data-stu-id="b66fb-222">This collection is compared to the initial list of Avro records to confirm that they are identical.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining the Schema and creating Sample Data Set...");

                //Define the schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on the schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record to represent the data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data to file.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize the data to stream by using the sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data to file...");

                    //Save stream to file
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing the data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify the results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete the file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream to a new file with the given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using the given path to a memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using the given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of the AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record to Avro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining the Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="b66fb-223">範例 5：使用物件容器檔案和自訂壓縮轉碼器進行序列化</span><span class="sxs-lookup"><span data-stu-id="b66fb-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="b66fb-224">第五個範例說明如何使用自訂壓縮轉碼器來處理 Avro 物件容器檔案。</span><span class="sxs-lookup"><span data-stu-id="b66fb-224">The fifth example shows how to use a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="b66fb-225">您可以從 [Azure 程式碼範例](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) (英文) 網站下載包含此案例程式碼的範例。</span><span class="sxs-lookup"><span data-stu-id="b66fb-225">A sample containing the code for this example can be downloaded from the [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="b66fb-226">[Avro 規格](http://avro.apache.org/docs/current/spec.html#Required+Codecs)允許使用選用的壓縮轉碼器 (**Null** 和 **Deflate** 預設值除外)。</span><span class="sxs-lookup"><span data-stu-id="b66fb-226">The [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition to **Null** and **Deflate** defaults).</span></span> <span data-ttu-id="b66fb-227">本範例並未實作新的轉碼器，例如 Snappy (如同 [Avro 規格](http://avro.apache.org/docs/current/spec.html#snappy)中所提及的支援選用轉碼器)。</span><span class="sxs-lookup"><span data-stu-id="b66fb-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in the [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="b66fb-228">其中說明如何使用 .NET Framework 4.5 的 [**Deflate**][deflate-110] 轉碼器實作，採用 [zlib](http://zlib.net/) 壓縮程式庫，提供比預設 .NET Framework 4 版本更好的壓縮演算法。</span><span class="sxs-lookup"><span data-stu-id="b66fb-228">It shows how to use the .NET Framework 4.5 implementation of the [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on the [zlib](http://zlib.net/) compression library than the default .NET Framework 4 version.</span></span>

    //
    // This code needs to be compiled with the parameter Target Framework set as ".NET Framework 4.5"
    // to ensure the desired implementation of the Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are the key ones for data compression.
        //To enable a custom codec, one needs to implement these methods for the required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs to implement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed to be null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define the actual codec class containing the required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory to be used in the reader.
        //It catches the attempt to use "Deflate" and provide  a custom codec.
        //For all other cases, it relies on the base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with the custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related to serialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data to file.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Here the custom codec is introduced. For convenience, the next commented code line shows how to use built-in Deflate.
                    //Note that because the sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize the data to stream using the sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream to file
                    Console.WriteLine("Saving serialized data to file...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment the line below if you want to use built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    //Here the custom codec factory is introduced.
                    //For convenience, the next commented code line shows how to use built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because the sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches the original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete the file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream to a new file with the given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using the given path to a memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection to Avro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.

## <a name="sample-6-using-avro-to-upload-data-for-the-microsoft-azure-hdinsight-service"></a><span data-ttu-id="b66fb-229">範例 6：使用 Avro 來上傳 Microsoft Azure HDInsight 服務的資料</span><span class="sxs-lookup"><span data-stu-id="b66fb-229">Sample 6: Using Avro to upload data for the Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="b66fb-230">第六個範例說明與 Azure HDInsight 服務互動相關的一些程式設計技巧。</span><span class="sxs-lookup"><span data-stu-id="b66fb-230">The sixth example illustrates some programming techniques related to interacting with the Azure HDInsight service.</span></span> <span data-ttu-id="b66fb-231">您可以從 [Azure 程式碼範例](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) (英文) 網站下載包含此案例程式碼的範例。</span><span class="sxs-lookup"><span data-stu-id="b66fb-231">A sample containing the code for this example can be downloaded from the [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="b66fb-232">此範例會執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="b66fb-232">The sample does the following tasks:</span></span>

* <span data-ttu-id="b66fb-233">連線至現有的 HDInsight 服務叢集。</span><span class="sxs-lookup"><span data-stu-id="b66fb-233">Connects to an existing HDInsight service cluster.</span></span>
* <span data-ttu-id="b66fb-234">序列化數個 CSV 檔案並上傳結果至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="b66fb-234">Serializes several CSV files and uploads the result to Azure Blob storage.</span></span> <span data-ttu-id="b66fb-235">(CSV 檔案會隨著範例一起散佈，並代表 [Infochimps](http://www.infochimps.com/) 在 1970-2010 期間散佈的 AMEX 庫存歷史資料的擷取。</span><span class="sxs-lookup"><span data-stu-id="b66fb-235">(The CSV files are distributed together with the sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for the period 1970-2010.</span></span> <span data-ttu-id="b66fb-236">範例會讀取 CSV 檔案資料、轉換記錄為 **庫存** 類別的執行個體，然後使用反映加以序列化。</span><span class="sxs-lookup"><span data-stu-id="b66fb-236">The sample reads CSV file data, converts the records to instances of the **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="b66fb-237">庫存類型定義是透過 Microsoft Avro Library 程式碼產生公用程式從 JSON 結構描述建立。</span><span class="sxs-lookup"><span data-stu-id="b66fb-237">Stock type definition is created from a JSON schema via the Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="b66fb-238">在 Hive 中建立名為 **Stocks** 的新外部資料表，並將它連結至前一個步驟中上傳的資料。</span><span class="sxs-lookup"><span data-stu-id="b66fb-238">Creates a new external table called **Stocks** in Hive, and links it to the data uploaded in the previous step.</span></span>
* <span data-ttu-id="b66fb-239">使用 Hive 對 **Stocks** 資料表執行查詢。</span><span class="sxs-lookup"><span data-stu-id="b66fb-239">Executes a query by using Hive over the **Stocks** table.</span></span>

<span data-ttu-id="b66fb-240">此外，範例會在執行主要作業之前和之後執行清理程序。</span><span class="sxs-lookup"><span data-stu-id="b66fb-240">In addition, the sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="b66fb-241">在清理期間，所有相關的 Azure Blob 資料和資料夾都會被移除，並捨棄 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="b66fb-241">During the clean-up, all of the related Azure Blob data and folders are removed, and the Hive table is dropped.</span></span> <span data-ttu-id="b66fb-242">您也可以從範例命令列叫用清理程序。</span><span class="sxs-lookup"><span data-stu-id="b66fb-242">You can also invoke the clean-up procedure from the sample command line.</span></span>

<span data-ttu-id="b66fb-243">範例有下列先決條件：</span><span class="sxs-lookup"><span data-stu-id="b66fb-243">The sample has the following prerequisites:</span></span>

* <span data-ttu-id="b66fb-244">使用中 Microsoft Azure 訂用帳戶和其訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="b66fb-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="b66fb-245">具有對應私密金鑰之訂用帳戶的管理憑證。</span><span class="sxs-lookup"><span data-stu-id="b66fb-245">A management certificate for the subscription with the corresponding private key.</span></span> <span data-ttu-id="b66fb-246">憑證應該安裝在用來執行範例之電腦上，目前使用者的私人儲存體中。</span><span class="sxs-lookup"><span data-stu-id="b66fb-246">The certificate should be installed in the current user private storage on the machine used to run the sample.</span></span>
* <span data-ttu-id="b66fb-247">使用中 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b66fb-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="b66fb-248">在先前的必要條件中連結至 HDInsight 叢集的 Azure 儲存體帳戶，以及對應的主要或次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b66fb-248">An Azure Storage account linked to the HDInsight cluster from the previous prerequisite, together with the corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="b66fb-249">執行範例之前，必要條件中的所有資訊均應輸入到範例組態檔案中。</span><span class="sxs-lookup"><span data-stu-id="b66fb-249">All of the information from the prerequisites should be entered to the sample configuration file before the sample is run.</span></span> <span data-ttu-id="b66fb-250">要執行此動作有兩個可行的方式：</span><span class="sxs-lookup"><span data-stu-id="b66fb-250">There are two possible ways to do it:</span></span>

* <span data-ttu-id="b66fb-251">編輯範例根目錄中的 app.config 檔案，然後建置範例</span><span class="sxs-lookup"><span data-stu-id="b66fb-251">Edit the app.config file in the sample root directory and then build the sample</span></span>
* <span data-ttu-id="b66fb-252">先建置範例，然後在組建目錄中編輯 AvroHDISample.exe.config</span><span class="sxs-lookup"><span data-stu-id="b66fb-252">First build the sample, and then edit AvroHDISample.exe.config in the build directory</span></span>

<span data-ttu-id="b66fb-253">在兩個情況下，所有編輯均應該在 **<appSettings>** 設定區段中完成。</span><span class="sxs-lookup"><span data-stu-id="b66fb-253">In both cases, all edits should be done in the **<appSettings>** settings section.</span></span> <span data-ttu-id="b66fb-254">依照檔案中的註解執行。</span><span class="sxs-lookup"><span data-stu-id="b66fb-254">Follow the comments in the file.</span></span>
<span data-ttu-id="b66fb-255">執行下列命令，範例即會從命令列中執行 (其中，具有範例的 .zip 檔案是假設應解壓縮至 C:\AvroHDISample；若沒有，則會使用相關的檔案路徑)：</span><span class="sxs-lookup"><span data-stu-id="b66fb-255">The sample is run from the command line by executing the following command (where the .zip file with the sample was assumed to be extracted to C:\AvroHDISample; if otherwise, use the relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="b66fb-256">若要清理叢集，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b66fb-256">To clean up the cluster, run the following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx

---
title: "Hadoop-Microsoft Avro Library-Azure 中的 aaaSerialize 資料 |Microsoft 文件"
description: "深入了解如何 tooserialize 和還原序列化使用 hello Microsoft Avro Library toopersist toomemory、 資料庫或檔案的 HDInsight 上的 Hadoop 中的資料。"
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
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a><span data-ttu-id="9bdd3-104">序列化 Hadoop 中的資料與 hello Microsoft Avro Library</span><span class="sxs-lookup"><span data-stu-id="9bdd3-104">Serialize data in Hadoop with hello Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="9bdd3-105">microsoft 不再支援 hello Avro SDK。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-105">hello Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="9bdd3-106">支援的開放原始碼社群 hello 程式庫。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-106">hello library is open source community supported.</span></span> <span data-ttu-id="9bdd3-107">hello 程式庫的 hello 來源位於[Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro)。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-107">hello sources for hello library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="9bdd3-108">本主題說明如何 toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize 物件與其他資料結構到資料流 toopersist 它們 toomemory、 資料庫或檔案。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-108">This topic shows how toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objects and other data structures into streams toopersist them toomemory, a database, or a file.</span></span> <span data-ttu-id="9bdd3-109">它也會示範如何 toodeserialize 它們 toorecover hello 原始物件。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-109">It also shows how toodeserialize them toorecover hello original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="9bdd3-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="9bdd3-110">Apache Avro</span></span>
<span data-ttu-id="9bdd3-111">hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a>實作 hello hello Microsoft.NET 環境 Apache Avro 資料序列化系統。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-111">hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements hello Apache Avro data serialization system for hello Microsoft.NET environment.</span></span> <span data-ttu-id="9bdd3-112">Apache Avro 提供一個可用於序列化的壓縮二進位資料交換格式。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="9bdd3-113">它會使用<a href="http://www.json.org" target="_blank">JSON</a> toodefine underwrites 語言互通性語言無從驗證結構描述。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> toodefine a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="9bdd3-114">以某個語言序列化的資料可以使用另一個語言讀取。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="9bdd3-115">目前支援 C、C++、C#、Java、PHP、Python 和 Ruby。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="9bdd3-116">Hello 格式的詳細的資訊位於 hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro 規格</a>。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-116">Detailed information on hello format can be found in hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="9bdd3-117">hello Microsoft Avro Library 不支援此規格的 hello 遠端程序呼叫 (Rpc) 的一部分。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-117">hello Microsoft Avro Library does not support hello remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="9bdd3-118">hello 序列化表示 hello Avro 系統中的物件會包含兩個部分： 結構描述和實際值。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-118">hello serialized representation of an object in hello Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="9bdd3-119">hello Avro 結構描述會描述 hello 的 hello 序列化 JSON 資料的語言無關的資料模型。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-119">hello Avro schema describes hello language-independent data model of hello serialized data with JSON.</span></span> <span data-ttu-id="9bdd3-120">它會與資料的二進位表示並存。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="9bdd3-121">具有 hello 分開 hello 二進位表示法的結構描述允許使用沒有每個值的額外費用，讓序列化快速、 以及 hello 表示小撰寫每個物件 toobe。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-121">Having hello schema separate from hello binary representation permits each object toobe written with no per-value overheads, making serialization fast, and hello representation small.</span></span>

## <a name="hello-hadoop-scenario"></a><span data-ttu-id="9bdd3-122">hello Hadoop 案例</span><span class="sxs-lookup"><span data-stu-id="9bdd3-122">hello Hadoop scenario</span></span>
<span data-ttu-id="9bdd3-123">Azure HDInsight 和其他 Apache Hadoop 的環境中廣泛使用 hello Apache Avro 序列化格式。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-123">hello Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="9bdd3-124">Avro 提供便利的方式 toorepresent Hadoop MapReduce 工作內的複雜資料結構。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-124">Avro provides a convenient way toorepresent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="9bdd3-125">hello 格式 Avro 檔案 （Avro 物件容器檔案） 的已設計的 toosupport hello 分散式 MapReduce 程式撰寫模型。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-125">hello format of Avro files (Avro object container file) has been designed toosupport hello distributed MapReduce programming model.</span></span> <span data-ttu-id="9bdd3-126">hello 啟用 hello 散發的重要功能是 「 可分割的圖形 「 hello 任一個可搜尋檔案中的任何點和從特定的區塊開始讀取 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-126">hello key feature that enables hello distribution is that hello files are “splittable” in hello sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="9bdd3-127">Avro Library 中的序列化</span><span class="sxs-lookup"><span data-stu-id="9bdd3-127">Serialization in Avro Library</span></span>
<span data-ttu-id="9bdd3-128">hello Avro.NET 程式庫支援序列化物件的兩種的方式：</span><span class="sxs-lookup"><span data-stu-id="9bdd3-128">hello .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="9bdd3-129">**反映**-hello hello 類型的 JSON 結構描述會自動建置 hello 資料中的 hello.NET 型別 toobe 序列化合約屬性。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-129">**reflection** - hello JSON schema for hello types is automatically built from hello data contract attributes of hello .NET types toobe serialized.</span></span>
* <span data-ttu-id="9bdd3-130">**泛型記錄**-由 hello 記錄中明確指定 JSON 結構描述[ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx)類別沒有.NET 型別時存在 hello 資料 toobe 的 toodescribe hello 結構描述序列化。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-130">**generic record** - A JSON schema is explicitly specified in a record represented by hello [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present toodescribe hello schema for hello data toobe serialized.</span></span>

<span data-ttu-id="9bdd3-131">當 tooboth hello 寫入器 」 和 「 hello 資料流的讀取器知道 hello 資料結構描述時，可以傳送 hello 資料，不會其結構描述。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-131">When hello data schema is known tooboth hello writer and reader of hello stream, hello data can be sent without its schema.</span></span> <span data-ttu-id="9bdd3-132">在案例中使用 Avro 物件容器檔案時，hello 結構描述儲存在 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-132">In cases when an Avro object container file is used, hello schema is stored within hello file.</span></span> <span data-ttu-id="9bdd3-133">可以指定其他參數，例如使用資料壓縮的 hello 轉碼器。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-133">Other parameters, such as hello codec used for data compression, can be specified.</span></span> <span data-ttu-id="9bdd3-134">這些案例的更多詳細資料中所述，而且 hello 下列程式碼範例所示：</span><span class="sxs-lookup"><span data-stu-id="9bdd3-134">These scenarios are outlined in more detail and illustrated in hello following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="9bdd3-135">安裝 Avro Library</span><span class="sxs-lookup"><span data-stu-id="9bdd3-135">Install Avro Library</span></span>
<span data-ttu-id="9bdd3-136">hello 下列是必要的然後再安裝 hello 程式庫：</span><span class="sxs-lookup"><span data-stu-id="9bdd3-136">hello following are required before you install hello library:</span></span>

* <span data-ttu-id="9bdd3-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="9bdd3-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="9bdd3-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="9bdd3-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="9bdd3-139">請注意該 hello Newtonsoft.Json.dll 相依性會自動下載 hello Microsoft Avro Library hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-139">Note that hello Newtonsoft.Json.dll dependency is downloaded automatically with hello installation of hello Microsoft Avro Library.</span></span> <span data-ttu-id="9bdd3-140">hello 程序提供的下列區段的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bdd3-140">hello procedure is provided in hello following section:</span></span>

<span data-ttu-id="9bdd3-141">以 NuGet 套件，可透過下列程序的 hello 安裝從 Visual Studio 發佈 hello Microsoft Avro Library:</span><span class="sxs-lookup"><span data-stu-id="9bdd3-141">hello Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via hello following procedure:</span></span>

1. <span data-ttu-id="9bdd3-142">選取 hello**專案** 索引標籤-> **管理 NuGet 封裝...**</span><span class="sxs-lookup"><span data-stu-id="9bdd3-142">Select hello **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="9bdd3-143">Hello 中的搜尋 「 Microsoft.Hadoop.Avro"**線上搜尋**方塊。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-143">Search for "Microsoft.Hadoop.Avro" in hello **Search Online** box.</span></span>
3. <span data-ttu-id="9bdd3-144">按一下 hello**安裝**太下一步按鈕**Microsoft Azure HDInsight Avro Library**。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-144">Click hello **Install** button next too**Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="9bdd3-145">請注意該 hello Newtonsoft.Json.dll (> = 6.0.4) 相依性也會自動下載以 hello Microsoft Avro Library。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-145">Note that hello Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with hello Microsoft Avro Library.</span></span>

<span data-ttu-id="9bdd3-146">hello Microsoft Avro Library 原始程式碼位於[Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro)。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-146">hello Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="9bdd3-147">使用 Avro Library 來編譯結構描述</span><span class="sxs-lookup"><span data-stu-id="9bdd3-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="9bdd3-148">hello Microsoft Avro Library 包含公用程式，讓建立 C# 類型會自動根據 hello 先前定義的 JSON 結構描述產生程式碼。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-148">hello Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on hello previously defined JSON schema.</span></span> <span data-ttu-id="9bdd3-149">hello 程式碼產生公用程式可執行檔的二進位檔分散，但是可以透過下列程序的 hello 使用者輕鬆建立：</span><span class="sxs-lookup"><span data-stu-id="9bdd3-149">hello code generation utility is not distributed as a binary executable, but can be easily built via hello following procedure:</span></span>

1. <span data-ttu-id="9bdd3-150">下載 HDInsight SDK 中的原始程式碼 hello 最新版本的 hello.zip 檔案<a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft.NET SDK 的 Hadoop</a>。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-150">Download hello .zip file with hello latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="9bdd3-151">(按一下 hello**下載**圖示，不 hello**下載** 索引標籤。)</span><span class="sxs-lookup"><span data-stu-id="9bdd3-151">(Click hello **Download** icon, not hello **Downloads** tab.)</span></span>
2. <span data-ttu-id="9bdd3-152">擷取的 hello HDInsight SDK tooa 目錄 hello 與.NET Framework 4 的電腦上安裝和 toohello 網際網路連線下載必要的依存性 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-152">Extract hello HDInsight SDK tooa directory on hello machine with .NET Framework 4 installed and connected toohello Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="9bdd3-153">以下，我們假設 hello 原始程式碼擷取的 tooC:\SDK。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-153">Below, we assume that hello source code is extracted tooC:\SDK.</span></span>
3. <span data-ttu-id="9bdd3-154">移 toohello 資料夾 C:\SDK\src\Microsoft.Hadoop.Avro.Tools 並執行 build.bat。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-154">Go toohello folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="9bdd3-155">（hello 檔案呼叫 MSBuild 從 hello 32 位元發佈的 hello.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-155">(hello file calls MSBuild from hello 32-bit distribution of hello .NET Framework.</span></span> <span data-ttu-id="9bdd3-156">如果您想要 toouse hello 64 位元版本中，編輯 build.bat 下列 hello hello 檔案內的註解。)確保 hello 建置成功完成。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-156">If you would like toouse hello 64-bit version, edit build.bat, following hello comments inside hello file.) Ensure that hello build is successful.</span></span> <span data-ttu-id="9bdd3-157">(在某些系統上，MSBuild 可能會產生警告。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="9bdd3-158">這些警告不會影響 hello 公用程式，只要不有任何建置錯誤。）</span><span class="sxs-lookup"><span data-stu-id="9bdd3-158">These warnings do not affect hello utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="9bdd3-159">hello 編譯公用程式位於 C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-159">hello compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="9bdd3-160">tooget 熟悉 hello 命令列語法中，執行 hello hello hello 程式碼產生公用程式所在的資料夾中的下列命令：`Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="9bdd3-160">tooget familiar with hello command-line syntax, execute hello following command from hello folder where hello code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="9bdd3-161">tootest hello 公用程式，您可以從 hello 範例 JSON 結構描述檔案隨附 hello 原始程式碼產生 C# 類別。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-161">tootest hello utility, you can generate C# classes from hello sample JSON schema file provided with hello source code.</span></span> <span data-ttu-id="9bdd3-162">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bdd3-162">Execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="9bdd3-163">這應該 tooproduce 兩個 C# 檔案 hello 目前目錄中： SensorData.cs 和 Location.cs。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-163">This is supposed tooproduce two C# files in hello current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="9bdd3-164">toounderstand hello 邏輯 hello 程式碼產生公用程式所使用時轉換 hello JSON 結構描述 tooC # 型別，請參閱 GenerationVerification.feature 位於 C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-164">toounderstand hello logic that hello code generation utility is using while converting hello JSON schema tooC# types, see hello file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="9bdd3-165">命名空間會擷取從 hello JSON 結構描述，使用 hello 邏輯 hello 前段中所述的 hello 檔案中所述。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-165">Namespaces are extracted from hello JSON schema, using hello logic described in hello file mentioned in hello previous paragraph.</span></span> <span data-ttu-id="9bdd3-166">擷取從 hello 結構描述的命名空間會優先於任何隨附 hello 公用程式命令列中的 hello /n 參數。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-166">Namespaces extracted from hello schema take precedence over whatever is provided with hello /n parameter in hello utility command line.</span></span> <span data-ttu-id="9bdd3-167">如果您想 hello 結構描述中包含的 toooverride hello 命名空間，請使用 hello /nf 參數。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-167">If you want toooverride hello namespaces contained within hello schema, use hello /nf parameter.</span></span> <span data-ttu-id="9bdd3-168">例如，toochange hello SampleJSONSchema.avsc toomy.own.nspace 的所有命名空間執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="9bdd3-168">For example, toochange all namespaces from hello SampleJSONSchema.avsc toomy.own.nspace, execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a><span data-ttu-id="9bdd3-169">有關 hello 範例</span><span class="sxs-lookup"><span data-stu-id="9bdd3-169">About hello samples</span></span>
<span data-ttu-id="9bdd3-170">本主題提供的六個範例說明不同 hello Microsoft Avro Library 所支援的案例。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-170">Six examples provided in this topic illustrate different scenarios supported by hello Microsoft Avro Library.</span></span> <span data-ttu-id="9bdd3-171">hello Microsoft Avro Library 是設計的 toowork 與任何資料流。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-171">hello Microsoft Avro Library is designed toowork with any stream.</span></span> <span data-ttu-id="9bdd3-172">為了方便一致起見，這些範例會透過記憶體資料流，而不是檔案資料流或資料庫。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="9bdd3-173">在實際執行環境中所採取的 hello 方法，取決於 hello 確切情況的需求、 資料來源和磁碟區、 效能限制，以及其他因素。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-173">hello approach taken in a production environment depends on hello exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="9bdd3-174">hello 第兩個範例顯示如何 tooserialize 和記憶體資料流緩衝區的資料序列化使用反映和泛用記錄。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-174">hello first two examples show how tooserialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="9bdd3-175">hello 結構描述兩種情況中的會假設 toobe hello 讀取器和寫入器之間共用的頻外。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-175">hello schema in these two cases is assumed toobe shared between hello readers and writers out-of-band.</span></span>

<span data-ttu-id="9bdd3-176">hello 第三個和第四個範例顯示如何 tooserialize 和還原序列化資料，藉由使用 hello Avro 物件容器檔案。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-176">hello third and fourth examples show how tooserialize and deserialize data by using hello Avro object container files.</span></span> <span data-ttu-id="9bdd3-177">當資料儲存在 Avro 容器檔案中時，會一律儲存其結構描述與其因為 hello 結構描述必須共用的還原序列化。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-177">When data is stored in an Avro container file, its schema is always stored with it because hello schema must be shared for deserialization.</span></span>

<span data-ttu-id="9bdd3-178">hello 範例包含 hello 前四個範例可從 hello 下載<a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure 程式碼範例</a>站台。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-178">hello sample containing hello first four examples can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="9bdd3-179">hello 第五個範例會示範如何自訂壓縮轉碼器的 Avro toouse 物件容器檔案。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-179">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="9bdd3-180">您可以從 hello 下載這個範例包含 hello 程式碼範例<a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure 程式碼範例</a>站台。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-180">A sample containing hello code for this example can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="9bdd3-181">hello 第六個範例顯示如何 toouse Avro 序列化 tooupload 資料 tooAzure Blob 儲存體，然後使用 Hive (Hadoop) HDInsight 叢集與分析。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-181">hello sixth sample shows how toouse Avro serialization tooupload data tooAzure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="9bdd3-182">它可以從 hello 下載<a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure 程式碼範例</a>站台。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-182">It can be downloaded from hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="9bdd3-183">以下是連結 toohello hello 主題所述的六個範例：</span><span class="sxs-lookup"><span data-stu-id="9bdd3-183">Here are links toohello six samples discussed in hello topic:</span></span>

* <span data-ttu-id="9bdd3-184"><a href="#Scenario1">**使用反映的序列化**</a> -hello 類型 toobe 序列化的 JSON 結構描述會自動建置 hello 資料合約屬性。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-184"><a href="#Scenario1">**Serialization with reflection**</a> - hello JSON schema for types toobe serialized is automatically built from hello data contract attributes.</span></span>
* <span data-ttu-id="9bdd3-185"><a href="#Scenario2">**與泛型記錄序列化**</a> -可供反映任何.NET 型別時，在記錄中明確指定 hello JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-185"><a href="#Scenario2">**Serialization with generic record**</a> - hello JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="9bdd3-186"><a href="#Scenario3">**使用物件容器的檔案，使用反映的序列化**</a> -hello JSON 結構描述會自動建立並共用以及透過 Avro 物件容器檔 hello 序列化資料。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - hello JSON schema is automatically built and shared together with hello serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="9bdd3-187"><a href="#Scenario4">**序列化物件容器檔案使用一般記錄**</a> -hello JSON 結構描述會明確地指定 hello 序列化之前並搭配 hello 資料透過 Avro 物件容器的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - hello JSON schema is explicitly specified before hello serialization and shared together with hello data via an Avro object container file.</span></span>
* <span data-ttu-id="9bdd3-188"><a href="#Scenario5">**序列化使用的自訂壓縮轉碼器的物件容器檔案**</a> -hello 範例將示範如何 toocreate Avro 物件具有自訂.NET 實作的 hello Deflate 資料壓縮轉碼器容器檔案。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - hello example shows how toocreate an Avro object container file with a customized .NET implementation of hello Deflate data compression codec.</span></span>
* <span data-ttu-id="9bdd3-189"><a href="#Scenario6">**使用 Avro tooupload 資料的 Microsoft Azure HDInsight 服務的 hello** </a> -hello 範例說明 Avro 序列化與 hello HDInsight 服務的互動方式。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-189"><a href="#Scenario6">**Using Avro tooupload data for hello Microsoft Azure HDInsight service**</a> - hello example illustrates how Avro serialization interacts with hello HDInsight service.</span></span> <span data-ttu-id="9bdd3-190">使用中 Azure 訂用帳戶和存取 tooan Azure HDInsight 叢集需要 toorun 這個範例。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-190">An active Azure subscription and access tooan Azure HDInsight cluster are required toorun this example.</span></span>

## <span data-ttu-id="9bdd3-191"><a name="Scenario1"></a>範例 1：使用反映進行序列化</span><span class="sxs-lookup"><span data-stu-id="9bdd3-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="9bdd3-192">hello hello 類型的 JSON 結構描述會自動由建置 hello Microsoft Avro Library 透過反映來從 hello 資料合約的 hello C# 物件 toobe 序列化的屬性。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-192">hello JSON schema for hello types can be automatically built by hello Microsoft Avro Library via reflection from hello data contract attributes of hello C# objects toobe serialized.</span></span> <span data-ttu-id="9bdd3-193">hello Microsoft Avro Library 建立[ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello 欄位 toobe 序列化。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-193">hello Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello fields toobe serialized.</span></span>

<span data-ttu-id="9bdd3-194">在此範例中，物件 ( **SensorData**類別成員**位置**結構) 是序列化的 tooa 記憶體資料流，並接著會還原序列化此資料流。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized tooa memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="9bdd3-195">hello 結果是，則比較的 toohello 初始執行個體 tooconfirm 該 hello **SensorData**物件復原為原始的相同 toohello。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-195">hello result is then compared toohello initial instance tooconfirm that hello **SensorData** object recovered is identical toohello original.</span></span>

<span data-ttu-id="9bdd3-196">在此範例中的 hello 結構描述會假設 toobe 共用之間 hello 讀取器和寫入器，因此不需要 hello Avro 物件的容器格式。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-196">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="9bdd3-197">如需如何 tooserialize 和還原序列化資料到記憶體緩衝區 hello 結構描述必須共用 hello 資料時，使用反映來與 hello 物件容器格式，請參閱<a href="#Scenario3">序列化使用反映物件容器的檔案</a>.</span><span class="sxs-lookup"><span data-stu-id="9bdd3-197">For an example of how tooserialize and deserialize data into memory buffers by using reflection with hello object container format when hello schema must be shared with hello data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

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
        //hello usage of Microsoft Avro Library
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

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
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

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="9bdd3-198">範例 2：使用一般記錄進行序列化</span><span class="sxs-lookup"><span data-stu-id="9bdd3-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="9bdd3-199">無法使用反映，因為無法 hello 資料表示透過.NET 類別，具有資料合約時，JSON 結構描述，可以明確指定泛型記錄中。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because hello data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="9bdd3-200">此方法較使用反映來得慢。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-200">This method is slower than using reflection.</span></span> <span data-ttu-id="9bdd3-201">在這種情況下，hello hello 資料的結構描述也可能是動態的也就是在編譯時期未知。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-201">In such cases, hello schema for hello data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="9bdd3-202">資料表示為逗號分隔值 (CSV) 檔案的結構描述才會知道它會轉換 toohello Avro 格式，在執行階段是這類動態案例的範例。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed toohello Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="9bdd3-203">這個範例會示範如何 toocreate 並用[ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly 方式指定 JSON 結構描述，toopopulate 它與 hello 資料，然後如何 tooserialize 加以還原序列化。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-203">This example shows how toocreate and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly specify a JSON schema, how toopopulate it with hello data, and then how tooserialize and deserialize it.</span></span> <span data-ttu-id="9bdd3-204">然後比較結果 hello toohello hello 復原記錄的初始執行個體 tooconfirm 是相同的原始 toohello。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-204">hello result is then compared toohello initial instance tooconfirm that hello record recovered is identical toohello original.</span></span>

<span data-ttu-id="9bdd3-205">在此範例中的 hello 結構描述會假設 toobe 共用之間 hello 讀取器和寫入器，因此不需要 hello Avro 物件的容器格式。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-205">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="9bdd3-206">如需如何 tooserialize 和還原序列化資料到記憶體緩衝區 hello 結構描述必須是包含 hello 序列化資料時，使用泛型的記錄與 hello 物件容器格式，請參閱 hello<a href="#Scenario4">使用物件容器的序列化檔案與泛用記錄</a>範例。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-206">For an example of how tooserialize and deserialize data into memory buffers by using a generic record with hello object container format when hello schema must be included with hello serialized data, see hello <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

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
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
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

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
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

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="9bdd3-207">範例 3：使用物件容器檔案進行序列化和使用反映進行序列化</span><span class="sxs-lookup"><span data-stu-id="9bdd3-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="9bdd3-208">這個範例是類似的 toohello 案例在 hello<a href="#Scenario1">第一個範例</a>，隱含地使用反映指定 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-208">This example is similar toohello scenario in hello <a href="#Scenario1"> first example</a>, where hello schema is implicitly specified with reflection.</span></span> <span data-ttu-id="9bdd3-209">hello 差異是，在這裡，hello 結構描述不會被 toobe 已知 toohello 讀取器將它還原序列化。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-209">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span> <span data-ttu-id="9bdd3-210">hello **SensorData**序列化的物件 toobe 和其隱含指定的結構描述會儲存在由 hello Avro 物件容器檔案[ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-210">hello **SensorData** objects toobe serialized and their implicitly specified schema are stored in an Avro object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="9bdd3-211">這個範例中序列化的 hello 資料[ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx)及使用已還原序列化[ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="9bdd3-211">hello data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="9bdd3-212">hello 結果則是比較的 toohello 初始執行個體 tooensure 身分識別。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-212">hello result then is compared toohello initial instances tooensure identity.</span></span>

<span data-ttu-id="9bdd3-213">hello hello 中的資料物件透過 hello 預設會壓縮容器檔[ **Deflate** ] [ deflate-100]壓縮轉碼器，從.NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-213">hello data in hello object container file is compressed via hello default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="9bdd3-214">請參閱 hello<a href="#Scenario5">第五個範例</a>在這個主題 toolearn 如何 toouse 最新且更好的版的 hello [ **Deflate** ] [ deflate-110]壓縮.NET Framework 4.5 中可用的轉碼器。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-214">See hello <a href="#Scenario5"> fifth example</a> in this topic toolearn how toouse a more recent and superior version of hello [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

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
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
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

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
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

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
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

                //Delete hello file
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

            //Saving memory stream tooa new file with hello given path
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
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
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

            //Reading a file content by using hello given path tooa memory stream
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
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
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
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
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

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="9bdd3-215">範例 4：使用物件容器檔案進行序列化和使用一般記錄進行序列化</span><span class="sxs-lookup"><span data-stu-id="9bdd3-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="9bdd3-216">這個範例是類似的 toohello 案例在 hello<a href="#Scenario2">第二個範例</a>，明確地使用 JSON 指定 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-216">This example is similar toohello scenario in hello <a href="#Scenario2"> second example</a>, where hello schema is explicitly specified with JSON.</span></span> <span data-ttu-id="9bdd3-217">hello 差異是，在這裡，hello 結構描述不會被 toobe 已知 toohello 讀取器將它還原序列化。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-217">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span>

<span data-ttu-id="9bdd3-218">hello 測試收集的資料集是一份到[ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx)透過明確定義的 JSON 結構描述物件，然後儲存在 hello 所代表的物件容器檔案[ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-218">hello test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="9bdd3-219">此容器檔案建立的寫入器是使用的 tooserialize hello 資料，未壓縮，然後儲存檔案 tooa tooa 記憶體資料流。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-219">This container file creates a writer that is used tooserialize hello data, uncompressed, tooa memory stream that is then saved tooa file.</span></span> <span data-ttu-id="9bdd3-220">hello [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx)建立 hello 讀取器時所使用的參數會指定，這項資料不會壓縮。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-220">hello [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating hello reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="9bdd3-221">hello 資料是從 hello 檔案讀取，然後還原序列化為物件的集合。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-221">hello data is then read from hello file and deserialized into a collection of objects.</span></span> <span data-ttu-id="9bdd3-222">這個集合是比較的 toohello 最初 Avro 記錄 tooconfirm 它們完全相同的清單。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-222">This collection is compared toohello initial list of Avro records tooconfirm that they are identical.</span></span>

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
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
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

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
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

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
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

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
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

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
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
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
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

            //Reading a file content by using hello given path tooa memory stream
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
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
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
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
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

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="9bdd3-223">範例 5：使用物件容器檔案和自訂壓縮轉碼器進行序列化</span><span class="sxs-lookup"><span data-stu-id="9bdd3-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="9bdd3-224">hello 第五個範例會示範如何自訂壓縮轉碼器的 Avro toouse 物件容器檔案。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-224">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="9bdd3-225">您可以從 hello 下載這個範例包含 hello 程式碼範例[Azure 程式碼範例](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111)站台。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-225">A sample containing hello code for this example can be downloaded from hello [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="9bdd3-226">hello [Avro 規格](http://avro.apache.org/docs/current/spec.html#Required+Codecs)允許選擇性壓縮轉碼器的使用方式 (除了太**Null**和**Deflate**預設值)。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-226">hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition too**Null** and **Deflate** defaults).</span></span> <span data-ttu-id="9bdd3-227">此範例中不會實作新的轉碼器，例如 Snappy (提及是支援的選擇性轉碼器在 hello [Avro 規格](http://avro.apache.org/docs/current/spec.html#snappy))。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="9bdd3-228">它會顯示如何 toouse hello hello 的.NET Framework 4.5 實作[ **Deflate** ] [ deflate-110]轉碼器，提供更好的壓縮演算法，根據 hello [zlib](http://zlib.net/) hello 預設.NET Framework 4 版本比壓縮程式庫。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-228">It shows how toouse hello .NET Framework 4.5 implementation of hello [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on hello [zlib](http://zlib.net/) compression library than hello default .NET Framework 4 version.</span></span>

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
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
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

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
        //Define hello actual codec class containing hello required methods for manipulating streams:
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
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
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
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
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

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
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

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
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

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
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
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
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

            //Reading file content by using hello given path tooa memory stream
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
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
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
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
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

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a><span data-ttu-id="9bdd3-229">範例 6： 使用 Avro tooupload 資料 hello Microsoft Azure HDInsight 服務</span><span class="sxs-lookup"><span data-stu-id="9bdd3-229">Sample 6: Using Avro tooupload data for hello Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="9bdd3-230">hello 第六個範例將說明一些程式設計技術相關的 toointeracting 與 hello Azure HDInsight 服務。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-230">hello sixth example illustrates some programming techniques related toointeracting with hello Azure HDInsight service.</span></span> <span data-ttu-id="9bdd3-231">您可以從 hello 下載這個範例包含 hello 程式碼範例[Azure 程式碼範例](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3)站台。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-231">A sample containing hello code for this example can be downloaded from hello [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="9bdd3-232">hello 範例並未 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="9bdd3-232">hello sample does hello following tasks:</span></span>

* <span data-ttu-id="9bdd3-233">連接 tooan 現有 HDInsight 服務叢集。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-233">Connects tooan existing HDInsight service cluster.</span></span>
* <span data-ttu-id="9bdd3-234">將序列化多個 CSV 檔案，並上傳 hello 結果 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-234">Serializes several CSV files and uploads hello result tooAzure Blob storage.</span></span> <span data-ttu-id="9bdd3-235">(hello CSV 檔案與 hello 範例一起散發，而且代表擷取自 AMEX 股票的歷程記錄資料散佈[Infochimps](http://www.infochimps.com/) hello 期間從 1970年-2010年。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-235">(hello CSV files are distributed together with hello sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for hello period 1970-2010.</span></span> <span data-ttu-id="9bdd3-236">hello 範例讀取 CSV 檔案資料、 將 hello 的 hello 記錄 tooinstances**股票**類別，並再將它們序列化使用反映。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-236">hello sample reads CSV file data, converts hello records tooinstances of hello **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="9bdd3-237">內建型別定義會建立從透過 hello Microsoft Avro Library 程式碼產生公用程式的 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-237">Stock type definition is created from a JSON schema via hello Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="9bdd3-238">建立新的外部資料表稱為**股票**登錄區，並將它連結 toohello 資料 hello 上一個步驟中上傳。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-238">Creates a new external table called **Stocks** in Hive, and links it toohello data uploaded in hello previous step.</span></span>
* <span data-ttu-id="9bdd3-239">執行查詢，透過使用 Hive hello**股票**資料表。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-239">Executes a query by using Hive over hello **Stocks** table.</span></span>

<span data-ttu-id="9bdd3-240">此外，hello 範例會執行清除程序之前和之後執行主要的作業。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-240">In addition, hello sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="9bdd3-241">Hello 清除工作期間 hello 的所有相關的 Azure Blob 資料和資料夾會遭到移除，並卸除 hello Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-241">During hello clean-up, all of hello related Azure Blob data and folders are removed, and hello Hive table is dropped.</span></span> <span data-ttu-id="9bdd3-242">您也可以叫用 hello hello 範例命令列清除程序。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-242">You can also invoke hello clean-up procedure from hello sample command line.</span></span>

<span data-ttu-id="9bdd3-243">hello 範例具有 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="9bdd3-243">hello sample has hello following prerequisites:</span></span>

* <span data-ttu-id="9bdd3-244">使用中 Microsoft Azure 訂用帳戶和其訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="9bdd3-245">Hello 相對應的私密金鑰與 hello 訂用帳戶管理憑證。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-245">A management certificate for hello subscription with hello corresponding private key.</span></span> <span data-ttu-id="9bdd3-246">hello 憑證應該安裝在 hello 目前使用者私人儲存體上 hello 使用機器 toorun hello 範例。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-246">hello certificate should be installed in hello current user private storage on hello machine used toorun hello sample.</span></span>
* <span data-ttu-id="9bdd3-247">使用中 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="9bdd3-248">Azure 儲存體帳戶連結從 hello 前一個必要元件，連同 hello 對應的主要或次要存取金鑰 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-248">An Azure Storage account linked toohello HDInsight cluster from hello previous prerequisite, together with hello corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="9bdd3-249">Hello 範例在開始執行前，所有 hello hello 必要條件應該是資訊的輸入的 toohello 範例組態檔。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-249">All of hello information from hello prerequisites should be entered toohello sample configuration file before hello sample is run.</span></span> <span data-ttu-id="9bdd3-250">有兩個可能的方式 toodo 它：</span><span class="sxs-lookup"><span data-stu-id="9bdd3-250">There are two possible ways toodo it:</span></span>

* <span data-ttu-id="9bdd3-251">編輯 hello 範例的根目錄中的 hello app.config 檔案，並再建立 hello 範例</span><span class="sxs-lookup"><span data-stu-id="9bdd3-251">Edit hello app.config file in hello sample root directory and then build hello sample</span></span>
* <span data-ttu-id="9bdd3-252">第一次建置 hello 範例，然後編輯在 hello 組建目錄中的 AvroHDISample.exe.config</span><span class="sxs-lookup"><span data-stu-id="9bdd3-252">First build hello sample, and then edit AvroHDISample.exe.config in hello build directory</span></span>

<span data-ttu-id="9bdd3-253">在這兩種情況下，所有的編輯作業應該在 hello  **<appSettings>** 設定 區段。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-253">In both cases, all edits should be done in hello **<appSettings>** settings section.</span></span> <span data-ttu-id="9bdd3-254">遵循 hello hello 檔案中的註解。</span><span class="sxs-lookup"><span data-stu-id="9bdd3-254">Follow hello comments in hello file.</span></span>
<span data-ttu-id="9bdd3-255">hello 執行範例時從 hello 命令列執行下列命令 （其中 hello.zip 檔案，與 hello 範例假設已解壓縮的 toobe tooC:\AvroHDISample; 若否則使用 hello 相關檔案路徑） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bdd3-255">hello sample is run from hello command line by executing hello following command (where hello .zip file with hello sample was assumed toobe extracted tooC:\AvroHDISample; if otherwise, use hello relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="9bdd3-256">tooclean 向上 hello 叢集，請執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bdd3-256">tooclean up hello cluster, run hello following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx

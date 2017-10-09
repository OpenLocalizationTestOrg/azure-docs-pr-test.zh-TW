---
title: "aaaAnalyze 和程序的 JSON 文件在 HDInsight 的 Hive |Microsoft 文件"
description: "了解 toouse JSON 文件，並加以分析使用 HDInsight 中的登錄區。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2017
ms.author: jgao
ms.openlocfilehash: b4b20172e8553f91a446615dc52f2ea2ef24cd04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="6186b-103">使用 HDInsight 中的 Hive 處理並分析 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="6186b-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="6186b-104">深入了解如何 tooprocess 和分析 JSON 檔案使用 HDInsight 中的登錄區。</span><span class="sxs-lookup"><span data-stu-id="6186b-104">Learn how tooprocess and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="6186b-105">hello 教學課程中，會使用下列 JSON 文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="6186b-105">hello following JSON document is used in hello tutorial:</span></span>

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

<span data-ttu-id="6186b-106">hello 檔案，請參閱wasb://processjson@hditutorialdata.blob.core.windows.net/。</span><span class="sxs-lookup"><span data-stu-id="6186b-106">hello file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="6186b-107">如需關於搭配 HDInsight 使用 Azure Blob 儲存體的詳細資訊，請參閱[在 HDInsight 上搭配 Hadoop 使用 HDFS 相容的 Azure Blob 儲存體](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="6186b-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="6186b-108">您可以複製您的叢集的 hello 檔案 toohello 預設容器。</span><span class="sxs-lookup"><span data-stu-id="6186b-108">You can copy hello file toohello default container of your cluster.</span></span>

<span data-ttu-id="6186b-109">在本教學課程中，您可以使用 hello Hive 主控台。</span><span class="sxs-lookup"><span data-stu-id="6186b-109">In this tutorial, you use hello Hive console.</span></span>  <span data-ttu-id="6186b-110">開啟 hello Hive 主控台的指示，請參閱[的上具有遠端桌面 HDInsight Hadoop Hive 使用](hdinsight-hadoop-use-hive-remote-desktop.md)。</span><span class="sxs-lookup"><span data-stu-id="6186b-110">For instructions of opening hello Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="6186b-111">簡維 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="6186b-111">Flatten JSON documents</span></span>
<span data-ttu-id="6186b-112">hello 下一節中所列的 hello 方法需要單一資料列中的 hello JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="6186b-112">hello methods listed in hello next section require hello JSON document in a single row.</span></span> <span data-ttu-id="6186b-113">因此，您必須扁平化 hello JSON 文件 tooa 字串。</span><span class="sxs-lookup"><span data-stu-id="6186b-113">So you must flatten hello JSON document tooa string.</span></span> <span data-ttu-id="6186b-114">如果已扁平化 JSON 文件，可以略過此步驟，並繼續分析 JSON 資料直線 toohello 下一節。</span><span class="sxs-lookup"><span data-stu-id="6186b-114">If your JSON document is already flattened, you can skip this step and go straight toohello next section on Analyzing JSON data.</span></span>

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

<span data-ttu-id="6186b-115">hello 未經處理的 JSON 檔案是位於 **wasb://processjson@hditutorialdata.blob.core.windows.net/** 。</span><span class="sxs-lookup"><span data-stu-id="6186b-115">hello raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="6186b-116">hello *StudentsRaw* Hive 資料表點 toohello 原始非扁平化的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="6186b-116">hello *StudentsRaw* Hive table points toohello raw unflattened JSON document.</span></span>

<span data-ttu-id="6186b-117">hello *StudentsOneLine* Hive 資料表將 hello 資料儲存在 hello HDInsight 預設檔案系統 hello */json/學生/*路徑。</span><span class="sxs-lookup"><span data-stu-id="6186b-117">hello *StudentsOneLine* Hive table stores hello data in hello HDInsight default file system under hello */json/students/* path.</span></span>

<span data-ttu-id="6186b-118">hello INSERT 陳述式會填入 hello StudentOneLine 資料表與 hello 扁平化 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="6186b-118">hello INSERT statement populates hello StudentOneLine table with hello flattened JSON data.</span></span>

<span data-ttu-id="6186b-119">hello SELECT 陳述式應該只傳回一個資料列。</span><span class="sxs-lookup"><span data-stu-id="6186b-119">hello SELECT statement shall only return one row.</span></span>

<span data-ttu-id="6186b-120">以下是 hello hello SELECT 陳述式的輸出：</span><span class="sxs-lookup"><span data-stu-id="6186b-120">Here is hello output of hello SELECT statement:</span></span>

![簡維 hello JSON 文件。][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="6186b-122">在 Hive 中分析 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="6186b-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="6186b-123">Hive 提供三種不同機制 toorun 查詢 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="6186b-123">Hive provides three different mechanisms toorun queries on JSON documents:</span></span>

* <span data-ttu-id="6186b-124">使用 hello GET\_JSON\_物件 UDF （使用者定義函式）</span><span class="sxs-lookup"><span data-stu-id="6186b-124">use hello GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="6186b-125">使用 hello JSON_TUPLE UDF</span><span class="sxs-lookup"><span data-stu-id="6186b-125">use hello JSON_TUPLE UDF</span></span>
* <span data-ttu-id="6186b-126">使用自訂 SerDe</span><span class="sxs-lookup"><span data-stu-id="6186b-126">use custom SerDe</span></span>
* <span data-ttu-id="6186b-127">使用 Python 或其他語言撰寫您自己的 UDF。</span><span class="sxs-lookup"><span data-stu-id="6186b-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="6186b-128">請參閱[這篇文章][hdinsight-python]，了解如何使用 Hive 執行您自己的 Python 程式碼。</span><span class="sxs-lookup"><span data-stu-id="6186b-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-hello-getjsonobject-udf"></a><span data-ttu-id="6186b-129">使用 hello GET\_JSON_OBJECT UDF</span><span class="sxs-lookup"><span data-stu-id="6186b-129">Use hello GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="6186b-130">Hive 提供的內建 UDF 稱為 [get json objec](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object)，可在執行階段期間執行 JSON 查詢。</span><span class="sxs-lookup"><span data-stu-id="6186b-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="6186b-131">這個方法會採用兩個引數 – hello 資料表名稱和方法名稱，其具有 hello 扁平化 JSON 文件和 hello JSON 欄位需要 toobe 剖析。</span><span class="sxs-lookup"><span data-stu-id="6186b-131">This method takes two arguments – hello table name and method name, which has hello flattened JSON document and hello JSON field that needs toobe parsed.</span></span> <span data-ttu-id="6186b-132">讓我們看看此 UDF 的運作方式範例 toosee。</span><span class="sxs-lookup"><span data-stu-id="6186b-132">Let’s look at an example toosee how this UDF works.</span></span>

<span data-ttu-id="6186b-133">取得 hello 名字和每個學生的姓氏</span><span class="sxs-lookup"><span data-stu-id="6186b-133">Get hello first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="6186b-134">在主控台視窗中執行此查詢時，以下是 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="6186b-134">Here is hello output when running this query in console window.</span></span>

![get_json_object UDF][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="6186b-136">有一些限制的 hello get json_object UDF。</span><span class="sxs-lookup"><span data-stu-id="6186b-136">There are a few limitations of hello get-json_object UDF.</span></span>

* <span data-ttu-id="6186b-137">Hello 查詢中的每個欄位需要重新剖析 hello 查詢，因為它會影響 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="6186b-137">Because each field in hello query requires reparsing hello query, it affects hello performance.</span></span>
* <span data-ttu-id="6186b-138">取得\_JSON_OBJECT() 傳回 hello 陣列的字串表示。</span><span class="sxs-lookup"><span data-stu-id="6186b-138">GET\_JSON_OBJECT() returns hello string representation of an array.</span></span> <span data-ttu-id="6186b-139">tooconvert 此陣列 tooa Hive 陣列，您有 toouse 規則運算式 tooreplace hello 方括號 '[' 和']'，然後同時呼叫分割 tooget hello 陣列。</span><span class="sxs-lookup"><span data-stu-id="6186b-139">tooconvert this array tooa Hive array, you have toouse regular expressions tooreplace hello square brackets ‘[‘ and ‘]’ and then also call split tooget hello array.</span></span>

<span data-ttu-id="6186b-140">這就是為什麼 hello Hive wiki 建議使用 json_tuple。</span><span class="sxs-lookup"><span data-stu-id="6186b-140">This is why hello Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-hello-jsontuple-udf"></a><span data-ttu-id="6186b-141">使用 hello JSON_TUPLE UDF</span><span class="sxs-lookup"><span data-stu-id="6186b-141">Use hello JSON_TUPLE UDF</span></span>
<span data-ttu-id="6186b-142">Hive 所提供的另一個 UDF 稱為 [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple)，其效能比 [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) 更高。</span><span class="sxs-lookup"><span data-stu-id="6186b-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="6186b-143">這個方法會採用一組索引鍵和 JSON 字串，並使用一個函式傳回值的 tuple。</span><span class="sxs-lookup"><span data-stu-id="6186b-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="6186b-144">hello 下列查詢會傳回 hello 學生識別碼以及 hello 等級 hello JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="6186b-144">hello following query returns hello student id and hello grade from hello JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="6186b-145">此指令碼 hello Hive 主控台中的 hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="6186b-145">hello output of this script in hello Hive console:</span></span>

![json_tuple UDF][image-hdi-hivejson-jsontuple]

<span data-ttu-id="6186b-147">JSON\_TUPLE 使用 hello[橫向檢視](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView)登錄區，可讓 json 語法\_tuple toocreate 藉由套用 hello UDT 函式 tooeach 資料表的資料列 hello 原始虛擬資料表。</span><span class="sxs-lookup"><span data-stu-id="6186b-147">JSON\_TUPLE uses hello [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple toocreate a virtual table by applying hello UDT function tooeach row of hello original table.</span></span>  <span data-ttu-id="6186b-148">因為重複 hello 變得難以的複雜 Json 使用橫向 檢視。</span><span class="sxs-lookup"><span data-stu-id="6186b-148">Complex JSONs become too unwieldy because of hello repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="6186b-149">此外，JSON_TUPLE 無法處理巢狀 JSON。</span><span class="sxs-lookup"><span data-stu-id="6186b-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="6186b-150">使用自訂 SerDe</span><span class="sxs-lookup"><span data-stu-id="6186b-150">Use custom SerDe</span></span>
<span data-ttu-id="6186b-151">SerDe hello 剖析巢狀的 JSON 文件的最佳選擇，它可讓您 toodefine hello JSON 結構描述，以及使用 hello 結構描述 tooparse hello 文件。</span><span class="sxs-lookup"><span data-stu-id="6186b-151">SerDe is hello best choice for parsing nested JSON documents, it allows you toodefine hello JSON schema, and use hello schema tooparse hello documents.</span></span> <span data-ttu-id="6186b-152">在本教學課程中，您使用下列其中一個 hello 已開發的常見 SerDe[蘇 Congiu](https://github.com/rcongiu)。</span><span class="sxs-lookup"><span data-stu-id="6186b-152">In this tutorial, you use one of hello more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="6186b-153">**toouse hello 自訂 SerDe:**</span><span class="sxs-lookup"><span data-stu-id="6186b-153">**toouse hello custom SerDe:**</span></span>

1. <span data-ttu-id="6186b-154">安裝 [Java SE 開發套件 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR)。</span><span class="sxs-lookup"><span data-stu-id="6186b-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="6186b-155">如果您要使用的 HDInsight hello Windows 部署 toobe，選擇 hello Windows X64 版的 hello JDK</span><span class="sxs-lookup"><span data-stu-id="6186b-155">Choose hello Windows X64 version of hello JDK if you are going toobe using hello Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="6186b-156">JDK 1.8 不適用於此 SerDe。</span><span class="sxs-lookup"><span data-stu-id="6186b-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="6186b-157">Hello 安裝完成之後，加入新的使用者環境變數：</span><span class="sxs-lookup"><span data-stu-id="6186b-157">After hello installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="6186b-158">開啟**檢視進階系統設定**從 Windows 囉 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="6186b-158">Open **View advanced system settings** from hello Windows screen.</span></span>
   2. <span data-ttu-id="6186b-159">按一下 [ **環境變數**]。</span><span class="sxs-lookup"><span data-stu-id="6186b-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="6186b-160">加入新**JAVA_HOME**環境變數指向太**C:\Program Files\Java\jdk1.7.0_55**或 JDK 安裝的任一處。</span><span class="sxs-lookup"><span data-stu-id="6186b-160">Add a new **JAVA_HOME** environment variable is pointing too**C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![為 JDK 設定正確的組態值][image-hdi-hivejson-jdk]
2. <span data-ttu-id="6186b-162">安裝 [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="6186b-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="6186b-163">新增 hello bin 資料夾 tooyour 路徑移 tooControl 面板--> 您帳戶的環境變數的編輯 hello 系統變數。</span><span class="sxs-lookup"><span data-stu-id="6186b-163">Add hello bin folder tooyour path by going tooControl Panel-->Edit hello System Variables for your account Environment variables.</span></span> <span data-ttu-id="6186b-164">hello 下列螢幕擷取畫面顯示您如何 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="6186b-164">hello following screenshot shows you how toodo this.</span></span>
   
    ![設定 Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="6186b-166">從複製 hello 專案[Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github 網站。</span><span class="sxs-lookup"><span data-stu-id="6186b-166">Clone hello project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="6186b-167">您可以按一下 hello"Download Zip 」 按鈕 hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="6186b-167">You can do this by clicking on hello “Download Zip” button as shown in hello following screenshot.</span></span>
   
    ![複製 hello 專案][image-hdi-hivejson-serde]

<span data-ttu-id="6186b-169">4： 您已下載此套件，然後類型 「 mvn 封裝 」 go toohello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="6186b-169">4: Go toohello folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="6186b-170">這應該建立 hello 必要 jar 檔案，然後您可以複製移轉 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="6186b-170">This should create hello necessary jar files that you can then copy over toohello cluster.</span></span>

<span data-ttu-id="6186b-171">5: hello hello 封裝的下載程式的根資料夾下，移至 toohello 目標資料夾。</span><span class="sxs-lookup"><span data-stu-id="6186b-171">5: Go toohello target folder under hello root folder where you downloaded hello package.</span></span> <span data-ttu-id="6186b-172">上傳 hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar 檔案 toohead 位在叢集的節點。</span><span class="sxs-lookup"><span data-stu-id="6186b-172">Upload hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file toohead-node of your cluster.</span></span> <span data-ttu-id="6186b-173">通常 hello hive 二進位資料夾下將： C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin 或類似的項目。</span><span class="sxs-lookup"><span data-stu-id="6186b-173">I usually put it under hello hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="6186b-174">6： 在 hello hive 提示字元中輸入 「 新增 jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar 」。</span><span class="sxs-lookup"><span data-stu-id="6186b-174">6: In hello hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="6186b-175">由於在這個案例中，hello jar hello C:\apps\dist\hive-0.13.x\bin 資料夾中，我可以直接加入 hello jar hello 名稱所示：</span><span class="sxs-lookup"><span data-stu-id="6186b-175">Since in my case, hello jar is in hello C:\apps\dist\hive-0.13.x\bin folder, I can directly add hello jar with hello name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![加入 JAR tooyour 專案][image-hdi-hivejson-addjar]

<span data-ttu-id="6186b-177">現在，您就準備好 toouse hello SerDe toorun 查詢 hello JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="6186b-177">Now, you are ready toouse hello SerDe toorun queries against hello JSON document.</span></span>

<span data-ttu-id="6186b-178">陳述式之後的 hello 會具有定義的結構描述中建立資料表：</span><span class="sxs-lookup"><span data-stu-id="6186b-178">hello following statement creates a table with a defined schema:</span></span>

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

<span data-ttu-id="6186b-179">toolist hello 名字和姓氏 hello 學生</span><span class="sxs-lookup"><span data-stu-id="6186b-179">toolist hello first name and last name of hello student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="6186b-180">以下是從 hello Hive 主控台 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="6186b-180">Here is hello result from hello Hive console.</span></span>

![SerDe 查詢 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="6186b-182">toocalculate hello 加總的 hello JSON 文件的分數</span><span class="sxs-lookup"><span data-stu-id="6186b-182">toocalculate hello sum of scores of hello JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="6186b-183">上述查詢會使用 hello[橫向檢視分裂](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView)UDF tooexpand hello 分數的陣列，以便可以加總。</span><span class="sxs-lookup"><span data-stu-id="6186b-183">hello preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello array of scores so that they can be summed.</span></span>

<span data-ttu-id="6186b-184">以下是 hello hello Hive 主控台輸出。</span><span class="sxs-lookup"><span data-stu-id="6186b-184">Here is hello output from hello Hive console.</span></span>

![SerDe 查詢 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="6186b-186">這會使指定的學生 toofind 具有計分超過 80 點：</span><span class="sxs-lookup"><span data-stu-id="6186b-186">toofind which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="6186b-187">hello 上述查詢會傳回不同於 get Hive 陣列\_json\_物件，傳回的字串。</span><span class="sxs-lookup"><span data-stu-id="6186b-187">hello preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![SerDe 查詢 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="6186b-189">如果您想 tooskil 格式不正確的 JSON，再為說明中的 hello [wiki 頁面](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master)此 SerDe 的一種，輸入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6186b-189">If you want tooskil malformed JSON, then as explained in hello [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing hello following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="6186b-190">摘要</span><span class="sxs-lookup"><span data-stu-id="6186b-190">Summary</span></span>
<span data-ttu-id="6186b-191">結論，您所選擇的登錄區中的 JSON 運算子 hello 類型取決於您的案例。</span><span class="sxs-lookup"><span data-stu-id="6186b-191">In conclusion, hello type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="6186b-192">如果您有簡單的 JSON 文件，因此您上只能有一個欄位 toolook-您可以選擇 toouse hello Hive UDF get\_json\_物件。</span><span class="sxs-lookup"><span data-stu-id="6186b-192">If you have a simple JSON document and you only have one field toolook up on – you can choose toouse hello Hive UDF get\_json\_object.</span></span> <span data-ttu-id="6186b-193">如果您最多有一個以上的索引鍵 toolook 時，您可以使用 json_tuple。</span><span class="sxs-lookup"><span data-stu-id="6186b-193">If you have more than one key toolook up on, then you can use json_tuple.</span></span> <span data-ttu-id="6186b-194">如果您有巢狀文件時，您應該使用 JSON SerDe hello。</span><span class="sxs-lookup"><span data-stu-id="6186b-194">If you have a nested document, then you should use hello JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6186b-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6186b-195">Next steps</span></span>

<span data-ttu-id="6186b-196">如需其他相關文章，請參閱</span><span class="sxs-lookup"><span data-stu-id="6186b-196">For other related articles, see</span></span>

* [<span data-ttu-id="6186b-197">在 HDInsight tooanalyze 範例 Apache log4j 檔案中的 Hadoop 使用 Hive 和 HiveQL</span><span class="sxs-lookup"><span data-stu-id="6186b-197">Use Hive and HiveQL with Hadoop in HDInsight tooanalyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="6186b-198">在 HDInsight 中使用 Hive 分析航班延誤資料</span><span class="sxs-lookup"><span data-stu-id="6186b-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="6186b-199">在 HDInsight 中使用 Hive 分析 Twitter 資料</span><span class="sxs-lookup"><span data-stu-id="6186b-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="6186b-200">使用 Azure Cosmos DB 和 HDInsight 執行 Hadoop 工作</span><span class="sxs-lookup"><span data-stu-id="6186b-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: ./media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png
